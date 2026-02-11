## AIM 
To write a python program to perform stop and wait protocol
## ALGORITHM
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
## SERVER:
```
import socket

server = socket.socket()
server.bind(('localhost', 8000))
server.listen(1)
print("Server is listening...")
conn, addr = server.accept()
print(f"Connected with {addr}")

while True:
    data = conn.recv(1024).decode()

    if data:
        print(f"Received: {data}")
        conn.send("ACK".encode())

        if data.lower() == 'exit':  
            print("Connection closed by client")
            conn.close()
            break
```
## CLIENT:
```
import socket
import time

client = socket.socket()
client.connect(('localhost', 8000))
client.settimeout(5)  

while True:
    msg = input("Enter a message (or type 'exit' to quit): ")

    client.send(msg.encode())  

    if msg.lower() == 'exit':  
        print("Connection closed by client")
        client.close()
        break

    try:
        ack = client.recv(1024).decode()
        if ack == "ACK":
            print(f"Server acknowledged: {ack}")
    except socket.timeout:
        print("No ACK received, retransmitting...")
        continue  
```


## OUTPUT
## SERVER:
<img width="1205" height="323" alt="Screenshot 2026-02-11 110602" src="https://github.com/user-attachments/assets/feae89ec-c39f-4a95-b370-0bbb3a9f0eec" />

## CLIENT:
<img width="1203" height="254" alt="Screenshot 2026-02-11 110624" src="https://github.com/user-attachments/assets/ed2a36b6-faf8-4d22-a570-ed8afcd85f81" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed.
