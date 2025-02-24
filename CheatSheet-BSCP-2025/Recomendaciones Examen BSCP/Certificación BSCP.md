* Caracteres extraños, polyglots, metodología primera by @andre
	* Video Examen Practica BSCP Andres Roldan: https://www.youtube.com/watch?v=dGsCA1N1BK0

```
 &&
 
 ¬
 ÷
 ¢
 “
 ≠
 ~
 ´

 
 ∑
 Ω
 ©
 &
 ||
 |
 ;
 `


'
"
""
''
}}
#
%
&
?
';
''-
```

- [https://micahvandeusen.com/burp-suite-certified-practitioner-exam-review/](https://micahvandeusen.com/burp-suite-certified-practitioner-exam-review/)

![[Pasted image 20250215093542.png]]  

![[Pasted image 20250215093754.png]] 

![[Pasted image 20250219203313.png]]

![[Pasted image 20250215095450.png]] 
## Pendiente aprender a manejar un poco mejor Burp Scanner para el BSCP y otra info importante sobre la BSCP →

- [https://portswigger.net/web-security/essential-skills/using-burp-scanner-during-manual-testing](https://portswigger.net/web-security/essential-skills/using-burp-scanner-during-manual-testing) → PENDIENTE.
- [https://portswigger.net/web-security/certification/how-to-prepare](https://portswigger.net/web-security/certification/how-to-prepare)
- [https://portswigger.net/web-security/certification/exam-hints-and-guidance](https://portswigger.net/web-security/certification/exam-hints-and-guidance)

### Usernames And Passwords Portswigger list:

- [https://portswigger.net/web-security/authentication/auth-lab-usernames](https://portswigger.net/web-security/authentication/auth-lab-usernames)
- [https://portswigger.net/web-security/authentication/auth-lab-passwords](https://portswigger.net/web-security/authentication/auth-lab-passwords)

### Obfuscating →

- [https://portswigger.net/web-security/essential-skills/obfuscating-attacks-using-encodings](https://portswigger.net/web-security/essential-skills/obfuscating-attacks-using-encodings)

### Cheat sheets - Portswigger (Aunque voy a crear mis propios cheat sheets)

- [https://portswigger.net/web-security/cross-site-scripting/cheat-sheet](https://portswigger.net/web-security/cross-site-scripting/cheat-sheet)
- [https://portswigger.net/web-security/ssrf/url-validation-bypass-cheat-sheet](https://portswigger.net/web-security/ssrf/url-validation-bypass-cheat-sheet) → urls bypass

### Cheat lists:

`Pendiente sacar enlaces especificos hacía los payloads cheat sheet - para cada tipo de vulnerabilidad (así no pierdo tiempo buscando payloads entre cada vuln, directo)` ⚠️ ⚠️ ⚠️ --> Eso ya lo estoy haciendo aqui en este obsidian. 

Este me interesa:

- [https://github.com/KrakenEU/BSCP/tree/main](https://github.com/KrakenEU/BSCP/tree/main) → A partir de este crearé el mio.

* [CheatSheet BSCP](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqazktOUFZdHJKWjZodkVnU2x1aERxeGhQQXJ3Z3xBQ3Jtc0tubmFyM250WU1mbkN2V3E4Q2h2MTFVUy1mS01EdXZKM2xFNUt5Mlc5MHdWbVN4akVVQ0Y4NVp3ejRNcmFMV2x4QTJjUGdrOWQzOGJlSkxwMlBHa0F3SDJqTUN0bm12QzRJN1J1VmRZT05FenVTd2pJYw&q=https%3A%2F%2Fgithub.com%2Fbotesjuan%2FBurp-Suite-Certified-Practitioner-Exam-Study&v=_Z6n1l5L2fs)[https://github.com/botesjuan/Burp-Sui](https://github.com/botesjuan/Burp-Sui)... → este en la parte de payloads/ está buenisimo.

* https://bscpcheatsheet.gitbook.io/exam/recommended_labs

## Extensiones de Burp

A medida que vas avanzando en la academia, te van introduciendo ciertas extensiones que son útiles para ciertos casos. Os dejo un resumen de aquellas que más me han gustado:

- [Param Miner](https://portswigger.net/bappstore/17d2949a985c4b7ca092728dba871943) – fuzzer de parámetros y cabeceras ocultas.
- [HTTP Request Smuggler](https://portswigger.net/bappstore/aaaa60ef945341e8a450217a54a11646) – contiene distintos vectores de Request Smuggling que puedes usar.
- [Agartha](https://github.com/volkandindar/agartha) – ésta no está en la academia, pero la recomiendo porque te proporciona un montón de payloads para LFI, Inyección de Comandos, SQL Injection, con bypass de WAFS incluido. Se puede, por ejemplo, generar los payloads y meterlos en el Intruder.
- [Turbo Intruder](https://portswigger.net/bappstore/9abaa233088242e8be252cd4ff534988) – útil para cuando tengas que jugar con el timing (race conditions) o quieras mandar requests parcialmente (por ejemplo solo mandar los headers y tras X segundos, mandar el body).
- [Content Type Converter](https://portswigger.net/bappstore/db57ecbe2cb7446292a94aa6181c9278) – pasar el cuerpo de la petición de XML a JSON y viceversa de manera automatizada.
- [JWT Editor](https://portswigger.net/bappstore/26aaa5ded2f74beea19e2ed8345a93dd) – útil para cuando se trata con tokens JWT, y la ext: JWT Web Tokens
- [Server-Side Prototype Pollution Scanner](https://portswigger.net/blog/server-side-prototype-pollution-scanner) – como su nombre indica, útil para Server-Side Prototype Pollution.
- [DOM Invader](https://portswigger.net/burp/documentation/desktop/tools/dom-invader) – viene integrado con el navegador de Burp, y es útil para encontrar Client-Side Prototype Pollution.
- [Java Deserialization Scanner](https://portswigger.net/bappstore/228336544ebe4e68824b5146dbbd93ae) – puedes cargarle el .jar del ysoserial y automatizar el tedioso procedimiento de explotar una deserialización en Java. **(corre con java jdk 8) y tener ysoserial clonado localmente, dejar la ruta en las configs.**
- [Hackvertor](https://portswigger.net/bappstore/65033cbd2c344fbabe57ac060b5dd100) – herramienta que soporta varios tipos de encodings y escapes (entidades HTML5, hex, octal, unicode, etc.)

#### Tener presente para algun ataque SSRF el hecho de que se debe mantener el puerto: `6566`

- **SSRF localhost:6566 o 192.168.0.[burp intruder]**
### Burp Scan

* Deep scan importante también
- Full domain
- Scan Insertion Points on repeater

### Key Words:

- location
- ng-app
- eval
- replace
- addEventListener
- postMessage

**[FOOTHOLD](https://github.com/botesjuan/Burp-Suite-Certified-Practitioner-Exam-Study?tab=readme-ov-file#foothold) - Stage 1**  
# Content Discovery

[Content-Discover Repo BotesJuan](https://github.com/botesjuan/Burp-Suite-Certified-Practitioner-Exam-Study?tab=readme-ov-file#content-discovery)

> Enumeration of target start with fuzzing web directories and files. Either use the Burp engagement tools, content discovery option to find hidden paths and files or use `FFUF` to enumerate web directories and files. Looking at `robots.txt` or `sitemap.xml` that can reveal content.

```shell
wget https://raw.githubusercontent.com/botesjuan/Burp-Suite-Certified-Practitioner-Exam-Study/main/wordlists/burp-labs-wordlist.txt

ffuf -c -w ./burp-labs-wordlist.txt -u https://TARGET.web-security-academy.net/FUZZ
```
[Content Discovery](https://github.com/botesjuan/Burp-Suite-Certified-Practitioner-Exam-Study?tab=readme-ov-file#content-discovery)  
[DOM-XSS](https://github.com/botesjuan/Burp-Suite-Certified-Practitioner-Exam-Study?tab=readme-ov-file#dom-based-xss)  
[XSS Cross Site Scripting](https://github.com/botesjuan/Burp-Suite-Certified-Practitioner-Exam-Study?tab=readme-ov-file#cross-site-scripting)  
[Web Cache Poison](https://github.com/botesjuan/Burp-Suite-Certified-Practitioner-Exam-Study?tab=readme-ov-file#web-cache-poison)  
[Host Headers](https://github.com/botesjuan/Burp-Suite-Certified-Practitioner-Exam-Study?tab=readme-ov-file#host-headers)  
[HTTP Request Smuggling](https://github.com/botesjuan/Burp-Suite-Certified-Practitioner-Exam-Study?tab=readme-ov-file#http-request-smuggling)  
[Brute force](https://github.com/botesjuan/Burp-Suite-Certified-Practitioner-Exam-Study?tab=readme-ov-file#brute-force)  
[Authentication](https://github.com/botesjuan/Burp-Suite-Certified-Practitioner-Exam-Study?tab=readme-ov-file#authentication)

**[PRIVILEGE ESCALATION](https://github.com/botesjuan/Burp-Suite-Certified-Practitioner-Exam-Study?tab=readme-ov-file#privilege-escalation) - Stage 2**  
[CSRF - Account Takeover](https://github.com/botesjuan/Burp-Suite-Certified-Practitioner-Exam-Study?tab=readme-ov-file#csrf-account-takeover)  
[Password Reset](https://github.com/botesjuan/Burp-Suite-Certified-Practitioner-Exam-Study?tab=readme-ov-file#password-reset)  
[SQLi - SQL Injection](https://github.com/botesjuan/Burp-Suite-Certified-Practitioner-Exam-Study?tab=readme-ov-file#sql-injection)  
[JWT - JSON Web Tokens](https://github.com/botesjuan/Burp-Suite-Certified-Practitioner-Exam-Study?tab=readme-ov-file#jwt)  
[Prototype pollution](https://github.com/botesjuan/Burp-Suite-Certified-Practitioner-Exam-Study?tab=readme-ov-file#prototype-pollution)  
[API Testing](https://github.com/botesjuan/Burp-Suite-Certified-Practitioner-Exam-Study?tab=readme-ov-file#api-testing)  
[Access Control](https://github.com/botesjuan/Burp-Suite-Certified-Practitioner-Exam-Study?tab=readme-ov-file#access-control)  
[GraphQL API Endpoints](https://github.com/botesjuan/Burp-Suite-Certified-Practitioner-Exam-Study?tab=readme-ov-file#graphql-api)  
[CORS - Cross-origin resource sharing](https://github.com/botesjuan/Burp-Suite-Certified-Practitioner-Exam-Study?tab=readme-ov-file#cors)

**[DATA EXFILTRATION](https://github.com/botesjuan/Burp-Suite-Certified-Practitioner-Exam-Study?tab=readme-ov-file#data-exfiltration) - Stage 3**  
[XXE - XML entities & Injections](https://github.com/botesjuan/Burp-Suite-Certified-Practitioner-Exam-Study?tab=readme-ov-file#xxe-injections)  
[SSRF - Server side request forgery](https://github.com/botesjuan/Burp-Suite-Certified-Practitioner-Exam-Study?tab=readme-ov-file#ssrf---server-side-request-forgery)  
[SSTI - Server side template injection](https://github.com/botesjuan/Burp-Suite-Certified-Practitioner-Exam-Study?tab=readme-ov-file#ssti---server-side-template-injection)  
[SSPP - Server Side Prototype Pollution](https://github.com/botesjuan/Burp-Suite-Certified-Practitioner-Exam-Study?tab=readme-ov-file#sspp---server-side-prototype-pollution)  
[LFI - File path traversal](https://github.com/botesjuan/Burp-Suite-Certified-Practitioner-Exam-Study?tab=readme-ov-file#file-path-traversal)  
[File Uploads](https://github.com/botesjuan/Burp-Suite-Certified-Practitioner-Exam-Study?tab=readme-ov-file#file-uploads)  
[Deserialization](https://github.com/botesjuan/Burp-Suite-Certified-Practitioner-Exam-Study?tab=readme-ov-file#deserialization)  
[OS Command Injection](https://github.com/botesjuan/Burp-Suite-Certified-Practitioner-Exam-Study?tab=readme-ov-file#os-command-injection)

![](Pasted%20image%2020250224172638.png)
