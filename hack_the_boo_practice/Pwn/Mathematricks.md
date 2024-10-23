- This challenge has downloadable files which includes a executable for trying the challenge locally and a solver to send inputs to the connection -> the solver file is not required if your fluent with `nc`
- Let's try executing the executable `mathematricks`
	- `./mathematricks` -> this would give the local testing flag => use `nc <ip> <port>` to get actual flag 
	- The option 2 reveals rules -> nothing of importance
	- Option 1 asks some questions 
		1. 1+1 -> 2
		2. 2 - 1 -> 1
		3. 1337 - 1337 -> 0
		4. Now this question is tricky as it is expecting two positive numbers and expects its sum to be negative
			- While this seems mathematically impossible, it is possible in a C or any **statically typed languages** that assign a data type before compilation 
			- We are going to exploit a common vulnerability in such languages -> **Integer overflow or wraparound** (CVE-190)
			- A value which exceeds the max limit of integer which is 2147483647 will start again from -2147483648
			- n1 = 2147483647, n2 = 1 -> sum = -2147483648
			- Flag -> `HTB{m4th3m4tINT_5tuff_<obfuscated>}`

