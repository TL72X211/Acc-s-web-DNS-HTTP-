*Prosit 2.3 - DNS, DHCP*

# Mots Clés

-	DNS
-	Apache
-	HTTP
-	NsLookup
-	FQDN
-	Nginix, apache, iis
-	Registrar
-	Virtual Host
-	Enregistrement DNS de type A
-	Résolution de nom
-	Adresse IP 8.8.8.8


# Problématique

-   *Comment faire en sorte que notre FAI reconnaisse notre DNS ?*

# Sommaire
### Etudes

-	DNS
-	Protocole HTTP
-	Fonctionnement de Nslookup
-	Organismes gérant les protocoles
-	Théorie de communication
-	Format des messages (émission/réception)
-	Messages
-	Canaux de communication
-	Couches des différents protocoles
-	Implémentation des protocoles

### Réalisations

-	Résoudre le problème
-	Connaitre "les 13"

# Etudes
### DNS

Le DNS (Domain Name System)
- Service permettant de traduire un nom de domaine vers une adresse IP.
- Utilise le port 53.
- Basé sur UDP
- Est organisé sous forme d'arbre (Voir Schéma)
    - Root Level
    - Top Level Domain (TLD)
    - Second Level Domain
    - Sub-Domain of Parent

Les types d'enregistrements DNS sont :
- A record ou address record (également appelé enregistrement d’hôte) qui fait correspondre un nom d'hôte ou un nom de domaine ou un sous-domaine à une adresse IPv4 de 32 bits distribués sur quatre octets ex: 123.234.1.2,
- AAAA record ou IPv6 address record qui fait correspondre un nom d'hôte à une adresse IPv6 de 128 bits distribués sur seize octets,
- CNAME record ou canonical name record qui permet de faire d'un domaine un alias vers un autre. Cet alias hérite de tous les sous-domaines de l'original,
- MX record ou mail exchange record qui définit les serveurs de courriel pour ce domaine,
- PTR record ou pointer record qui associe une adresse IP à un enregistrement de nom de domaine, aussi dit « reverse » puisqu'il fait exactement le contraire du A record,
- NS record ou name server record qui définit les serveurs DNS de ce domaine,
- SOA record ou Start Of Authority record qui donne les informations générales de la zone : serveur principal, courriel de contact, différentes durées dont celle d'expiration, numéro de série de la zone,
- SRV record qui généralise la notion de MX record, mais qui propose aussi des fonctionnalités avancées comme le taux de répartition de charge pour un service donné, standardisé dans la RFC 278221,
- NAPTR record ou Name Authority Pointer record qui donne accès à des règles de réécriture de l'information, permettant des correspondances assez lâches entre un nom de domaine et une ressource. Il est spécifié dans la RFC 340322,
- TXT record permet à un administrateur d'insérer un texte quelconque dans un enregistrement DNS (par exemple, cet enregistrement est utilisé pour implémenter la spécification Sender Policy Framework) ; d'autres types d'enregistrements sont utilisés occasionnellement, ils servent simplement à donner des informations (par exemple, un enregistrement de type LOC indique l'emplacement physique d'un hôte, c'est-à-dire sa latitude et sa longitude). Cet enregistrement aurait un intérêt majeur mais n'est malheureusement que très rarement utilisé sur le monde Internet.

En-tête de message de requète DNS
Nom de champ | Description
-------------|------------
**ID de transaction** | Un champ de 16 bits qui identifie une transaction DNS spécifique. L'ID de transaction est créée par l'expéditeur du message et est copié par le répondeur dans son message de réponse. À l'aide de l'ID de transaction, le client DNS peut correspondre à des réponses à ses demandes.
**Indicateurs :** | Un champ de 16 bits contenant divers indicateurs de service sont échangées entre le client DNS et le serveur DNS, y compris :
Demande/réponse | champ de 1 bit défini sur 0 pour représenter une demande de service de nom ou la valeur 1 pour représenter une réponse de service de nom.
Code d'opération | champ 4 bits représente l'opération de service de nom du paquet: 0 x 0 est une requête.
Réponse faisant autorité | Un champ de 1 bit indique que le répondeur fait autorité pour le nom de domaine dans le message de requête.
Troncature | Un champ de 1 bit défini sur 1 si le nombre total de réponses dépasse le datagramme UDP (User Datagram Protocol). Sauf si les datagrammes UDP supérieurs à 512 octets ou EDNS0 sont activés, seuls les 512 premiers octets de la réponse UDP sont renvoyés.
Récursivité souhaitée | champ de 1 bit défini sur 1 pour indiquer une requête récursive et 0 pour les requêtes itératives. Si un serveur DNS reçoit un message de requête avec ce champ la valeur 0, elle retourne une liste d'autres serveurs DNS que le client peut contacter. Cette liste est remplie à partir des données du cache local.
Récursivité disponible | champ de bits 1 défini par un serveur DNS à 1 pour représenter le serveur DNS peut traiter les requêtes récursives. Si la récursivité est désactivée, le serveur DNS définit le champ de manière appropriée.
Réservé | Champ de 3 bits qui est réservé et défini sur 0.
Code de retour | champ 4 bits contenant le code de retour : 0 est une réponse correcte (requête réponse est dans la réponse de requête). 0 x 3 est une erreur de nom, indiquant qu'un serveur DNS faisant autorité a répondu que le nom de domaine dans le message de requête n'existe pas. .
**Nombre d'enregistrements de ressource de question** | Un champ de 16 bits représentant le nombre d'entrées dans la section de la question du message DNS.
**Nombre d'enregistrements de ressource de réponse** | Un champ de 16 bits représentant le nombre d'entrées dans la section réponse du message DNS.
**Nombre d'enregistrements de ressource autorité** | Un champ de 16 bits représentant le nombre d'enregistrements de ressource d'autorité dans le message DNS.
**Nombre d'enregistrements de ressources supplémentaire** | Un champ de 16 bits représentant le nombre d'enregistrements de ressources supplémentaires dans le message DNS.

Réponse de requète DNS
Nom de champ | Description
-------------|------------
**Requête identificateur (ID de Transaction)** | Pour activer la résolution du client DNS faire correspondre la réponse à la requête, définissez un numéro unique.
**Indicateurs** | Ils définissent une requête standard avec récursivité activée.
**Nombre de question** | La valeur 1.
**Saisie de la question** | Pour renvoyer la valeur du nom de domaine interrogé et le type d'enregistrement de ressource.

### HTTP

Hyper Text Transfer Protocol
- Permet à un client de communiquer avec un server,
- utilise le port 443.

Communication avec le serveur se fait via des requêtes :
- GET - C'est la méthode la plus courante pour demander une ressource. Une requête GET est sans effet sur la ressource, il doit être possible de répéter la requête sans effet.
- HEAD - Cette méthode ne demande que des informations sur la ressource, sans demander la ressource elle-même.
- POST - Cette méthode doit être utilisée lorsqu'une requête modifie la ressource.
- OPTIONS - Cette méthode permet d'obtenir les options de communication d'une ressource ou du serveur en général.
- CONNECT - Cette méthode permet d'utiliser un proxy comme un tunnel de communication.
- TRACE - Cette méthode demande au serveur de retourner ce qu'il a reçu, dans le but de tester et d'effectuer un diagnostic sur la connexion.
- PUT - Cette méthode permet d'ajouter une ressource sur le serveur.
- DELETE - Cette méthode permet de supprimer une ressource du serveur.

Syntaxe des Requètes
- Ligne de commande (Commande, URL, Version de Protocole)
- En-tête de requète
- New Line
- Corps de requète

Syntaxe des Réponses
- Ligne de Status (Version, Code-réponse, texte-réponse)
- En-tête de réponse
- New Line
- Corps de réponse

Messages d'erreure pour le HTTP
- 100 = Information
- 200 = OK
- 300 = Redirection
- 400 = Err Ressource
- 500 = Err Serveur

### NSLOOKUP

nslookup est un programme informatique permettant d'interroger les serveurs DNS pour récuperer des informations. (Voir Image)

### Théorie de communication

Pour avoir une communication, il faut :
-	Une source,
-	Une destination,
-	Un media de transport de l’information,
-	Format de message,
-	Protocole (Règle d’échange).

### Couches de différents protocoles

(Voir Schéma)
