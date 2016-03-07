---
title: MODULE SRW3 - Installation et configuration d'une Serveur IIS
author: Centre professionnel du Nord vaudois
geometry: margin=2cm,a4paper
fontsize: 12pt
lang: french
header-includes:
- \usepackage{fancyhdr}
- \pagestyle{fancy}
- \fancyhead[CO,CE]{}
- \fancyfoot[C]{\date\today}
- \fancyfoot[RO,LE]{\thepage}
- \fancyfoot[RE,LO]{CPNV}
---

# Mise en place d'un service Internet et Intranet
*   Ajout de 2 sites dans le gestionnaire des services internet (IIS)
    * Cr�ation de 2 r�pertoires Internet et Intranet dans C:/www
    * Cr�ation de 2 fichiers index.html dans les 2 r�pertoires

*  Dans les settings de la Machine Virtuelle, ajouter une carte r�seau afin d'en avoir 1 en bridge et 1 en NAT
*  Pour les tests, modifiers les fichiers hosts de la machine local et virtuelle
*  Mise en place du document par d�faut index.html dans les deux sites : Gestionnaire de services / Selection serveur et de site / Dans la partie IIS s�lectionner Document par d�faut et ajouter XXX.html (pr�sent dans le C:/www)
 

Premier site 
 - Nom : Internet
 - Repertoire : C:\www\Internet
 - Nom de l'h�te : www.dupont.com
 - port 80
 - Adresse ip : 172.17.xxx.xxx
  
 Second site 
 - Nom : Intranet
 - Repertoire : C:\www\Intranet
 - Nom de l'h�te : intranet.dupont.com
 - port 80
 - Adresse ip : 192.168.xxx.xxx


# Cr�ation des utilisateurs
Aller dans Configuration / Utilisateurs et groupes locaux / Utilisateurs / Clic droit et cr�er.
Pareil pour les groupes (Directeur, Comptable, Ing�nieur) et assigner chaque membre au groupe correspondant

# Gestion de l'acc�s aux sites
Afin de rendre l'intranet accessible depuis l'internet, il faut :
*   Selectionner le site Internet dans Serveur/Sites/Internet
*   Clic droit cr�er un r�pertoire virtuel
*   Pointer sur le chemin physique de l'intranet (c�d C:/www/Intranet)
*   Activer l'authentificiation de base sur le dossier "intranet" cr��e et d�sactiv� l'authentification anonyme

# Gestion Espace priv� de l'intranet
* Cr�ation d'un dossier utilisateur pour chaque utilisateur
* Pour ce dossier, dans s�curit� / avanc�, supprimer Utilisateurs et ajouter l'utilisateur correspondant au dossier "mdupont" par ex ainsi que le groupe "IIS_IUSRS".
* Verifier que l'authentification de base soit bien pr�sente
* Le partie client sera disponible � cette adresse : www.dupont.com/intranet/mdupont

# Gestion Espace client de l'internet
* Utilisateur client, login : dclient, password : Qwertz123
* Dans les autorisation /s�curit� du dossier Internet/client supprimer le groupe "utilisateurs" et ajouter dclient ainsi que IIS_IUSRS
* Activer l'authentification de base sur le dossier Internet/Client
* 
