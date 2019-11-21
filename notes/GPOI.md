---
tags: [General]
title: GPOI
created: '2019-11-21T07:50:52.720Z'
modified: '2019-11-21T08:32:02.260Z'
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

### Linus Torvalds

Sviluppatore del kernel Linux, ha creato git per risanare alla mancanza di un sistema decentralizzato libero per lo sviluppo.
Git è un programma per CLI, ma è integrato in molti editor.  

---

### Comandi

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

```


---

