Prosit 1.3
===================



Mots clés
-------------

>- **DNS** : Domain Name System, son rôle sera développé plus tard dans le plan d'action.
>- **Apache** : serveur web http, l'un de ses rôle principal est d’écouter les requêtes émises par les navigateurs, de chercher la page demandée et de la renvoyer.
>- **HTTP** : Hypertext Transfer Protocol, c'est un protocole de communication client-serveur. Les détails de l'implémentation de l'HTTP seront détaillés plus tard dans le plan d'action, ainsi que la variante HTTPS, qui est sécurisée.
>- **nsookup** : name server lookup, est une commande Unix qui permet de demander des informations à des serveurs DNS, par défaut elle traduira une nom de domaine en une adresse IP et vice-versa. 
>- **FAI** : Fournisseur d'accès Internet
>- **FQDN** : Fully Qualified Domain Name, c'est un nom de domaine qui défini la position absolue d'un nœud dans l’arborescence DNS (il indique tous les nœuds supérieurs jusqu'à la racine).
>- **Nginx** : serveur web open source
>- **IIS** : serveur web développé par Microsoft
>- **Registrar** : société gérant l'attribution des noms de domaines sur Internet, l'ICANN pour les noms de domaines en .com, et l'AFNIC pour ceux en .fr
>- **Virtual Host** : méthode permettant à un seul ordinateur d'accueillir plusieurs noms de domaines. La différentiation peut se faire sur le nom d'hôte, sur l'adresse IP, ou sur le numéro de port.
>- **enregistrement DNS de type A** : type particulier d'enregistrement DNS, une partie entière est consacrée à ce point par la suite.
>- **résolution de nom** : résolution du nom d'hôte en adresse IP, ce travail est principalement effectué par le DNS.
>- **adresse IP 8.8.8.8** : adresse IP de google



Plan d'action
-------------

#### DNS
Le rôle du DNS est principalement de traduire les adresses IP des équipements connectés à un réseaux IP en un nom, ce dernier étant plus simple à retenir.
Le service DNS est organisé sous la forme d'un arbre, dont le premier nœud ("racine") est situé tout en haut, et il est représenté par un point. Dans un domaine on peut créer un ou plusieurs sous domaines ainsi qu'une délégation (c'est à dire que les informations relatives à ce sous domaine sont sur un autre serveur).
Les noms de domaines se trouvant sous la racine sont appelés les TLD (Top Level Domain), parmis ces nom de domaines, ceux correspondants à une extension de pays sont appelés les ccTLD (coutry code TLD) et les autres gTLD (generic TLD).
Un nom de domaine est représenté selon la règle suivante :
les noms de domaines supérieurs se trouvent à droite, et chaque domaine est séparé des autres par un point.

>- Le protocole DNS utilise le port 53 et la taille maximale des paquets est de 512 octets

Il existe plusieurs types d'enregistrements DNS, chacun ayants ses particularités :
>- **A** record ou address record (également appelé enregistrement d’hôte) qui fait correspondre un nom d'hôte ou un nom de domaine ou un sous-domaine à une adresse IPv4 de 32 bits distribués sur quatre octets ex: 123.234.1.2 ;
>- **AAAA** record ou IPv6 address record qui fait correspondre un nom d'hôte à une adresse IPv6 de 128 bits distribués sur seize octets ;
>- **CNAME** record ou canonical name record qui permet de faire d'un domaine un alias vers un autre. Cet alias hérite de tous les sous-domaines de l'original ;
>- **MX** record ou mail exchange record qui définit les serveurs de courriel pour ce domaine ;
>- **PTR** record ou pointer record qui associe une adresse IP à un enregistrement de nom de domaine, aussi dit « reverse » puisqu'il fait exactement le contraire du A record ;
>- **NS** record ou name server record qui définit les serveurs DNS de ce domaine ;
>- **SOA** record ou Start Of Authority record qui donne les informations générales de la zone : serveur principal, courriel de contact, différentes durées dont celle d'expiration, numéro de série de la zone ;
>- **SRV** record qui généralise la notion de MX record, mais qui propose aussi des fonctionnalités avancées comme le taux de répartition de charge pour un service donné, standardisé dans la RFC 278221 ;
>- **NAPTR** record ou Name Authority Pointer record qui donne accès à des règles de réécriture de l'information, permettant des correspondances assez lâches entre un nom de domaine et une ressource. Il est spécifié dans la RFC 340322 ;
>- **TXT** record permet à un administrateur d'insérer un texte quelconque dans un enregistrement DNS (par exemple, cet enregistrement est utilisé pour implémenter la spécification Sender Policy Framework) ; d'autres types d'enregistrements sont utilisés occasionnellement, ils servent simplement à donner des informations (par exemple, un enregistrement de type LOC indique l'emplacement physique d'un hôte, c'est-à-dire sa latitude et sa longitude). Cet enregistrement aurait un intérêt majeur mais n'est malheureusement que très rarement utilisé sur le monde Internet.


Les  "13" représentent les 13 serveurs racines du DNS, ces serveurs répondent aux requêtes concernant les noms de domaines de premier niveau, puis ils les redirigent vers le serveur de premier niveau concerné.

#### Protocole HTTP

Le protocole HTTP est un protocole de communication qui va permettre à un client de communiquer avec un serveur HTTP.

La syntaxe d'un requête HTTP (côté client) est toujours la même :

	ligne de commande
	En-tête de requête
	Nouvelle ligne
	Corps de la requête

La ligne de commande spécifie le type de requête, il en existe 9 :

>-**GET** : permet de récupérer une ressource sans la modifier
>-**HEAD** : permet de demander des informations sur la ressource, sans demander la ressource en elle même
>-**POST** :  permet de modifier la ressource
>-**OPTIONS** : permet d'obtenir les options de communication du serveur/ de la ressource
>-**CONNECT** : permet d'utiliser un proxy comme tunnel de communication
>-**TRACE** : commande de diagnostic
>-**PUT** : permet d'ajouter une ressource sur le serveur
>-**PATCH** : permet la modification **partielle** d'une ressource
>-**DELETE** : permet de supprimer une ressource du serveur

L'en-tête de la requête contient des informations concernant la requête, comme par exemple la longueur du corps de requête, les valeurs de certains cookies, le nom de domaine du site,...
>- Ils sont sous la forme Nom: valeur

Le corps de la requête n'est pas tout le temps utile, il est par exemple utile lors d'une requête POST (il contient les informations à modifier).

Les réponse HTTP présentent la même syntaxe, à l'exception près que la première ligne est constituée de la version HTTP du serveur, du code d'erreur retourné, et du texte associé à l'erreur.

Les différents codes d'erreurs sont les suivants :
>- 1xx : Information
>- 2xx : Succès
>- 3xx : Redirection
>- 4xx : Erreur du client
>- 5xx : Erreur du serveur


####  nslookup

nslookup est une commande Unix permettant d’interroger des serveurs DNS et ainsi d'obtenir des 
informations sur un domaine.

La syntaxe de la commande est la suivante :
>- nslookup [-options] [name | -] [server]


	-[no]debug : active l'affichage d'informations supplémentaires concernant la réponse
	-port : spécifie le port utilisé (53 par défaut)
	-querytype/type : spécifie le type d’information qui va être retourné par la commande
				a : adresse IP
				any : toutes les informations disponibles
				gid : identifier de groupe
				hinfo : informations sur l'OS et sur le CPU
				mb : mailbox domain name
				mg : mail group member
				minfo : mailbox /mail information
				ns : nom du serveur de la zone
				
	-retry : nombre d'essais
	-timeout : temps d'attente maximal en secondes

----------