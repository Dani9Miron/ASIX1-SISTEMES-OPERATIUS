# Sprint P2 S3 - Configuració i Administració de Dominis en Entorn Windows

## Introducció

En aquest sprint veurem com configurar i administrar dominis en un entorn Windows, gestionant comptes d'usuari, grups i perfils mòbils. També establirem polítiques de seguretat i control d'accés als recursos tant locals com de xarxa.

---

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
![1](imatges/SPRINT3P2/1.png)  
![2](imatges/SPRINT3P2/2.png)  
![3](imatges/SPRINT3P2/3.png)  
![4](imatges/SPRINT3P2/4.png)


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
![5](imatges/SPRINT3P2/5.png)  
![6](imatges/SPRINT3P2/6.png)  
![7](imatges/SPRINT3P2/7.png)  
![8](imatges/SPRINT3P2/8.png)  
![9](imatges/SPRINT3P2/9.png)  
![10](imatges/SPRINT3P2/10.png)  
![11](imatges/SPRINT3P2/11.png)  
![12](imatges/SPRINT3P2/12.png)  

### Promoció a controlador de domini

1. Escull:
   - Crear un **nou bosc**.
   - Assigna un **nom de domini**.

2. Defineix una **contrasenya per al directori**.

3. Apareixerà un error relacionat amb DNS (esperat), ignora’l.

4. Defineix el **nom NetBIOS** del domini.

5. Revisa tots els passos i genera, si es vol, un script d’instal·lació.

6. Finalitza la instal·lació. El servidor es reiniciarà i podràs iniciar sessió com a **Administrador del domini**.
![13](imatges/SPRINT3P2/13.png)  
![14](imatges/SPRINT3P2/14.png)  
![15](imatges/SPRINT3P2/15.png)  
![16](imatges/SPRINT3P2/16.png)  
![17](imatges/SPRINT3P2/17.png)  
![18](imatges/SPRINT3P2/18.png)  
![19](imatges/SPRINT3P2/19.png)  



## Unió d’equips al domini

1. Configura la xarxa del client:
   - Porta d'enllaç i servidor DNS apuntant al servidor.

2. Verifica la IP amb `ipconfig`.

3. Fes un **ping** entre el client i el servidor (pot ser necessari desactivar el **firewall**).

4. Al client, obre **Configuració avançada del sistema > Nom d’equip** i canvia el grup.

5. Selecciona l’opció **Membre del domini** i escriu el nom del domini.

6. Rebràs un missatge de confirmació i s’haurà de **reiniciar** el client.
![20](imatges/SPRINT3P2/20.png) 
![21](imatges/SPRINT3P2/21.png)  
![22](imatges/SPRINT3P2/22.png)  
![23](imatges/SPRINT3P2/23.png)  
![24](imatges/SPRINT3P2/24.png)  
![25](imatges/SPRINT3P2/25.png)  
![26](imatges/SPRINT3P2/26.png) 

## Gestió d’Usuaris

1. Obre l’eina **Usuarios y equipos de Active Directory**.

2. Navega fins a la carpeta **Usuaris** dins l'arbre del directori.

3. Amb botó dret, crea un nou usuari (ex: *Keanu*).

4. Un cop creat, des del client, a la pantalla d’inici de sessió selecciona **Altres usuaris** i escriu les credencials creades.

![26](imatges/SPRINT3P2/26.png) 
![27](imatges/SPRINT3P2/27.png)  
![28](imatges/SPRINT3P2/28.png)  
![29](imatges/SPRINT3P2/29.png)  
![30](imatges/SPRINT3P2/30.png)
![31](imatges/SPRINT3P2/31.png)   
## Hores d’inici de sessió

Es poden definir horaris en què cada usuari pot iniciar sessió. Aquesta funcionalitat permet controlar que només treballin en horari laboral.

- Es configura des del perfil d’usuari dins de **Active Directory Users and Computers**.
- Si s’intenta iniciar sessió fora d’hores, no es permet l'accés.

![32](imatges/SPRINT3P2/32.png)  
![33](imatges/SPRINT3P2/33.png)  
![34](imatges/SPRINT3P2/34.png) 

## Creació i gestió de grups

1. Des del mateix entorn on creem usuaris, escollim l’opció de crear un **nou grup**.

2. Introduïm les dades del grup i assignem membres.

3. Assignem un **usuari com a administrador del grup** des de la pestanya “Administrado por”.

![35](imatges/SPRINT3P2/35.png)  
![36](imatges/SPRINT3P2/36.png)  
![37](imatges/SPRINT3P2/37.png)  
![38](imatges/SPRINT3P2/38.png)  


## Accés remot a internet (NAT)

Per tal que el client pugui accedir a internet a través del servidor, configurem **Enrutament i accés remot**:

1. A l’Administrador del servidor, afegeix el rol **Accés remot**.

2. Inclou tots els serveis suggerits.

3. Un cop instal·lat, apareixerà un missatge per fer la configuració inicial.

4. A la finestra de configuració:
   - Selecciona **NAT**.
   - Escull l’adaptador que fa servir NAT.

5. Completa la configuració i inicia el servei d’enrutament.



 ![39](imatges/SPRINT3P2/39.png) 
![40](imatges/SPRINT3P2/40.png)  
![41](imatges/SPRINT3P2/41.png)  
![42](imatges/SPRINT3P2/42.png)  
![43](imatges/SPRINT3P2/43.png)  
![44](imatges/SPRINT3P2/44.png)

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
![45](imatges/SPRINT3P2/45.png)
![46](imatges/SPRINT3P2/46.png)
![47](imatges/SPRINT3P2/47.png)
![48](imatges/SPRINT3P2/48.png)

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
![49](imatges/SPRINT3P2/49.png)
![50](imatges/SPRINT3P2/50.png)
![52](imatges/SPRINT3P2/52.png)
![53](imatges/SPRINT3P2/53.png)
![54](imatges/SPRINT3P2/54.png)
![55](imatges/SPRINT3P2/55.png)
![56](imatges/SPRINT3P2/56.png)
![57](imatges/SPRINT3P2/57.png)
![58](imatges/SPRINT3P2/58.png)

## Recomanació

Sempre prova les GPOs en una UO de test abans d'aplicar-les a l'organització sencera per evitar impactes no desitjats.


## Conclusions

Amb aquests passos hem configurat un entorn de domini Windows amb Active Directory, afegint usuaris, grups, limitacions d'accés per hora, i possibilitat d'accés remot a internet per part dels clients. Aquesta pràctica és essencial per entendre la gestió centralitzada d'usuaris i recursos dins d'una xarxa empresarial.



