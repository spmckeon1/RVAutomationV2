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

---
