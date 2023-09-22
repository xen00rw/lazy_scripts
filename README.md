# Intro
Hello, during reconnaissance we commonly need to search on paid tools (Censys, Shodan, Security Trails) in other to get some useful information about the target.<br>
And sometimes we don't need to pay for that tool, since we just need a fast and easy information about it.<br>
So here I introduce you the _Lazy Scripts_<br>
It's basic javascript codes that can be save as an Bookmark on your browser in order to extract some information about this tools<br>

# How to configure
It's quite simple, you just need to include one of the Javascript codes below that is of your interest.<br>

Steps:<br>
1. Right click on the Bookmark bar on your Browser (I'm using Chrome)
2. Go to "Add Page"
3. On "Name" define the name for this bookmark that you prefer
4. On "URL" insert one of the Javascripts that you selected
5. Access the site corresponding for that Javascript, and try it, just click it
<br>

If you prefer, here is a video:<br>
![Alt Text](./contents/how_to.gif)

# Codes
Let's go to the interesting part!! <br>

#### Censys Search
```javascript
javascript: (function() {
	var divs = document.getElementsByClassName("SearchResult result");
	const results = new Set;
	var values = [];

	for (var i = 0; i < divs.length; i++) {
		var notes = divs[i].getElementsByTagName("strong")[0].textContent.trim();
		var result = notes;
		results.add(result);
		values.push(result);
	}

	function writeResults() {
	document.write('<button onclick="location.reload()">Reload Page</button><br>');
	results.forEach(function(t) {
			document.write(t + "<br>")
		})
	}
	setTimeout(writeResults, 3000);
})();
```

