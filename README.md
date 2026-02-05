# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
### server.py
```
import socket
s=socket.socket()
s.bind(('127.0.0.1',8000))
s.listen(5)
print("Server is listening on port 8000...")   

conn,addr=s.accept()
print("Connection from:",addr)

while True:
    frame=conn.recv(1024).decode()
    if not frame:
        break
    print("Received frame:",frame)
    ack_message="ACK for frame: "+frame
    conn.send(ack_message.encode()) 
conn.close()    
s.close()
```
### client.py:

```
import socket
s=socket.socket()
s.connect(('127.0.0.1',8000))

size=int(input("Enter frame size: "))
l=list(range(size))
frame_size=int(input("Enter frame size to send: "))
i=0
while True:
    while i<len(l):
        st=i+frame_size
        frame_to_send=l[i:st]
        print("Sending frame:",frame_to_send)   
        s.send(str(frame_to_send).encode())
        ack=s.recv(1024).decode()
        if not ack:
            break
        else:
            print("Received acknowledgment:",ack)
        i+=frame_size
    break
s.close()

```

## OUPUT
### server:

![alt text](<Screenshot 2026-02-05 205110 copy.png>)

### client:

![alt text](<Screenshot 2026-02-05 205127.png>)

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
