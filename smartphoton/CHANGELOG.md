## 1.4.00
/!\ Attention /!\ 
Cette version integre les calculs crc à la volé certain changement de parametre peuvent ne pas fonctionner correctement

Note dev
R21 - Modification de l'Intervalle des requetes, faire sauvegarde. QPGS Completement désactivé pour le moment
R22 - Paramètre 12 et 13 en 0.1
R23 - Correction de l'intervalle

- Ajout Calcul CRC
- Ajout des création de capteurs HA (Appareil mqtt => smartphoton => Redemarer Ha)
- Ajout du Capteur conso réseaux (Compatible avec les nouveaux onduleurs)
- Ajout de l'Intervalle de temps entre chaque communication pour l'onduleur en seconde (par default 2 Seconde)
- Ajout d'intervalle de requete suivant le temps intervalle de communication
- Ajout des modes Charge, Bypass, Eco.
- Ajout du deuxieme mptt sur des onduleurs différents
- Ajout du control des LEDs
- Ajout de la configuration de la date et l'heure de l'onduleur à partir du serveur
- Ajout de commandes personnalisées
- Ajout des attributs sur les codes erreurs
- Ajout numéro version et modèle
- Ajout option 130 et 140 au parametre charge max
- Ajout debug
- Modification des options des parametres 12 et 13 voltronic à 0.1
- Vérification des données Voltronic
- Alerte : signalement et tentative de reconnexion suite à un problème de communication
- Remplacement des globals name
- Remplacement des globals Paramètre
- Remplacement des globals Mqtt
- Remplacement des Noms de l'onduleur
- Mise a jour vers nodejs:0.2.5
- Mise a jour node red 4.0.3
- // Préparation Ajout la création thème //
- Refonte de la configuration des globals variables


## 1.3.11
- mise a jour vers nodejs:0.2.4
- Correction du chemin batterie


## 1.3.10
- Correction du Life Cycle sur pylontech
- Mise a jour node red 4.0.2
- Mise a jour node-red-contrib-home-assistant-websocket v0.68.0
- Mise a jour node-red-contrib-modbus v5.42.0
- Mise a jour node-email v3.0.1
- Mise a jour node-red-node-serialport v2.0.3
- 

## 1.3.9
- Modification de la classe watt en power
- Nouvelle gestion pylontech
- Renomage des noms mqtt pour les onduleurs
- Ajout d'un mqtt interne pour utilisation futur
- Correction d'affichage des erreurs onduleur
- Ajout du sensor code erreur en forme de tableau
- Mise à jour base-nodejs v0.2.2
- Mise a jour node-email v3.0.0
- Mise a jour node-red-contrib-modbus v5.40.0
- Mise a jour theme-collection v4.0.1
- Mise a jour node red 4.0.0

## 1.3.8
- Mise a jour node red v3.1.9
- Mise a jour node-red-contrib-home-assistant-websocket v0.64.0
- Mise a jour node-red-contrib-modbus v5.31.0
- Mise a jour base-nodejs v0.2.1

## 1.3.7
- Mise a jour node red v3.1.8
- Mise a jour node-red-contrib-home-assistant-websocket v0.63.1
- Mise a jour node-red-dashboard v3.6.5
- Correction du dashboard smartphoton
- Mise a jour base-nodejs v0.1.4
- Mise a jour node red v3.1.6
- Mise a jour node-red-contrib-bigtimer v2.8.6
- Mise a jour node-red-node-email v2.2.0

## 1.3.6
- Correction connection auto mqtt
- Correction Paramètre 11, 12 et 29 onduleur 24v
- Retour QPGS1
- Ajout code erreur
- Ajout des parametres dans l'appareil smartphoton
- Modification des noms de paramètres par défault pour compatibilités avec d'autres onduleurs
- Ajout de tension de charge en vrac (paramètre 26 sous voltronic)

## 1.3.5
- Correction Paramètre 11 et 2 sur les onduleurs non parallèles

## 1.3.4
- Force les mises à jour des capteurs mqtt

## 1.3.3 /!\ Attention voir forum (Version 1.3) avant installation /!\ 
Voir ici: https://domosimple.eu/forum/thread-691.html
- mise à jour node-red-contrib-home-assistant-websocket to v0.63.0

## 1.3.2  
- mise à jour node-red-contrib-modbus to v5.29.0
- Mise a jour to v3.1.5

## 1.3.1
- Nouvelle configuration des onduleurs
- Nouvelle gestion des serials
- Nouvelle gestion des IPs (elfin)
- Nouvelle gestion des onduleurs parallèles
- Simplification elfin
- Mise en place des multi USBs
- Suppression du nombre d'onduleur via le parallèle
- Ajout de la tension batterie par onduleur
- Possibilité d'activer ou non la récupération des onduleurs parallèles (option multionduleur)
- Ajout de l'appareil mqtt smartphoton (Pour de futurs options)
- Correction parametre 11

## 1.3
- Prise en charge de plusieurs USBs

## 1.2.1
- Mise à jour base-nodejs v0.1.3
- Mise à jour alpine_3_19/nginx to v1.24.0-r15

## 1.2.0
- Ajout conso maison onduleur parallèle
- Ajout serial onduleur parallèle
- Correction sur le paramètre onduleur non parallèle

## 1.2.0
- Ajout Nombre d'onduleur
- info sur les onduleurs secondaires

## 1.1.5
- Correction du mode onduleur

## 1.1.4
- Correction sur la création des sensors mppt
- Correction sur la création du sensor nombre de batterie
- Correction parametre 2 pour onduleur parallèle

## 1.1.3
- Mise à jour base-nodejs en v0.1.2
- Mise à jour addon node red en v17.0.3
- Ajout debug vision
- Ajout Version sur les appareils mqtt

## 1.1.2
- Ajout deuxième entrée mppt

## 1.1.1
- Ajout de l'option Aucune sur le choix des batteries

## 1.1.0
- Mise à jour de certaines aplications
- Mise à jour alpine v3.19
- Mise à jour De addon-node-red v17.0.2 (v3.1.3)

## 1.0.0

