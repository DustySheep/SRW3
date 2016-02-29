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

Premier site 
 - Nom : Site01
 - Repertoire : C:\www\Internet
 - Nom de l'hôte : www.dupont.com
  
 Second site 
 - Nom : Site02
 - Repertoire : C:\www\Intranet
 - Nom de l'hôte : intranet.dupont.com

