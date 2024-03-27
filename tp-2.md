1. Find me

🌞 Trouver le chemin vers le répertoire personnel de votre utilisateur
``````
matis@matis:~$ pwd
/home/matis
``````
🌞 Trouver le chemin du fichier de logs SSH
``````
matis@matis:/$ cd /var
matis@matis:/var$ ls
backups  cache  crash  lib  local  lock  log  mail  metrics  opt  run  snap  spool  tmp
matis@matis:/var$ cd log
matis@matis:/var/log$ ls
alternatives.log  auth.log       btmp          dmesg       dmesg.2.gz  dpkg.log  fontconfig.log   gpu-manager-switch.log  journal   openvpn            syslog                vbox-setup.log
apport.log        boot.log       cups          dmesg.0     dmesg.3.gz  faillog   gdm3             hp                      kern.log  private            ubuntu-advantage.log  wtmp
apt               bootstrap.log  dist-upgrade  dmesg.1.gz  dmesg.4.gz  firebird  gpu-manager.log  installer               lastlog   speech-dispatcher  unattended-upgrades
matis@matis:/var/log$ nano auth.log
``````
🌞 Trouver le chemin du fichier de configuration du serveur SSH
``````
matis@matis:/var/log$ cd ..
matis@matis:/var$ cd ..
matis@matis:/$ cd /var
matis@matis:/var$ ls
backups  crash  local  log   metrics  run   spool
cache    lib    lock   mail  opt      snap  tmp
matis@matis:/var$ cd log
matis@matis:/var/log$ ls
alternatives.log  dmesg       fontconfig.log          openvpn
apport.log        dmesg.0     gdm3                    private
apt               dmesg.1.gz  gpu-manager.log         speech-dispatcher
auth.log          dmesg.2.gz  gpu-manager-switch.log  syslog
boot.log          dmesg.3.gz  hp                      ubuntu-advantage.log
bootstrap.log     dmesg.4.gz  installer               unattended-upgrades
btmp              dpkg.log    journal                 vbox-setup.log
cups              faillog     kern.log                wtmp
dist-upgrade      firebird    lastlog
matis@matis:/var/log$ nano fontconfig.log
``````
II. Users

1. Nouveau user
🌞 Créer un nouvel utilisateur
``````
(matis@thinkpad)-[~]$ : sudo useradd -m -d /home/papier_alu/marmotte marmotte
(matis@thinkpad)-[~]$ : sudo passwd marmotte 
(mettre le mot de passe 'chocolat')
``````
2. Infos enregistrées par le système
🌞 Prouver que cet utilisateur a été créé
``````
(matis@thinkpad)-[/home]$ : cat /etc/passwd | grep marmotte
(matis@thinkpad)-[/home]$ : marmotte:x:1001:1001::/home/papier_alu/marmotte:/bin/sh
``````
🌞 Déterminer le hash du password de l'utilisateur marmotte
````
(matis@thinkpad)-[/home]$ : sudo cat /etc/shadow | grep marmotte
(matis@thinkpad)-[/home]$ : marmotte:$y$j9T$TJLmx5v/Ke.ticrIDRn20$BAEt8r.TjrGZtVv0M3GTfKmufqnUtUjxLHfiPFNxfoB:19744:0:99999:7:::
````
3. Connexion sur le nouvel utilisateur

🌞 Tapez une commande pour vous déconnecter : fermer votre session utilisateur
``````
(matis@thinkpad)-[/home]$ : exit
``````
🌞 Assurez-vous que vous pouvez vous connecter en tant que l'utilisateur marmotte
``````
(matis@thinkpad)-[/home]$ : su - marmotte
Password : (chocolat)
$
``````
Partie 2 : Programmes et paquets

I. Programmes et processus

1. Run then kill

🌞 Lancer un processus sleep

``````
(dans le premier terminal):
(matis@thinkpad)-[~] : sleep 1000
(dans le deuxième terminal):
(matis@thinkpad)-[/home]$ : ps aux | grep sleep
matis  63898 0.0 0.0 5896 1536 pts/0 S+ 20:22 0:00 sleep 1000
matis  63984 0.0 0.0 6872 2176 pts/2 S+ 20:22 0.00 /usr/bin/grep slepp
``````
🌞 Terminez le processus sleep depuis le deuxième terminal

``````
(matis@thinkpad)-[/home/matis] : pgrep sleep
PS > 67472
(matis@thinkpad)-[/home/matis] : kill 67472 
(dans le premier terminal) :
(matis@thinkpad)-[~] : sleep 1000
zsh : terminated sleep 1000
``````

2. Tâche de fond

🌞 Lancer un nouveau processus sleep, mais en tâche de fond

``````
(matis@thinkpad)-[~] : sleep 1000 &
[1] 71451
``````

🌞 Visualisez la commande en tâche de fond
``````
(matis@thinkpad)-[~] : jobs
[1] +running sleep 1000
``````
3. Find paths

🌞 Trouver le chemin où est stocké le programme sleep

``````
(matis@thinkpad)-[~] : which sleep (command -v sleep)
/usr/bin/sleep
(ls -al /bin | grep sleep)
``````
🌞 Tant qu'on est à chercher des chemins : trouver les chemins vers tous les fichiers qui s'appellent .bashrc
``````
(matis@thinkpad)-[/home/matis] : sudo find / -name *.bashrc
[sudo] password for matis :
/usr/share/kali-defaults/etc/skel/.bashrc
/usr/share/doc/adduser/examples/adduser.local.conf.examples/skel/dot.bashrc
/usr/share/doc/adduser/examples/adduser.local.conf.examples/bash.bashrc
/usr/share/base-files/doc.bashrc
find: '/run/user/1000/gvfs': Permission denied
/etc/skel/.bashrc
/etc/bash.bashrc
/root/.bashrc
/home/matis/.bashrc
/home/papier_alu/marmotte/.bashrc
``````
4. La variable PATH

🌞 Vérifier que

``````
- pour sleep :
(matis@thinkpad)-[/home/matis] : which sleep
/usr/bin/sleep

- pour ssh :
(matis@thinkpad)-[/home/matis] :  which ssh
/usr/bin/ssh

- pour ping :
(matis@thinkpad)-[/home/matis] : which ping
/usr/bin/ping
``````
II. Paquets

🌞 Installer le paquet firefox

``````
(matis@thinkpad)-[/home/matis] : sudo apt install firefox
``````
🌞 Utiliser une commande pour lancer Firefox
``````
(matis@thinkpad)-[/home/matis] : firefox
``````
🌞 Installer le paquet nginx
``````
(matis@thinkpad)-[/home/matis] : sudo apt install nginx
``````
🌞 Déterminer
``````
(le chemin vers le dossiers de logs de NGINX):

(matis@thinkpad)-[/home/matis] : sudo grep -R access_log /etc/nginx/
/etc/nginx/nginx.conf: access_log /var/log/nginx/access.log;

(matis@thinkpad)-[/home/matis] : sudo grep -R error_log /etc/nginx
/etc/nginx/nginx.conf:error_log /var/log/nginx/error_log;

(pour le chemin vers le dossier qui contient la configuration de NGINX)

(matis@thinkpad)-[/home/matis] : ls /etc/nginx/nginx.conf
/etc/nginx/nginx.conf

(matis@thinkpad)-[/home/matis] : ls /etc/nginx/sites-available
default

(matis@thinkpad)-[/home/matis] : ls /etc/nginx/sites-enabled
default
``````
🌞 Mais aussi déterminer...
``````
- l'adresse http ou https des serveurs où vous téléchargez des paquets :

(matis@thinkpad)-[/home/matis] : cat /etc/apt/sources.list
#see https://www.kali.org/docs/general-use/kali-linux-sources-list-repositories/ deb https://http.kali.org/kali kali-rolling main contrib non-free non-free-firmware

# Additionnal line for source packages

# deb-src http://htpp.kali.org/kali kali-rolling main non-free non-free-firmware

- une commande apt install ou dnf install permet juste de faire un téléchargement HTTP :

(matis@thinkpad)-[/home/matis] : sudo apt-get download http
- ma question c'est donc : sur quel URL tu t'es connecté pour télécharger ce paquet :

Je me suis connecté avec le premier URL pour télécharger ce paquet

- il existe un dossier qui contient la liste des URLs consultées quand vous demandez un téléchargement de paquets: 

(matis@thinkpad)-[/home/matis] : /etc/apt/sources.list
``````

Partie 3 : Poupée russe

🌞 Récupérer le fichier meow
``````
┌──(matis㉿thinkpad)-[~] : wget "https://gitlab.com/it4lik/b1-linux-2023/-/blob/master/tp/2/meow"
``````

🌞 Trouver le dossier dawa/

``````
- utilisez la commande file /path/vers/le/fichier pour déterminer le type du fichier:

(matis@thinkpad)-[~] : file -v meow
file-5.45
magic file from /etc/magic:/usr/share/misc/magic

- renommez-le fichier correctement (si c'est une archive compressée ZIP, il faut ajouter .zip à son nom) :

(matis㉿thinkpad)-[~]
└─$ cd Downloads    
(matis@thinkpad)-[~] : mv -i meow meow.zip
┌──(matis㉿thinkpad)-[~/Downloads]
└─$ ls
meow.zip
                
- extraire l'archive avec une commande :

(matis㉿thinkpad)-[~]
└─$ cd Downloads    
(matis@thinkpad)-[~] : ls
meow.zip
┌──(matis㉿thinkpad)-[~/Downloads]
└─$ ls  
meow.zip
(matis㉿thinkpad)-[~]
└─$ sudo unzip meow.zip
Archive: meow.zip
    inflating: meow

- répétez ces opérations jusqu'à trouver le dossier dawa/ :

┌──(matis㉿thinkpad)-[~/Downloads/dossier]
└─$ ls
meow
┌──(matis㉿thinkpad)-[~/Downloads/dossier]
└─$ file meow
meow: XZ compressed data, checksum CRC64┌──(matis㉿thinkpad)-[~/Downloads/dossier]
└─$ mv meow meow.xz
┌──(matis㉿thinkpad)-[~/Downloads/dossier]
└─$ file meow.xz
meow.xz: XZ compressed data, checksum CRC64
┌──(matis㉿thinkpad)-[~/Downloads/dossier]
└─$ xz -d meow.xz
┌──(matis㉿thinkpad)-[~/Downloads/dossier]
└─$ ls
meow
┌──(matis㉿thinkpad)-[~/Downloads/dossier]
└─$ file meow
meow: bzip2 compressed data, block size = 900k
┌──(matis㉿thinkpad)-[~/Downloads/dossier]
└─$ bunzip2 meow
┌──(matis㉿thinkpad)-[~/Downloads/dossier]
└─$ ls
meow.out      
┌──(matis㉿thinkpad)-[~/Downloads/dossier]
└─$ file meow.out
meow.out: RAR archive data, v5
┌──(matis㉿thinkpad)-[~/Downloads/dossier]
└─$ unrar meow.out
┌──(matis㉿thinkpad)-[~/Downloads/dossier]
└─$ mv meow.out meow.rar
┌──(matis㉿thinkpad)-[~/Downloads/dossier]
└─$ ls
meow.rar
┌──(matis㉿thinkpad)-[~/Downloads/dossier]
└─$ unrar x meow.rar

UNRAR 7.00 beta 2 freeware      Copyright (c) 1993-2023 Alexander Roshal


Extracting from meow.rar

Extracting  meow                                                      OK
All OK
┌──(matis㉿thinkpad)-[~/Downloads/dossier]
└─$ file meow
meow: gzip compressed data, from Unix, original size modulo 2^32 145049600 gzip compressed data, reserved method, has CRC, extra field, has comment, from FAT filesystem (MS-DOS, OS/2, NT), original size modulo 2^32 145049600
┌──(matis㉿thinkpad)-[~/Downloads/dossier]
└─$ mv meow  meow.tar.gz
┌──(matis㉿thinkpad)-[~/Downloads/dossier]
└─$ tar -xvf meow.tar.gz
┌──(matis㉿thinkpad)-[~/Downloads/dossier]
└─$ ls
dawa  meow.rar  meow.tar.gz

``````
🌞 Dans le dossier dawa/, déterminer le chemin vers

``````
- le seul fichier de 15Mo
┌──(matis㉿thinkpad)-[~/Downloads/dossier/dawa]
└─$ find -type f -size 15M
./folder31/19/file39

- le seul fichier qui ne contient que des 7
┌──(matis㉿thinkpad)-[~/Downloads/dossier/dawa]
└─$ 

- le seul fichier qui est nommé cookie :

┌──(matis㉿thinkpad)-[~/Downloads/dossier/dawa]
└─$ find -type f -name "cookie"                           
./folder14/25/cookie
                         

- le seul fichier caché (un fichier caché c'est juste un fichier dont le nom commence par un .) :

┌──(matis㉿thinkpad)-[~/Downloads/dossier/dawa]
└─$ find -type f -name .* (ou find -type f -name .* -exec basename {};)  
./folder32/14/.hidden_file


- le seul fichier qui date de 2014 :

┌──(matis㉿thinkpad)-[~/Downloads/dossier/dawa]
└─$ find  -type f -newermt 2014-01-01 ! -newermt 2015-01-01 -exec stat --format="%Y %n" {} \; | sort -n | head -n 1 

1390312815 ./folder36/40/file43

- le seul fichier qui a 5 dossiers-parents :
