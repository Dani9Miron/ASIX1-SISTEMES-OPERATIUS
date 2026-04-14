# Introducció

En aquest projecte veurem la funcionalitat del sistema operatiu Windows, el seu tipus de llicències i també identificarem els seus elements funcionals. Realitzarem la seva instal·lació i configuració, i mostrarem com configurar els serveis de xarxa i els seus protocols mitjançant màquines virtuals.

---

## Instal·lació Windows Server

Per instal·lar un Windows Server en una màquina virtual, el primer que necessitarem serà una ISO del sistema operatiu. Després començarem amb una instal·lació creant una màquina nova amb VirtualBox.
![1](imatges/SPRINT1P2/W1.png)  

Els primers passos després d'afegir la ISO del sistema són donar les capacitats de la màquina de VirtualBox: memòria RAM, nombre de nuclis que utilitzarà el processador i la memòria física que tindrà la nostra màquina.
![2](imatges/SPRINT1P2/W2.png)  
![3](imatges/SPRINT1P2/W3.png) 
Un cop confirmada la configuració, arrenquem la màquina i comencem la instal·lació del sistema, seguint els passos que es mostren.
![4](imatges/SPRINT1P2/W4.png)  
![5](imatges/SPRINT1P2/W5.png) 
En aquest punt ens demanarà quina versió del sistema volem instal·lar. Escollirem la que ens facilita una interfície gràfica i després acceptarem els termes de la llicència.
![6](imatges/SPRINT1P2/W6.png)  
![7](imatges/SPRINT1P2/W7.png)
Seguidament escollirem el tipus d'instal·lació personalitzada, per escollir les mides del disc de forma manual (en aquest cas, que el sistema ocupi el 100% del disc).
![8](imatges/SPRINT1P2/W8.png)  
![9](imatges/SPRINT1P2/W9.png)  
Finalment veurem que ja se'ns comença a instal·lar i simplement hem d'esperar.
![10](imatges/SPRINT1P2/W10.png) 
Un cop acabat esborrem la imatge ISO de la instal·lació i arrenquem la màquina de nou. A continuació haurem de configurar l'usuari administrador.

![11](imatges/SPRINT1P2/W11.png)  
![12](imatges/SPRINT1P2/W12.png) 

### Configuració IP estàtica

En aquest punt configurarem una IP estàtica, ja que ens interessa que el servidor sempre tingui la mateixa IP. Els passos a seguir són els següents:

1. Entrar a la configuració de xarxa.
2. Ethernet → opcions de l'adaptador.
3. Propietats de l'adaptador → funcions de xarxa.
4. Escollir IPv4.
5. Assignar IP, màscara i porta d'enllaç.

![13](imatges/SPRINT1P2/W13.png)  
![14](imatges/SPRINT1P2/W14.png)  
[!15](imatges/SPRINT1P2/W15.png)  
![16](imatges/SPRINT1P2/W16.png)  
![17](imatges/SPRINT1P2/W17.png)  
![18](imatges/SPRINT1P2/W18.png) 
Un cop tot configurat, des del terminal (CMD) comprovem que la IP sigui la configurada amb la comanda `ipconfig`.
![19](imatges/SPRINT1P2/W19.png)

## Instal·lació Windows 10

Com hem fet a l'apartat anterior, seleccionarem la imatge ISO del sistema operatiu Windows 10. Un cop fet això, donarem els paràmetres de la màquina virtual: RAM, espai i nuclis.
![1](imatges/SPRINT1P2/1.png)  
![2](imatges/SPRINT1P2/2.png)  
![3](imatges/SPRINT1P2/3.png)  
 
Un cop tenim feta la configuració de la màquina, l'arrenquem i s'iniciarà l'instal·lador de Windows. Seguirem els passos que hem vist en l'apartat anterior, ja que la instal·lació és molt similar.
![4](imatges/SPRINT1P2/4.png)  
![5](imatges/SPRINT1P2/5.png)  
![6](imatges/SPRINT1P2/6.png)  
![7](imatges/SPRINT1P2/7.png)  
![8](imatges/SPRINT1P2/8.png)  
![9](imatges/SPRINT1P2/9.png)

Un cop acabada la instal·lació esborrarem la imatge ISO d'instal·lació. I arrenquem la màquina de nou. Ara ens demanarà configurar l'usuari i una sèrie de funcionalitats de Windows. Aquestes es poden escollir al nostre gust — en aquest cas s’han rebutjat totes.
![10](imatges/SPRINT1P2/10.png)  
![11](imatges/SPRINT1P2/11.png)  
![12](imatges/SPRINT1P2/12.png)  
