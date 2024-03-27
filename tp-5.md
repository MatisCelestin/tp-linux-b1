🌞 Vous fournirez dans le compte-rendu Markdown, en plus du fichier, un exemple d'exécution avec une sortie

```
matis@root:~$ sudo mkdir -p /srv/idcard/
matis@root:~$ sudo nano /srv/idcard/idcard.sh
matis@root:~$ cd /srv/idcard
matis@root:/srv/idcard$ sudo chmod +x idcard.sh
matis@root:/srv/idcard$ sudo ./idcard.sh
Nom de la machine :
LTS
Nom de l'OS de la machine :
Ubuntu 22.04.3 LTS
Version du noyau Linux :
6.5.0-17-generic
Adresse IP de la machine :
127.0.0.1
192.168.1.78
10.3.1.1
État de la RAM :
Mem:            15Gi       5,3Gi       1,2Gi       1,2Gi       8,9Gi       8,6Gi
Espace restant sur le disque dur :
288G
Top 5 des processus qui utilisent le plus de RAM :
firefox 4.1
Isolated Web
Isolated Web
chrome 2.4
chrome 2.3
Liste des ports en écoute :
udp 0.0.0.0:631
udp 0.0.0.0:37486
udp 224.0.0.251:5353
udp 224.0.0.251:5353
udp 224.0.0.251:5353
udp 0.0.0.0:5353
udp 127.0.0.53%lo:53
udp [::]:42356
udp [::]:5353
tcp 0.0.0.0:22
tcp 127.0.0.53%lo:53
tcp 127.0.0.1:631
tcp *:80
tcp [::]:22
tcp [::1]:631
Dossiers disponibles dans la variable PATH :
/usr/local/sbin
/usr/local/bin
/usr/sbin
/usr/bin
/sbin
/bin
/snap/bin

```
II. Script youtube-dl

1. Premier script youtube-dl

A. Le principe + B. Rendu attendu

```
matis@root:/$ sudo su
root@root:/# mkdir -p /var/log/yt/
root@root:/# exit
exit
matis@root:/$ sudo chown root:root /var/log/yt/
matis@root:/$ ls -l /var/log/yt/
total 0
matis@root:/$ sudo mkdir -p /srv/yt/downloads
matis@root:/$ sudo chown root:root /srv/yt/downloads
matis@root:/$ sudo chmod 755 /srv/yt/downloads
matis@root:/$ sudo chmod +x /srv/yt/yt.sh
Video https://www.youtube.com/watch?v=sNx57atloH8 was downloaded.
File path : /srv/yt/downloads//.mp4
matis@root:/$ sudo apt install youtube-dl
matis@root:/$ sudo /srv/yt/yt.sh --verbose https://www.youtube.com/watch?v=sNx57atloH8
[debug] System config: []
[debug] User config: []
[debug] Custom config: []
[debug] Command-line args: ['--get-title', '--verbose']
[debug] Encodings: locale UTF-8, fs utf-8, out utf-8, pref UTF-8
[debug] youtube-dl version 2021.12.17
[debug] Python version 3.10.12 (CPython) - Linux-6.5.0-17-generic-x86_64-with-glibc2.35
[debug] exe versions: ffmpeg 4.4.2, ffprobe 4.4.2, rtmpdump 2.4
[debug] Proxy map: {}
WARNING: Long argument string detected. Use -- to separate parameters and URLs, like this:
youtube-dl --verbose -- --get-title

Usage: youtube-dl [OPTIONS] URL [URL...]

youtube-dl: error: You must provide at least one URL.
Type youtube-dl --help to see a list of all options.
Video --verbose was downloaded.
File path : /srv/yt/downloads//.mp4
matis@root:/srv/yt$ sudo /srv/yt/yt.sh https://www.youtube.com/watch?v=YOQbZPtj4Bg
ERROR: Unable to extract uploader id; please report this issue on https://yt-dl.org/bug . Make sure you are using the latest version; see  https://yt-dl.org/update  on how to update. Be sure to call youtube-dl with the --verbose flag and include its complete output.
Téléchargement de la vidéo...
ERROR: Unable to extract uploader id; please report this issue on https://yt-dl.org/bug . Make sure you are using the latest version; see  https://yt-dl.org/update  on how to update. Be sure to call youtube-dl with the --verbose flag and include its complete output.
Téléchargement de la description...
ERROR: Unable to extract uploader id; please report this issue on https://yt-dl.org/bug . Make sure you are using the latest version; see  https://yt-dl.org/update  on how to update. Be sure to call youtube-dl with the --verbose flag and include its complete output.
Téléchargement terminé avec succès dans /srv/yt/downloads//.
matis@root:/srv/yt$ sudo youtube-dl --u
--update      --user-agent  --username    
matis@root:/srv/yt$ sudo youtube-dl --update 
Usage: youtube-dl [OPTIONS] URL [URL...]

youtube-dl: error: youtube-dl's self-update mechanism is disabled on Debian.
Please update youtube-dl using apt(8).
See https://packages.debian.org/sid/youtube-dl for the latest packaged version.


```

2. MAKE IT A SERVICE

A. Adaptation du script + B. Le service + C. Rendu

🌞 Vous fournirez dans le compte-rendu, en plus des fichiers :

```
matis@root:/srv/yt$ cd yt-v2/
matis@root:/srv/yt/yt-v2$ ls
matis@root:/srv/yt/yt-v2$ sudo nano /srv/yt/yt-v2.sh
matis@root:/srv/yt/yt-v2$ sudo /srv/yt/yt.sh
Veuillez fournir l'URL de la vidéo YouTube à télécharger.
matis@root:/srv/yt/yt-v2$ cd ..
matis@root:/srv/yt$ chmod +x yt-v2.sh
chmod: modification des droits de 'yt-v2.sh': Opération non permise
matis@root:/srv/yt$ sudo chmod +x yt-v2.sh
matis@root:/srv/yt$ ./yt-v2.sh
(en chargement)
 cd ..
matis@root:/srv$ cd ..
matis@root:/$ sudo nano /etc/systemd/system/yt.service
([Unit]
Description=Service de téléchargement de vidéos YouTube
After=network.target

[Service]
ExecStart=/srv/yt/yt-v2.sh
User=yt

[Install]
WantedBy=multi-user.target
)
matis@root:/$ sudo adduser --system --no-create-home yt
Ajout de l'utilisateur système « yt » (UID 131) ...
Ajout du nouvel utilisateur « yt » (UID 131) avec pour groupe d'appartenance « nogroup » ...
Pas de création du répertoire personnel « /home/yt ».
matis@root:/$ sudo addgroup yt
Ajout du groupe « yt » (GID 1001)...
Fait.
matis@root:/$ sudo chown -R :yt /srv/yt
matis@root:/$ sudo chown yt:yt /var/log/yt.log
chown: impossible d'accéder à '/var/log/yt.log': Aucun fichier ou dossier de ce type
matis@root:/$ sudo su
root@root:/# sudo chown yt:yt /var/log/yt.log
chown: impossible d'accéder à '/var/log/yt.log': Aucun fichier ou dossier de ce type
root@root:/# exit
exit
matis@root:/$ sudo touch /var/log/yt.log
matis@root:/$ sudo chown yt:yt /var/log/yt.log
matis@root:/$ sudo usermod -aG yt yt
matis@root:/$ sudo systemctl daemon-reload
matis@root:/$ systemctl status yt
○ yt.service - Service de téléchargement de vidéos YouTube
     Loaded: loaded (/etc/systemd/system/yt.service; disabled; vendor preset: enabled)
     Active: inactive (dead)
matis@root:/$ systemctl start yt
matis@root:/$ systemctl status yt
● yt.service - Service de téléchargement de vidéos YouTube
     Loaded: loaded (/etc/systemd/system/yt.service; disabled; vendor preset: enabled)
     Active: active (running) since Fri 2024-03-01 18:06:32 CET; 2s ago
   Main PID: 148376 (yt-v2.sh)
      Tasks: 2 (limit: 18764)
     Memory: 552.0K
        CPU: 2ms
     CGroup: /system.slice/yt.service
             ├─148376 /bin/bash /srv/yt/yt-v2.sh
             └─148377 sleep 60

mars 01 18:06:32 root systemd[1]: Started Service de téléchargement de vidéos YouTube.
matis@root:/$ systemctl stop yt
matis@root:/$ systemctl status yt
○ yt.service - Service de téléchargement de vidéos YouTube
     Loaded: loaded (/etc/systemd/system/yt.service; disabled; vendor preset: enabled)
     Active: inactive (dead)

mars 01 18:06:32 root systemd[1]: Started Service de téléchargement de vidéos YouTube.
mars 01 18:10:37 root systemd[1]: Stopping Service de téléchargement de vidéos YouTube...
mars 01 18:10:37 root systemd[1]: yt.service: Deactivated successfully.
mars 01 18:10:37 root systemd[1]: Stopped Service de téléchargement de vidéos YouTube.
```
