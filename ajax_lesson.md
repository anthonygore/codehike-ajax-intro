##Codehike Lesson

#AJAX Introduction

* AJAX allows a web page to request and receive data without reloading the page.
* Allows functionality like Google's search autocomplete.

__Exercise__: allow a user to check their IP by retrieving it from an IP-checking web service (URL provided below)

index.html

	<!DOCTYPE html>
	<html>
	<head>
		<meta charset="utf-8"/>
		<link rel="stylesheet" type="text/css" href="style.css">
	</head>
	<body>
		<div id="container">
			<span>Your IP:</span>
			<span id="ip"></span>
		</div>
		<button id="update">Update</button>
		<script src="script.js"></script>
	</body>
	</html>

1. Create a function called `sync` with no arguments.
2. `sync` will clear the contents of the span `ip`, then will fill it with a string ("hello" will do for now).
3. Create a function which is called on the click event of the button with id `update`. This function should call `sync`.

	* `XMLHttpRequest` API is used to manage AJAX in Javascript. The API documentation can be found here: https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest

4. Now get the function to make an AJAX call to httpbin and retrieve an IP address. Do it synchronously. The URL is `https://httpbin.org/ip`

	* This works, but hangs the browser. If the server takes a while to respond it will provide a bad user experience.

5. Copy the function `sync` and create a new function, `async`. It will do the same AJAX call, only asyncronously. Make your button click event call `async` now instead of `sync`.

	* If you make the request asynchronous i.e. `xhr.open('GET', url, true);`, nothing is added to the div because the code executes before the HTTP request has been completed. If you check the `readyState` property you'll see at the time of return it's at `1` in this example.
	* The solution is to  use the event handler `onreadystatechange` which triggers at every stage of the HTTP request

6. To finish off, parse the IP properly, style the document etc.