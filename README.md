# Intro
Here I introduce you the _Lazy Scripts_<br>
It's basic javascript codes that can be save as an Bookmark on your browser in order to extract some information about tools with useful information for recon phase of pentesting<br>

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
<img src="./contents/how_to.gif" alt="GIF" width="600" />

# Codes

<details><summary><h6>[Censys Search] Default Search</h6></summary>
<a><b>URL used: </b>https://search.censys.io/search?resource=hosts&sort=RELEVANCE&per_page=25&virtual_hosts=EXCLUDE&q=google.com</a><br>
<a><b>Description: </b>This script will get all the IPs from the current page of Censys search.</a><br><br>

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

<details><summary><h6>[Censys Search] New Search</h6></summary>
<a><b>URL used: </b>https://platform.censys.io/search?q=host.services.cert.name%3A+"example.com"</a><br>
<a><b>Description: </b>This script will get all the IPs from the current page of Censys search.</a><br><br>

```javascript
javascript: (function() {
    var divs = document.getElementsByClassName("rAnPY");
    var notes = divs[0].getElementsByClassName("apoUv");
    const results = new Set;
    for (var i = 0; i < notes.length; i++) {
        var ip = notes[i].textContent;
        var result = ip;
        results.add(result);
    }

    function writeResults() {
        document.write('<button onclick="history.go(0);">Reload Page</button><br>');
        results.forEach(function(t) {
            document.write(t + "<br>")
        })
    }
    setTimeout(writeResults, 3000);
})();
```
</details>

<details><summary><h6>[Security Trails] Extract Ips from DNS History Subdomains</h6></summary> 
<a><b>URL used: </b>https://securitytrails.com/domain/example.com/history/a</a><br>
<a><b>Description: </b>This script will extract all IPs plus the hostname present on the current page of Security Trails IP history search.</a><br>
<a><b>Requirements: </b>Be logged in</a><br><br>

```javascript
javascript: (function() {
    var divs = document.getElementsByTagName("tr");
    const resultsgrep = new Set();
    for (var i = 1; i < divs.length; i++) {
        var anchors = divs[i].getElementsByTagName("a");
        for (var j = 0; j < anchors.length; j++) {
            let note = anchors[j].textContent.trim();
            let currentUrl = window.location.href;
            let valueUrl = currentUrl.match(/\/domain\/(.*?)\/history\//)[1];
            console.log(valueUrl);
            let extracted = note.replace(/.*\/domain\/([^\/]+)\/dns.*/, '$1');
            let extracted2 = extracted + " - " + valueUrl;
            console.log(extracted2);
            if (extracted2) {
                resultsgrep.add(extracted2);
            }
        }
    }

    function writeResults() {
        document.write('<button onclick="location.reload()">Reload Page</button><br>');
        resultsgrep.forEach(function(t) {
            document.write(t + "<br>");
        });
    }
    setTimeout(writeResults, 3000);
})();
```
</details>

<details><summary><h6>[Security Trails] Search Subdomains</h6></summary> 
<a><b>URL used: </b>https://securitytrails.com/domain/example.com/dns</a><br>
<a><b>Description: </b>This script will extract all subdomains present on the current page of Security Trails subdomains search.</a><br>
<a><b>Requirements: </b>Be logged in</a><br><br>

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
</details>

<details><summary><h6>[Jira Server] Users Management</h6></summary> 
<a><b>URL used: </b>https://jira.instance.net/secure/admin/user/UserBrowser.jspa<a><br>
<a><b>Description: </b>This will get some informations about the users on Jira Server. Including Full name, username and groups. Useful for users list extraction.</a><br>
<a><b>Requirements: </b>Be logged in.<a><br><br>

```javascript
javascript: (function() {
	var divs = document.getElementsByClassName("vcard user-row");
	const results = new Set;

	for (var i = 0; i < divs.length; i++) {
		var fullname = divs[i].getElementsByTagName("td")[0].textContent;
		var fullname = fullname.replace(/\s+$/, '');

		var username = divs[i].getElementsByTagName("td")[1].textContent.trim();
		var username = username.replace(/ /gi,"");
  		var username = username.replace("\n\n",",");

  		var groups = Array.from(divs[i].getElementsByTagName("td")[3].querySelectorAll("li"), li => li.textContent.trim());  
  		var groups = groups.map(item => item.replace(/,/g, ";"));

		var result = fullname + "," + username + "," + groups;
		results.add(result);
	}

	function writeResults() {
		document.write('<button onclick="location.reload()">Reload Page</button><br>');
		results.forEach(function(content) {
			document.write(content + "<br>")
		})
	}
	setTimeout(writeResults, 3000);
})();
```

</details>

<details><summary><h6>[IllServices 0t Rocks] Domain and more search</h6></summary>
<a><b>URL: </b>REDACTED</a><br>
<a><b>Description: </b>This is a service provided for free OSINT information where you can search for content related to emails, URLs, phone numbers and much more. This script will extract from domain search the Domain, URL, Username and Source.</a><br><br>

```javascript
javascript: (function() {
	var divs = document.getElementsByClassName("record");
	const results = new Set;

	for (var i = 0; i < divs.length; i++) {
		var domain = divs[i].getElementsByTagName("dd")[0].textContent.trim();
		var domain = domain.replace(/domain: /g, "");

		var notes = divs[i].getElementsByTagName("dd")[1].textContent.trim();
		var notes = notes.replace(/notes: /g, "");
		var notes = notes.replace(/url: /g, "");

		var emails = divs[i].getElementsByTagName("dd")[2].textContent.trim();
		var emails = emails.replace(/emails: /g, "");
		var emails = emails.replace(/usernames: /g, "");

		var source = divs[i].getElementsByTagName("dd")[3].textContent.trim();
		var source = source.replace(/source: /g, "");

		var result = domain + ", " + notes + ", " + emails + ", " + source;
		results.add(result);
	}

	function writeResults() {
		document.write('<button onclick="location.reload()">Reload Page</button><br>');
		results.forEach(function(content) {
			document.write(content + "<br>")
		})
	}
	setTimeout(writeResults, 3000);
})();
```

</details>

<details><summary><h6>[Hunter.io] Domain Search - Email addresses</h6></summary>
<a><b>URL: </b>https://hunter.io/search/domain.com</a><br>
<a><b>Description: </b>Hunter.io helps find and verify professional email addresses associated with a domain.</a><br><br>

```javascript
javascript:(function() {
	var divs = document.getElementsByClassName("ds-result__email");
	const results = new Set();

	for (var i = 0; i < divs.length; i++) {
		var email = divs[i].textContent.trim();
		results.add(email);
	}

	function writeResults() {
		document.write('<button onclick="location.reload()">Reload Page</button><br>');
		results.forEach(function(email) {
			document.write(email + "<br>");
		});
	}

	setTimeout(writeResults, 3000);
})();
```

</details>