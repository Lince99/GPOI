---
tags: [General]
title: GPOI
created: '2019-11-21T07:50:52.720Z'
modified: '2019-12-19T08:34:29.866Z'
---

# GPOI

## GIT

Git è un sistema di **versioning**
> Sistema di versioning: serve per tenere traccia di ciascun cambiamento nei file di un progetto apportati da più utenti

### Storia

- Prima di git si utilizzava un copia/incolla dei file e delle cartelle oppure rinominando le versioni.  
  Questo ha portato ad un problema di fondo: se un file non viene copiato da una cartella all'altra? Se ne perde le tracce.  
- VCS locali: sistemi di versioning tramite database locali, ma se il sistema dove risiedeva il progetto falliva si perdeva tutto.
- VCS centralizzati: versioning distribuito tra i vari utenti

#### Linus Torvalds

Sviluppatore del kernel Linux, ha creato git per risanare alla mancanza di un sistema decentralizzato libero per lo sviluppo.
Git è un programma per CLI, ma è integrato in molti editor.  

---

### Comandi

```bash
alias gs = git status
alias gl = git log --oneline
```

```bash
git --version #stampa la versione di git
```

```bash
ls -lah #mostra tutti i file
```

#### Creazione repository git

```bash
mkdir Repository
git init #crea cartella .git
```

```bash
git status #mostra lo stato della repo
#Sul branch master

#Initial commit

#Untracked files:
#  (use "git add <file>..." to include in what will be committed)

#	index.html

#nothing added to commit but untracked files present (use "git add" to track)Sul branch master

#Commit iniziale

#Untracked files:
#  (use "git add <file>..." to include in what will be committed)

#	index.html

#nothing added to commit but untracked files present (use "git add" to track)

```

#### Tracciare i file

- _untracked file_ significa che un file non è sotto un controllo della versione.  
- Per ignorare dei file dal tracciamento (come i _.class_ in java o i _.o_ in c) bisogna usare il file **.gitignore**.

**SOLO DA FARE LA PRIMA VOLTA CHE SI USA GIT IN UN DISPOSITIVO**

```bash
git config --global user.email "nomeutente@email.com"
git config --global user.name "Username"
```

```bash
git add index.html #aggiunge al tracciamento il file index.html allo snapshot
git status #cambia lo stato del file
```

> COMMIT: sono degli snapshot fatti ai file da tracciare fatti da specifici utenti con una breve descrizione

D'ora in poi il file passa dallo stato di **staging** fatto da git add allo stato di **Committing**.

```bash
git commit -m "Messaggio significativo delle modifiche fatte"
```

```bash
git log
#commit dfba6054a117c5201f6e25f3f7eb5bcd07a5bea2
#Author: Lince99 <lynxnic99@gmail.com>
#Date:   Thu Nov 21 09:28:50 2019 +0100

#    Add index.html
#commit dfba6054a117c5201f6e25f3f7eb5bcd07a5bea2
#Author: Lince99 <lynxnic99@gmail.com>
#Date:   Thu Nov 21 09:28:50 2019 +0100

#    Add index.html
```

Se vengono apportate delle modifiche git status mostrerà che ci sono stati dei cambiamenti

```bash
git log --oneline
```

#### Ritorno al futuro

Per tornare indietro usare 
```bash
git checkout #primi sette caratteri dell'id
```

Linea del tempo:
```
                                    HEAD
------- o ------------- o ---------- o
  Initial commit  Add index.html  Add test

git checkout Add index.html (il suo id)

                       HEAD
------- o ------------- o ---------- o
  Initial commit  Add index.html  Add test
```

HEAD è il puntatore all'ultimo commit (stato della repo).  
Con il **checkout** non vengono eliminati i commit successivi, ma sposta l'HEAD.

Per tornare all'ultimo commit (nel branch master):

```bash
git checkout master
```

#### TAG

I tag servono a sostituire il codice generato nei commit, usato solitamente nelle versioni stable della repository.

```bash
git tag #mostra i tag presenti
git tag -a v1.0 -m "First stable version"
```

#### REVERT

```
                                    HEAD
------- o ------------- o ---------- o
  Initial commit  Add index.html  Broken commit

git checkout "Add index.html" (il suo id)

                                                    HEAD
------- o ------------- o ---------- o ------------- o ---
  Initial commit  Add index.html  Broken commit     Fix
```

Per tornare ad una versione stabile

```bash
git revert Broken commit #--abort in caso di problemi, usare sempre i 7 caratteri del commit precedente
```

#### RESET

Lascia i file non tracciati, ma va a modificare i file già tracciati al precedente commit
```bash
git reset --hard
```

Per togliere i file non tracciati
```bash
git clean -f
```

---

#### BRANCH

In git un branch è una linea di sviluppo indipendente.

- Serve per aggiungere nuove funzionalità al programma senza andare a compromettere lo sviluppo principale
- 

```
 master
   |
   o
   | \ 
   |  \
   |   | dev
   o   o 
   |   |
   |   o 
   |  /  \
   o /    \
   |merge  | experimental
   |       o
   |       |
   o       o
   |      / 
   |    /   
   |  /
   o /  
   |merge
   |
```

```bash
git branch #mostra solo master e l'asterisco mostra il branch corrente
```


Facendo un checkout viene creata una specie di branch
```bash
git checkout
git branch
git checkout master
```

Per creare un branch
```bash
git branch prova
git checkout prova
```

D'ora in poi si lavorerà nel branch prova senza andare a modificare il branch master.

```
 master
   |
   o
   | \ 
   |  \
   |   | prova
   o   o 
```

#### MERGE CONFLICT

Conflitto nel merge tra più branch, bisogna scegliere quale versione tenere

#### MERGE IN AZIENDA

Quando si è pronti al rilascio di una versione stabile, si mette in produzione il progetto.
> MAI METTERE IN PRODUZIONE IL VENERDI' SERA

#### Esempio di più branch

```bash
mkdir sito
cd sito
git init
nano index.html
git add *
git commit -m "Add index.html"
git log --oneline #gl
git branch dev
git checkout dev
git checkout -b css #crea il branch se non esiste
nano style.css
git add *
git commit -m "Add style.css"
git checkout dev
git merge css
git log --oneline
git checkout master
git merge dev
```

[Tree view with git log](https://stackoverflow.com/questions/2421011/output-of-git-branch-in-tree-like-fashion)

```bash
git log --graph --all --format='%C(cyan dim) %p %Cred %h %C(white dim) %s %Cgreen(%cr)%C(cyan dim) <%an>%C(bold yellow)%d%Creset'
```

### REBASE

Simile al merge, prende un set di commit e li copia in un altro branch

Obbiettivo: allineare master a bugFix

```bash
git checkout -b bugFix
git commit -m "vari commit in bugFix"
git rebase master #in bugFix
git rebase bugFix #in master
```

Passaggi:
- Creare nuovo branch
- Fare commit in entrambi i branch
- fare checkout nel branch da fare il rebase
- git rebase master
- allineare master con i commit del branch con git rebase nomeBranch

---

### Repository remote

Sono delle cartelle git salvate su piattaforme cloud.  


#### Creare una copia locale di una repository da internet

```bash
git clone linkdellarepo
```

#### Branch remote

Le repository remote hanno come nome **o/master** e sta per **origin/master**.  

```bash
git remote -v
```

#### Update locali

- Repository locale clonata da quella remota
- Nel caso qualcuno abbia modificato qualcosa nella repository remota si verifica un conflitto
- Per risolverlo esistono una serie di comandi

Fetch va a copiare i commit che non sono presenti in locale dopo un certo commit

```bash
git fetch
```

- Scarica i commit che mancano nella repository locali da quella remota
- aggiorna il punto in cui si trova il puntatore

**IMPORTANTE** : non aggiorna lo stato dei file in locale (scarica e basta)

Per applicare le modifiche in master si utilizza git pull (è un fetch e un merge)

```bash
git pull
```

#### Update remoti

```bash
git push
```

In caso di conflitti nella storia dei commit

```bash
git fetch
git rebase o/master
git push
```

oppure più brevemente

```bash
git pull --rebase
```

```bash
git fetch
git merge o/master
git push
```



---

# Licenza

Questa documentazione è sotto licenza [MIT](https://opensource.org/licenses/MIT)

