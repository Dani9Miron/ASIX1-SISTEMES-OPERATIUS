# P2 S4 - Configuració RAID 5 a Windows Server

## Introducció

En aquest sprint veurem com configurar un sistema de RAID 5 en un sistema **Windows Server**. Comprovarem com es comporten els volums davant d’errades.

---

## RAID 5

### Afegir discs

En primer lloc, afegirem **tres discs de 10 GB** a la nostra màquina virtual.

<img width="746" height="459" alt="image" src="https://github.com/user-attachments/assets/10ffac1c-ff9a-4665-90c1-167a2fc0bccc" />


Un cop afegits, obrim el **Gestor de discs** del sistema operatiu. Se’ns demanarà el format: seleccionem **MBR**.
<img width="761" height="516" alt="image" src="https://github.com/user-attachments/assets/21031170-c4dd-40ea-af27-89e6f10032ad" />





### Crear volum RAID 5

Veurem que els tres discs de 10 GB estan "sense assignar". Fem clic dret sobre un d’ells i seleccionem **Nou volum RAID-5**.

<img width="754" height="499" alt="image" src="https://github.com/user-attachments/assets/9b9b6e92-8060-473a-8929-7cc27b7bec64" />

<img width="747" height="509" alt="image" src="https://github.com/user-attachments/assets/560c6d49-5e6a-4df2-b59e-eef11991f9f2" />



A la finestra de configuració, escollim els altres dos discs per afegir al RAID i fem clic a **Següent**. Assignem:

- **Lletra d’unitat**
- **Sistema de fitxers (NTFS)**
- **Etiqueta de volum**

Finalment, confirmem la configuració.
<img width="555" height="426" alt="image" src="https://github.com/user-attachments/assets/3735aa4e-e2da-4536-891f-030f995a6361" />

<img width="546" height="434" alt="image" src="https://github.com/user-attachments/assets/b379aa0e-cb51-45e9-b7c9-77dc8ab50817" />
<img width="527" height="410" alt="image" src="https://github.com/user-attachments/assets/c80495f4-637f-4d1d-a723-e6741af2c0dc" />

<img width="547" height="409" alt="image" src="https://github.com/user-attachments/assets/252a757d-68cf-43e8-a25e-7df71ce6093c" />

<img width="531" height="428" alt="image" src="https://github.com/user-attachments/assets/cf2ec4bc-550b-468d-9603-7b3e11c41ff5" />

<img width="726" height="448" alt="image" src="https://github.com/user-attachments/assets/833e6e55-5ff6-4972-a10c-336717982109" />

<img width="754" height="488" alt="image" src="https://github.com/user-attachments/assets/14283d78-f449-4a8c-bb17-b1aeb49c94b4" />



### Proves de redundància

Un cop creat el volum, descarreguem **dues imatges** i creem un **fitxer de text** dins d’una carpeta anomenada `prova`.
![12](imatges/SPRINT4P2/12.png)


Ara desactivem un dels discs del RAID: fem clic dret i seleccionem **Sense connexió**. El sistema mostrarà un **error de redundància**, però:
<img width="755" height="573" alt="image" src="https://github.com/user-attachments/assets/d8fae46d-92da-4351-91fd-626e446ab501" />

<img width="760" height="512" alt="image" src="https://github.com/user-attachments/assets/a2cdddee-9ac7-4ee5-808e-87fc4b5b3c1b" />

<img width="580" height="347" alt="image" src="https://github.com/user-attachments/assets/c8a5695e-7a2b-4e59-bc11-d6a0da94ea7b" />


> **Els fitxers encara són accessibles.**



### Fallada de múltiples discs

Desactivem un **segon disc**. Com que RAID 5 requereix almenys **dos discos actius**, ara les dades **deixaran de ser accessibles**.
<img width="610" height="510" alt="image" src="https://github.com/user-attachments/assets/31aef46c-9423-4ebf-9c5c-1568eb5fceb8" />

<img width="643" height="264" alt="image" src="https://github.com/user-attachments/assets/b7d93db3-ce8b-467b-8c1d-6a7d81c9cd75" />



### Recuperació del sistema

Reactivem els discs amb clic dret → **En línia**. Amb només un disc desactivat, tot i mantenir l'error de redundància, les dades tornen a estar disponibles.

<img width="596" height="535" alt="image" src="https://github.com/user-attachments/assets/6326f378-82af-4b43-90f4-a1d72c51d906" />

<img width="668" height="525" alt="image" src="https://github.com/user-attachments/assets/6f296d0a-9842-4c04-9e4a-97c46106851b" />

<img width="627" height="341" alt="image" src="https://github.com/user-attachments/assets/6b6f82c1-d70f-4ea8-81ec-f26a5b7ce333" />

<img width="757" height="250" alt="image" src="https://github.com/user-attachments/assets/eca22926-7dac-4d7f-816f-a97e3b8a4d21" />


Finalment, activem el **tercer disc**. El sistema sincronitza automàticament el volum i es **restableix la redundància** del RAID.
<img width="740" height="247" alt="image" src="https://github.com/user-attachments/assets/de74dd18-a364-40b0-becc-c01f78667cd3" />


### Substitució de disc fallat

Si un disc es perd definitivament, afegim un de nou. Però cal tenir en compte:

> **Caldrà recrear el RAID 5 i restaurar la còpia de seguretat.**



<img width="750" height="451" alt="image" src="https://github.com/user-attachments/assets/ca9a81ab-c9c2-43cf-b501-42c838b031ef" />

<img width="750" height="444" alt="image" src="https://github.com/user-attachments/assets/0c3d7d46-0e70-4e35-8c88-11f708d4d01b" />

<img width="666" height="88" alt="image" src="https://github.com/user-attachments/assets/32961c91-5e6b-4be1-9e2d-fab5c1836644" />

<img width="758" height="148" alt="image" src="https://github.com/user-attachments/assets/1c9b1c2b-f3bf-4628-8d40-e02df529c4e3" />

<img width="617" height="60" alt="image" src="https://github.com/user-attachments/assets/89d84edd-2e7f-4b2c-a1ec-3fa1c642ba19" />


<img width="751" height="272" alt="image" src="https://github.com/user-attachments/assets/e3430d51-2f8c-44a8-a2ef-f0b712b0a596" />

## Conclusió

Aquest exercici ens permet entendre el funcionament bàsic de RAID 5, la seva tolerància a errors i la importància de les còpies de seguretat per garantir la recuperació de dades.
