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

Comprovem amb el client extern de **Windows**
