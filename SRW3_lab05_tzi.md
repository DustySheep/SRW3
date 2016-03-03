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
    * Création de 2 répertoires Internet et Intranet dans C:/www
    * Création de 2 fichiers index.html dans les 2 répertoires

*  Dans les settings de la Machine Virtuelle, ajouter une carte réseau afin d'en avoir 1 en bridge et 1 en NAT
*  Pour les tests, modifiers les fichiers hosts de la machine local et virtuelle
*  Mise en place du document par défaut index.html dans les deux sites : Gestionnaire de services / Selection serveur et de site / Dans la partie IIS sélectionner Document par défaut et ajouter XXX.html (présent dans le C:/www)
 

Premier site 
 - Nom : Internet
 - Repertoire : C:\www\Internet
 - Nom de l'hôte : www.dupont.com
 - port 80
 - Adresse ip : 172.17.xxx.xxx
  
 Second site 
 - Nom : Intranet
 - Repertoire : C:\www\Intranet
 - Nom de l'hôte : intranet.dupont.com
 - port 80
 - Adresse ip : 192.168.xxx.xxx


# Création des utilisateurs
Aller dans Configuration / Utilisateurs et groupes locaux / Utilisateurs / Clic droit et créer.
Pareil pour les groupes (Directeur, Comptable, Ingénieur)

# Gestion accès des sites
Afin de rendre l'intranet accessible depuis l'internet, il faut :
*   Selectionner le site Internet dans Serveur/Sites/Internet
*   Clic droit créer un répertoire virtuel
*   Pointer sur le chemin physique de l'intranet (càd C:/www/Intranet)

