# ModuleRegistry

**API Contract:** [`module-registry.yaml`](../../spec/api/contracts/module-registry.yaml)

## Overview

"ModuleRegistry" provides application-level registration, discovery, access, and runtime loading management for "Modules" associated with a "MobileApp".

A "ModuleRegistry" maintains the set of "Module"s known to the app and provides operations for making registered "Module"s available to the runtime.

Registration and loading are separate operations. Registering a "Module" does not implicitly load its implementation.

## Registration

A "Module" becomes known to the app when it is registered with the "ModuleRegistry".

A registered "Module":

- has been added to the registry;
- can be discovered through the registry;
- can be retrieved using its identifier; and
- does not necessarily have its implementation loaded into the runtime.

Registering a "Module" MUST NOT implicitly load the "Module".

A "Module" MAY remain registered without being loaded. This allows tooling and runtime systems to identify "Module"s that are registered but not currently used.

## Loading

Loading makes a registered "Module" available to the runtime.

A "Module" MUST be registered before it can be loaded through the "ModuleRegistry".

Loading a "Module" MUST NOT be interpreted as equivalent to initializing or starting the "Module". "Module" initialization and activation are governed by the "Module" lifecycle specification.

A loaded "Module" MAY subsequently be unloaded while remaining registered.

## "Module" States

The registry distinguishes between the registration and runtime availability of a "Module".

At a conceptual level, a "Module" may progress through states such as:

Registered
    │
    │ load
    ▼
Loaded
    │
    │ initialize
    ▼
Initialized
    │
    │ start
    ▼
Active

The complete "Module" lifecycle and the semantics of initialization and activation are defined by the "Module" and "Module" lifecycle specifications.

## Operations

### "registerModule"

Registers a "Module" with the registry, making the "Module" known and accessible through the registry without loading its implementation into the runtime.

### "unregisterModule"

Removes a "Module" from the registry.

A "Module" SHOULD NOT be unregistered while it remains loaded or active. The exact requirements for removing a "Module" from the registry are defined by the "Module" lifecycle specification.

### "getModule"

Retrieves a registered "Module" using its identifier.

If no registered "Module" matches the requested identifier, the operation returns no "Module".

### "getModules"

Retrieves the "Module"s currently registered with the registry.

The returned collection represents registered "Module"s and MUST NOT be interpreted as a list of currently loaded "Module"s.

### "loadModule"

Loads a registered "Module" and makes its implementation available to the runtime.

Loading a "Module" does not, by itself, imply that the "Module" has been initialized or activated.

### "unloadModule"

Unloads a loaded "Module" and releases the resources associated with its runtime availability.

Unloading a "Module" does not necessarily remove its registration. A successfully unloaded "Module" MAY remain registered and may subsequently be loaded again.

## Scope

A "ModuleRegistry" operates within the app scope of the "MobileApp" from which it is obtained.

The registry manages "Module" registration and runtime loading but does not define the internal behavior of individual "Modules".

## Responsibilities

"ModuleRegistry" is responsible for:

- maintaining registered "Modules";
- providing "Module" discovery and retrieval;
- loading registered "Module"s;
- unloading loaded "Module"s; and
- maintaining the distinction between "Module" registration and runtime availability.

"ModuleRegistry" is not responsible for defining:

- the internal implementation of a "Module";
- "Module" initialization behavior;
- "Module" activation behavior;
- "Module"-specific business logic; or
- the mechanism used internally to load a "Module".

## Implementation Independence

The mechanism used to load a "Module" is an implementation detail.

An implementation MAY use a class loader, package system, dynamic library, dependency injection mechanism, filesystem resource, or another mechanism to make a "Module" available to the runtime.

The "ModuleRegistry" contract defines the observable "Module" management behavior and does not require a particular loading mechanism.

## Related Specifications

- "MobileApp"
- "ApplicationContext"
- "Module"
- Module Lifecycle