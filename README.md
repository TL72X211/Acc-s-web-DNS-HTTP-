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
  
  **Flo** sur definition et hiérarchie
  **Nico** sur les type d'enregistrement

  * Protocole HTTP
  
  **Pierre M**
  
  Requête:
  
  * GET demande un fichier
  * HEAD info sur la ressource
  * POST modifie une ressource
  * CONNECT : utiise un proxy comme tunnel de communication
  * TRACE : retourne ce qu'il a reçu
  * PUT : ajouter une ressource
  * DELETE : suppr une ressource
  
  
  requête :
  * ligne de commande 
  * en-tête
  * corps de requête
  
  réponse:
  * ligne de statut
  * entête
  * corps de réponse
  
  
  **Raph**
  
  paramètres des en-têtes (défini ce qu'on autorise ou demande):
  
  accept: type de contenu accéptés par le navigateur
  accetp char-set : jeu de caractère accepté
  accept encoding : encodage accepté
  language : language
  content encoding : encodage
  coentent length : longeur du corp de la requête
  date : date de début du transfert
  
  etc

  Port : 
  * 80 http
  * 443 https
  
  portocole:
  * http utilise tcp
  * dns utilise udp ou tcp
  
  100 = informtion
  200 = ok
  300 = redirection
  400 = erreur ressource
  500 = erreur serveur
  
  
  seveur: propose un service
  http://www.truc.fr
  on passe www.truc.fr en argument du protocole
  
  note : un server html ne peut pas faire de php par défaut 
  
  
  
  * Fonctionnement de mslookup
  * Organismes gérant les protocoles
   * ICANN gère les DNS et sa branche IANA IP aux USA
   * IEEE 
   * IETF internet engineering taskforce
   * AFNIC IP en france
   * Les registrar qui vendent des noms de domaines (font le relai avec l'ICANN)
  * Théorie de communication
  
  on a un canal (media)
  éméteur
  recepteur
  un message 
  et des règles de communication
  
  pour http on a donc 
  * canal :
  * récepteur : serveur
  * éméteur : navigateur
  * langage : structure de la reqête
  * message : post paramètres
  
  
  * Format des messages (émission/réception)
    
    TO DO
    
  * Messages
  * Canaux de communication
  
      * cuivres
      * fibres
      * ondes
      
  * Couches des différents protocoles
  
  HTPP et DNS sont dans application
  
  Pierre M
  
  ICMP : protocole utilisé par ping
  ARP : lie une adresse MAC à un hôte
  802.2, .3, .4, .5 normes ISO
  
  * Implémentation des protocoles
  
  en-tête DNS:
  
  émilien

  récursivité : si le serveur peut demander à un autre serveur
  
  itérative vs récursive : 
  * récursive : attends une réponse
  * itérative répond au mieux avec ses informations locales 
  
  serveurs dns
  bind9
  opendns
  answerx
  le service dns de microsft
  
  serveurs http :
  apache
  enginex
  light
  
  
###Réalistions
* Résoudre le problème 
* Connaitre "les 13"

 hugo
