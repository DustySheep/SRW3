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
# Chapitre 1
Texte

# Installation du r�le Serveur Web (IIS)
-   S�lection de r�les 
-   Ajouter r�le
-   Cocher la case "Serveur Web (IIS)
-   Dans la rubrique Services de r�les cocher la case ASP.NET

# D�sactivation sites actifs par d�faut
1.   R�les
2.  Serveur Web (IIS)
3.   Gestionaire des services
4.   Sites
5.   Default websites
6.   Click droit (arr�ter)

# Ajout d'un site web (IIS)
*  Click droit sur site - Ajouter un site web
*   Nom du site : Site IIS
*   Chemin : C:\iis_www
*   Liaison port : 8080
*   nom de l'h�te : iis.html