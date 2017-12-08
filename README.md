CER

Titre : Protocole HTTP / dns


R�alisation du plan d�action :
Le Hypertext Transfer Protocol, plus connu sous l'abr�viation HTTP, litt�ralement le � protocole de transfert hypertexte �, est un protocole de communication client-serveur d�velopp� pour le World Wide Web. Il est utilis� pour �changer toute sorte de donn�es entre client HTTP et serveur HTTP.
HTTP est un langage qui permet au client via un navigateur de communiquer � un serveur connect� au r�seau (serveur http install� sur le serveur d�un site : Apache)

 Requ�te :
Syntaxe de la req�te client : 

Ligne de commande est compos� de 3 param�tres :
?	Commande : C�est la m�thode � utiliser, elle sp�cifie le type de requ�te
Il existe de nombreuses m�thodes, les plus courantes �tant GET, HEAD et POST :
GET
C'est la m�thode la plus courante pour demander une ressource. Une requ�te GET est sans effet sur la ressource, il doit �tre possible de r�p�ter la requ�te sans effet.
HEAD
Cette m�thode ne demande que des informations sur la ressource, sans demander la ressource elle-m�me.
POST
Cette m�thode est utilis�e pour transmettre des donn�es en vue d'un traitement � une ressource (le plus souvent depuis un formulaire HTML). L'URI fourni est l'URI d'une ressource � laquelle s'appliqueront les donn�es envoy�es. Le r�sultat peut �tre la cr�ation de nouvelles ressources ou la modification de ressources existantes. � cause de la mauvaise impl�mentation des m�thodes HTTP (pour Ajax) par certains navigateurs (et la norme HTML qui ne supporte que les m�thodes GET et POST pour les formulaires), cette m�thode est souvent utilis�e en remplacement de la requ�te PUT, qui devrait �tre utilis�e pour la mise � jour de ressources.
OPTIONS
Cette m�thode permet d'obtenir les options de communication d'une ressource ou du serveur en g�n�ral.
CONNECT
Cette m�thode permet d'utiliser un proxy comme un tunnel de communication.
TRACE
Cette m�thode demande au serveur de retourner ce qu'il a re�u, dans le but de tester et effectuer un diagnostic sur la connexion.
PUT
Cette m�thode permet de remplacer ou d'ajouter une ressource sur le serveur. L'URI fourni est celui de la ressource en question.
PATCH
Cette m�thode permet, contrairement � PUT, de faire une modification partielle d'une ressource.
DELETE
Cette m�thode permet de supprimer une ressource du serveur.
Ces 3 derni�res m�thodes n�cessitent g�n�ralement un acc�s privil�gi�.

?	URL : 
L�adresse de la page sur le serveur ex : "/repertoire/page.ext".
?	Version http :

Ensuite on a l�en-t�te de requ�te :
Maintenant, attaquons-nous � l'en-t�te : celui-ci peut contenir tout un tas de valeurs (c'est un peu le m�me principe que les balises <meta> en HTML), toujours pr�sent�es sous la forme :
Nom: valeur
En voici quelques-unes :
?	Host: ?	www.site.com
Sp�cifie le nom de domaine du site, par exemple s'il y a plusieurs sites � la m�me adresse IP.
?	Cookie: nom-cookie=valeur cookie
Permet d'envoyer au serveur les cookies qui ont �t� enregistr�s. Un cookie � toujours un nom et une valeur. Pour en envoyer plusieurs, �crivez-les � la suite, s�par�s par un point-virgule.
?	Connection: Close|Keep-Alive
D�finit le type de connexion :
?	Close : la connexion est ferm�e apr�s la r�ponse
?	Keep-Alive : cr�e une connexion persistante. Avec ce type de connexion, il est m�me possible d'envoyer une requ�te sans attendre la r�ponse � la pr�c�dente.
?	Content-type: application/x-www-form-urlencoded
Sp�cifie le ?	type MIME du corps de requ�te, il sera tr�s utile dans le cas d'une requ�te POST.
?	Content-Length: 42
Sp�cifie la longueur du corps de requ�te.

Le corps de la requ�te : Il peut contenir, par exemple, le contenu d'un formulaire HTML envoy� en POST.
Dans le cas du formulaire, les variables ont un nom et une valeur, comme l'en-t�te Cookie, et les diff�rentes variables sont s�par�es par des esperluettes : "&" (notez que les variables pass�es par GET sont �galement s�par�es par "&").
Exemple : variable=valeur&variable2=valeur2


R�ponses :
 Les r�ponses ont, elles aussi, toujours la m�me syntaxe : 

La ligne de statut est compos�e de :
?	Version : la version HTTP du serveur
?	Code-r�ponse : le code d'erreur retourn� (par exemple 200, 403, 404, 500)
?	Texte-r�ponse : le texte associ� � l'erreur (respectivement pour les exemples pr�c�dents : "OK", "FORBIDDEN", "NOT FOUND", "INTERNAL ERROR").

Code d�erreurs :

Code	Message	Description
10x	Message d'information	Ces codes ne sont pas utilis�s dans la version 1.0 du protocole
20x	R�ussite	Ces codes indiquent le bon d�roulement de la transaction
200	OK	La requ�te a �t� accomplie correctement
201	CREATED	Elle suit une commande POST, elle indique la r�ussite, le corps du reste du document est sens� indiquer l'URL � laquelle le document nouvellement cr�� devrait se trouver.
202	ACCEPTED	La requ�te a �t� accept�e, mais la proc�dure qui suit n'a pas �t� accomplie
203	PARTIAL INFORMATION	Lorsque ce code est re�u en r�ponse � une commande GET, cela indique que la r�ponse n'est pas compl�te.
204	NO RESPONSE	Le serveur a re�u la requ�te mais il n'y a pas d'information � renvoyer
205	RESET CONTENT	Le serveur indique au navigateur de supprimer le contenu des champs d'un formulaire
206	PARTIAL CONTENT	Il s'agit d'une r�ponse � une requ�te comportant l'en-t�te range. Le serveur doit indiquer l'en-t�te content-Range
30x	Redirection	Ces codes indiquent que la ressource n'est plus � l'emplacement indiqu�
301	MOVED	Les donn�es demand�es ont �t� transf�r�es � une nouvelle adresse
302	FOUND	Les donn�es demand�es sont � une nouvelle URL, mais ont cependant peut-�tre �t� d�plac�es depuis...
303	METHOD	Cela implique que le client doit essayer une nouvelle adresse, en essayant de pr�f�rence une autre m�thode que GET
304	NOT MODIFIED	Si le client a effectu� une commande GET conditionnelle (en demandant si le document a �t� modifi� depuis la derni�re fois) et que le document n'a pas �t� modifi� il renvoie ce code.
40x	Erreur due au client	Ces codes indiquent que la requ�te est incorrecte
400	BAD REQUEST	La syntaxe de la requ�te est mal formul�e ou est impossible � satisfaire
401	UNAUTHORIZED	Le param�tre du message donne les sp�cifications des formes d'autorisation acceptables. Le client doit reformuler sa requ�te avec les bonnes donn�es d'autorisation
402	PAYMENT REQUIRED	Le client doit reformuler sa demande avec les bonnes donn�es de paiement
403	FORBIDDEN	L'acc�s � la ressource est tout simplement interdit
404	NOT FOUND	Classique ! Le serveur n'a rien trouv� � l'adresse sp�cifi�e. Parti sans laisser d'adresse... :)
50x	Erreur due au serveur	Ces codes indiquent qu'il y a eu une erreur interne du serveur
500	INTERNAL ERROR	Le serveur a rencontr� une condition inattendue qui l'a emp�ch� de donner suite � la demande (comme quoi il leur en arrive des trucs aux serveurs...)
501	NOT IMPLEMENTED	Le serveur ne supporte pas le service demand� (on ne peut pas tout savoir faire...)
502	BAD GATEWAY	Le serveur a re�u une r�ponse invalide de la part du serveur auquel il essayait d'acc�der en agissant comme une passerelle ou un proxy
503	SERVICE UNAVAILABLE	Le serveur ne peut pas vous r�pondre � l'instant pr�sent, car le trafic est trop dense (toutes les lignes de votre correspondant sont occup�es veuillez rappeler ult�rieurement)
504	GATEWAY TIMEOUT	La r�ponse du serveur a �t� trop longue vis-�-vis du temps pendant lequel la passerelle �tait pr�par�e � l'attendre (le temps qui vous �tait imparti est maintenant �coul�...)



En-t�tes
Les en-t�tes sont nombreux ici aussi, en voici quelques-uns utiles :
?	Date: Fri, 31 Dec 1999 23:59:59 GMT
Date de g�n�ration de la r�ponse.
?	Server: Apache/2.2.3
Sp�cifie le mod�le du serveur HTTP.
?	Content-type: text/plain
cf. chapitre pr�c�dent.
?	Content-Length: 42
cf. chapitre pr�c�dent.
?	Set-Cookie: variable=valeur; expires=Fri, 31-Dec-2010 23:59:59 GMT; path=/; domain=.site.com
Demande au navigateur d'enregistrer un cookie (voir setcookie()).
Corps
Et pour finir, le Corps de r�ponse contient le contenu du fichier, le HTML d'une page par exemple.


Proxy :
Un proxy, ou serveur mandataire, est un serveur faisant le lien entre un r�seau priv� et internet. Il r�cup�re les requ�tes http des utilisateurs du r�seau priv�, les transmet au serveur demand�, r�cup�re la r�ponse, la stocke en cache et la transmet au client. Le fait de la stocker en cache permet d��viter de faire trop de requ�tes r�p�titives. Si 12 utilisateurs du r�seau demandent la m�me page, seule 1 requ�te sortira du r�seau (la premi�re arriv�e), car le proxy pourra r�pondre aux 11 autres gr�ce � son stockage. Un serveur proxy poss�de deux adresses IP, une sur le r�seau priv� et une sur Internet. Avoir un proxy permet aussi de bloquer des requ�tes � des sites dont l�url est tendancieuse, gr�ce � un syst�me de d�tection de mots-cl�s.

Serveur Web : 
Un serveur Web est un serveur informatique utilis� pour publier des sites web sur Internet ou un intranet. L'expression � serveur Web � d�signe �galement le logiciel utilis� sur le serveur pour ex�cuter les requ�tes HTTP, le protocole de communication employ� sur le World Wide Web.
Un serveur web diffuse g�n�ralement des sites web, il peut contenir d'autres services li�s comme l'envoi d'e-mails, du streaming, le transfert de fichiers par FTP, etc.

Les serveurs Web publics sont reli�s � Internet et h�bergent des ressources (pages web, images, vid�os, etc.) du Web. Certains serveurs sont seulement accessibles sur des r�seaux priv�s (intranets) et h�bergent des sites utilisateurs, des documents, ou des logiciels, internes � une entreprise, une administration, etc. Techniquement il serait possible qu'un m�me ordinateur remplisse les deux fonctions, mais c'est rarement le cas pour des raisons de s�curit�.
La fonction principale d'un serveur Web est de stocker et d�livrer des pages web qui sont g�n�ralement �crites en HTML. Le protocole de communication Hypertext Transfer Protocol (HTTP) permet de dialoguer avec le logiciel client, g�n�ralement un navigateur Web.

Le serveur HTTP ou daemon HTTP est le logiciel prenant en charge les requ�tes client-serveur du protocole HTTP d�velopp� pour le World Wide Web. Les plus connus sont Apache, IIS, Nginx, Lighttpd...
Ces logiciels int�grent g�n�ralement des modules permettant d'ex�cuter un langage serveur comme PHP pour g�n�rer des pages web dynamiques.

Un ordinateur sur lequel fonctionne un serveur HTTP est appel� serveur Web. Mais un serveur HTTP peut aussi �tre appel�, informellement, � serveur Web �. Ainsi, si � serveur HTTP � d�signe toujours un logiciel, � serveur Web � peut aussi bien d�signer le logiciel que l'ordinateur qui l'h�berge.

Les deux termes sont utilis�s pour le logiciel car le protocole HTTP a �t� d�velopp� pour le Web, et les pages Web sont en pratique toujours servies avec ce protocole. Cependant d'autres ressources du Web comme les fichiers � t�l�charger ou les flux audio ou vid�o sont parfois servis avec d'autres protocoles.

CERN httpd est le premier serveur HTTP, invent� en m�me temps que le World Wide Web, en 1990 au CERN de Gen�ve, il est rapidement devenu obsol�te en raison de l'�volution exponentielle des fonctionnalit�s du protocole.
Quelques serveurs HTTP :
?	 Apache HTTP Server de la Apache Software Foundation, successeur du NCSA HTTPd ;
?	Apache Tomcat de la Apache Software Foundation, �volution de Apache pour J2EE ;
?	BusyBox httpd, utilis� dans le domaine de l'embarqu�, et notamment avec OpenWRT1 ;
?	Google Web Server de Google ;
?	Internet Information Services (IIS) de Microsoft ;
?	lighttpd de Jan Kneschke ;
?	Monkey web server de Eduardo Silva Pereira, d�di� au noyau Linux, permettant d'utiliser pleinement ses fonctionnalit�s ;
?	nginx d'Igor Sysoev ;
?	NodeJS sous MIT Licence con�u par Ryan Lienhart Dahl en lignes de programmation en JavaScript ;
?	Sun Java System Web Server de Sun Microsystems (anciennement iPlanet de Netscape, puis Sun ONE de Sun Microsystems) ;
?	Tengine, fork de nginx, de Taobao (9e rang mondial Alexa en juillet 2014) ;
?	Zeus Web Server de Zeus Technology.
?	Le serveur HTTP le plus utilis� est Apache HTTP Server qui sert environ 55 % des sites web en janvier 2013 selon Netcraft2.

S�curit� serveur web :
Poss�der son propre serveur et le g�rer soi-m�me donne une plus grande flexibilit� � son propri�taire que les serveurs dits � cl� en main � ou autres serveurs mutualis�s. Il y a cependant un aspect sur lequel il ne faut pas prendre � la l�g�re : la s�curit�.
Quelque point important de s�curit� :
?	Prot�ger son acc�s SSH
?	Adopter une politique de mots de passe robustes
?	Avoir un syst�me � jour
?	Se pr�munir des attaques DoS
?	Bridez votre PHP
?	Ne pas �tre trop bavard

Virtual Host :
A l�arriv�e d�une requ�te, un serveur virtuel bas� sur le nom va rechercher l'argument de section <VirtualHost> pr�sentant la meilleure (la plus exacte) correspondance avec la paire adresse IP/port utilis�e dans la requ�te. Si plusieurs serveurs virtuels poss�dent cette m�me paire adresse IP/port, Apache va ensuite comparer les valeurs des directives ServerName et module="core">ServerAlias avec le nom de serveur pr�sent dans la requ�te.
Si on ne d�finit pas de directive ServerName pour un serveur virtuel � base de nom, le serveur utilisera par d�faut le nom de domaine enti�rement qualifi� (FQDN) d�duit du nom d'h�te syst�me. Voir ressource pour la configuration d�un virtual host.

 
DNS :
Un syst�me appel� DNS (Domain Name System) associe des noms en langage courant aux adresses num�riques

Ce syst�me propose :
?	un espace de noms hi�rarchique permettant de garantir l'unicit� d'un nom dans une structure arborescente, � la mani�re des syst�mes de fichiers d'Unix.
?	un syst�me de serveurs distribu�s permettant de rendre disponible l'espace de noms.
?	un syst�me de clients permettant de � r�soudre � les noms de domaines, c'est-�-dire interroger les serveurs afin de conna�tre l'adresse IP correspondant � un nom.
FQDN :
Un FQDN est compos� d'un nom d'h�te et d'un nom de domaine, par exemple www.google.com est un FQDN o� www est le nom d'h�te et google.com le nom de domaine.
Les noms de domaine sont organis�s de mani�re hi�rarchique, le domaine se trouvant le plus haut dans la hi�rarchie est � . �, il est omis dans les FQDN. En � dessous � dans la hi�rarchie se trouvent les TLD (Top Level Domain).

Les serveurs de noms :
Les machines appel�es serveurs de nom de domaine permettent d'�tablir la correspondance entre le nom de domaine et l'adresse IP des machines d'un r�seau.
Chaque domaine poss�de un serveur de noms de domaines, appel� � serveur de noms primaire � (primary domain name server), ainsi qu'un serveur de noms secondaire (secondary domaine name server), permettant de prendre le relais du serveur de noms primaire en cas d'indisponibilit�.
Les serveurs correspondant aux domaines de plus haut niveau (TLD) sont appel�s � serveurs de noms racine �. Il en existe treize, r�partis sur la plan�te, poss�dant les noms � a.root-servers.net � � � m.root-servers.net �. 
Le serveur le plus r�pandu s'appelle BIND (Berkeley Internet Name Domain). Il s'agit d'un logiciel libre disponible sous les syst�mes UNIX, d�velopp� initialement par l'universit� de Berkeley en Californie et d�sormais maintenu par l'ISC (Internet Systems Consortium).
Un serveur de noms d�finit une zone, c'est-�-dire un ensemble de domaines sur lequel le serveur a autorit�. Le syst�me de noms de domaine est transparent pour l'utilisateur, n�anmoins il ne faut pas oublier les points suivants :
?	Chaque ordinateur doit �tre configur� avec l'adresse d'une machine capable de transformer n'importe quel nom en une adresse IP. Cette machine est appel�e Domain Name Server.
?	L'adresse IP d'un second Domain Name Server (secondary Domain Name Server) doit �galement �tre d�finie : le serveur de noms secondaire peut relayer le serveur de noms primaire en cas de dysfonctionnement.


Un DNS est une base de donn�es r�partie contenant des enregistrements, appel�s RR (Resource Records), concernant les noms de domaines. Seules sont concern�es par la lecture des informations ci-dessous les personnes responsables de l'administration d'un domaine, le fonctionnement des serveurs de noms �tant totalement transparent pour les utilisateurs. 
En raison du syst�me de cache permettant au syst�me DNS d'�tre r�parti, les enregistrements de chaque domaine poss�dent une dur�e de vie, appel�e TTL (Time To Live, traduisez esp�rance de vie), permettant aux serveurs interm�diaires de conna�tre la date de p�remption des informations et ainsi savoir s'il est n�cessaire ou non de la rev�rifier.


