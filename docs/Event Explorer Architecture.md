# Event Explorer Architecture

## Purpose

The Event Explorer is an application that consumes `LogEvent` and presents them to the user for monitoring, debugging, diagnostics, and analysis. It does not create, modify, store, or transmit events. It presents `LogEvent` in a manner that allows users to efficiently understand and analyze system activity.

## Responsibilities

### The Event Explorer IS responsible for:

- Consuming LogEvent objects
- Presenting events in a human-readable format
- Searching events
- Filtering events
- Sorting events
- Correlating events
- Displaying event details

### The Event Explorer is NOT responsible for:

- Creating events
- Assigning sequence numbers
- Writing log files
- Sending MQTT
- Generating alerts
- Modifying events
- Interpreting the meaning of events

## Event Sources

The Event Explorer is source-agnostic. It does not depend on the origin of a `LogEvent`. Its only requirement is that each event conforms to the `LogEvent` specification. All searching, filtering, sorting, and presentation are performed solely on the contents of the `LogEvent`.

## User Questions

- What is happening right now?
- What happened before this error?
- Show me everything from GPS.
- Show me only warnings.
- What happened between sequence 1200 and 1300?
- What happened during boot?
- Find all MQTT events.
- Show me all events containing "timeout".
- Show me everything that happened on one device during this boot

## Version Roadmap

### Version 1 — Event Viewing

- Live display
- Search
- Filter
- Pause
- Clear
- Expand event

### Version 2 — Event Analysis

- Multiple sources
- Saved filters
- Timeline
- Statistics

### Version 3 — Event Intelligence

- Correlation
- Performance graphs
- Boot analyzer