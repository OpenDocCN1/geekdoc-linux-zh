![image](Images/image-4RML5381.png)

## Wi-Fi HACKING

avec

### KALI LINUX

Guide étape par étape : apprenez à pénétrer les réseaux Wi-Fi et les meilleures stratégies pour les sécuriser

––––––––

B.Anass

––––––––

Copyright © 2021 HackinGeeK LTD

Also by B. Anass

Hacking

[Hacking pour débutant : le guide ultime du débutant pour apprendre les bases du hacking avec Kali Linux et comment se protéger des hackers](https://www.draft2digital.com/catalog/756654)

[Kali Linux pour débutant : le guide ultime du débutant pour apprendre le système d'exploitation des hackers](https://www.draft2digital.com/catalog/757010)

[Metasploit Pour Débutant: Le guide du débutant pour bypasser les antivirus, contourner les pare-feu et exploiter des machines avec le puissant Framework Metasploit](https://www.draft2digital.com/catalog/757314)

[Dark Python : Apprenez à créer vos propres outils de Hacking (2e édition)](https://www.draft2digital.com/catalog/757617)

[Le coté obscur d’Internet: explorez ce que 99% des internautes ignorent sur les ténèbres d’Internet et apprenez à visiter le dark net en toute sécurité](https://www.draft2digital.com/catalog/757941)

[Le secret De La Cybersécurité: Le guide pour protéger votre famille et votre entreprise de la cybercriminalité](https://www.draft2digital.com/catalog/757622)

[Web hacking: apprenez à tester la sécurité des applications web comme un hacker pro avec kali linux](https://www.draft2digital.com/catalog/757624)

[Wi-Fi hacking avec Kal Linux : guide étape par étape : apprenez à pénétrer les réseaux Wi-Fi et les meilleures stratégies pour les sécuriser](https://www.draft2digital.com/catalog/757945)

## Table des Matières

[Droits d'Auteur](#chapter0000.html)

[Also By B. Anass](#chapter0001.html)

[Wi-Fi hacking avec Kal Linux : guide étape par étape : apprenez à pénétrer les réseaux Wi-Fi et les meilleures stratégies pour les sécuriser](#chapter0002.html)

[Pourquoi kali linux ?](#chapter0003.html)

[Ce dont tu as besoin pour suivre ce livre](#chapter0004.html)

[Matériel](#chapter0005.html)

[CHAPITRE 4 | Wi-Fi HACKING... NIVEAU : 0](#chapter0006.html)

[Sign up for B. Anass's Mailing List](#chapter0007.html)

[Further Reading: Hacking pour débutant : le guide ultime du débutant pour apprendre les bases du hacking avec Kali Linux et comment se protéger des hackers](#chapter0008.html)

[Also By B. Anass](#chapter0009.html)

## Pourquoi J’ai Écrit Ce Livre :

Il y a deux sortes de personnes qui se posent la question de : comment hacker un Wi-Fi ?

La première catégorie : une personne qui cherche une méthode miracle, un bouton à appuyer ou encore une application qui va lui permettre de PIRATER la clé Wi-Fi de son voisin. Si tu en fais partie, ne continue surtout pas de lire. Si ce n’est pas le cas, ce livre est fait pour toi.

La deuxième catégorie : un geek (ou une geek) qui a compris que le hacking est un art qui s’apprend, et qu’il n’y a rien de miraculeux dedans, juste une compréhension approfondie du fonctionnement des systèmes menant à une compréhension des méthodes altèrant ce fonctionnement. C'est ce qu'on appelle en effet, “exploitation”, des personnes curieuses, à la recherche du savoir et de pouvoir.  C’est pour ces gens-là que j’écris ces lignes.

### “IF YOU AREN’T MAKING

### ANY MISTAKES, YOU

### AREN’T REALLY TRYING”

Marcus J.carey

## Table des matiéres

[Introduction](#chapter0002.html)

[Pourquoi kali linux ?](#chapter0003.html)

[Ce dont tu as besoin pour suivre ce livre](#chapter0004.html)

[Chapitre 2](#chapter0004.html)

[préparation du lab](#chapter0004.html)

[Matériel](#chapter0005.html)

[Logiciels](#chapter0005.html)

[Chapitre 3](#chapter0005.html)

[Configuration du lab](#chapter0005.html)

[CONFIGURATION DU POINT D’ACCÈS](#chapter0005.html)

[Chapitre 4](#chapter0006.html)

[Wi-Fi HACKING... NIVEAU : 0](#chapter0006.html)

[Chapitre 5](#chapter0006.html)

[Anatomie du réseau : wireshark](#chapter0006.html)

[Real hacking !](#chapter0006.html)

[Chapiter 6](#chapter0006.html)

[Wi-Fi hacking... niveau : 1](#chapter0006.html)

[Dévoiler les SSID cachés](#chapter0006.html)

[Bypasser le filtrage MAC](#chapter0006.html)

[Chapiter 7](#chapter0006.html)

[WLAN ET CHIFFREMENT](#chapter0006.html)

[WIRED EQUIVALENT PRIVACY (WEP)](#chapter0006.html)

[Chapitre 8](#chapter0006.html)

[ATTAQUER LE COTÉ CLIENT](#chapter0006.html)

[Attaque honeypot](#chapter0006.html)

[Attaque de l’homme du milieu (MITM)](#chapter0006.html)

[ATTAque EVIL TWIN  (jumeau maléfique)](#chapter0006.html)

[sslstrip : adieu le cryptage !](#chapter0006.html)

[KRACK ATTACK](#chapter0006.html)

[Chapiter 9](#chapter0006.html)

[WPS CRACKING](#chapter0006.html)

[REAL HACKING !](#chapter0006.html)

[Chapiter 10](#chapter0006.html)

[attaque  par dénie de service (Dos)](#chapter0006.html)

[Chapiter 11](#chapter0006.html)

[Maintenir l’accès](#chapter0006.html)

## Disclaimer

Toute action ou activité liée au contenu de ce livre relève de votre entière responsabilité. L'usage abusif des informations contenues dans ce livre peut donner lieu à des poursuites pénales contre les personnes en question, donc veillez à créer un environnement propice afin de tester les connaissances que je vais vous présenter dans ce livre. Et surtout, n’hésitez pas : Virtualbox est à votre disposition.

Une autre chose importante : les connaissances fournies dans ce livre ne sont pas garanties et ce domaine est en évolution continue. Donc si vous trouvez que certaines informations ne sont plus valables, n’hésitez pas à me le signaler en me contactant. Je serais ravi de corriger ce qui est nécessaire et de vous remercier par la même occasion.

Ma chaîne YouTube : youtube.com/HackinGeeK

Mon site web : https://hackingeek.com/

Mon adresse e-mail : anass@hackingeek.com

Notre page Facebook : hackingeek0x/

#### Introduction

![image](Images/image-4RML5381.png)

Un pirate qui arrive à pénétrer un réseau, quel qu’il soit : le réseau d’une entreprise, d’une banque, ou d’une organisation gouvernementale a de lourdes conséquences, car tout simplement, le réseau est en sa possession.

Et avec l’augmentation exponentielle des réseaux sans fil (Wi-Fi) et leur omniprésence dans notre vie quotidienne ainsi que la simplicité qu’ils apportent à notre façon de traiter l’information et de la partager, les hackers travaillent avec acharnement pour les sécuriser. De l’autre côté, l’on a aussi les black hat qui font de leur mieux pour les exploiter.

Il existe plusieurs attaques efficaces contre les réseaux Wi-Fi, qui cependant, causent le vol de données, l’intrusion des réseaux, des dénis de service et beaucoup d’autres attaques.

Cette approche d’attaque et de défense contre le bien et le mal (entre hackers et pirates) est éternelle et il n’y a aucun moyen de s’en débarrasser. En revanche, la seule solution que je te propose dans ce livre afin de diminuer les risques au maximum est : le savoir.

Malheureusement, même un script kiddie peut exécuter ces attaques en utilisant des outils preinstallés sur Kali Linux sans connaître le fonctionnement interne de ces outils-là (et c’est pour cette raison que l’on les appelle “script kiddies”).

Cependant, ce que nous allons faire ensemble dans ce livre, c’est  comprendre le fonctionnement des réseaux (en simplifiant les concepts le plus possible). Nous allons également apprendre à exploiter leur vulnérabilité afin de mieux se défendre contre les pirates.

En tant que hacker, tu dois disposer d’un savoir approfondi sur les réseaux (dont le Wi-Fi), les stratégies d’attaque et de défense, car c’est notre arène et notre combat !

Wi-Fi HACKING avec KALI LINUX est destiné au débutant hacker dans le but de l’aider à comprendre les failles communes des réseaux Wi-Fi et comment procéder un test d’intrusion pour les exploiter. J’ai veillé à ce que le livre soit un guide étape par étape couvrant la théorie et la pratique.

## Pourquoi kali linux ?

J’ai choisi Kali comme OS de démonstration pour plusieurs raisons :

●  C’est la distribution Linux la plus populaire dans le domaine de la sécurité informatique et du hacking

●  Distribution open source

●  Presque tous les outils que nous allons utiliser sont disponibles par défaut sur Kali

## Ce dont tu as besoin pour suivre ce livre

●  Un cerveau humain

●  Une compréhension des concepts de base des réseaux (protocole TCP, IP, MAC, paquet...)

●  Un laptop pour l’utiliser comme machine de l’attaquant.

●  Un dispositif supportant le Wi-Fi pour l’utiliser comme machine victime. Je vais utiliser mon smartphone comme machine victime.

●  Un adaptateur Wi-Fi qui supporte le mode moniteur (injection de paquets)

●  Une passion pour les systèmes Linux  

### Chapitre 2

![image](Images/image-4RML5381.png)

### préparation du lab

Il est essentiel de rester dans le cadre de la loi.

En tant que white hat hacker tu dois obligatoirement avoir un laboratoire sur lequel tu as un contrôle et une liberté d’exercer.

Dans cette partie, nous allons créer un environnement de test Wi-Fi propice. De cette façon, tu peux appliquer les attaques au fur et à mesure de notre avancement dans le livre.

Voici ce que nous allons voir :

›  Préparation du matériel et du logiciel

›  Lancement de Kali Linux

›  Configuration du point d’accès

## Matériel

Pour exercer avec moi, tu auras besoin de :

◆  Un laptop avec un minimum de 4Gb de RAM et 2.2Ghz de CPU, doté d’une carte réseau interne

◆  Un adaptateur Wi-Fi : indispensable pour appliquer les attaques sur les réseaux sans fil. Cependant, il faut avoir un adaptateur qui supporte l’injection de paquets (nous allons voir plus tard de quoi il s’agit). Idéalement, opte pour l'alfa awus036h ou le TP-link-WN722N qui sont tous les deux supportés par Kali

![awus036h-carte-wifi-usb-alfa-network-1000-mw-et-antenne-5-dbi](Images/image-4M59MCK8.png)

––––––––

◆  Un point d’accès : n’importe quel point d’accès qui supporte le chiffrement  WEP/WPA/WPA2 fera l’affaire. Personnellement, je vais utiliser celui-là :

![Huawei-B310-Main](Images/image-09QPUBL8.jpg)

#### Logiciels

En ce qui concerne le software tout ce dont tu auras besoin c’est :

[D’une image de Kali Linux : si tu n’utilises pas Kali comme sytème d'exploitation primaire, il suffit de télécharger le fichier ISO depuis le site officiel et de le lancer comme machine virtuelle avec VirtualBox](https://www.kali.org/downloads/)

[De VirtualBox : un logiciel qui te permet de virtualiser Kali Linux si tu ne veux pas l’installer ou le lancer depuis un disque d’amorçage](https://www.virtualbox.org/wiki/Downloads)

Pour installer VirtualBox, il suffit de télécharger l’exécutable depuis le site officiel et de l’installer (installation standard).

Si tu es un Linuxien, tu peux l’installer avec la commande suivante :

![image](Images/image-WLWKPUON.png)

root@kali:~# sudo apt-get install virtualbox

![image](Images/image-0Y16SR3H.png)

#### Chapitre 3

![image](Images/image-4RML5381.png)

#### Configuration du lab

### Lancement de  kali :

Voyons maintenant comment lancer Kali.

Il y a plusieurs façons de le faire :

›  La première façon est de l’utiliser comme machine virtuelle : télécharge l’image depuis le site officiel de Kali. Cette image est préconfigurée, donc double-clique dessus et Kali sera lancé

›  La deuxième méthode est de booter Kali depuis un flash disque. Cette méthode est intéressante pour ceux qui n’ont pas de matériel assez puissant pour lancer Kali en virtuel.

Dans le deuxième cas, télécharge le fichier ISO et brûle-le sur un flash disque de 8Gb d’espace (minimum) en utilisant un logiciel comme Linux USB creator (pour Windows) ou Rosa (pour GNU/Linux), puis redémarre ton PC et, avant de booter, appuie sur la touche qui te permet de choisir ton flash disque comme plateforme d’amorçage.

CONFIGURATION DU POINT D’ACCÈS

Allume ton point d’accès car nous allons réaliser quelques modifications sur sa configuration afin de clarifier quelques concepts.

Connecte ton routeur en entrant son adresse IP dans le champ de recherche de ton navigateur. Tu trouveras l’adresse IP et les paramètres de connexion dans le manuel d’utilisation ou sur le site officiel du fabricant.

![192.168.8.1](Images/image-DR9WK0Q2.png)

Une page de login (ou pop-up) s’affiche. Le nom d’utilisateur et le mot de passe varient en fonction du fabricant du routeur.

Dans mon cas, c’est admin : admin :

![pop-up_login](Images/image-PVBM9500.png)

Fais une petite balade et découvre les différentes configurations afin que tu t’habitues à cette même interface.

Ce qui nous intéresse maintenant, c’est de changer le SSID (le nom du réseau Wi-Fi) à “Pentest-Lab” et de désactiver le chiffrement (Wi-Fi ouvert) :

![pentest-lab](Images/image-TNU5835H.png)

Sauvegarde les changements effectués, et redémarre le routeur afin de les appliquer.

Vérifie ton network manager pour voir si les modifications ont été appliquées avec succès :

![network-manaer-pentest-lab](Images/image-QRN5JLEK.png)

La raison pour laquelle nous avons mis le point d’accès en mode “ouvert”, c’est pour t’initier à quelques concepts fondamentaux concernant les reseaux.

Au fur et à mesure de notre progression, nous allons augmenter le niveau de sécurité, étudier ses points forts et ses points faibles puis l’exploiter.

### CHAPITRE 4

![image](Images/image-4RML5381.png)

### Wi-Fi HACKING... NIVEAU : 0

#### Connexion au point d’accès

Après avoir préparé notre environnement de test, voyons voir comment nous pouvons connecter notre carte réseau externe avec le point d’accès via le terminal (ligne de commande).

L’avantage d’utiliser les cartes réseaux sus-citées (notamment la alfa awus036h), c’est qu’elles sont supportées par Kali avec des périphériques préinstallés, ce qui veut dire que tu dois juste brancher ta carte et tu seras prêt.

Tout d'abord, je vais te montrer quelques commandes qui te seront utiles lors de la configuration de ton adaptateur en ligne de commande.

La première commande que tu dois connaître est ifconfig :

![ifconfig](Images/image-K74J8EZY.png)

Comme tu peux le voir, wlx00e04c8e263e est l’interface Wi-Fi que mon système a créé pour ma carte alfa.

Pour étudier ses détails séparément, entre la commande ifconfig suivie du nom de l’interface :

![ifconfig_interface](Images/image-G59VO1AT.png)

Tu peux voir l’adresse MAC de la carte et la comparer avec celle qui est marquée sur le dos de la carte (pour t’assurer que tu as une carte originelle et non pas une copie). Puisqu'elle n’est pas encore connectée à un réseau, il n'y a pas grand chose à expliquer.

Tout d’abord, voyons les réseaux Wi-Fi que notre carte alfa a pu détecter. Pour cela, entre la commande iwlist “interface” scanning et tu auras la liste des réseaux qui sont à portée de votre antenne :

![iwlist](Images/image-27IIQPSM.png)

Fais défiler les résultats vers le bas et tu devrais apercevoir notre point d’accès “Pentest-Lab” dans le champ ESSID :

![iwlist_pentstlab](Images/image-D40OP0L8.png)

Ensuite, pour connecter à notre réseau “Pentest-Lab” nous devons exécuter la commande :iwconfig “interface” essid “Pentest-Lab”, ou tout simplement via notre network-manager :

![iwconfig_connect](Images/image-FA818HP7.png)

Bien. Maintenant, assure-toi que le DHCP t’a attribué une adresse IP en exécutant la commande ifconfig :

![ifconfig_alfa](Images/image-OVANGCO1.png)

Ifconfig nous permet d’avoir les informations suivantes :

Inet_addr est l’adresse IP de notre machine dans le réseau “Pentest-Lab”

Bcast est l’adresse de diffusion du réseau, autrement dit, si une machine dans un réseau veut diffuser une information qui intéresse toutes les machines connectées au même réseau, elle va l’envoyer à cette adresse

Mask est l’adresse qui nous permet de classer un réseau selon son nombre d’hôtes. Dans notre cas le réseau peut accepter jusuqu’à 254 hôtes

Dernière chose, vérifie la connexion entre toi et le routeur en envoyant des paquets ICMP avec la commande ping :

![ping](Images/image-WQF27AMQ.png)

Comme tu peux le voir, la connexion s’est bien établie.

Le petit échauffement pour te préparer aux chapitres qui vont suivre est terminé.

Nous allons maintenant entamer les choses sérieuses : comprendre le fonctionnement du réseau dans le but de révéler ses vulnérabilités et les exploiter.

Now, let’s the hack begin !

#### ‘IN ORDER TO KEEP UP

#### AND BE RELEVANT, YOU

#### HAVE TO WORK HARD’

Ming Chow

##### Chapitre 5

![image](Images/image-4RML5381.png)

##### Anatomie du réseau : wireshark

Nous venons de désactiver le cryptage de notre point d’accès, ce qui fait que toutes les communications entre les utilisateurs et le routeur ne seront pas cryptées. N’importe quel hacker (ou pirate) peut sniffer le réseau et avoir les informations échangées entre le routeur et les clients avec la carte réseau adequate.

#### Wireshark, kesako ?

Wireshark est un analyseur de paquets libre et gratuit qui nous permet de lire et d’enregistrer les paquets circulant dans un réseau donné. Il est principalement utilisé dans le dépannage de réseaux et le développement de protocoles.

Cependant, ce qui nous intéresse en tant que hackers, c’est de sniffer le réseau pour récolter le plus d’informations.

Note aussi que tu peux accomplir le même objectif en utilisant d’autres outils tels que tcpdump ou encore tashark. Néanmois, sache que wireshark est le plus populaire des analyseurs de paquets.

#### Le mode moniteur

La première chose à faire avant d’entamer notre attaque, c’est de créer une interface en mode moniteur. Ce mode va nous permettre de capturer et lire tous les paquets dans notre champ aérien. L’on appelle plus communément ce mode “le mode promiscous".

Pour mettre notre carte dans le mode moniteur, nous aurons besoin de l’utilitaire airmon-ng. Exécute la commande airmon-ng pour vérifier que la carte est toujours disponible :

![airmon-ng](Images/image-B9UE42WK.png)

Ensuite, pour commuter vers le mode moniteur, entre la commande airmon-ng start “interface”. Cela va faire en sorte que le mode change en mode moniteur et que le nom de l’interface change également :

![wlanmon0](Images/image-J8TCTNWE.png)

Comme tu le vois dans la capture ci-dessus, le nom de la carte s’est transformé en wlan0mon. Tu peux confirmer avec la commande iwconfig :

![iwconfig_monitor](Images/image-62RMOVUV.png)

Bien. Nous sommes maintenant prêts à balayer l’air (haha !).

Note :  Dans le cas où tu as un adaptateur autre que alfa awus036h, exécute la commande suivante afin de t’assurer qu’il supporte l’injection de paquets :

![image](Images/image-LCZX4EAH.png)

root@kali:~# aireplay-ng -9 “interface-monitor”

![image](Images/image-W7O0E9VR.png)![injection](Images/image-KUSTH7RS.png)

Il arrive que certains processus empêchent de mettre la carte réseau en mode moniteur. Dans ce cas present, tu dois TUER ces processus avec la commande suivante :

![image](Images/image-NUSAJRR4.png)

root@kali:~# airmong-ng check kill

![image](Images/image-I3A7R2Q6.png)

Pour réactiver ces processus, il suffit d’exécuter ces commandes :

![image](Images/image-QHYJP407.png)

root@kali:~# service networking restart

root@kali:~# service network-manager restart

![image](Images/image-QZGH1N6D.png)

#### Sniffer le réseau

Lance wireshark en entrant wireshark dans le terminal :

![wireshark](Images/image-2MM9A2KN.png)

Note : wireshark met par défaut les interfaces réseaux en mode promiscous.

Une fois wireshark lancé, double-clique sur le nom de ton interface pour commencer la capture. Tu verras un tas d’informations défiler sur ton écran comme suit :

![wireshark-sniff](Images/image-U9OZAII5.png)

Tous ces paquets sont des informations qui circulent en permanence autour de nous. Notre carte peut les capturer et les présenter sous une forme lisible.

L’interface de wireshark est assez intuitive. En effet, le champ des résultats, tu peux voir que l’on dispose de la source du paquet ainsi que sa destination, le protocole utilisé dans la communication ainsi que d’autres informations.

Au-dessus, des détails plus avancés sont fournis par wireshark concernant chaque paquet capture. Ce sontt des informations détaillées sur les frames et le modèle OSI de façon générale.

Prête attention aux paquets en bleu. Ce sont des paquets non chiffrés et c’est la raison pour laquelle nous voyons leurs contenus en clair (ce qui n’est pas normal d’ailleurs).

Le grand danger se manifeste quand l’utilisateur visite des sites web qui n’utilisent pas le cryptage SSL. Autrement dit, des sites qui ne sont pas HTTPS, ce qui implique que toutes les communications se passent (même les informations confidentielles).

Voici un exemple : connecte-toi à ton point d’accès “Pentest-Lab”, puis lance wireshark et accede à l’interface de configuration : un nom d’utilisateur et un mot de passe sont exigés pour se loguer :

![router_login](Images/image-O88EN15Q.png)

Maintenant, entre le nom d’utilisateur et le mot de passe puis clique sur connexion.

Reviens à wireshark et arrête la capture, puis filtre les paquets http dans la barre qui est en vert :

![http_filter](Images/image-E5AGBPAM.png)

Les paquets HTTP vont alors apparaître dans le champ de résultats, ce qui va nous faciliter la recherche du paquet contenant le nom d’utilisateur et le mot de passe.

Comme tu le sais, les paramètres entrés précédement sont envoyés par la méthode POST !. Tu peux donc tout de suite identifier le paquet en question.

![admin_admin](Images/image-46JZUGFD.png)

Maintenant, sélectionne le paquet, puis dans le champ en dessous, sélectionne hypertext transfer protocol :

Username et password sur un plateau d’argent !

Tu viens donc de voir les énormes risques de passer à côté du chiffrement Heureusement que la majorité écrasante des sites web utilisent le protocole SSL (HTTPS) dans leurs transferts de données.

Même cela peut être hacké !.

##### Real hacking !

Les aéroports, les hotels et coffee shop sont les grandes victimes de ce type d’attaque. Dans mon livre DARK PYTHON l’on y retrouve la scenario suivant : un hôtel qui dispose d’un point d’accès sans aucun protocole de chiffrement. Le terms et les conditions nous révèlent que le mot de passe est composé de 6 numéros. C’est à nous de jouer !

Voici à quoi ressemble l’interface de login pour accéder à internet :

![rais](Images/image-VG8XOV5W.png)

Tu vois donc qu’il n'y a pas de chiffrement SSL.

La méthode la plus facile est de simplement capturer le mot de passe.

Je lance wireshark puis je filtre les paquets http et j’attends.

Le fait qu’un utilisateur s’authentifie avec le bon mot de passe, wireshark me présente les paquets contenant tous les paramètres d’authentification dont le mot de passe :

![raiswifi](Images/image-7J4BYOOT.png)

Done !

#### Comment se defendre ?

❖  utiliser le chiffrement dans tous les réseaux sans exception

##### Chapiter 6

![image](Images/image-4RML5381.png)

##### Wi-Fi hacking... niveau : 1

##### Dévoiler les SSID cachés

Par défaut, les points d’accès diffusent leur SSID (nom du réseau Wi-Fi) en envoyant des trames nommées “beacons”. Cela permet au dispositive, qui est dans le champ de transmission, de détecter le point d’accès et d’éventuellement se connecter.

Cependant, une des mesures de “sécurité” est de cacher le SSID du point d’accès, impliquant que le routeur ne diffuse plus de trames beacons et que seuls ceux qui connaissent le vrai SSID peuvent s’y connecter.

Voyons voir le cas typique où le point d’accès diffuse son SSID.

Mets ta carte réseau en mode moniteur avec la commande airmong-ng start ‘interface’ puis lance la capture avec wireshark :

![SSID](Images/image-TU1RPAF9.png)

Comme tu peux le voir, le SSID de notre point d’accès est diffusé en clair.

Maintenant, désactive la diffusion SSID depuis l’interface de configuration de ton routeur (la démarche diffère selon le type de point d’accès). Voici la mienne :

![desactivate_ssid](Images/image-7QYZFHYL.png)

Relance la capture, et tu devrais voir que le SSID de ton point d’accès a disparu et est remplacé par le string “Wildcard(broadcast)” comme suit :

![hidden_ssid](Images/image-A2YR1RDA.png)

Dans ce cas-là nous devons provoquer une reconnexion d’un utilisateur légitime avec le point d’accès. Grâce à ce processus, il y aura sûrement un échange de SSID dans le paquet de requête et celui de la réponse.

C’est ainsi que tu vas procéder : avec aireplay-ng, tu vas envoyer des paquets (injections) de désauthentification à toutes les stations du point d’accès “Pentest-Lab” ce qui va déclencher une tentative de reconnexion des dispositifs ayant déjà reconnu le vrai SSID.

Voici la commande à utiliser :

![image](Images/image-NO6S3N7G.png)

root@kali:~# aireplay-ng -0 10 -a <AP MAC> <interface>

![image](Images/image-237A2M9B.png)

›  -0 : pour la désauthentification

›  10 : nombre de paquets à injecter dans le réseau.

›  -a <AP MAC> : l’adresse MAC du point d’accès

![aireplay-ng](Images/image-FW1ZGRV6.png)

Cela va forcer la déconnexion des hôtes déjà connectés.

Ensuite, et d’une manière automatique, il y aura une tentarive de rétablir la connexion avec le point d’accès en envoyant le SSID (qui sera non-chiffré). Notre carte en mode moniteur le capture immédiatement.

![ssid_trouvé](Images/image-OOJXPX6H.png)

Utilise le filtre “wlan,bssid == MAC” afin de faciliter la recherche.

Tu viens de voir que même si le SSID du point d’accès n’est pas diffusé (pas visible) et que même si les communications ne sont pas chiffrées, nous avons réussi à capturer le SSID sans aucune difficulté.

##### Bypasser le filtrage MAC

L’adresse MAC (Media access control) est un identifiant physique unique stocké dans chaque carte réseau.

En se basant sur l’unicité de cet identifiant, l’on a créé un mécanisme de défense basé sur le filtrage des adresses MAC.

L’administrateur du réseau va créer, au niveau de la configuration du point d’accès, une liste de MAC adresses autorisées (ou interdites) à se connecter. Ainsi, à chaque fois, un dispositif envoie une requête d’authentification au point d’accès. Ce dernier va juger l’authentification en se basant sur la liste des MAC autorisés.

Par définition, l’adresse MAC doit être unique et ne peut pas être modifiée par l’utilisateur. Néanmoins, ce n’est pas réellement le cas.

Pour commencer, configurons notre routeur pour qu’il n’accepte qu’une seule adresse MAC (celle de mon smartphone).

Rends-toi sur l’interface de configuration et entre une (ou plusieurs) adresse MAC autorisée :

![MAC_router](Images/image-78BDRR2W.png)

Maintenant, seul mon smartphone est autorisé à se connecter au routeur, et toute autre requête (avec MAC différée) est rejetée.

Pour battre cette barrière de défense, nous devons sniffer.

En utilisant airodump-ng, on peut trouver les adresses MAC qui sont connectées (et donc autorisées) au point d’accès. Voici la commande à utiliser :

![image](Images/image-NDGPKX35.png)

root@kali:~# airodump-ng -c <channel> -a—bssid <mac> “interface-mon”

![image](Images/image-RXZPDYD8.png)

Où :

›  -c : pour définir le canal du point d’accès

›  -a—bssid : pour définir l’adresse MAC du point d’accès

›  Interface-mon : ta carte réseau en mode moniteur

Et si je ne connais ni le canal ni l’adresse MAC du point d’accès ?

Très bonne question !

Pour récupérer l’adresse MAC du point d’accès ainsi que le canal dans lequel il est actif, il suffit d’utiliser une simple commande qui fera tout le travail pour nous, la voici :

![image](Images/image-CIO5LXMM.png)

root@kali:~# airodump-ng “interface-monitor”

![image](Images/image-OER7O58N.png)![airodump-ng](Images/image-4WSQSCR1.png)

Comme tu peux le voir, en capturant les paquets circulant autour de moi, j’ai pu récupérer les informations suivantes :

›  Le réseau cible : “Pentest-Lab”.

›  Le BSSID du réseau cible : c’est l’adresse MAC du point d’accès “Pentest-Lab”.

›  Le numéro du canal : “6”

Maintenant, pour révéler les utilisateurs connectés au point d’accès exécute la commande suivante :

![image](Images/image-JGEICGX9.png)

root@kali:~# airodump-ng -c <canal> -a—bssid <mac> “interface”

![image](Images/image-LXRL7JFV.png)

Exemple :

![image](Images/image-5ZF1IY8W.png)

root@kali:~# airodump-ng -c 1 -a—bssid 00:9A:CD:2E:DE:7A wlan0mon

![image](Images/image-2QF167J5.png)![doogee_airodump](Images/image-4IETEJZZ.png)

Une fois l’adresse MAC autorisée est repérée, nous pouvons spoofer notre MAC adresse (si si, on peut !) en utilisant l’outil macchanger qui est installé par défaut sur Kali.

D’abord, désactive l’interface réseau avec la commande (sinon, les changements ne peuvent pas être appliqués) :

![image](Images/image-60STII76.png)

root@kali:~# ifconfig “interface” down

![image](Images/image-YG1CSFKC.png)![ifconfig_down](Images/image-51TGZ1WD.png)

Puis spoof l’adresse MAC connectée au point d’accès :

![image](Images/image-8LXY47V3.png)

root@kali:~# macchanger -m <MAC> “interface”

![image](Images/image-HV76LVE3.png)![MACCHANGER](Images/image-L87QROC3.png)

Maintenant, réactive l’interface avec la commande :

![image](Images/image-2KCDXCVF.png)

root@kali:~# ifconfig wlan0mon up

![image](Images/image-PGKUL4S2.png)

Voilà, tu disposes d’une toute nouvelle adresse MAC qui te permettra de te connecter au point d’accès le plus normalement possible.

Note : Pour éviter les problèmes de collision avec d’autres utilisateurs essayant de se reconnecter, utilise aireplay-ng pour couper toute tentative de connexion (cf. le chapitre Dos attaque). À toi de jouer !

Cette méthode est aussi valable pour les réseaux sans fil cryptés (WEP, WPA...). Le raisonnement est donc le même.

#### Comment se defendre ?

❖  Comme tu peux le constater, l’utilisation de ce type de filtrage n’offre presque aucune protection réelle à un réseau sans fil.

#### “IF YOU WANT SOMETHING

#### TO HAPPEN, YOU DON’T

#### NEED TO WAIT FOR

#### PERMISSION”

Ian Coldwater

##### Chapiter 7

![image](Images/image-4RML5381.png)

##### WLAN ET CHIFFREMENT

Comme tu dois le savoir, les WLANs (Wireless local area network) transmettent les données par voie aérienne, et au vu de leur sensibilité aux écoutes clandestines, il est devenu indispensable de créer une solution afin de renforcer la sécurité de ces mêmes réseaux.

IEEE 802.11 est un ensemble de normes qui concerne les réseaux sans fil locaux (Wi-Fi). Ce comité, en s’appuyant sur la cryptographie, a créé des protocoles afin de renforcer la sécurité des WLANs. Les voici :

›  Wired equivalent privacy (WEP)

›  Wi-Fi protected access (WPA)

›  Wi-Fi protected access version 2 (WPA2)

Dans ce chapitre, nous allons voir les points faibles de ces protocoles de cryptage et les différentes façons de les exploiter.

##### WIRED EQUIVALENT PRIVACY (WEP)

Il est apparu en 1999 et a été cracké en 2000\. De ce fait, l’on a tendance à le nommer “Weak encryption protocole”.

Il existe plusieurs faiblesses dans ce protocole que l’on ne va cependant pas détailler ici, carcela requiert des connaissances approfondies en mathématiques.

WEP n’a pas été conçu pour être un protocole de confidentialité. Cependant, nous allons voir comment briser ce cryptage en utilisant des outils disponibles sur Kali.

La faille majeure de ce protocole étant son utilisation des IVs (Initialisation verctor). Voici en quoi cela consiste : quelle que soit la taille de la clé, dans tous les cas, 24 bit seront alloués aux IVs. Le problème est que ces mêmes IVs contiennent des informations sur le restant de la clé de chiffrement.

Ainsi, pour trouver la clé, il suffit de capturer un nombre suffisant de paquets puis de les soumettre à un traitement adéquat afin de récupérer la clé.

Pour démontrer l’attaque, change la configuration de ton point d’accès à WEP et mets une clé de ton choix :

![XEP](Images/image-EOAH523S.png)

Maintenant, tu vas être déconnecté du réseau ainsi qu’à tous les autres dispositifs connectés. Dès maintenant, tu dois t’authentifier avec la clé définie précédemment :

![WEP_AUTHENTICATION](Images/image-EKJ3O91C.png)

Jusque-ici, tout se passe bien.

Commençons maintenant notre attaque

Tout d’abord, mets ton adaptateur en mode moniteur :

![image](Images/image-56JTM2UD.png)

root@kali:~# airmon-ng start “interface”

![image](Images/image-4VR3QTSA.png)![airmong-ng_WEP](Images/image-OHBKZWVS.png)

Jete un coup d’œil sur ce qui se passe autour de toi pour capturer les paramètres dont nous aurons besoin  :

![airodump-WEP](Images/image-DORFRBJ4.png)

Oups ! Je viens de découvrir qu’il n’y a pas que mon lab qui est sous WEP ! Tu vois donc que même en 2019, ces zombies existent toujours, mettant tout le réseau en danger, car cette attaque n’est pas compliquée à exécuter au point qu’un script kiddie peut le faire (je ne parle pas de toi bien sûr, haha !). Je vais essayer de résister à la tentation de le cracker.

Attention : dans certains cas, l’on utilise des protocoles obsolètes afin de créer des pièges pour les pirates. L’on appelle ce ces pièges “honeypot” (littéralement, “pot de miel”)

Deuxième étape, tu dois capturer un nombre suffisant de paquets avec airodump-ng et les stocker dans des fichiers intitulés “WEP_HACK” pour les crackers en offline. Pour cela, utilise la commande suivante :

![image](Images/image-Q5OJ5ZZ4.png)

root@kali:~# airodump-ng—bssid <AP MAC>—channel <canal>—write WEP_HACK “interface-monitor”

![image](Images/image-HWKWC67I.png)![airodump-ng_capture_WEP](Images/image-0CRYZZIV.png)

En exécutant cette commande, tu viens de démarrer la capture de paquets. Cependant, afin que l’on parvienne à notre objectif, il faut capturer une quantité suffisante de données chiffrés avec la même clé.

Dans le cas où tu stagnes, tu peux forcer le réseau à produire plus de paquets avec aireplay-ng vus précédemment :

![image](Images/image-U02SHTT3.png)

root@kali:~# aireplay-ng -3 -b <AP MAC> -h <CLIENT MAC>—ignore-negative-one wlan0mon

![image](Images/image-4VJXXWA4.png)

Voici l’explication des arguments utilisés :

›  -3 : pour le ARP replay

›  -b : l’adresse MAC du point d’accès

›  -h : l’adresse MAC d’un client connecté au réseau

›  —ignore-negative-one : pour éviter les problèmes de canal

›  wlan0mon : adaptateur en mode moniteur

Une fois cette commande exécutée, tu vas constater une augmentation considérable dans la quantité de #Data reçus :

![aireplay-ng_WEp](Images/image-CA947158.png)

Let’s the hack begin !

Laisse ces deux terminales faire leur travail et ouvres-en un troisième pour cracker la clé avec airckrack-ng.

En s’appuyant sur les paquets captures qui sont dans les fichiers WEP_HACK*, airckrack-ng peut (tout en étant en mode hors ligne) récupérer facilement la clé juste en exécutant la commande suivante :

![image](Images/image-SY0X4ZB2.png)

root@kali:~# aircrack-ng WEP_HACK-0*

![image](Images/image-656JICPI.png)

Note : les fichiers WEP_HACK sont dans le même chemin où tu as lancé airodump-ng.

––––––––

![WEP_FOUND](Images/image-QVIAFA2Y.png)

Voilà, en une fraction de seconde, il a pu cracker la clé.

Dans cette partie dédiée au hacking d’une clé WEP, nous avons vu que le WEP est très facile à cracker, peu importe la complexité de la clé, et que ce processus ne demande que quelques minutes, le temps de capturer suffisamment de paquets contenant les IVs.

Et le plus important, c’est que nous avons vu que le WEP est toujours vivant !

#### Comment se défendre ?

❖  Ne jamais utiliser le protocole WEP

#### Wi-Fi protected access(WPA)

Le protocole WPA utilise principalement le cryptage TKIP. Il a été créé dans le but de renforcer le protocole WEP que nous avons vu précédemment sans apporter de changements aux infrastructures des réseaux.

Tandis que le WPA2 (deuxième version de WPA) est basé sur l’utilisation de l’algorithme AES-CCMP pour le cryptage de données, ce qui est plus puissant par rapport au TKIP.

Cependant, tous les deux permettent l’authentification basée sur EAP en utilisant des clés prépartagées, des PSK (personnel) ou bien des serveurs RADIUS (entreprise).

Heureusement (ou malheureusement), WPA/WPA2 est vulnérable à l’attaque par dictionnaire. Tout ce dont tu as besoin pour mener l’attaque est :

›  Le four-way handshake (paquets échangés pour établir la connexion entre un client et un point d’accès sous WPA en passant par 4 étapes)

›  Un dictionnaire robuste qui contient les mots de passe fréquemment utilisés ou que tu juges être utilisés par ta cible après avoir fait la collecte d’informations

›  Un outil comme airckrack-ng qui va tenter de casser le WPA/WPA2 passphrase (phrase secrète)

Voici un schéma illustrant le mécanisme d’échange de données dans le protocole WPA :

![fourwayhandshake](Images/image-RDDVEICE.png)

›  Étape 1 : le point d'accès envoie un nombre aléatoire au client : c'est le ANonce

›  Étape 2 : le client crée un autre nombre aléatoire appelé “SNonce”. La combinaison de SNonce+ANonce+le mot de passe entré par l'utilisateur crée ce qu'on appelle MIC (Message integrity check). Le MIC et SNonce sont envoyés au point d'accès.

›  Étape 3 : le point d'accès hash le ANonce, SNonce et le mot de passe et si ça fonctionne, le client sera authentifié et va envoyer la clé chiffrée

›  Étape 4 : le client accepte la clé de chiffrement

Tu vas cependant me dire “comment la clé de prépartage est créée ?”

Bonne question. En fait la clé de prépartage est la combinaison entre le WPA-passphrase (fourni par l’utilisaeur) et le SSID (nom du réseau Wi-Fi), le résultat étant envoyé sous forme de PBKDF2 (Password -based key derivation function) qui forme une clé de 256-bit .

Les choses vont maintenant se corser...

Tout ce qui nous intéresse en tant que pentesters (hackers) est le four-way handshake, autrement dit ces 4 messages dessinés sur le schéma.

Aicrack-ng va dériver la clé prépartagée 256-bit de chaque mot contenu dans notre dictionnaire puis l’utiliser avec les paramètres que nous avons pu capturer pour créer le PTK (Pairwise transient key). Ce dernier va être utilisé pour vérifier le MIC (Message integrity check) dans l’un des paquets du handshake. Si cela correspond, le mot de passe du dictionnaire est correct.

Voici un schéma qui simplifie le processus de l’attaque :

![sheemaa_WPA](Images/image-24UI16S9.png)

Voyons voir comment le faire d’un point de vue pratique.

Comme d’habitude, pivote vers le mode WPA dans la configuration de ton point d’accès, puis mets “manchester” comme mot de passe :

![manchester](Images/image-6JYF7EUJ.png)

Commence la capture de paquets avec airodump-ng en redirigeant les outputs vers des fichiers nommés “WPA_HACK” avec la commande :

![image](Images/image-H96CCB49.png)

root@kali:~# airodump-ng—bssid <AP MAC>—channel <numéro du canal>—write WPA_HACK “interface-monitor”

![image](Images/image-49P721LH.png)![wpa_airodump](Images/image-7T2TQQ01.png)

Et on commence la capture :

![wpa_capture](Images/image-KVKTFRF1.png)

Très bien. Maintenant nous avons besoin du 4-way handshake. Comme expliqué plus haut, ces paquets sont échangés au moment d’établir la connexion entre l’utilisateur et le point d’accès. Cependant, nous sommes en présence (dans la capture ci-dessus) avec des clients déjà connectés.

Pour forcer une reconnexion, nous allons devoir désauthentifer les clients avec aireplay-ng.

![image](Images/image-YYGRN9MD.png)

root@kali:~# aireplay-ng—deauth 10 -a <AP MAC> “interface-monitor”—ignore-negative-one

![image](Images/image-E23HXZS2.png)

Ou :

›  —deauth 10 : envoyer 10 requêtes de désauthentification

![wpa_deauthentication](Images/image-6SNQX33H.png)

Une fois le 4-way handshake capture, tu auras une indication en haut du terminal suivie du BSSID du point d’accès cible (comme le montre la capture ci-dessus).

Arrête airodump-ng et ouvre le fichier WPA_HACK-01.cap avec wireshark. Voici les paquets que nous sommes en train de chercher :

![WPA_HACK_CAP](Images/image-5RVJ9SBG.png)

Les paquets que airckrack-ng aura besoin pour cracker le passphase sont en vert.

Dans cette attaque, sache que toi-même tu es aussi bon que ton dictionnaire.

Bien sûr, Kali met à notre disposition une multitude de wordlists destinées aux attaques de brute force dont le fameux rockyou.txt et d’autres dictionnaires propres à Metasploit, mais souvent tout ne se déroule pas comme prévu.

L’intrusion d’un réseau fait partie d’un test d’intrusion mené par un expert en sécurité. Cela veut donc dire que cracker le passphrase n’est qu’une étape précédée et suivie par d’autres étapes et qui vont au final permettre de compromettre un système.

Cela dit, tu comprends que c’est une mauvaise idée d’effectuer ce genre d’attaque avec n’importe quel dictionnaire sur n’importe quelle cible parce que ça varie.

En effet, un réseau qui appartient à un ingénieur en sécurité informatique n’aura pas le même “style” de mot de passe qu’un réseau d’un médecin (et je pense que tu es d’accord avec moi sur ce point).

Donc, veille à récolter le maximum d’informations sur ta cible. C’est d’ailleurs une étape cruciale pour la réussite de tout test d’intrusion que tu entameras.

Par exemple : j’ai imaginé que l’admin du réseau “Pentest-Lab” est un fan de Manchester, car il porte souvent des t-shirts de cette équipe et parce qu’il parle beaucoup des joueurs sur les réseaux sociaux. Je m’assure donc que mon dictionnaire contient ce genre de mots : “football”, “Manchester united”, “Diogo”... etc., bref, un jargon approprié.

Voilà, je pense que tu as compris ce que je veux dire. La quête d’un dictionnaire robuste n’est pas compliquée : une petite recherche sur Google et tu tomberas sur un dictionnaire qui contient 1,5 BILLION de mots.

Note : si tu as une idée précise sur les caractères du mot de passe, tu peux utiliser crunch pour créer tes propres dictionnaires

Let’s go ! En se basant sur le dictionnaire, aircrack-ng va essayer les différentes combinaisons de mots de passe dans le but de cracker la clé. Voici la commande à utiliser :

![wpa_airckrack](Images/image-8C85EWN8.png)

Et si tu es assez chanceux (oui, il faut l’accepter) tu auras une belle vue comme celle-ci :

![WPA_CRACKED](Images/image-YNC9IRMX.png)

Note : les attaques de brute force sont coûteuses en termes de temps et de ressources. Tu peux réduire le temps de l’attaque en augmentant la puissance du CPU effectuant les calculs ou en précalculant le PMK.

#### Comment se défendre ?

❖  Utiliser des mots de passe complexes

#### ‘THERE IS NO PERFECT

#### SECURITY, AND MAKING

#### PERFECTION YOUR GOAL

#### RESULTS IN A BRITTLE

#### SECURITY STRATEGY’

Dan Cornell

##### Chapitre 8

![image](Images/image-4RML5381.png)

##### ATTAQUER LE COTÉ CLIENT

##### Attaque honeypot

Quand tu allumeras ton laptop, il va automatiquement rechercher les réseaux avec lesquels il a déjà été connecté.

Sous Windows, ces réseaux sont stockés dans une liste appelée “PNL” (Preffered network list). De cette façon, dès qu’il reconnaît un réseau (ou plusieurs) il va se connecter avec celui qui dispose du signal le plus fort.

En exploitant ce mécanisme, nous pouvons créer un faux point d’accès avec le même ESSID que le client est en train de rechercher, poussant le client à se connecter à notre machine pensant que c’est le réseau légitime.

Ce type d’attaque est plus communément appelée “attaque Honeypot” (piège).

Let’s see how to do it !

Tout d’abord, je vais déconecter mon smartphone du réseau “Pentest-Lab”, puis m’assurer, avec la commande suivante, qu’il n’y est plus associé :

![image](Images/image-5CTM7U0A.png)

root@kali:~# airodump-ng—bssid <AP MAC>—channel<numero du canal> wlan0mon

![image](Images/image-T8DZG35D.png)![airodump-NOone](Images/image-9HMTO35T.png)

Comme tu peux le constater, aucun dispositif n’est associé au point d’accès “Pentest-Lab”.

L’étape suivante est de créer le faux point d’accès avec l’utilitaire airbase-ng avec un ESSID“Pentest-Lab” :

![image](Images/image-6FXKIIRI.png)

root@kali:~# airbase-ng  -c 3 -e “Pentest-Lab” wlan0mon

![image](Images/image-YHKQUFOA.png)![airbase-ng](Images/image-CMU67J8F.png)

Quelques secondes plus tard, le smartphone est automatiquement associé à mon faux point d’accès (sans avoir d’adresse IP).

––––––––

![airbase-ng-assi](Images/image-10BZ3JXX.jpg)

Parfait. Maintenant, que ferais-tu dans le cas où le client est déjà associé au point d’accès ?

Tu l’as deviné, n’est-ce-pas ?

En effet, tu vas le désauthentifier avec aireplay-ng.

Voyons un exemple concret.

Arrête le faux point d’accès et connecte ta machine victime au point d’accès légitime.

Une fois fait, recrée le faux point d’accès avec la commande précédente et attends un petit moment :

![airbase-ng](Images/image-CMU67J8F.png)

Rien ne se passe ! Pourtant le signal du faux point d’accès est plus fort que celui du vrai point d’accès.

Effectivement, car le client a établi la connexion avec son point d’accès, et si tu souhaites détourner ce mécanisme tu n’as qu’à le désauthentifier.

Voici la commande que je vais utiliser pour envoyer une boucle infinie de messages de désauthentification, laissant au client aucune chance de reconnexion :

![image](Images/image-3MF3XPW4.png)

root@kali:~# aireplay-ng—deauth 0 -a <AP MAC>—ignore-negative-one wlan0mon

![image](Images/image-0XCEMK8N.png)![airbase-and-airepaly](Images/image-6DI93UOI.png)

Et voilà !

Nous avons pu forcer le client à se connecter à notre faux point d’accès.

Note : le client n’aura pas d’adresse IP tant que notre DHCP et le pare-feu ne sont pas configures.

##### Attaque de l’homme du milieu (MITM)

L’attaque de l’homme du milieu est l’une des attaques les plus répandues et les plus puissantes sur les réseaux WLANs.

Cette attaque peut prendre plusieurs forms. Nous allons cependant voir ensemble uniquement la forme la plus commune :

Le hacker est connecté à Internet à l’aide d’un réseau local filaire. En utilisant son adaptateur externe, il va créer un faux point d’accès (Rogue Acess point), puis relier les deux interfaces (filaire et non filiare).

Le faux point d’accès diffuse un SSID identique à celui auquel la victime sera connectée (ou déjà connectée).

Voyons voir comment nous pouvons effectuer cette attaque dans notre propre lab.

![74c4193e-b33e-41e2-921a-6f2916e9075b (2)](Images/image-LHIH9P8H.png)

Optimisons un peu l’attaque de la partie précédente en ajoutant une configuration qui permet au client d’obtenir une adresse IP et de pouvoir se connecter à Internet le plus normalement possible.

Crée un faux point d’accès avec le même ESSID que celle de ta cible :

![image](Images/image-2WD52B26.png)

root@kali:~# airbase-ng -e “Pentest-Lab” -c 10 wlan0mon

![image](Images/image-BTFPDNUW.png)![at0](Images/image-XYPX1XCH.png)

Comme tu peux le voir, airbase-ng a crée une interface virtuelle at0. C’est en quelque sorte l’interface filiaire de notre point d’accès créé par airbase-ng.

![ifconfig_at0](Images/image-XW1LNJZ9.png)

Pour que le client puisse connecter à Internet, il va devoir passer par le routeur, autrement dit, il me faut (en tant que hacker) relier l’interface at0 créée par airbase-ng avec l’interface filiaire de mon routeur. C’est tout simplement un pont de trafic.

La première chose à faire est de brancher le câble RJ45 à ton routeur, car l’on ne peut pas ponter deux interfaces sans fil. C’est, en revanche, faisable avec une interface filiaire et une non-filiaire.

Voici la succession de commandes à utiliser pour appliquer ce concept de pontage :

![image](Images/image-9KDK9H6J.png)

root@kali:~# apt-get install bridge-utils

root@kali:~#  brctl addbr PentestLab-bridge

root@kali:~#  brctl addif PentestLab-bridge enp0s10

root@kali:~#  brctl addif PentestLab-bridge at0

root@kali:~#  ifconfig enp0s10 0.0.0.0 up

root@kali:~#  ifconfig at0 0.0.0.0 up

![image](Images/image-GHCPA4JZ.png)

Note : pour mon cas, l’interface ethernet est appelée “enp0s10”. Pour trouver la tienne, exécute ifconfig et tu la trouveras ormalement en tout premier :

![Ethernet](Images/image-8K6KEV4O.png)

Et voilà le résultat issu des commandes précédentes :

![bidge_commands](Images/image-17UOVCGL.png)

La deuxième étape consiste à attribuer une adresse IP à ce pont. Note que la meilleure (et la plus facile) solution est d’utiliser DHCP en exécutant une seule commande :

![image](Images/image-OAWBS2P4.png)

root@kali:~# ifconfig PentestLab-bridge 192.168.8.10 up

![image](Images/image-QCGRF8TV.png)![ifconfig____192.168.0.2](Images/image-GCV8JCA5.png)

Note : l’adresse IP du pont devrait appartenir au réseau filaire.

Vérifie la connectivité avec le pont en envoyant des paquets ICMP avec ping. Normalement tu disposeras d’une réponse comme celle-ci :

![ping_192.168.8.10](Images/image-JIXJMPYX.png)

Dernière chose, pour t’assurer que le noyau du système gère correctement le transfert et le routage des paquets, exécute la commande suivante :

![image](Images/image-MNMU59R6.png)

root@kali:~# echo 1 > /proc/sys/net/ipv4/ip_forward

![image](Images/image-KJCA64TR.png)![firewal](Images/image-MKVXJTFE.png)

Excellent, nous sommes donc prêts à lancer l’attaque !

Mon smartphone est connecté au vrai “Pentest-Lab”. Dès maintenant, tu sais comment traiter cette situation : désauthentification !

Je le désauthentifie violement avec aireplay-ng sans lui donner aucune chance de se reconnecter, sachant que l’interface utilisée pour la désauthentification est autre que celle que j’ai utilisé pour créer le faux point d’accès, car le canal d’émission n’est pas le même.

Pour désauthentifier le client, je vais donc utiliser ma carte réseau interne en la mettant bien sûr en mode moniteur d’abord :

![image](Images/image-AERQP63D.png)

root@kali:~# airmon-ng start wlp5s0

![image](Images/image-IZ0NB0OP.png)

Puis je lance airepaly-ng en même temps que airbase-ng :

![allinONE_evil](Images/image-ON31Q070.png)

Le client tombe sur le faux “Pentest-Lab” et il se connecte naïvement. Une fois fait, le DHCP du routeur lui attribue gentillement une adresse IP et il devient NOTRE VICTIME.

Je démarre mon service apache et je vérifie que ma victime y a accès :

![image](Images/image-WA409KG9.png)

root@kali:~# service apache2 start

![image](Images/image-QU00AJIP.png)

Maintenant, sur le navigateur du smartphone, j’entre l’adresse IP du pont :

![Screenshot_2019-03-18-18-55-16](Images/image-P7NVU7S8.png)

Bingo ! Nous l’avons attrapé !

Cette attaque est très puissante au point qu’elle nous permet de voir tout le trafic transmis par la machine victime et de l’intercepter facilement.

La raison pour laquelle cela est possible se résume dans le fait que nous sommes l’intermédiaire entre la victime et Internet, c’est ce qu’on appelle “MAN-IN-THE-MIDDLE-ATTACK” (l’attaque de l’homme du milieu).

![MITJMIDDEL](Images/image-J1KWW3BM.png)

Mais la question qui se pose est : comment peut-on exploiter cette technique pour avoir le mot de passe d’un réseau Wi-Fi ?

#### ‘COMPUTERS AND THE

#### INTERNET WERE BUILT

#### WITHOUT THE IDEA

#### THAT THEY WOULD ONE

#### DAY BE ATTACKED’

Daniel Crowley

––––––––

##### ATTAque EVIL TWIN  (jumeau maléfique)

Il est évident que tu peux utiliser le scénario précédent pour demander à l’utilisateur de te donner un mot de passe (oui, tu as bien lu, il suffit de demander et tu peux l’auras !).

La puissance derrière cette attaque réside dans le fait que la victime a baissé toutes ses gardes. Elle croit qu’elle est sur un réseau de confiance, mais un hacker peut exploiter cette faille humaine.

Le principe est simple : en s’appuyant sur le MITM (Man in the middle), le hacker va rediriger toutes les requêtes de sa victime vers un site truqué qui demande une confirmation de mot de passe pour une raison ou une autre. Face à cette réalité, la victime va entrer ses coordonnées qui seront tombées directement dans la main du hacker (ou pirate). c’est le « phishing ».

Je vais donc te montrer une attaque qui s’appelle « Wi-Fi PHISHING ». Pour cela, je n’ai besoin que d’une page qui contient un formulaire et un peu de design pour convaincre la victime d’entrer le mot de passe de son réseau Wi-Fi.

Par contre, l’utilisation d’un outil qui automatise ce que nous avons réalisé jusqu’à maintenant avec la possibilité de nous fournir des pages préécrites va nous faire gagner du temps.

C’est la raison pour laquelle je souhaite te présenter : Wifiphisher, a.k.a l’outil ultime du Wi-Fi phishing.

Wifiphisher est un outil de sécurité capable de monter des attaques phishing rapides et automatisées contre les réseaux Wi-Fi pour obtenir les identifiants sans brute force.

Tout d’abord, installe l’outil avec la commnde suivante :

![image](Images/image-R5OCLQ7B.png)

root@kali:~# apt-install wifiphisher

![image](Images/image-KYH67O1C.png)

Une fois installé, tu peux le lancer en tapant wifiphisher dans le terminal :

![wifiphisher](Images/image-PK75064G.png)

Il chargera les dépendances dont il aura besoin, puis il débutera la découverte des réseaux :

![wifiphser_decouverte](Images/image-UIOMX5UN.png)

Note : petit rappel, le nombre de réseaux découverts dépend de la puissance de ton adaptateur. Ici, c’est le résultat d’un scan de ma carte alfa awus036h.

Sélectionne ton point d’accès et appuie sur Entrée. Plusieurs scénarios s’offrent à toi, utilise donc les flèches du clavier pour en choisir un.

Ce qui nous intéresse ici, c’est le deuxième scénario “firmware upgrade page” :

![wifiphisher_upgrade](Images/image-YGNXXR1X.png)

Appuie sur Entrée.

Si tu as eu une erreur comme celle-ci... :

![wifipihsier_error](Images/image-IVEPVLUO.png)

Cela veut dire que Roguehostapd (outil qui permet de créer de faux point d’accès) n’est pas installé sur ton système. Dans ce cas-là, tu disposes de deux solutions :

La première solution : installer Roguehostapd

La deuxième solution : ne pas utiliser Roguehostapd pour créer le faux point d’accès

Je vais continuer mon attaque sans avoir besoin d’utiliser Roguehostapd en utilisant simplement l’argument —force-hostapd comme il est indiqué dans le message d’erreur :

![image](Images/image-AABYFX3M.png)

root@kali:~# wifiphisher—force-hostapd

![image](Images/image-8PPQJCWS.png)

Puis suis les mêmes étapes que précédemment. Wifiphisher va automatiser ce que nous avons fait manuellement, en commençant par la création du point d’accès maléfique. Puis, elle continuera avec l’attribution d’une adresse IP aux victimes et enfin avec la redirection vers la page de phishing.

Premièrement, la victime est déconnectée de son point d’accès et automatiquement connectée au faux (si le signal est assez fort). L’on voit du coup que Wifiphisher a commencé à envoyer ses pages de phishing, comme le montre la capture suivante :

![wifiphisher_capting](Images/image-UTD0OC2N.png)

Plusieurs victimes, ont été déconnectées, mais seulement un seul client a pu joindre notre réseau.

Du côté de la victime, un pop-up d’authentification s’affiche :

![Screenshot_2019-03-19-17-20-45](Images/image-QNRFBIR5.png)

La victime, curieuse, clique dessus pour voir ce qui vient l'interrompre au milieu de son travail. Une page de mise à jour s’affiche alors :

![Screenshot_2019-03-19-17-21-03](Images/image-BS0ED56G.png)

La victime (sans réfléchir et anticiper) entre le mot de passe du Wi-Fi et clique sur “Upgrade”.

YOU HAVE BEEN HACKED !

Le hacker reçoit le mot de passe directement :

![wifiphisher_passw](Images/image-XZH6UNOU.png)

Note : bien sûr, tu peux jouer avec le code html/css de la page de phishing comme tu le veux. Dans ce cas, il faut juste apporter les modifications aux fichiers qui se trouvent dans le chemin suivant :

![image](Images/image-5L741O0F.png)

root@kali:~# /usr/local/lib/python2.7/dist-packages/Wi-Fiphisher-1.3-py2.7.egg/Wi-Fiphisher/data/phishing-pages/firmware-upgrade

![image](Images/image-OG7W05EC.png)

Pour ne pas réveiller plus de soupçons la victime est redirigée vers une page de chargement en attendant que le hacker se retire.

![Screenshot_2019-03-19-17-22-24](Images/image-AN6405P5.png)

Ces attaques sont très répandues et très efficaces. La situation s’aggrave toujours plus à cause de l’utilisation des technologies sans prendre conscience des risques encourus.

Et comme tu viens de le voir, un pirate peut récupérer le mot de passe du réseau et peut aussi récupérer (avec un peu plus de créativité) des informations plus confidentielles, comme les coordonnées de la carte de crédit par exemple.

#### “HUMANS ARE THE

#### WEAKEST LINK”

Robert Willis

##### sslstrip : adieu le cryptage !

L’utilisateur d’un réseau est principalement protégé par deux boucliers, le premier étant le chiffrement du protocole WPA que nous avons pu casser dans les chapitres précédents.

Cependant, il nous reste une deuxième barrière de défense : le chiffrement SSL.

Tout d’abord, il va falloir répondre à quelques questions fondamentales à la compréhension de l’attaque que l’on verra par la suite.

Qu’est-ce-que SSL ?

SSL (Secure socket layer) récemment appelé “TLS” est un protocole qui permet la sécurisation des données échangées entre le navigateur et le serveur en satisfaisant les objectifs de sécurité :

›  Authentification

›  Confidentialité

›  Intégrité

#### Comment fonctionne le certificat SSL ?

Il agit en veillant à ce que les données transférées entre les utilisateurs et les sites restent difficiles à lire. SSL utilise l'algorithme de chiffrement pour brouiller les données en transit, empêchant les pirates de les lire lorsqu'elles sont envoyées via la connexion.

Un certificat SSL est installé sur le côté serveur, mais il y a des indices visuels sur le navigateur qui peuvent dire aux utilisateurs qu'ils sont protégés par SSL. Tout d'abord, si SSL est présent sur le site, les utilisateurs verront “https://” au début de l'adresse web au lieu du “http://” comme le montre la figure suivante :

![site-http-https-exemple-login-chrome.v636573289323980081](Images/image-NUNY5EVT.png)

Lors de l’échange des informations, le certificat SSL déclenche le protocole SSL qui va chiffrer les informations en agissant directement comme une couverture pour le protocole TCP. Il permet aux couches supérieures du protocole de rester inchangées tout en offrant une connexion sécurisée.

Ce chiffrement des informations fait qu’un hacker qui s’est mis au milieu de la connexion ne pourra intercepter aucune information.

Maintenant que tu as compris le principe du protocole SSL, à nous de voir comment bipasser cette mesure de sécurité afin de pouvoir intercepter les paquets envoyés par l’utilisateur.

Sslstrip est un outil qui permet de détourner le trafic sécurisé HTTPS en le redirigeant vers du HTTP tout en jouant le rôle d’un proxy entre le navigateur et le serveur.

Maintenant que tu as compris le principe du protocole SSL, à nous de voir comment bipasser cette mesure de sécurité afin de pouvoir intercepter les paquets envoyés par l’utilisateur.

Sslstrip est un outil qui permet de détourner le trafic sécurisé HTTPS en le redirigeant vers du HTTP tout en jouant le rôle d’un proxy entre le navigateur et le serveur.

Pour expliquer en détails cette attaque, voici une illustration qui schématise cette dernière :

![74c4193e-b33e-41e2-921a-6f2916e9075b](Images/image-R9639IF3.jpg)

Tout d’abord, la vicitme va ouvrir son navigateur et essayer de se connecter à un site web via HTTPS

Arpsoof est un utilitaire que le hacker va utiliser afin que le routeur redirige vers lui tout le trafic provenant de la victime.

Le hacker va convertir la requête en HTTP avec Sslstrip

Puis il renvoie la nouvelle requête HTTP vers le routeur

Le routeur prend la requête et l’envoie au serveur

Enfin, le serveur reçoit la requête et répond en établissant une connexion HTTP

Voilà, nous avons accompli notre objectif en obligeant la victime à se connecter via HTTP. De cette façon, nous pourrons lire les informations échangées.

Voyons tout de suite comment nous pouvons appliquer cette attaque avec Kali.

Nous devons tout d’abord déterminer l'interface que nous utilisertons pour nous connecter au réseau. Pour se faire, nous pouvons utiliser la commande ifconfig sur notre machine Kali.

![ifconfig_sslstrip](Images/image-8LOOBMP6.png)

Une fois que nous avons déterminé l'interface que nous utilisons, nous devons exécuter le processus de transfert IP pour lequel nous tapons la commande suivante :

![image](Images/image-9YA7R9PA.png)

root@kali:~# echo 1 > /proc/sys/net/ipv4/ip_forward

![image](Images/image-RQXVY2TM.png)![sslstrip_echo](Images/image-ZOU5TCTA.png)

Configurons note pare-feu pour qu’il puisse rediriger le trafic :

![image](Images/image-55JPHGB2.png)

root@kali:~# iptables -t nat -A PREROUTING -p TCP—destination-port 80 -j REDIRECT—to-port 8080

![image](Images/image-FZLM1ILH.png)![sslstrip_iptables](Images/image-OYDRAETX.png)

Comme nous avons configuré le trafic pour qu'il soit routé via notre machine, nous devons maintenant trouver l'adresse IP du routeur. Exécute donc la commande suivante  :

![image](Images/image-3DDPML9Q.png)

root@kali:~# route -n

![image](Images/image-3M4LL9I9.png)![sslstrip_gateway](Images/image-9WSUUSY0.png)

Pour te montrer cette attaque, je vais utiliser une machine sous Windows comme victime avec l’adresse IP suivante :

![sslstrip_vicitme](Images/image-7R40FURN.png)

Une fois que nous avons déterminé l’adresse IP du routeur et de la machine cible, nous pouvons mener à bien le processus de arpsoofing, où le trafic provenant du serveur et destiné au système de la victime nous sera redirigé et nous le transmettrons à son tour au système de la victime.

![image](Images/image-R8LQAALA.png)

root@kali:~# arpspoof -i wlp5s0 -t 10.20.32.191 10.20.30.1

![image](Images/image-D60XZ677.png)![sslstrio_arpsoof](Images/image-P4L31KFI.png)

Dès que nous exécutons cette commande, le trafic sera redirigé vers la machine du hacker. Simultanément, nous devons ouvrir un nouveau terminal, où nous devons taper cette commande :

![image](Images/image-29V19NF0.png)

root@kali:~# sslstrip -l 8080

![image](Images/image-2SCRRS8K.png)![sslstrip_8080](Images/image-A4O88T7M.png)

Cela convertira les sites Web HTTPS en HTTP et nous initions un écouteur sur le port 8080.

Nous sommes donc prêts à partir. À chaque fois que la victime ouvre son navigateur et navigue sur Internet, le trafic nous est redirigé.

Sur la machine cible, j’ouvre le navigateur et je me connecte à Facebook :

![sslstrip_detection](Images/image-TE6SM576.png)

Instantanément, le navigateur détecte qu’il y a une redirection de traffic. Mais ce qui est intéressant, c’est que cet avertissement n’apporte pas assez d’informations sur ce qui se passe derrière les coulisses, il y a simplement une redirection vers Facebook.

L’utilisateur n’a que deux choix : soit il continue vers le site ou bien il revient à la page précédente.

Sachant qu’il y a de fortes chances que l’utilisateur cliquera sur le lien de redirection, le site web s’affichera le plus normalement possible :

![sslstrip_facebook](Images/image-P692P2BQ.png)

Jusque-là, c’est assez bien joué.

Prête attention au protocole utilisé dans le transfert de données, c’est du HTTP et non pas du HTTPS.

La victime va entrer ses informations en cliquant sur Login et elle se connectera normalement. Cependant, l’attaquant peut lui aussi se loguer avec ses informations personnelles.

![sslstrip_login](Images/image-9YLU5XF6.png)

DONE !

Arrête arpsoof et Sslstrip en appuyant sur Ctrl+c.

Les informations capturées seront stockées dans un fichier sslstrip.log que tu trouveras au même endroit où tu as lancé sslstrip. Pour cela, exécute la commande suivante :

![image](Images/image-GF8RMQDX.png)

root@kali:~# cat sslstrip.log | grep "pass"

![image](Images/image-K75A7AO9.png)![sslstrip_hacked](Images/image-8J2FVRZJ.png)

Note : le “%40” est l’encodage URL de “@”.

##### KRACK ATTACK

Le 17 octobre 2017, Mathy Vanhoef, un chercheur en sécurité informatique publie une recherche qui dévoile une vulnérabilité qui touche presque tous les réseaux Wi-Fi utilisant le protocole WPA. C'est l’attaque “KRACK” (Key reinstallation attack).

Bien sûr, Mathy n’a pas publié le script qui permet l’exploitation de cette faille (sinon ça aurait été la catastrophe !), cependant, il a réalisé une vidéo de preuve du concept ainsi qu’un article détaillé qui démontre comment l’on peut exploiter les appareils basés sur Android, iOS, Linux, Windows et d’autres systèmes d’exploitation pour accéder à toutes les informations que l’utilisateur télécharge ou met en ligne.

En créant un faux point d’accès, l’attaquant va cibler la troisième étape du processus du 4-way handshake. La clé de chiffrement peut être renvoyée plusieurs fois au cours de la troisième étape. Si les attaquants collectent et rejouent ces retransmissions de manière particulière, le chiffrement de sécurité Wi-Fi peut être rompu.

Une fois l’attaque établie, l’attaquant peut accéder aux noms d'utilisateur, aux mots de passe et aux données stockées sur les appareils. Le pirate peut lire les e-mails et voir des photos des données transmises, puis utiliser ces informations pour faire du chantage aux utilisateurs ou les vendre sur le Dark Web.

#### Comment se défendre ?

❖  Savoir que ces attaques existent

❖  Être vigilant

#### “DEFENSIVE NEEDS TO SECURE

#### EVERYTHING, WHEREAS AN

#### ATTACKER ONLY NEEDS TO

#### FIND THAT ONE OPENING”

Jennifer Havermann

##### Chapiter 9

![image](Images/image-4RML5381.png)

##### WPS CRACKING

Wireless protected setup (WPS) a été introduit en 2006 pour aider les utilisateurs non-geeks (à savoir, ayant peu de connaissances en sécurité des technologies) à mieux configurer et sécuriser leurs réseaux.

L’idée derrière le WPS était que les appareils Wi-Fi n’aient qu’une seule valeur codée en dur sur le routeur, à savoir, un code PIN. Ce dernier permettrait un accès au réseau sans être obligé d'entrer la clé de ce même réseau (souvent longue et complexe).

Autrement dit, les appareils qui veulent avoir accès au réseau doivent obligatoirement disposer du code PIN et l’accès physique au point d’accès.

L’utilisateur voulant se connecter, doit juste entrer le code PIN et appuyer sur le bouton WPS qui se trouve sur la box. Suite à cette action, le routeur va générer un mot de passe et l’envoyer à l’appareil qui envoie la requête d’authentification, lui permettant de se connecter instantanément.

Ce standard fait que les personnes qui n’ont pas d’accès physique au point d’accès ne peuvent pas se connecter. Malheureusement (ou heureusement pour les black hat), ce n’est pas le cas.

En effet, en 2011, le chercheur Stefan Viehböck a découvert une vulnérabilité qui permet d’exploiter ce protocole.

Le fait que le code PIN ne soit composé que de 8 caractères compris entre 0 et 9, donne qu’un nombre de 100 000 000 possibilités en comparaison avec un mot de passe de azAZ09 à 8 caractéres ayant 218.340.105.584.896 combinaisons possibles (je parle de WPA).

Cela facilite drastiquement l’attaque.

Cependant, ce nombre restreint de possibilités n’est pas la seule faiblesse de ce protocole :

›  Première faille : il n’y a que 7 chiffres significatifs dans le code PIN. Le huitième chiffre est une somme de contrôle, que l’attaquant peut calculer. L’on passe donc à 10 000 000 possibilités.

›  La seconde faille : (plus gênante), l’appareil vérifie le code en deux fois. Concrètement, il est possible de vérifier si les 4 premiers chiffres sont justes et ensuite de vérifier si les quatre suivants sont bons. Au lieu de 100 000 000 possibilités, l’on passe donc à 10 000 possibilités + 10 000 possibilités, soit 20 000 possibilités.

Voyons voir comment nous pouvons cracker la clé en exploitant toutes ces vulnérabilités au même temps.

Comme d’habitude, rends-toi sur l’interface de configuration de ta box et active le standard WPS si ce n’est pas encore fait. En ce qui me concerne, le WPS est désactivé par défaut donc je vais l’activer pour te montrer l’attaque :

![WPS_actiatet](Images/image-SBZJXE1A.png)

Comme tu peux le voir, le code PIN de mon routeur est écrit d’une manière visible.

Très bien, notre environnement de test est prêt.

Wash est un outil qui permet de scanner l’entourage à la recherche de réseaux ayant le protocole WPS activé. Mets donc ta carte réseau en mode moniteur pour pouvoir lancer wash :

![image](Images/image-SASZJWKA.png)

root@kali:~# airmon-ng start “interface”

![image](Images/image-PZO5Q9S7.png)![WPS_airmon](Images/image-DRCIQAO2.png)

Avec la carte réseau en mode moniteur tu peux maintenant lancer wash à la recherche de réseaux ayant un WPS active. Exécute la commande suivante :

![image](Images/image-G59LW6EA.png)

root@kali:~# wash -i “interface-monitor”

![image](Images/image-ROS9UVF6.png)![wps_error](Images/image-ICYE3R9A.png)

Oups ! Une erreur !

En vérité, je ne sais pas à quoi est due cette erreur, mais le fait d’exécuter la commande ifconfig wlan0mon up, fera tout rentrer dans l’ordre :

![WPs_up](Images/image-UK7BVQR4.png)

Réexecute la commande wash -i wla0mon. Cette fois-ci, tu devrais avoir un résultat comme celui-là :

![WPSscan](Images/image-TAIB5807.png)

Très intéressant ! Je vois que je ne suis pas le seul qui est en train d’étudier le protocole WPS !

Même s’il est connu que ce standard soit très vulnérable, les constructeurs de point d’accès vendent toujours des points d'accès avec un WPS activé par défaut, ce qui rend le réseau et ses utilisateurs sans défense.

Wash nous dévoile les réseaux avec un WPS activé, sa version, et s’il est verrouillé ou non.

Maintenant, c’est à reaver de brute forcer le code PIN. Pour cela, entre cette commande dans ton terminal :

![image](Images/image-KIJSY7YS.png)

root@kali:~# reaver -i “interface-monitor” -b <AP MAC> -vv

![image](Images/image-PP554BXX.png)

-vv : pour le mode verbeux

![reaver_stary](Images/image-19PJPXSF.png)

Après quelques tentations de brute force, le routeur a détecté l’attaque et a imposé un temps d’attente de 60 secondes entre chaque tentative ce qui augmente considérablement le temps de calcul :

![WPS_failed](Images/image-H3E2W6PR.png)

Ce mécanisme de défense a été introduit avec la version WPS 2.0, rendant notre attaque beaucoup moins efficace.

Note : que dirais-tu de changer l’adresse MAC à chaque tentative de brute force ? Est-ce que cela va bypasser la détection ? À toi de voir !

##### REAL HACKING !

Etant donné que je n'ai pas pu me hacker, je me dois de te démontrer une attaque réussie sur le réseau d’un ami .

Je vais attaquer le point d’accès avec le ESSID “ABD0u” (attention, j’ai demandé la permission) :

![abdou_wps](Images/image-GFH6HFX6.png)

En exécutant la commande reaver -i wlan0mon -b 74:DA:DA:BD:70:69 -vv j’ai pu cracker le code PIN et récupérer le mot de passe du Wi-Fi en quelques secondes seulement :

![abdou_crack](Images/image-O16N0BYD.png)

#### Comment se défendre ?

❖  Désactiver la fonction WPS

#### “IT’S THE VERY FACT PEOPLE AVOID THE

#### COMPLICATED BITS THAT ENABLE THE

#### FEW WHO ACTUALLY STUDY [HACKING]

#### TO HAVE EXTRAORDINARY POWER”

Robert Rraham

##### Chapiter 10

![image](Images/image-4RML5381.png)

##### attaque  par dénie de service (Dos)

Dos, l’une des attaques les plus utilisées sur la toile.

Cette attaque a pour but de rendre un service indisponible ainsi que d’empêcher les utilisateurs légitimes de se connecter.

Les attaques Dos augmentent non seulement en nombre, mais aussi en sophistication, en complexité et en durée.

Les réseaux Wi-Fi sont extrêmement sensibles aux attaques par déni de service, et il est difficile de localiser l'attaquant sur un réseau sans fil.

Les exemples d'attaques DoS sont les suivants :

Le hacker peut créer des requêtes d’authentification et de dissociation qui sont utilisées dans un réseau sans fil pour fermer des connexions autorisées ou pour inonder le réseau et empêcher les utilisateurs légitimes de maintenir leur connexion à un point d’accès sans fil.

Bombarder le réseau d’un flot de paquets de données pour le rendre indisponible pour l’utilisation. Par exemple, une attaque par inondation HTTP faisant des milliers de requêtes à un serveur web peut épuiser sa capacité de traitement, même chose pour le réseau Wi-Fi.

Certains appareils et applications peuvent reconnaître qu’une attaque est en cours et désactivent automatiquement le reseau. Cependant, un hacker peut lancer une attaque évidente puis laisser la cible créer le Dos elle-même.

En fait, le protocole sans fil 802.11 a été créé dans le but de prendre en charge la désauthentification à la reception d’un paquet de sorte que l’utilisateur puisse rompre une connexion quand elle n’est plus nécessaire.

Comme tu peux le constater, envoyer des paquets de désauthentification dans le réseau est conforme à la norme, ce qui rend l’attaque Dos dévastatrice et il n’y a aucun moyen de l’empêcher de se produire.

Pour démontrer ce point, nous allons utiliser aireplay-ng pour déconnecter tous les utilisateurs du point d’accès.

Tout d’abord, mets ton adapteur en mode moniteur afin qu’il puisse injecter les paquets de désauthentification :

![DOS_monitor](Images/image-A9QJYXCS.png)

Puis lance airodump-ng pour repérer le point d’accès cible :

![image](Images/image-U6MQUAT6.png)

root@kali:~# airodump-ng wlan0mon

![image](Images/image-0LCLMJ97.png)![DOS_cible](Images/image-I19A92B9.png)

Voyons les utilisateurs qui sont déjà connectés au point d’accès avec la commande suivante :

![image](Images/image-U2AQQK4R.png)

root@kali:~# airodump-ng—bssid <AP MAC>—channel <canal> wlan0mon

![image](Images/image-GZ01EDY3.png)![DOs-clients](Images/image-AI1UY4FI.png)

Et voici le résultat :

![DOs_smartphone](Images/image-VGODDKS2.png)

Voilà, un utilisateur est connecté (et il ne le sera plus après le lancement de notre attaque Dos !)

Exécute la commande suivante pour lancer l’attaque :

![image](Images/image-J8KLTQKX.png)

root@kali:~# aireplay-ng -0 0 -a <AP MAC>—ignore-negative-one “interface-moniteur”

![image](Images/image-WZI75L4N.png)![DOS](Images/image-VW6YT27V.png)

Le point d’accès n’est plus disponible à ses utilisateurs et le smartphone ne peut plus se connecter.

![Screenshot_2019-03-22-18-46-35](Images/image-90RBOJJP.png)

Note : DDos (l’attaque par déni de service destribué) est tout simplement une attaque Dos effectuée depuis plusieurs machines (BOT) rendant l’attaque beaucoup plus efficace et dont l’origine est plus complexe à localizer.

##### Chapiter 11

![image](Images/image-4RML5381.png)

##### Maintenir l’accès

Dans les chapitres précédents, nous avons vu comment briser/bypasser les protocoles de sécurité des réseaux Wi-Fi en capturant les paquets échangés entre le point d’accès et ses clients légitimes.

Une fois le mot de passe dans la poche, nous allons pousser un peu plus loin ton test d’intrusion en mettant en place un mécanisme qui te permettra d’avoir le mot de passe sans avoir à le recracker.

Cependant, la démarche que je vais te présenter ici n’est pas applicable à tous les points d’accès, car tout dépendra de plusieurs facteurs dont le type de routeurs, le fabricant, ou encore le firmware..

Dans tous les cas, c’est une technique dont tu auras besoin un jour dans ton processus de hacking. N’oublie pas que c’est entre “savoir” et “ne pas savoir” que réside toute la différence.

J’ai utilisé cette méthode avec un routeur D-Link DSL-2750U lors d’un test d’intrusion afin de maintenir mon accès au routeur même après que le changement du mot de passe du Wi-Fi.

Après avoir cracké le mot de passe, je me suis mis sur l’interface de configuration :

![Dlink_login](Images/image-6GNI3JR5.png)

Premier challenge...

ou pas ! En effet, une petite recherche “default D-link routeur username and pasword” sur Google m’a donné instantanément la réponse : “admin”:”admin” étant donné que l’administrateur a laissé les valeurs par défaut (une mauvaise habitude très répandue et qu’il ne faut pas négliger).

Note : même si les paramètres (username et password) ont été changés, tu détiens toujours la capacité de brute-forcer les deux champs avec un outil comme hydra.

Après avoir atterri sur l’interface de configuration, je me déplace vers l’onglet “Advanced puis Dynamic DNS”.

––––––––

![dynamic_dns](Images/image-MY31MOJF.png)

Après avoir atterri sur l’interface de configuration, je me déplace vers l’onglet “Advanced puis Dynamic DNS”.

Tu vas voir apparaître une liste de fournisseurs DDNS. Personnellement, je préfère utiliser noip.com, donc rends-toi sur leur site et crée un compte (c'est gratuit !).

![NOIP](Images/image-FEBIXNG6.png)

Voilà, maintenant clique sur “Active hostnames”, puis crée “un nom d’hôte” :

![create-hostname](Images/image-XHLSLRBP.png)

Mets le nom d’hôte de ton choix et change le domaine à “hopto.org”. Clique enfin sur “create hostname”.

![host-name-created](Images/image-MHU7EZ22.png)

Il ne te reste plus qu’à configurer le nom d’hôte.

Clique sur l’écriture en jaune pour commencer avec la configuration et mets les informations nécessaires :

![web_server_config](Images/image-OHCIPQV2.png)

Ils te demanderont le port que tu souhaites utiliser afin de te connecter au serveur :

![port_80](Images/image-K2031FCJ.png)

Là, on arrête !

Je pense que ton sixième sens t’a prévenu, Noip vient de nous demander d’ouvrir l’un des deux ports le 80 ou bien le 443.

Ouvrir un port sur un routeur de n’importe quelle infrastructure la rend FORTEMENT vulnérable, car l’on donne un accès direct du réseau à tout le monde (y compris les gens malintentionnés).

Il faut donc réfléchir deux fois avant de faire un tel geste. L’essentiel est d’avoir conscience de ce que tu es en train de faire et comme dit précédemment, c’est le savoir qui compte (et l’action aussi !).

Revenons donc à notre interface de configuration.

Voici comment ouvrir un port sur WAN (Wide area network) :

![open_80](Images/image-W1RQ9GIC.png)

Voilà, avec le port 80 (service http) ouvert, on est prêt a continuer la configuration de notre hostname.

![open_80_check](Images/image-55SNDDPH.png)

DONE !

![hosname_done](Images/image-WP602XL1.png)

Maintenant, si tu fais une recherche sur le nom de domaine “pentest-lab.hopto.org”, tu tomberas sur la page de login du routeur :

![pentest-lab_online](Images/image-Y6QTP88D.png)

C’est fort, n’est-ce-pas ?

Maintenant, tu as accès au routeur à n’importe quel moment, dès que tu en auras besoin. N’oublie cependant pas ce que je t’ai dit plus haut, “les risques du confort” !

Note : Tu peux aussi créer un autre compte administrateur pour perfectionner ton maintien d’accès

![ADMIN](Images/image-F4QL144I.png)

Pas la peine d’essayer de connecter, je vais le retirer dès  le chapitre terminé

N’oublie pas de noter le code PIN du point d’accès, tu en auras sûrement besoin

#### “NO REAL EXPERT I KNOW CALLS

#### THEMSELVES AN EXPERT”

Robert M. Lee

#### Autres Livres De B.Anass

[DARK PYTHON : Apprenez à créer vos propres outils de Hacking](https://amzn.to/2vxyNhF)

––––––––

![1580303538](Images/image-URI0DUUW.png)

#### Python, pourquoi l’apprendre? 

Il est évident que ce n'est pas possible de devenir un hacker respectable sans avoir la compétence de programmer, à savoir, la chose la plus effrayante pour les débutants en hacking !

La programmation t’offre la flexibilité, la souplesse, et le raisonnement pour que tu puisses t’adapter aux différentes situations dans lesquelles les outils proposés par d’autres programmeurs sur le web ne répondent pas à tes besoins.  Tu serras donc obligé de créer l’outil adéquat toi-même et ainsi mettre tes compétences de programmation en pratique.

Comme nous le voyons, l’évolution du web est en accélération de jour en jour, ce qui fait que ce qui marche aujourd’hui ne marchera peut-être plus demain.  Le vrai hacker ne reste pas coincé avec  des outils périmés pour effectuer ses hacks, car attaquer un système sophistiqué à l’aide de vieux outils ou  de méthodes inefficaces ne fait qu'accélérer ton  processus d’échec et peut être d’emprisonnement (je parle bien sûr aux black hat).

Ainsi,  si tu sais  programmer, cela augmente tes chances de réussite dans un hack, en bipassant toutes les mesures de sécurité que tu rencontreras, que ce soit des IDS (Intrusion detection system), antivirus ou autres outils de défense. En tant que programmeur, tu es au courant de comment tout cela fonctionne, rendant tes attaques plus pertinentes tout en restant sur tes gardes.

Un autre atout pour ceux qui savent programmer est qu’ils connaissent le mode de fonctionnement des outils qu’ils utilisent durant leur processus de hacking. Certes, il n’est pas nécessaire de créer tous ses outils pour être hacker, mais utiliser un outil dont tu  ne connais pas le  fonctionnement ne fait de toi  qu’un “script-kiddie”.

Souvent, tu n’auras qu’à modifier un script écrit par d’autres hackers pour l’adapter à ta  situation (ce qui pour moi, est une opportunité qui ne s’offre qu’aux programmeurs, car cela  fait gagner un temps fou). Tu vas certainement te retrouver dans des situations où tu  n’auras pas ce luxe. Alors, la seule solution serait d’écrire son propre programme de A à Z, puis de le partager avec la communauté des programmeurs (c’est une communauté géniale, je te l’assure !). Le partage permet de voir de quelle manière d’autres cerveaux peuvent résoudre le même challenge par différentes stratégies. Leurs feed-back vont aussi te faire passer à un niveau supérieur et tu vas te retrouver entouré de bonnes personnes.

#### Python, c’est quoi ?

Python est un langage de programmation de haut niveau, objet interprété, multi-plate-forme et open source, impliquant donc que son interpréteur avec ses librairies sont disponibles au téléchargement gratuit pour les différents systèmes d’exploitation (Windows, Linux, iOS...).

C’est un langage de haut niveau, c'est-à-dire que tu peux comprendre ses syntaxes facilement, ce qui fait la différence avec les langages de bas niveau qui sont proches du langage machine tel que Assembly que seules les machines peuvent comprendre.

Python a été créé aux environs des années 1980 par Guido Van ossum (son nom a l’odeur de la programmation) et il a pris de l’ampleur petit à petit jusqu’à devenir l’un des plus populaires langages de programmation.

La propagation de ce langage est due à sa syntaxe explicite et sa puissance, l’on peut pratiquement tout créer avec Python (GUI, application web, jeux... Etc.).

Si tu programmes avec d’autres langages de haut niveau, tu ne trouveras aucune difficulté à comprendre ses syntaxes, et même, au contraire tu constateras que les commandes sont plus courtes (comparé à Java par exemple), ameliorant donc la lisibilité des lignes de codes.

Python vient avec une pile de librairies et modules intégrés, donnant à l’utilisateur un large spectre de possibilités et de flexibilité, faisant de lui l’une des meilleures armes des hackers.

Voici un exemple :

Si tu veux écrire un programme classique qui affiche “Hello, world !” en utilisant le C++, tu seras obligé de procéder comme ce qui suit :

| #include <iostream> int main() { std::cout << "Hello, new world!" << std::endl; return 0;} |

Relativement long, non ?

Par contre, je peux obtenir le même résultat en utilisant une seule ligne en Python :

| print("Hello, world!") |

C’est juste une petite démonstration de la simplicité de Python comparé à d’autres langages de script de haut niveau.

Note : “print” veut dire “imprime” en anglais. En Python l’on utilise ce même terme pour l’affichage.

Si tu es nouveau dans le dojo de la programmation, tu apprécieras sa simplicité, ainsi que sa portabilité, car tu pourras utiliser tes programmes dans quasiment tous les systèmes de programmation.

Du point de vue du hacking, tu auras la capacité de contrôler n’importe quel microcontrôleur qui marche sous un OS quelconque. Ces microcontrôleurs sont présents un peu partout : dans les jouets, les caméras, les ordinateurs et même les voitures.

## Une dernière chose ...

#### Si tu as apprécié ce livre ou si tu l’as trouvé utile, je te serais reconnaissant de poster un court commentaire sur Amazon. Le soutien de mes lecteurs fait vraiment une différence et je lirai tous les commentaires personnellement afin de pouvoir obtenir tous les feed-back et améliorer ce même livre.

––––––––

#### Merci encore pour ton soutien !

![image](Images/image-J6J7DQGV.png)

## Don't miss out!

Click the button below and you can sign up to receive emails whenever B. Anass publishes a new book. There's no charge and no obligation.

![Sign Me Up](Images/image-81EQGQQ5.png)

[https://books2read.com/r/B-A-JUUP-TFDRB](https://books2read.com/r/B-A-JUUP-TFDRB)

![books2read](Images/image-CBLL8YCC.png)

Connecting independent readers to independent writers.

Did you love Wi-Fi hacking avec Kal Linux : guide étape par étape : apprenez à pénétrer les réseaux Wi-Fi et les meilleures stratégies pour les sécuriser? Then you should read Hacking pour débutant : le guide ultime du débutant pour apprendre les bases du hacking avec Kali Linux et comment se protéger des hackers by B. Anass!

![Hacking pour débutant : le guide ultime du débutant pour apprendre les bases du hacking avec Kali Linux et comment se protéger des hackers](Images/image-S7EF7RHC.jpg)

Voulez-vous devenir hacker même si vous n'avez jamais touché à un clavier ! Faire partie d'une communauté de hackers talentueux et motivés et obtenir en plus de tout ça une formation vidéo gratuite ?

Laissez-moi d'abord vous raconter une histoire :

Je me réveille le matin, je mets mon laptop dans le sac à dos, la destination la fac où j'ai cours toute la mâtiné. Le problème, c'est que j'ai pas envie de perdre 4 heures à entendre des choses que je connaisse déjà, je décide de m'amuser !

Le prof parle sans arrêt et je commence à m'ennuyer, je lance ma distribution préféré : Kali Linux, et en bidouillant quelques instants j'arrive à exploiter le laptop du prof .... Hum, que puis-je faire maintenant !Je me balade un peu dans les différents dossiers, peut-être, je trouverai le sujet de mon prochain examen ! Aha, très intéressant son navigateur enregistre tous ses mots de passe allant du compte Gmail, compte Facebook, carte de crédit .... Mais tout cela m'intéresse peu, car je veux juste m'amuser (en plus, je ne suis pas si méchant que ça!). Allez, j'en ai marre de ce cours, je supprime la diapo qu'utilise le prof et je redémarre l'ordinateur après avoir changé le mot de passe d'utilisateur.....Ouf enfin, il panique et nous laisse partir. 

Ça vous dit d'avoir un tel pouvoir ? 

La capacité de pénétrer les systèmes informatiques et de manipuler leurs utilisateurs pour avoir les informations que vous en avez besoin...... je vais VOUS aider à le faire.

Attention, je vais vous révéler ma propre stratégie pour devenir hacker éthique !

J'ai galéré longtemps pour acquérir un tel pouvoir, et peut-être, c'est votre cas aussi, vous ne trouvez pas les ressources qui vous permettent d'apprendre le hacking en partant de zéro, les livres de hacking que vous avez acheter ou télécharger ne sont pas destiné aux débutants, et les vidéos sur YouTube sont en anglais et vous ne maîtrisez pas l'anglais pour le moment !.Vous avez toujours voulu pirater un compte Facebook, ou apprendre à utiliser Kali Linux.J'étais comme vous, il y a quelques années de cela, et aujourd'hui je vais vous accompagner et vous montrer comment le faire pas à pas.

Vous pouvez utiliser l'option "Feuilleter" pour découvrir ce que vous allez apprendre dans le livre.

À la fin de ce livre :

Vous allez avoir une solide base en cybersécurité et hacking.Vous n'avez pas besoin de permissions.Vous avez la compétence (et la confiance) de pénétrer des systèmes informatiques.

À vous de reprendre contrôle

Also by B. Anass

Hacking

[Hacking pour débutant : le guide ultime du débutant pour apprendre les bases du hacking avec Kali Linux et comment se protéger des hackers](https://www.draft2digital.com/catalog/756654)

[Kali Linux pour débutant : le guide ultime du débutant pour apprendre le système d'exploitation des hackers](https://www.draft2digital.com/catalog/757010)

[Metasploit Pour Débutant: Le guide du débutant pour bypasser les antivirus, contourner les pare-feu et exploiter des machines avec le puissant Framework Metasploit](https://www.draft2digital.com/catalog/757314)

[Dark Python : Apprenez à créer vos propres outils de Hacking (2e édition)](https://www.draft2digital.com/catalog/757617)

[Le coté obscur d’Internet: explorez ce que 99% des internautes ignorent sur les ténèbres d’Internet et apprenez à visiter le dark net en toute sécurité](https://www.draft2digital.com/catalog/757941)

[Le secret De La Cybersécurité: Le guide pour protéger votre famille et votre entreprise de la cybercriminalité](https://www.draft2digital.com/catalog/757622)

[Web hacking: apprenez à tester la sécurité des applications web comme un hacker pro avec kali linux](https://www.draft2digital.com/catalog/757624)

[Wi-Fi hacking avec Kal Linux : guide étape par étape : apprenez à pénétrer les réseaux Wi-Fi et les meilleures stratégies pour les sécuriser](https://www.draft2digital.com/catalog/757945)