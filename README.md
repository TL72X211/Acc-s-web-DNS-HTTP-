CER

Titre : Protocole HTTP / dns


Réalisation du plan d’action :
Le Hypertext Transfer Protocol, plus connu sous l'abréviation HTTP, littéralement le « protocole de transfert hypertexte », est un protocole de communication client-serveur développé pour le World Wide Web. Il est utilisé pour échanger toute sorte de données entre client HTTP et serveur HTTP.
HTTP est un langage qui permet au client via un navigateur de communiquer à un serveur connecté au réseau (serveur http installé sur le serveur d’un site : Apache)

 Requête :
Syntaxe de la reqête client : 

Ligne de commande est composé de 3 paramètres :
?	Commande : C’est la méthode à utiliser, elle spécifie le type de requête
Il existe de nombreuses méthodes, les plus courantes étant GET, HEAD et POST :
GET
C'est la méthode la plus courante pour demander une ressource. Une requête GET est sans effet sur la ressource, il doit être possible de répéter la requête sans effet.
HEAD
Cette méthode ne demande que des informations sur la ressource, sans demander la ressource elle-même.
POST
Cette méthode est utilisée pour transmettre des données en vue d'un traitement à une ressource (le plus souvent depuis un formulaire HTML). L'URI fourni est l'URI d'une ressource à laquelle s'appliqueront les données envoyées. Le résultat peut être la création de nouvelles ressources ou la modification de ressources existantes. À cause de la mauvaise implémentation des méthodes HTTP (pour Ajax) par certains navigateurs (et la norme HTML qui ne supporte que les méthodes GET et POST pour les formulaires), cette méthode est souvent utilisée en remplacement de la requête PUT, qui devrait être utilisée pour la mise à jour de ressources.
OPTIONS
Cette méthode permet d'obtenir les options de communication d'une ressource ou du serveur en général.
CONNECT
Cette méthode permet d'utiliser un proxy comme un tunnel de communication.
TRACE
Cette méthode demande au serveur de retourner ce qu'il a reçu, dans le but de tester et effectuer un diagnostic sur la connexion.
PUT
Cette méthode permet de remplacer ou d'ajouter une ressource sur le serveur. L'URI fourni est celui de la ressource en question.
PATCH
Cette méthode permet, contrairement à PUT, de faire une modification partielle d'une ressource.
DELETE
Cette méthode permet de supprimer une ressource du serveur.
Ces 3 dernières méthodes nécessitent généralement un accès privilégié.

?	URL : 
L’adresse de la page sur le serveur ex : "/repertoire/page.ext".
?	Version http :

Ensuite on a l’en-tête de requête :
Maintenant, attaquons-nous à l'en-tête : celui-ci peut contenir tout un tas de valeurs (c'est un peu le même principe que les balises <meta> en HTML), toujours présentées sous la forme :
Nom: valeur
En voici quelques-unes :
?	Host: ?	www.site.com
Spécifie le nom de domaine du site, par exemple s'il y a plusieurs sites à la même adresse IP.
?	Cookie: nom-cookie=valeur cookie
Permet d'envoyer au serveur les cookies qui ont été enregistrés. Un cookie à toujours un nom et une valeur. Pour en envoyer plusieurs, écrivez-les à la suite, séparés par un point-virgule.
?	Connection: Close|Keep-Alive
Définit le type de connexion :
?	Close : la connexion est fermée après la réponse
?	Keep-Alive : crée une connexion persistante. Avec ce type de connexion, il est même possible d'envoyer une requête sans attendre la réponse à la précédente.
?	Content-type: application/x-www-form-urlencoded
Spécifie le ?	type MIME du corps de requête, il sera très utile dans le cas d'une requête POST.
?	Content-Length: 42
Spécifie la longueur du corps de requête.

Le corps de la requête : Il peut contenir, par exemple, le contenu d'un formulaire HTML envoyé en POST.
Dans le cas du formulaire, les variables ont un nom et une valeur, comme l'en-tête Cookie, et les différentes variables sont séparées par des esperluettes : "&" (notez que les variables passées par GET sont également séparées par "&").
Exemple : variable=valeur&variable2=valeur2


Réponses :
 Les réponses ont, elles aussi, toujours la même syntaxe : 

La ligne de statut est composée de :
?	Version : la version HTTP du serveur
?	Code-réponse : le code d'erreur retourné (par exemple 200, 403, 404, 500)
?	Texte-réponse : le texte associé à l'erreur (respectivement pour les exemples précédents : "OK", "FORBIDDEN", "NOT FOUND", "INTERNAL ERROR").

Code d’erreurs :

Code	Message	Description
10x	Message d'information	Ces codes ne sont pas utilisés dans la version 1.0 du protocole
20x	Réussite	Ces codes indiquent le bon déroulement de la transaction
200	OK	La requête a été accomplie correctement
201	CREATED	Elle suit une commande POST, elle indique la réussite, le corps du reste du document est sensé indiquer l'URL à laquelle le document nouvellement créé devrait se trouver.
202	ACCEPTED	La requête a été acceptée, mais la procédure qui suit n'a pas été accomplie
203	PARTIAL INFORMATION	Lorsque ce code est reçu en réponse à une commande GET, cela indique que la réponse n'est pas complète.
204	NO RESPONSE	Le serveur a reçu la requête mais il n'y a pas d'information à renvoyer
205	RESET CONTENT	Le serveur indique au navigateur de supprimer le contenu des champs d'un formulaire
206	PARTIAL CONTENT	Il s'agit d'une réponse à une requête comportant l'en-tête range. Le serveur doit indiquer l'en-tête content-Range
30x	Redirection	Ces codes indiquent que la ressource n'est plus à l'emplacement indiqué
301	MOVED	Les données demandées ont été transférées à une nouvelle adresse
302	FOUND	Les données demandées sont à une nouvelle URL, mais ont cependant peut-être été déplacées depuis...
303	METHOD	Cela implique que le client doit essayer une nouvelle adresse, en essayant de préférence une autre méthode que GET
304	NOT MODIFIED	Si le client a effectué une commande GET conditionnelle (en demandant si le document a été modifié depuis la dernière fois) et que le document n'a pas été modifié il renvoie ce code.
40x	Erreur due au client	Ces codes indiquent que la requête est incorrecte
400	BAD REQUEST	La syntaxe de la requête est mal formulée ou est impossible à satisfaire
401	UNAUTHORIZED	Le paramètre du message donne les spécifications des formes d'autorisation acceptables. Le client doit reformuler sa requête avec les bonnes données d'autorisation
402	PAYMENT REQUIRED	Le client doit reformuler sa demande avec les bonnes données de paiement
403	FORBIDDEN	L'accès à la ressource est tout simplement interdit
404	NOT FOUND	Classique ! Le serveur n'a rien trouvé à l'adresse spécifiée. Parti sans laisser d'adresse... :)
50x	Erreur due au serveur	Ces codes indiquent qu'il y a eu une erreur interne du serveur
500	INTERNAL ERROR	Le serveur a rencontré une condition inattendue qui l'a empêché de donner suite à la demande (comme quoi il leur en arrive des trucs aux serveurs...)
501	NOT IMPLEMENTED	Le serveur ne supporte pas le service demandé (on ne peut pas tout savoir faire...)
502	BAD GATEWAY	Le serveur a reçu une réponse invalide de la part du serveur auquel il essayait d'accéder en agissant comme une passerelle ou un proxy
503	SERVICE UNAVAILABLE	Le serveur ne peut pas vous répondre à l'instant présent, car le trafic est trop dense (toutes les lignes de votre correspondant sont occupées veuillez rappeler ultérieurement)
504	GATEWAY TIMEOUT	La réponse du serveur a été trop longue vis-à-vis du temps pendant lequel la passerelle était préparée à l'attendre (le temps qui vous était imparti est maintenant écoulé...)



En-têtes
Les en-têtes sont nombreux ici aussi, en voici quelques-uns utiles :
?	Date: Fri, 31 Dec 1999 23:59:59 GMT
Date de génération de la réponse.
?	Server: Apache/2.2.3
Spécifie le modèle du serveur HTTP.
?	Content-type: text/plain
cf. chapitre précédent.
?	Content-Length: 42
cf. chapitre précédent.
?	Set-Cookie: variable=valeur; expires=Fri, 31-Dec-2010 23:59:59 GMT; path=/; domain=.site.com
Demande au navigateur d'enregistrer un cookie (voir setcookie()).
Corps
Et pour finir, le Corps de réponse contient le contenu du fichier, le HTML d'une page par exemple.


Proxy :
Un proxy, ou serveur mandataire, est un serveur faisant le lien entre un réseau privé et internet. Il récupère les requêtes http des utilisateurs du réseau privé, les transmet au serveur demandé, récupère la réponse, la stocke en cache et la transmet au client. Le fait de la stocker en cache permet d’éviter de faire trop de requêtes répétitives. Si 12 utilisateurs du réseau demandent la même page, seule 1 requête sortira du réseau (la première arrivée), car le proxy pourra répondre aux 11 autres grâce à son stockage. Un serveur proxy possède deux adresses IP, une sur le réseau privé et une sur Internet. Avoir un proxy permet aussi de bloquer des requêtes à des sites dont l’url est tendancieuse, grâce à un système de détection de mots-clés.

Serveur Web : 
Un serveur Web est un serveur informatique utilisé pour publier des sites web sur Internet ou un intranet. L'expression « serveur Web » désigne également le logiciel utilisé sur le serveur pour exécuter les requêtes HTTP, le protocole de communication employé sur le World Wide Web.
Un serveur web diffuse généralement des sites web, il peut contenir d'autres services liés comme l'envoi d'e-mails, du streaming, le transfert de fichiers par FTP, etc.

Les serveurs Web publics sont reliés à Internet et hébergent des ressources (pages web, images, vidéos, etc.) du Web. Certains serveurs sont seulement accessibles sur des réseaux privés (intranets) et hébergent des sites utilisateurs, des documents, ou des logiciels, internes à une entreprise, une administration, etc. Techniquement il serait possible qu'un même ordinateur remplisse les deux fonctions, mais c'est rarement le cas pour des raisons de sécurité.
La fonction principale d'un serveur Web est de stocker et délivrer des pages web qui sont généralement écrites en HTML. Le protocole de communication Hypertext Transfer Protocol (HTTP) permet de dialoguer avec le logiciel client, généralement un navigateur Web.

Le serveur HTTP ou daemon HTTP est le logiciel prenant en charge les requêtes client-serveur du protocole HTTP développé pour le World Wide Web. Les plus connus sont Apache, IIS, Nginx, Lighttpd...
Ces logiciels intègrent généralement des modules permettant d'exécuter un langage serveur comme PHP pour générer des pages web dynamiques.

Un ordinateur sur lequel fonctionne un serveur HTTP est appelé serveur Web. Mais un serveur HTTP peut aussi être appelé, informellement, « serveur Web ». Ainsi, si « serveur HTTP » désigne toujours un logiciel, « serveur Web » peut aussi bien désigner le logiciel que l'ordinateur qui l'héberge.

Les deux termes sont utilisés pour le logiciel car le protocole HTTP a été développé pour le Web, et les pages Web sont en pratique toujours servies avec ce protocole. Cependant d'autres ressources du Web comme les fichiers à télécharger ou les flux audio ou vidéo sont parfois servis avec d'autres protocoles.

CERN httpd est le premier serveur HTTP, inventé en même temps que le World Wide Web, en 1990 au CERN de Genève, il est rapidement devenu obsolète en raison de l'évolution exponentielle des fonctionnalités du protocole.
Quelques serveurs HTTP :
?	 Apache HTTP Server de la Apache Software Foundation, successeur du NCSA HTTPd ;
?	Apache Tomcat de la Apache Software Foundation, évolution de Apache pour J2EE ;
?	BusyBox httpd, utilisé dans le domaine de l'embarqué, et notamment avec OpenWRT1 ;
?	Google Web Server de Google ;
?	Internet Information Services (IIS) de Microsoft ;
?	lighttpd de Jan Kneschke ;
?	Monkey web server de Eduardo Silva Pereira, dédié au noyau Linux, permettant d'utiliser pleinement ses fonctionnalités ;
?	nginx d'Igor Sysoev ;
?	NodeJS sous MIT Licence conçu par Ryan Lienhart Dahl en lignes de programmation en JavaScript ;
?	Sun Java System Web Server de Sun Microsystems (anciennement iPlanet de Netscape, puis Sun ONE de Sun Microsystems) ;
?	Tengine, fork de nginx, de Taobao (9e rang mondial Alexa en juillet 2014) ;
?	Zeus Web Server de Zeus Technology.
?	Le serveur HTTP le plus utilisé est Apache HTTP Server qui sert environ 55 % des sites web en janvier 2013 selon Netcraft2.

Sécurité serveur web :
Posséder son propre serveur et le gérer soi-même donne une plus grande flexibilité à son propriétaire que les serveurs dits « clé en main » ou autres serveurs mutualisés. Il y a cependant un aspect sur lequel il ne faut pas prendre à la légère : la sécurité.
Quelque point important de sécurité :
?	Protéger son accès SSH
?	Adopter une politique de mots de passe robustes
?	Avoir un système à jour
?	Se prémunir des attaques DoS
?	Bridez votre PHP
?	Ne pas être trop bavard

Virtual Host :
A l’arrivée d’une requête, un serveur virtuel basé sur le nom va rechercher l'argument de section <VirtualHost> présentant la meilleure (la plus exacte) correspondance avec la paire adresse IP/port utilisée dans la requête. Si plusieurs serveurs virtuels possèdent cette même paire adresse IP/port, Apache va ensuite comparer les valeurs des directives ServerName et module="core">ServerAlias avec le nom de serveur présent dans la requête.
Si on ne définit pas de directive ServerName pour un serveur virtuel à base de nom, le serveur utilisera par défaut le nom de domaine entièrement qualifié (FQDN) déduit du nom d'hôte système. Voir ressource pour la configuration d’un virtual host.

 
DNS :
Un système appelé DNS (Domain Name System) associe des noms en langage courant aux adresses numériques

Ce système propose :
?	un espace de noms hiérarchique permettant de garantir l'unicité d'un nom dans une structure arborescente, à la manière des systèmes de fichiers d'Unix.
?	un système de serveurs distribués permettant de rendre disponible l'espace de noms.
?	un système de clients permettant de « résoudre » les noms de domaines, c'est-à-dire interroger les serveurs afin de connaître l'adresse IP correspondant à un nom.
FQDN :
Un FQDN est composé d'un nom d'hôte et d'un nom de domaine, par exemple www.google.com est un FQDN où www est le nom d'hôte et google.com le nom de domaine.
Les noms de domaine sont organisés de manière hiérarchique, le domaine se trouvant le plus haut dans la hiérarchie est « . », il est omis dans les FQDN. En « dessous » dans la hiérarchie se trouvent les TLD (Top Level Domain).

Les serveurs de noms :
Les machines appelées serveurs de nom de domaine permettent d'établir la correspondance entre le nom de domaine et l'adresse IP des machines d'un réseau.
Chaque domaine possède un serveur de noms de domaines, appelé « serveur de noms primaire » (primary domain name server), ainsi qu'un serveur de noms secondaire (secondary domaine name server), permettant de prendre le relais du serveur de noms primaire en cas d'indisponibilité.
Les serveurs correspondant aux domaines de plus haut niveau (TLD) sont appelés « serveurs de noms racine ». Il en existe treize, répartis sur la planète, possédant les noms « a.root-servers.net » à « m.root-servers.net ». 
Le serveur le plus répandu s'appelle BIND (Berkeley Internet Name Domain). Il s'agit d'un logiciel libre disponible sous les systèmes UNIX, développé initialement par l'université de Berkeley en Californie et désormais maintenu par l'ISC (Internet Systems Consortium).
Un serveur de noms définit une zone, c'est-à-dire un ensemble de domaines sur lequel le serveur a autorité. Le système de noms de domaine est transparent pour l'utilisateur, néanmoins il ne faut pas oublier les points suivants :
?	Chaque ordinateur doit être configuré avec l'adresse d'une machine capable de transformer n'importe quel nom en une adresse IP. Cette machine est appelée Domain Name Server.
?	L'adresse IP d'un second Domain Name Server (secondary Domain Name Server) doit également être définie : le serveur de noms secondaire peut relayer le serveur de noms primaire en cas de dysfonctionnement.


Un DNS est une base de données répartie contenant des enregistrements, appelés RR (Resource Records), concernant les noms de domaines. Seules sont concernées par la lecture des informations ci-dessous les personnes responsables de l'administration d'un domaine, le fonctionnement des serveurs de noms étant totalement transparent pour les utilisateurs. 
En raison du système de cache permettant au système DNS d'être réparti, les enregistrements de chaque domaine possèdent une durée de vie, appelée TTL (Time To Live, traduisez espérance de vie), permettant aux serveurs intermédiaires de connaître la date de péremption des informations et ainsi savoir s'il est nécessaire ou non de la revérifier.


