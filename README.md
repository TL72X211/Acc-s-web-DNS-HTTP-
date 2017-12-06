**Accès web (DNS, HTTP)**
--------------------------
##Team
   * Animateur : **Hugo**
   * Secrétaire : **Emilien**
   * Scribe : **Flo**
   * Gestionnaire : **Max**


## Mots Clés
   * DNS : Domain Name Server 
   * Apache : Serveur HTTP créé et maintenu par la fondation Apache, c’est le plus populaire sur le World Wide Web.
   * http : Hypertext Transfer Protocol
   * Nslookup : Programme informatique de recherche d’information dans le DNS, qui associe le nom de domaine à une @IP. Il n’est plus utilisé pour UNIX, on utilise plus « dig » ou « host », cependant il est toujours d’actualisé sous Windows.
   * FAI : Fournisseur d’Accès Internet (Sfr, orange…)
   * FQDN : Fully Qualified Domain Name, dans le DNS, c’est un nom de domaine qui révèle la position absolue dans l’arborescence DNS en indiquant tous les domaines de niveau supérieur jusqu’à la racine. Par convention, un FQDN est terminé par un point. Ce qui signifie qu’il est suivie par une chaîne vide qui représente le domaine racine.
Par exemple : mymail.somecollege.edu
Le hostname est mymail, et il est dans le domaine, ‘somecollege.edu ‘, edu est le TLD (top level domain)
   * nginx ,  iis : Nginx est un logiciel libre de serveur Web (ou http), ainsi qu’un proxy inverse. Sa particularité est qu’il est un serveur asynchrone, il utilise les changements d’état pour gérer plusieurs connexions en même temps. (Ainsi, performances élevées + consommation de mémoire faible). 
IIS est un serveur Web pour les différents systèmes d’exploitation Windows NT.
   * registrar : 
C'est un organisme accrédité par les autorités compétentes en matière d'attribution et de gestion des noms de domaine.
Le métier de registrar consiste principalement à la vente et à la gestion des noms de domaines auprès du grand public. Ainsi dans l'organisation du système de nommage, le registrar est le dernier intermédiaire technique accessible au public pour enregistrer un nom de domaine.
L'activité de registrar est complémentaire avec celles d'hébergeur, de fournisseur d'accès et d'attribution des adresses IP. L'ensemble de ces acteurs interviennent dans le fonctionnement d'Internet.

   * Virtual Host : Hébergement virtuel, méthode que le serveurs (web)utilisent pour accueillir plus d’un nom de domaine sur un même ordinateur, parfois sur la même @IP, tout en maintenant une gestion séparée de chacun de ces noms. Cela permet de partager les ressources du serveur (mémoire, processeur). On y retrouve : Un nom, une @IP (pour chaque nom) (+N° de port rarement, car peu ergonomique).
   * enregistrement DNS de type A : Lien entre un nom unique et une @IPv4. Ainsi, on aura un nom de domaine qui pointera sur le serveur trouvé à une @IP données. On y retrouve un TTL, qui lui donne une durée de vie.
   * résolution de nom : Fais référence au DNS.
   * adresse IP 8.8.8.8 : serveur DNS de google.
    

## Contexte

### Quoi ?
 *  Panne/Réparer du serveur DNS du FAI
 * Rétablir l'accès au site
 * Rétablir le serveur DNS
  
### Comment ?
  * En réparant le problème avec le DNS
  
### Pourquoi ?
* Pour pouvoir accéder à [lemonde.fr](lemonde.fr)

## Contraintes
   * aucune

## Problématique
   * Comment faire en sorte que notre FAI reconnaisse notre DNS





## Généralisation
   * MCO : maintenance en condition opérationnelle

## Hypothèses
 * 8.8.8.8 est l'adresse du DNS de google
 * nslookup donne le domaine dans lequel on est et nous donne l'adresse IP correspondante
 * Appache et IIS sont des paquets qui permettent de construire un serveur
 * On ne peut demander au FAI de mettre à jour un DNS nous correspondant
 * OVH donne les noms de domaines
   
## Plan d'action

### Études
  * DNS
  * Protocole HTTP
  * Fonctionnement de nslookup
  * Organismes gérant les protocoles
  * Théorie de communication
  * Format des messages (émission/réception)
  * Messages
  * Canaux de communication
  * Couches des différents protocoles
  * Implémentation des protocoles
  
###Réalistions
* Résoudre le problème 
* Connaitre "les 13"




**1 – Etude du DNS :**
**ARCHITECTURE**
Ensemble de protocoles pour :
-	Interroger et MAJ la base de données d’un serveur DNS
-	Réplication des informations dans la BDD entre serveurs
-	Schéma de la BDD
Un nom de domaine pleinement qualifié (FQDN) identifie de position l’hôte dans l’arborescence hiérarchique DNS en spécifiant la liste de noms par des points, de la racine vers l’hôte.

![](https://github.com/TL72X211/UE2-Prosit-3-Acces-web-DNS-HTTP/blob/Emilien/Images_Prosit/1.png)
 
-	Com = organisations commerciales
-	Edu = etablissement d’enseignement
-	Org = Organisation à but non lucratif
-	NET = Réseaux (dorsale d’internet)
-	Gov = Organisation gouvernementales non militaires
-	Mil = Organisations gouvernementales militaires
-	Arpa = DNS inverse
-	« xx » code de pays à deux lettres.

La délégation du DNS :
-	Déléguer la gestion d’un domaine DNS à un nombre d’organisations ou départements au sein d’une organisation.
-	Besoin de distribuer la charge de maintenance d’une grande base de données DNS entre plusieurs serveurs DNS pour améliorer les performances de résolution de nom, et créer un environnement à tolérance de panne DNS.
-	Nécessaire pour permettre l’affiliation d’organisation d’un hôte en incluant l’hôte dans les domaines appropriés.
 
![](https://github.com/TL72X211/UE2-Prosit-3-Acces-web-DNS-HTTP/blob/Emilien/Images_Prosit/2.png)


Il existe trois endroits où on retrouve les noms de domaines, dans une zone :
-	Principale : Toutes les MAJ pour les enregistrements qui appartiennent à cette zone = Serveur DNS principal.
-	Secondaire : Une copie de la zone principale. MAJ auto.
-	Stub : Copie en lecture seule de la zone principale, qui contient uniquement les enregistrements de ressources qui identifient les serveurs DNS qui font autorités.

Transfert de zone :
Il se produit des copies de fichiers de zones entre les serveurs DNS, fait à partir des principaux ou des secondaires. Le serveur DNS maître envoie une notif vers un ou plusieurs serveurs DNS secondaires d’un changement dans le fichier zone. Les serveurs DNS secondaires interrogent à chaque fois qu’une expiration est faite (TTL) les serveurs principaux pour connaître l’état des noms, et MAJ si besoin.

On peut faire des transferts de zones par :
-	Complet (AXFR)
-	Incrémental, qui n’envoi que les modifiés (IXFR)

Comment interagir avec notre base de données ? :
On peut communiquer entre Client DNS et Serveur DNS, ou de Serveur DNS à Serveur DNS.
-	Récursive : Force un serveur DNS pour répondre à une demande avec une défaillance ou une réponse de succès. C’est le cas des clients (résolveurs). Le serveur DNS doit contacter les autres serveurs DNS pour connaitre la réponse (vers le maître la majorité du temps, ou la ‘racine’), et il envois ensuite sa réponse vers le client.
-	Itérative : Prévu pour répondre avec les meilleures informations locales. Si le DNS n’a pas la réponse, il envois juste au client une réponse négative.
 
![](https://github.com/TL72X211/UE2-Prosit-3-Acces-web-DNS-HTTP/blob/Emilien/Images_Prosit/3.png)


Le TTL :
Time to leave, c’est dans un enregistrement de ressources, un intervlle de temps utilisé par d’autres serveurs DNS pour déterminer combien de temps en cache les informations sont conservés avant d’expirer. Le minimum est d’une heure. Il vaut mieux le mettre long, en vue de ne pas avoir des informations périmées, et diminuer le trafic réseau (moins de requêtes entre DNS pour trouver un hôte)

![](https://github.com/TL72X211/UE2-Prosit-3-Acces-web-DNS-HTTP/blob/Emilien/Images_Prosit/4.png)

![](https://github.com/TL72X211/UE2-Prosit-3-Acces-web-DNS-HTTP/blob/Emilien/Images_Prosit/5.png)
 
 
**PROTOCOLE**

Il existe trois types de messages DNS :
-	Message
-	Réponses
-	Mises à jour 
Ils suivent tous trois un format de message courant :
Un entête de 12 octets de longueur fixe et une position variable réservée à la question, réponse, autorité et des enregistrements de ressources DNS supplémentaires.
 
![](https://github.com/TL72X211/UE2-Prosit-3-Acces-web-DNS-HTTP/blob/Emilien/Images_Prosit/6.png)

Dans l’entête DNS pour une requête :
-	ID Transaction [16 bits]
-	Indicateurs [16 bits] 
-	Demande / réponse [1 bit] : 0 pour une demande, et 1 une réponse
-	Code d’opération [4 bits] : Opération de service de nom du paquet, équivalent du flag
-	Réponse faisant autorité [1 bit] : Indique que le répondeur fait autorité pour le nom de domaine dans le message de requête.
-	Troncature [1 bit] : passe à 1 si le nombre total de réponses dépasse le datagramme UDP (User Datagram Protocol).
-	Récursivité souhaitée [1 bit] : 1 pour récursive, et 0 pour itératives.
-	Récursivité disponible [1 bit] : indique si le serveur DNS peut traiter les requêtes récursives.
-	Réservé [3 bits] : Tout est défini sur 0
-	Code de retour [4 bits] : 0 = OK, 0x3 = erreur de nom, càd que le domaine n’existe pas.
-	Nombre d’enregistrements de ressources de questions [16 bits] : Nb d’entrées dans la section de la question du message DNS
-	Nombre d’enregistrements de ressources de réponse [16 bits] : Nb d’entrées dans la section réponse du message DNS
-	Nombre d’enregistrements de ressources autorité [16 bits] : ‘’ ‘’ ressources autorités
-	Nombre d’enregistrements de ressources supplémentaire [16 bits] : ‘’ ‘’ ressources supplémentaires.

Pour l’enregistrement de questions, réponses, autorités, et supplémentaires, on retrouve les détails sur le lien suivant : https://technet.microsoft.com/fr-fr/library/dd197470(v=ws.10).aspx
Dans l’entête DNS pour une MAJ :
-	Identification [16 bits] : Affecté par le demandeur de client DNS. C’est un identificateur qui est copié dans la réponse correspondante, permet d’identifier les demandes dupliquées.
-	Indicateurs [16 bits] : ?
-	Nombre d’entrées de zone [ ? ] : Le nombre d’enregistrements de ressources dans la section d’entrée de zone :
-	Nombre d’enregistrements de ressources requis [ ?]
-	Nombre ‘’ ‘’ ressources MAJ [ ? ]
-	Nombres ‘’ ‘’ ressources supplémentaires [ ? ]
-	Entrée de zone : Désigne la zone des enregistrements mis à jour. 
-	Enregistrements de ressources requis [ ?] / Ensemble de conditions qui doivent être remplis au moment que le message de MAJ est reçu par le DNS maître.
-	Mettre à jour enregistrement de ressources [ ? ] : Contient les ressources qui doivent êtres ajoutés, ou supprimés de la zone. 
-	Demande / Réponse [1 bit] : 1 pour demande / réponse
-	Code d’opération [4 bits] :  0 x 5 pour MAJ DNS
-	Réservé [7 bits] : Définie à 0
-	Code de retour [4 bits] : Statut de la requête de MAJ (+erreurs)



**Protocole http**
HyperText Transfer Protocol, est un protocole de communication client-serveur développé pour le WWW. C’est un langage qui va permettre au client de communiquer avec un serveur connecté.
C’est un protocole extensible, facile utilisation, avec la possibilité d’ajouter simplement des entêtes, et de progresser au fur et à mesure de l’ajout de nouvelles fonctionnalités sur le web.
Son n° de port est le 80, et on parle aussi de HTTPS pour le côté sécure (SSL ou TLS) avec port 443.
Utilisation :
 
 ![](https://github.com/TL72X211/UE2-Prosit-3-Acces-web-DNS-HTTP/blob/Emilien/Images_Prosit/7.png)
 
![](https://github.com/TL72X211/UE2-Prosit-3-Acces-web-DNS-HTTP/blob/Emilien/Images_Prosit/8.png)
 
![](https://github.com/TL72X211/UE2-Prosit-3-Acces-web-DNS-HTTP/blob/Emilien/Images_Prosit/9.png)
 
![](https://github.com/TL72X211/UE2-Prosit-3-Acces-web-DNS-HTTP/blob/Emilien/Images_Prosit/10.png)
 


GET /fichier.ext?variable=valeur&variable2=valeur2 HTTP/1.1
On utilise les ‘ ? ’pour séparer la liste des variables, et un & pour annoncer une autre variable.
Pour les utiliser, on doit utiliser des sockets, par exemple en PHP. Il s’appuie sur du TCP pour faire circuler les requêtes.
**Fonctionnement de nslookup**
> nslookup www.wikipedia.org
 Serveur :  dns1.proxad.net
 Address:  212.27.40.240
 
 Réponse ne faisant pas autorité :
 Nom :    rr.esams.wikimedia.org
 Address:  91.198.174.2
 Aliases:  www.wikipedia.org
           rr.wikimedia.org

**Organismes gérant les protocoles**
C’est l’IANA, du département de l’ICANN, une société américaine privée à but non lucratif qui supervise l’allocation globale des @IP, la gestion de la zone racine dans le DNS. (DNS qui répond aux requêtes, et qui redirige vers le serveur DNS du premier niveau concerné, càd .com, .fr, .net …). Elle s’occupe également des numéros de protocoles, et de nombreux protocoles IP. C’est elle qui délivre la liste des numéros de ports TCP et UDP.
En France, c’est l’AFNIC (Association Française pour le nomage Internet en coopération), qui gère les domaines internet nationaux de premier niveau).

**Théorie de communication**
Il existe plusieurs modèles sur la théorie de la communication, ils peuvent-être consultés sous le lien suivant : http://olivier-moch.over-blog.net/article-les-modeles-de-communication-72295675.html

**Format des messages (émission/réception)**
???

**Protocoles :**
 
 ![](https://github.com/TL72X211/UE2-Prosit-3-Acces-web-DNS-HTTP/blob/Emilien/Images_Prosit/11.png)

APPLICATION  : 

NOM SYSTÈME : 

DNS : Domain Name Service – Traduit les noms de domaines comme cisco.com en adresse IP

CONFIGURATION D'HOTE :

BOOTP : Bootstrap Protocol : Permet à une station sans disque de travail de découvrir sa propre adresse IP, l'adresse IP d'un BOOTP serveur sur le réseau. Un fichier peut être chargé dans la mémoire de démarrage de la machine. -> Remplacé par DHCP

DHCP : Dynamic Host Configuration Protocol : Assigne dynamiquement des adresses IP aux clients au démarrage. Permet de réutiliser les adresses quand elles ne sont plus utilisées.

EMAIL :

SMTP : Simple Mail Transfert Protocol - Autorise les clients à envoyer des email vers les mail server, mais aussi les ses server vers les autres server

POP (POP3) : Post Office Protocol - Autorise les clients à retrouver leur email à partir d'un mail serveur télécharge les email de l'email server vers le bureau.

IMAP : - Internet Message Access Protocol  - Autorise les clients à accéder à leur email enregistré dans un mail server et maintient les email sur le serveur.

TRANSFERT DE FICHIER :

FTP : - File Transfert Protocol - Définit les règles qui autorisent un utilisateur sur un hôte à accéder et transférer les fichiers depuis et vers un autre hôte sur un réseau. Fournit également des fichiers importants.

TFTP : - Trivial File Transfer Protocol – Un protocole sans connexion, sans retour d'accusé de réception - Utilisé moins que le FTP

WEB :

HTTP : HypertText Transfer Protocol - Définit les règles d'échanges de textes, des images, de sons, de vidéos et autres fichiers multimédias sur le WWW.

TRANSPORT : 
UDP : User Datagram Protocol – Autorise un processus qui tourne sur un hôte à envoyer des paquets à un autre processus sur un autre hôte. N'a pas de confirmation qu'une transmission datagram a bien été effectuée.

TCP : Transmission Control Protocol – Autorise des communications fiables entre les processus tournant sur des hôtes séparés. Fiable, il y a des accusés de réceptions.

INTERNET 
IP : Internet Protocol - Reçoit les segments de messages des couches transports, paquette les messages, adresse les paquets pour les "end device".

NAT : Network Address Translation -  Transforme les adresses IP privés dans une adresse IP publique.
IP SUPPORT

ICMP : Internet Control Message Protocol – Fournit un feedback depuis une destination hôte vers une source hôte, à propos des erreurs dans le délivrement des paquets.

ROUTING PROTOCOLS 
OSPF : Open Shortest Path First – Relie l'état d'un protocole de routage. Désign hiérarchique basé sur des zones. Ouvre un intérieur standard pour les protocoles de routages.

EIGRP : Enhanced Interior Gateway Routing Protocol – La propriété de Cisco sur le routage, utilise des composés métriques basé sur la bande passante, les délais, le chargement et la fiabilité.

ACCES RESEAU 
ARP : Adress Resolution Protocol – Fournit une adresse dynamique mappé, entre une IP adresse, et un accès physique.

PPP : Point-to-Point Protocol – Fournit un semblant de paquets d'encapsulations pour la transmission sur une liaison série.

Ethernet : Définit les règles pour le câblage et le signalement des standards d'un réseau accédant aux couches.

Interface Drivers : Fournit des instructions à la machine pour contrôler une certaine interface sur un équipement réseau.


**Les treize serveurs racines**
Neuf de ces serveurs ne sont pas de simples machines mais correspondent à plusieurs installations réparties dans des lieux géographiques divers, il y a ainsi plus de 130 sites dans 53 pays qui hébergent un serveur racine du DNS, grâce  à la technologie « anycast »
 
C’est les Etats-Unis qui gèrent les serveur racines.




![](https://github.com/TL72X211/UE2-Prosit-3-Acces-web-DNS-HTTP/blob/Emilien/Images_Prosit/12.png)






**Complément sur les virtual Hosts sous Appache2 **
C’est donc sur la même @IP, plusieurs sites internet, ou nom de domaine.
http://www.installerunserveur.com/creer-des-virtualhost
-	/etc/apache2/sites-available
-	/etc/apache2/sites-enabled
 
![](https://github.com/TL72X211/UE2-Prosit-3-Acces-web-DNS-HTTP/blob/Emilien/Images_Prosit/13.png)


**WORKSHOP **

![](https://github.com/TL72X211/UE2-Prosit-3-Acces-web-DNS-HTTP/blob/Emilien/Images_Prosit/14.png)
 
http://tvaira.free.fr/reseaux/tp10-dns.pdf
/etc/hosts : C’est l’@ FQDN de chaque machine du réseau ainsi que son @IP. 
/etc/host.conf :  On détermine dans quel ordre se fera la résolution de nom sur notre machine, ici il est en « muli on ».
/etc/resolv.conf : On y retrouve l’adresse IP du serveur de nom DNS que le résolveur intérrogera. C’est-à-dire quel DNS interroger. 
Par exemple, pour le serveur 8.8.8.8 (Google DNS), on écrira : nameserver 8.8.8.8

La commande ‘host’ permet de connaître l’@IP lié à un nom d’hôte.
Dans notre cas 194.2.77.162 = @IP DE www.cesi.fr
Si on tape ‘host -v [nom de domaine]’ on trouve des informations complémentaires.

En utilisant ‘dif’ www.cesi .fr : On obtient de nombreuses informations, comme si c’est une IPV4 (un A) ou une IPV6 (AAA), ou s’il supporte la récursivité (AA). On peut regarder la première ligne qui nous indique, via les flags, s’il supporte la récursivité, ou il sa réponse fait réponse d’autorité.

Dig +trace www.lasalle84.org -> Tracer la suite des serveurs contactés pour trouver l’@IP de lasalle84.org. On peut voir qu’il passe par tous les serveurs racines.
On remarque qu’il ne passe pas par le même ordre à chaque exécution.
dig system-linux.eu +trace


dig ns @a.root¬servers.net. org -> permet de connaître qui est en charge de la zone org

Les enregistrements SOA (Start Of Authority) donnent les informations générales de la zone (Serveur principal, courriel…)

Connaître le TTL -> « dig www.cesi.fr »
Ou 	« host -a -t aaaa www.cyberciti.biz »
Connaître le SOA : dig -t aaaa www.cesi.fr

CNAME = permet de faire un alias. Ex : dig yahoo.fr est un CNAME.

Dix mx www.cesi.fr -> Déterminer le ou les serveurs d’échange de courrier.
OU 
Nslookup
Set type = mx
Cesi.fr

On obtient les @IP des deux serveurs de messagerie du CESI.
 
![](https://github.com/TL72X211/UE2-Prosit-3-Acces-web-DNS-HTTP/blob/Emilien/Images_Prosit/15.png)

Dig -x [@IP] permet de trouver un nom d’hôte à partir d’une @IP.

**Canaux de communication**
3 types :
-Cuivre
-Fibre optiques
-Ondes

Les canaux sont les moyens par lesquels un message est transmis. C'est un media.

