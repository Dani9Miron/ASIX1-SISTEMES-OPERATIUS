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

![1](/sprint4/1.png)

## Configuració dels discs

Un cop el paquet està instal·lat, configurarem els discs amb la comanda `fdisk`. Els discs que modifiquem hauran de complir la següent configuració:

![2](/sprint4/2.png)
![3](/sprint4/3.png)

## Comprovació de les particions

Un cop finalitzada la configuració, consultarem les particions i discos de la nostra màquina i ens assegurarem que el format tingui autodetecció de RAID Linux.
![4](/sprint4/4.png)

## Creació d'una carpeta per fer proves

Crearem una carpeta i li donarem els permisos adequats.

![5](/sprint4/5.png)

## Creació del RAID 1

Executem la següent comanda per crear el RAID 1 amb dos dispositius:

```bash
mdadm --create /dev/md0 --level=1 --raid-devices=2 /dev/sdb1 /dev/sdc1
```
![6](/sprint4/6.png)

## Format del RAID

Un cop creat, donarem el format d'arxius a l'array del RAID:

```bash
mkfs.ext4 /dev/md0
```
![7](/sprint4/7.png)

## Verificació de la configuració

Per comprovar que s'ha creat correctament, utilitzarem:

```bash
mdadm --detail /dev/md0
```
![8](/sprint4/8.png)

## Creació del fitxer de configuració

```bash
mdadm --detail --scan > /etc/mdadm/mdadm.conf
```

![10](/sprint4/10.png)

Dins del fitxer afegirem la línia següent:

```bash
DEVICE /dev/sdb1 /dev/sdc1
```
![9](/sprint4/9.png)

## Configuració del muntatge permanent

Per muntar permanentment el RAID, haurem de configurar el fitxer `fstab`.

Un cop feta la configuració, reiniciarem els serveis i muntarem el disc:

```bash
update-initramfs -u -k all
```

## Comprovació després del reinici

Després de reiniciar el sistema, comprovarem que el RAID està correctament configurat.

## Creació de directoris i fitxers de prova

Crearem diversos directoris i fitxers per verificar el funcionament del RAID.

## Simulació d'error de disc

Per veure com el RAID 1 suporta la fallada d'un disc, podem desmuntar-lo i veure que segueix funcionant:

```bash
mdadm /dev/md0 -f /dev/sdb1
```
![14](/sprint4/14.png)

## Eliminació d'un disc

```bash
mdadm /dev/md0 -r /dev/sdb1
```
![15](/sprint4/15.png)

Tot i això, encara podrem accedir a les dades.

## Reafegir un disc al RAID

```bash
mdadm /dev/md0 -a /dev/sdb1
```
![16](/sprint4/16.png)

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
![17](/sprint4/17.png)
![18](/sprint4/18.png)
![19](/sprint4/19.png)
![20](/sprint4/20.png)
![21](/sprint4/21.png)
![22](/sprint4/22.png)
![23](/sprint4/23.png)
![24](/sprint4/24.png)
![25](/sprint4/25.png)


A més, hem d'eliminar les línies corresponents de `fstab` i `mdadm.conf`.

Per assegurar que el superblock s'ha eliminat:

```bash
mdadm --zero-superblock /dev/sdb1 /dev/sdc1
systemctl daemon-reload
