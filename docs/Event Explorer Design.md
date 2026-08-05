# Event Explorer Design

## Purpose

## Inputs

- MQTT Live Stream
- Boot Log File
- Log File
- Replay File

## Outputs

Human-readable event display

- Filtered event list

- Search results

- Event detail view

- Export (future?)

## Major Components

- Input Manager

- Event Store

- Search Engine

- Filter Engine

- Display Engine

- Detail View

## Data Flow

LogEvent Source
        │
        ▼
 Input Manager
        │
        ▼
 Event Store
        │
 ┌──────┴─────────┐
 ▼                ▼
Search         Filter
        │
        ▼
 Display Engine
        │
        ▼
      User

## Internal Data Structures

## User Interface

## Future Enhancements