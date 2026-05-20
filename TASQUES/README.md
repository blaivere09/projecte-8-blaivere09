# 🛡️ Resum de la Tasca: Seguretat i Filtratge de Xarxa amb IPFire

## 🎯 Objectiu de la Pràctiques
L'objectiu principal d'aquesta tasca és dissenyar i implementar la infraestructura de seguretat perimetral per a l'empresa **FoodLogístic S.A.** utilitzant la distribució Linux **IPFire**. Mitjançant el desplegament d'un tallafocs i la configuració d'un servidor Proxy avançat, s'aconsegueix un control total, auditable i granular de l'activitat de la xarxa local.

---

## 💻 Descripció de les Fases Realitzades

### 1. Preparació de l'Entorn Virtual (Fase 0)
* Es desplega el tallafocs IPFire connectat en mode pont/NAT cap a Internet (**Interfície RED**) i connectat en xarxa interna (**Interfície GREEN**) amb la IP `192.169.25.254`.
* Es configura un client web amb el sistema operatiu **Zorin OS** utilitzant un direccionament IP estàtic dins del mateix rang (`192.169.25.1`) per tal de gestionar el tallafocs mitjançant la interfície web de gestió (WebGUI) al port `444`.

### 2. Configuració del Servidor Proxy i Filtre d'URL (Fase 1 i 2)
* S'activa el **Web Proxy** a la zona GREEN per centralitzar tot el trànsit de navegació.
* S'implementa seguretat addicional activant el **Filtre de tipus MIME** per bloquejar la descàrrega de fitxers executables o binaris potencialment perillosos.
* Es carregaven les categories globals de bloqueig i es restringeix l'accés a nivell d'empresa a serveis de **banca (bank)** i reproducció multimèdia o **ràdio en línia (radio)**.

### 3. Personalització de Restriccions Quirúrgiques (Fase 3)
* **Llista Negra:** Es bloquegen dominis complets com `elnacional.cat` i `tecnocampus.cat`. També es demostra el filtratge granular prohibint una URL o perfil específic d'una xarxa social sense afectar el domini base de la plataforma.
* **Llista Blanca:** S'aplica una política restrictiva per a entorns d'entreteniment (Anime), on només es permet l'accés a una única web autoritzada, bloquejant automàticament tota la resta de pàgines de la mateixa temàtica.

### 4. Control Horari al Cortafuegos (Fase 4 i 5)
* Es dissenya una regla de tall total de xarxa a l'IPFire utilitzant la **Restricció de temps (Time Restriction)** de `00:00` a `24:00` hores.
* Es valida des del client que el tall de comunicació és efectiu a nivell de xarxa, provocant errors de connexió segura (SSL/TLS) en horaris no permesos.

---

## 📈 Validació Final del Sistema
Es realitza una auditoria des de l'apartat **"Estado"** de l'IPFire per monitoritzar el rendiment del tallafocs, l'ús de la memòria cau del proxy i el tràfic de dades en temps real (bits/s), garantint que la xarxa corporativa de FoodLogístic S.A. és completament robusta, eficient i segura.
