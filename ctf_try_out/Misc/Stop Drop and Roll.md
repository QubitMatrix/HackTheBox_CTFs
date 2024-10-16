- Challenge has no files and just a IP and port that we can connect to
- `nc <ip> <port>`
	- Playing around with the netcat connection shows that the first response consists of a ready or not which expects a 'y' after which the game starts
- Python script to mimic the netcat connection and automate the process
	```
	import socket
	client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
	
	client_socket.connect(("<ip>", <port>))
	
	count = 0
	while True:
		count += 1
		data = client_socket.recv(1024).decode('utf-8')
		print(count,data)
		if not data:
			break
		last_line = data.split("\n")[-1]
		second_last_line = None
		if("ready" in last_line):
			bytes = client_socket.send("y\n".encode('utf-8'))
		else:
			for line in data.split("\n"):
				if("GORGE" in line  or "PHREAK" in line or "FIRE" in line):
					second_last_line = line
					break
	
			ans = ""
			if(not second_last_line):
				continue
			for word in second_last_line.split(", "):
				print("word:",word)
				if(word == "GORGE"):
					ans += "STOP-"
				elif(word == "PHREAK"):
					ans += "DROP-"
				elif(word == "FIRE"):
					ans += "ROLL-"
			if(len(ans) > 0):
				ans = ans[:-1] + "\n"
				bytes = client_socket.send(ans.encode("utf-8"))
	
	client_socket.close()

	```

