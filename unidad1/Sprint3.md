## [ Sprint3]


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
<img width="662" height="212" alt="image" src="https://github.com/user-attachments/assets/110063d9-ba05-4492-920c-71c6bbcba2aa" />

A més, podem aplicar diferents filtres de cerca per trobar usuaris segons el seu `uid`, `objectClass`, correu electrònic, o qualsevol altra propietat rellevant.

<img width="668" height="40" alt="image" src="https://github.com/user-attachments/assets/96838e0d-e590-46a8-a4f1-ed6c0aa74b9c" />



# Servidor Samba

El **Samba** és una implementació lliure del protocol **SMB/CIFS**, que permet compartir arxius i impressores entre sistemes **Windows i Linux**. Samba pot autenticar usuaris **localment** o mitjançant un servidor **LDAP**, cosa que permet gestionar usuaris i permisos de manera centralitzada.

## Característiques de Samba

- **Compartició d'arxius i impressores**: Permet compartir recursos entre diferents sistemes operatius.
- **Autenticació flexible**: Pot utilitzar autenticació local o a través d'un servidor LDAP.
- **Gestió de permisos**: Es poden definir rols i permisos específics per a usuaris i grups.

## Instal·lació i Configuració de Samba
<img width="580" height="26" alt="image" src="https://github.com/user-attachments/assets/826e2eec-b859-4eb9-bcb5-114e30893857" />




### Instal·lació del paquet Samba

En primer lloc, actualitzem el nostre servidor i instal·lem el paquet **samba**:

```bash
apt update && apt install samba
```

### Creació d'una carpeta compartida

Un cop tenim el paquet instal·lat, creem una carpeta a l'arrel i assignem els permisos adients:

```bash
mkdir 
chmod 770 
chown root:colors 
```
<img width="671" height="242" alt="image" src="https://github.com/user-attachments/assets/9ddcde21-a1f5-418a-867f-be52db48e02b" />


### Configuració del fitxer smb.conf

Editem el fitxer de configuració de Samba:

```bash
nano /etc/samba/smb.conf
```

Afegim la configuració per compartir la carpeta i definir permisos:

<img width="657" height="440" alt="image" src="https://github.com/user-attachments/assets/b912ab52-0d23-4862-8693-0eabe50eead1" />


Desem i tanquem el fitxer.

### Creació d'usuaris i grups

Creem el grup **colors**:

```bash
groupadd colors
```

Creem els usuaris amb restricció d'inici de sessió:

```bash
useradd -M -s /sbin/nologin blau
useradd -M -s /sbin/nologin groc
useradd -M -s /sbin/nologin roig
```
<img width="606" height="25" alt="image" src="https://github.com/user-attachments/assets/f54aa90b-2e61-470f-b80c-21e9695a2933" />

<img width="607" height="196" alt="image" src="https://github.com/user-attachments/assets/c0af9cf1-f55c-4aff-a456-3fb554ead491" />


Afegim els usuaris al grup **colors**:

```bash
usermod -aG colors blau
usermod -aG colors groc
```

L'usuari **roig** no el posem al grup per restringir-ne l'accés.

### Assignació de contrasenyes Samba

Per permetre que els usuaris iniciïn sessió en Samba, assignem una contrasenya per a cadascun:

```bash
smbpasswd -a blau
smbpasswd -a groc
smbpasswd -a roig
```
<img width="498" height="261" alt="image" src="https://github.com/user-attachments/assets/d119408a-bedf-46f7-82bb-bb64b051f836" />



### Configuració de permisos

Modifiquem els permisos perquè:

- **Blau** pugui **llegir i escriure**.
- **Verd** només pugui **llegir**.
- **Roig** **no pugui accedir**.


<img width="558" height="327" alt="image" src="https://github.com/user-attachments/assets/97c2be96-4816-4b55-a05f-e27036ec872f" />

Reiniciem el servei Samba:

```bash
systemctl restart smbd
```

## Connexió des del client

### Accés com a convidat

Obrim l'explorador d'arxius i anem a **Altres ubicacions**. Introduïm l'adreça del servidor Samba:

```
smb://IP_DEL_SERVIDOR
```
<img width="656" height="406" alt="image" src="https://github.com/user-attachments/assets/9d55788d-5f16-4206-97b4-7fe07b991bf0" />


Triem l'opció **Convidat** i comprovem si podem accedir.

### Accés com a usuari registrat

Repetim el procés, però aquest cop introduïm les credencials d'un usuari creat (**blau, verd o roig**).

- **Blau** hauria de poder crear i modificar arxius.
- **Groc** només hauria de poder llegir.
- **Roig** hauria de rebre un error d'accés denegat.

### Comprovació de permisos des del servidor

Tornem al servidor i executem:

```bash
ls -l 
```
<img width="442" height="90" alt="image" src="https://github.com/user-attachments/assets/675cfc9d-065a-4ecb-82a2-d4416dd0666b" />

<img width="670" height="406" alt="image" src="https://github.com/user-attachments/assets/3daf5507-4cc7-4404-88d2-025df373c283" />

<img width="525" height="103" alt="image" src="https://github.com/user-attachments/assets/4a2c6b29-8be4-4867-bf01-3b1999c8fda3" />



Això ens permetrà verificar que els permisos s'han aplicat correctament.

## Integració de Samba amb LDAP

En un entorn Samba, els usuaris poden tenir un directori **home** centralitzat que es munta automàticament en qualsevol màquina de la xarxa. Això és possible gràcies a la integració de Samba amb **LDAP** (Lightweight Directory Access Protocol), que facilita la gestió centralitzada de les comptes d'usuari.

## Conclusió

En aquest document hem vist com **instal·lar, configurar i gestionar Samba** en un servidor Linux, definir **usuaris i permisos** i realitzar proves des d'un client per assegurar que tot funciona correctament.








# Unir equips al domini

En aquesta part veurem com connectar un equip client al domini que hem creat prèviament.

## Instal·lació del paquet necessari

El primer pas seria instal·lar el següent paquet al nostre equip client:

```bash
apt install libnss-ldap libpam-ldap nscd
```

Un cop finalitzi la instal·lació del paquet, se'ns obrirà una pestanya de configuració similar a l'anterior que hem vist durant la configuració del servidor. En aquest cas, és important saber la IP de la màquina servidor, ja que serà el primer que configurarem.

## Configuració del domini

Un cop feta aquesta part, seguirem amb la configuració respectant els noms de domini que hem donat prèviament.

Amb aquests passos ja tindrem el paquet configurat. Seguidament, haurem de canviar alguns paràmetres del client, ja que volem que detecti primer el servidor LDAP, i ho farem modificant el fitxer `/etc/nsswitch.conf`.

```bash
sudo nano /etc/nsswitch.conf
```

D'aquesta forma, ens assegurem que els usuaris que hi ha a l'LDAP siguin revisats pel nostre client. Per això, li indiquem els fitxers que ha de revisar, els d'usuari, grups i contrasenyes.

## Configuració de la sessió dels usuaris LDAP

Per configurar la sessió dels usuaris LDAP, també necessitarem modificar el següent fitxer:

```bash
sudo nano /etc/pam.d/common-session
```

Aquesta modificació assegura que, quan un usuari inicia sessió i no té un directori principal, se li crearà automàticament un nou directori principal amb el contingut de `/etc/skel` i amb els permisos especificats per `umask=022`.

## Configuració de la pantalla d'inici de sessió

A continuació, ajustarem com es presenta la pantalla d'inici de sessió als usuaris, especificant la sessió per defecte i permetent l'accés manual amb el nom d'usuari.

Amb aquesta configuració, indiquem que el gestor de pantalla ha de mostrar una opció per permetre als usuaris introduir manualment el seu nom d'usuari en lloc de seleccionar-lo d'una llista. Això pot ser útil en entorns on hi ha molts usuaris o quan es vol permetre l'accés a usuaris que no apareixen a la llista predeterminada.

## Prova d'accés amb un usuari

Seguidament, farem una prova per `alu1`, un usuari inserit i configurat prèviament. Primerament, ens assegurem que aquest aparegui al fitxer `/etc/passwd`.

```bash
grep alu1 /etc/passwd
```

Si `alu1` apareix, reiniciarem el sistema i, a l'hora d'escollir usuari, seleccionarem l'opció de "no apareixeu llistat", llavors indicarem usuari i contrasenya.

Una altra opció és fer-ho des del terminal, canviant d'usuari amb:

```bash
su alu1
```

La qüestió és poder utilitzar l'usuari `alu1` correctament.


