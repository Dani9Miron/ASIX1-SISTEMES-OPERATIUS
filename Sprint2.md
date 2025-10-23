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
      -Comandes



## 2.Gestio de procesos
## 3.Gestio d'usuaris i grups i permisos
## 4.Copies de seguretat i automatitzacio de tasques
## 5.Quotes d'usuari
