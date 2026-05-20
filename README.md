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
## Server 
```
# SERVER CODE

import socket

port = 60000

s = socket.socket()
host = socket.gethostname()

s.bind((host, port))
s.listen(5)

print("Server listening on port", port)

while True:
    conn, addr = s.accept()
    print("Connected to", addr)

    data = conn.recv(1024)
    print("Server received:", data.decode())

    filename = "untitled.txt"   # Make sure this file exists

    try:
        with open(filename, 'rb') as f:

            file_data = f.read(1024)

            while file_data:
                conn.send(file_data)
                file_data = f.read(1024)

        # Send extra message
        conn.send("\nThank you for connecting".encode())

        print("Done sending")

    except FileNotFoundError:
        conn.send("File not found".encode())

    conn.close()
```

## Client 
```
# CLIENT CODE

import socket

s = socket.socket()

host = socket.gethostname()
port = 60000

s.connect((host, port))

s.send("Hello server!".encode())

with open("received_file.txt", "wb") as f:

    print("Receiving data...")

    while True:
        data = s.recv(1024)

        if not data:
            break

        f.write(data)

print("Successfully received the file")

s.close()

print("Connection closed")
```

## OUPUT
<img width="1920" height="1080" alt="Screenshot 2026-05-20 154546" src="https://github.com/user-attachments/assets/98ac1043-0e2b-47eb-b118-f68099e5706a" />

<img width="1907" height="459" alt="Screenshot 2026-05-20 154737" src="https://github.com/user-attachments/assets/39581574-d9a1-4fd4-ba72-146482794f95" />

## RESULT
Thus, the python program for creating File Transfer using TCP Sockets Links was 
successfully created and executed.
