# P2 S5 - Auditoria a Windows Server

## Introducció

En aquest Sprint veurem com configurar una **auditoria** en un entorn **Windows Server** i com actua sobre el client. També realitzarem un **monitoratge** dels esdeveniments generats per l’auditoria.

---

## Auditoria Server

Per fer una auditoria amb Windows, cal configurar-la mitjançant les **GPOs** (polítiques de grup). Anirem a:

`Configuració de Windows > Configuració de seguretat > Directives d’auditoria`

Des d'aquí definirem les polítiques desitjades.

![1](imatges/SPRINT5P2/1.png)  
 

---

## Configuració de polítiques d'auditoria

Podem establir que cada política només es registri en cas d’**error**, d’**èxit**, o ambdues. Comencem amb la de **"accés a objectes"**.

![2](imatges/SPRINT5P2/2.png)  


---

## Activació d’opcions addicionals

Per fer un seguiment complet d’accessos i esdeveniments, activem totes les opcions marcades:


![3](imatges/SPRINT5P2/3.png)  

---

## Visor d’esdeveniments (Event Viewer)

A l'apartat **Seguretat** del Visor d'esdeveniments, veurem els esdeveniments generats per la GPO. Per exemple, un procés acabat de manera abrupta amb l'**ID 4688**.

![4](imatges/SPRINT5P2/4.png) 

---

## Prova d'inici de sessió des del client

Ara provarem una **connexió d’usuari** des del client. L’usuari  iniciarà sessió, i nosaltres haurem de veure al Visor un registre amb categoria **Logon** i **ID 4624**.



---

## Prova d’eliminació d’un usuari

Eliminem l’usuari **Antoni Banderas** des de l’Active Directory. Al Visor d'esdeveniments, es generarà un esdeveniment amb **ID 4726**.

---
