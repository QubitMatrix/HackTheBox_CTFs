- This challenge has no downloadable files but has an IP and port that we can connect to
- `nc <ip> <port>` 
	- The connection shows a message asking for an index to show the character
	- Random numbers show that there are close to 100 indexes to cover so we need a script to automate the process
	- Python script
		```
		import socket
		
		client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
		client_socket.connect(("<ip>", <port>))
		
		pos = 0
		flag = ""
		data = client_socket.recv(1024).decode('utf-8')
		while True:
		    val = str(pos) + "\n"
		    client_socket.send(val.encode('utf-8'))
		    ans = client_socket.recv(1024).decode('utf-8')
		    character = ans.split("\n")[0][-1] # Retrieve the answer from first line of output and the character is the last character in the line
		
		    if(not character.isspace()):
		        flag += character
		    pos += 1
		    if(character == '}'):
		        break
		
		print(flag)

		```
