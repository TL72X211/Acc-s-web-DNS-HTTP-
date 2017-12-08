**Accès web (DNS, HTTP)**
--------------------------
##Team
   * Animateur : **Hugo**
   * Secrétaire : **Emilien**
   * Scribe : **Nico**
   * Gestionnaire : **Max**


## Mots Clés
   * DNS
   * Appache
   * HTTP
   * Nhookup
   * FAI
   * FQDN
   * nginix, appache, iis
   * registrar
   * Virtual Host
   * enregistrement DNS de type A
   * résolution de nom
   * adresse IP 8.8.8.8
    

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
 * mslookup donne le domaine dans lequel on est et nous donne l'adresse IP correspondante
 * Appache et IIS sont des paquets qui permettent de construire un serveur
 * On ne peut demander au FAI de mettre à jour un DNS nous correspondant
 * OVH donne les noms de domaines
   
## Plan d'action

### Études
  * DNS

Le Domain Name System (ou DNS, système de noms de domaine) est un service permettant de traduire un nom de domaine en informations de plusieurs types qui y sont associées, notamment en adresses IP de la machine portant ce nom. 
Le port utilisé par ce protocole est le 53. Il utilise le protocole UDP. La taille maximale de paquets est de 512 octets. Le protocole DNS est basé sur le protocole UDP mais peut aussi utiliser TCP.

Il existe plusieurs types d'enregistements DNS:
   -  **A record** ou address record (également appelé enregistrement d’hôte) qui fait correspondre un nom d'hôte ou un nom de domaine ou un sous-domaine à une adresse IPv4 de 32 bits distribués sur quatre octets ex: 123.234.1.2 ;
   -  **AAAA record** ou IPv6 address record qui fait correspondre un nom d'hôte à une adresse IPv6 de 128 bits distribués sur seize octets ;
   -  **CNAME record** ou canonical name record qui permet de faire d'un domaine un alias vers un autre. Cet alias hérite de tous les sous-domaines de l'original ;
   -  **MX record** ou mail exchange record qui définit les serveurs de courriel pour ce domaine ;
   -  **PTR record** ou pointer record qui associe une adresse IP à un enregistrement de nom de domaine, aussi dit « reverse » puisqu'il fait exactement le contraire du A record ;
   -  **NS record** ou name server record qui définit les serveurs DNS de ce domaine ;
   -  **SOA record** ou Start Of Authority record qui donne les informations générales de la zone : serveur principal, courriel de contact, différentes durées dont celle d'expiration, numéro de série de la zone ;
   -  **SRV record** qui généralise la notion de MX record, mais qui propose aussi des fonctionnalités avancées comme le taux de répartition de charge pour un service donné, standardisé dans la RFC 278221 ;
   -  **NAPTR record** ou Name Authority Pointer record qui donne accès à des règles de réécriture de l'information, permettant des correspondances assez lâches entre un nom de domaine et une ressource. Il est spécifié dans la RFC 340322 ;
   -  **TXT record** permet à un administrateur d'insérer un texte quelconque dans un enregistrement DNS (par exemple, cet enregistrement est utilisé pour implémenter la spécification Sender Policy Framework) ;
    d'autres types d'enregistrements sont utilisés occasionnellement, ils servent simplement à donner des informations (par exemple, un enregistrement de type LOC indique l'emplacement physique d'un hôte, c'est-à-dire sa latitude et sa longitude). Cet enregistrement aurait un intérêt majeur mais n'est malheureusement que très rarement utilisé sur le monde Internet.

Les DNS sont organisés en arbres. Les DNS racines sont nommés les "13". En dessous il y a les DNS TLD(Top Level Domains) qui gérent les domaines de premier niveau comme .org .com .net ou .info. Puis s'en suit les DNS qui gérent les autres domaines.

Les "13" utilisent la technique du "Round-Robin" pour se répartir la charge des requettes

![DNS_tree](http://www.inetdaemon.com/img/dns-hierarchy.gif)

Voici une entête DNS :

![entête](http://perso.citi.insa-lyon.fr/afraboul/net/cours017.png)

  * Protocole HTTP

Http signifie HyperText Transfer Protocol, il peut être accompagné d’un « s » pour Secure. C’est un protocole de communication client-server développé pour le World Wide Web. Le protocole HTTPS utilise les protocoles SSL et TLS pour sécuriser les données.
Http fait parti de la couche application dans le modèle OSI. Il utilise TCP pour le transport. Les ports principalement utilisés sont le 80 (http) et le 443(https). Il utilise le navigateur web comme client. 

Il existe 8 (principales) requêtes en http:

- GET demande un fichier
- HEAD info sur la ressource
- POST modifie une ressource
- CONNECT : utiise un proxy comme tunnel de communication
- TRACE : retourne ce qu'il a reçu
- PUT : ajouter une ressource
- DELETE : suppr une ressource
- OPTIONS: obtenir les options de communication d'une ressource ou du serveur
 
Voici une liste des paramètres qu'on peut placer dans les entêtes http afin de spécifier des options au destinataire:

- accept: type de contenu accéptés par le navigateur
- accetp char-set : jeu de caractère accepté
- accept encoding : encodage accepté
- language : language
- content encoding : encodage
- content length : longeur du corp de la requête
- date : date de début du transfert

Il existe des codes d'erreurs qui permettent d'identifier les problèmes (ou non) des requêtes. Ils sont placés dans l'entête de la requête.
- 100 = informtion
- 200 = ok
- 300 = redirection
- 400 = erreur ressource
- 500 = erreur serveur

![Schéma_http_dns](http://www.bases-hacking.org/images/web.jpg)

  * Fonctionnement de nslookup

nslookup est un programme informatique de recherche d'information dans le Domain Name System (DNS), qui associe nom de domaine et adresses IP. nslookup permet donc d'interroger les serveurs DNS pour obtenir les informations définies pour un domaine déterminé.

Par défaut nslookup indique les enregistrements de type A et CNAME. Si on ne lui fournit pas d'argument, la console rentre dans un mode interactive dans lequel on peut définir nos paramètre comme le type de requète (A, CNAME, PTR, MX, SOA, AAAA ...).
A l'heure actuelle, il n'est plus maintenu pour UNIX, il est donc conseillé d'utiliser à la place la commande "dig".

![nslookup](http://geek-university.com/wp-content/images/linux/nslookup_command_soa.jpg)

  * Organismes gérant les protocoles

- ICANN (Internet Corporation for Assigned Names and Numbers) gère les DNS
- IANA (Internet Assigned Numbers Authority) gére les IP aux USA
- IEEE (Institute of Electrical and Electronics Engineers)  joue un rôle très important dans l'établissement de normes. Ceci est fait par la IEEE Standards Association. Elle assure la publication de ses propres normes et des autres textes rédigés par des membres de son organisation.
- IETF (Internet Engineering Task Force). Le but du groupe est généralement la rédaction d'un ou plusieurs Request for comments (RFC), nom donné aux documents de spécification à la base d’Internet.
- AFNIC (Association française pour le nommage Internet en coopération) Elle a pour mission de gérer les domaines Internet nationaux de premier niveau de France (.fr), La Réunion (.re), Terres australes et antarctiques françaises (.tf), Mayotte (.yt), Saint-Pierre-et-Miquelon (.pm) et Wallis-et-Futuna (.wf). L'Afnic se définit également comme fournisseur de solutions techniques et de services de registre, elle est notamment le partenaire technique de nouveaux domaines génériques dont le .paris, le .bzh, le .alsace, le .ovh.


  * Théorie de communication

![schéma_comunication](https://image.slidesharecdn.com/schmadecommunication-130830092732-phpapp01/95/schma-de-communication-1-638.jpg?cb=1377854966)

  * Couches des différents protocoles

![couche_protocole_osi](http://www.machaon.fr/isn/reseaux/protocoles.png)

  * Implémentation des protocoles
  
Pour l'implémentation des protocoles DNS et HTTP, voici une liste des services qu'on peut utiliser pour créer des serveurs:

DNS :
- bind9
- opendns

HTTP :
- apache
- nginx
- lighttpd

###Réalistions
* Résoudre le problème 
* Connaitre "les 13"

Chaque DNS des "13" sont des "serveur racine du DNS". Un serveur racine du DNS est un serveur DNS qui répond aux requêtes qui concernent les noms de domaine de premier niveau (top-level domain, TLD) et qui les redirige vers le serveur DNS de premier niveau concerné.
Les domaines de premier niveau (par exemple .com, .org et .fr) sont des sous-domaines du domaine racine.
Un "serveur racine du DNS" est généralement utilisé pour désigner l'un des treize serveurs racine du DNS d'Internet géré sous l'autorité de l'ICANN.
Il y a 13 serveurs racine du DNS dont les noms sont de la forme lettre.root-servers.net (la liste est disponible sur root-servers.org) où lettre est une lettre comprise entre A et M. Douze organisations contrôlent ces serveurs, deux sont européennes (RIPE NCC et Autonomica), une japonaise (WIDE), les autres étant américaines. Neuf de ces serveurs ne sont pas de simples machines mais correspondent à plusieurs installations réparties dans des lieux géographiques divers, il y a ainsi plus de 130 sites dans 53 pays qui hébergent un serveur racine du DNS.

![13dns](https://i.stack.imgur.com/S8U3B.png)
