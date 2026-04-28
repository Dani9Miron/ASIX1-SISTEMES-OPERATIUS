
# Sprint 2 - Configuració d’usuaris, permisos i automatitzacions

En aquest segon sprint aprendrem a configurar usuaris i grups, controlar permisos i automatitzar tasques quan els usuaris inicien sessió.


Primer afegirem un disc nou per fer proves. A la pestanya d’emmagatzematge n’afegim un i, un cop arranquem Windows, obrim el gestor de discs. Crearem dues particions: una en format **NTFS** que es dirà **Dades**, i una altra en **FAT32** que es dirà **Portable**.
![1]()  
![2]()  
![3]()  
![4]()  

Per comprovar-les, obrim CMD i fem servir la comanda `diskpart` per llistar els discos i volums i veure si estan ben creats.
![5]() 

Després, anem a l’explorador d’arxius, cliquem amb el botó dret al disc **Dades** i obrim les propietats. A la pestanya “Quota” entrem a la configuració, activem les quotes i limitem l'espai a **300MB** amb un avís a **290MB**. També podem evitar que es passi del límit i activar el registre. Si tot va bé, sortirà una llum verda indicant que està tot correcte.
![6]()  
![7]()  
![8]() 

A continuació, crearem els usuaris. Obrim “cuentas de usuario” i a les opcions avançades entrem a **lusrmgr**, on creem dos usuaris: **alumne1** i **alumne2**. Després anem als grups, creem un que es digui **Limitats** i hi afegim els dos alumnes.
![9]()  
![10]()  
![11]()  
![12]()  
![13]()  
![14]() 
Comprovem que podem iniciar sessió amb ells. Per fer una prova, amb **alumne1** intentem passar-nos de la quota del disc **D**. Ens avisa que ens hem passat, però com que ho vam permetre, ens deixa continuar.
![15]() 

Ara afegim un altre disc de **10GB**, el formategem en **NTFS** i l’anomenem **Backups**. A dins hi creem una carpeta que es digui **CòpiesUsuaris** (millor no posar accents per evitar errors).

Crearem un script `.bat` que copiï les carpetes dels usuaris dins **CòpiesUsuaris**. El fem amb el Bloc de notes i el guardem amb extensió `.bat`. Important: encara que el Windows estigui en castellà o un altre idioma, les rutes han de portar **Users** i no **Usuarios**.
![17]()  
![18]()
![19]()  
![20]()  
![21]()  
![22]()  
![23]()

Provem el script amb l’usuari administrador i veiem que les carpetes es creen bé. Ara volem que el script s’executi cada vegada que un usuari inicia sessió. Obrim **gpedit**, anem a la configuració de Windows -> Scripts -> Inici de sessió, i afegim el script allà.

Iniciem sessió amb els usuaris per comprovar que les còpies es fan. S’obrirà una finestra del terminal (és normal) i quan acabi es tanca sola.

També aprendrem a gestionar processos. Per veure quins estan actius, utilitzem la comanda `tasklist` al CMD. Aquesta ens mostra els processos, amb el seu nom, ID, sessió i memòria usada. Si volem, podem guardar aquesta informació en un fitxer de text amb:

```
tasklist > "C:\ruta\nom_fitxer.txt"
```

Molts processos no són necessaris, com **Skype** o **OneDrive**, i poden ocupar memòria. Els podem tancar amb:

```
taskkill /IM "nomproces" /F
```

Per no fer-ho cada vegada, afegim aquestes comandes al mateix script d’inici de sessió.

Per comprovar-ho, iniciem sessió amb **alumne2** i mirem si OneDrive s'ha tancat. També provem a tancar un procés important com `explorer.exe`, que fa desaparèixer l’escriptori i la barra de tasques. No passa res: podem fer-lo tornar amb:

```
start explorer.exe
```

Ara configurarem permisos. Al disc **Dades** creem una carpeta **Projectes** on treballaran **alumne1** i **alumne2**. Obrim les propietats -> pestanya de seguretat -> opcions avançades. Desactivem l’herència i esborrem tots els permisos que no siguin de l’administrador. Afegim permisos complets per al grup **Limitats**.

Ara els alumnes poden llegir, escriure, modificar i esborrar dins **Projectes**. Si volem que **alumne2** només pugui llegir, fem servir:

```
icacls "D:\Projectes" /grant:r alumne2:(R)
```

Després provem d’escriure, modificar o esborrar i veurem que no pot fer-ho.
