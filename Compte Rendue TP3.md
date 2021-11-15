# TP 3 Emre Acet
## Exercice 1. Commandes de base


1. Commencez par mettre à jour votre système avec les commandes vues dans le cours.  <br/> 
`sudo apt upgrade (Met à jour les paquets qui le peuvent); sudo apt get update (Met à jour l’index des dépôts) et sudo apt dist-upgrade (Met à jour la distribution)`

2. Créez un alias “maj” de la ou des commande(s) de la question précédente. Où faut-il enregistrer cet alias pour qu’il ne soit pas perdu au prochain redémarrage? <br/> 
`commande : alias maj ='sudo apt update && sudo apt upgrade && sudo apt dist-upgrade'` <br/> 
 `il faut ensuite la mettre a la fin du fichier .bashrc (pour que ce soit sauvegradé): `

3. Utilisez le fichier /var/log/dpkg.log pour obtenir les 5 derniers paquets installés sur votre machine.<br/> 
`Avec la commande : tail -n5 /var/log/dpkg.log'` <br/> 
`Resultat :` <br/> 
2021-10-25 08:27:54 status half-configured openssl:amd64 1.1.1f-1ubuntu2.8 <br/> 
2021-10-25 08:27:54 status installed openssl:amd64 1.1.1f-1ubuntu2.8 <br/> 
2021-10-25 08:27:54 trigproc man-db:amd64 2.9.1-1 <br/> 
2021-10-25 08:27:54 status half-configured man-db:amd64 2.9.1-1 <br/> 
2021-10-25 08:27:57 status installed man-db:amd64 2.9.1-1<br/> 

4. Listez les derniers paquets qui ont été installés explicitement avec la commande apt install <br/> 
`Avec la commande : tail -n5 /var/log/dpkg.log'  ` <br/> 



5. Utilisez les commandes dpkg et apt pour compter de deux manières différentes le nombre de total de
paquets installés sur la machine (ne pas hésiter à consulter le manuel!). Comment explique-t-on la
(petite) différence de comptage? Pourquoi ne peut-on pas utiliser directement le fichier dpkg.log ?
6. Combien de paquets sont disponibles en téléchargement sur les dépôts Ubuntu?
7. A quoi servent les paquets glances, tldr et hollywood ? Installez-les et testez-les.
8. Quels paquets proposent de jouer au sudoku?
N’installez pas le paquet gnome-sudoku ou ksudoku sous peine de devoir probablement réinstaller
votre VM