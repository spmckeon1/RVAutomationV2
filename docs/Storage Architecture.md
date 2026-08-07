# Storage Architecture

## Purpose

The Storage Architecture provides persistent storage services for the RVAutomation system.

Storage enables subsystems to preserve information across power cycles while remaining independent of the underlying storage technology.

---

## Responsibilities

### The Storage subsystem is responsible for:

- Providing persistent storage services.
- Reading stored information.
- Writing stored information.
- Managing the underlying storage media.
- Reporting storage availability.
- Detecting storage failures.

### The Storage subsystem is not responsible for:

- Configuration ownership.
- Runtime state ownership.
- Data validation.
- Business logic.
- Serialization format.
- User interface.

These responsibilities belong to the owning subsystem.

---

## Design Philosophy

Storage is a shared service.

Storage provides the ability to store and retrieve information but does not own the information it stores.

Subsystems remain the authoritative owners of their own persistent information.

---

## Ownership

Every subsystem owns its own persistent information.

The Storage subsystem stores and retrieves that information on behalf of the owning subsystem.

Storage never becomes the authoritative owner of stored information.

---

## Storage Lifetime

Stored information exists independently of subsystem execution.

Subsystems determine what information should be stored and when it should be restored.

Storage simply preserves that information.

---

## Storage Technologies

The Storage Architecture is independent of the underlying storage technology.

Possible implementations include:

- Internal Flash
- SD Card
- External Flash
- Network Storage
- Future storage technologies

Changing storage technology shall not require changes to subsystem architecture.

---

## Availability

Storage may not always be available.

Subsystems should tolerate temporary storage failures whenever practical.

The inability to access storage should not necessarily prevent normal device operation.

---

## Startup

During initialization, storage services become available before subsystems requiring persistent information begin normal operation.

Subsystems restore their own persistent information after storage becomes available.

---

## Failure Handling

Storage failures shall be reported to the requesting subsystem.

The requesting subsystem determines the appropriate recovery action.

Possible responses include:

- Retry the operation.
- Use default values.
- Continue operating with reduced functionality.
- Enter a fault condition.

---

## Data Integrity

Storage preserves information.

Validation of stored information remains the responsibility of the owning subsystem.

Storage assumes no knowledge of the meaning or correctness of the information it stores.

---

## Shared Information

When multiple subsystems require access to the same persistent information, one subsystem remains the authoritative owner.

Storage does not establish ownership relationships.

---

## Architectural Goals

The Storage Architecture should:

- Preserve subsystem ownership.
- Separate storage from ownership.
- Remain independent of storage technology.
- Support autonomous device operation.
- Provide reliable persistent storage services.
- Minimize coupling between subsystems.