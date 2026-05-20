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
<img width="827" height="969" alt="Screenshot 2026-05-20 155053" src="https://github.com/user-attachments/assets/456aa7c6-36ec-45e3-be3c-984c13ccd2be" />
<img width="880" height="842" alt="Screenshot 2026-05-20 155201" src="https://github.com/user-attachments/assets/2b97e3b4-ac28-462d-9218-8f84a9b19279" />
<img width="1845" height="520" alt="Screenshot 2026-05-20 155419" src="https://github.com/user-attachments/assets/32126f12-6846-48d3-92b6-afd7a947a29b" />
## RESULT
Thus, the python program for creating File Transfer using TCP Sockets Links was 
successfully created and executed.
