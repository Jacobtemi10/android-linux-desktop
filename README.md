
# Android Linux Desktop

Run a complete Debian XFCE graphical desktop on an Android smartphone without rooting the device.

## Project Overview

This project demonstrates how to transform an Android smartphone into a lightweight Linux workstation using:

- Termux
- Proot-Distro
- Debian Linux
- XFCE Desktop Environment
- Termux:X11

The installation runs alongside Android without replacing the existing operating system.

## Hardware Specifications

| Component | Specification |
|---|---|
| Device | Infinix X693 |
| Android | Android 11 |
| RAM | 6GB |
| Storage | 128GB |
| Linux Distribution | Debian |
| Desktop | XFCE |
| Display | Termux:X11 |

## Architecture

Android → Termux → Proot-Distro → Debian → XFCE → Termux:X11

## 1. Install Termux

Download Termux from:

https://github.com/termux/termux-app/releases

## 2. Configure Termux repositories

```bash
pkg update && pkg upgrade -y
pkg install x11-repo -y
pkg install proot-distro -y
pkg install termux-x11-nightly -y
```

Install the Termux:X11 Android application from:

https://github.com/termux/termux-x11/releases

## 3. Install Debian

```bash
proot-distro install debian
```

Log into Debian:

```bash
proot-distro login debian
```

## 4. Install XFCE

Inside Debian:

```bash
apt update && apt upgrade -y
apt install xfce4 xfce4-goodies xfce4-session dbus-x11 -y
```

Install additional desktop utilities:

```bash
apt install x11-xserver-utils xfce4-terminal thunar mousepad -y
```

## 5. Start Termux:X11

Exit Debian:

```bash
exit
```

Start the X11 server from Termux:

```bash
termux-x11 :0 &
```

Open the Termux:X11 Android application.

## 6. Launch Debian Desktop

Return to Termux:

```bash
proot-distro login debian --shared-tmp
```

Set the display:

```bash
export DISPLAY=:0
export XDG_RUNTIME_DIR=/tmp
```

Start XFCE:

```bash
dbus-launch --exit-with-session xfce4-session
```

The XFCE graphical desktop should now appear in Termux:X11.

## 7. Install Linux Applications

Update Debian:

```bash
apt update
```

Install applications:

```bash
apt install firefox-esr geany git python3 python3-pip curl wget -y
```

## 8. Troubleshooting

### Termux:X11 command not found

```bash
pkg install x11-repo
pkg install termux-x11-nightly
```

### X11 server already running

Avoid starting multiple X11 server instances. Keep the existing server running.

### XFCE session not found

```bash
apt install xfce4-session xfce4 -y
```

### Desktop does not appear

Check that:
- Termux:X11 is running.
- The display is set to `:0`.
- Debian was launched with `--shared-tmp`.
- XFCE packages are installed.

## Project Status

- [x] Termux installation
- [x] Debian installation
- [x] XFCE installation
- [x] Termux:X11 installation
- [x] Graphical desktop successfully launched
- [ ] Linux application installation
- [ ] Desktop optimization
- [ ] Performance testing

## Objective

Build a functional Linux workstation on Android for programming, system administration, development and everyday desktop computing.

## License

MIT License
