# **Què és un Raid i els seus tipus**

Un **raid** és un atac organitzat per un grup de jugadors en un videojoc, generalment en jocs en línia multijugador massius (MMORPG) o jocs de tipus cooperatiu. Normalment, els raids impliquen enfrontaments contra enemics poderosos o caps (*bosses*) i requereixen una estratègia ben coordinada.

## **Tipus de Raids en Videojocs**  
Els raids es poden classificar segons diferents criteris, com ara la mida del grup, la dificultat i el tipus de joc. Alguns dels tipus més comuns són:

### **Segons la mida del grup**  
- **Raids petits:** Normalment entre 3 i 10 jugadors, són més fàcils de gestionar i sovint es troben en jocs com *Destiny* o *World of Warcraft* en la seva modalitat més simple.  
- **Raids grans:** Aquests poden involucrar 20, 40 o més jugadors, com en MMORPGs clàssics (*Final Fantasy XIV*, *Guild Wars 2*). Requereixen una coordinació més complexa.  

### **Segons la dificultat**  
- **Normal:** Apte per a la majoria de jugadors, amb mecàniques accessibles i errors perdonables.  
- **Heroic/Veterà:** Més difícil que el mode normal, amb enemics més forts i mecàniques més exigents.  
- **Mític/Hardcore:** El nivell més alt de dificultat, amb reptes que només poden superar grups molt ben coordinats i amb una bona estratègia.  

### **Segons l'objectiu**  
- **Raids de PVE (*Player vs. Environment*):** Els jugadors lluiten contra enemics controlats pel joc, com en *World of Warcraft* o *Destiny 2*.  
- **Raids de PVP (*Player vs. Player*):** Aquí els jugadors ataquen altres jugadors en grans batalles, com en *Guild Wars 2* o *Elder Scrolls Online*.  
- **Raids de saqueig:** Es fan per aconseguir botí i millorar l’equip dels jugadors, com en *The Division 2*.  

## **Tipus de RAID en Informàtica**  
Els sistemes RAID en informàtica combinen diversos discos durs per millorar el rendiment, la seguretat o ambdues coses. Aquests són els tipus més comuns:

1. **RAID 0 (Striping):** Divideix les dades entre diversos discos per millorar la velocitat, però no ofereix redundància. Si un disc falla, es perden totes les dades.  
2. **RAID 1 (Mirroring):** Guarda una còpia exacta de les dades en dos discos per millorar la seguretat. En cas de fallada d’un disc, les dades continuen disponibles.  
3. **RAID 5 (Striping amb paritat):** Reparteix les dades entre diversos discos i afegeix informació de paritat per recuperar dades en cas de fallada d’un disc. És un bon equilibri entre seguretat i rendiment.  
4. **RAID 6 (Doble paritat):** Similar al RAID 5, però amb una segona capa de paritat, permetent que fallin fins a dos discos sense perdre dades.  
5. **RAID 10 (1+0, Mirroring + Striping):** Combina RAID 1 i RAID 0, proporcionant velocitat i redundància, però requereix almenys 4 discos.  

## **Conclusió**  
Tant en videojocs com en informàtica, els raids són una part fonamental per millorar l'experiència i el rendiment. En els videojocs, ofereixen reptes col·laboratius, mentre que en informàtica ajuden a optimitzar l’emmagatzematge i la seguretat de les dades.






# Configuració de RAID 1

## Instal·lació del paquet necessari

En primer lloc, necessitem el paquet `mdadm`, que ens permet instal·lar i configurar els RAIDs.

<img width="667" height="326" alt="image" src="https://github.com/user-attachments/assets/d4d4f1af-068f-4868-8b20-cfed32afc596" />


## Configuració dels discs

Un cop el paquet està instal·lat, configurarem els discs amb la comanda `fdisk`. Els discs que modifiquem hauran de complir la següent configuració:

<img width="650" height="373" alt="image" src="https://github.com/user-attachments/assets/df652b33-1166-438e-ae44-495aabf89576" />

<img width="663" height="405" alt="image" src="https://github.com/user-attachments/assets/32043429-3cf2-4079-b94b-c50d4bb500cf" />


## Comprovació de les particions

Un cop finalitzada la configuració, consultarem les particions i discos de la nostra màquina i ens assegurarem que el format tingui autodetecció de RAID Linux.
<img width="612" height="351" alt="image" src="https://github.com/user-attachments/assets/fb119791-6efd-432b-8a9f-c7cb2f603dc9" />


## Creació d'una carpeta per fer proves

Crearem una carpeta i li donarem els permisos adequats.

<img width="475" height="155" alt="image" src="https://github.com/user-attachments/assets/5d038548-05d9-4b4e-9169-d9c2f6dfa1ba" />


## Creació del RAID 1

Executem la següent comanda per crear el RAID 1 amb dos dispositius:

```bash
mdadm --create /dev/md0 --level=1 --raid-devices=2 /dev/sdb1 /dev/sdc1
```
!<img width="668" height="217" alt="image" src="https://github.com/user-attachments/assets/1bc806e7-9d7a-416c-b969-ed3d3024626f" />


## Format del RAID

Un cop creat, donarem el format d'arxius a l'array del RAID:

```bash
mkfs.ext4 /dev/md0
```
<img width="644" height="193" alt="image" src="https://github.com/user-attachments/assets/cf4f5e8a-780f-46ff-a1d7-89ea22071e04" />


## Verificació de la configuració

Per comprovar que s'ha creat correctament, utilitzarem:

```bash
mdadm --detail /dev/md0
```
<img width="554" height="440" alt="image" src="https://github.com/user-attachments/assets/1dd2b39b-d5b9-4af3-93ce-7bff8d303043" />


## Creació del fitxer de configuració

```bash
mdadm --detail --scan > /etc/mdadm/mdadm.conf
```

<img width="620" height="41" alt="image" src="https://github.com/user-attachments/assets/70444c94-6b47-4a8c-be28-09306d019d4f" />


Dins del fitxer afegirem la línia següent:

```bash
DEVICE /dev/sdb1 /dev/sdc1
```
<img width="521" height="52" alt="image" src="https://github.com/user-attachments/assets/8254502f-4128-4236-9af8-2bbf2246766c" />


## Configuració del muntatge permanent

Per muntar permanentment el RAID, haurem de configurar el fitxer `fstab`.

Un cop feta la configuració, reiniciarem els serveis i muntarem el disc:

```bash
update-initramfs -u -k all
```

## Comprovació després del reinici

Després de reiniciar el sistema, comprovarem que el RAID està correctament configurat.
<img width="647" height="592" alt="image" src="https://github.com/user-attachments/assets/800e8653-6206-4484-bb88-f503693f55ca" />


## Creació de directoris i fitxers de prova

Crearem diversos directoris i fitxers per verificar el funcionament del RAID.
<img width="534" height="179" alt="image" src="https://github.com/user-attachments/assets/294760d5-75e9-408f-90dc-7558b048c708" />


## Simulació d'error de disc

Per veure com el RAID 1 suporta la fallada d'un disc, podem desmuntar-lo i veure que segueix funcionant:

```bash
mdadm /dev/md0 -f /dev/sdb1
```
<img width="642" height="678" alt="image" src="https://github.com/user-attachments/assets/b963c1df-ae3d-4e9a-9598-11d842a8167f" />


## Eliminació d'un disc

```bash
mdadm /dev/md0 -r /dev/sdb1
```
<img width="638" height="637" alt="image" src="https://github.com/user-attachments/assets/916c41cc-0294-4a2b-9a28-032d00e15fe3" />


Tot i això, encara podrem accedir a les dades.

## Reafegir un disc al RAID

```bash
mdadm /dev/md0 -a /dev/sdb1
```
<img width="667" height="657" alt="image" src="https://github.com/user-attachments/assets/e139652b-07be-4b3e-b676-795f0b42634f" />


Inicialment estarà en estat `spare rebuilding` i, un cop finalitzat, tornarà a estar actiu.

## Substitució d'un disc defectuós

Si un disc es trenca i ha de ser substituït, després de retirar-lo, veurem que només en queda un actiu.

Aturarem els serveis i reiniciarem el RAID:

```bash
systemctl stop mdadm
```

Afegirem el nou disc seguint la configuració inicial. Un cop el RAID es recuperi, tornarà a estar actiu.

## Eliminació del RAID

Per esborrar definitivament el RAID, executem:

```bash
umount /dev/md0
mdadm --stop /dev/md0
mdadm --remove /dev/md0
rm -r /mnt/raid1
```
<img width="584" height="577" alt="image" src="https://github.com/user-attachments/assets/8e7e21d9-9680-4d8a-930c-c47eff13d308" />

<img width="670" height="500" alt="image" src="https://github.com/user-attachments/assets/4938bf87-71d6-40c2-b501-c323402d6c7d" />

<img width="529" height="40" alt="image" src="https://github.com/user-attachments/assets/5b8953bf-6157-4714-8727-b2f108b185a8" />

<img width="663" height="559" alt="image" src="https://github.com/user-attachments/assets/920c49b5-3a93-45fb-bd0d-e63c1501ac9f" />

<img width="667" height="476" alt="image" src="https://github.com/user-attachments/assets/5114d695-4329-4764-a6fc-bace85738207" />

<img width="566" height="146" alt="image" src="https://github.com/user-attachments/assets/e2262df0-bf4f-4224-bdd5-a8c99e5e4889" />

<img width="545" height="50" alt="image" src="https://github.com/user-attachments/assets/e718bd1e-7360-445d-9346-16c2cd2e6a47" />

<img width="668" height="259" alt="image" src="https://github.com/user-attachments/assets/06d05455-bb5c-4d73-8609-6ac5899af814" />

<img width="652" height="142" alt="image" src="https://github.com/user-attachments/assets/05c08304-8379-4051-a87a-206da98fc649" />



A més, hem d'eliminar les línies corresponents de `fstab` i `mdadm.conf`.

Per assegurar que el superblock s'ha eliminat:

```bash
mdadm --zero-superblock /dev/sdb1 /dev/sdc1
systemctl daemon-reload
