**Accès web (DNS, HTTP)**
--------------------------
#TO DO

* installer apache
* créer un virtual host 
* et des sites web
* dl postman
* faire des requêtes (éventuellement sur newbiecontest)
* rechercher les DNS secure

##Team
   * Animateur : **Max**
   * Secrétaire : **Emilien**
   * Scribe : **Nico**
   * Gestionnaire : **Hugo**


## Mots Clés
   * DNS: domain name system
   * Appache: serveur http libre
   * HTTP: hypertext transfer protocole
   * Nslookup: programme de troubleshooting
   * FAI: fournisseur d'accès internet
   * FQDN: fully qualified domain name (ex: wikipedia.fr)
   * nginix, appache, iis: serveur http libre (détail émilien)
   * registrar: métier: vendreles domaines au grand publique
   * Virtual Host: ouil permettant d'héberger plusieurs noms de domaine (sur le même IP) dans apache on associe un port à un nom de machine
   * /etc/site-available : commande permet de voir les sites web gérés par le VHost
   * enregistrement DNS de type A : lie un FQDN ipv4
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
 * nslookup donne le domaine dans lequel on est et nous donne l'adresse IP correspondante
 * Appache et IIS sont des paquets qui permettent de construire un serveur
 * On ne peut demander au FAI de mettre à jour un DNS nous correspondant
 * OVH donne les noms de domaines
   
## Plan d'action

### Études

* DNS
Le système DNS (Domain Name System) est un système hiérarchique décentralisé de dénomination d'ordinateurs, de services ou d'autres ressources connectées à Internet ou à un réseau privé. Il associe diverses informations aux noms de domaine attribués à chacune des entités participantes. Plus important encore, il traduit plus facilement les noms de domaines mémorisés en adresses IP numériques nécessaires pour localiser et identifier les services et dispositifs informatiques avec les protocoles de réseau sous-jacents. En fournissant un service d'annuaire distribué dans le monde entier, le système de noms de domaine est un composant essentiel de la fonctionnalité sur Internet, qui est utilisé depuis 1985. Il offre une zone de recherche directe.
Enregistrement type A -> IPv4
		type AAAA -> IPv6
		type CNAME -> Alias
    MX -> eMail
	  PTR ->  A
	  SOA -> Retour authority



* Protocole HTTP

Le protocole HTTP (Hypertext Transfer Protocol) est un protocole d'application pour les systèmes d'information distribués, collaboratifs et hypermédias. HTTP est le fondement de la communication de données pour le web.
Voici toutes les méthodes existantes de ce protocole :
GET, HEAD, POST, OPTIONS, CONNECT, TRACE, PUT, DELETE, PATCH

La méthode GET demande une représentation de la ressource spécifiée. Les requêtes utilisant GET devraient uniquement récupérer des données et ne devraient avoir aucun autre effet. (Cela est également vrai pour d'autres méthodes HTTP.)

La méthode HEAD demande une réponse identique à celle d'une requête GET, mais sans le corps de la réponse. Ceci est utile pour récupérer des méta-informations écrites dans les en-têtes de réponse, sans avoir à transporter tout le contenu.

La méthode POST demande que le serveur accepte l'entité incluse dans la requête en tant que nouveau subordonné de la ressource Web identifiée par l'URI (Uniform Ressource Identifier).

La méthode PUT demande que l'entité incluse soit stockée sous l'URI fournie. Si l'URI fait référence à une ressource déjà existante, elle est modifiée; Si l'URI ne pointe pas vers une ressource existante, le serveur peut créer la ressource avec cet URI.

La méthode DELETE supprime la ressource spécifiée.

La méthode TRACE fait écho à la demande reçue afin qu'un client puisse voir quelles modifications ou ajouts ont été apportés (le cas échéant) par des serveurs intermédiaires.

La méthode OPTIONS renvoie les méthodes HTTP que le serveur prend en charge pour l'URL spécifiée. Cela peut être utilisé pour vérifier la fonctionnalité d'un serveur Web en demandant '*' au lieu d'une ressource spécifique.

La méthode PATCH applique des modifications partielles à une ressource.


* Fonctionnement de mslookup

NSLOOKUP est une application de recherche d'informations dans le DNS (Domain Name System [RFC1034, RFC1035, RFC1033]). L'utilitaire NSLOOKUP est un outil Unix.
Fondamentalement, DNS mappe les noms de domaine aux adresses IP.
Bien que ce service en ligne Web puisse interroger un serveur DNS spécifique, dans la plupart des cas, il peut être suffisant et pratique d'utiliser simplement le serveur de noms par défaut KLOTH.NET "ns.kloth.net" ou "localhost" /127.0.0.1.
Pour résoudre une adresse IP par recherche inversée (obtenir le nom d'un ordinateur si vous n'avez que son adresse IP), essayez d'exécuter une requête PTR au lieu de ANY. Cette recherche inversée ne fonctionnera que si le propriétaire de l'adresse IP a inséré un enregistrement PTR dans le DNS. L'information PTR est informelle seulement et elle peut être la plupart du temps vraie, mais parfois non. Si vous n'obtenez pas d'informations PTR sur un ordinateur spécifique à partir d'une requête NSLOOKUP, vous pouvez essayer notre service whois pour trouver le propriétaire de cette adresse IP.


* Organismes gérant les protocoles

L'IANA (Internet Assigned Numbers Authority) est un département de l'ICANN, une société américaine privée à but non lucratif qui supervise l'allocation d'adresses IP globales, l'attribution de numéros de système autonomes, la gestion des zones racine dans le DNS, les types de média et autres symboles liés et numéros d'Internet.
Avant que l'ICANN ne soit créée à cet effet en 1998, l'IANA était principalement administrée par Jon Postel à l'Institut des sciences de l'information (ISI) de l'Université de Californie du Sud (USC) à Marina Del Rey (Los Angeles). ISI avait avec le département de la Défense des États-Unis, jusqu'à ce que l'ICANN soit créée pour assumer la responsabilité en vertu d'un contrat du département du Commerce des États-Unis. Suite à la transition de l'ICANN vers un modèle de gouvernance multipartite mondial, les fonctions de l'IANA ont été transférées à Public Technical Identifiers, un affilié de l'ICANN.
En outre, cinq registres Internet régionaux délèguent des ressources numériques à leurs clients, aux registres Internet locaux, aux fournisseurs de services Internet et aux organisations d'utilisateurs finaux. Un registre Internet local est une organisation qui attribue des parties de son allocation d'un registre Internet régional à d'autres clients. La plupart des registres Internet locaux sont également des fournisseurs de services Internet.


* Théorie de communication
//

* Format des messages (émission/réception)

Un exemple de canal simplex est la radiodiffusion telle la radio FM. Les informations sont envoyées à partir d'une station émettrice et reçues sur un poste. Les auditeurs ne peuvent pas répondre.

La liaison half-duplex peut être comparée à une communication avec des talkies-walkies, l’un parle (l’autre ne peut parler en même temps) et lorsqu'il lâche le bouton (signal de fin de conversation) l’autre peut parler à son tour.

Le full-duplex est très souvent l'association de deux canaux simplex, de la même façon qu'une autoroute est l'association de deux routes à un seul sens. La liaison full-duplex peut également être comparée à une conversation téléphonique : les deux interlocuteurs peuvent parler en même temps.

* Messages



* Canaux de communication

Câbles Ethernet, fibre optique, wifi

* Couches des différents protocoles

![](https://supportforums.cisco.com/legacyfs/online/legacy/4/1/0/136014-proto.jpg)

* Implémentation des protocoles
  
  
  
###Réalistions
* Résoudre le problème 
* Connaitre "les 13"

Les 13 sont les 13 serveurs DNS dans le monde

![](http://2.bp.blogspot.com/-Y_AY6xG9D3o/T3YI0b-vEeI/AAAAAAAAFdE/pF3lGt7qbVw/s640/DNS+root+servers.gif)
