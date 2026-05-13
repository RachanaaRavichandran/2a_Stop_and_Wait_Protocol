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
```
import socket
import threading

HOST = "localhost"
PORT = 6000

# Sender side
def start_sender():
    sender_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    sender_socket.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)

    sender_socket.bind((HOST, PORT))
    sender_socket.listen(1)

    print("Sender is waiting for connection...")

    connection, address = sender_socket.accept()
    print("Receiver connected from:", address)

    while True:
        text = input("Send Message: ")
        connection.sendall(text.encode())

        if text.lower() == "exit":
            break

        response = connection.recv(1024).decode()
        print("Reply from Receiver:", response)

    connection.close()
    sender_socket.close()


# Receiver side
def start_receiver():
    receiver_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

    receiver_socket.connect((HOST, PORT))

    while True:
        message = receiver_socket.recv(1024).decode()

        print("Message Received:", message)

        if message.lower() == "exit":
            break

        acknowledgement = "Message Accepted"
        receiver_socket.send(acknowledgement.encode())

    receiver_socket.close()


# Thread for receiver
receiver_thread = threading.Thread(target=start_receiver, daemon=True)
receiver_thread.start()

# Start sender
start_sender()
Developed by:R.Rachanaa
Ref no: 212225040322
```
## OUTPUT
<img width="605" height="487" alt="image" src="https://github.com/user-attachments/assets/e140c8df-df80-46f0-af66-a67e54bb9003" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed.
