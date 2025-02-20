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

### Extensions:

- param miner
- http smuggler
- Ysoserial en burp o tenerlo listo en el Github Codespaces (Github Pro)
- **SSRF localhost:6566 o 192.168.0.[burp intruder]**
- JWT Web Tokens - Pendiente instalar again - JWT Editor

### Burp Scan

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


