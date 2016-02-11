##Codehike Lesson

#AJAX Introduction

__Solution__

script.js

	function async(){
		var url = 'https://httpbin.org/ip';
		var xhr = new XMLHttpRequest();
		xhr.onreadystatechange = function(){
			if (xhr.readyState === 4) {
				$('#ip').html(xhr.responseText);
			}
		};
		xhr.open('GET', url, true);
		xhr.send();
	}

	function sync(){
		var url = 'https://httpbin.org/ip';
		var xhr = new XMLHttpRequest();
		xhr.open('GET', url, false);
		xhr.send();
		$('#ip').html(xhr.responseText);
	}

	$('#update').click(function(){
		$('#ip').empty();
		// Swap between sync and async to see the effect
		async();
	});

Further challenges:

* Implement this in jQuery