# Esercizio Guidato GIT
In questo esercizio guidato, vedremo come:

 - Creare una repository locale
 - Eseguire dei commit
 - Creare dei Branch
 - Eseguire il merge tra branch
 - Eseguire il push in una repository remota
---
### Creare una repository locale
Per creare una repository, è necessario, prima di tutto, installare [GIT](https://git-scm.com/downloads)
Una volta installato, aprire il terminale del proprio sistema operativo, *per windows consigliamo GIT Bash* e spostarsi sulla cartella sulla quale vogliamo creare una repository, attraverso il comando `cd percorso_verso_la_directory`.
*N.B: evita di utilizzare cartelle di sistema o la propria cartella utente, scegli invece una cartella creata da te.*

Per inizializzare una repository sulla propria macchina. digitare `git init` sul terminale.
*N.B: Se abiliti la visualizzazione dei file nascosti sul tuo sistema operativo, noterai una cartella `.git`, questa cartella terrà conto di tutte le modifiche effettuate in quella repository.*

---
### Eseguire dei commit
Possiamo pensare ai `commit` come delle foto della nostra repository, è lo strumento principale con il quale GIT tiene conto delle modifiche. Ogni commit, ha un codice identificativo, un messaggio, quando è stato effettuato e da chi.
Prima di eseguire un commit, però, dobbiamo effettuare delle modifiche alla nostra repository, così che il nostro sistema di versionamento possa notarle. Quindi crea un file di testo qualunque.
Una volta creato, digita sul terminale `git status`, questo comando mostra lo stato della repository a partire dall'ultima commit effettuata *(nel nostro particolare caso, dalla creazione della repository, in quanto non sono presenti altre commit precedenti)*.
Dovresti vedere che il file appena creato si trova sotto `Untracked files`, quindi per aggiungerlo alla staging area, cioè in preparazione per il commit, bisogna digitare uno di questi due comandi sul terminale: 
 - `git add .` (aggiunge tutti file alla staging area)
 - `git add "nome_file"` (aggiunge solo il file indicato alla staging area)

Una volta aggiunto, ed rieseguito `git status`, dovresti vedere il file sotto `Changes to be committed`
Se è così, siamo pronti per eseguire il commit, quindi digita sul terminale: `git commit -m "prima commit"`
*N.B: il parametro `-m` serve per aggiungere direttamente il commento, senza passare per editor esterni.*

Una volta fatto, eseguendo ,nuovamente, il comando `git status` verremo informati che non è presente nessun file per il commit.
Eseguendo, invece, il comando `git log` nel terminale, verrà mostrata l'intera storia dei nostri commit, nel nostro caso sarà presente solo il commit appena fatto e di questo vedremo: 
- **id univoco** utile per ritornare a questo snapshot (foto) della storia della repository, 
- **branch** *ci arriveremo dopo*, 
- **l'autore** Nome utente e email,
- **Data**
- **Messaggio**
 ---
 ### Creare dei Branch
 Il Branch (ramo) è una linea temporale che segue una storia diversa da quella del branch dal quale l'abbiamo creata. Ad esempio, se vogliamo sviluppare feature slegate tra di loro, ognuna di queste avrà il proprio branch. In un progetto reale, per esempio, vogliamo creare un sito web composto da più pagine, quindi a partire da `master` il branch di default, creeremo diversi branch, ognuno dei quali si occupererà di tenere traccia delle diverse pagine, quindi avremo il branch `homepage`, il branch `chi-siamo` ecc... I quali poi verranno uniti (`merge`) nel branch principale, quando saranno completi.
 
  Per creare un branch possiamo digitare sul terminale il comando: `git branch 'nome_branch'`, quindi creiamo il branch `develop` attraverso: `git branch develop`, una volta fatto spostiamoci sul branch appena creato attraverso `git switch 'nome_branch'` un messaggio di conferma dovrebbe apparire nel terminale. 
  *N.B: È possibile creare un branch e spostarsi all'interno in comando solo, digitando nel terminale: `git checkout -b "nome_branch"`*

  Se eseguiamo il comando `git branch`, senza passare alcun parametro, verrà visualizzata la lista di tutti i branch presenti nella repository, con un * vicino il branch nel quale ci troviamo. 

In questo branch, creiamo un altro file *(file2.txt)* e poi faremo commit *(se non ricordi come fare, riguarda la sezione precedente)*
Dopo aver *commitato* rispostiamoci sul branch `master`, puoi usare il comando `git switch 'nome_branch'` che hai usato precedente oppure `git checkout 'nome_branch'` è indifferente. 

---
### Eseguire il merge tra branch
Se adesso guardiamo la cartella che contiene la nostra repository, noteremo che il *file2* che abbiamo creato sul branch `develop` non è presente. Questo perché le storie di `master` e `develop` sono slegate tra di loro. Per unire le due storie dobbiamo fare un merge di `develop` dentro `master`. Per farlo eseguiamo il seguente comando nel nostro terminale: `git merge develop`. 
*N.B: Nell'eseguire il merge tra due branch, è fondamentale sapere in che branch ci troviamo al momento, questo perché quando eseguiamo il `merge`, GIT, aggiungerà tutte le modifiche del branch che stiamo unendo, in quello nel quale ci troviamo. Nel nostro caso, GIT, prenderà tutte le modifiche (commit) effettuate nella storia del branch `develop`, e le aggiungerà nel branch `master`, `develop` rimarrà invariato invece.*

---

### Eseguire il push in una repository remota
È possibile collegare la nostra repository, creata in locale, con una remota, per poter lavorare allo stesso progetto con diverse macchine e/o persone. Ci serviremo di [Github](https://github.com/) un hosting gratuito. Dopo aver creato un account, possiamo creare una nuova repository cliccando sul bottone *new* oppure al seguente [indirizzo](https://github.com/new). 
Qui inseriremo solo il nome della repository e lasceremo vuoto e non selezionato tutto il resto, se vuoi, puoi decidere se renderla pubblica e quindi visibile a chi visualizza il tuo profilo, oppure privata.
Una volta creata, possiamo seguire le istruzioni fornite da Github, quindi nel nostro caso dovremmo guardare il secondo set di istruzioni, quelle al di sotto di *or push an existing repository from the command line*, in quanto abbiamo già creato una repository in locale.
*N.B: in quel set di istruzioni, GitHub, fa eseguire anche un comando per cambiare il nome del branch `master` in `main`*

Quindi nel nostro terminale eseguiremo il comando: `git remote add origin link_repsoitory`, per recuperare il link della repository remota, basta copiare il link della barra degli indirizzi del browser, il link sarà comunque in questo formato

    https://github.com/nome_utente_github/nome_repository_remota
Il comando appena eseguito, ci permette di unire le due repository, locale e remota, tuttavia ancora in remoto non sarà presente nulla di ciò che abbiamo in locale.

Per far arrivare le nostre modifiche in remoto, dobbiamo eseguire il `push` del nostro branch, quindi eseguiamo il comando `git push -u origin 'nome_branch_da_pushare'`.
*N.B: Il parametro `-u` è fondamentale in caso di branch non presenti ancora in remoto.*

Una volta effettuato il `push`, e riaggiornata la pagina di github sul nostro browser, dovremmo vedere i nostri file creati in locale, presenti anche in remoto. 
