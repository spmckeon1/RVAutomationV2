# Config

## Decision

The `global.config` object provides centralized access to configuration items that 
define the behavior of RV Automation V2 and change infrequently.

## Responsibilities

- Provide centralized access to application configuration.
- Load and validate configuration during startup.
- Present a consistent interface for accessing configuration data.
- Isolate consumers from the underlying configuration storage.

## Explicitly Not Responsible For

- Bootstrap configuration.
- Runtime device state.
- System constants (`global.CONSTANTS`).
- Temporary runtime data.
- Device-specific configuration.

## Rationale

Configuration is a shared system resource used by many components throughout 
RV Automation V2. Centralizing access through `global.config` provides a single 
authoritative source for configuration data, promotes consistency, and isolates 
the rest of the system from how configuration is stored or loaded.

By separating configuration from runtime state and system constants, each global 
object has a well-defined responsibility, resulting in a simpler and more 
maintainable architecture.