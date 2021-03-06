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
*   Puis cr�ation similaire d'un r�pertoire virtuel dans intranet vers internet

# Gestion Espace priv� de l'intranet
* Cr�ation d'un dossier utilisateur pour chaque utilisateur
* Pour ce dossier, dans s�curit� / avanc�, supprimer Utilisateurs et ajouter l'utilisateur correspondant au dossier "mdupont" par ex ainsi que le groupe "IIS_IUSRS".
* Verifier que l'authentification de base soit bien pr�sente
* Le partie client sera disponible � cette adresse : www.dupont.com/intranet/mdupont

# Gestion Espace client de l'internet
* Utilisateur client, login : dclient, password : Qwertz123
* Dans les autorisation /s�curit� du dossier Internet/client supprimer le groupe "utilisateurs" et ajouter dclient ainsi que IIS_IUSRS
* Activer l'authentification de base sur le dossier Internet/Client
* D�sormais seul le dclient et Administrateur peuvent acc�der � : http://www.dupont.com/client/
* Ajout du groupe ing�nieur dans les autorisations du dossier Internet/Client d�sormais les ing�nieurs ont acc�s au dossier client
* Ajout du groupe ing�nieur au Sites internet et intranet


# Service de gestion

* Installation des services de r�les "Gestionnaire de sites internet"
* Sur le serveur, cliquer sur service de gestion, s�lectionner l'ip en 192.168 et activer la connexion � distance.
* Dans les sites internet et intranet sous Gestion/Autorisations du Gestionnaire des services Internet, ajouter le groupe ing�nieurs dans l'action "Autoriser l'utilisateur"
* Pour pouvoir r�aliser cette t�che, le service doit �tre arr�t�.


# S�curit�
## impl�mentation Certificat auto-sign� sur le serveur
*   Dans Gestionnaire des services Internet (IIS) cliquer sur le serveur / Affichage des fonctionnalit�s / Certificats de serveur (Section IIS) / Cr�er un certificat auto-sign�
*   Lui donner un nom par exemple "certif_dupont"
*   Selectionner en suite un site puis aller dans ses liaisons
*   Ajouter une liaison, port : 443, type : https, l'adresse ip reste la m�me.
 ## Activation SSL
* S�lectionner un site puis "param�tres SSL" dans les param�tres SSL cocher la case Exiger SSL et "Ignorer".
* Le site est d�sormais accessible sous https://www.dupont.com ou https://intranet.dupont.com

## Redirections des URL 
* D�cocher la case "Exiger SSL" dans les param�tres des sites (case coch� pr�c�demment)
* T�l�charger et installer le module "URL Rewrite" de microsoft (http://www.iis.net/downloads/microsoft/url-rewrite)
* Remplacer le contenu de web.config dans le repertoire racine d'intranet par :
```
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
 <system.webServer>
    <rewrite>
        <rules>
            <rule name="HTTP to HTTPS redirect" stopProcessing="true">
            <match url="(.*)" />
            <conditions>
            <add input="{HTTPS}" pattern="off" ignoreCase="true" />
            </conditions> 
            <action type="Redirect" redirectType="Found"
url="https://{HTTP_HOST}{REQUEST_URI}" />
            </rule>
        </rules>
    </rewrite>
    </system.webServer>
</configuration>
```
* Dans le fichier web.config du repertoire mdupont coller ce code :
```
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
<system.webServer>
    <rewrite>
    <rules>
       <rule name="private client folder" stopProcessing="true">
          <match url="(.*)" />
          <conditions>
             <add input="{HTTPS}" pattern="off" ignoreCase="true" />
           </conditions>
           <action type="Redirect" redirectType="Found" url="https://{HTTP_HOST}{REQUEST_URI}" />
         </rule>
   </rules>
    </rewrite>
</system.webServer>
</configuration>
```
* Dans le r�pertoire Internet/Client 
* Remplacer le contenu de web.config par ce code :
```
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <system.webServer>
        <rewrite>
           <rules>
                <rule name="clients space" stopProcessing="true">
                    <match url="(.*)" />
                        <conditions>
                             <add input="{HTTPS}" pattern="off" ignoreCase="true" />
                         </conditions>
                    <action type="Redirect" redirectType="Found"url="https://{HTTP_HOST}{REQUEST_URI}" />
                </rule>
            </rules>
          </rewrite>
    </system.webServer>
</configuration>
```

*   La redirection en https est maintenant pr�sente lors de la navigation 




    
