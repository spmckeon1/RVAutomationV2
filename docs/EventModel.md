# Event Model

## Purpose

The Event Model defines how information moves throughout the RVAutomation system.

Events provide a common mechanism for communication between subsystems, devices, services, and user interface components while minimizing direct dependencies.

The goal is to allow each subsystem to operate independently while remaining responsive to changes occurring elsewhere in the system.

---

## Responsibilities

The Event Model is responsible for:

- Defining what constitutes an event.
- Defining how events are produced.
- Defining how events are consumed.
- Defining event ownership.
- Defining event lifetime.
- Promoting loose coupling between subsystems.

### Not Responsible For

The Event Model is not responsible for:

- Transport mechanisms.
- MQTT topics.
- Network protocols.
- Data persistence.
- Device configuration.
- Business logic.

These responsibilities belong to the appropriate subsystems.

---

## Design Philosophy

The architecture is event-driven.

Subsystems communicate by publishing events that describe something that has occurred.

Other subsystems may observe those events and respond if appropriate.

The publisher does not know who receives the event.

The consumer does not know who generated the event.

This separation minimizes coupling throughout the system.

---

## What Is an Event?

An event represents something that has already happened.

Examples include:

- GPS position updated.
- Heartbeat received.
- WiFi connected.
- Tank level changed.
- Configuration modified.
- Device started.
- Device stopped.
- Button pressed.
- Timer expired.

Events describe facts.

They do not describe intentions.

---

## Events Are Immutable

Once published, an event shall never be modified.

Consumers must treat events as read-only.

If additional information becomes available, a new event is published.

---

## Event Ownership

The subsystem that detects or creates a condition owns the publication of the corresponding event.

Examples:

- GPS publishes GPS events.
- Network publishes connection events.
- Storage publishes file system events.
- Logging publishes logging events.
- User Interface publishes user interaction events.

Ownership should never be ambiguous.

---

## Event Consumers

Any subsystem may subscribe to events.

Consumers determine whether an event is relevant.

Ignoring an event is considered normal behavior.

---

## Event Lifetime

Events are transient.

An event represents something that occurred at a specific point in time.

Events are not intended to represent current state.

Current state belongs to the subsystem that owns it.

---

## Events versus State

Events describe change.

State describes the current condition.

For example:

Event:

    GPS Position Updated

State:

    Current Latitude
    Current Longitude

An event may cause state to change, but the event itself is not the state.

---

## Events versus Commands

Commands request that something happen.

Events report that something has already happened.

Examples:

Command:

    Open Windshield Shade

Event:

    Windshield Shade Opened

Commands flow toward responsibility.

Events flow away from responsibility.

---

## Event Ordering

Events should be processed in the order they are received.

The architecture does not require global event ordering across the system.

Subsystems should not assume events arrive in chronological order unless guaranteed by the transport mechanism.

---

## Event Reliability

The Event Model does not require guaranteed delivery.

Individual transports may provide different reliability guarantees.

Subsystems should tolerate missed or duplicated events whenever practical.

---

## Event Naming

Event names should describe completed actions or observed changes.

Examples:

- HeartbeatReceived
- PositionUpdated
- ConfigurationChanged
- NetworkConnected
- StorageMounted

Names should represent facts rather than requests.

---

## Architectural Goals

The Event Model should:

- Promote loose coupling.
- Eliminate unnecessary subsystem dependencies.
- Scale as new devices are added.
- Support multiple transport mechanisms.
- Remain independent of implementation technology.
- Clearly separate events, commands, and state.