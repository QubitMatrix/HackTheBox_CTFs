- The challenge consists on a web page hosted in the given IP and port
- One accessing the web page it seems to be a game with multiple decisions and paths

	**Direct Approach**   
	- The network tab shows the files that are used and we see an unusual file called 'options' which is fetched from 'main.js'
	- On checking main.js we see that the options file is fetched through the /api/options -> this file can be access through browser using the url and it shows the list of available options.
	- One options shows a secret command which would not show up through the website options
	- Pasting that option instead of the options shown will give the flag

	**Detailed Approach**   
	This approach can be used if the code was designed to only work with the visible options and not the secret option -> in that case the website will show the option is invalid but hitting the api directly will give the flag   
	- Inspecting the network tab shows a `main.js`
	- The source code of main.js shows the functions and APIs that the game uses
	- The `checkMessage` function seems to call the `/api/monitor` to get some data and checks if it consists of the characters 'HTB{'
	- Trying to hit this api directly would not work as it requires the method to be POST and not GET -> we can use burpsuite or postman to modify the request as needed
	- To check how exactly the game works we can capture the requests and response on burpsuite and see how the request is formed to hit the /api/monitor API
	- From this we see that any input we give first checks if it is valid input using the call to `/api/option` -> we can directly hit this url from the browser and see the available options
		- Here we see that there is a secret option which would not show up on the screen 
		- If we create a request to /api/monitor using this input we can retrieve the flag
		- To do that we can capture any normal request using the game and modify the input to the secret input we found and the output would give the flag