# Sprint2

## Sistemes de fitxers i particions
  -Mida sector
  -Mida block
  <img width="467" height="128" alt="image" src="https://github.com/user-attachments/assets/e8b4dc6f-3c91-49f5-b0f5-0d753ce76238" />
  <img width="579" height="76" alt="image" src="https://github.com/user-attachments/assets/0cac94a6-1062-45b0-8c5b-45d003bdc0fa" />

  -Fragmentacio interna
    La fragmentació interna és l’espai que desaprofitem dels blocs perquè no s’acaben d’emplenar. Una solució possible és canviar la mida del block reduïm la fragmentació interna, però pots fragmentar un arxiu (baixes el rendiment), busquem un equilibri. Aquesta canvi de mida per reduir l'espai del bloc ens pot servir si emmagatzemem arxius que no tinguin una mida molt gran, com podiren ser els fitxers de text. D'altra banda si volem guardar fitxers mes grans com podrien ser pel·licules o ISOs em de fer més gran la mida del bloc perqué sino fragmentarem molt els arxius. RECOMANACIÓ! buscar sempre un equilibri i emmagatzemar els tipus d'arxius diferents en particions diferents, per no barrejar "pelis amb textos".
 
  
  -Fragmentacio externa
    La fragmentació externa és quan el disc fa temps que treballa i els arxius es guarden en blocs separats i no continus, això ens fa baixar el rendiment, aquesta baixada de rendiment es pot solucionar desfragmentant el disc. La desfragmentació intenta ordenar els arxius per a que no estiguin .

<img width="1190" height="341" alt="image" src="https://github.com/user-attachments/assets/13d80321-3378-4ff8-878c-e5a7a008f027" />
<img width="442" height="59" alt="image" src="https://github.com/user-attachments/assets/7c70df6d-a502-4490-bc72-cb956a7b560d" />

  
  -Tipus formateig
      Hi ha tres maneres de formatar un disc i son les següents:

  Ràpid: Aquest formateig no borra els arxius, elimina el sistema de fitxers i en cas d'haver-hi un bloc defectuos s'ignora.

  Nivell mig: Aquest tampoc elimina els arxius sinó que elimina el sistema de fitxers igual que ho fa el ràpid, la diferencia es que el mig detecta i marca els sectors i/o blocs defectuosos, sense reperar-los.

  Nivell baix: En aquest igual necessitem algún programa extern. I en aquest cas si es borren els arxius, es borra tot i intenta reparar els blocs defectuosos. És el més lent dels tres. Amb commandes també tal i com es mostra a continuació. Hi ha una command per mostar la cantitat de fragmentació que tenim a la partició en concret (ens recomana si em de desfragmentar o no), i després una altra per desfragmentar-lo.

e4defrag -c /dev/sda2 (consulta)

e4defrag /dev/sda2 (desfragmentació)

  -Gestio Particions
      -Gparted
      <img width="777" height="533" alt="image" src="https://github.com/user-attachments/assets/bf11066c-4c38-42f7-aaca-b689f2a4e981" />
     
  -Comandes
<img width="833" height="384" alt="image" src="https://github.com/user-attachments/assets/15002eca-dcdd-44db-8b11-77aaea4aeeb5" />
<img width="785" height="318" alt="image" src="https://github.com/user-attachments/assets/c0147d32-b5f8-465d-a37d-4bc1089332c2" />
<img width="581" height="216" alt="image" src="https://github.com/user-attachments/assets/849f504a-3e55-4f77-bf57-879fd5005709" />
<img width="829" height="233" alt="image" src="https://github.com/user-attachments/assets/d891bbd3-932f-4364-9ba4-ceb92e29f16b" />
<img width="597" height="79" alt="image" src="https://github.com/user-attachments/assets/5ab8bd4e-17e1-4f27-af2c-03297075113c" />
<img width="729" height="131" alt="image" src="https://github.com/user-attachments/assets/c5019674-8729-405d-9369-666a57570734" />
<img width="941" height="534" alt="image" src="https://github.com/user-attachments/assets/e75b96e0-43e5-4275-a56a-758c3ed64cc4" />



## 2.Gestio de procesos
## 3.Gestio d'usuaris i grups i permisos
  -Fitxers importants
  <img width="1209" height="760" alt="image" src="https://github.com/user-attachments/assets/025e457b-20b8-48cb-9be7-cb04a5d04c3f" />
  <img width="1206" height="769" alt="image" src="https://github.com/user-attachments/assets/7b37c045-8d4d-4434-84c1-0a7640f3ff62" />
  <img width="1206" height="759" alt="image" src="https://github.com/user-attachments/assets/4bb9174a-6b31-4042-95ae-950b4c7c1267" />
  <img width="1208" height="758" alt="image" src="https://github.com/user-attachments/assets/caceb980-2d89-41ee-92a6-e7388b9d72b5" />
  <img width="679" height="434" alt="image" src="https://github.com/user-attachments/assets/d2bad246-4d58-4b86-8c60-96e31576203e" />

  -Comandes bàsiques
  <img width="743" height="464" alt="image" src="https://github.com/user-attachments/assets/e03d0aa5-7ba0-4a03-a45b-38506e895904" />
  <img width="1012" height="226" alt="image" src="https://github.com/user-attachments/assets/ae7c31cb-5182-4da6-9fce-cc2dc763465f" />
  <img width="693" height="89" alt="image" src="https://github.com/user-attachments/assets/ba3b0588-1eae-4796-9572-f365a09b9e61" />
  <img width="640" height="222" alt="image" src="https://github.com/user-attachments/assets/d1741c67-5d23-4769-ada5-28cec1a41c7f" />
<img width="640" height="222" alt="image" src="https://github.com/user-attachments/assets/4f7f807d-0ca3-4cb7-8b67-bd64d0f0f6e2" />
  <img width="724" height="354" alt="image" src="https://github.com/user-attachments/assets/d417a0ae-f085-425c-9a47-a6c3fee7ef4d" />
  <img width="646" height="112" alt="image" src="https://github.com/user-attachments/assets/e57de532-216e-42b0-baa3-7c0da537866c" />
  <img width="1015" height="116" alt="image" src="https://github.com/user-attachments/assets/bc7db0ac-ff4f-4986-93e1-fc5e3b8df3a3" />
  <img width="999" height="66" alt="image" src="https://github.com/user-attachments/assets/2703e7c8-4336-4df5-8ad5-5c5fd25fb75f" />
  <img width="602" height="222" alt="image" src="https://github.com/user-attachments/assets/8705665e-5b00-4e59-9ac5-c712de16b755" />
  <img width="672" height="592" alt="image" src="https://github.com/user-attachments/assets/d3c3249e-c45c-4c36-b98d-dd8483c17705" />

  -Directoris i fitxers importants
  -Gestió avançada
  -PAM
  quines comande se de utilizar quan vull cambiar un nom de usuari correctament
## 4.Copies de seguretat i automatitzacio de tasques
## 5.Quotes d'usuari

## Mascara
  -umask és la màscara que defineix els permisos per defecte en fitxers i directoris nous. Resta permisos dels valors base (666 per fitxers, 777 per directoris) per controlar seguretat i accessibilitat.
   <img width="359" height="55" alt="image" src="https://github.com/user-attachments/assets/4cb7b334-5908-4af6-86a4-4aa9daaa8411" />
Explicacio de la captura
<img width="737" height="132" alt="image" src="https://github.com/user-attachments/assets/2b2df245-1f34-4fae-bf6c-2ef1eef19511" />
Aquí tens una explicació en dues línies de la captura:

**ERASECHAR** (`0177`) i **KILLCHAR** (`025`) defineixen tecles de control del terminal per esborrar caràcters o línies.  
**UMASK** (`022`) estableix els permisos per defecte: fitxers amb `644` i directoris amb `755`.

.profile
<img width="1204" height="675" alt="image" src="https://github.com/user-attachments/assets/0d828fea-cd14-44c8-9979-6ccc38e790a3" />
umask temporal
<img width="350" height="112" alt="image" src="https://github.com/user-attachments/assets/dbeafcc7-1218-419f-9b9f-588679c3130d" />
<img width="392" height="52" alt="image" src="https://github.com/user-attachments/assets/eb7adeca-a936-4906-959b-999a3d53c0f3" />
<img width="606" height="70" alt="image" src="https://github.com/user-attachments/assets/5f6dce85-e6d6-48c1-8d44-cca869a9b8bd" />


<img width="514" height="25" alt="image" src="https://github.com/user-attachments/assets/b8cf39f0-4a9e-46eb-868e-11748b959a80" />
<img width="698" height="125" alt="image" src="https://github.com/user-attachments/assets/e5dedcd1-d695-4bad-a1c0-f4a269db98cc" />
<img width="525" height="245" alt="image" src="https://github.com/user-attachments/assets/329e1fff-b8e9-4f48-946c-cd1fb3e17ce1" />



## ACL

<img width="410" height="160" alt="image" src="https://github.com/user-attachments/assets/0416eb44-361a-496e-b71f-814ab1819ad1" />

<img width="547" height="226" alt="image" src="https://github.com/user-attachments/assets/f2e33366-0835-4384-8483-c3fad4de4e4e" />

<img width="903" height="359" alt="image" src="https://github.com/user-attachments/assets/5f9cfdb8-facd-40b8-99ad-946f5b32b0bb" />

<img width="413" height="190" alt="image" src="https://github.com/user-attachments/assets/00893ae2-2d98-4290-9081-e6c7b3790b03" />




