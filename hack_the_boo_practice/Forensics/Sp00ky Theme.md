- The challenge consists of downloadable files which need to be analysed to find the flag
- Since it consists of multiple files as a first step we can try to search for the file directly
	- `grep -r "HTB" ./*` 
	- However no match indicates that the flag is not directly stored anywhere
- Next common way of storing flags is base 64 encoding so let's search for base64 encoded flags
	- grep -r "base64" ./*
	- This time we get lucky and it shows one line that matched the regex. It is seen to be a piped command where the string is sent into reverse and then decoded for base64
	- Reversing the string and decode for base64 using the command given in the file `echo 952MwBHNo9lb0M2X0FzX/Eycz02MoR3X5J2XkNjb3B3eCRFS | rev | base64 -d` or cyberchef to get the flag
- Flag -> `HTB{pwn3d_by_th3m3s!?_1t_c4n_<obfuscated>}`

