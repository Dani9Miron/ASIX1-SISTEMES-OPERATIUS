# Monitorització

## LOGS

Els LOGS són una sèrie de registres que emmagatzemen informació de tot el sistema. Són una font de registres de totes les parts del sistema i recopilen tot tipus d'informació que ens pot ser rellevant. Per això, ens interessa monitoritzar-los. Poden haver-hi logs del sistema i logs d'aplicacions.

La majoria d'aquests LOGS es troben al directori `/var/log`. Com podem apreciar, hi ha logs de tot tipus.
<img width="667" height="152" alt="image" src="https://github.com/user-attachments/assets/590098e1-0599-4a82-8c8e-78f43f2c7ce9" />



Un dels aspectes importants dels LOGS és la seva rotació, ja que no ens interessa que estiguin acumulant-se indefinidament. Per això, podem configurar el fitxer `/etc/logrotate.conf` per assignar-los un tipus de rotació, per exemple, setmanalment.

<img width="669" height="289" alt="image" src="https://github.com/user-attachments/assets/e3c5bf57-6f1e-459a-85d3-0d39cc3fa437" />



Dins del directori `/etc/logrotate.d/` podem configurar la rotació de logs en concret.

Per provar com configurar la rotació d'un log en específic, escollirem els logs de `dpkg`. La configuració ens mostra que els arxius rotaran cada mes, es conservaran els últims 12 arxius de logs antics abans d'eliminar-los, els antics es comprimiran, i la compressió es farà després de la rotació. Finalment, es donaran els permisos adequats.

<img width="669" height="288" alt="image" src="https://github.com/user-attachments/assets/475924d3-9a9a-4e6a-852f-344fd65455ba" />


Ara veurem els logs del sistema al fitxer `/etc/rsyslog.d/50-default.conf`. En aquest fitxer podem configurar quins logs es mostren i quins no en el fitxer al qual estan assignats. Després de modificar-lo, s'ha de reiniciar el servei.

<img width="672" height="180" alt="image" src="https://github.com/user-attachments/assets/67bcd9de-c901-4131-900b-55d3a7012ca0" />

<img width="446" height="168" alt="image" src="https://github.com/user-attachments/assets/da3b6680-e508-4212-9cd8-2d990dc8f933" />



Per fer una prova, enviarem una alerta al servei de mail i després farem un `cat` a l'arxiu on es guarden els logs del mail per veure si ha registrat l'alerta.


<img width="669" height="207" alt="image" src="https://github.com/user-attachments/assets/219d2c77-528e-4e68-b447-287d8810a883" />



Ara, el que volem és que TOTES les alertes de nivell crític quedin registrades en una nova carpeta, on podrem analitzar tots els logs d'alerta crítica. Com hem dit abans, si modifiquem aquest arxiu, s'ha de reiniciar el sistema.

<img width="454" height="212" alt="image" src="https://github.com/user-attachments/assets/3ecf409c-3b75-47f7-b149-8b60dcffe343" />


A continuació, per comprovar que els canvis funcionen, crearem una alerta crítica anomenada "Bomba", i després consultarem la carpeta dels logs que hem creat per comprovar si realment apareix.

<img width="659" height="168" alt="image" src="https://github.com/user-attachments/assets/3ceaddd7-17de-4efa-a9d8-eafaacda57ac" />

## Journal

El `journal` consulta el fitxer `systemd journal`, que unifica logs de diferents serveis i components del sistema en un sol lloc. En canvi, el `cat` només ens mostra informació d'un sol fitxer, el que estem consultant.

En aquest cas, farem la consulta:

```bash
journalctl -p crit
```


El `-p` filtra els registres i `crit` selecciona els crítics. El resultat ens mostra errors del RAID, un error d'autenticació (per equivocació amb la contrasenya tres cops).

## Rendiment

Per visualitzar el rendiment podem utilitzar una eina pròpia d'Ubuntu, el monitor del sistema.


# Servidor d'Actualitzacions

Un **servidor d'actualitzacions** és un servidor al qual diversos equips clients estan connectats i agafen els paquets d'actualitzacions d'aquesta màquina servidor. D'aquesta manera, evitem col·lapsar els serveis si molts clients volen descarregar un paquet a la vegada.

Per comprovar el funcionament d'aquesta metodologia utilitzarem l'eina **Apache**.

---

##  Servidor

En aquesta part prepararem la màquina que actuarà com a repositori central.

1. **Instal·lació del servidor:** En primer lloc, instal·larem el paquet `apache2`.
<img width="850" height="225" alt="image" src="https://github.com/user-attachments/assets/22930a1d-d912-4680-bf1c-29cf45e5e349" />

2. **Instal·lació de mirror:** Seguidament, instal·larem el paquet `mirror`, que serà el que ens permetrà copiar qualsevol cosa que tinguem en un directori a un altre, com si fos un mirall.
<img width="712" height="290" alt="image" src="https://github.com/user-attachments/assets/a7e326d6-f7ca-4d2f-994c-af7967f5f29a" />

   
3. **Configuració del repositori:** Al fitxer `/etc/apt/mirror.list` configurarem el paquet d'instal·lació de **Google Chrome**.
<img width="721" height="450" alt="image" src="https://github.com/user-attachments/assets/d5fc1617-6070-41b9-a87b-6304e310f6d7" />


4. **Sincronització:** Un cop tenim aquest fitxer modificat, executarem la comanda `apt-mirror`.

   <img width="805" height="507" alt="image" src="https://github.com/user-attachments/assets/69dc54bd-8e1d-49c6-9ae9-585db84632e1" />

5. **Verificació:** Ens assegurarem que a la carpeta del mirror hi hagi el paquet d'instal·lació del Chrome correctament descarregat.

   <img width="879" height="86" alt="image" src="https://github.com/user-attachments/assets/2622192f-efe8-4294-9275-6ec1612205e3" />




##  Client

Un cop el servidor està llest, configurarem el client per accedir a l'instal·lador del Chrome des del servidor local.

* **Clau GPG:** El primer pas és afegir la clau GPG de Google al sistema. Aquesta clau s'utilitza per verificar la integritat i autenticitat dels paquets descarregats.
<img width="875" height="66" alt="image" src="https://github.com/user-attachments/assets/55ca8a15-af9f-4569-94d5-6ac225b93b0f" />

  
* **Ruta del paquet:** Al fitxer `ubuntu.sources`, afegirem la ruta del paquet del Chrome, però utilitzant la **IP del nostre servidor**.
  <img width="611" height="235" alt="image" src="https://github.com/user-attachments/assets/b8d56e2a-d63c-4711-910c-45c569063323" />

* **Fonts del sistema:** Modificarem l'arxiu `/etc/apt/sources.list.d/ubuntu.sources`. Aquí també li indicarem que els paquets que volem instal·lar tinguin la ruta del nostre servidor per assegurar-nos que els extreu d'allà.
  <img width="587" height="191" alt="image" src="https://github.com/user-attachments/assets/02b29331-94ba-4ec3-adb5-988e3baec09f" />
<img width="594" height="53" alt="image" src="https://github.com/user-attachments/assets/b6e07166-19db-4b64-99ff-8e40ce7ae8a3" />

* **Actualització:** Finalment, llançarem un `update` al client per veure si realment utilitza les rutes que apunten al servidor (ens fixarem si els paquets contenen la IP d'aquest).
 <img width="879" height="462" alt="image" src="https://github.com/user-attachments/assets/eead678e-549d-4369-a6da-31226bd8a4ac" />
 <img width="880" height="269" alt="image" src="https://github.com/user-attachments/assets/0081df72-cc9f-4af0-9295-564400a7fe93" />


###  Resultat Final
Per acabar, verificarem que el client agafa els paquets del servidor i comprovarem que el Chrome s'ha instal·lat correctament.

<img width="801" height="498" alt="image" src="https://github.com/user-attachments/assets/07d8bbd6-e8ae-42bf-b9f8-576bb7ec56d9" />


