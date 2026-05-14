
# Sprint 2 - Configuració d’usuaris, permisos i automatitzacions

En aquest segon sprint aprendrem a configurar usuaris i grups, controlar permisos i automatitzar tasques quan els usuaris inicien sessió.


Primer afegirem un disc nou per fer proves. A la pestanya d’emmagatzematge n’afegim un i, un cop arranquem Windows, obrim el gestor de discs. Crearem dues particions: una en format **NTFS** que es dirà **Dades**, i una altra en **FAT32** que es dirà **Portable**.
<img width="670" height="410" alt="image" src="https://github.com/user-attachments/assets/601afb65-a84d-4ff8-90ad-ddb57ed1a420" />

<img width="493" height="381" alt="image" src="https://github.com/user-attachments/assets/177fc718-ca3f-43c3-9970-57b1bdcf612f" />
<img width="498" height="387" alt="image" src="https://github.com/user-attachments/assets/932dbd6d-c8ca-4217-ba98-a4a32f8803ed" />
 
<img width="643" height="157" alt="image" src="https://github.com/user-attachments/assets/a5661f31-d40b-40ed-95f2-866a9d04af73" />


Per comprovar-les, obrim CMD i fem servir la comanda `diskpart` per llistar els discos i volums i veure si estan ben creats.
<img width="352" height="492" alt="image" src="https://github.com/user-attachments/assets/37c89f48-c41d-4e54-8975-f34c6decbb82" />


Després, anem a l’explorador d’arxius, cliquem amb el botó dret al disc **Dades** i obrim les propietats. A la pestanya “Quota” entrem a la configuració, activem les quotes i limitem l'espai a **300MB** amb un avís a **290MB**. També podem evitar que es passi del límit i activar el registre. Si tot va bé, sortirà una llum verda indicant que està tot correcte.
<img width="358" height="446" alt="image" src="https://github.com/user-attachments/assets/304fa633-3cdb-4cdb-896d-ed74f05c21c9" />
<img width="360" height="441" alt="image" src="https://github.com/user-attachments/assets/30dbf1b7-942f-40b8-9d83-add07cbbfd97" />
 
<img width="456" height="508" alt="image" src="https://github.com/user-attachments/assets/0edd3575-8f1f-47be-bf0f-297b875bb5ef" />


A continuació, crearem els usuaris. Obrim “cuentas de usuario” i a les opcions avançades entrem a **lusrmgr**, on creem dos usuaris: **alumne1** i **alumne2**. Després anem als grups, creem un que es digui **Limitats** i hi afegim els dos alumnes.
<img width="589" height="388" alt="image" src="https://github.com/user-attachments/assets/3de19912-05db-4b50-b6cf-f7667092d1f9" />
<img width="662" height="448" alt="image" src="https://github.com/user-attachments/assets/751d3533-f5bd-4452-a2e7-6c3581816248" />


<img width="585" height="200" alt="image" src="https://github.com/user-attachments/assets/6914de7f-0489-492d-8a41-448e4c788c60" />

 <img width="603" height="426" alt="image" src="https://github.com/user-attachments/assets/f8e26b37-ef42-40dd-8079-e08efdeb0944" />

<img width="412" height="391" alt="image" src="https://github.com/user-attachments/assets/cfe28592-cf90-471f-ac23-ba980d7b7709" />

<img width="549" height="388" alt="image" src="https://github.com/user-attachments/assets/319e3c6b-6c80-4ddc-b862-d32927d6e8f9" />


Comprovem que podem iniciar sessió amb ells. Per fer una prova, amb **alumne1** intentem passar-nos de la quota del disc **D**. Ens avisa que ens hem passat, però com que ho vam permetre, ens deixa continuar.
<img width="249" height="414" alt="image" src="https://github.com/user-attachments/assets/17094d85-ee4a-4c01-b818-b6235fbac613" />


Ara afegim un altre disc de **10GB**, el formategem en **NTFS** i l’anomenem **Backups**. A dins hi creem una carpeta que es digui **CòpiesUsuaris** (millor no posar accents per evitar errors).

Crearem un script `.bat` que copiï les carpetes dels usuaris dins **CòpiesUsuaris**. El fem amb el Bloc de notes i el guardem amb extensió `.bat`. Important: encara que el Windows estigui en castellà o un altre idioma, les rutes han de portar **Users** i no **Usuarios**.
<img width="664" height="408" alt="image" src="https://github.com/user-attachments/assets/d0d5f3ee-3f8f-4f67-bee8-086ed317db8b" />

<img width="489" height="394" alt="image" src="https://github.com/user-attachments/assets/8ad3248c-bb7b-4bc4-9168-393637c5390e" />

<img width="359" height="332" alt="image" src="https://github.com/user-attachments/assets/492677f6-e8c4-4f55-9c4a-a29bc5fd2819" />

<img width="352" height="326" alt="image" src="https://github.com/user-attachments/assets/99f39c7d-9f2c-4680-ad2a-f3962c7657ef" />

<img width="373" height="267" alt="image" src="https://github.com/user-attachments/assets/84fdb010-cd49-4165-a982-c0bd9d012545" />
 
<img width="605" height="464" alt="image" src="https://github.com/user-attachments/assets/bbae08a3-3f5c-4022-ba23-5e48f6bd70f7" />

<img width="348" height="147" alt="image" src="https://github.com/user-attachments/assets/b91682a2-26f1-4542-9ab7-804ac32276b2" />


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
