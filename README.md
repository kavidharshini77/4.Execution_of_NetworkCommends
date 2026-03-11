# 4.Execution_of_NetworkCommands
## AIM :Use of Network commands in Real Time environment
## Software : Command Prompt And Network Protocol Analyzer
## Procedure: To do this EXPERIMENT- follows these steps:
<BR>
In this EXPERIMENT- students have to understand basic networking commands e.g cpdump, netstat, ifconfig, nslookup ,traceroute and also Capture ping and traceroute PDUs using a network protocol analyzer 
<BR>
All commands related to Network configuration which includes how to switch to privilege mode
<BR>
and normal mode and how to configure router interface and how to save this configuration to
<BR>
flash memory or permanent memory.
<BR>
This commands includes
<BR>
• Configuring the Router commands
<BR>
• General Commands to configure network
<BR>
• Privileged Mode commands of a router 
<BR>
• Router Processes & Statistics
<BR>
• IP Commands
<BR>
• Other IP Commands e.g. show ip route etc.
<BR>

## Program
## Server.py
import socket
import subprocess

host = "127.0.0.1"
port = 8000

server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
server.bind((host, port))
server.listen(1)

print("Server is running...")
conn, addr = server.accept()
print("Client connected:", addr)

while True:
    data = conn.recv(1024).decode()

    if data.lower() == "exit":
        print("Client disconnected")
        break

    try:
        output = subprocess.getoutput(f"ping -n 2 {data}")
        conn.send(output.encode())
    except:
        conn.send("Unable to ping the host".encode())

conn.close()
server.close()
## Client.py
import socket

host = "127.0.0.1"
port = 8000

client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client.connect((host, port))

print("Connected to server")

while True:
    site = input("Enter website to ping (or type exit): ")

    client.send(site.encode())

    if site.lower() == "exit":
        break

    result = client.recv(4096).decode()
    print("\nPing Result:\n", result)

client.close()

## Output
<img width="805" height="80" alt="image" src="https://github.com/user-attachments/assets/405034ba-ae8e-489d-93bd-aa32a9276e6f" />
<img width="808" height="550" alt="image" src="https://github.com/user-attachments/assets/97aa4126-f7c8-4d5b-be08-0ac577dfc2a5" />


## Result
Thus Execution of Network commands Performed 
