# Logging Service

This document describes the design and implementation of the Logging
Service.

The service is responsible for receiving runtime log events,
maintaining the in-memory log buffer, and providing log events to
consumers.

The architectural role of the service is documented in
Architecture.md.

                    Log Producers
                         |
          +--------------+--------------+
          |                             |
      External                      Internal
       (MQTT)                       (Link In)
          |                             |
          +--------------+--------------+
                         |
                         V
                  Logging Service
                         |
          +--------------+--------------+
          |              |              |
          V              V              V
      Validate      Normalize      Buffer
                         |
                         V
                  Log Consumers
          +--------------+--------------+
          |              |              |
          V              V              V
      Dashboard     File Writer      Future 

 
       Figure 1. Logging Service Data Flow

---

## Design Goals

- Provide a single logging interface for all runtime components.
- Separate log producers from log consumers.
- Maintain a bounded in-memory log buffer.
- Allow additional consumers to be added without modifying log producers.
- Provide a consistent LogEvent structure throughout the application.

---

## Interfaces

The service accepts LogEvents through two interfaces.

### MQTT Interface

External devices submit LogEvents using the documented MQTT topics.

### Internal Interface

Internal Node-RED flows submit LogEvents through the Link In interface.

No other write interfaces are supported.

---

## LogEvent

Every LogEvent submitted to the service shall contain the
following elements.

| Element | Required | Description |
|---------|:--------:|-------------|
| timestamp | Yes¹ | Time the event occurred. |
| source | Yes | Producer-supplied source identifier. |
| criticality | Yes² | Indicates the importance of the event. |
| message | Yes | Human-readable log message. |

¹ If not supplied, the service assigns the current date and time.

² If not supplied, the service determines the criticality from
the message prefix or assigns the default criticality.

---

## LogEvent Validation

The service validates every LogEvent received through its
supported interfaces.

Validation includes, but is not limited to:

- Verifying required elements.
- Assigning a timestamp if one is not supplied.
- Determining the event criticality.
- Discarding undefined LogEvent elements.

---

## Normalization

The service normalizes accepted LogEvents into the canonical
LogEvent format before they are committed to the in-memory buffer.

Normalization may include:

- Assigning default values.
- Determining criticality.
- Removing recognized message prefixes.
- Discarding undefined elements.

---

## Producer Identity

The service accepts the producer-supplied `source` value without
verification.

It is the responsibility of the producer to provide a meaningful and
consistent source identifier.

The service does not authenticate producers or guarantee source
uniqueness.

---

## Criticality

The service recognizes a set of standard criticality prefixes
when they appear at the beginning of a log message.

| Prefix | Criticality |
|---------|-------------|
| ERROR:  | ERROR |
| WARN:   | WARNING |
| INFO:   | INFO |
| DEBUG:  | DEBUG |

If a recognized prefix is present, the service shall assign the
corresponding criticality and remove the prefix from the stored message.

If no recognized prefix is present, the service shall assign the
default criticality of INFO.

---

## In-Memory Buffer

The service maintains a bounded in-memory circular buffer containing
the most recent LogEvents.

The buffer is owned exclusively by the service. Producers and
consumers shall not directly access or modify the buffer.

When the configured buffer capacity is reached, the oldest LogEvent is
discarded as each new LogEvent is accepted.

The buffer provides the authoritative source of LogEvents for all
consumers.

---

## Dashboard Interface

The Dashboard is a consumer of the Logging Service and provides a
real-time view of recent LogEvents.

Implementation details are TBD.

---

## Future Enhancements

The following capabilities are anticipated but are not part of the
initial implementation.

- Dashboard viewer
- File logging
- Log rotation
- Search
- Filtering
- Download/export
- Remote log streaming

---