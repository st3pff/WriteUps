### Challenge: File upload - Type MIME

Url :  https://www.root-me.org/fr/Challenges/Web-Serveur/File-upload-Type-MIME

Writeups:

Etape 1 :

En lisant le pdf sur le challenge root me, on nous explique qu'il y'a une multitudes de failles de sécurités
qui existe lorsque qu'on upload un fichier sur un site web en .php

Cette implémentation souffre d'une faille de sécurité majeure. upload1.php permet aux utilisateurs de télécharger des fichiers arbitraires dans le répertoire uploads/ sous la racine web. 

Un utilisateur malveillant peut télécharger un fichier PHP, tel qu'un shell PHP et exécuter des commandes arbitraires sur le serveur avec le privilège du processus du serveur web. Un shell PHP est un script PHP qui permet à un utilisateur d'exécuter des commandes shell arbitraires sur le serveur.

script pour ouvrir un shell php:
```BASH
<?php
system($_GET['command']);
?>
``` 
Je décide donc de créer un nouveau fichier et de copier le code et de le renomer en test.php

Je décide de l'uploader mais le fichier n'est pas accepté car ce n'est pas un format .jpg .gif ou .png 


