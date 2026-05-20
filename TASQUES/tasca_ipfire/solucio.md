

---

# MANUAL TÈCNIC D'IMPLANTACIÓ I SEGURETAT AMB IPFIRE

**Projecte:** Disseny de Seguretat per a FoodLogístic S.A.

**Mòdul:** Serveis de Xarxa (CFGM SMX)

**Configuració:** Alumne Número 25

---

## FASE 0: Desplegament i Preparació de l'Entorn Virtual

Abans de començar amb l'activació dels serveis de filtratge, es realitza el desplegament i la interconnexió del sistema tallafocs (IPFire) i l'equip de xarxa interna (Zorin OS) mitjançant el programari de virtualització Oracle VirtualBox.

### Pas 0.1: Arrencada del Servidor IPFire

Es posa en marxa la màquina del tallafocs. Durant la càrrega del sistema basat en Linux, es valida que els serveis principals s'inicien correctament (`[ OK ]`). S'estableix el nom de l'equip (*hostname*) com a `FW25.foodlogistic.test` i s'aixeca de forma automatitzada la interfície de xarxa local **green0** amb la direcció IP gateway `192.169.25.254`.

![captura](/TASQUES/tasca_ipfire/ip_fire/1.png)

### Pas 0.2: Inicialització de la Màquina Client (Zorin OS)

Es procedeix a l'arrencada de l'entorn de treball de l'usuari/client sota el sistema operatiu Zorin OS. Aquest terminal s'utilitzarà per fer les proves de navegació i gestionar de forma remota l'IPFire.

<img width="754" height="501" alt="2" src="https://github.com/user-attachments/assets/403f0086-4ec6-4cf0-ad9b-9a72c4e3256d" />


### Pas 0.3: Configuració de Paràmetres IP Estàtics al Client

Dins de l'entorn de Zorin OS, s'accedeix a la configuració de la connexió cablejada per assignar manualment el direccionament de la subxarxa interna vinculada al número de llista 25:

* **Mètode IPv4:** Manual
* **Adreça IP:** `192.169.25.1`
* **Màscara de xarxa:** `255.255.255.0`
* **Porta d'enllaç:** `192.169.25.254` *(IP de la interfície GREEN de l'IPFire)*
* **Servidor DNS:** `8.8.8.8`

![captura](/TASQUES/tasca_ipfire/ip_fire/3.png)

### Pas 0.4: Accés Remot a la Interfície Web de Gestió (WebGUI)

Obrim el navegador a la màquina client i introduïm l'adreça de seguretat `https://192.169.25.254:444`. Després d'acceptar l'avís de seguretat del certificat digital auto-signat, s'accedeix al tauler principal d'IPFire on es visualitza l'estat actual de les interfícies:

* **Xarxa RED (Internet):** Connectat amb IP dinàmica `10.0.2.8` (Gateway `10.0.2.1`).
* **Xarxa GREEN (LAN):** Assignat a la xarxa `192.169.25.254/24` (Estat inicial: *Proxy Apagado*).

![captura](/TASQUES/tasca_ipfire/ip_fire/4.png)

---

## FASE 1: Configuració del Servidor Proxy Web (Web Proxy)

L'activació del proxy web permetrà centralitzar i analitzar tot el trànsit HTTP/HTTPS provinent de la xarxa d'àrea local de FoodLogístic S.A.

### Pas 1.1: Panell del Proxy Web Avançat i Filtre d'URL

Es navega al menú superior **Red** > **Web Proxy** per accedir als paràmetres avançats. En un primer moment s'identifiquen els ports predeterminats del sistema (Port del proxy: `800` i Port transparent: `3128`) així com la casella de verificació desactivada per al component **Filtro de URL**.

![captura](/TASQUES/tasca_ipfire/ip_fire/5.png)

### Pas 1.2: Activació del Control de Seguretat per Tipus MIME

Es desplaça la pantalla cap a la part inferior per configurar les restriccions del proxy. Es localitza la secció de control i s'activa la casella **Filtro de tipos MIME**. Aquesta funcionalitat permetrà interceptar i denegar la descàrrega de fitxers binaris o extensions potentment perilloses basant-se en la seva capçalera MIME.

![captura](/TASQUES/tasca_ipfire/ip_fire/6.png)

### Pas 1.3: Disseny Inicial de l'Estructura del Filtre d'URL

S'accedeix a la secció **Red** > **Filtro de URL**. El panell mostra les zones per a la definició de polítiques de seguretat personalitzades, dividides en:

* **Lista Negra personalizada:** Dominis i URLs bloquejats per l'administrador.
* **Lista Blanca personalizada:** Dominis i URLs permesos explícitament (ignorant restriccions genèriques).

![captura](/TASQUES/tasca_ipfire/ip_fire/7.png)

### Pas 1.4: Habilitació del Servei i Assignació de la Zona GREEN

Es torna a la pestanya de configuració del Proxy Web per realitzar la posada en marxa definitiva del servei:

1. Es marca la casella **Activado en Green**.
2. S'activa definitivament la verificació del **Filtro de URL**.
3. S'estableix l'idioma de missatges d'error en espanyol (`es`).

![captura](/TASQUES/tasca_ipfire/ip_fire/8.png)

### Pas 1.5: Verificació del Certificat del Servidor

Es comprova que la pestanya de navegació manté la comunicació xifrada sota el domini i la identitat establerta de la màquina tallafocs securitzada de l'empresa.

![captura](/TASQUES/tasca_ipfire/ip_fire/9.png)

### Pas 1.6: Càrrega i Visualització de les Categories del Filtre

Un cop s'ha inicialitzat i actualitzat correctament el mòdul del filtre d'adreces, el panell de **Configuración de Filtro de URL** mostra el llistat complet de categories mundials emmagatzemades (com *ads*, *adult*, *audio-video*, *bank*, *cryptojacking*, *drugs*, *gambling*, *hacking*, *radio*, entre moltes d'altres) preparades per ser seleccionades.

![captura](/TASQUES/tasca_ipfire/ip_fire/10.png)

---

## FASE 2: Polítiques de Filtratge d'URL

### Pas 2.1: Selecció de Categories de Llistes Negres Corporatives

Dins del llistat de categories globals del **Filtro de URL**, busquem i marquem de forma específica les caselles de verificació corresponents a **bank** (banca i entitats financeres) i **radio** (reproducció de contingut d'àudio en llínia) per restringir-ne l'accés a tota la xarxa de l'empresa.

![captura](/TASQUES/tasca_ipfire/ip_fire/11.png)

### Pas 2.2: Aplicació i Reinici dels Serveis de Filtratge

Un cop seleccionades les categories desitjades, es baixa fins a la part inferior de la interfície de configuració de l'IPFire i es fa clic sobre el botó **"Guardar y Reiniciar"**. Aquesta acció reconfigura i reinicia els dimonis de filtratge squid per tal d'actualitzar les bases de dades operatives amb les noves restriccions aplicades.

...

![captura](/TASQUES/tasca_ipfire/ip_fire/12.png)

---

## FASE 3: Personalització de Bloquejos (Llistes Negres i Blanques Pròpies)

### Pas 3.1: Bloqueig de Dominis Específics a la Llista Negra Personalitzada

Per tal de restringir l'accés a pàgines de premsa i portals educatius no vinculats a l'activitat de l'empresa, s'utilitza la secció **"Lista Negra personalizada"**.

1. S'introdueixen a l'apartat *Dominios bloqueados (uno por línea)* els valors:

* `elnacional.cat`
* `tecnocampus.cat`

2. Es marca la casella de verificació **"Activar Lista Negra personalizada"**.
3. Es desen els canvis aplicant la comanda del programari.

![captura](/TASQUES/tasca_ipfire/ip_fire/13.png)

### Pas 3.2: Filtratge Quirúrgic d'una URL Concreta

L'IPFire permet implementar polítiques de filtratge avançat que distingeixen entre un domini base complet i una adreça de recurs específica. En aquest supòsit, es vol prohibir un perfil concret d'una xarxa social d'un personatge famós. S'afegeix l'adreça sencera a la caixa de text **"URLs bloqueada (una por línea)"** i s'activa la regla.

![captura](/TASQUES/tasca_ipfire/ip_fire/14.png)

### Pas 3.3: Comprovació de Denegació del Perfil de la Xarxa Social

Es realitza la prova des de la màquina client Zorin OS introduint l'adreça exacta del perfil bloquejat en el pas anterior. Com es pot observar, el motor del filtre d'URL de l'IPFire intercepta la petició HTTP/HTTPS, denega la connexió i llança una pàgina d'error corporativa que indica de forma explícita que l'accés a aquesta URL està terminantment prohibit (*Acceso denegado!*).

![captura](/TASQUES/tasca_ipfire/ip_fire/15.png)

### Pas 3.4: Validació de l'Accés Permès al Domini Base de la Plataforma

A l'efecte de comprovar el correcte funcionament granular del filtre, des del mazeix navegador de la màquina client s'intenta accedir al domini genèric principal `instagram.com`. El sistema d'IPFire valida correctament la petició i permet la càrrega de la interfície general, demostrant que el bloqueig s'aplica exclusivament a la URL exacta definida a la llista negra i no a toda la xarxa social.

![captura](/TASQUES/tasca_ipfire/ip_fire/16.png)

### Pas 3.5: Configuració de Polítiques Basades en Llistes Blanques (Entorn d'Anime)

S'estableix un scenari restrictiu d'estil llista blanca en l'apartat de continguts d'entreteniment (Anime). Per fer-ho, introduïm a la secció **"Lista Blanca personalizada"** (apartat d'adreces de dominis permesos) la pàgina web de referència de la temàtica que sí que estarà autoritzada per a la seva visualització. Tot seguit, es marca la casella **"Activar Lista Blanca personalizada"** i es guarden les preferències.

![captura](/TASQUES/tasca_ipfire/ip_fire/17.png)

### Pas 3.6: Resolució de Bloqueig per Continguts d'Anime No Autoritzats

En obrir el navegador a la màquina d'usuari i intentar accedir a qualsevol altre portal o pàgina web relacionada amb la temàtica de l'anime que no s'hagi llistat de manera explícita a la llista blanca anterior, el mòdul de seguretat de l'IPFire actua bloquejant de forma immediata el pas de dades i mostrant en pantalla el missatge d'accés denegat per política del proxy.

![captura](/TASQUES/tasca_ipfire/ip_fire/18.png)

---

## FASE 4: Polítiques de Seguretat al Cortafuegos (Restricció Horària)

### Pas 4.1: Definició i Paràmetres d'una Regla de Temps al Tallafocs

Es fa el salt al mòdul de nivell de xarxa de l'equip accedint a **Cortafuegos** > **Reglas del cortafuegos**. Es crea una nova regla de seguretat avançada on es defineix l'origen de la subxarxa interna i es configura l'apartat inferior **"Restricción de tiempo"**. S'estableixen de forma estricta els paràmetres temporals:

* **Dies d'aplicació:** Dilluns, Dimarts, Dimecres, Dijous, Divendres, Dissabte i Diumenge (tots seleccionats).
* **Franja de temps del tall:** Des de les `00:00` hores fins a les `24:00` hores.

![captura](/TASQUES/tasca_ipfire/ip_fire/19.png)

### Pas 4.2: Auditoria i Validació Tècnica del Registre del Cortafuegos

Es valida la taula global de regles de firewall actives en l'IPFire per confirmar la implantació de la regla. En l'apartat de l'esquema d'accessos, s'audita visualment que la regla està corrent sota la definició correcta, mostrant les propietats del filtre aplicat, l'origen de la xarxa, el destí de les peticions i el rellotge de restricció horària de format complet operatiu en el sistema.

![captura](/TASQUES/tasca_ipfire/ip_fire/20.png)

---

## FASE 5: Validació de Seguretat i Traçabilitat del Sistema

Un cop aplicades totes les polítiques de filtratge i seguretat a nivell de xarxa i aplicació (Proxy i Cortafuegos), es realitzen les proves de càrrega i auditories de funcionament directament des dels terminals d'usuari de l'empresa.

### Pas 5.1: Comprovació del Bloqueig per llistes d'Horari (Tallafocs)

Amb la regla temporal del cortafuegos completament activa, s'intenta iniciar qualsevol tipus de comunicació externa cap a la xarxa RED des del navegador de la màquina de treball. El sistema del tallafocs intercepta la petició de connexió d'origen i llança immediatament una advertència de seguretat SSL/TLS indicant que s'ha tallat el flux de dades de forma expressa, evitant la navegació fora de l'horari autoritzat.

![captura](/TASQUES/tasca_ipfire/ip_fire/21.jpg)

### Pas 5.2: Anàlisi Granular del Bloqueig Temàtic de Ràdio i Banca

Es reverteix temporalment el tall total de xarxa per auditar el comportament de les primeres llistes negres globals configurades. En intentar accedir a una adreça de reproducció multimèdia en línia o ràdio web (com ara un portal generalista d'àudio o *streaming*), l'IPFire respon de forma instantània aplicant el mòdul *URL Filter*, denegant l'accés amb l'error de categoria en espanyol configurat prèviament.

![captura](/TASQUES/tasca_ipfire/ip_fire/22.png)

### Pas 5.3: Gestió Tècnica dels Dominis Blocs des de la Taula Interna

S'accedeix al menú de manteniment de l'IPFire per realitzar tasques de control del motor de cerca del proxy. Des d'aquí es pot avaluar com respon la infraestructura davant de canvis dinàmics en la llista negra personalitzada, observant com queden registrats els dominis d'actualitat catalana i portals universitaris (`elnacional.cat` i `tecnocampus.cat`) dins de l'historial d'accions pendents de validació.

![captura](/TASQUES/tasca_ipfire/ip_fire/23.png)

### Pas 5.4: Monitorització de l'Estat Global i Tràfics del Firewall

Per finalitzar la pràctica, s'accedeix a la pantalla d'**Estado**. En aquest apartat es valida que el servei IPFire està operant al 100% de la seva capacitat, mesurant els paràmetres de tràfic d'entrada i sortida en temps real (en *bits/s*), el recompte de memòria de la memòria cau utilitzada i la persistència de connexió de la interfície d'Internet (RED) per garantir el correcte funcionament de toda la infraestructura de xarxa dissenyada.

![captura](/TASQUES/tasca_ipfire/ip_fire/24.png)

---

***Fi.***

---

