

## 1ère étape : Génération de la requête de certificat
***Sur le serveur IIS***

Dans la console de gestion de IIS, ouvrir la console *Certificat*, faire un clic-droit et sélectionner *Créer une demande de certificat*

![image](https://github.com/criss1180/ADCS_IIS/assets/115303549/4c91e50b-5165-4895-aaec-50f892ea07dd)


Renseigner les informations suivantes:

![image](https://github.com/criss1180/ADCS_IIS/assets/115303549/f7041d32-8b09-4ad4-95d3-9b152a75331b)


Sélectionner le paramétrage ci-dessous

![image](https://github.com/criss1180/ADCS_IIS/assets/115303549/345d1068-5cf9-4923-98ff-ca34bbf867f3)


Renseigner le dossier et le nom où se trouvera la requête

![image](https://github.com/criss1180/ADCS_IIS/assets/115303549/e021b81c-47a3-42fd-977f-e46a1560fd1e)

![image](https://github.com/criss1180/ADCS_IIS/assets/115303549/4cc744e9-4669-4a81-88d9-5a67dc54c2d9)


## 2ème étape : Récupération de la requête
***Sur le serveur AD-CS***  
***Via Partage réseau / Winscp / VMtools***

## 3ème étape : Création du certificat
***Sur le serveur AD-CS***

exécuter cette commande en powershell:
certutil -setreg policy\EditFlags +EDITF_ATTRIBUTESUBJECTALTNAME2

![image](https://github.com/criss1180/ADCS_IIS/assets/115303549/1e83ac4d-f6ff-4c26-a0d8-6b44885546c5)


redémarrer le service ADCS dans la console 

![image](https://github.com/criss1180/ADCS_IIS/assets/115303549/8cf1b262-e417-402e-a5e4-7264168b1f2e)

exécuter cette commande en powershell:
certreq -submit -attrib "CertificateTemplate:WebServer\nSAN:dns=intranet.cris.lan&ipaddress=192.168.145.7" intranet.txt 

![image](https://github.com/criss1180/ADCS_IIS/assets/115303549/2a97af7d-b216-45cf-b4d4-de7d86a3829b)


Sélectionner l'autorité de certification

![image](https://github.com/criss1180/ADCS_IIS/assets/115303549/590c60f2-d105-4d33-a075-8166d7176ed2)


Enregistrer le certificat en .cer

![image](https://github.com/criss1180/ADCS_IIS/assets/115303549/d8fd2a7e-ef52-4580-b5c7-badb361ecffa)


## 4ème étape : Récupération du certificat
***Sur le serveur IIS***  
***Partage réseau / Winscp / VMtools***

## 5ème étape : Importation du certificat
***Sur le serveur IIS***

Dans la console de gestion de IIS, ouvrir la console *Certificat*, faite un clic-droit et sélectionner *Terminer une demande de certificat*

![image](https://github.com/criss1180/ADCS_IIS/assets/115303549/dfc79d7e-4ac9-4ff2-a15b-c53327241298)

![image](https://github.com/criss1180/ADCS_IIS/assets/115303549/9d253eac-fa44-401a-b1ac-9409360748d3)


Sélectionner le certificat

![image](https://github.com/criss1180/ADCS_IIS/assets/115303549/8972c9c1-d4ad-43d7-bafe-119498ffc857)


## 6ème étape : Liaison HTTPS
***Sur le serveur IIS***

Dans la console de gestion de IIS, faire un clic-droit sur le VHost et sélectionner *Modifier les liaisons*

![image](https://github.com/criss1180/ADCS_IIS/assets/115303549/58043d1c-e290-41cd-a8ff-cf9c3a1c99bd)


Créer la liaison suivante en sélectionnant le certificat récemment importé

![image](https://github.com/criss1180/ADCS_IIS/assets/115303549/601bec96-8c1c-43fd-ae62-6eada01ecd83)


## 7ème étape : Redirection HTTP => HTTPS

![image](https://github.com/criss1180/ADCS_IIS/assets/115303549/837cb4e2-3f6c-435a-9b15-981437050eb0)


redémarrer le service IIS

![image](https://github.com/criss1180/ADCS_IIS/assets/115303549/c1a2566b-9580-4b35-974a-ae6f8fdf3bde)


Et voici notre page intranet en HTTPS :

![image](https://github.com/criss1180/ADCS_IIS/assets/115303549/5c6275a9-ae84-48b7-b1cf-7c27f9424e8e)

