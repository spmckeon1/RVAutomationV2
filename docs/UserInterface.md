# User Interface Architecture

## Purpose

The RVAutomation user interface provides a consistent, intuitive method for operating, monitoring, configuring, and maintaining the RVAutomation system.

The interface is organized around the responsibilities of the system rather than its implementation details. Users should naturally know where to go based on what they are trying to accomplish rather than how the software is implemented.

---

## Responsibilities

The user interface is responsible for:

- Presenting system status.
- Providing operational control of the coach.
- Providing access to individual device management.
- Providing access to common device infrastructure.
- Providing access to system configuration.
- Displaying alerts, notifications, and historical information.

### Not Responsible For

The user interface is not responsible for:

- Device control logic.
- System automation.
- Communications.
- Data persistence.
- Business logic.

These responsibilities belong to the appropriate EmbeddedInfrastructure or RVAutomation subsystems.

---

## Design Philosophy

The user interface is organized around four primary user activities:

- Operate the coach.
- Manage an individual device.
- Configure common device infrastructure.
- Configure the RVAutomation platform.

Each activity has its own area within the user interface.

Navigation should follow the user's intent rather than the internal implementation of the software. Users should be able to predict where functionality resides without understanding the underlying architecture.

The goal is to minimize navigation complexity while providing access to all system capabilities.

---

## Design Principles

### Operational and configuration functions are separated.

Operating the coach should not require navigating through configuration pages.

Configuration should not interfere with normal operation.

---

### Every device has its own management page.

Each EmbeddedInfrastructure device provides a dedicated page containing all information and controls related to that device.

---

### Common services are configured once.

Services shared by all EmbeddedInfrastructure devices are configured from a common location.

---

### Infrastructure is configured separately.

Node-RED and platform infrastructure are managed independently from the devices they support.

---

## Top Level Navigation

1. Dashboard

2. Devices
   - GPS
   - Windshield Shade
   - Router Fan
   - Air Compressor
   - Dining Light
   - ...

3. Device Infrastructure
   - Heartbeat
   - Logging
   - Registration
   - Statistics
   - Firmware
   - ...

4. System Configuration
   - MQTT
   - SMTP
   - Notifications
   - Storage
   - Network
   - ...

5. History

6. Logs

---

## Dashboard

### Purpose

The Dashboard provides the primary operational interface for the RVAutomation system.

### Responsibilities

- Display overall system status.
- Present information from multiple devices.
- Provide quick access to frequently used controls.
- Display system alerts and notifications.
- Navigate to detailed device pages.

### Not Responsible For

- Device configuration.
- Device diagnostics.
- Infrastructure configuration.
- System configuration.

---

## Devices

Each EmbeddedInfrastructure device has its own management page.

A device page contains all information, controls, and configuration associated with a single device.

### Responsibilities

A device page is responsible for:

- Displaying current device status.
- Providing device-specific commands.
- Viewing and modifying device configuration.
- Displaying live operational data.
- Displaying diagnostics.
- Displaying statistics.
- Displaying historical information.

### Not Responsible For

A device page is not responsible for:

- Configuring common infrastructure.
- Configuring platform services.
- Managing unrelated devices.

Typical information panels include:

- Status
- Commands
- Live Data
- Configuration
- Statistics
- Diagnostics
- History

Not every device implements every panel.

---

## Device Infrastructure

Device Infrastructure contains services that are common to all EmbeddedInfrastructure devices.

Typical services include:

- Heartbeat
- Logging
- Registration
- Statistics
- Firmware Management

These services are configured once and shared across all devices.

---

## System Configuration

System Configuration contains platform-wide configuration that supports the entire RVAutomation system.

Examples include:

- MQTT
- SMTP
- Notifications
- Storage
- Network
- Security

These settings affect the operation of the platform rather than any individual device.

---

## Pages

A page is the primary unit of navigation within the user interface.

Each page has a clearly defined responsibility and is composed of one or more information panels.

Pages should avoid mixing unrelated responsibilities.

---

## Information Panels

The fundamental building block of the user interface is the information panel.

Each panel has a single responsibility and presents one aspect of a page.

Panels may display information, accept user input, or both.

Examples include:

- Status
- Commands
- Configuration
- Live Data
- Statistics
- Diagnostics
- History

Pages are composed of one or more information panels.

Panels should be reusable whenever practical while remaining independent of the pages in which they are used.

---

## Architectural Goals

The user interface should:

- Be intuitive to navigate.
- Organize functionality by user responsibility.
- Separate operation from configuration.
- Encourage reuse through modular information panels.
- Scale naturally as additional EmbeddedInfrastructure devices are added.
- Remain independent of any specific user interface technology.