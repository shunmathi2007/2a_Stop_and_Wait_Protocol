# 2a_Stop_and_Wait_Protocol
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

client.py

import socket

c = socket.socket()

c.connect(('localhost', 8000))

c.settimeout(5)

while True:
    msg = input("Message: ")
    c.send(msg.encode())

    if msg == "exit":
        break

    try:
        if c.recv(1024).decode() == "ACK":
            print("ACK received")
    except socket.timeout:
        print("No ACK, retransmitting...")

c.close()

server.py

import socket

s = socket.socket()

s.bind(('localhost', 8000))

s.listen(1)

print("Server ready...")

c, _ = s.accept()

while True:

    msg = c.recv(1024).decode()
    if not msg:
        break
    print("Received:", msg)
    c.send(b"ACK")
    if msg == "exit":
        break

c.close()

s.close()
## OUTPUT
<img width="1037" height="607" alt="WhatsApp Image 2026-11-02 at 1 24 01 PM" src="https://github.com/user-attachments/assets/3dbbe99f-a993-4631-bfad-895a9f3a5b2b" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed.
