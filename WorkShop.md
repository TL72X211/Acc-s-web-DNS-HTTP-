# WorkShop DNS

## Configuration d'un client DNS

 * Que contient votre fichier /etc/hosts ?
 Les noms d'hôtes attribués à chaque adresse IP, le domaine e tsous-domaine auquel ils appartiennent et leur Alias

 * Dans quel ordre se fera la resolution de noms sur votre machine ?
 De la droite vers la gauche, du domaine le plus large au sous-domaine le plus proche puis le nom de la machine

 * Quelle est l'adresse IP du serveur de noms DNS que le resolveur interrogera ?
 192.168.145.2, c'est sur VMWare l'adresse du routeur qui s'occupe de la resolution de noms/d'adresses

 * Modifier le fichier de configuration de la resolution de noms pour qu'il interroge les serveurs DNS donnés
 DNS Primaire 208.67.222.222  
 DNS Secondaire 208.67.220.220  
 nano /etc/network/interfaces  
 En dessous de la gateway :  
 dns-nameservers 208.67.222.222 208.67.220.220

## Requete DNS

 * Determiner l'adresse IP de www.cesi.fr  
 dig www.cesi.fr  
 réponse 194.2.77.162

 * Determinez si la reponse du serveur dns qui vous a repondu supporte la recursivite et si sa reponse fait autorite ("authoritative")
 On voit dans la réponse les 'flags' : qr , rd , ra  
 qr = réponse à une requete  
 rd = réponse recursive demandee  
 ra = reponse recursive disponible sur le serveur  
 Le Flag aa n'etant pas présent, cette reponse ne fait pas autorite

 * Determinez le serveur a utiliser pour obtenir une reponse «authoritative ». ce serveur supporte-t-il la recursivite ?
 Commande dig -t aaaa  
 ns.net4all-dns.com.

 * Quelle reponse vous donne un serveur dns lorsqu’il ne supporte pas la recursivite et qu’il ne connait pas la reponse a votre question ?
 Soit il ne repond pas, soit il nous renvoie un status : ERROR, soit il renvoie l'adresse d'un dns qui supporte la récursivité

 * Visualisez, avec l’option +trace la suite des serveurs contactes pour trouver l’adresse ip de www.cesi.fr. Quels sont les domaines traverses et les serveurs de noms interroges ? La requete est-elle recursive ? Que constatezvous en lançant plusieurs fois cette commande ?
 **Fonctionne pas**

 * Comment savoir quels serveurs DNS gerent le TLD .FR ?
 **Ne sais pas**

 * Comment recuperer avec dig les informations contenues dans les entrees de type SOA du DNS gerant la zone cesi.fr ?
 Avec la commande dig soa www.cesi.fr

 * Determiner le ttl (duree pendant laquelle l’enregistrement sera valide dans les caches des dns) de www.cesi.fr ?
 Le dernier chiffre obtenu avec la commande dig soa représente la ttl (durée de vie) en seconde et est de 3600

 * Le type nom canonique (alias). Verifier le type de www.yahoo.fr ?
 Le CNAME de www.yahoo.fr est rc.yahoo.com.

 * Trouver l’adresse ip et le nom du serveur d’echange de courrier de cesi.fr ?
 nslookup  
 set type=mx  
 cesi.fr  
 L'adresse trouvée est : cesi-fr.mail.protection.outlook.com.

## Installation et configuration d'un serveur DNS

 * Installation des paquets
 apt-get install bind9 bind9utils dnsutils

 * 
