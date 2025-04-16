# VPN Auto Deployment Script (Sample Project for GitHub)

import os
import subprocess

# VPN configuration details
vpn_name = "RemoteVPN"
server_ip = "vpn.example.com"
username = "user123"
password = "your_password_here"  # NOTE: In production, use secure credential storage

# Linux command to add a VPN connection using strongSwan or OpenVPN (for example purposes)
def create_vpn():
    print("Creating VPN connection profile...")
    try:
        # Create a .ovpn config file or add credentials to a VPN manager
        config = f"""
        client
        dev tun
        proto udp
        remote {server_ip} 1194
        resolv-retry infinite
        nobind
        persist-key
        persist-tun
        remote-cert-tls server
        auth-user-pass auth.txt
        cipher AES-256-CBC
        verb 3
        """

        with open("remotevpn.ovpn", "w") as f:
            f.write(config)

        with open("auth.txt", "w") as f:
            f.write(f"{username}\n{password}")

        print("VPN configuration files created successfully.")
        print("You can now use a VPN client to connect using remotevpn.ovpn")

    except Exception as e:
        print(f"Error creating VPN config: {e}")


if __name__ == "__main__":
    create_vpn()
