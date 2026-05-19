# AA5 PRÀCTICA: Analitzador de protocols Wireshark

---

# PAS 1 — Obrir Wireshark

Primer he obert el programa **Wireshark**.

Després, he seleccionat la interfície de xarxa activa, que normalment és una de les següents:

- `eth0`
- `enp0s3`
- `enp0s8`

Finalment, he comprovat que es veia trànsit de xarxa movent-se.


<img width="909" height="675" alt="1" src="https://github.com/user-attachments/assets/4fbb0033-15cc-444a-84d0-b60df7129559" />

---

# PAS 2 — Començar captura

<img width="842" height="611" alt="2" src="https://github.com/user-attachments/assets/05e316c3-4502-42de-96bf-5c1245712984" />

---

# PAS 3 — Fer un ping

Després, he obert el terminal.

A continuació, he executat la següent comanda per fer un ping a l’adreça `8.8.8.8`:

```bash
ping 8.8.8.8

```

<img width="660" height="467" alt="3" src="https://github.com/user-attachments/assets/ee74cc94-527e-4f74-9ff6-65ff58034636" />

---

### ATUREM LA CAPTURA

<img width="806" height="96" alt="4" src="https://github.com/user-attachments/assets/e9463595-15b4-41f5-9c88-8f8857d248c6" />

---

# PAS 5 — Filtrar ICMP

Després, he anat a la barra superior on diu **Display Filter**.

A continuació, he escrit el filtre següent:

```text
icmp

```

<img width="821" height="78" alt="6" src="https://github.com/user-attachments/assets/e2d260de-1398-4e31-8506-781b612037d9" />

---

# 2. MODE PROMISCU

# PAS 1 — Activar mode promiscu a VirtualBox

Primer, he obert **VirtualBox**.

Després, he anat a la configuració de la màquina virtual.

A continuació, he seguit aquesta ruta:

- **Xarxa**
- **Adaptador Pont**
- **Avançat**

Finalment, al camp **Mode promiscu**, he seleccionat l’opció:

```text
Permetre-ho tot

```

<img width="877" height="503" alt="7" src="https://github.com/user-attachments/assets/3a13f9c8-9f79-4ad2-bb4d-9efd20facbb4" />

---

#  Tornar a capturar

Després, he iniciat una nova captura a **Wireshark**.

---


# Exercici 2 — DNS

Primer, he aplicat el filtre següent a Wireshark:

```text
dns && ip.addr == 192.168.c.x

```

Després, he generat trànsit DNS des del terminal executant una d’aquestes comandes:

nslookup www.xtec.cat

A continuació, a Wireshark, he observat tant la consulta DNS com la resposta.

Finalment, he comprovat que la resposta contenia l’adreça IP de www.xtec.cat, la mateixa que també s’obté amb nslookup.

<img width="835" height="260" alt="8" src="https://github.com/user-attachments/assets/a4f74912-e3e7-4aaa-a27b-4dbe55df984a" />

---

<img width="568" height="345" alt="9" src="https://github.com/user-attachments/assets/9717c8b8-2d1b-49e9-82a7-7cd9ca1a27cf" />


---


# 4. ARP

## PAS 1 — Filtre ARP

Primer, he aplicat el filtre següent a Wireshark:

```text
arp

```

<img width="831" height="43" alt="10" src="https://github.com/user-attachments/assets/3af067e3-ea6e-4d12-905b-1f693cce0762" />

---

<img width="154" height="302" alt="11" src="https://github.com/user-attachments/assets/81c249c2-7b6d-4dca-ba46-50f07e93e5c1" />

---

# PAS 2 — Buscar gateway

Després, he buscat paquets ARP del tipus:

```text
Who has 192.168.X.254?

```

---

# PART 2 — ANÀLISI DE CAPTURES PCAP

Després, he obert els fitxers de captura següents a Wireshark:

```text
captura1.pcapng
captura2.pcapng

```

<img width="615" height="239" alt="12" src="https://github.com/user-attachments/assets/73044cf5-d4ca-4ae1-8de6-23cd72e719d1" />

---


# OBRIR PCAP

Primer, he obert **Wireshark**.

Després, he anat al menú:

- **File**
- **Open**

Finalment, he seleccionat el fitxer de captura `.pcapng` per obrir-lo.

<img width="826" height="712" alt="13" src="https://github.com/user-attachments/assets/bbcfc4e6-8159-4278-84a8-59b5f56570ff" />

---

# EXERCICI 1 — ARP

Primer, he aplicat el filtre següent a Wireshark:

```text
arp && ip.addr == 192.168.1.1

```

Si no ha funcionat, he utilitzat el filtre més general:

arp

A continuació, he buscat manualment el missatge:

```

192.168.1.1 is at ...

````

Finalment, he identificat l’adreça MAC associada a la IP 192.168.1.1.

```
````
<img width="875" height="436" alt="14" src="https://github.com/user-attachments/assets/c2fee71a-c0a4-4643-b042-5e9f9d24cc6d" />

---

# 4.2 FTP (contrasenya i fitxer)

Primer, he aplicat el filtre següent a Wireshark:

```text
ftp

```

<img width="820" height="383" alt="15" src="https://github.com/user-attachments/assets/5d127eba-2fc4-4d58-bd14-fda9f16319fa" />

---

# Telnet (nau espacial)

Primer, he aplicat el filtre següent a Wireshark:

```text
telnet

```

<img width="956" height="449" alt="16" src="https://github.com/user-attachments/assets/70384a44-eed0-4e20-90fa-fae2bae06dae" />

<img width="846" height="819" alt="17" src="https://github.com/user-attachments/assets/d02308e4-4e0a-4c97-801f-1df1f9785afa" />

<img width="798" height="744" alt="18" src="https://github.com/user-attachments/assets/47922679-3fe4-45e4-93b0-07097c49b784" />


---


# SSH (paquet de 326 bytes)

Primer, he aplicat el filtre següent a Wireshark:

```text
ssh

```

