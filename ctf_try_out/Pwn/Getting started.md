- The challenge consists of the source codes and an IP and port to connect to

**Approach 1:**   
- `nc <ip> <port>` shows the stack trace and gives a hint to overwrite the alignment and target address -> buffer overflow exploit
- Giving an input of multiple a's (minimum 48) will change the required values and give the flag

**Approach 2:**   
- Using the wrapper.py code
- Change the number of A's to 5 (as minimum 48 A's needed)
- Run the python script to get the flag