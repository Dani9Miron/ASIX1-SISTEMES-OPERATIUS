# Sprint P2 S3 - Configuració i Administració de Dominis en Entorn Windows

## Introducció

En aquest sprint veurem com configurar i administrar dominis en un entorn Windows, gestionant comptes d'usuari, grups i perfils mòbils. També establirem polítiques de seguretat i control d'accés als recursos tant locals com de xarxa.

## Active Directory

**Active Directory** és el nom que Microsoft dona a la seva implementació del servei de directori en una xarxa distribuïda de computadors.

📖 Referència:
> Microsoft. (s. f.). *Información general sobre los servicios de dominio de Active Directory*. Microsoft Learn.  
> https://learn.microsoft.com/es-es/windows-server/identity/ad-ds/get-started/virtual-dc/active-directory-domain-services-overview

### Configuració prèvia

1. Configura un segon adaptador de xarxa a la màquina servidor de Windows:
   - Un amb NAT
   - Un amb xarxa interna (per simular ambients diferenciats)

2. A la configuració de xarxa del servidor, comprova que detecta els dos adaptadors.

3. Assigna una adreça IP fixa a un dels adaptadors utilitzant IPv4, i comprova la configuració amb el CMD.
<img width="725" height="437" alt="image" src="https://github.com/user-attachments/assets/5b6d3fa9-1c05-451a-89fb-f67912ad4f64" />
<img width="639" height="262" alt="image" src="https://github.com/user-attachments/assets/1239f7db-04fd-415f-b447-c02e6d0aa50a" />
 
<img width="719" height="421" alt="image" src="https://github.com/user-attachments/assets/8482944c-9f55-41eb-b5e5-8c8549cc4e2a" />

<img width="625" height="322" alt="image" src="https://github.com/user-attachments/assets/cb8984e2-6452-4cbd-b830-c85eb21ec0cf" />



## Configuració del Domini

### Instal·lació del rol

1. Obre l’eina **Administrador del servidor**.
2. Afegeix rols i característiques:
   - Instal·lació basada en rols.
   - Escull el servidor local.

3. Selecciona els serveis:
   - **DNS Server**
   - **Active Directory Domain Services**

4. Revisa les característiques associades i confirma la instal·lació.

5. Un cop finalitzat, apareixerà l’opció per **promoure el servidor a controlador de domini**.
<img width="727" height="322" alt="image" src="https://github.com/user-attachments/assets/4a8de4bd-74ba-4921-a54a-f24e4148ee54" />

<img width="728" height="513" alt="image" src="https://github.com/user-attachments/assets/f6ae6408-8350-40ae-9032-fb56ddd74961" />
 
<img width="721" height="509" alt="image" src="https://github.com/user-attachments/assets/ff0a17c7-7a8f-4cbd-bf23-402479b6ec03" />
<img width="706" height="510" alt="image" src="https://github.com/user-attachments/assets/701307e5-6498-4a81-9812-af191511784d" />

<img width="715" height="509" alt="image" src="https://github.com/user-attachments/assets/2a524308-e474-4207-a6a3-0f922bf87d8d" />
<img width="720" height="512" alt="image" src="https://github.com/user-attachments/assets/4bdcc323-804a-4775-a7ec-03b1e0d87cd1" />
<img width="704" height="508" alt="image" src="https://github.com/user-attachments/assets/083ca549-e842-4212-9147-326a45fb1f74" />

<img width="718" height="527" alt="image" src="https://github.com/user-attachments/assets/26fa0850-d2ec-4f61-b08d-9ca81f7c6f0f" />
 

### Promoció a controlador de domini

1. Escull:
   - Crear un **nou bosc**.
   - Assigna un **nom de domini**.

2. Defineix una **contrasenya per al directori**.

3. Apareixerà un error relacionat amb DNS (esperat), ignora’l.

4. Defineix el **nom NetBIOS** del domini.

5. Revisa tots els passos i genera, si es vol, un script d’instal·lació.

6. Finalitza la instal·lació. El servidor es reiniciarà i podràs iniciar sessió com a **Administrador del domini**.
<img width="638" height="470" alt="image" src="https://github.com/user-attachments/assets/94aff952-3d16-4e9f-b1f8-0a7a5f87af46" />
 
<img width="636" height="466" alt="image" src="https://github.com/user-attachments/assets/c85bdc26-75c6-4dae-9eed-9374e2632f19" />
 
<img width="646" height="475" alt="image" src="https://github.com/user-attachments/assets/510599af-da24-4adf-9d5e-f7e379a4158b" />

<img width="631" height="473" alt="image" src="https://github.com/user-attachments/assets/f5b637af-4acc-47af-ad99-37d9082da9f7" />
<img width="635" height="467" alt="image" src="https://github.com/user-attachments/assets/d6e15073-d305-41df-b760-5d95fc78ec0a" />

<img width="636" height="481" alt="image" src="https://github.com/user-attachments/assets/a20adebb-ce78-44cf-81aa-16916c5a98e7" />

<img width="245" height="32" alt="image" src="https://github.com/user-attachments/assets/7248ecc8-1702-45b0-8b8b-505cfecaac96" />


## Unió d’equips al domini

1. Configura la xarxa del client:
   - Porta d'enllaç i servidor DNS apuntant al servidor.

2. Verifica la IP amb `ipconfig`.

3. Fes un **ping** entre el client i el servidor (pot ser necessari desactivar el **firewall**).

4. Al client, obre **Configuració avançada del sistema > Nom d’equip** i canvia el grup.

5. Selecciona l’opció **Membre del domini** i escriu el nom del domini.

6. Rebràs un missatge de confirmació i s’haurà de **reiniciar** el client.
<img width="629" height="376" alt="image" src="https://github.com/user-attachments/assets/af37802e-96aa-466a-a786-5f2911dea1bd" />
<img width="547" height="201" alt="image" src="https://github.com/user-attachments/assets/5447a588-0530-46ce-b92b-5667a78db4c2" />
 
<img width="478" height="211" alt="image" src="https://github.com/user-attachments/assets/9ca0bcff-a701-4eb7-aa71-438947a6b3b9" />

<img width="407" height="475" alt="image" src="https://github.com/user-attachments/assets/2ec5e2d7-43fa-4b51-aa44-67961479eeba" />

<img width="319" height="385" alt="image" src="https://github.com/user-attachments/assets/3fedc8e4-636d-4e1c-927e-e49f4a1e20ce" />

<img width="326" height="148" alt="image" src="https://github.com/user-attachments/assets/ed4a3f30-e0f8-42a8-ad87-c23009fa5bc6" />

<img width="530" height="310" alt="image" src="https://github.com/user-attachments/assets/f20f7803-82ba-41d6-87d5-4bf369260173" />


## Gestió d’Usuaris

1. Obre l’eina **Usuarios y equipos de Active Directory**.

2. Navega fins a la carpeta **Usuaris** dins l'arbre del directori.

3. Amb botó dret, crea un nou usuari (ex: *Keanu*).

4. Un cop creat, des del client, a la pantalla d’inici de sessió selecciona **Altres usuaris** i escriu les credencials creades.

<img width="514" height="267" alt="image" src="https://github.com/user-attachments/assets/b6923d6a-f3c6-4bb5-99ee-39d8822453f2" />

<img width="667" height="493" alt="image" src="https://github.com/user-attachments/assets/163446f8-064f-4817-8950-778f841adb3f" />
 
<img width="438" height="382" alt="image" src="https://github.com/user-attachments/assets/36bcaf4a-5655-41bd-b511-3b6f4d0cb12e" />

<img width="436" height="373" alt="image" src="https://github.com/user-attachments/assets/4a7d4698-e851-4cf2-a56a-390cf2ff648d" />

<img width="666" height="461" alt="image" src="https://github.com/user-attachments/assets/c0149157-24fb-424d-90a2-e094fe3ad7fc" />

<img width="671" height="546" alt="image" src="https://github.com/user-attachments/assets/6d8b265b-51f3-43e0-9542-5584cc49f919" />
  
## Hores d’inici de sessió

Es poden definir horaris en què cada usuari pot iniciar sessió. Aquesta funcionalitat permet controlar que només treballin en horari laboral.

- Es configura des del perfil d’usuari dins de **Active Directory Users and Computers**.
- Si s’intenta iniciar sessió fora d’hores, no es permet l'accés.

<img width="446" height="527" alt="image" src="https://github.com/user-attachments/assets/144590da-62b5-4c11-ab88-dfc6f21203b1" />

<img width="526" height="312" alt="image" src="https://github.com/user-attachments/assets/6a7f2a6f-cfb7-476b-8982-900a77da61ae" />

<img width="667" height="499" alt="image" src="https://github.com/user-attachments/assets/a7fb30ec-61af-48cd-81c7-3894a1ed4e7a" />


## Creació i gestió de grups

1. Des del mateix entorn on creem usuaris, escollim l’opció de crear un **nou grup**.

2. Introduïm les dades del grup i assignem membres.

3. Assignem un **usuari com a administrador del grup** des de la pestanya “Administrado por”.

<img width="436" height="368" alt="image" src="https://github.com/user-attachments/assets/787d5365-c343-4616-87cc-47f3ed2670cc" />

<img width="427" height="447" alt="image" src="https://github.com/user-attachments/assets/9b587c0d-d442-4d99-8b7c-74d640f4eed1" />

<img width="550" height="445" alt="image" src="https://github.com/user-attachments/assets/d06a9cc5-f068-4536-9b7f-f9aae97f191c" />

<img width="426" height="447" alt="image" src="https://github.com/user-attachments/assets/c59cfcf0-9010-47a8-9298-1f7641d53b3c" />



## Accés remot a internet (NAT)

Per tal que el client pugui accedir a internet a través del servidor, configurem **Enrutament i accés remot**:

1. A l’Administrador del servidor, afegeix el rol **Accés remot**.

2. Inclou tots els serveis suggerits.

3. Un cop instal·lat, apareixerà un missatge per fer la configuració inicial.

4. A la finestra de configuració:
   - Selecciona **NAT**.
   - Escull l’adaptador que fa servir NAT.

5. Completa la configuració i inicia el servei d’enrutament.



<img width="664" height="472" alt="image" src="https://github.com/user-attachments/assets/52be49ab-8ae3-4893-a541-ec3188d18b10" />

<img width="665" height="471" alt="image" src="https://github.com/user-attachments/assets/2ccc3ac4-f894-45dd-9358-c8b73345ae60" />

<img width="651" height="491" alt="image" src="https://github.com/user-attachments/assets/4e8064c5-1698-4bdc-a9ca-df451dd97d25" />
<img width="602" height="415" alt="image" src="https://github.com/user-attachments/assets/525c4a33-dc3a-456b-bc3e-f3b915aa70b4" />

<img width="498" height="468" alt="image" src="https://github.com/user-attachments/assets/ce7bb18a-6b6d-47fe-b3c0-03ab8bed539a" />

<img width="489" height="474" alt="image" src="https://github.com/user-attachments/assets/94eaa3e5-b871-4490-9695-e925d714ab98" />


# Unitats Organitzatives (UO) i GPOs en Active Directory

## Què són les Unitats Organitzatives (UO)?

Les Unitats Organitzatives (OU) en un domini gestionat amb els Serveis de Domini d’Active Directory (AD DS) permeten agrupar lògicament objectes com:

- Comptes d’usuari
- Comptes de servei
- Comptes d’equip

### Per què serveixen?
- Delegació d'administració per UO
- Aplicació de Directives de Grup (GPOs) de manera específica

Referència:  
Microsoft. (s. f.). *Crear una unidad organizativa (OU) en Domain Services administrado*. Microsoft Learn.  
https://learn.microsoft.com/es-es/entra/identity/domain-services/create-ou

## Crear una Unitat Organitzativa

1. Obre l’eina Active Directory Users and Computers (`dsa.msc`)
2. Clica amb el botó dret sobre el nom del domini
3. Selecciona "Nou > Unitat Organitzativa (OU)"
4. Introdueix el nom de la UO (per exemple: `Proves`)
5. Assegura’t que l’opció "Protegeix aquest contenidor contra eliminació accidental" està activada

Un cop creada, pots:
- Afegir-hi usuaris nous
- Moure-hi usuaris existents per fer proves
<img width="664" height="456" alt="image" src="https://github.com/user-attachments/assets/0c75eeb5-6c79-4893-9c6e-7d69b5331c80" />

<img width="428" height="373" alt="image" src="https://github.com/user-attachments/assets/13c791a5-ce60-4ae8-8bc7-daa36bd45535" />

<img width="533" height="215" alt="image" src="https://github.com/user-attachments/assets/ac11904f-fedf-4fc1-9bdc-eaa4dbcf3859" />

<img width="513" height="256" alt="image" src="https://github.com/user-attachments/assets/48e2221a-ad0d-4a49-9c18-ffcedbff77fd" />


## Què és una GPO?

Una Directiva de Grup (GPO) permet configurar:

- Paràmetres d’usuari
- Paràmetres d’equip
- Opcions de seguretat i funcionament per a equips clients i servidors Windows

Referència:  
Microsoft. (s. f.). *Información general sobre la directiva de grupo*. Microsoft Learn.  
https://learn.microsoft.com/es-es/windows-server/identity/ad-ds/manage/group-policy/group-policy-overview

## Crear i vincular una GPO

1. Obre l’eina Administració de Directives de Grup (`gpmc.msc`)
2. Clica amb el botó dret sobre la UO que has creat
3. Selecciona "Crea un GPO nou en aquest domini i vincula’l aquí"
4. Dona-li un nom (per exemple: `Restriccions`)
5. Un cop creat, pots editar-lo:
   - Clic dret > Edita
   - Defineix polítiques com desactivar el panell de control, restringir accessos, etc.
<img width="631" height="421" alt="image" src="https://github.com/user-attachments/assets/493aa878-1553-421d-9002-bc06d5842b42" />

<img width="546" height="238" alt="image" src="https://github.com/user-attachments/assets/e5f27d80-88b5-4439-80ee-f6b4857907da" />

<img width="408" height="497" alt="image" src="https://github.com/user-attachments/assets/3fd3dc8d-f6ed-4bf1-9e14-da08ff1e4829" />

<img width="639" height="153" alt="image" src="https://github.com/user-attachments/assets/ba7388fe-15fc-4a0a-9953-45f04c0335ae" />

<img width="633" height="385" alt="image" src="https://github.com/user-attachments/assets/84771062-31ce-4dc0-a2c5-d85358c600fe" />

<img width="637" height="434" alt="image" src="https://github.com/user-attachments/assets/2664c1b2-27aa-4a08-ad15-811a63f921c9" />


<img width="642" height="266" alt="image" src="https://github.com/user-attachments/assets/9bad2205-14d2-4946-9e04-2878dddab707" />

<img width="330" height="186" alt="image" src="https://github.com/user-attachments/assets/dc5f295d-1932-488a-b078-339e9e03eb78" />

<img width="548" height="127" alt="image" src="https://github.com/user-attachments/assets/052328a2-c76a-498e-bf2f-2d0027dd209f" />


## Recomanació

Sempre prova les GPOs en una UO de test abans d'aplicar-les a l'organització sencera per evitar impactes no desitjats.


## Conclusions

Amb aquests passos hem configurat un entorn de domini Windows amb Active Directory, afegint usuaris, grups, limitacions d'accés per hora, i possibilitat d'accés remot a internet per part dels clients. Aquesta pràctica és essencial per entendre la gestió centralitzada d'usuaris i recursos dins d'una xarxa empresarial.



