# P2 S4 - Configuració RAID 5 a Windows Server

## Introducció

En aquest sprint veurem com configurar un sistema de RAID 5 en un sistema **Windows Server**. Comprovarem com es comporten els volums davant d’errades.

---

## RAID 5

### Afegir discs

En primer lloc, afegirem **tres discs de 10 GB** a la nostra màquina virtual.

![1](imatges/SPRINT4P2/1.png)

Un cop afegits, obrim el **Gestor de discs** del sistema operatiu. Se’ns demanarà el format: seleccionem **MBR**.
![2](imatges/SPRINT4P2/2.png)




### Crear volum RAID 5

Veurem que els tres discs de 10 GB estan "sense assignar". Fem clic dret sobre un d’ells i seleccionem **Nou volum RAID-5**.

![3](imatges/SPRINT4P2/3.png)
![4](imatges/SPRINT4P2/4.png)


A la finestra de configuració, escollim els altres dos discs per afegir al RAID i fem clic a **Següent**. Assignem:

- **Lletra d’unitat**
- **Sistema de fitxers (NTFS)**
- **Etiqueta de volum**

Finalment, confirmem la configuració.
![5](imatges/SPRINT4P2/5.png)
![6](imatges/SPRINT4P2/6.png)
![7](imatges/SPRINT4P2/7.png)
![8](imatges/SPRINT4P2/8.png)
![9](imatges/SPRINT4P2/9.png)
![10](imatges/SPRINT4P2/10.png)
![11](imatges/SPRINT4P2/11.png)


### Proves de redundància

Un cop creat el volum, descarreguem **dues imatges** i creem un **fitxer de text** dins d’una carpeta anomenada `prova`.
![12](imatges/SPRINT4P2/12.png)


Ara desactivem un dels discs del RAID: fem clic dret i seleccionem **Sense connexió**. El sistema mostrarà un **error de redundància**, però:
![13](imatges/SPRINT4P2/13.png)
![14](imatges/SPRINT4P2/14.png)
![15](imatges/SPRINT4P2/15.png)

> **Els fitxers encara són accessibles.**



### Fallada de múltiples discs

Desactivem un **segon disc**. Com que RAID 5 requereix almenys **dos discos actius**, ara les dades **deixaran de ser accessibles**.
![16](imatges/SPRINT4P2/16.png)
![17](imatges/SPRINT4P2/17.png)


### Recuperació del sistema

Reactivem els discs amb clic dret → **En línia**. Amb només un disc desactivat, tot i mantenir l'error de redundància, les dades tornen a estar disponibles.

![18](imatges/SPRINT4P2/18.png)
![19](imatges/SPRINT4P2/19.png)
![20](imatges/SPRINT4P2/20.png)
![21](imatges/SPRINT4P2/21.png)

Finalment, activem el **tercer disc**. El sistema sincronitza automàticament el volum i es **restableix la redundància** del RAID.

![22](imatges/SPRINT4P2/22.png)

### Substitució de disc fallat

Si un disc es perd definitivament, afegim un de nou. Però cal tenir en compte:

> **Caldrà recrear el RAID 5 i restaurar la còpia de seguretat.**



![23](imatges/SPRINT4P2/23.png)
![24](imatges/SPRINT4P2/24.png)
![25](imatges/SPRINT4P2/25.png)
![26](imatges/SPRINT4P2/26.png)
![27](imatges/SPRINT4P2/27.png)
![28](imatges/SPRINT4P2/28.png)

## Conclusió

Aquest exercici ens permet entendre el funcionament bàsic de RAID 5, la seva tolerància a errors i la importància de les còpies de seguretat per garantir la recuperació de dades.
