# Architecture

Defines the high-level architecture and design principles of the RV Automation V2 system.

This document describes the intended design of the system. Detailed implementation belongs 
in the source code. Architectural decisions are documented here before they are implemented.

EVERY MAJOR ENTRY MUST HAVE THESE SECTIONS WHEN THEY ARE ENTERED:
## <Topic>
### Decision
### Responsibilities
### Explicitly Not Responsible For
### Rationale

Architectural decisions should be documented before implementation.

The architecture should be driven by implementation experience, not speculation.

---

## Architectural Principles

Every external device or system is represented by exactly one Node-RED Service.

### Ownership

Every subsystem is the authoritative owner of its own configuration, runtime state, and statistics.

No other subsystem may directly modify information owned by another subsystem.

Subsystems communicate through published interfaces and events.

---

### Autonomous Devices

Devices are authoritative over their own behavior.

External systems may request actions but cannot compel them.

Every device validates requests against its current configuration, runtime state, and current operating conditions before deciding whether to act.

A device may accept, defer, modify, or reject a requested action based on its own operating rules.

Devices should continue operating correctly whenever practical, even when external systems are unavailable.

## Design Goals

- Every piece of shared information shall have a single authoritative owner.

- Ownership belongs to the object responsible for maintaining the correctness
  of the information throughout its lifetime.

- Creating or initializing information does not imply ownership. Ownership
  belongs to the object that subsequently maintains the information.

- Application constants define values that are expected to remain unchanged during normal 
  operation. Modifying these values constitutes a software change.

- Application configuration contains administrator-configurable values that customize 
  system behavior without changing application logic.

- The device repository maintains the authoritative runtime representation of all physical 
  and logical devices.

---

## Startup

### Decision

The Startup flow is responsible for constructing the global application environment.

### Responsibilities

- Define and initialize the global CONSTANTS object.
- Define and initialize the global CONFIG object.
- Define and initialize the global UTILS object.
- Define and initialize the global DEVICES object.
- Initialize shared infrastructure.
- Validate application configuration.
- Signal that application initialization is complete.

### Explicitly Not Responsible For

- Populate device global objects
- Monitoring device health.
- Processing device messages.
- Executing device logic.
- Managing device runtime state.
- Performing timer evaluation.

### Rationale

The startup flow is device-agnostic. New devices can be added without modifying 
the startup flow, improving modularity and maintainability.

---


## Global Objects

### Object Modeling

Every object in the application's global model shall represent either:

- A distinct entity, or
- A distinct responsibility.

Objects shall not be introduced solely as containers for unrelated values or to reserve space 
for possible future expansion.

When a distinct entity or responsibility is identified, it should be represented explicitly, 
even if it initially contains only a single member. This establishes a stable object model 
and minimizes future structural changes.

---

## Devices

"Each object under `devices` represents one external hardware controller. The structure 
within that object models the resources, state, and capabilities owned by that controller."

---

## Standard Service Lifecycle

Every service should define:

### Initialization
- Perform startup initialization.
- Load persistent configuration.
- Initialize runtime state.

### Receive <Primary Event>
- Process the primary event handled by the service.

### Timer_tick
- Perform periodic maintenance and time-based processing.
        
## Logging Service

### Decision

The Logging Service is the authoritative service responsible for
collecting and maintaining all runtime log entries.

### Responsibilities

- Receive log entries
- Validate log entries
- Maintain the in-memory circular buffer
- Provide access to recent log entries

### Explicitly Not Responsible For

- Dashboard display
- File storage
- Log rotation
- Searching
- Filtering

### Rationale

The Logging Service provides a single authoritative interface for
runtime logging. By separating log producers from log consumers,
additional consumers (Dashboard, file writer, MQTT publisher, etc.)
can be added without modifying the code that generates log events.

### Implementation Notes

The Logging Service defines a canonical `LogEvent` structure used by all
log producers. Producers create and populate `LogEvent` instances before
submitting them to the Logging Service.

---

## Notifications

---

## Timers

---

## Error Handling

---

## Configuration Management

---

## Future Enhancements