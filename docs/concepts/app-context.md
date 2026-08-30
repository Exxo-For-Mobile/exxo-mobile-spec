AppContext

**API Contract:** [`app-context.yaml`](../../spec/api/contracts/app-context.yaml)

Overview

"AppContext" represents the application-scoped context through which a "MobileApp" and its managed components access application-level runtime resources, configuration, modules, services, and environment information.

An "AppContext" is associated with a single "MobileApp" and provides access to resources and facilities that are scoped to that app.

Properties

"appId"

Identifies the app associated with the "AppContext".

The identifier MUST uniquely identify the app within the applicable runtime or deployment environment.

"appVersion"

Identifies the version of the app associated with the "AppContext".

The property MAY be unavailable when app version information is not provided by the app or runtime environment.

"metadata"

Contains application-defined descriptive attributes associated with the app represented by the "AppContext".

Metadata is intended to provide descriptive information and MUST NOT be treated as app configuration unless explicitly defined by another specification.

Operations

"getApp"

Returns the "MobileApp" associated with the "AppContext".

"getModuleRegistry"

Returns the application-level "ModuleRegistry" used to discover, access, and manage modules associated with the "MobileApp".

The behavior and lifecycle semantics of module management are defined by the "ModuleRegistry" and "Module" specifications.

"getServiceRegistry"

Returns the application-level "ServiceRegistry" used to discover and access services available within the "MobileApp".

The service discovery and resolution semantics are defined by the "ServiceRegistry" specification.

"getConfiguration"

Returns the application-level "Configuration" available to the "MobileApp" and its managed components.

The structure, sources, and precedence of configuration values are defined by the "Configuration" specification.

"getRuntimeEnvironment"

Returns information about the runtime environment in which the "MobileApp" is operating.

The runtime environment abstraction MUST remain independent of platform-specific app objects. Platform-specific environment information is defined by the applicable platform specification.

Scope

"AppContext" provides access to application-scoped facilities but does not itself define the behavior of the modules, services, configuration system, or runtime environment that it exposes.

Those facilities are defined by their respective specifications.

Related Specifications

- "MobileApp"
- "ModuleRegistry"
- "Module"
- "ServiceRegistry"
- "Configuration"
- "RuntimeEnvironment"
- App Lifecycle