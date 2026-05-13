# Agregar Zorin a un AD 

---

### PAS 1: Creació de unitat organitzativa

Al meu servidor windows he creat la unitat organitzativa anomenada linux i he creat un grup i un usuari.


<img width="776" height="557" alt="4" src="https://github.com/user-attachments/assets/d197da79-6a61-4017-9bed-147995268718" />

---

### PAS 2: Canviar DNS en ZORIN

He canviat el DNS de la màquina de ZORIN per poderse comunicar amb la màquina WINDOWS.

<img width="1196" height="721" alt="5" src="https://github.com/user-attachments/assets/ba3d4b95-7253-495d-a6f2-bd08a4b0a3da" />

---

### PAS 3: Instal·lació de paquets

He usat la comanda *sudo apt install sssd-ad sssd-tools realmd adcli -y* per fer la instal·lació en la màquina de ZORIN

<img width="743" height="481" alt="6" src="https://github.com/user-attachments/assets/0a9e6736-1912-4094-8fa9-3db32d38b7fe" />

---

### PAS 4: Canvi de hostname a ZORIN

He anat a la màquina de ZORIN i he executat aquesta comanda per canviar el hostname
*sudo hostnamectl set-hostname foodlogistic.test*

I per comprovar: *hostname -f*


<img width="802" height="667" alt="7" src="https://github.com/user-attachments/assets/7ed3f2cd-4d52-4d02-9683-fdb92076645a" />

---

### PAS 5: Sincrtonitazió de hores entre màquines

He sincronitzat que les 2 màquines estiguin en la maiteixa hora

<img width="1920" height="943" alt="10" src="https://github.com/user-attachments/assets/46529c95-041e-4b40-8457-1b69518f3b65" />

---

### PAS 6: Connexió al domini

Primer, he verificat que el client detecta el domini amb la comanda:

*realm discover nom_del_teu_domini*   

<img width="855" height="704" alt="9" src="https://github.com/user-attachments/assets/9adc74e8-7c82-4f01-a937-199207f15b11" />


Unió (Join): Si el detecta, l'he unit amb:

*sudo realm join nom_del_teu_domini*

<img width="671" height="117" alt="11" src="https://github.com/user-attachments/assets/60955b0a-1577-4201-a8dc-1ee0907ed0c7" />

---

### PAS 7: Usuari linux

He entrat a la màquina ZORIN desde el usuari anteriorment creat al server manager

<img width="811" height="605" alt="12" src="https://github.com/user-attachments/assets/cb8f68a2-ee79-4ba8-b984-0b04d664ef86" />

---

### PAS 8: 
