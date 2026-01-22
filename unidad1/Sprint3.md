## [Index Sprint3](Sprint3.md)
### [1.Instal·lació domini LDAP]( ldap.md )

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
![6](imatges/sprint3/ldap/6.png)
![7](imatges/sprint3/ldap/7.png)
![8](imatges/sprint3/ldap/8.png)
![9](imatges/sprint3/ldap/9.png)
![10](imatges/sprint3/ldap/10.png)

Quan s’executa la reconfiguració, apareix un menú de configuració en què haurem d’introduir diferents valors. És important eliminar la base de dades prèvia per evitar problemes.

Durant aquest procés, establirem una contrasenya i definirem els noms de domini necessaris.

### 3. Configuració de les Unitats Organitzatives, grups i usuaris

Ara definirem les UO, grups i usuaris dins del directori LDAP. És essencial verificar que els noms de domini coincideixin amb els configurats anteriorment per evitar errors.

Els valors han de coincidir amb la configuració prèvia. A continuació, configurarem les UO, grups i usuaris, i aplicarem els canvis al servidor LDAP.

![11](imatges/sprint3/ldap/11.png)

#### 3.1. Creació de les UO

Editem l’arxiu `ou.ldif` per afegir les unitats organitzatives:

![11](imatges/sprint3/ldap/11.png)

#### 3.2. Especificar grups

Especificarem els grups dins de l’arxiu `group.ldif`:

![12](imatges/sprint3/ldap/12.png)

#### 3.3. Afegir usuaris

Afegirem els usuaris al fitxer `usu.ldif`:

![13](imatges/sprint3/ldap/13.png)

Com que aquests fitxers han estat creats manualment, hem d’afegir-los al servidor LDAP amb la següent comanda:

```bash
ldapadd -x -D "cn=admin,dc=example,dc=com" -W -f ou.ldif
ldapadd -x -D "cn=admin,dc=example,dc=com" -W -f group.ldif
ldapadd -x -D "cn=admin,dc=example,dc=com" -W -f usu.ldif
```
![14](imatges/sprint3/ldap/14.png)
![15](imatges/sprint3/ldap/15.png)
![16](imatges/sprint3/ldap/16.png)

### 4. Verificació dels canvis

Per comprovar que els canvis s’han aplicat correctament, utilitzarem la comanda `slapcat`:

```bash
slapcat
```
![17](imatges/sprint3/ldap/17.png)

Aquest procediment assegura que el domini LDAP estigui configurat correctament, amb les unitats organitzatives, grups i usuaris afegits adequadament.


### [2. Gestió del domini mitjançant comandes]( gestiodomini.md )


### Gestió del domini

Per estructurar l'organització i començar a gestionar usuaris, hi ha dues opcions principals: treballar amb fitxers LDIF o utilitzar comandes directament. En aquest apartat, ens centrarem en l'ús de comandes essencials com `search`, `add`, `modify` i `delete`.

Abans de començar, comprovarem que el domini s'ha creat correctament i després revisarem els fitxers preparats a l'escriptori que contenen informació sobre els usuaris.
![1](imatges/sprint3/gestiodominii/1.png)

#### 2.1. ldapadd

Tal com es pot observar, el fitxer inclou diverses dades d'usuaris que volem incorporar al sistema. Ho farem utilitzant la comanda `ldapadd`.

Per registrar els usuaris definits en el fitxer LDIF, executarem la comanda següent:

```bash
ldapadd -x -D "cn=admin,dc=dani-m,dc=cat" -w -f dades.ldif
```
![2](imatges/sprint3/gestiodominii/2.png)

#### 2.2. ldapsearch

Un cop els usuaris s'han creat correctament, podem verificar-ne l'existència amb la comanda `ldapsearch`:

```bash
ldapsearch -xLLL -b "dc=dani-m,dc=cat"
```
![3](imatges/sprint3/gestiodominii/3.png)

A més, podem aplicar diferents filtres de cerca per trobar usuaris segons el seu `uid`, `objectClass`, correu electrònic, o qualsevol altra propietat rellevant.

![4](imatges/sprint3/gestiodominii/4.png)
