## [ Sprint3]
### [1.Instal·lació domini LDAP]

# Instal·lació domini LDAP

## Què és un domini LDAP?

Un domini LDAP (Lightweight Directory Access Protocol) és una estructura organitzativa jeràrquica utilitzada per administrar i gestionar informació sobre usuaris, grups, recursos i altres elements dins d’una xarxa. Actua com un repositori centralitzat per a l’autenticació i el control d’accés, permetent que diferents sistemes i aplicacions comparteixin informació sobre usuaris i permisos.

Dins d’un directori LDAP, les Unitats Organitzatives (UO) serveixen com a contenidors per estructurar usuaris, grups i altres objectes de manera més ordenada. Aquestes UO permeten una administració més eficient, ja que poden agrupar-se segons criteris com departaments, ubicacions o rols dins de l’organització.

## Pasos per a la instal·lació d'un domini LDAP

### 1. Configuració inicial

El primer que cal fer és comprovar la IP del servidor. En aquest cas, la configurarem manualment i verificarem la seva connectivitat fent un ping.

Després, modificarem el nom de la màquina host. Per fer-ho, editarem el fitxer `/etc/hostname` i també farem els canvis corresponents al fitxer `/etc/hosts`.
<img width="664" height="181" alt="image" src="https://github.com/user-attachments/assets/23e0504c-7541-4ff2-bed4-65a3257836d9" />

<img width="673" height="464" alt="image" src="https://github.com/user-attachments/assets/9fc94b43-15d0-46fa-a5e1-e4410d711875" />

<img width="673" height="320" alt="image" src="https://github.com/user-attachments/assets/94b351a4-744f-4f73-bbb0-c297cf7c8a45" />

<img width="440" height="74" alt="image" src="https://github.com/user-attachments/assets/26a09467-47b6-48b0-8500-ee04e3e9cf5e" />

<img width="461" height="180" alt="image" src="https://github.com/user-attachments/assets/fa5019c7-3a29-49ad-bd17-630a7771f624" />




### 2. Instal·lació del servei LDAP

Si no tenim instal·lat el paquet `slapd`, el descarregarem i executarem. Pot ser que durant la configuració apareguin alguns errors. En cas que sigui així, podem tornar a reconfigurar el paquet utilitzant la següent comanda:

```bash
dpkg-reconfigure slapd
```
<img width="665" height="116" alt="image" src="https://github.com/user-attachments/assets/f32ef6b9-6270-4a5d-bcb1-228c8ddb5ee1" />
<img width="668" height="389" alt="image" src="https://github.com/user-attachments/assets/de517c92-9454-4866-8ca7-668fb514613b" />

<img width="665" height="384" alt="image" src="https://github.com/user-attachments/assets/da33c36a-d120-4ea7-b579-53ff274658be" />

<img width="665" height="385" alt="image" src="https://github.com/user-attachments/assets/10474052-bb09-4ab8-b34d-2dc668960dbc" />

<img width="668" height="339" alt="image" src="https://github.com/user-attachments/assets/a3e75d17-d584-4e39-acd5-55905c9ef9a4" />


Quan s’executa la reconfiguració, apareix un menú de configuració en què haurem d’introduir diferents valors. És important eliminar la base de dades prèvia per evitar problemes.

Durant aquest procés, establirem una contrasenya i definirem els noms de domini necessaris.

### 3. Configuració de les Unitats Organitzatives, grups i usuaris

Ara definirem les UO, grups i usuaris dins del directori LDAP. És essencial verificar que els noms de domini coincideixin amb els configurats anteriorment per evitar errors.

Els valors han de coincidir amb la configuració prèvia. A continuació, configurarem les UO, grups i usuaris, i aplicarem els canvis al servidor LDAP.

<img width="492" height="130" alt="image" src="https://github.com/user-attachments/assets/abfaa008-e3dd-47a5-bc21-9c17ba9e3d83" />


#### 3.1. Creació de les UO

Editem l’arxiu `ou.ldif` per afegir les unitats organitzatives:

<img width="451" height="107" alt="image" src="https://github.com/user-attachments/assets/1b0851b5-4970-45bd-a5c9-370e7d9504fd" />


#### 3.2. Especificar grups

Especificarem els grups dins de l’arxiu `group.ldif`:

<img width="461" height="145" alt="image" src="https://github.com/user-attachments/assets/edc6b5b3-6933-4b73-a0c3-b792003b9ccb" />


#### 3.3. Afegir usuaris

Afegirem els usuaris al fitxer `usu.ldif`:

<img width="458" height="285" alt="image" src="https://github.com/user-attachments/assets/addc84a4-ce27-4dda-a0fc-7b42d9f19f54" />


Com que aquests fitxers han estat creats manualment, hem d’afegir-los al servidor LDAP amb la següent comanda:

```bash
ldapadd -x -D "cn=admin,dc=example,dc=com" -W -f ou.ldif
ldapadd -x -D "cn=admin,dc=example,dc=com" -W -f group.ldif
ldapadd -x -D "cn=admin,dc=example,dc=com" -W -f usu.ldif
```
<img width="665" height="49" alt="image" src="https://github.com/user-attachments/assets/aa3bf9be-5a3b-49e4-be3c-2f5fe9b1661b" />

<img width="671" height="38" alt="image" src="https://github.com/user-attachments/assets/669c3c3a-952a-45e9-a4df-2ad7de754a2d" />

<img width="664" height="41" alt="image" src="https://github.com/user-attachments/assets/b850cdf2-d790-408a-b849-3be9c55de3d2" />


### 4. Verificació dels canvis

Per comprovar que els canvis s’han aplicat correctament, utilitzarem la comanda `slapcat`:

```bash
slapcat
```
<img width="633" height="621" alt="image" src="https://github.com/user-attachments/assets/fabdef5d-cb11-41f8-9f0f-abf0419cb724" />


Aquest procediment assegura que el domini LDAP estigui configurat correctament, amb les unitats organitzatives, grups i usuaris afegits adequadament.


### [2. Gestió del domini mitjançant comandes]


### Gestió del domini

Per estructurar l'organització i començar a gestionar usuaris, hi ha dues opcions principals: treballar amb fitxers LDIF o utilitzar comandes directament. En aquest apartat, ens centrarem en l'ús de comandes essencials com `search`, `add`, `modify` i `delete`.

Abans de començar, comprovarem que el domini s'ha creat correctament i després revisarem els fitxers preparats a l'escriptori que contenen informació sobre els usuaris.
<img width="543" height="422" alt="image" src="https://github.com/user-attachments/assets/a1cb8a8e-2612-45b8-97d8-b0bb6552e345" />


#### 2.1. ldapadd

Tal com es pot observar, el fitxer inclou diverses dades d'usuaris que volem incorporar al sistema. Ho farem utilitzant la comanda `ldapadd`.

Per registrar els usuaris definits en el fitxer LDIF, executarem la comanda següent:

```bash
ldapadd -x -D "cn=admin,dc=dani-m,dc=cat" -w -f dades.ldif
```
<img width="659" height="238" alt="image" src="https://github.com/user-attachments/assets/454efbed-2e2a-408c-8ada-a7ddad4bd37b" />


#### 2.2. ldapsearch

Un cop els usuaris s'han creat correctament, podem verificar-ne l'existència amb la comanda `ldapsearch`:

```bash
ldapsearch -xLLL -b "dc=dani-m,dc=cat"
```
![3](imatges/sprint3/gestiodominii/3.png)

A més, podem aplicar diferents filtres de cerca per trobar usuaris segons el seu `uid`, `objectClass`, correu electrònic, o qualsevol altra propietat rellevant.

<img width="662" height="212" alt="image" src="https://github.com/user-attachments/assets/110063d9-ba05-4492-920c-71c6bbcba2aa" />

