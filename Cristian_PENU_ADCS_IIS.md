

## 1ère étape : Génération de la requête de certificat
***Sur le serveur IIS***

Dans la console de gestion de IIS, ouvrir la console *Certificat*, faire un clic-droit et sélectionner *Créer une demande de certificat*

![[Pasted image 20231026113256.png]]

Renseigner les informations suivantes:

![[Pasted image 20231026113420.png]]

Sélectionner le paramétrage ci-dessous

![[Pasted image 20231026113508.png]]

Renseigner le dossier et le nom où se trouvera la requête

![[Pasted image 20231026113645.png]]
![[Pasted image 20231026113728.png]]

## 2ème étape : Récupération de la requête
***Sur le serveur AD-CS***  
***Via Partage réseau / Winscp / VMtools***

## 3ème étape : Création du certificat
***Sur le serveur AD-CS***

exécuter cette commande en powershell:
certutil -setreg policy\EditFlags +EDITF_ATTRIBUTESUBJECTALTNAME2

![[Pasted image 20231026114057.png]]

redémarrer le service ADCS dans la console 

![[Pasted image 20231026114144.png]]

exécuter cette commande en powershell:
certreq -submit -attrib "CertificateTemplate:WebServer\nSAN:dns=intranet.cris.lan&ipaddress=192.168.145.7" intranet.txt 

![[Pasted image 20231026114351.png]]

Sélectionner l'autorité de certification

![[Pasted image 20231026114427.png]]

Enregistrer le certificat en .cer

![[Pasted image 20231026114511.png]]

## 4ème étape : Récupération du certificat
***Sur le serveur IIS***  
***Partage réseau / Winscp / VMtools***

## 5ème étape : Importation du certificat
***Sur le serveur IIS***

Dans la console de gestion de IIS, ouvrir la console *Certificat*, faite un clic-droit et sélectionner *Terminer une demande de certificat*

![[Pasted image 20231026114655.png]]
![[Pasted image 20231026115650.png]]

Sélectionner le certificat

![[Pasted image 20231026114823.png]]

## 6ème étape : Liaison HTTPS
***Sur le serveur IIS***

Dans la console de gestion de IIS, faire un clic-droit sur le VHost et sélectionner *Modifier les liaisons*

![[Pasted image 20231026115749.png]]

Créer la liaison suivante en sélectionnant le certificat récemment importé

![[Pasted image 20231026115841.png]]
## 7ème étape : Redirection HTTP => HTTPS

![[Pasted image 20231026115915.png]]

redémarrer le service IIS

![[Pasted image 20231026115931.png]]

Et voici notre page intranet en HTTPS :

![[Pasted image 20231026120512.png]]
