## FUNCTIONS

### Rationale

A single authoritative implementation of shared services prevents duplicate
code and makes existing functionality easy to discover.

### Responsibilities

- Eliminate duplicate code.
- Provide shared services.
- Encapsulate reusable algorithms.

### Explicitly Not Responsible For

- Runtime state.
- Configuration.
- Device data.
- Application workflow.

## Design

- A function provides a single, well-defined service.
- A function should normally contain no more than 15-20 lines of executable code, 
  excluding comments.  This is a design guideline, not a strict rule.
- If a function becomes difficult to understand, decompose it into helper functions.

## Naming

- Function names use camelCase.
- Function names begin with a verb.
- Function names describe the service they provide.
- Function names describe what they do, not how they do it.
- Avoid abbreviations unless they are common throughout the project.
- A function name should be understandable without reading its implementation.

## Global Functions

Global functions are published using `global.set()` and may be called from
any Node-RED Function node.

- Global function names shall be prefixed with `g_`.
- Global functions should provide reusable services needed by multiple parts
  of the application.Examples:
