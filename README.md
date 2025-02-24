# OpenVPN Client Configuration for IPVanish

## Overview
This repository contains an OpenVPN client configuration file for connecting to IPVanish VPN servers using the UDP protocol on port 1194. The configuration includes multiple remote servers for redundancy and failover.

## Configuration Details

- **Protocol**: UDP
- **Port**: 1194
- **Tunnel Mode**: TUN
- **Remote Selection**: Randomized among available servers
- **Authentication**: Username and password stored in `/vpn/vpn.auth`
- **Certificate Authority (CA)**: Located at `/vpn/ca.ipvanish.com.crt`
- **Cipher**: AES-256-CBC (alternative: AES-128-GCM)
- **Authentication Algorithm**: SHA256
- **TLS Version**: Minimum 1.2
- **TLS Cipher**: Multiple ciphers supported (see configuration)

## Server List
The configuration includes multiple servers from different locations to ensure connectivity and redundancy. Some of the available locations:

- **Bod** (Bordeaux, France)
- **Mrs** (Marseille, France)
- **Par** (Paris, France)
- **Fra** (Frankfurt, Germany)
- **Dub** (Dublin, Ireland)
- **Bru** (Brussels, Belgium)
- **Ams** (Amsterdam, Netherlands)
- **Lon** (London, UK)

## Connection Settings
- **Reconnect Behavior**: Infinite retries on failure (`resolv-retry infinite`)
- **Keepalive Interval**: 10 seconds (600s timeout)
- **Compression**: LZO enabled
- **Persistence**:
  - Keep session keys (`persist-key`)
  - Keep tunnel active (`persist-tun`)
- **Security**:
  - `auth-nocache` to avoid storing authentication credentials in memory
  - `remote-cert-tls server` for server verification

## Installation & Usage
1. Install OpenVPN on your system (Linux, macOS, Windows, or Synology NAS).
2. Place the configuration file in your OpenVPN configuration directory (e.g., `/etc/openvpn/client/` on Linux).
3. Create a file `/vpn/vpn.auth` containing your IPVanish username and password:
   ```
   your_username
   your_password
   ```
4. Start the VPN connection:
   ```sh
   sudo openvpn --config /path/to/your/config.ovpn
   ```
5. Verify connection status using:
   ```sh
   curl ifconfig.me
   ```
   This should return an IP address from the VPN provider.

## Troubleshooting
- Increase verbosity (`verb 5`) for detailed logs.
- Ensure your CA certificate file is correctly placed at `/vpn/ca.ipvanish.com.crt`.
- Check if your credentials in `/vpn/vpn.auth` are correct.
- Restart your OpenVPN service if necessary:
  ```sh
  sudo systemctl restart openvpn-client@your_config
  ```

## Disclaimer
Use this configuration at your own risk. Ensure you comply with IPVanish's terms of service and legal regulations in your jurisdiction.

