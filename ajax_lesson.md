##Codehike Lesson

#AJAX Introduction

###Anthony Gore, 6/2/16

* AJAX allows a web page to request and receive data without reloading the page.
* Allows functionality like Google's search autocomplete.
* `XMLHttpRequest` API is used to manage AJAX in Javascript.

Example 1: Synchronous AJAX  

index.html

	<!DOCTYPE html>
	<html>
	<head>
		<meta charset="utf-8"/>
		<link rel="stylesheet" type="text/css" href="style.css">
	</head>
	<body>
		<div id="container"></div>
		<script src="script.js"></script>
	</body>
	</html> 
	
script.js

	function load() {
		var url = 'https://httpbin.org/ip';
		var xhr = new XMLHttpRequest();         
	    xhr.open('GET', url, false);
	    xhr.send();
		document.getElementById('container').innerHTML = xhr.responseText;
	}

	load();
	
* This works, but hangs the browser. If the server takes a while to respond it will provide a bad user experience.
* If you make the request asynchronous i.e. `xhr.open('GET', url, true);`, nothing is added to the div because the code executes before the HTTP request has been completed. If you check the `readyState` property you'll see at the time of return it's at `1` in this example.
* The solution is to  use the event handler `onreadystatechange` which triggers at every stage of the HTTP request

Example 2: Asynchronous AJAX

script.js 
  
	function load() {
		var url = 'https://httpbin.org/ip';
		var xhr = new XMLHttpRequest();
		xhr.onreadystatechange = function() {
			if (xhr.readyState === 4) {
     			document.getElementById('container').innerHTML = xhr.responseText;
    		}
  		};      
	    xhr.open('GET', url, true);
	    xhr.send();
	}

	load();

Exercise: An app that shows the time

index.html

	<!DOCTYPE html>
	<html>
	<head>
		<meta charset="utf-8"/>
		<link rel="stylesheet" type="text/css" href="style.css">
	</head>
	<body>
		<div id="container"></div>
		<button id="trigger">Get Time</div>
		<script src="script.js"></script>
	</body>
	</html> 

script.js

	function load() {
		var url = 'https://api.timezonedb.com/?zone=America/Toronto&format=json&key=P9SJIAQ7AHKD';
		var xhr = new XMLHttpRequest();
		xhr.onreadystatechange = function() {
			if (xhr.readyState === 4) {
				var responseObj = JSON.parse(xhr.responseText);
     			document.getElementById('container').innerHTML = responseObj.timestamp;
    		}
  		};      
	    xhr.open('GET', url, true);
	    xhr.send();
	}

	document.getElementById("trigger").addEventListener("click", function(){
   		load(); 
	});

Further reading:

https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest
	