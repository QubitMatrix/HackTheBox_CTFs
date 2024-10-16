- This challenge consists of a output text which consists of a decrypted text and the source code used to encrypt the flag
- The source code can be used to create a decrypt function to retrieve that flag
- Source code for decryption
	```
	def to_identity_map_rev(a):
	    return chr(a%26 + 0x41)
	
	def from_identity_map_rev(a):
	    return ord(a) - 0x41
	
	def decrypt(m):
	    ans = ''
	    for i in range(len(m)):
	        ch = m[i]
	        if not ch.isalpha():
	            ech = ch
	        else:
	            chi = from_identity_map_rev(ch) - i
	            ech = to_identity_map_rev(chi)
	        ans += ech
	    return ans
	print(decrypt(<cipher from output file>))

	```

