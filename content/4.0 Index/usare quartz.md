---
title: usare quartz
type: 
campagna:
name: usare quartz
tags: []
---
# PRE

fare fork di quarz

# PER LINUX

clonare repo "quarz" dal proprio account (puo essere rinominato come 'nome utente.github.io' per il server pages ma sul proprio pc puo avere qualsiasi nome l'importante é la cartella .git)
installare go
installare rust
go install di [hugo-obsidian](https://github.com/jackyzha0/hugo-obsidian) (vedere dove viene installato per poi usare il file)
	oppure scaricare eseguibile .bin
installare [hugo-extended](https://github.com/gohugoio/hugo/releases)
installare nodemon
scaricare [obsidian-export](https://github.com/zoni/obsidian-export) da github con l'eseguibile (funziona con rust)

fare i due file watch e compile

### watch.sh

```sh
#!/bin/bash

cd /home/riccardo/Scrivania/website/quartz;

nodemon -w /home/riccardo/Scrivania/website/prova -w /home/riccardo/Scrivania/website/quartz/assets/js -w /home/riccardo/Scrivania/website/quartz/assets/styles -w /home/riccardo/Scrivania/website/quartz/layouts -w /home/riccardo/Scrivania/website/quartz/config.toml -w /home/riccardo/Scrivania/website/quartz/data/config.yaml -x "/home/riccardo/Scrivania/website/quartz/compile.sh" -e md,html,js,scss,xml
```

nodemon fa andare in loop e controlla nelle directory i cambiamenti
ultimo fa partire compile

### compile.sh

```sh
#!/bin/bash

cd /home/riccardo/Scrivania/website;
rm -fr ./quartz/content/*;
rm -rf ./quartz/public/*;
./obsidian-export.bin --frontmatter=always ./prova ./quartz/content;
cd ./quartz;
./hugo-obsidian -input=content -output=assets/indices -index -root=. && hugo server --enableGitInfo --minify;
```

rm cancella i file nelle cartelle
obsidian-export.bin è il file da utilizzare, --frontmatter inserisce --- --- all'inizio
hugo-obsidian serve per far partire il server locale



# PER WINDOWS

clonare repo "quarz" dal proprio account (puo essere rinominato come 'nome utente.github.io' per il server pages ma sul proprio pc puo avere qualsiasi nome l'importante é la cartella .git)
installare go
installare rust
go install di [hugo-obsidian](https://github.com/jackyzha0/hugo-obsidian)
installare [hugo-extended](https://github.com/gohugoio/hugo/releases) 
installare nodemon
	installare [nvm](https://github.com/coreybutler/nvm-windows/releases) .exe
	aprire terminale e fare nvm install nodemon
scaricare [obsidian-export](https://github.com/zoni/obsidian-export)

fare i due file e mettere a posto le directory

### watch.sh

```sh
#!/bin/bash

cd C:/Users/crick/Desktop/webserver/quartz;

nodemon -w C:/Users/crick/Desktop/webserver/prova -w C:/Users/crick/Desktop/webserver/quartz/assets/js -w C:/Users/crick/Desktop/webserver/quartz/assets/styles -w C:/Users/crick/Desktop/webserver/quartz/layouts -w C:/Users/crick/Desktop/webserver/quartz/config.toml -w C:/Users/crick/Desktop/webserver/quartz/data/config.yaml -x "C:/Users/crick/Desktop/webserver/quartz/compile.sh" -e md,html,js,scss,xml
```

### compile.sh

```sh
#!/bin/bash
 
cd C:/Users/crick/Desktop/webserver;
rm -fr ./quartz/content/*;
rm -rf ./quartz/public/*;
./obsidian-export.exe --frontmatter=always ./prova ./quartz/content;
cd ./quartz;
hugo-obsidian -input=content -output=assets/indices -index -root=. && hugo server --enableGitInfo --minify;
```

## SERVE GIT BASH INSTALLATO 

possibile installare direttamente quando si installa git



per far partire il tutto fare destro->destro-> git bash here, runnare sh watch.sh