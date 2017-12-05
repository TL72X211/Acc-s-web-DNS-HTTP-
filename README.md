**Accès web (DNS, HTTP)**
--------------------------

##Team
   * Animateur : **Hugo**
   * Secrétaire : **Emilien**
   * Scribe : **Nico**
   * Gestionnaire : **Max**


## Mots Clés
   * DNS : Domain Name System
   * Appache : Serveur HTTP le plus répandu sur Internet
   * HTTP : Hyper Text Transfer Protocol, protocole de communication Client-Serveur développé pour le Web, il utilise le port 80 par défaut
   * Nslookup : Commande permettant de diagnostiquer l'infrastructure du système de nom de domaine (DNS)
   * FAI : Fournisseur d'accès Internet
   * FQDN : Nom de domaine révélant la position absolue d'un nœud dans une arborescence DNS en indiquant tous les domaines de niveau supérieur jusqu'à la racine. Par convention, le FQDN est ponctué par un point final. (ex : commons.wikimedia.org.)
   * nginix, appache, iis : Nginx est un logiciel libre de serveur Web, Apache est le serveur HTTP le plus répandu sur Internet, IIS (prononcé 2 I S) est un serveur Web (FTP, SMTP, HTTP, etc.) des différents systèmes d'exploitation Windows NT.
   * registrar : Bureau d'enregistrement, société ou association gérant la réservation de noms de domaine Internet
   * Virtual Host : 
   * enregistrement DNS de type A
   * résolution de nom : Fait souvent référence au DNS
   * adresse IP 8.8.8.8 : Adresse DNS de google
    

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
  A l'époque lorsque Internet était un petit réseau de l'US Department of Defense, les noms d'hôtes étaient gérés grâce à un fichier HOSTS sur un serveur central, téléchargeait ce fichier pour résoudre les noms d'hôtes.
  Le nombre d'utilisateurs augmentant, DNS fut inventé et les noms d'hôtes résident dans une base de donnée réparti entre plusieurs serveurs réduisant la charge sur chacun.
  
  Le DNS permet d'associer des noms de langage courant aux adresses numériques (194.153.205.26 = www.commentcamarche.net)
  La corrélation entre les deux s'appelle résolution de noms de domaines

  D'une adresse IP le DNS donne le nom du domaine (le FQDN) et inversement, à partir d'un nom de domaine, le DNS sait retrouver l'adresse IP

  On dit que le serveur DNS d'un réseau a autorité sur ce réseau


  * Protocole HTTP
  * Fonctionnement de mslookup
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