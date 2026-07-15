## Device Organization

Each object under devices represents one physical or logical device that has a 
single authoritative runtime representation within the application.

Each device is the sole owner of the information stored within its entry in
`global.devices`. Information not owned by the device shall not be stored within
that device's entry.

Application-wide information belongs in either `global.CONSTANTS` or
`global.config`.

A device may contain one or more of the following components:

- config - Device-specific configuration.
- state - Runtime state.
- monitor - Device monitoring information.
- timer - Timer-related information.
- Additional components may be added when they represent a distinct responsibility.

Not every device is required to implement every section. A device should contain
only those sections necessary to support its responsibilities.

###
## Responsibilities

- Maintain the application's authoritative representation of every physical and logical device.
- Provide a consistent interface for accessing device information.
- Maintain device-specific information.
- Support optional device subsystems (for example, `monitor` and `timer`) as required by each device.
- Enable generic application logic to operate across multiple device types.

### Design Checklist