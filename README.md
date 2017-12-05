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
 * nslookup donne le domaine dans lequel on est et nous donne l'adresse IP correspondante
 * Apache et IIS sont des paquets qui permettent de construire un serveur
 * On ne peut demander au FAI de mettre à jour un DNS nous correspondant
 * OVH donne les noms de domaines
   
## Plan d'action

### Études :
####**DNS**
Rôle : paire un nom de domaine à une adresse IP 

Avant DNS la résolution de nom se faisait à l’ide d’un fichier texte appelé HOST.TXT maintenu par le NIC (network information center) du Stanford Research Institut

Le DNS (Domain Name System) est un service qui permet d'effectuer la résolution de noms, c'est à dire d'associer une adresse IP à un FQDN (Full Qualified Domain Name) et inversement.

Un FQDN est composé d‘un nom d’hôte et d’un nom de domaine, exemple : www.google.com est un FQN où www est le nom d’hôte et google.com est le nom de domaine

Les noms de domaine sont organisés de manière hiérarchique le domaine se trouvant le plus haut dans la hiérarchie est « . » il est omispar le FQDN on trouve en dessous dans la hiérarchie les TLD
Ce nom a la structure ww.xx.yy.zz soit une suite d'éléments séparés par des points. Chaque élément est fait des lettres de l'alphabet, chiffres et/ou trait d'union, et ne peut excéder 63 caractères. L'ensemble d'un FQDN ne peut excéder 255 caractères.

Domaine de premier niveau (TLD): sous domaine de la racine, est le dernier label du nom de domaine ( .com, .org, .fr) il devrait être suivi d’un point mas on l’omet dans l’usage courrant
Il existe approximativement 560 domaines de premier niveau
260 nationaux
300 génériques 

####Hiérarchie du DNS :
Le système DNS est une hiérarchie donc le sommet est la racine représentée par un point
On peut créer un ou plusieurs sous-domaines dans un domaine et une délégations de ceux-ci ( indication que les info relatives à ce sous-domaine sont enregistrées sur un autre serveur, tous les sous-domaines ne sont pas nécessairement dlégués
Les délégation créent des zones : ensembles de domaines et leurs sous-domaines non délégués
Les domaines sous la rcines sont appelés Top Level Domains(TLD) si ils correspondent à un pays ils sont appelés ccTLC (country cocde TLD) sinon génériques (gTLD)

####Types de résolution

Résolution de noms directe
Dans un réseau IP, lorsqu’une machine A veut communiquer avec une machine B, la machine A connaît le nom FQDN de B.
Par exemple, lorsqu’on navigue sur le net, on connaît en général le nom FQDN des serveurs qu’on visite (exemple www.microsoft.fr.).
Pour que A puisse communiquer avec B grâce au protocole IP, A va avoir besoin de connaître l’adresse IP de B.
A doit posséder un moyen d’effectuer la résolution de noms directe, c’est-à-dire un moyen de trouver l’adresse IP de B à partir de son nom qualifié.
Le résolveur est le programme chargé de cette opération.

Résolution de noms inverse
La machine B reçoit un datagramme IP en provenance de A. Ce datagramme contient l’adresse IP de A. B peut avoir besoin de connaître le nom FQDN de la machine A.
B doit donc être capable de trouver le nom FQDN de A à partir de son adresse IP. C’est ce qu’on appelle la résolution de noms inverse.
Le résolveur est également chargé de cette opération.

Résolution de nom par serveur DNS (Domain Name System)
On installe un serveur de noms sur le réseau. Chaque machine du réseau doit connaître l’adresse IP de ce serveur DNS. Dès qu’une machine veut effectuer une résolution de noms directe ou inverse, elle va interroger le serveur de noms. L’administrateur doit configurer le serveur de noms pour que ce dernier connaisse l’adresse IP et le nom de toutes les machines du réseau.




####**Protocole http**

Hypertext transfer protocol : protocole de communication client-serveur dévelopé pour le world wide web

Structure d’une requête :

Première ligne :

*	verbe
*	identifiant local de la ressource
*	version du protocole HTTP
*	En-têtes (suivis d’une ligne vide)
*	Contenu facultatif (selon le verbe)

Structure d’une réponse :

Première ligne

*	version du protocole HTTP
*	code de statut
*	libellé textuel
*	En-têtes (suivis d’une ligne vide)
*	Contenu facultatif (selon le code de statut)


####**Fonctionnement de mslookup**
####**Organismes gérant les protocoles**
####**Théorie de communication**
####**Format des messages (émission/réception)**
####**Messages**
####**Canaux de communication**
#####**Couches des différents protocoles**
#####**Implémentation des protocoles**
  
###Réalistions
####**Résoudre le problème** 
####**Connaitre "les 13"** 
Serveur racine du DNS est un serveur DNS qui réponds aux requêtes qui concernent les noms de domaines de premier niveau TLD) et les redirige vers le serveur DNS de premier niveau concerné

![](img/DNSracines.png)

Ils sont géré sous l’autorité de l’ICANN
 
