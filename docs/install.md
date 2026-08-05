# install.md

## Raspberry Pi OS

Use Raspberry Pi Imager.

Configure:

- Hostname: skye
- Username: admin
- SSH: Enabled
- Password Authentication
- Raspberry Pi Connect: Disabled

Install Raspberry Pi OS Desktop (64-bit).

---

## Update OS

```bash
sudo apt update
sudo apt full-upgrade -y
sudo reboot
```

---

## Install Node-RED

```bash
bash <(curl -sL https://raw.githubusercontent.com/node-red/linux-installers/master/deb/update-nodejs-and-nodered)
```

---

## Enable Node-RED

```bash
sudo systemctl enable nodered.service
sudo systemctl start nodered.service
```

Verify:

```bash
sudo systemctl status nodered.service
```

---

## Verify Versions

```bash
git --version
node-red --version
node -v
npm -v
```

---

## Installed Versions

- Git: 2.47.3
- Node-RED: 5.0.1
- Node.js: 22.23.1
- npm: 10.9.8

---

## Node-RED Configuration

- Projects: Enabled
- Function External Modules: Enabled
- Credential Encryption: Custom Key
- Git Repository: Initialized

---

## Project

- Project Name: RVAutomationV2
- Initial Repository: Git
- Branch: main

---

## Development Environment

Aliases:

Add all of the following aliases to `~/.bashrc`.

```bash
alias rv='cd ~/projects/RVAutomation'
alias gs='git status'
alias ga='git add .'
alias gc='git commit'
alias gl='git log --oneline --graph --decorate'
```

---
## Install Mosquitto

Install the MQTT broker and client utilities.

```bash
sudo apt update
sudo apt install mosquitto mosquitto-clients
```

Enable and start the Mosquitto service.

```bash
sudo systemctl enable mosquitto
sudo systemctl start mosquitto
```

Verify:

```bash
sudo systemctl status mosquitto
```

## Configure Mosquitto Security

Create the MQTT application account.

Note: Use the -c option only when creating the password file for the first time. 
Omitting it when adding additional users prevents the existing password file 
from being overwritten.

```bash
sudo mosquitto_passwd -c `/etc/mosquitto/passwd` curly
```

Set the password file ownership and permissions.

```bash
sudo chown root:mosquitto /etc/mosquitto/passwd
sudo chmod 640 /etc/mosquitto/passwd
```
**Important:** These ownership and permission settings are required because the 
Mosquitto service runs as the `mosquitto` user.

Create `/etc/mosquitto/conf.d/auth.conf`.

```
allow_anonymous false
password_file /etc/mosquitto/passwd
```

Restart the broker.

```bash
sudo systemctl restart mosquitto
```

Verify:

```bash
sudo systemctl status mosquitto
```

Configure the Node-RED MQTT Broker node using the `curly` account credentials.


## Create RVAutomation Log Directories

RVAutomation stores operational log files outside of the project directory. This keeps runtime data separate from the application source code and configuration files.

Create the RVAutomation log directory structure:

```bash
sudo mkdir -p /var/log/RVAutomation/syslog
```

Set the directory owner to the Node-RED user:

```bash
sudo chown -R admin:admin /var/log/RVAutomation
```

Restrict access to the owner:

```bash
sudo chmod -R 700 /var/log/RVAutomation
```

Verify the directory ownership and permissions:

```bash
ls -ld /var/log/RVAutomation
ls -ld /var/log/RVAutomation/syslog
```

Expected output:

```text
drwx------ admin admin ... /var/log/RVAutomation
drwx------ admin admin ... /var/log/RVAutomation/syslog
```

After installation, the directory structure should be:

```text
/var/log/
└── RVAutomation/
    └── syslog/
```

The current system log is stored in:

```text
/var/log/RVAutomation/syslog/syslog.jsonl
```

The `syslog` directory contains the current system log and its historical log files. Additional logging subsystems (for example, telemetry, audit, or statistics) may create their own subdirectories under `/var/log/RVAutomation` as future functionality is implemented.
