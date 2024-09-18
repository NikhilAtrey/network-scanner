# Network Scanner

## Overview

This Python script scans a local network to identify devices by their IP and MAC addresses using ARP (Address Resolution Protocol) requests. It's designed to be simple and effective for network discovery.

## Features

- **Scan a Local Network**: Identify devices connected to your local network by their IP and MAC addresses.
- **Support for IP Ranges**: Allows scanning a range of IP addresses.
- **Command-Line Interface**: Easy to use with command-line arguments.

## Installation

1. **Install Python 3**: Ensure Python 3 is installed on your system.
2. **Install Required Libraries**: Use pip to install the `scapy` library.
   ```bash
   pip install scapy
## Usage

- Save the Script: Save the provided script as network_scanner.py.
- Run the Script: Execute the script from the command line with the target IP or IP range.
   ```bash
  python network_scanner.py -t <target_ip>
- Replace <target_ip> with the IP address or range you want to scan (e.g., 192.168.1.1 or 192.168.1.0/24).

##Example
- **python network_scanner.py -t 192.168.1.0/24**
- This command will scan the IP range 192.168.1.0/24 and display the IP and MAC addresses of all devices found.
- IP: 192.168.1.2    MAC: 00:14:22:01:23:45
- IP: 192.168.1.5    MAC: 00:15:5D:3A:4F:88


## Code Explanation
- **get_arguments()**: Uses argparse to parse command-line arguments and retrieve the target IP or range. 
- **scan(ip)**: Sends ARP requests to the provided IP range and collects responses. Each response contains the IP and MAC address of a connected device.
- **print_result(results_list)**: Outputs the results in a tabular format, listing IP and MAC addresses of discovered devices.

