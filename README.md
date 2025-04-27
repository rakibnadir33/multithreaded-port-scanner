This is a lightweight Python script designed to scan open ports on a target IP address.
It uses multithreading to scan multiple ports simultaneously, making the process faster than traditional single-threaded scanners.
The script includes basic input validation and simple error handling, making it beginner-friendly for CTF challenges, basic network testing, or learning socket programming.

Features:

1.Fast multithreaded port scanning
2.Input validation for IP addresses and port ranges
3.No external libraries required
4.Easy to understand and modify

Usage : python3 port_scanner.py

Enter the IP address: 192.168.1.1
Enter the start port: 20
Enter the end port: 100



The scanner will check the specified port range and print any open ports it finds.
