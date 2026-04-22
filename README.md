# Echoserver
Echo server and client using python socket
# AIM:

To develop a simple webserver to serve html programming pages.

## DESIGN STEPS:

### Step 1:

HTML content creation is done

### Step 2:

Design of webserver workflow

### Step 3:

Implementation using Python code

### Step 4:

Serving the HTML pages.

### Step 5:

Testing the webserver

## PROGRAM:
```
from http.server import HTTPServer,BaseHTTPRequestHandler

content='''
<!doctype html>
<html>
<head>
<title> My Web Server</title>
</head>
<body>
<h1>Top Five Web Application Development Frameworks</h1>
<h2>1.Django</h2>
<h2>2. MEAN Stack</h2>
<h2>3. React </h2>
</body>
</html>


class MyServer(BaseHTTPRequestHandler):
    def do_GET(self):
        print("Get request received...")
        self.send_response(200) 
        self.send_header("content-type", "text/html")       
        self.end_headers()
        self.wfile.write(content.encode())

print("This is my webserver") 
server_address =('keerthi',2323)
httpd = HTTPServer(server_address,MyServer)
httpd.serve_forever()
```
CLIENT.PY
```
# echo_client.py

import socket

# Create socket
client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# Connect to server
client_socket.connect(("127.0.0.1", 12345))

while True:
    message = input("Enter message: ")
    
    if message.lower() == "exit":
        break
    
    # Send message
    client_socket.send(message.encode())
    
    # Receive echo
    data = client_socket.recv(1024).decode()
    print("Server replied:", data)

# Close socket
client_socket.close()
```

SERVER.PY
```
# echo_server.py

import socket

# Create socket
server_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# Bind to localhost and port
server_socket.bind(("127.0.0.1", 12345))

# Listen for connections
server_socket.listen(1)
print("Server is waiting for connection...")

# Accept connection
conn, addr = server_socket.accept()
print("Connected to:", addr)

while True:
    data = conn.recv(1024).decode()
    
    if not data:
        break
    
    print("Client says:", data)
    
    # Echo back the same message
    conn.send(data.encode())

# Close connection
conn.close()
server_socket.close()
```

##  Architecture Diagram

```bash
+--------------------------+
|  User's Web Browser      |
|  (Client: Chrome/Firefox)|
+-----------+--------------+
            |
            |  HTTP Request (GET /)
            v
+-----------+--------------+
|   Python Web Server      |
| (http.server + Handler)  |
| - Listens on Port 8000   |
| - Handles GET Requests   |
| - Sends HTML Response    |
+-----------+--------------+
            |
            |  HTML Response
            v
+--------------------------+
|  User Sees Rendered Page |
|  <h1>Hello Web Server</h1>|
+--------------------------+
```


## OUTPUT:
### CLIENT OUTPUT:
<img width="519" height="420" alt="Screenshot 2026-04-22 113204" src="https://github.com/user-attachments/assets/735aa618-c4c5-4b72-8819-e6ce52072099" />

### SERVER OUTPUT:
<img width="574" height="418" alt="Screenshot 2026-04-22 113158" src="https://github.com/user-attachments/assets/c8fb0528-0732-4e1c-8558-ba78b176201b" />

## RESULT:
The program is executed succesfully
