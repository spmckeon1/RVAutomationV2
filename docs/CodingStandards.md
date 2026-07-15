# Coding Standards

---

## Source Files

- Use UTF-8 encoding.
- Use LF (`\n`) line endings.
- End every text file with a newline.
- Remove trailing whitespace.

---

## Naming

- Constants use UPPER_CASE.
- Object names use camelCase.
- Function names use camelCase.
- File names use descriptive names.

---

## Constants

CONSTANTS are values that may be changed by the developer or administrator,
but only intentionally as part of the system's design. They are not runtime
preferences.

Use CONSTANTS to:

- Eliminate magic numbers.
- Centralize design parameters.
- Define protocol values.
- Define default system behavior.

Do not use CONSTANTS for:

- Runtime state.
- User preferences.
- Frequently changing operational values.

---

## Architecture

- Shared functionality belongs in utilities.
- Avoid duplicated code.

---

## Git

- Commit one logical change at a time.
- Use descriptive commit messages.
- Test changes before committing.

---

## Documentation

- Document architectural decisions.
- Keep documentation synchronized with implementation.

---

## Guiding Principles

- Configuration is separate from runtime state.
- Every piece of data has a single authoritative owner.
- Consumers read authoritative data; they do not redefine or duplicate it.
- Functionalize repetitive code.
- Keep non-repetitive code as simple as possible.
- Prefer clarity over cleverness.
