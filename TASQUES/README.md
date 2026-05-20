Descripció de la Tasca: Implantació de Seguretat Perimetral amb IPFire
Aquesta tasca consisteix en el desplegament, configuració i validació d'un sistema tallafocs (Firewall) i un servidor Proxy Web avançat utilitzant la distribució de codi obert IPFire. El projecte es planteja com una simulació real per implementar un entorn de xarxa segur i monitoritzat per a l'empresa FoodLogístic S.A., adaptat amb els paràmetres de direccionament específics assignats a l'alumne (Subxarxa GREEN: 192.169.25.0/24).

Els objectius i blocs tècnics clau que es treballen en aquesta pràctica són els següents:

Preparació de l'Entorn Virtual: Interconnexió d'una màquina client interna (Zorin OS) amb les interfícies de xarxa d'IPFire (GREEN per a la xarxa local LAN i RED per a la connexió cap a Internet extern).

Servidor Proxy Avançat (Web Proxy): Activació del servei Squid a la xarxa de l'empresa per centralitzar el trànsit, integrant la configuració de filtres de tipus MIME per bloquejar la descàrrega d'extensions de fitxers de risc o no desitjats.

Polítiques de Filtratge d'URL: * Categories Globals: Bloqueig d'accés a serveis complets a nivell d'empresa, com ara banca en línia (bank) i plataformes de reproducció multimèdia (radio).

Llistes Negres Personalitzades: Restricció quirúrgica de dominis específics de premsa o entorns educatius, així com filtratge avançat per URLs d'un sol perfil concret d'una xarxa social sense afectar el domini base.

Llistes Blanques: Implementació d'un entorn restrictiu tancat per a temàtiques concretes (per exemple, entreteniment/anime), on només es permet l'accés a les pàgines explícitament autoritzades per l'administrador.

Polítiques del Cortafuegos (Restricció Horària): Creació de regles de xarxa a nivell de firewall per tallar completament el trànsit de dades cap a l'exterior fora de les hores permeses (configuració de restricció horària de 00:00 a 24:00).

Auditoria, Traçabilitat i Estat: Validació pràctica des del client dels errors llançats pel sistema (com els missatges corporatius d'accés denegat o els talls de connexió SSL/TLS) i monitorització dels gràfics de tràfic (bits/s) i rendiment general de l'IPFire en temps real.
