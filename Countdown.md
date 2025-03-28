# Countdown

**Tema**: Digital Forensics

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image.png)

### **Escenario:**

La policía de Nueva York recibió información de que una banda de atacantes ingresó a la ciudad y planea detonar un artefacto explosivo. Las autoridades han comenzado a investigar todas las pistas para determinar si esto es cierto o un engaño.

Se detuvo a personas de interés y un sospechoso adicional llamado "Zerry" fue detenido mientras los agentes allanaban su casa. Durante la búsqueda encontraron una computadora portátil, recolectaron la evidencia digital y la enviaron a la división forense digital de la ciudad de Nueva York.

La policía cree que Zerry está directamente asociado con la pandilla y está analizando su dispositivo para descubrir cualquier información sobre el posible ataque.

**Descargo de responsabilidad:** la historia, todos los nombres, personajes e incidentes retratados en este desafío son ficticios y cualquier relevancia para los eventos del mundo real es completamente coincidencia.

**En una carrera contra el tiempo, ¿podrás investigar una computadora portátil incautada por las fuerzas del orden para identificar si una amenaza de bomba es real o un engaño?**

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%200.png)

# Presentación de investigación

Empezamos:

Damos click en “Start Investigation” y se abrira nuesta maquina virtual donde trabajaremos.

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2001.png)

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2002.png)

### 1.Verifique la imagen del disco. Enviar SectorCount y MD5

💡**Sugerencia:** Lea el archivo Zerry.E01.txt que se generó durante la recopilación de pruebas.

Entrar a la carpeta “Investigation Files” que se encuentra en el escritorio y entramos a la carpeta “Disk Image”.

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2003.png)

Dentro de Disk Image entramos a Zerry

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2004.png)

Abrimos Zerry.E01.txt y buscamos lo que nos pide:

- Sector Count
- MD5 checksum

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2005.png)

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2006.png)

**Respuesta:** 25,165,824 , 5c4e94315039f890e839d6992aeb6c58

### 2.¿Cuál es la clave de descifrado de la aplicación de mensajería online utilizada por Zerry?

💡**Sugerencia: V**erifique los listados de Programas instalados + Búsqueda previa de Windows en Autopsy para identificar las aplicaciones instaladas. Busque aplicaciones de mensajería en línea (especialmente aquellas que puedan usarse para una comunicación segura).

Una vez que crea que ha encontrado el programa adecuado, intente buscar en línea la "clave de descifrado del nombre de la aplicación". ¡Autopsy se puede utilizar para extraer archivos de la imagen del disco si necesita profundizar más!

Abrimos Autopsy, que se encuentra en el escritorio

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2007.png)

Hacemos click en “Open Recent Case” y selecionamos Countdown y click en Open

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2008.png)

Una vez ya cargado nuesto caso, lo que haremos sera buscar el archivo que necesitamos, para esto debes seguir esta direccion para encontrar el archivo:

Data Source > Zerry.E01 > vol3(NTFS/exFAT(0x07):104448-24125556) >Users >Zerry🍎 >AppData > Roaming > Signal > config.json

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2009.png)

Al archivo config.json hacemos click dercho y click en Extract File(s)

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2010.png)

Y lo extraemos en el escritorio 

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2011.png)

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2012.png)

Abrimos el archivo config.json que esta en el esritorio. Y ahi tenemos la respuesta

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2013.png)

**Respuesta**: c2a0e8d6f0853449cfcf4b75176c277535b3677de1bb59186b32f0dc6ed69998

### 3.¿Cuál es el número de teléfono registrado y el nombre de perfil de Zerry en la aplicación de mensajería utilizada?

💡Sugerencia: Puede abrir la base de datos SQL de la aplicación utilizando una de las herramientas instaladas para usted.

Entrar a la carpeta “Investigation Files” que se encuentra en el escritorio luego entramos a la carpeta “Tools” y abrimos SQLiteDatabaseBrowserPortable

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2014.png)

En la misma direccion de la pregunta 2, vamos a abrir sql, deberia ser asi:

Data Source > Zerry.E01 > vol3(NTFS/exFAT(0x07):104448-24125556) >Users >Zerry🍎 >AppData > Roaming > Signal > sql >db.sqlite

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2015.png)

Extraemos el archivo “db.sqlite” al escritorio

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2016.png)

Ahora entramos a SQLiteDatabaseBrowserPortable y click en “Open Database” , buscamos en Desktop y abrimos el archivo db.sqlite

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2017.png)

Se abrira una ventana donde nos pedira la contraseña, para esto primero cambiamos “Passphrase” por “Raw key”

En Password añadimos: 0x , y al costado pegamos lo que es la llave que es la respuesta de la pregunta 2.

Seria: 0xc2a0e8d6f0853449cfcf4b75176c277535b3677de1bb59186b32f0dc6ed69998

Lo demas lo dejamos por defecto y hacemos click en OK

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2018.png)

Se nos abrira la Base de Datos

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2019.png)

Luego vamos a la tabla “conversations” , damos click derecho y click en Browse Table

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2020.png)

Dentro de la tabla encontramos lo que es el telefono y perfil

![](6https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2021.png)

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2022.png)

Para el caso del emoji que sale en el nombre, buscaremos en emojipedia. Buscamos Fire y copiamos el emoji

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2023.png)

**Respuesta:** 13026482364,ZerryThe🔥 

### 4.¿Cuál es el ID de correo electrónico que se encuentra en el chat?

💡Sugerencia: Mire diferentes tablas dentro de la base de datos.

Click derecho en “messages” y hacemos click en browse table

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2024.png)

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2025.png)

Podemos ver la conversacion y saber el contexto. Buscamos el ID del correo

**Respuesta:** eekurk@baybabes.com

### 5.¿Cuál es el nombre del archivo (incluida la extensión) que se recibe como archivo adjunto por correo electrónico?

💡Sugerencia: Los Documentos recientes pueden ayudarle a identificar esto, con el contexto de los registros de chat.

Entramos al Autopsy y vamos: Extracted Content << Recent Documents . Ahi encontramos el nombre del archivo 

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2026.png)

Nos vamos a Emojipedia y buscamos los emojis que necesitamos

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2027.png)

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2028.png)

**Respuesta:** ⌛📅.png

### 6.¿Cuál es la fecha y hora del ataque planeado?

💡Sugerencia: Exportar thumbcache_256.db de /Users/Zerry/AppData/Local/Microsoft/Windows/Explorer via Autopsy. Abra este archivo usando Thumbcache Viewer y observe las imágenes.

-Entramos a Autopsy y seguimos esta secuencia :

/Users/Zerry/AppData/Local/Microsoft/Windows/Explorer

Una vez dentro buscamos el archivo thumbcache_256.db , damos click derecho y Extract File(s) . Lo extraemos en el escritorio

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2029.png)

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2030.png)

Vamos a la carpeta Investigation Files que se encuentra en el escritoio, luego a la carpeta Tools y abrimos el “thumbcache_viewer”

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2031.png)

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2032.png)

Una vez abierta damos click en “File” y luego a “Open” , buscamos el archivo que extraimos en el escritorio “thumbcache_256”.

Observamos que la mayoria son de 0KB , pero uno es de 9KB donde se encuentra la fecha.

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2033.png)

Respuesta: 01-02-2021 09:00 AM

### 7.¿Cuál es la ubicación GPS de la explosión? El formato es el mismo que se encuentra en la evidencia. [Sugerencia: codificar (XX grados, XX minutos, XX segundos)]

💡Sugerencia: Es posible que esta información se haya almacenado en una nota adhesiva. Encuentra esto en /Users/Zerry/AppData/Local/Packages and export it.

Abra el archivo de base de datos plum, sqrlite en el /LocalState/ directory using SQLiteDatabaseBrowser.

Encuentre en qué tabla están almacenadas las notas. Podemos descubrir cómo descifrar el resultado codificado verificando los sitios visitados recientemente a través de Tor en Autopsy mirando /Tor Browser/Browser/TorBrowser/Data/Browser/profile.default/places.sqlite

Entramos a Autposy y buscamos la siguiente direccion : /Users/Zerry/AppData/Local/Packages

Buscamos la carpeta Microsoft.MicrosoftStickyNotes_8wekyb3d8bbwe y extraemos al escritorio toda la carpeta

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2034.png)

Abrimos SQLiteDatabaseBrowserPortable , luego click en Open Database , buscamos la carpeta en escritorio que es Microsoft.MicrosoftStickyNotes_8wekyb3d8bbwe , luego abrimos Local State y hacemos click al archivo plum.sqlite

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2035.png)

Click derecho a la tabla “Note” y click en Browse Table

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2037.png)

Copiamos lo que se encuentra en la columna “Text”

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2038.png)
Borramos la primera parte y dejamos desde “40 qrterrf …” hasta el ultimo digito 

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2039.png)

En Autopsy buscamos esta direccion TorBrowser/Browser/TorBrowser/Data/Browser/profile.default/places.sqlite

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2040.png)

Y extraemos al escritorio el archivo places.sqlite

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2041.png)

Abrimos el archivo con SQLiteDatabaseBrowserPortable, haciendo click en Open Database y buscando el archivo places.sqlite

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2042.png)

Abrimos el archivo “moz_places” con clik derecho y en “Browse Table”

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2043.png)

Observamos que es encirptado en rot13

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2044.png)

Abrimos el CyberChef que se encuentra en el escritorio

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2045.png)

En input ponemos lo que teniamos el “40 qrterrf …” y en Recipe el “ROT13”

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2046.png)

Entonces nos sale la respuesta

### Felicidades, completaste todas las respuestas:

![](https://github.com/EnocRosales20/Investigation_Countdown/blob/main/images/image%2047.png)
