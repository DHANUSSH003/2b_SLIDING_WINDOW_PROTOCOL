# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
To write a python program for the implementation of sliding window protocol.
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
### client

```
import socket
import time

def client_program():
    host = "127.0.0.1"  # server IP
    port = 5000         # server port

    client_socket = socket.socket()
    client_socket.connect((host, port))

    total_frames = int(input("Enter total number of frames: "))
    window_size = int(input("Enter window size: "))

    sent = 0

    while sent < total_frames:
        # Send a window of frames
        for i in range(sent, min(sent + window_size, total_frames)):
            frame = f"Frame {i+1}"
            print("Sending:", frame)
            client_socket.send(frame.encode())

            # Receive ACK from server
            ack = client_socket.recv(1024).decode()
            print("Received from server:", ack)
            time.sleep(1)

        sent += window_size  # slide window

    client_socket.close()


if __name__ == '__main__':
    client_program()

```
### server
```
import socket

def server_program():
    host = "127.0.0.1"  # localhost
    port = 5000         # server port

    server_socket = socket.socket()
    server_socket.bind((host, port))
    server_socket.listen(1)
    print("Server is waiting for connection...")

    conn, address = server_socket.accept()
    print("Connection from:", address)

    while True:
        data = conn.recv(1024).decode()
        if not data:
            break

        print("Received:", data)

        # Simulate ACK
        ack = f"ACK for {data}"
        conn.send(ack.encode())

    conn.close()


if __name__ == '__main__':
    server_program()

```
## OUPUT

<img width="1920" height="1200" alt="Screenshot (8)" src="https://github.com/user-attachments/assets/9eeeb0a7-c31f-4086-9b32-63e41c1e54d6" />




## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
