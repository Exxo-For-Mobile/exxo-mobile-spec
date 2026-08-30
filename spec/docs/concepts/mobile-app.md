# MobileApp

## Definition

MobileApp is the framework-defined representation of a mobile
application's application-level runtime scope.

A MobileApp provides the root lifecycle boundary for
framework-managed resources and establishes the scope within which
application-level modules, components, and services operate.

## Requirements

A MobileApp MUST have a unique application identifier.

A MobileApp MUST expose an application lifecycle defined by the
Mobile Framework lifecycle contract.

A MobileApp MUST provide access to the application-level module
management mechanism.

A MobileApp MAY support modules being registered or loaded after
application initialization.

Platform-specific application mechanisms MUST NOT be considered
part of the platform-independent MobileApp contract.

## Responsibilities

...

## Lifecycle Semantics

...

## Dependencies

...

## Implementation Considerations

...