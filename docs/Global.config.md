# CONFIG

global.config is a runtime application object, not a bootstrap mechanism.

## Decision

The global.config object provides centralized access to configuration items 
that define the behavior of RV Automation V2. Configuration items are 
expected to change infrequently and are typically modified only during 
installation, maintenance, or system customization.

## Responsibilities

- Provide centralized access to configuration items.
- Load configuration during system startup.
- Validate configuration before making it available.
- Present a consistent interface for accessing configuration data.
- Isolate consumers from the physical storage of configuration data.

## Explicitly Not Responsible For

- Runtime device state.
- System constants (`global.CONSTANTS`).
- Temporary runtime data.
- Device communications.
- Calculated or derived values.

## Rationale

Configuration is a shared system resource used by many components throughout RV 
Automation V2. Centralizing access through `global.config` provides a single 
authoritative source for configuration data, promotes consistency, and isolates 
the rest of the system from how configuration is stored or loaded.

By separating configuration from runtime state and system constants, each global 
object has a well-defined responsibility, resulting in a simpler and more 
maintainable architecture.