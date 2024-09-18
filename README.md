#!usr/bin/env python3
from asyncio import timeout
from ipaddress import ip_address
from tabnanny import verbose

import scapy.all as scapy
import optparse

def get_arguments():
    # Create a parse object
    parser = optparse.OptionParser()
    # Add option for IP or IP range (correcting syntax)
    parser.add_option("-t", "--target", dest="target", help="Enter the IP or IP range")
    # Parse arguments
    (options,arguments) = parser.parse_args()
    # Error if no ip address provided
    if not options.ip:
        parser.error("Please enter the IP Address or IP range")
    # Return the provided ip
    return options.ip

def scan(ip):
    # Create an ARP request object, which asks for the MAC address of the given IP
    arp_request = scapy.ARP(pdst=ip)
    # Create an Ethernet frame to broadcast the ARP request
    broadcast = scapy.Ether(dst="ff:ff:ff:ff:ff:ff")
    # Combine ARP request with broadcast
    arp_request_broadcast = broadcast/arp_request
    # Send the packet and receive responses
    answared_list = scapy.srp(arp_request_broadcast, timeout=1, verbose=False)[0]
    # Print a header for the output
    clients_list = []
    # Loop through all responses and print IP and MAC
    for element in answared_list:
        client_dict = {"ip": element[1].psrc, "mac":element[1].hwsrc }
        clients_list.append(client_dict)
    return clients_list

def print_result(results_list):
    print("IP\t\t\tMAC Address\n-----------------------------------------")
    for client in results_list:
        print(client["ip"] + "\t\t" + client["mac"])

ip_range = get_arguments()
scan_result = scan(ip_range)
print_result(scan_result)
