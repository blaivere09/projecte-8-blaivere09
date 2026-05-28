---

# AA4 NAT i VPN

---

# Instal·lació de serveis a la màquina Zorin

A la màquina amb sistema operatiu Zorin s’instal·laran els paquets necessaris per habilitar els serveis **SSH** i **Apache**.

<img width="864" height="489" alt="image" src="https://github.com/user-attachments/assets/434e686b-f365-47b4-bc4c-d05f6460958b" />

<img width="958" height="667" alt="image" src="https://github.com/user-attachments/assets/df6be9a2-65cb-4977-9554-3eab62834de6" />

---

# Configuració per mostrar missatge 

Haurem de editar el arxiu per poder mostrar el missatge desitjat

<img width="911" height="350" alt="image" src="https://github.com/user-attachments/assets/57f253a3-3bb4-425b-ac01-ed657acce152" />

---


# Comprovació

Comprovarem accedint amb: http://localhost

<img width="874" height="367" alt="image" src="https://github.com/user-attachments/assets/8d50f3de-a80f-4032-8a5d-d3e1afac1fb6" />

---

# Destinació NAT

L’objectiu d’aquesta configuració és que un equip extern (**Client**) connectat a la xarxa **RED** pugui visualitzar la pàgina web allotjada al sistema **Zorin OS** de la xarxa **GREEN**, mitjançant l’adreça IP assignada a l’IPFire.

Per configurar-ho, des de la interfície gràfica d’IPFire accedirem a l’apartat de **Firewall** i després a **Regles de Firewall**. A continuació, afegirem una nova regla amb la configuració indicada.


<img width="1175" height="754" alt="image" src="https://github.com/user-attachments/assets/fc289b86-3e69-48b1-83bd-687732c5a286" />

<img width="1094" height="639" alt="image" src="https://github.com/user-attachments/assets/0e13199d-7aae-41fb-a4bd-36f467109c7a" />

Li donem a agregar i ja tindriem els canvis aplicats en la configuració.

---

<img width="983" height="641" alt="image" src="https://github.com/user-attachments/assets/29b64d95-ff5a-49ef-8cc4-e9c25139882f" />



# Comprovació amb el client extern de **Windows**

Des de un client de Windows he accedit a la IP del adaptador de xarxa del ipfire 

---

# VPN amb OpenVPN (Roadwarrior)

En aquest apartat configurem un accés remot segur mitjançant un túnel xifrat, evitant així exposar ports directament a Internet.

###  Generació de Certificats a l'IPFire
1. Accedeix al menú **Servicios** ➔ **OpenVPN**.
2. Com que és la primera configuració, clica el botó **Generate Root/Host Certificates**.
3. **Omple les dades del formulari** (país, organització, etc.) i confirma per **generar-los** (aquest procés pot trigar una mica).

###  Creació de l'Usuari Roadwarrior
1. Ves a la pestanya **Control y estado de conexión** i clica a **Agregar**.
2. Tria el tipus de connexió: **Red privada virtual VPN Host-to-Net (Roadwarrior)** i torna a clicar **Agregar**.
3. Dins de la configuració de la connexió, assegura't de marcar l'opció **Activat** (✓).

<img width="873" height="301" alt="image" src="https://github.com/user-attachments/assets/758f308b-c927-47c9-a446-152f2244b1e0" />

<img width="966" height="350" alt="image" src="https://github.com/user-attachments/assets/c7063b18-bc3f-4493-a0fe-f99317c3f52d" />

---

# Extracció d'arxius del client

Una vegada finalitzada la creació de l'usuari, l'IPFire obtindrà dos fitxers:
* **Serveis25.ovpn** (paràmetres de connexió OpenVPN)
* **Serveis25.p12** (certificat i clau privada)

Descarrega'ls i transféreix-los a la màquina virtual client externa (per exemple, un entorn Windows). Per fer-ho, pots fer servir plataformes d'emmagatzematge com Google Drive o serveis d'enviament de fitxers temporals per enllaç com FileMail.

<img width="980" height="195" alt="image" src="https://github.com/user-attachments/assets/911d03e1-3aa0-40da-acab-aa87b3b2af61" />

<img width="963" height="577" alt="image" src="https://github.com/user-attachments/assets/f1941f46-a845-4597-96e9-ce7b574b1fa2" />

---


# Habilitar el servei

Hem de marcar la opcio de *"Activado"*

<img width="926" height="228" alt="image" src="https://github.com/user-attachments/assets/57872701-301b-4d26-a31b-3a1dcbeda515" />

---

# Preparar el client Windows

###  Instal·lació d'OpenVPN GUI
Descarrega l'aplicació **OpenVPN GUI** des de la seva pàgina web oficial i procedeix a realitzar la instal·lació al teu sistema.

###  Edició del fitxer .ovpn (pas crític)
Obre el fitxer de configuració .ovpn utilitzant l'editor de text (com el Bloc de notes). Localitza la línia que s'inicia amb el paràmetre `remote` i substitueix l'adreça existent per la IP corresponent a la interfície RED de l'IPFire. Finalment, desa les modificacions aplicades.

<img width="869" height="622" alt="image" src="https://github.com/user-attachments/assets/81b59c37-a4f7-428a-9882-1c528f552f32" />

###  Configuració de la carpeta de perfils

Fes **clic secundari** a la icona del programa **OpenVPN** i tria la funció **Import files** per triar el teu fitxer `.ovpn`. El sistema obrirà una carpeta específica per a aquest perfil a l'adreça `C:\Users\usuari\OpenVPN\config\`. Perquè tot funcioni correctament, assegura't de moure també el certificat `.p12` a aquesta mateixa ubicació.


<img width="974" height="406" alt="image" src="https://github.com/user-attachments/assets/a94c06b3-5c4f-4d99-a33f-312215e5cca6" />

###  Modificació del fitxer hosts de Windows (Opcional)

Amb l'objectiu de garantir la resolució de noms correcta per al domini `ipfire.foodlogistic.test` definit a la configuració del vostre `.ovpn`, cal modificar el fitxer del sistema situat a la ruta `C:\Windows\System32\drivers\etc\hosts`. 

Per fer-ho, obriu l'editor de text amb permisos d'**administrador** i introduïu la línia següent al final del document:
`192.169.25.254  ipfire.foodlogistic.test`

---

# Conectar VPN

Farem click i introduirem la contrassenya anteriorment posada.

<img width="487" height="269" alt="image" src="https://github.com/user-attachments/assets/d13d9785-e5e9-412c-a68b-a61111eb3636" />

Rebrem un missatge amb una Ip.

Ara comprovarem que tot funciona be.

# Comprovació

<img width="631" height="82" alt="image" src="https://github.com/user-attachments/assets/36600bc7-6509-40e4-8746-d06ba5841496" />

<img width="511" height="242" alt="image" src="https://github.com/user-attachments/assets/32cbc871-27cf-4652-8510-0be192755ea9" />

---

***fi***

---
