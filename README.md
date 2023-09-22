# Intro
Hello, during reconnaissance we commonly need to search on paid tools (Censys, Shodan, Security Trails) in other to get some useful information about the target.<br>
And sometimes we don't need to pay for that tool, since we just need a fast and easy information about it.<br>
So here I introduce you the _Lazy Scripts_<br>
It's basic javascript codes that can be save as an Bookmark on your browser in order to extract some information about this tools<br>

#### [@phor3nsic](https://github.com/phor3nsic)

Credits by the root idea :)

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
<img src="./contents/how_to.gif" alt="GIF" width="800" />

# Codes
Let's go to the interesting part!! <br>

<details><summary><h6>Censys Search</h6></summary>

URL used: https://search.censys.io/search?resource=hosts&sort=RELEVANCE&per_page=25&virtual_hosts=EXCLUDE&q=google.com <br>

```javascript
javascript: (function() {
	var divs = document.getElementsByClassName("SearchResult result");
	const results = new Set;

	for (var i = 0; i < divs.length; i++) {
		var notes = divs[i].getElementsByTagName("strong")[0].textContent.trim();
		var result = notes;
		results.add(result);
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

</details>

<details><summary><h6>Security Trails Search</h6></summary> 

URL used: https://securitytrails.com/domain/example.com/dns

```javascript
javascript: (function() {
  var divs = document.getElementsByTagName("tr");
  const resultsgrep = new Set;

  for (var i = 1; i < divs.length; i++) {
    var notes = divs[i].getElementsByTagName("a")[0];
    var notes = notes.textContent;
    var result = notes;
    var result = result.replace(/.*\/domain\/([^\/]+)\/dns.*/, '$1');
    resultsgrep.add(result);
  }

  function writeResults() {
  document.write('<button onclick="location.reload()">Reload Page</button><br>');
  resultsgrep.forEach(function(t) {
      document.write(t + "<br>")
    })
  }
  setTimeout(writeResults, 3000);
})();
```

<details>

