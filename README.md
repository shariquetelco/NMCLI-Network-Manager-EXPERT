# 🌐 NetworkManager NMCLI Complete Guide

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Linux](https://img.shields.io/badge/OS-Linux-blue.svg)](https://www.linux.org/)
[![NetworkManager](https://img.shields.io/badge/NetworkManager-Latest-green.svg)](https://networkmanager.dev/)
[![Terminal](https://img.shields.io/badge/Interface-CLI-red.svg)](https://en.wikipedia.org/wiki/Command-line_interface)
[![Version](https://img.shields.io/badge/Version-2.0-orange.svg)](https://github.com/ahmadsharique/networkmanager-guide)
[![Maintenance](https://img.shields.io/badge/Maintained%3F-yes-green.svg)](https://github.com/ahmadsharique/networkmanager-guide/graphs/commit-activity)

![NetworkManager Banner](https://images.unsplash.com/photo-1558494949-ef010cbdcc31?ixlib=rb-4.0.3&auto=format&fit=crop&w=1200&h=300&q=80)

## 📖 Overview

Welcome to the comprehensive NetworkManager guide! This repository serves as your complete handbook for mastering NetworkManager and its powerful command-line interface `nmcli`. Whether you're a system administrator, DevOps engineer, or Linux enthusiast, this guide will help you navigate the complexities of network management with confidence.

NetworkManager is the backbone of modern Linux networking, providing intelligent network configuration and seamless connectivity management. This guide covers everything from basic operations to advanced configurations.

## 🚀 Quick Start

![Quick Start](https://images.unsplash.com/photo-1516321318423-f06f85e504b3?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&h=200&q=80)

Get up and running with NetworkManager in minutes:

```bash
# Check NetworkManager status
nmcli general status

# View all network connections
nmcli connection show

# Connect to a Wi-Fi network
sudo nmcli device wifi connect "YourSSID" password "YourPassword"
```

## 📚 Table of Contents

- [🔌 Connection Management](#-connection-management)
- [💻 Device Operations](#-device-operations)
- [🌐 General Network Status](#-general-network-status)
- [📡 Network Controls](#-network-controls)
- [📻 Radio Management](#-radio-management)
- [🔧 Advanced Configuration](#-advanced-configuration)
- [💡 Best Practices](#-best-practices)

## 🔌 Connection Management

![Connection Management](https://images.unsplash.com/photo-1573804633927-bfcbcd909acd?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&h=200&q=80)

### 🔍 Viewing Connection Profiles

Display comprehensive information about your network connections:

```bash
# Show all connection profiles
nmcli connection show

# Display only active connections
nmcli connection show --active

# Show connection details with sensitive information
nmcli connection show --show-secrets

# View specific connection by name or UUID
nmcli connection show "Connection Name"
```

### ⚡ Activating Connections

Bring your network connections online:

```bash
# Activate connection by interface name
nmcli connection up ifname eth0

# Connect to specific Wi-Fi access point
nmcli connection up ifname wlan0 ap AA:BB:CC:DD:EE:FF

# Use password file for secure authentication
nmcli connection up ifname wlan0 passwd-file /path/to/passwords
```

### ⏹️ Deactivating Connections

Safely disconnect from networks:

```bash
# Deactivate connection by name
nmcli connection down "WiFi Connection"

# Deactivate by UUID
nmcli connection down uuid 12345678-abcd-1234-efgh-123456789abc
```

### ➕ Creating New Connection Profiles

Build custom network configurations:

#### 🖥️ Ethernet Configuration
```bash
# Create static IP ethernet profile
nmcli connection add \
    con-name "Office-Ethernet" \
    ifname eth0 \
    type ethernet \
    ip4 192.168.1.100/24 \
    gw4 192.168.1.1 \
    ipv4.dns "8.8.8.8,8.8.4.4"
```

#### 📶 Wi-Fi Configuration
```bash
# Create secure Wi-Fi profile
nmcli connection add \
    con-name "Home-WiFi" \
    ifname wlan0 \
    type wifi \
    ssid "MyHomeNetwork" \
    wifi-sec.key-mgmt wpa-psk \
    wifi-sec.psk "SuperSecurePassword123" \
    ip4 192.168.0.50/24 \
    gw4 192.168.0.1
```

#### 🌉 Bridge Configuration
```bash
# Create network bridge
nmcli connection add \
    con-name "VM-Bridge" \
    type bridge \
    ip4 192.168.100.1/24 \
    gw4 192.168.100.1

# Add interface to bridge
nmcli connection add \
    con-name "Bridge-Slave-eth0" \
    type bridge-slave \
    ifname eth0 \
    master "VM-Bridge"
```

### ✏️ Modifying Connection Properties

Update existing connections:

```bash
# Change IP address
nmcli connection modify "Connection Name" ipv4.addresses 192.168.1.200/24

# Add DNS server
nmcli connection modify "Connection Name" +ipv4.dns 1.1.1.1

# Remove DNS server
nmcli connection modify "Connection Name" -ipv4.dns 8.8.8.8
```

### 📋 Cloning Connections

Duplicate existing configurations:

```bash
# Clone connection profile
nmcli connection clone "Original-Profile" "New-Profile"

# Create temporary clone
nmcli connection clone --temporary "Base-Config" "Test-Config"
```

### 🗑️ Removing Connections

Clean up unused profiles:

```bash
# Delete connection by name
nmcli connection delete "Old-Connection"

# Delete by UUID
nmcli connection delete uuid 12345678-abcd-1234-efgh-123456789abc
```

### 🔄 Reloading Configurations

Refresh NetworkManager settings:

```bash
# Reload all connection files
nmcli connection reload

# Load specific configuration file
nmcli connection load /etc/NetworkManager/system-connections/my-connection.nmconnection
```

## 💻 Device Operations

![Device Operations](https://images.unsplash.com/photo-1558618666-fcd25c85cd64?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&h=200&q=80)

### 📊 Device Information

Monitor your network interfaces:

```bash
# Show all device details
nmcli device show

# Show specific device information
nmcli device show eth0

# Display device status summary
nmcli device status
```

**Status Output Example:**
```
DEVICE    TYPE      STATE         CONNECTION
eth0      ethernet  connected     Wired connection 1
wlan0     wifi      disconnected  --
lo        loopback  unmanaged     --
```

### ⚙️ Device Configuration

Control device behavior:

```bash
# Enable auto-connect for device
nmcli device set eth0 autoconnect yes

# Disable device management
nmcli device set wlan0 managed no

# Re-enable device management
nmcli device set wlan0 managed yes
```

### 🔗 Device Connections

Manage device connectivity:

```bash
# Connect device (auto-select best connection)
nmcli device connect eth0

# Disconnect device
nmcli device disconnect wlan0

# Temporarily modify device settings
nmcli device modify eth0 ipv4.addresses 192.168.1.150/24
```

### 🗑️ Device Removal

Remove software-defined interfaces:

```bash
# Delete bridge interface
nmcli device delete br0

# Remove bond interface
nmcli device delete bond0
```

*Note: Hardware devices cannot be deleted through nmcli*

## 📡 Wi-Fi Management

![Wi-Fi Management](https://images.unsplash.com/photo-1516321318423-f06f85e504b3?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&h=200&q=80)

### 🔍 Scanning Networks

Discover available Wi-Fi networks:

```bash
# List all available access points
nmcli device wifi list

# Scan specific interface
nmcli device wifi list ifname wlan0

# Force rescan
nmcli device wifi list --rescan yes

# Show specific BSSID
nmcli device wifi list bssid AA:BB:CC:DD:EE:FF
```

### 🔌 Connecting to Wi-Fi

Join wireless networks:

```bash
# Basic connection
sudo nmcli device wifi connect "NetworkName" password "Password123"

# Secure connection (password prompt)
sudo nmcli --ask device wifi connect "NetworkName"

# Connect to hidden network
sudo nmcli device wifi connect "HiddenSSID" password "Password123" hidden yes

# Connect with specific interface
sudo nmcli device wifi connect "NetworkName" password "Password123" ifname wlan0
```

### 🔥 Wi-Fi Hotspot

Create your own access point:

```bash
# Create basic hotspot
nmcli device wifi hotspot ifname wlan0 con-name "MyHotspot" ssid "MyNetwork" password "HotspotPassword"

# Advanced hotspot configuration
nmcli device wifi hotspot \
    ifname wlan0 \
    con-name "AdvancedHotspot" \
    ssid "DeviceAP" \
    band bg \
    channel 6 \
    password "SecurePassword123"
```

### 🔐 Wi-Fi Security

Manage wireless security:

```bash
# Show saved Wi-Fi password
nmcli device wifi show-password

# View connection security details
nmcli connection show "WiFi-Connection" | grep -i security
```

## 🌐 General Network Status

![Network Status](https://images.unsplash.com/photo-1451187580459-43490279c0fa?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&h=200&q=80)

### 📈 System Status

Monitor overall network health:

```bash
# Show general status
nmcli general status

# Compact status view
nmcli general
```

### 🔍 Connectivity Testing

Verify internet connectivity:

```bash
# Check connectivity status
nmcli networking connectivity

# Force connectivity check
nmcli networking connectivity check
```

**Connectivity States:**
- `none`: No network connection
- `portal`: Behind captive portal
- `limited`: Network connected, no internet
- `full`: Full internet access
- `unknown`: Cannot determine status

## 📻 Radio Management

![Radio Management](https://images.unsplash.com/photo-1573804633927-bfcbcd909acd?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&h=200&q=80)

### 📡 Radio Controls

Manage wireless radios:

```bash
# Show all radio status
nmcli radio all

# Enable/disable all radios
nmcli radio all on
nmcli radio all off

# Wi-Fi radio control
nmcli radio wifi on
nmcli radio wifi off

# Mobile broadband control
nmcli radio wwan on
nmcli radio wwan off
```

## 🔧 Advanced Configuration

![Advanced Config](https://images.unsplash.com/photo-1518709268805-4e9042af2176?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&h=200&q=80)

### 🏗️ Complex Network Setups

#### VLAN Configuration
```bash
# Create VLAN interface
nmcli connection add \
    type vlan \
    con-name "VLAN-100" \
    ifname eth0.100 \
    dev eth0 \
    id 100 \
    ip4 192.168.100.10/24
```

#### VPN Configuration
```bash
# Add OpenVPN connection
nmcli connection add \
    type vpn \
    con-name "Corporate-VPN" \
    vpn-type openvpn \
    vpn.data "remote=vpn.company.com,connection-type=tls"
```

#### Bond Configuration
```bash
# Create network bond
nmcli connection add \
    type bond \
    con-name "Bond-Connection" \
    ifname bond0 \
    bond.options "mode=active-backup,miimon=100"

# Add slave to bond
nmcli connection add \
    type ethernet \
    slave-type bond \
    con-name "bond-slave-eth0" \
    ifname eth0 \
    master bond0
```

## 💡 Best Practices

![Best Practices](https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&h=200&q=80)

### 🛡️ Security Guidelines

1. **Use strong passwords** for Wi-Fi connections
2. **Avoid plain text passwords** in commands (use --ask flag)
3. **Regularly update** connection profiles
4. **Monitor** network activity and connections
5. **Use VPN** for secure remote connections

### 🔧 Performance Tips

1. **Disable unused** network interfaces
2. **Use static IP** for servers and critical systems
3. **Configure proper DNS** servers
4. **Monitor connection** stability
5. **Keep NetworkManager** updated

### 📝 Configuration Management

1. **Backup** connection profiles regularly
2. **Use meaningful** connection names
3. **Document** complex configurations
4. **Test configurations** before deployment
5. **Version control** your network configs

## 🚨 Troubleshooting

![Troubleshooting](https://images.unsplash.com/photo-1573804633927-bfcbcd909acd?ixlib=rb-4.0.3&auto=format&fit=crop&w=800&h=200&q=80)

### 🔍 Common Issues

#### Connection Problems
```bash
# Restart NetworkManager service
sudo systemctl restart NetworkManager

# Check service status
sudo systemctl status NetworkManager

# View detailed logs
sudo journalctl -u NetworkManager -f
```

#### Wi-Fi Issues
```bash
# Reset Wi-Fi interface
sudo nmcli device set wlan0 managed no
sudo nmcli device set wlan0 managed yes

# Clear Wi-Fi cache
sudo nmcli device wifi rescan
```

#### DNS Resolution
```bash
# Check DNS configuration
nmcli device show eth0 | grep IP4.DNS

# Flush DNS cache
sudo systemctl restart systemd-resolved
```

## 📖 Additional Resources

- **Official Documentation**: [NetworkManager Documentation](https://networkmanager.dev/docs/)
- **Man Pages**: `man nmcli`, `man NetworkManager`
- **Community Forums**: [NetworkManager Users](https://mail.gnome.org/mailman/listinfo/networkmanager-list)
- **Bug Reports**: [GitLab Issues](https://gitlab.freedesktop.org/NetworkManager/NetworkManager/-/issues)

## 🤝 Contributing

We welcome contributions! Please read our contributing guidelines and submit pull requests for any improvements.

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👨‍💻 Author

**AHMAD SHARIQUE**
- 📧 Email: eshariq.am@gmail.com
- 🌐 GitHub: [@ahmadsharique](https://github.com/ahmadsharique)
- 💼 LinkedIn: [Ahmad Sharique](https://linkedin.com/in/ahmadsharique)

---

<div align="center">
  <p><strong>⭐ Star this repository if you found it helpful!</strong></p>
  <p>Made with ❤️ by Ahmad Sharique</p>
</div>
