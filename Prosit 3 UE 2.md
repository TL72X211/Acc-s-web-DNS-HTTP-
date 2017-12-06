Accès web (DNS, HTTP)

##Team

    Animateur : Max
    Secrétaire : Emilien
    Scribe : Nico
    Gestionnaire : Hugo

Mots Clés

    DNS
    Appache
    HTTP
    Nhookup
    FAI
    FQDN : fully qualified domain name -> nom de domaine qui révèle la position absolue d'un noeud dans l'arborescence DNS en indiquant tous les domaines de niveau supérieur jusqu'à la racine.
    nginix, appache, iis
    registrar
    Virtual Host
    enregistrement DNS de type A
    résolution de nom
    adresse IP 8.8.8.8

Contexte
Quoi ?

    Panne/Réparer du serveur DNS du FAI
    Rétablir l'accès au site
    Rétablir le serveur DNS

Comment ?

    En réparant le problème avec le DNS

Pourquoi ?

    Pour pouvoir accéder à lemonde.fr

Contraintes

    aucune

Problématique

    Comment faire en sorte que notre FAI reconnaisse notre DNS

Généralisation

    MCO : maintenance en condition opérationnelle

Hypothèses

    8.8.8.8 est l'adresse du DNS de google
    mslookup donne le domaine dans lequel on est et nous donne l'adresse IP correspondante
    Appache et IIS sont des paquets qui permettent de construire un serveur
    On ne peut demander au FAI de mettre à jour un DNS nous correspondant
    OVH donne les noms de domaines

Plan d'action
Études

* DNS : 
	*  Protocole:
		* Le protocole DNS se décompose en différents types de messages DNS qui sont traités suivant les informations qu'ils contiennent dans leurs champs messages. 
		* Il existe plusieurs types de messages: les requêtes, les réponses et les mises à jour. Les requêtes et les réponses sont définis dans la norme DNS alors que mises à jour sont définies dans la RFC 2136. Les trois types suivent un format de message courant.
		* Le format de messages DNS commun a un en-tête de 12 octets de longueur fixe et une position variable réservée aux questions, réponses, autorités et enregistrements de ressources DNS supplémentaire. Il peut être illustré comme suis : 
			>* En-tête DNS (de longueur fixe);
			
			>* Entrées de la question (de longueur variable);
			
			>* Réponses des enregistrements de ressources (de longueur variable);
			
			>* Enregistrements de ressources d'autorité (de longueur variable);
		
			>* Enregistrements de ressources supplémentaire (de longueur variable);
			
		* L'en-tête du message DNS contient les champs suivants (dans cet ordre) :

		>**ID de transaction** : champ de 16 bits qui identifie une transaction DNS spécifique.
			
		>**Indicateur **: 
				* Demande/Réponse : champ de 1 bit défini sur 0 pour représenter une demande de service de nom ou 1 pour représenter une réponse de service de nom;
				* Code opération : champ de 4 bits représente l'opération de service de nom du paquet : 0x0 est une requête;
				* Réponse faisant autorité : champ de 1 bit qui indique que le répondeur fait autorité pour le nom de domaine dans le message de requête;
				* Troncature : champ de 1 bit défini sur 1 si le nombre total de réponse dépasse le datagramme UDP;
				* Récursivité souhaitée : champ de 1 bit défini sur 1 pour indiquer une requête récursive et 0 pour les requêtes itératives; 
				* Récursivité disponible : champ de 1 bit défini par un serveur DNS à 1 pour représenter le serveur DNS pouvant traiter les requêtes récursives;
				* Réservé : champ de 3 bits réservé et défini sur 0
				* Code de retour : champ de 4 bits contenant le code retour : 0 est une réponse correcte alors que 0x3 est une erreur de nom, indiquant qu'un serveur DNS faisant autorité a répondu que le nom de domaine dans le message de requête n'existe pas;

		> **Nombre d'enregistrements de ressource de question** :
				Champs de 16 bits représentant le nombre d'entrées dans la section de la question du message DNS.
		> **Nombre d'enregistrements de ressource de réponse ** :
				Champs de 16 bits représentant le nombre d'entrées dans la section de la réponse du message DNS.
		> **Nombre d'enregistrements de ressource autorité** : 
				Champs de 16 bits représentant le nombre d'entrées de ressource d'autorité dans le message DNS.
		> **Nombre d'enregistrements de ressource supplémentaire** :
			Champs de 16 bits représentant le nombre d'entrées d'enregistrement de ressource supplémentaires dans le message DNS.
			
		* Section entrées de la question des requêtes DNS : 
			La section contient le nom de domaine qui est interrogé et possède les trois champs suivants :
				
		* Enregistrements de ressource DNS :
			La réponse, autorité et informations supplémentaires les sections d'un messages de réponse DNS peuvent contenir des enregistrements de ressources qui répondent à la section de question de message de requête. Ils sont sous cette forme:
			
		* Format de message de requête de nom DNS :
			 Un format de message de requête de nom est le même que le format de message DNS. Dans un message de requête de nom classique, les champs sont définis comme suit :
			 
		* Format de message de réponse à la requête de nom:
			Un format de message de requête de nom est le même que le format de message DNS. Dans un message de requête de nom par défaut, ils sont fixée comme cela :
			
		* Format de message de requête de nom inversé :
			Inverser la requête de nom en utilisant le format de message courant en appliquant les modifications suivantes :
				* la résolution du client DNS construit le nom de domaine dans le domaine in-addr.arpa basé sur l'addresse IP qui est interrogé
				* Un enregistrement de ressource de pointeur est interrogé au lieu d'un enregistrement de ressource Hôte.
		* Format de message de mise à jour DNS:
			le serveur DNS utilise un en-tête de définition de l'opération de mise à jour à effectuer et un jeu d'enregistrements de ressource qui contient la mise à jour. Il comporte les champs suivant:
		
		* Champ d'indicateur de message de mise à jour DNS :
			Demande/réponse: champ de 1 bit défini sur 0 pour représenter une demande de MAJ et 1 pour représenter une réponse de MAJ ;
			Code d'opération : champ de 4 bit défini sur 0 x 5 pour les MAJ DNS ;
			Réservé : champ réservé de 7 bit défini sur 0 ;
			Code de retour : champ 4 bits contenant les codes pour représenter le résultat de la requête de MAJ. les codes sont : 
		* Format de message de réponse de mise à jour dynamique :
			le message de réponse de MAJ dynamique suit le même format que le serveur DNS à l'exception des indicateurs DNS. Ces indicateurs d'en-tête de message réponse  mise à jour dynamique indique si la MAJ est réussie en incluant le code de réponse de succès ou l'un des codes d'erreur décrit dans les indicateurs de message de MAJ DNS.
			
		* Architecture : 
			* l'architecture DNS est une base de données hiérarchique distribuée et associé à un ensemble de protocoles définissant : 
				>* Un mécanisme pour l'interrogation et mise à jour de la base de données ;
				>* Un mécanisme de réplication des informations dans la base de données entre les serveurs ;
				>* Un schéma de la base de données;
		* Noms de domaine DNS :
			>* Ce système de nom est implémenté comme base de données hiérarchique et répartie contenant différents types de données (noms d'hôtes et de domaine compris). 
			>* Les noms dans une base de données forment une structure d'arborescence hiérarchique appelée espace de noms de domaine. Les noms des domaines sont formé par les étiquettes individuelles séparées par des points.
			>* Un nom de domaine pleinement qualifié (FQDN) identifie la position de l'hôte dans l'arborescence DNS en spécifiant une liste de noms séparés par des points dans le chemin d'accès de l'hôte référencé vers la racine. 
* Compréhension de l'espace de noms de domaine DNS :
			>L'espace de noms de domaine est basé sur le concept d'une arborescence de domaines nommés. Chaque niveau de l'arborescence peut représenter une feuille de l'arborescence. Une branche est un niveau où plus d'un nom est utilisé pour identifier un ensemble de ressource. Un feuille représente un nom unique utilisé une seule fois à ce niveau pour indiquer une ressource spécifique.
			
	* L'organisation de l'espace de noms de domaine DNS:
			>* Tout nom de domaine DNS utilisé dans l'arborescence es un domaine. Cependant la plupart des discussions DNS identifient les noms sur 5 catégories : selon le niveau et la façon dont le nom est utilisé couramment. Exemple : microsoft.com est un nom de domaine de niveau 2.
			>* Les 5 catégories sont :
			
	* Domaines DNS et internet :
			>* Le système de nom de domaine internet est géré par une autorité d'inscription de nom sur internet responsable de la gestion des domaines de niveau supérieur qui sont affectés par organisation et par pays/région. Ces noms de domaine suivent la norme international 3166. Exemple de nom de domaine :
	* Enregistrement de ressources : 
		>* Une base de données DNS se compose d'enregistrement de ressource (RR). Chaque RR identifie une ressource particulière dans la base de données. Il existe différent types de RRR dans DNS. Liste d'enregistrement de ressources DNS :
		
* Protocole HTTP :
	    * 
* Fonctionnement de nslookup :
	* nslookup est un outil permettant d'interroger un serveur de noms pour obtenir les informations concernant un domaine ou un hôte et permet de diagnostiquer es éventuels problèmes de configuration du DNS.
	* la commande nslookup affiche le nom et l'addresse IP du serveur de noms primaire et affiche une invite de commande pour l'interrogation. il suffit de taper le nom d'un domaine à l'invite afin d'en afficher les caractéristiques. il est également possible de demander les informations sur un hôte en indiquant son nom à la suite de la commande nslookup : nslookup host.name
	* Par défaut, cette commande interroge le serveur de noms primaire configuré sur la machine. Il est possible d'interroger un serveur de noms spécifique en le spécifiant comme suis : nslookup host.name -serveur.de.nom
	* Il est possible de modifier le mode d'interrogation de nslookup avec la clause set:
		* set type=mx permet de recueillir les informations concernant le ou les serveurs de messagerie d'un domaine ;
		* set type=ns permet de recueillir les informations concernant le serveur de noms associé au domaine ;
		* set type=a permet de recueillir les informations concernant un hôte du réseau (mode d'interrogation par défaut)
		* set type=soa permet d'afficher les informations du champ SOA ( start of authority) ;
		* set type=cname permet d'afficher les informations concernant les alias ;
		* set type=hinfo permet lorsque ces données sont renseignées d'afficher les informations concernant le matériel et le système d'exploitation de l'hôte.

Pour sortir de nslookup il faut taper exit.

* Organismes gérant les protocoles :
	    * 
* Théorie de communication : 
	    * 
* Canaux de communication :
	    * 
* Couches des différents protocoles :
	    * 
* Implémentation des protocoles :
	    * 

###Réalistions

    Résoudre le problème
    Connaitre "les 13"