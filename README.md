import socket
import threading

# Function to scan an individual port
def scan_port(ip, port):
    try:
        # Create a socket object
        sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        sock.settimeout(1)  # Timeout after 1 second
        result = sock.connect_ex((ip, port))  # Try to connect to the port

        # If the result is 0, the port is open
        if result == 0:
            print(f"Port {port} is open")
        sock.close()
    except socket.error as e:
        pass  # Ignore errors (we don't need to print them for closed ports)

# Function to scan a range of ports in parallel
def scan_ports(ip, start_port, end_port):
    try:
        # Validate the IP address
        socket.inet_aton(ip)
    except socket.error:
        print(f"Invalid IP address: {ip}")
        return
    
    # Validate port range
    if not (1 <= start_port <= 65535 and 1 <= end_port <= 65535):
        print("Port range must be between 1 and 65535")
        return
    
    if start_port > end_port:
        print("Start port must be less than or equal to end port.")
        return

    print(f"Scanning ports {start_port}-{end_port} on {ip}...")
    
    threads = []
    for port in range(start_port, end_port + 1):
        # Create a new thread for each port scan
        thread = threading.Thread(target=scan_port, args=(ip, port))
        threads.append(thread)
        thread.start()  # Start the thread

    # Wait for all threads to complete
    for thread in threads:
        thread.join()

# Main block to run the script
if __name__ == "__main__":
    # Get user input for IP and port range
    ip_address = input("Enter the IP address: ")
    try:
        start_port = int(input("Enter the start port: "))
        end_port = int(input("Enter the end port: "))
    except ValueError:
        print("Port range must be integers.")
        exit()

    # Call the function to scan ports
    scan_ports(ip_address, start_port, end_port)
