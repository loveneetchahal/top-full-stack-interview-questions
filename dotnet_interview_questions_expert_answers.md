# RUNTIME AND PLATFORM FUNDAMENTALS

## 1. What is .NET, and how do the runtime, the base class library, and the SDK relate to each other?

**.NET** is a development platform consisting of a runtime, libraries, compilers/tooling, and application frameworks.

The three concepts are different:

- **Runtime:** Executes managed code. The CLR/CoreCLR provides garbage collection, JIT compilation, exception handling, threading, type loading, and other execution services.
- **Base Class Library (BCL):** Reusable APIs such as `System.String`, collections, HTTP, JSON, file I/O, cryptography, tasks, and networking.
- **SDK:** Developer tooling. It includes the `dotnet` CLI, MSBuild, compilers, templates, project tooling, and commands such as `dotnet build`, `dotnet test`, and `dotnet publish`.

A useful mental model is:

```text
Your C# code
    ↓
Compiler / SDK
    ↓
Assembly containing IL + metadata
    ↓
.NET runtime
    ↓
Native machine instructions
    ↓
CPU
```

The SDK is what you use to **build** the application; the runtime is what is required to **run** it; the libraries provide the APIs your application calls.

---

## 2. What is the difference between .NET Framework, .NET Core, and modern .NET, and what does the unified platform mean in practice?

**.NET Framework** is the original Windows-focused implementation. It remains important for legacy applications such as older ASP.NET, Web Forms, WCF, and Windows-specific workloads.

**.NET Core** was the cross-platform, open-source redesign. It introduced side-by-side runtime versions, Linux/macOS support, a modern hosting model, and strong performance characteristics.

Starting with **.NET 5**, Microsoft unified the product under the name **.NET**. Modern releases are `.NET 6`, `.NET 7`, `.NET 8`, `.NET 9`, `.NET 10`, etc.

In practice, "unified" means:

- One primary platform and SDK.
- Common runtime and BCL.
- Cross-platform execution.
- ASP.NET Core, worker services, console applications, and libraries use the same underlying platform.
- A common project system and CLI.

It does **not** mean every .NET Framework technology magically exists on modern .NET. Migration compatibility still has to be evaluated.

---

## 3. What is an assembly, and how does it differ from a namespace and a NuGet package?

An **assembly** is a compiled .NET unit containing IL, metadata, and often resources. It is typically a `.dll` or `.exe`.

A **namespace** is a logical naming mechanism used to organize types:

```csharp
namespace MyCompany.Orders;

public class Order { }
```

A namespace has no independent runtime deployment identity.

A **NuGet package** is a distribution artifact. A package can contain one or more assemblies, analyzers, build targets, native libraries, metadata, and other files.

Think:

```text
Namespace  → organizes types
Assembly   → compiled/runtime unit
NuGet      → distribution/package unit
```

For example, one NuGet package may contain several assemblies targeting different frameworks.

---

## 4. What happens to your code between compilation and execution, and where do IL, the JIT, and AOT each fit?

C# is normally compiled into an assembly containing **Intermediate Language (IL)** and metadata.

At runtime, the .NET runtime loads the assembly and the **JIT compiler** converts methods from IL into native machine code for the current architecture.

```text
C# → Roslyn compiler → IL + metadata → JIT → native code → CPU
```

The JIT can optimize based on the actual runtime environment.

With **Native AOT**, much more of this compilation occurs ahead of time:

```text
C# → compiler/AOT toolchain → native executable
```

Native AOT can provide fast startup, lower runtime overhead, and smaller deployment footprints for appropriate applications, but it restricts scenarios that depend heavily on runtime code generation or reflection.

A strong interview answer should distinguish **compile time**, **JIT time**, and **runtime execution** rather than saying "C# is compiled directly to machine code."

---

## 5. What is the difference between framework-dependent and self-contained deployment, and what would make you pick each?

A **framework-dependent deployment (FDD)** publishes your application without shipping the .NET runtime. The target machine must have a compatible runtime installed.

Advantages:

- Smaller deployment.
- Runtime can be centrally patched.
- Useful in controlled infrastructure.

A **self-contained deployment (SCD)** ships the runtime with the application.

Advantages:

- The application does not depend on a separately installed .NET runtime.
- More predictable runtime availability.
- Useful for isolated hosts, appliances, containers, or environments where runtime installation is undesirable.

Trade-off:

```text
FDD → smaller, relies on installed runtime
SCD → larger, carries its runtime
```

For containers, SCD is not automatically better. A framework-dependent container can use a trusted .NET runtime base image and remain small.

---

## 6. What do trimming and Native AOT actually do, and why can a working service break once you enable them?

**Trimming** removes code that the linker determines is not reachable from the application's roots. This reduces deployment size.

**Native AOT** goes further by compiling the application to native code ahead of time, reducing or eliminating the need for JIT at runtime.

The problem is dynamic behavior.

For example:

```csharp
var type = Type.GetType(configuration["HandlerType"]);
var instance = Activator.CreateInstance(type);
```

A static analysis tool may not know that the type is required. It can therefore remove it.

Common trouble areas include:

- Reflection.
- Dynamically loaded assemblies.
- Runtime code generation.
- Some serializers.
- Dependency injection patterns that rely on reflection.
- Native libraries.
- Plugins.

The fix is not "disable trimming everywhere." Instead, identify dynamic dependencies and use supported annotations, source generation, explicit registrations, or AOT-compatible APIs.

Always test the **published trimmed/AOT artifact**, not only the normal build.

---

## 7. How would you standardise target frameworks and package versions across a solution with dozens of projects?

Use centralized build configuration rather than editing every `.csproj`.

Typical mechanisms include:

- `Directory.Build.props`
- `Directory.Build.targets`
- Central Package Management with `Directory.Packages.props`
- Shared MSBuild properties
- Renovate/Dependabot or an equivalent controlled update process
- CI validation

For example, centralize:

```xml
<PropertyGroup>
  <TargetFramework>net10.0</TargetFramework>
  <Nullable>enable</Nullable>
  <ImplicitUsings>enable</ImplicitUsings>
</PropertyGroup>
```

And centralize package versions separately.

The architectural principle is **one source of truth**. Also establish an exception process: a project may need a different target framework temporarily, but that exception should be explicit and reviewable.

---

# HOSTING AND STARTUP

## 8. Walk through what happens between `CreateBuilder()` and `app.Run()`. Where is the boundary between the two phases?

`CreateBuilder()` begins **host/application construction**.

During this phase you typically:

- Read configuration.
- Configure logging.
- Register dependency injection services.
- Configure the web host.
- Register framework services.

Then:

```csharp
var app = builder.Build();
```

`Build()` constructs the host, finalizes the service provider, and creates the application pipeline.

After `Build()`, you configure middleware/endpoints on `app`:

```csharp
app.UseAuthentication();
app.UseAuthorization();
app.MapControllers();
```

Finally:

```csharp
app.Run();
```

starts the host and begins accepting work.

The important boundary is:

```text
CreateBuilder → Build
    Configure the application

Build → Run
    Configure/use the built application and start it
```

---

## 9. Why does registering a service after `builder.Build()` throw, and what does that tell you about how the container works?

`builder.Build()` creates the application's service provider.

After that point, the container is effectively finalized. Adding registrations would make the already-created provider inconsistent with the registration collection.

So this is wrong:

```csharp
var app = builder.Build();

builder.Services.AddSingleton<MyService>(); // too late
```

The correct pattern is:

```csharp
builder.Services.AddSingleton<MyService>();
var app = builder.Build();
```

This demonstrates an important distinction:

- `IServiceCollection` is the **registration/configuration model**.
- `IServiceProvider` is the **runtime resolver**.

Dependency injection is configured before the provider is built.

---

## 10. What is Kestrel, and if IIS or Nginx sits in front of it, which one is actually running your application?

**Kestrel** is ASP.NET Core's cross-platform HTTP server.

If IIS or Nginx sits in front:

```text
Client → IIS/Nginx → Kestrel → ASP.NET Core application
```

Both can be involved, but Kestrel is still the server hosting the ASP.NET Core application process in the common reverse-proxy model.

IIS can also host ASP.NET Core using the ASP.NET Core Module, while Nginx normally acts as a reverse proxy.

The key distinction is:

- Reverse proxy: receives external traffic and forwards it.
- Kestrel: runs the ASP.NET Core HTTP pipeline.

---

## 11. Your app is behind a reverse proxy and sees the wrong client IP and scheme, causing redirect loops. What is missing?

Usually **Forwarded Headers Middleware** configuration.

A proxy may send:

- `X-Forwarded-For` → original client IP.
- `X-Forwarded-Proto` → original scheme (`http`/`https`).
- `X-Forwarded-Host` → original host.

ASP.NET Core must be configured to trust and process those headers:

```csharp
app.UseForwardedHeaders();
```

This middleware should run early enough that downstream components see the corrected scheme and client information.

You must also configure trusted proxies/networks appropriately. Blindly trusting forwarded headers from arbitrary clients creates a security problem.

A redirect loop commonly occurs when:

```text
Client uses HTTPS
→ proxy terminates TLS
→ app sees HTTP
→ app redirects to HTTPS
→ proxy sends request again
→ repeat
```

---

## 12. Why does a Web API and a Worker Service use the same host, and what does the host actually own?

The **Generic Host** provides common application infrastructure independent of whether the application is an HTTP API, worker, or another process.

The host owns concerns such as:

- Dependency injection.
- Configuration.
- Logging.
- Lifetime management.
- Hosted services.
- Application startup and shutdown.

ASP.NET Core adds the web-specific layer on top.

Conceptually:

```text
Generic Host
 ├── Configuration
 ├── Logging
 ├── DI
 ├── Lifetime
 └── Hosted services

ASP.NET Core
 └── HTTP server + middleware + endpoints
```

This is why the same hosting model works for both web and background applications.

---

# THE MIDDLEWARE PIPELINE

## 13. What is middleware, and how does a request actually travel through the pipeline and back out?

Middleware is a component in the HTTP request pipeline. It receives `HttpContext` and may either:

1. Handle the request itself, or
2. Call the next middleware.

Typical structure:

```csharp
public async Task InvokeAsync(HttpContext context)
{
    // Before downstream
    await _next(context);
    // After downstream
}
```

The request travels forward:

```text
A → B → C → Endpoint
```

The response travels back through the same middleware stack:

```text
Endpoint → C → B → A → Client
```

That is why middleware can perform both request preprocessing and response postprocessing.

---

## 14. Give the correct middleware order for a typical API, and justify why authentication, authorization, routing, and CORS sit where they do.

A common API pipeline is approximately:

```csharp
app.UseExceptionHandler("/error");

app.UseForwardedHeaders();

app.UseHttpsRedirection();

app.UseCors("Default");

app.UseRouting();

app.UseAuthentication();

app.UseAuthorization();

app.MapControllers();
```

Exact ordering depends on the application. The important rules are:

- Forwarded headers must be processed before components that depend on the original scheme/IP.
- CORS must be placed where it can affect the relevant responses.
- Authentication establishes `HttpContext.User`.
- Authorization evaluates whether that authenticated/anonymous principal may access the endpoint.
- Endpoint routing needs route metadata available before endpoint-specific authorization and filters execute.

For endpoint-specific rate limiting, routing needs to run before the rate limiter.

ASP.NET Core's current middleware guidance explicitly emphasizes ordering because middleware executes in registration order for requests and reverse order for responses. citeturn0search5turn0search8

---

## 15. What is the difference between `Use`, `Run`, and `Map`, and what happens to middleware registered after a terminal component?

`Use` normally adds middleware that can call the next component:

```csharp
app.Use(async (context, next) =>
{
    await next();
});
```

`Run` adds terminal middleware:

```csharp
app.Run(async context =>
{
    await context.Response.WriteAsync("Done");
});
```

It does not call the next component.

`Map` branches the pipeline based on a path or predicate:

```csharp
app.Map("/health", healthApp =>
{
    healthApp.Run(...);
});
```

If a terminal component handles the request, middleware registered after it will not execute for that request.

This is called **short-circuiting**.

---

## 16. Your middleware sets a status code after `await next()` and throws "response has already started". Why, and how do you restructure it?

Once the response headers have been sent to the client, some response properties can no longer be changed.

Example:

```csharp
await next();

context.Response.StatusCode = 500; // may be too late
```

The downstream endpoint may already have written the response.

Better approaches:

- Decide the status before downstream execution when possible.
- Handle exceptions with dedicated exception-handling middleware.
- Check `context.Response.HasStarted` before attempting late modifications.
- Buffer responses only when the specific use case justifies the complexity.

A common exception middleware pattern is:

```csharp
try
{
    await next(context);
}
catch (Exception ex)
{
    if (!context.Response.HasStarted)
    {
        context.Response.StatusCode = 500;
        // write error response
    }

    throw;
}
```

Do not attempt to rewrite a response that has already been committed.

---

## 17. Where must exception-handling middleware sit, and why does placing it late mean it silently catches nothing?

Exception-handling middleware should be **early in the pipeline** so that it wraps the components whose exceptions you want to catch.

Conceptually:

```text
Exception Handler
    ↓
Authentication
    ↓
Authorization
    ↓
Endpoint
```

If exception handling is placed after the component that throws, the exception never travels through it.

The middleware needs to be an outer wrapper:

```csharp
app.UseExceptionHandler(...);
```

before most application middleware.

One nuance: exceptions thrown by infrastructure before your ASP.NET Core middleware pipeline begins require different diagnostics/hosting mechanisms.

---

## 18. Your custom middleware needs a scoped service. Why does constructor injection create a bug, and what is the correct approach?

Middleware registered as conventional middleware is generally constructed outside the request scope and may effectively behave like a singleton.

Injecting a scoped service into its constructor can therefore create a **captive dependency**.

Instead, inject the scoped dependency into `InvokeAsync`:

```csharp
public async Task InvokeAsync(
    HttpContext context,
    IMyScopedService service)
{
    await service.DoWorkAsync();
    await _next(context);
}
```

This allows ASP.NET Core to resolve the dependency from the current request scope.

Another option is to make the middleware itself explicitly scoped/transient when appropriate, but method injection is usually the clearest pattern for conventional middleware.

---

# DEPENDENCY INJECTION INTERNALS

## 19. Explain Transient, Scoped, and Singleton in terms of state and thread safety rather than just instance counts.

Think in terms of **state ownership and lifetime**.

### Transient

A new instance is normally created each time it is requested.

Good for:

- Stateless lightweight services.
- Operations that should not share mutable state.

### Scoped

One instance per dependency-injection scope. In ASP.NET Core, the request is normally one scope.

Good for:

- `DbContext`.
- Request-specific state.
- Unit-of-work style services.

### Singleton

One instance for the application's lifetime.

Good for:

- Immutable configuration-derived services.
- Thread-safe caches.
- Expensive stateless infrastructure.

The critical issue is thread safety.

A singleton may be used concurrently by many requests:

```text
Request A ─┐
Request B ─┼→ Singleton
Request C ─┘
```

Therefore mutable singleton state must be synchronized or avoided.

---

## 20. What is a captive dependency, why does it often pass locally and fail in production, and how do you fix it?

A captive dependency occurs when a long-lived service captures a shorter-lived service.

Classic example:

```text
Singleton
   ↓
Scoped DbContext
```

The singleton can retain a scoped object beyond its intended lifetime.

This can cause:

- Stale state.
- Cross-request data contamination.
- Thread-safety issues.
- Object disposal problems.

It may pass locally because low concurrency hides the problem.

Fix the lifetime relationship or resolve the scoped service inside an explicitly created scope:

```csharp
using var scope = scopeFactory.CreateScope();
var db = scope.ServiceProvider.GetRequiredService<MyDbContext>();
```

The architectural rule is:

> A longer-lived component must not directly depend on a shorter-lived component unless the shorter-lived object is resolved within an appropriate scope.

---

## 21. You register three implementations of the same interface. What does resolving the interface give you, and how do you get all three?

For:

```csharp
services.AddTransient<INotifier, EmailNotifier>();
services.AddTransient<INotifier, SmsNotifier>();
services.AddTransient<INotifier, PushNotifier>();
```

Resolving:

```csharp
GetRequiredService<INotifier>()
```

returns the **last registered implementation**.

To get all implementations:

```csharp
IEnumerable<INotifier> notifiers
```

You can then iterate over all three.

This pattern is useful for plugin-like processing, notification strategies, handlers, validators, and pipelines.

---

## 22. What problem do keyed services solve, and when would you still prefer separate interfaces?

Keyed services let you register multiple implementations and select one using a key.

Conceptually:

```csharp
services.AddKeyedTransient<IPaymentGateway>("stripe", ...);
services.AddKeyedTransient<IPaymentGateway>("adyen", ...);
```

Then the consumer can request a particular key.

They are useful when implementations have the same contract but are selected by runtime configuration or context.

However, separate interfaces are often better when the implementations represent **different business concepts**.

Prefer:

```text
ICardPayment
IBankTransfer
```

over:

```text
IPaymentGateway keyed by "card"/"bank"
```

when the semantics are genuinely different.

Keys are a selection mechanism; they should not become a substitute for good domain modeling.

---

## 23. Who disposes the services the container creates, and which case surprises people most?

The DI container tracks disposable services it creates and disposes them when their owning scope/provider is disposed.

Typical behavior:

- Scoped disposable → disposed when the request scope ends.
- Singleton disposable → disposed when the root provider shuts down.
- Transient disposable resolved from a container scope → the container tracks it for disposal by that scope.

The surprising case is often:

> A transient `IDisposable` resolved from DI is still tracked and disposed by the container.

Therefore, avoid creating disposable objects through DI and then assuming the container will not manage them.

Conversely, if you manually construct an object with `new`, DI did not create it and generally does not own its disposal.

---

## 24. When would you replace the built-in container with a third-party one, and what do you give up?

The built-in container is sufficient for most applications.

A replacement may be justified when you need advanced capabilities such as:

- Complex convention-based registrations.
- Sophisticated decorators.
- Advanced interception.
- More elaborate lifetime models.
- Specific existing ecosystem integrations.

But replacing it introduces:

- Additional dependency.
- More operational and upgrade complexity.
- Different semantics for lifetimes/disposal.
- Another abstraction developers must understand.
- Potential incompatibility with framework assumptions.

Architecturally, do not replace the default container because "enterprise applications use another DI container." Replace it only when a concrete requirement outweighs the cost.

---

# CONFIGURATION AND OPTIONS

## 25. Two providers set the same configuration key. Which one wins, and what is the default provider order?

Configuration providers are layered. A provider added later has higher precedence.

In the standard ASP.NET Core setup, later sources generally override earlier ones. A typical order includes:

```text
appsettings.json
appsettings.{Environment}.json
User Secrets (development)
Environment variables
Command-line arguments
```

Thus:

```text
Environment variable > appsettings.json
```

for the same key in the default arrangement.

This is useful because deployment-specific values can override source-controlled defaults without modifying application files.

---

## 26. What is the difference between `IOptions`, `IOptionsSnapshot`, and `IOptionsMonitor`, and which one belongs in a background service?

### `IOptions<T>`

- Singleton-style access.
- Configuration is generally read once.
- Does not support per-request change tracking.

### `IOptionsSnapshot<T>`

- Scoped.
- Re-evaluates options per scope.
- Commonly useful in web requests.

### `IOptionsMonitor<T>`

- Singleton-friendly.
- Supports change notifications and current-value access.

For a `BackgroundService`, **`IOptionsMonitor<T>`** is usually the appropriate choice if configuration may change while the process is running.

Example:

```csharp
public Worker(IOptionsMonitor<MyOptions> options)
{
    _options = options;
}
```

If settings never change, `IOptions<T>` may be sufficient.

---

## 27. How do you make invalid configuration fail the deployment instead of failing a customer request at 3am?

Use **fail-fast startup validation**.

Bind configuration to a strongly typed options class and validate it:

```csharp
services
    .AddOptions<DatabaseOptions>()
    .BindConfiguration("Database")
    .ValidateDataAnnotations()
    .ValidateOnStart();
```

For complex rules, use custom validation.

Examples:

- Connection string must exist.
- Timeout must be between 1 and 120 seconds.
- Required API endpoint must be HTTPS.
- Two settings must not be mutually contradictory.

The principle is:

```text
Bad configuration
    ↓
Startup failure
    ↓
Deployment/health system notices
```

rather than:

```text
Bad configuration
    ↓
First real customer request
    ↓
Runtime failure
```

---

## 28. How does the app decide which environment-specific settings file to load, and where does the environment name come from?

ASP.NET Core commonly loads:

```text
appsettings.json
appsettings.{Environment}.json
```

For example:

```text
appsettings.json
appsettings.Development.json
appsettings.Production.json
```

The environment is determined by the host environment configuration, commonly using:

```text
DOTNET_ENVIRONMENT
ASPNETCORE_ENVIRONMENT
```

The environment name is available through `IHostEnvironment`/`IWebHostEnvironment`.

Do not confuse the environment name with configuration itself. Configuration providers establish values, while the host uses the environment name to decide which environment-specific configuration to load.

---

## 29. How would you manage secrets and connection strings across local, staging, and production?

Never store production secrets in source control.

A practical model:

### Local

Use:

- User Secrets.
- Environment variables.
- Local developer secret stores.

### Staging/Production

Use a managed secret store such as:

- Azure Key Vault.
- AWS Secrets Manager.
- GCP Secret Manager.
- Kubernetes secrets integrated with an external secret manager.

Applications should receive secrets through environment-specific configuration/injection.

Use different credentials per environment and preferably per application/service.

Also:

- Rotate credentials.
- Restrict access by identity.
- Audit secret access.
- Avoid logging secrets.
- Prefer managed identities/workload identity where available.

---

# ROUTING, FILTERS AND MODEL BINDING

## 30. How do you decide between middleware and a filter for a cross-cutting concern?

Use **middleware** when the concern is HTTP-pipeline-wide and should not depend on MVC/action semantics.

Examples:

- Correlation IDs.
- Global exception handling.
- Request logging.
- Security headers.
- Rate limiting.
- Forwarded headers.

Use **filters** when the concern is specifically tied to MVC/controller/action execution.

Examples:

- Action-specific authorization behavior.
- Model/action concerns.
- Result processing.
- MVC-specific validation or auditing.

Rule of thumb:

```text
HTTP concern → Middleware
MVC/action concern → Filter
```

Minimal APIs have endpoint filters for endpoint-level behavior.

---

## 31. What is the filter execution order, and where can a filter short-circuit the rest of the pipeline?

MVC filters execute in defined stages:

```text
Authorization
    ↓
Resource
    ↓
Action
    ↓
Exception/Result-related stages
    ↓
Action result
```

More precisely, filters have scopes and orders within their filter type, and some filter types wrap others.

An authorization filter can short-circuit by setting a result, preventing later authorization/action execution.

Resource filters can also short-circuit before model binding/action execution.

Action filters can short-circuit by assigning `context.Result` instead of calling the continuation.

The key interview point is not memorizing every number; understand that filters form nested stages around controller execution and that earlier stages can prevent later stages from running.

---

## 32. What is the Minimal API equivalent of an action filter, and what can it see that middleware cannot?

The Minimal API equivalent is an **endpoint filter**.

Endpoint filters can inspect:

- Endpoint arguments.
- Endpoint metadata.
- The endpoint invocation context.
- The result.
- The endpoint delegate.

Example:

```csharp
app.MapPost("/orders", CreateOrder)
   .AddEndpointFilter(async (context, next) =>
   {
       // inspect arguments
       var result = await next(context);
       // inspect/transform result
       return result;
   });
```

Middleware sees `HttpContext` and operates at the HTTP pipeline level. Endpoint filters operate closer to the actual endpoint invocation and therefore have endpoint arguments and metadata available.

---

## 33. How does model binding decide which part of the request a parameter comes from, and why can only one parameter bind from the body?

ASP.NET Core model binding uses parameter metadata and binding sources.

Common sources include:

- Route values.
- Query string.
- Headers.
- Form data.
- Body.
- Services.

Explicit attributes make intent clear:

```csharp
public IActionResult Get(
    [FromRoute] int id,
    [FromQuery] string sort,
    [FromBody] OrderRequest request)
```

The body is normally a single stream. Once a formatter consumes/deserializes that body into one model, it cannot naturally be independently deserialized into several unrelated body parameters.

Therefore this is not a good shape:

```csharp
Post([FromBody] A a, [FromBody] B b)
```

Instead create one request DTO containing both.

---

## 34. How do you validate input in a Minimal API without pulling in a third-party validation library, and where does that approach run out?

You can use:

- Data annotations.
- Explicit validation in the endpoint.
- `IValidatableObject`.
- Endpoint filters.
- Custom reusable validation services.

For example:

```csharp
if (request.Quantity <= 0)
    return Results.BadRequest("Quantity must be positive.");
```

For larger applications, move validation into a dedicated validator/service or use a validation framework.

The limitation of manual validation is consistency. As rules become complex, repeated validation code becomes difficult to maintain and test.

The right goal is not "avoid libraries at all costs"; it is "use the simplest validation mechanism that remains maintainable."

---

## 35. What are the trade-offs between Minimal APIs and controller-based APIs for a large team?

### Minimal APIs

Advantages:

- Less ceremony.
- Concise endpoint definitions.
- Excellent for small services and focused APIs.
- Endpoint filters and route groups provide useful composition.

Disadvantages at large scale:

- Large files can become difficult to navigate.
- Team conventions need to be strong.
- Complex endpoint metadata and organization can become harder to manage.

### Controllers

Advantages:

- Strong organizational conventions.
- Familiar MVC filter/model-binding structure.
- Clear grouping by controllers/actions.
- Often easier for large teams with established MVC patterns.

Disadvantages:

- More ceremony.
- More framework concepts.

For a large organization, consistency is usually more important than choosing the theoretically smallest API surface.

---

# REQUEST LIFECYCLE AND BACKGROUND WORK

## 36. What is `HttpContext`, how long does it live, and why is holding a reference to it a bug?

`HttpContext` represents the current HTTP request/response context.

It contains:

- Request.
- Response.
- User.
- Headers.
- Services.
- Connection information.
- Items.
- Endpoint metadata.

Its lifetime is tied to the request.

Do not store it in long-lived objects:

```csharp
_singleton.Context = httpContext; // bad
```

After the request completes, the context may be recycled or otherwise no longer represent a valid active request.

Instead copy the small piece of information you need:

```csharp
var userId = httpContext.User.FindFirst("sub")?.Value;
```

and pass that value to longer-lived work.

---

## 37. Does one request run on one thread? What happens across an `await`, and why does ASP.NET Core have no synchronization context?

No. A request does not have a permanent thread.

Before an `await`, code may run on one ThreadPool thread. When the awaited operation completes, continuation code may run on another ThreadPool thread.

ASP.NET Core intentionally does not install the classic ASP.NET synchronization context. Therefore `await` does not need to marshal continuations back to a request-specific context.

This is one reason async I/O scales well:

```text
Request
  ↓
await database/network I/O
  ↓
thread returns to ThreadPool
  ↓
I/O completes
  ↓
continuation executes
```

The key is that `await` does not make CPU work asynchronous; it primarily prevents a thread from being blocked while waiting for asynchronous I/O.

---

## 38. You need the current user inside a singleton service. How do you get it, and what are the catches?

A singleton can use `IHttpContextAccessor`:

```csharp
public MyService(IHttpContextAccessor accessor)
{
    _accessor = accessor;
}
```

Then:

```csharp
var user = _accessor.HttpContext?.User;
```

But this has important catches:

- There may be no HTTP context.
- The singleton must not retain the context.
- Background threads/workers may not have a current user.
- Business logic becomes coupled to ambient HTTP state.
- Testing becomes harder.

Prefer passing explicit identity/context into business operations:

```csharp
await orderService.CreateAsync(command, currentUserId);
```

Use `IHttpContextAccessor` primarily at application boundaries.

---

## 39. Your `BackgroundService` needs a database context. Why is constructor injection a trap, and what is the correct pattern?

`BackgroundService` is effectively long-lived. `DbContext` is scoped.

Injecting `DbContext` directly into the worker constructor creates a lifetime mismatch.

Instead inject `IServiceScopeFactory` and create a scope per unit of work:

```csharp
protected override async Task ExecuteAsync(CancellationToken stoppingToken)
{
    while (!stoppingToken.IsCancellationRequested)
    {
        using var scope = _scopeFactory.CreateScope();

        var db = scope.ServiceProvider
                     .GetRequiredService<MyDbContext>();

        await ProcessAsync(db, stoppingToken);
    }
}
```

For async disposal:

```csharp
await using var scope = _scopeFactory.CreateAsyncScope();
```

Each iteration gets a fresh scoped context with a clear lifetime.

---

## 40. A deployment restarts the service while requests and background jobs are in flight. How do you implement graceful shutdown?

Graceful shutdown requires cooperation across the application and infrastructure.

ASP.NET Core signals cancellation through the host lifetime token.

Your code should:

- Accept `CancellationToken`.
- Stop accepting new work.
- Let in-flight operations finish when practical.
- Stop background loops.
- Drain queues.
- Dispose resources.
- Configure sufficient termination grace time in the hosting platform.

Example:

```csharp
await service.ProcessAsync(stoppingToken);
```

For background queues, a robust architecture often separates:

```text
Receive work
   ↓
Durable queue
   ↓
Worker
   ↓
Process
   ↓
Ack
```

If the process dies before acknowledgement, durable messaging can redeliver the work.

Graceful shutdown reduces loss, but **durability and idempotency** are still required for reliable distributed processing.

---

## 41. Walk through the full journey of a request, from the socket to your endpoint and back.

A simplified journey:

```text
Client
  ↓
Network / load balancer / reverse proxy
  ↓
Kestrel
  ↓
HTTP parsing
  ↓
ASP.NET Core middleware pipeline
  ↓
Routing
  ↓
Authentication
  ↓
Authorization
  ↓
Endpoint
  ↓
Model binding / validation / endpoint filters
  ↓
Application service
  ↓
Database/downstream services
  ↓
Endpoint result
  ↓
Response middleware unwinds
  ↓
Kestrel
  ↓
Proxy/load balancer
  ↓
Client
```

At the transport level, TLS may terminate at the proxy or Kestrel. At the application level, middleware controls the HTTP processing pipeline.

The exact path changes for Minimal APIs, controllers, gRPC, WebSockets, static files, and other endpoint types.

---

# EF CORE AND DATA ACCESS

## 42. How does change tracking work, and what actually happens when you save?

EF Core's `DbContext` maintains a **change tracker** for entities it tracks.

Suppose:

```csharp
var order = await db.Orders.FindAsync(id);
order.Status = "Paid";
await db.SaveChangesAsync();
```

EF Core knows the original state and current state. When `SaveChangesAsync()` runs, it:

1. Detects changes when appropriate.
2. Determines which entities are Added/Modified/Deleted.
3. Generates database commands.
4. Sends them to the database, often batching commands.
5. Updates tracking state.

Conceptually:

```text
Database row
    ↓
Tracked entity
    ↓
Property changes
    ↓
Change tracker detects Modified
    ↓
SaveChanges
    ↓
SQL UPDATE
```

Change tracking is useful for unit-of-work scenarios but has memory and CPU overhead.

---

## 43. When would you turn tracking off, and what do you lose by doing so?

For read-only queries, use:

```csharp
var products = await db.Products
    .AsNoTracking()
    .ToListAsync();
```

You gain:

- Less memory.
- Less change-tracking overhead.
- Often better read performance.

You lose automatic tracking and therefore cannot simply modify the returned entities and expect `SaveChanges()` to detect those changes.

Use tracking when the entity is part of a unit of work that will be updated. Use no-tracking for read models, reporting, list endpoints, and other read-only workloads.

---

## 44. How does the N+1 query problem arise, and how do eager, lazy, and explicit loading each affect it?

N+1 occurs when you execute one query for the parent collection and then one query for each parent.

Example:

```text
1 query → load 100 orders
100 queries → load each customer's details
-----------------------------------------
101 queries
```

### Eager loading

```csharp
.Include(x => x.Customer)
```

Loads related data as part of the query.

### Lazy loading

Accessing a navigation property triggers a query automatically.

Convenient, but can accidentally create N+1 behavior.

### Explicit loading

You explicitly request related data when needed.

It gives control but requires deliberate query design.

For APIs, prefer predictable query shapes and projections:

```csharp
.Select(x => new OrderDto
{
    Id = x.Id,
    CustomerName = x.Customer.Name
})
```

This can fetch exactly the data required.

---

## 45. How would you run migrations safely across environments and a team, and what would you never do in production?

Treat migrations as **versioned database changes**.

Recommended process:

1. Developer creates migration.
2. Migration is reviewed.
3. Migration is committed to source control.
4. CI validates it.
5. Deployment pipeline applies it in a controlled way.
6. Application and schema compatibility are managed during rollout.

For zero-downtime systems, use **expand-and-contract**:

```text
Expand schema
→ deploy backward-compatible application
→ migrate/backfill data
→ switch reads/writes
→ contract old schema later
```

Avoid running `dotnet ef database update` manually against production as an ad-hoc operational procedure.

Also avoid destructive changes in the same deployment that still requires the old schema.

---

## 46. How do you handle two users updating the same record, and what does optimistic concurrency actually detect?

Optimistic concurrency assumes collisions are relatively uncommon.

A row version/token can be used:

```text
User A reads row version 10
User B reads row version 10

A updates → version 11

B updates WHERE version = 10
→ zero rows affected
→ concurrency conflict
```

EF Core can represent this using a concurrency token such as a SQL Server `rowversion`.

It detects:

> The row changed since I read it.

It does not automatically tell you which business change should win.

Your application must decide whether to:

- Reject the update.
- Reload and merge.
- Retry.
- Apply a domain-specific conflict rule.

---

## 47. A query looks fine in C# but generates terrible SQL. How do you find that out and fix it?

Do not judge query quality from LINQ syntax.

Inspect generated SQL using:

- EF Core logging.
- `ToQueryString()`.
- Database query profiler.
- Database execution plans.
- Query statistics.

Example:

```csharp
var sql = query.ToQueryString();
```

Then inspect the actual database plan.

Common problems:

- Missing indexes.
- Cartesian explosion.
- Excessive joins.
- Unnecessary columns.
- Client-side evaluation or materialization too early.
- Functions preventing index use.
- Large `Include` graphs.
- Poor pagination.
- Parameter/data distribution issues.

Fix the **database workload**, not merely the C# appearance.

---

## 48. How would you insert several hundred thousand rows efficiently, and why is a loop of saves the wrong shape?

This is a bulk data problem.

Avoid:

```csharp
foreach (var item in items)
{
    db.Add(item);
    await db.SaveChangesAsync();
}
```

That creates many database round trips and repeated change-tracking work.

Better options include:

- Add entities in batches and call `SaveChanges` per batch.
- Use database-native bulk loading.
- Use provider-specific bulk APIs where appropriate.
- Use `SqlBulkCopy` for SQL Server scenarios.
- Use `ExecuteUpdate`/`ExecuteDelete` for set-based updates/deletes where applicable.

For hundreds of thousands of rows, measure:

- Batch size.
- Transaction size.
- Log growth.
- Index maintenance.
- Locking.
- Memory consumption.

The key principle is **set-based/batched work rather than one database transaction per item**.

---

# DATA AT SCALE

## 49. Users see stale data immediately after saving because reads go to a lagging replica. How do you fix it?

This is a read-after-write consistency problem.

Options:

1. Route the user's immediate follow-up read to the primary.
2. Use a consistency-aware routing mechanism.
3. Return the updated resource directly from the write operation.
4. Use a short-lived cache keyed by the updated version.
5. Wait for replication when the business requirement requires it.

A common API pattern is:

```text
POST /orders
→ write primary
→ return created/updated representation
```

instead of immediately doing:

```text
POST
→ primary write

GET
→ replica read
→ stale result
```

Do not solve consistency problems by blindly increasing replication frequency without understanding the workload.

---

## 50. A nightly batch job locks a large table and the API starts failing. What do you change about the job?

First determine what causes the lock:

- Long transaction.
- Full-table update.
- Missing indexes.
- Large deletes.
- Lock escalation.
- Inefficient query plan.

Then redesign the job:

- Process in small batches.
- Commit frequently.
- Use indexed predicates.
- Avoid unnecessary table scans.
- Run during lower traffic when appropriate.
- Use partitioning for very large datasets.
- Move heavy analytical work to replicas or dedicated stores.
- Use queue-based incremental processing instead of one giant transaction.

Do not merely move the job from midnight to 2am if the system still experiences unacceptable contention.

---

## 51. You need to add a non-nullable column to a two-hundred-million-row table with zero downtime. Walk through the steps.

Use an **expand-and-contract** migration.

### Step 1: Add nullable column

```sql
ALTER TABLE Orders ADD NewColumn ... NULL;
```

This is usually much safer than immediately requiring a value.

### Step 2: Deploy application code

Application understands both old and new schema.

### Step 3: Backfill

Backfill in batches:

```text
UPDATE small batch
COMMIT
repeat
```

Monitor locks, log growth, replication lag, and performance.

### Step 4: Start writing the new column

Deploy code that writes a valid value for new/updated rows.

### Step 5: Verify

Ensure no rows remain null.

### Step 6: Enforce constraint

Only after the data is clean, make the column non-nullable or add the required constraint.

### Step 7: Remove compatibility code later

This separation is important because schema changes and application releases do not necessarily happen atomically in a distributed deployment.

---

## 52. When is moving off a relational database actually justified, and what do you give up?

Do it when the relational model is demonstrably the wrong tool for the workload, not because NoSQL sounds more scalable.

Possible reasons:

- Extremely high write scale.
- Document-oriented aggregates.
- Specialized graph relationships.
- Time-series workloads.
- Globally distributed access patterns.
- Requirements that map poorly to relational joins/transactions.

You may give up or complicate:

- Strong relational integrity.
- Rich joins.
- Mature transaction semantics.
- Familiar query tooling.
- Ad-hoc reporting.
- Operational simplicity.

The strongest architecture answer starts with the workload and consistency model, not the database brand.

---

# MEMORY, GC AND THE THREAD POOL

## 53. Your API's memory climbs all day and drops on restart. How do you determine whether it is really a leak?

A growing process is not automatically a leak.

Investigate:

1. **Managed heap size.**
2. **GC collection frequency and pause time.**
3. **Gen 2 survival.**
4. **Large Object Heap.**
5. **Object type counts.**
6. **Native/unmanaged memory.**
7. **Working set vs managed heap.**

Take multiple heap dumps over time and compare retained objects.

If the same objects remain rooted and grow continuously, suspect a managed memory leak.

Typical causes:

- Static collections.
- Unbounded caches.
- Event subscriptions.
- Long-lived tasks.
- Incorrect singleton state.
- `HttpClient`/socket misuse.
- Native resources.

If heap usage is stable but RSS grows, the problem may be outside the managed heap.

---

## 54. What is the difference between Server GC and Workstation GC, and why might your configured choice be ignored entirely?

**Workstation GC** is designed with client/interactive workloads in mind.

**Server GC** is optimized for throughput on server workloads and can use multiple heaps.

However, modern .NET GC behavior includes **DATAS (Dynamic adaptation to application sizes)**, which can materially change the traditional Server-vs-Workstation mental model.

Also, configuration may be overridden or constrained by runtime/version/platform settings.

Do not assume that setting a GC switch guarantees the exact behavior you expect. Verify the actual runtime configuration and runtime version.

---

## 55. What is DATAS, when did it become the default, and why does it matter to teams upgrading right now?

**DATAS = Dynamic Adaptation To Application Sizes.**

It adapts GC behavior to the application's memory requirements, aiming for heap size to remain more proportional to long-lived application data rather than simply growing according to machine capacity.

DATAS was introduced as an opt-in feature in **.NET 8** and became enabled by default in **.NET 9**. citeturn0search0turn0search7

Why it matters:

- Memory-constrained environments can benefit from a smaller working set.
- Bursty workloads can give memory back more effectively.
- Behavior can differ from teams' older Server GC assumptions.
- Upgrade performance testing should measure both throughput and memory.

Microsoft's documentation reports substantial working-set improvements in some benchmarks, with a modest throughput trade-off in the tested scenarios. citeturn0search0

The interview-level lesson is: **do not blindly carry old GC tuning assumptions into a newer runtime.**

---

## 56. What lands on the Large Object Heap, why does that hurt, and what is the fix that is not a GC setting?

Large allocations—traditionally allocations around **85,000 bytes or larger**—are candidates for the Large Object Heap.

Examples:

- Large byte arrays.
- Large strings.
- Large object graphs/arrays.

Problems include:

- Expensive allocation patterns.
- Fragmentation.
- Larger GC impact.
- High memory retention.

A common real fix is **change the allocation pattern**, not tune the GC.

For example:

```text
Bad:
Allocate 10 MB buffer for every request.

Better:
Rent reusable buffers from ArrayPool<T>.
Stream data instead of buffering everything.
```

The best fix is often reducing allocation size/frequency or reusing buffers.

---

## 57. Gen 0 collections are supposed to be cheap, so why is your p99 spiking?

"Cheap" does not mean "free."

High Gen 0 allocation rates can cause:

- Frequent GC activity.
- CPU consumption.
- Allocation stalls.
- Increased scheduling pressure.
- Cascading latency under load.

Also, the p99 request may not be directly blocked by one Gen 0 collection. It can be a symptom of an allocation-heavy workload that creates broader CPU/ThreadPool pressure.

Measure:

- Allocation rate.
- GC pause time.
- CPU.
- Gen 0/1/2 counts.
- ThreadPool queue length.
- Request latency.

Then reduce allocation volume before tuning GC settings.

---

## 58. Your process holds far more memory than the heap snapshot accounts for. Where is the rest?

Process memory includes more than the managed heap.

Possible sources:

- Native allocations.
- JIT/code pages.
- Thread stacks.
- Loaded native libraries.
- Memory-mapped files.
- Runtime structures.
- TLS/native buffers.
- Socket/network buffers.
- Graphics or other native resources.
- Fragmentation/allocator behavior.

Compare:

```text
RSS / Working Set
vs
Managed Heap
```

If the difference is large, investigate native memory.

Useful diagnostics include process-level counters, runtime counters, dump analysis, native allocation diagnostics, and OS-level tools.

Do not call every RSS increase a ".NET GC leak."

---

## 59. Your API times out under load while CPU sits at 15%. What is happening, and how do you confirm it?

Low CPU plus high latency often means **waiting**, not insufficient compute.

Possible causes:

- ThreadPool starvation.
- Database connection pool exhaustion.
- Slow database.
- External API latency.
- Lock contention.
- Semaphore contention.
- Network I/O.
- Synchronous blocking around async code.

Confirm by measuring:

- ThreadPool queue length.
- Active/available worker threads.
- Request duration.
- DB connection pool metrics.
- Downstream latency.
- Lock contention.
- Thread dumps/stacks.

A common failure pattern is:

```csharp
var result = SomeAsync().Result;
```

or:

```csharp
SomeAsync().Wait();
```

These block worker threads and can cause starvation under load.

---

## 60. You have confirmed thread pool starvation. How do you find the exact blocking call in production?

Do not immediately increase the ThreadPool minimum.

First capture evidence.

Use:

- `dotnet-counters` for ThreadPool/runtime counters.
- `dotnet-stack` for live managed stack traces.
- `dotnet-dump` when a dump is appropriate.
- Tracing/profiling tools.
- Application telemetry showing synchronous waits.

Look for stacks containing:

```text
.Wait()
.Result
Monitor.Enter
Task.Wait
Semaphore.Wait
synchronous I/O
```

Correlate the stack with endpoint/downstream telemetry.

The goal is:

```text
ThreadPool starvation
→ identify blocked threads
→ identify common blocking stack
→ remove synchronous wait
```

Increasing ThreadPool capacity can sometimes reduce symptoms but does not fix the blocking operation.

---

## 61. Choose between `lock`, `SemaphoreSlim`, and `Interlocked` for a shared counter, and defend the choice.

For a simple numeric counter, prefer **`Interlocked`**:

```csharp
Interlocked.Increment(ref count);
```

It is atomic and very cheap for simple operations.

Use **`lock`** when you need to protect a compound critical section:

```csharp
lock (_gate)
{
    state.Update();
    cache.Remove(...);
}
```

Use **`SemaphoreSlim`** when you need asynchronous waiting:

```csharp
await semaphore.WaitAsync(token);
try
{
    await DoAsyncWork();
}
finally
{
    semaphore.Release();
}
```

Decision:

```text
Atomic primitive → Interlocked
Synchronous critical section → lock
Async coordination → SemaphoreSlim
```

Do not use `lock` around long-running asynchronous operations.

---

## 62. Your `ConcurrentDictionary.GetOrAdd` factory ran twice. Why, and when does that actually matter?

`GetOrAdd` guarantees the dictionary's resulting value, not necessarily that the factory runs exactly once.

Under concurrency:

```text
Thread A → factory()
Thread B → factory()
```

Both may compute a value, but only one value wins the race.

Therefore the factory should generally be:

- Cheap.
- Side-effect-free.
- Idempotent.

If creating the value has an expensive or externally visible side effect, `GetOrAdd` alone may be insufficient. Use another synchronization mechanism or store a shared task/lazy value.

---

## 63. You need to call a downstream API five hundred times. How do you do it without taking that service down?

Do not fire 500 requests simultaneously.

Use bounded concurrency:

```csharp
var semaphore = new SemaphoreSlim(20);

var tasks = items.Select(async item =>
{
    await semaphore.WaitAsync();
    try
    {
        return await CallAsync(item);
    }
    finally
    {
        semaphore.Release();
    }
});

await Task.WhenAll(tasks);
```

Also implement:

- Timeout.
- Retry only for transient failures.
- Exponential backoff + jitter.
- Circuit breaker where appropriate.
- Cancellation.
- Bulkhead/concurrency limits.
- Rate limits if the provider publishes them.
- Idempotency where retries can duplicate operations.

The objective is not maximum parallelism; it is **maximum sustainable throughput**.

---

# PRODUCTION DIAGNOSTICS AND OBSERVABILITY

## 64. Production is slow, you cannot attach a debugger and cannot deploy. Which tools do you reach for, and in what order?

Start with **metrics**, because they are cheap and broad.

1. Dashboard: latency, throughput, errors, saturation.
2. `dotnet-counters`: runtime/GC/ThreadPool signals.
3. Distributed tracing: identify slow dependencies.
4. Logs with correlation IDs.
5. `dotnet-stack` for live stack evidence.
6. `dotnet-dump` for deeper analysis when needed.
7. OS/database/network diagnostics.

The order is:

```text
Observe → narrow → capture evidence → diagnose
```

Avoid restarting the process simply because it "fixes" the symptom. A restart destroys valuable diagnostic evidence.

---

## 65. Which four numbers would you put on a dashboard for a .NET API, and why is latency a percentile?

A good starting four are:

1. **Request rate** — how much traffic is arriving.
2. **Error rate** — how often requests fail.
3. **Latency percentiles** — how users experience the service.
4. **Saturation** — CPU, memory, ThreadPool, DB pool, or another dominant resource.

Latency is a distribution, not a single number.

If:

```text
p50 = 40 ms
p99 = 6 sec
```

then half the requests are fast but the slowest 1% are terrible.

An average could hide this completely.

Percentiles answer:

> "How bad is the experience for the slower fraction of users?"

For customer-facing systems, p95/p99 are often more actionable than averages.

---

## 66. A bug appears in production once a week and never locally. How do you catch it?

You need **production-grade observability**, not necessarily a production debugger.

Use:

- Structured logs.
- Correlation/request IDs.
- Distributed traces.
- Metrics.
- Exception telemetry.
- Feature flags.
- Sampling strategies.
- Diagnostic dumps triggered by conditions.
- Reproduction data where privacy allows.

For intermittent bugs, preserve enough context to answer:

```text
Who?
Which request?
Which version?
Which node?
What inputs?
What dependencies?
What timing?
What exception/state?
```

Avoid logging sensitive payloads just to get more detail.

---

## 67. You have 40 GB of logs a day and still cannot answer why one request was slow. What is wrong with the logging?

You have **volume without diagnostic structure**.

Common problems:

- Too much debug noise.
- No correlation ID.
- No trace/span IDs.
- No duration fields.
- No downstream dependency timings.
- Unstructured text.
- No consistent event names.
- Logging entire payloads instead of relevant metadata.

A useful request log might include:

```text
trace_id
request_id
route
method
status
duration_ms
user/tenant identifier where safe
deployment version
dependency durations
exception type
```

The goal is **high-cardinality context with controlled volume**, not "log everything."

---

## 68. How would you add distributed tracing across several services, and what do you correlate on?

Use **OpenTelemetry** with W3C trace context.

A trace consists of spans:

```text
Trace
 ├── API span
 ├── DB span
 ├── downstream HTTP span
 │     └── downstream service span
 └── cache span
```

Propagate trace context across service boundaries.

Correlate primarily using:

- `trace_id`
- `span_id`
- Service name/version.
- Request/operation metadata.

A single `trace_id` lets you follow one logical request across multiple services.

Logs should include the trace identifiers so you can jump:

```text
Metric → Trace → Span → Logs
```

---

## 69. What is the difference between a liveness and a readiness probe, and what belongs in each health check?

### Liveness

Answers:

> "Is this process alive enough that restarting it may help?"

Keep it lightweight.

Do not make liveness depend on every downstream dependency.

### Readiness

Answers:

> "Should this instance receive traffic right now?"

Readiness may check critical dependencies such as:

- Database.
- Required configuration.
- Essential downstream service.

A database outage might make an instance **not ready** without meaning the process should be killed.

Confusing these probes can cause cascading restarts during a dependency outage.

---

## 70. p50 is 40ms and p99 is 6 seconds. Where do you look first?

This strongly suggests a **tail-latency problem**.

Look for operations affecting only a subset of requests:

- Database lock waits.
- Slow queries.
- Cache misses.
- Large payloads.
- Specific tenants/data.
- Downstream API timeouts.
- Connection pool exhaustion.
- ThreadPool starvation.
- GC pauses.
- Queueing.

Break p99 down by:

```text
endpoint
dependency
status
tenant/customer
instance
region
payload size
```

If only one endpoint has a bad p99, start there. If every endpoint has it, suspect shared infrastructure.

---

# SECURITY

## 71. What is the difference between authentication and authorization, and how does the pipeline handle each?

**Authentication** answers:

> Who are you?

It establishes the `ClaimsPrincipal`, normally represented by `HttpContext.User`.

**Authorization** answers:

> Are you allowed to perform this operation?

The typical sequence is:

```text
Authentication
    ↓
Creates/establishes identity
    ↓
Authorization
    ↓
Evaluates policy/roles/requirements
    ↓
Endpoint
```

A user can be authenticated but unauthorized.

Example:

```text
Authenticated: Alice
Required role: Admin
Alice role: User
→ 403 Forbidden
```

No valid identity at all may result in:

```text
401 Unauthorized
```

depending on the authentication scheme and endpoint configuration.

---

## 72. How does bearer token authentication work, and what does token validation actually check?

A client sends:

```http
Authorization: Bearer eyJ...
```

The authentication handler validates the token.

For a JWT, validation commonly includes:

- Signature.
- Issuer (`iss`).
- Audience (`aud`).
- Expiration (`exp`).
- Not-before (`nbf`) where applicable.
- Cryptographic algorithm/key constraints.
- Required claims depending on policy.

A valid signature alone is not sufficient.

For example, a token signed correctly by a trusted issuer but intended for another API should not be accepted by your API.

After successful validation, claims become the authenticated principal.

---

## 73. What is the difference between role-based and policy-based authorization, and when do you need the latter?

Role-based:

```csharp
[Authorize(Roles = "Admin")]
```

checks membership in a role.

Policy-based authorization can express richer requirements:

```text
User must:
- be authenticated
- have scope orders.write
- belong to tenant X
- satisfy a custom business requirement
```

Policies can combine:

- Claims.
- Roles.
- Custom requirements.
- Custom authorization handlers.

Use policy-based authorization when authorization depends on more than a simple role label.

---

## 74. What is CORS, and why does a preflight request fail when middleware is ordered wrongly?

CORS (**Cross-Origin Resource Sharing**) controls whether browser JavaScript from one origin may access resources from another origin.

For some cross-origin requests, the browser first sends an `OPTIONS` **preflight** request.

The server must respond with appropriate CORS headers.

If CORS middleware is placed incorrectly, the request may be rejected or the required headers may not be added.

A typical setup is:

```csharp
app.UseCors("Default");
```

in the correct location relative to routing/endpoints.

Important: CORS is primarily a **browser security mechanism**. It does not prevent a server-to-server HTTP client from calling your API.

---

## 75. An unauthenticated API call now returns 401 where it used to redirect to a login page. What changed?

The authentication scheme/behavior likely changed.

Browser-oriented cookie authentication commonly redirects unauthenticated users to a login page.

Bearer-token APIs generally return:

```http
401 Unauthorized
```

because an API client should receive a protocol-level authentication response rather than an HTML login page.

Modern framework behavior and cookie handler configuration can also influence whether redirects are suppressed for API endpoints.

The correct behavior depends on the authentication scheme and endpoint type.

---

## 76. What is the Data Protection API, and why does it need explicit configuration in a load-balanced or containerised deployment?

ASP.NET Core Data Protection provides cryptographic services used by framework features such as:

- Authentication cookies.
- CSRF/antiforgery protection.
- Temporary protected data.
- Other framework tokens.

In a single process, the framework can manage its key ring automatically.

In a load-balanced deployment:

```text
Node A → key ring A
Node B → key ring B
```

If keys are not shared/persisted appropriately, data protected by A may not be decryptable by B.

Therefore configure:

- A persistent key store.
- Shared keys across instances.
- Appropriate key encryption at rest.
- Stable application discriminator when required.

Container restarts make ephemeral key storage particularly dangerous for cookie/session-style protected data.

---

## 77. How would you protect an API from abuse, and what does built-in rate limiting give you?

Use multiple layers:

- Authentication.
- Authorization.
- Input limits.
- Request body size limits.
- Timeouts.
- Rate limiting.
- Concurrency limits.
- API gateway/WAF protection.
- Resource quotas.
- Abuse detection.

ASP.NET Core provides built-in rate limiting middleware with policies such as fixed/sliding windows, token bucket, and concurrency-oriented controls.

Rate limiting is useful for protecting server resources and enforcing product quotas.

But it is not a complete DDoS solution. Large-scale attacks should also be handled at network/CDN/WAF layers.

---

# PERFORMANCE, CACHING AND MEASUREMENT

## 78. You claim your change made an endpoint three times faster. Prove it.

Define a reproducible experiment.

Measure:

- Same code path.
- Same representative dataset.
- Same infrastructure.
- Same request mix.
- Warm vs cold state explicitly.
- Multiple repetitions.
- p50/p95/p99.
- Throughput.
- CPU.
- Memory.
- Allocations.
- Downstream database behavior.

Example:

```text
Before:
p50 120 ms
p95 310 ms
p99 900 ms

After:
p50 42 ms
p95 95 ms
p99 210 ms
```

Then verify statistical stability and understand **why** it improved.

A benchmark that only reports average latency from ten local requests is not proof.

---

## 79. Why do microbenchmarks lie, and when is a benchmark the wrong instrument entirely?

Microbenchmarks isolate tiny operations. Production systems contain:

- Network latency.
- Database behavior.
- Serialization.
- Contention.
- GC.
- Thread scheduling.
- Caches.
- Real payload distributions.

A microbenchmark can tell you:

> "Operation A is faster than operation B under this controlled workload."

It cannot automatically tell you:

> "The API will be faster in production."

Use microbenchmarks for hot, isolated code paths.

Use load/performance tests for system-level questions.

Use production telemetry for real customer behavior.

---

## 80. Where do you spend optimisation effort on a slow API, and in what order?

A practical order:

1. Measure the endpoint.
2. Identify the dominant latency component.
3. Fix inefficient algorithms/query shapes.
4. Fix excessive network/database calls.
5. Reduce unnecessary serialization/payload.
6. Improve caching where justified.
7. Reduce allocation/GC pressure.
8. Tune concurrency/threading.
9. Only then consider low-level optimizations.

For example:

```text
800 ms API
→ 650 ms database query
```

Optimizing a JSON allocation from 2 ms to 1 ms is irrelevant.

Optimization should follow **cost contribution**, not developer convenience.

---

## 81. When is "just add a cache" the wrong answer?

Caching is wrong when:

- Data changes too frequently.
- Stale data is unacceptable.
- Cache invalidation is harder than the original problem.
- The underlying query is already cheap.
- Cache cardinality is enormous.
- Cache misses create a thundering herd.
- The real bottleneck is downstream contention.
- The cache becomes a second database with complex consistency rules.

Caching can also hide poor architecture.

First understand:

```text
Why is this operation slow?
```

Then determine whether caching changes the cost model without introducing unacceptable consistency risk.

---

## 82. How do in-memory, distributed, and hybrid caching differ, and which would you reach for first?

### In-memory cache

Fastest and simplest.

But each application instance has its own copy.

### Distributed cache

Shared across instances.

Useful for:

- Multiple replicas.
- Shared sessions.
- Shared expensive results.

Adds network latency and operational dependency.

### Hybrid

Use local memory for very hot data and a distributed cache for shared state.

A sensible starting point for a single-instance application is often in-memory caching.

For horizontally scaled systems, distributed caching becomes more attractive when consistency across nodes matters.

---

## 83. A hot cache key expires under load and every request hits the database at once. How do you prevent it?

This is a **cache stampede/thundering herd**.

Strategies:

- Single-flight/request coalescing.
- Per-key locking.
- Early refresh.
- Stale-while-revalidate.
- Jittered expiration.
- Background refresh.
- Distributed locks when appropriate.

For example:

```text
First request detects miss
→ becomes refresh owner

Other requests
→ wait for shared refresh result
```

Do not use a global lock if only one cache key is hot; use fine-grained per-key coordination.

---

## 84. Why is creating a new `HttpClient` per call a problem, and what does the factory actually fix?

Creating and disposing a new `HttpClient` for every request can cause inefficient connection management and contribute to socket/port exhaustion patterns.

`IHttpClientFactory` provides:

- Managed handler lifetimes.
- Connection reuse.
- Named/typed clients.
- Centralized configuration.
- Integration with resilience policies.

It does **not** mean every call creates a brand-new network connection.

The factory manages the underlying handlers/connections while giving application code clean client instances.

---

## 85. How would you add retries, timeouts, and a circuit breaker to outbound calls, and where can retries make an outage worse?

Use a resilience pipeline with:

- Timeout.
- Retry with exponential backoff + jitter.
- Circuit breaker.
- Concurrency/bulkhead controls where appropriate.

Ordering matters because each policy has a different purpose.

Retries should normally apply only to **transient** failures and ideally idempotent operations.

Retries can make an outage worse:

```text
Downstream overloaded
→ requests fail
→ clients retry
→ traffic multiplies
→ downstream becomes more overloaded
```

This is a retry storm.

Respect provider rate limits and use bounded retries.

---

## 86. When do `Span<T>`, `Memory<T>`, and pooled buffers meaningfully help, and when are they premature?

They help when profiling shows allocation/copying overhead is significant, especially in:

- Serialization.
- Parsing.
- Networking.
- High-throughput data processing.
- Large buffer transformations.

`Span<T>` provides a high-performance view over contiguous memory without necessarily allocating.

`Memory<T>` can cross async boundaries where `Span<T>` cannot.

`ArrayPool<T>` allows reusable buffers.

But these APIs increase complexity and can make code harder to reason about.

Do not introduce them because they "look faster." First measure allocation rate and CPU hotspots.

---

# TESTING, ARCHITECTURE AND MIGRATION

## 87. How would you write integration tests for an API without mocking away the thing you actually want to test?

Use an in-process test host such as `WebApplicationFactory<TEntryPoint>` for ASP.NET Core.

Test:

```text
HTTP request
→ middleware
→ routing
→ authentication/authorization
→ endpoint
→ real application services
→ controlled database
```

Use a real database engine when database behavior is important. A fake/in-memory provider can produce semantics different from production.

Mock only external boundaries where real integration is impractical:

- Payment provider.
- Third-party API.
- Email service.

The goal is to test the real composition of your application.

---

## 88. A dependency upgrade broke production but every test passed. What kind of test was missing?

Potentially several types:

- Compatibility/integration test.
- Contract test.
- End-to-end test.
- Upgrade-specific regression test.
- Production-like environment test.

If the dependency is a database driver, for example, unit tests may not catch differences in:

- SQL generation.
- Connection behavior.
- TLS.
- Transaction semantics.
- Performance.

The lesson is:

> Tests only protect behavior that they actually exercise.

For critical dependencies, test the real integration boundary.

---

## 89. You inherit a codebase with three competing patterns. What do you do in your first month?

Do not immediately rewrite it.

First:

1. Map architecture and dependencies.
2. Identify production-critical paths.
3. Identify why the three patterns exist.
4. Measure operational pain.
5. Find high-risk duplication.
6. Establish coding/architecture conventions.
7. Pick one preferred pattern for new code.
8. Migrate old code opportunistically.

Document:

```text
Current state
Target direction
Exceptions
Migration triggers
```

The goal is to stop architectural entropy from increasing before attempting to remove all historical variation.

---

## 90. Your team wants to adopt a new technology. How do you decide?

Evaluate it against explicit criteria:

- Business problem solved.
- Operational maturity.
- Team expertise.
- Security.
- Performance.
- Cost.
- Vendor/community health.
- Integration complexity.
- Migration/exit strategy.
- Long-term maintenance.
- Regulatory requirements.

Run a small proof of concept against a **realistic workload**.

Avoid:

```text
Technology is popular
→ therefore adopt
```

Prefer:

```text
Problem
→ requirements
→ options
→ evidence
→ decision
→ measurable success criteria
```

---

## 91. How do you decide which technical debt to pay down and which to leave?

Prioritize debt based on its business and operational cost.

High-priority debt often:

- Causes incidents.
- Blocks releases.
- Creates security risk.
- Causes repeated performance problems.
- Makes scaling expensive.
- Prevents necessary product changes.

Low-priority debt may be harmless and stable.

A useful model is:

```text
Priority = impact × frequency × risk × strategic relevance
```

Do not pay technical debt simply because the code is aesthetically unpleasant.

---

## 92. The architecture is wrong and a rewrite is off the table. What is your play?

Use **incremental architecture change**.

Strategies:

- Strangler pattern.
- Anti-corruption layer.
- Introduce seams around legacy components.
- Extract one bounded capability at a time.
- Replace infrastructure behind interfaces.
- Move new functionality to the target architecture.
- Stop adding new coupling.

For example:

```text
Legacy monolith
      ↓
Facade
 ┌────┴─────┐
Old module  New service/module
```

The objective is to make the system increasingly compatible with the desired architecture without requiring a risky big-bang rewrite.

---

## 93. How would you scale this service to ten times the traffic, and what breaks that did not break before?

Start by identifying current bottlenecks.

Potential failures at 10×:

- Database CPU/connections.
- Lock contention.
- ThreadPool pressure.
- Memory/GC.
- Cache capacity.
- Downstream rate limits.
- Network bandwidth.
- Queue depth.
- Hot partitions/keys.
- Load balancer capacity.
- Logging volume.

A useful approach:

```text
Current RPS
→ load test at 2×
→ 5×
→ 10×
→ observe first saturation point
```

Then scale the actual bottleneck.

Do not assume "add more application servers" works if all servers hammer one database.

---

## 94. You have a legacy .NET Framework monolith and a mandate to modernise. What is the plan?

First inventory:

- .NET Framework version.
- ASP.NET technology.
- WCF.
- Web Forms.
- Windows-only APIs.
- COM dependencies.
- Third-party libraries.
- Database coupling.
- Deployment model.
- Authentication.
- Background jobs.

Then choose a migration strategy.

A practical sequence:

1. Stabilize and add characterization tests.
2. Upgrade dependencies where possible.
3. Separate business logic from framework-specific code.
4. Introduce APIs/facades around legacy areas.
5. Migrate incrementally.
6. Move workloads to modern .NET where supported.
7. Replace unsupported technologies deliberately.
8. Run old and new paths together during transition.
9. Remove legacy components only after traffic has moved.

Do not start by mechanically changing the target framework and assuming the application is modernized.

---

## 95. What exists in .NET Framework with no modern .NET equivalent, and what does that mean for a migration estimate?

Examples of technologies that require significant redesign or replacement include:

- ASP.NET Web Forms.
- Some legacy ASP.NET System.Web infrastructure.
- WCF server hosting in the same form.
- Certain Windows-only APIs.
- Remoting.
- AppDomain-based patterns.
- Some legacy configuration/hosting assumptions.

The important point is that migration cost is driven by **technology coupling**, not line count.

A 200,000-line application with clean business logic may be easier than a 50,000-line application deeply coupled to System.Web, Web Forms, WCF, COM, and Windows services.

Therefore migration estimates should inventory dependencies and categorize them:

```text
Portable
Adaptable
Replace
Redesign
```

---

## 96. How do you keep a large codebase current across annual .NET releases without it becoming a project?

Make upgrades part of normal engineering.

Use:

- Centralized package versions.
- Automated dependency update tooling.
- CI compatibility testing.
- Regular upgrade windows.
- Small incremental upgrades.
- Runtime compatibility tests.
- Architecture decision records for major changes.
- Observability before and after upgrades.

Avoid waiting three or four major versions and then doing a massive upgrade.

A healthy approach is:

```text
Release N
→ upgrade
→ validate
→ release N+1
→ repeat
```

Keep deprecated APIs and unsupported packages visible through build warnings and dependency scanning.

---

## 97. Your team uses AI coding tools. How do you keep quality and architectural direction from sliding?

Treat AI as a **developer accelerator**, not an architectural authority.

Establish guardrails:

### 1. Architecture rules

Document:

- Dependency direction.
- Layer boundaries.
- Approved frameworks.
- Data access rules.
- Security requirements.
- API conventions.

### 2. Automated enforcement

Use:

- Build analyzers.
- Roslyn analyzers.
- Formatting.
- Unit/integration tests.
- Architecture tests where useful.
- Dependency vulnerability scanning.
- CI quality gates.

### 3. Human review

Review AI-generated code for:

- Correctness.
- Security.
- Concurrency.
- Resource lifetime.
- Error handling.
- Performance.
- Architectural fit.

### 4. Require tests

AI-generated code should still satisfy the same test standards as human-written code.

### 5. Control dependencies

Do not allow an AI tool to introduce arbitrary packages without review.

### 6. Protect secrets and sensitive code

Never paste credentials, production secrets, private keys, or sensitive customer data into an AI tool unless the organization's approved controls explicitly allow it.

The key principle is:

> AI can accelerate implementation, but architecture, risk acceptance, and engineering standards remain human responsibilities.

---

# QUICK INTERVIEW REFERENCE

## High-value principles to remember

### Runtime
- SDK builds; runtime executes.
- C# normally compiles to IL; JIT produces native code at runtime.
- Native AOT moves more compilation ahead of runtime.
- Trimming removes code that static analysis considers unreachable.

### Hosting
- `builder.Services` is configuration/registration.
- `Build()` finalizes the service provider and application.
- `Run()` starts the host.
- Kestrel is the ASP.NET Core HTTP server.

### Middleware
- Registration order matters.
- Request flows forward; response unwinds backward.
- Terminal middleware can short-circuit.
- Exception handling belongs early.
- Forwarded headers must be processed before consumers.

### DI
- Transient: short-lived/stateless.
- Scoped: request/unit-of-work lifetime.
- Singleton: application lifetime and must be thread-safe.
- Never accidentally capture scoped state in a singleton.

### EF Core
- Tracking is useful for updates.
- `AsNoTracking()` is useful for read-only workloads.
- Avoid N+1.
- Prefer projections for API read models.
- Use optimistic concurrency for collision detection.
- Batch large writes.

### Performance
- Measure before optimizing.
- p99 exposes tail latency.
- Low CPU + high latency often means waiting.
- ThreadPool starvation is frequently caused by blocking.
- Allocation reduction is often better than GC tuning.

### Distributed systems
- Design for retries and duplicates.
- Bound concurrency.
- Do not retry aggressively during outages.
- Use idempotency for retryable operations.
- Read-after-write consistency must be designed explicitly.

### Observability
- Metrics tell you **that** something is wrong.
- Traces help identify **where**.
- Logs explain **what happened**.
- Correlate everything with trace/request identifiers.

### Architecture
- Prefer incremental migration over big-bang rewrites.
- Pay down debt based on business/operational impact.
- Standardize patterns to reduce entropy.
- Choose technology based on workload and constraints, not popularity.

---

# Interview Answering Strategy

For senior/architect-level questions, a strong answer usually follows this structure:

1. **State the principle.**
2. **Explain how the runtime/framework actually behaves.**
3. **Give a short example.**
4. **Mention the failure mode or trade-off.**
5. **Explain what you would do in production.**

For example, instead of answering:

> "Use `AsNoTracking()` for performance."

A stronger answer is:

> "`AsNoTracking()` is appropriate for read-only queries because EF Core does not need to maintain entity state. It can reduce CPU and memory overhead, particularly for large result sets. The trade-off is that the returned entities are not automatically tracked, so changing one and calling `SaveChanges()` will not behave like a normal tracked unit of work. I would use it for read models/list endpoints and keep tracking for workflows that intentionally modify entities."

That style demonstrates **understanding, not memorization**.
