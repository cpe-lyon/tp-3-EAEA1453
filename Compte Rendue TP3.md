# TP 3 Emre Acet
## Exercice 1. Commandes de base


1. Commencez par mettre à jour votre système avec les commandes vues dans le cours.  <br/> 
`sudo apt upgrade (Met à jour les paquets qui le peuvent); sudo apt get update (Met à jour l’index des dépôts) et sudo apt dist-upgrade (Met à jour la distribution)`

2. Créez un alias “maj” de la ou des commande(s) de la question précédente. Où faut-il enregistrer cet alias pour qu’il ne soit pas perdu au prochain redémarrage? <br/> 
`commande : alias maj ='sudo apt update && sudo apt upgrade && sudo apt dist-upgrade'` <br/> 
 `il faut ensuite la mettre a la fin du fichier .bashrc (pour que ce soit sauvegradé) et taper source bashrc (pour mettre a jour le bashrc) `

3. Utilisez le fichier /var/log/dpkg.log pour obtenir les 5 derniers paquets installés sur votre machine.<br/> 
`Avec la commande : grep installed /var/log/dpkg.log | tail -n5 | cut -d' ' -f5 | cut -d: -f1` <br/> 

4. Listez les derniers paquets qui ont été installés explicitement avec la commande apt install <br/> 
`Avec la commande : grep "apt install" /var/log/apt/history.log | cut -d' ' -f4` 
 <br/> 


5. Utilisez les commandes dpkg et apt pour compter de deux manières différentes le nombre de total de
paquets installés sur la machine (ne pas hésiter à consulter le manuel!). Comment explique-t-on la
(petite) différence de comptage ? Pourquoi ne peut-on pas utiliser directement le fichier dpkg.log ?  <br/> 
`dpkg : ` Il faut se déplacer dans le dossier /var/log avec la commande :
cd /var/log  <br/> 
Ensuite on vérifie le nombre de paquets présent dans le fichier dpkg.log en utilisant dpkg : <br/> 
`dpkg -l | grep "^ii" | wc -l`  <br/> 
le grep "^ii" permet de sélectionner seulement les lignes qui commence par "ii"  <br/> 
Le résultat est 595.  <br/> 
`apt : ` Il faut se déplacer dans le dossier /var/log/apt avec la commande :
cd /var/log  <br/> 
Ensuite on vérifie le nombre de paquets présent dans le fichier dpkg.log en utilisant apt :  <br/> 
`apt list --installed | wc -l`   <br/> 
Le résultat est 596 car il y a seulement une ligne en plus.  <br/> 


6. Combien de paquets sont disponibles en téléchargement sur les dépôts Ubuntu ? <br/> 
67 506 paquets sont disponibles en téléchargements. On obtient cela avec la comande : . <br/> 
`apt list | wc -l` <br/> 

7. A quoi servent les paquets glances, tldr et hollywood ? Installez-les et testez-les.  <br/> 
pour voir a quoi ils servent : `apt show Glances`  <br/> 
`Glances` est une application en mode caractère (ligne de commande) qui permet d'afficher l'état des principales ressources d'un système, de sa charge et du fonctionnement des applications <br/> 
`tldr` est une alternative au man mais dirigé par la communautée<br/> 
`hollywood` permet de simuler une fenêtre de hacking comme au cinéma, sur Ubuntu. ...  <br/> 
sudo apt install Glances tldr hollywood 
 
8. Quels paquets proposent de jouer au sudoku? <br/> 
N’installez pas le paquet gnome-sudoku ou ksudoku sous peine de devoir probablement réinstaller
votre VM  <br/> 
`gnome-sudoku` ou `ksudoku`

## Exercice 2.
A partir de quel paquet est installée la commande ls ? Comment obtenir cette information en une
seule commande, pour n’importe quel programme? Utilisez la réponse à cette question pour écrire un
script appelé origine-commande (sans l’extension .sh) prenant en argument le nom d’une commande, et
indiquant quel paquet l’a installée. <br/> 

`which -a ls | xargs dpkg -S` <br/> 
`coreutils: /bin/ls ` <br/>

`Script origine-commande :` <br/> 
``` bash
#!/bin/bash 

echo $(which -a $1 | xargs dpkg -S 2> /dev/null) ` <br/>
```

`on tape : bash origine-commande lacommande` <br/>


## Exercice 3.
Ecrire une commande qui affiche “INSTALLÉ” ou “NON INSTALLÉ” selon le nom et le statut du package
spécifié dans cette commande. <br>

`script verif_install : ` <br>
``` bash
#!/bin/bash

(apt list --installed | grep $1) && echo "installé" || echo "NON installé"
``` 

`résultat avec hollywood : `<br>
ii  hollywood      1.20-1       all          fill your console with Hollywood melodrama technobabble <br>
installé <br>


## Exercice 4.
Lister les programmes livrés avec coreutils. En particulier, on remarque que l’un deux se nomme [. De
quoi s’agit-il ?

`Pour voir les programmes livrés avec coreutils : dpkg -L coreutils `<br>

`Résultat :` <br>
...
/bin/mktemp
/bin/mv
/bin/pwd
/bin/readlink
/bin/rm
/bin/rmdir
/bin/sleep
/bin/stty
/bin/sync
/bin/touch
/bin/true
/bin/uname
/bin/vdir
/usr
/usr/bin
/usr/bin/[
/usr/bin/arch
/usr/bin/b2sum
/usr/bin/base32
/usr/bin/base64
/usr/bin/basename
/usr/bin/chcon
...

`le programme [ est un equivalent de la commande test, il est generalement utilisé dans les conditions comme if [ ... ]`

## Exercice 5. aptitude

`emacs est un éditeur de texte complet`

`Lynx est un client World Wide Web (WWW) complet`

## Exercice 6. Installation d’un paquet par PPA

Certains logiciels ne figurent pas dans les dépôts officiels. C’est le cas par exemple de la version ”officielle”
de Java depuis qu’elle est développée par Oracle. Dans ces cas, on peut parfois se tourner vers un ”dépôt
personnel” ou PPA.

`Dans le répértoire /etc/apt/sources.list.d$ se trouve le fichier tiblouk@abletteserver:/etc/apt/sources.list.d$` <br>

`Contenue :` deb http://ppa.launchpad.net/linuxuprising/java/ubuntu focal main <br>
#deb-src http://ppa.launchpad.net/linuxuprising/java/ubuntu focal main

## Exercice 7 Installation d’un logiciel à partir du code source

`installation en local :` <br>
`sudo apt install make`<br>
`sudo apt install pkg-config` <br>
`sudo apt install gcc` <br>
`make install PREFIX=~/.tiblouk` <br> <br> <br>

`installation checkinstall :  sudo apt install checkinstall`
<br><br>
`apres avoir taper sudo checkinstall dans le répertoire cbonsai : ` <br>
checkinstall 1.6.3, Copyright 2010 Felipe Eduardo Sanchez Diaz Duran
           This software is released under the GNU GPL.


The package documentation directory ./doc-pak does not exist.
Should I create a default set of package docs?  [y]: y

...
<br><br>
`Je peux maintenant lancer cbonsai de n'importe ou`