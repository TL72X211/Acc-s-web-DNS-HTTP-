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
   * Nslookup
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
 * Appache et IIS sont des paquets qui permettent de construire un serveur
 * On ne peut demander au FAI de mettre à jour un DNS nous correspondant
 * OVH donne les noms de domaines
   
## Plan d'action

### Études
  * DNS
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
