# 3c.CREATION FOR FILE TRANSFER USING TCP SOCKETS
## AIM
To write a python program for creating File Transfer using TCP Sockets Links
## ALGORITHM:
1. Import the necessary python modules.
2. Create a socket connection using socket module.
3. Send the message to write into the file to the client file.
4. Open the file and then send it to the client in byte format.
5. In the client side receive the file from server and then write the content into it.
## PROGRAM
~~~
Server Program (server.py)

import socket
port = 60000
# Create socket
s = socket.socket()
# Get local machine name
host = socket.gethostname()
# Bind socket
s.bind((host, port))
# Start listening
s.listen(5)
print("Server is listening...")
while True:
    # Accept connection
    conn, addr = s.accept()
    print("Got connection from", addr)
    # Receive message from client
    data = conn.recv(1024)
    print("Server received:", repr(data))
    # File to send
    filename = "mytext.txt"
    # Open and send file
    with open(filename, 'rb') as f:
        l = f.read(1024)

        while l:
            conn.send(l)
            print("Sent", repr(l))
            l = f.read(1024)

    print("Done sending")

    # Close connection
    conn.close()
    print("Connection closed")


Client Program (client.py)
import socket
# Create socket
s = socket.socket()
# Get host and port
host = socket.gethostname()
port = 60000
# Connect to server
s.connect((host, port))
print("Connected to server")
# Send greeting message
s.send("Hello server!".encode())
# Receive file
with open('received_file.txt', 'wb') as f:
    while True:
        print("Receiving data...")

        data = s.recv(1024)

        print("Data =", data)

        if not data:
            break

        f.write(data)

print("Successfully received the file")

# Close connection
s.close()

print("Connection closed")
~~~
## OUPUT
<img width="1437" height="292" alt="Screenshot 2026-05-19 091038" src="https://github.com/user-attachments/assets/834d5895-cf6e-4957-b289-be8fb88aa813" />

## RESULT
Thus, the python program for creating File Transfer using TCP Sockets Links was 
successfully created and executed.
