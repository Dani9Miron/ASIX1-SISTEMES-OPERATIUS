# Introducció

En aquest projecte veurem la funcionalitat del sistema operatiu Windows, el seu tipus de llicències i també identificarem els seus elements funcionals. Realitzarem la seva instal·lació i configuració, i mostrarem com configurar els serveis de xarxa i els seus protocols mitjançant màquines virtuals.

---

## Instal·lació Windows Server

Per instal·lar un Windows Server en una màquina virtual, el primer que necessitarem serà una ISO del sistema operatiu. Després començarem amb una instal·lació creant una màquina nova amb VirtualBox.
<img width="662" height="360" alt="image" src="https://github.com/user-attachments/assets/863a93f1-c888-4960-8fe5-c8e408cac59d" />

 

Els primers passos després d'afegir la ISO del sistema són donar les capacitats de la màquina de VirtualBox: memòria RAM, nombre de nuclis que utilitzarà el processador i la memòria física que tindrà la nostra màquina.
<img width="672" height="352" alt="image" src="https://github.com/user-attachments/assets/2eac3c1e-8748-49da-8cf7-e6ff8dd2a92f" />


<img width="667" height="358" alt="image" src="https://github.com/user-attachments/assets/a9907a4b-be68-4ab7-8d79-5056bed1f760" />


Un cop confirmada la configuració, arrenquem la màquina i comencem la instal·lació del sistema, seguint els passos que es mostren.
<img width="675" height="352" alt="image" src="https://github.com/user-attachments/assets/e3660e3a-a7bf-4a27-a602-b2a7bf4d3089" />

<img width="667" height="413" alt="image" src="https://github.com/user-attachments/assets/691f0556-47d1-4b3a-96d9-8a17566ebb46" />

En aquest punt ens demanarà quina versió del sistema volem instal·lar. Escollirem la que ens facilita una interfície gràfica i després acceptarem els termes de la llicència.
<img width="657" height="538" alt="image" src="https://github.com/user-attachments/assets/4c420da9-be60-40fd-a85f-430702935933" />
 
<img width="675" height="556" alt="image" src="https://github.com/user-attachments/assets/842b7933-25ef-4df2-85b4-fd86a0e82572" />

Seguidament escollirem el tipus d'instal·lació personalitzada, per escollir les mides del disc de forma manual (en aquest cas, que el sistema ocupi el 100% del disc).
<img width="672" height="552" alt="image" src="https://github.com/user-attachments/assets/d895a2be-05ac-4011-b650-0aca4d0797d0" />
 
<img width="657" height="531" alt="image" src="https://github.com/user-attachments/assets/c2c65aa9-01ae-43e9-b01e-3b2a499bd0b0" />

Finalment veurem que ja se'ns comença a instal·lar i simplement hem d'esperar.
<img width="666" height="548" alt="image" src="https://github.com/user-attachments/assets/e42a43ff-c00b-45e4-9620-061ef40d4b51" />

Un cop acabat esborrem la imatge ISO de la instal·lació i arrenquem la màquina de nou. A continuació haurem de configurar l'usuari administrador.

<img width="669" height="552" alt="image" src="https://github.com/user-attachments/assets/908e0042-e751-464f-acc4-8d2c092284a8" />

<img width="670" height="550" alt="image" src="https://github.com/user-attachments/assets/4ea858bd-a7da-475c-90fb-6a9347291e5c" />


### Configuració IP estàtica

En aquest punt configurarem una IP estàtica, ja que ens interessa que el servidor sempre tingui la mateixa IP. Els passos a seguir són els següents:

1. Entrar a la configuració de xarxa.
2. Ethernet → opcions de l'adaptador.
3. Propietats de l'adaptador → funcions de xarxa.
4. Escollir IPv4.
5. Assignar IP, màscara i porta d'enllaç.

<img width="673" height="588" alt="image" src="https://github.com/user-attachments/assets/b21c3752-b647-4e8e-a444-61d95bd5df24" />
 
<img width="671" height="543" alt="image" src="https://github.com/user-attachments/assets/69112583-5367-4365-b977-d2479ba0ec47" />

<img width="669" height="497" alt="image" src="https://github.com/user-attachments/assets/a5efaca4-c58d-49f8-82c4-7cf08b90d074" />

<img width="362" height="466" alt="image" src="https://github.com/user-attachments/assets/d58428e4-6d66-4123-9185-65a751ab6cd1" />
 
<img width="405" height="449" alt="image" src="https://github.com/user-attachments/assets/dd27d78b-87f6-47cc-9e4b-23280272db8c" />
 
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
