# P2 S5 - Auditoria a Windows Server

## Introducció

En aquest Sprint veurem com configurar una **auditoria** en un entorn **Windows Server** i com actua sobre el client. També realitzarem un **monitoratge** dels esdeveniments generats per l’auditoria.

---

## Auditoria Server

Per fer una auditoria amb Windows, cal configurar-la mitjançant les **GPOs** (polítiques de grup). Anirem a:

`Configuració de Windows > Configuració de seguretat > Directives d’auditoria`

Des d'aquí definirem les polítiques desitjades.

<img width="667" height="414" alt="image" src="https://github.com/user-attachments/assets/7c2573f5-5891-4d72-bdb9-0c4a5578092d" />
 
 

---

## Configuració de polítiques d'auditoria

Podem establir que cada política només es registri en cas d’**error**, d’**èxit**, o ambdues. Comencem amb la de **"accés a objectes"**.

<img width="676" height="464" alt="image" src="https://github.com/user-attachments/assets/852a6872-70e4-4364-b512-dfa8b835f2dd" />



---

## Activació d’opcions addicionals

Per fer un seguiment complet d’accessos i esdeveniments, activem totes les opcions marcades:


<img width="674" height="409" alt="image" src="https://github.com/user-attachments/assets/acbb6995-fcd0-472e-9420-567fbc121907" />

---

## Visor d’esdeveniments (Event Viewer)

A l'apartat **Seguretat** del Visor d'esdeveniments, veurem els esdeveniments generats per la GPO. Per exemple, un procés acabat de manera abrupta amb l'**ID 4688**.

<img width="675" height="478" alt="image" src="https://github.com/user-attachments/assets/12e73b12-7e69-4c39-972d-a67678533041" />


---

## Prova d'inici de sessió des del client

Ara provarem una **connexió d’usuari** des del client. L’usuari  iniciarà sessió, i nosaltres haurem de veure al Visor un registre amb categoria **Logon** i **ID 4624**.



---

## Prova d’eliminació d’un usuari

Eliminem l’usuari **Antoni Banderas** des de l’Active Directory. Al Visor d'esdeveniments, es generarà un esdeveniment amb **ID 4726**.

---
