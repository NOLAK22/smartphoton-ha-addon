# Smartphoton Add-on Home Assistant basé sur node red

Smartphoton est un addon de gestion d'onduleurs et de batteries

**Onduleur**
* [x] Voltronic (wks, Axpert ...)

**Batterie**
* [x] Pylontech
* [x] JKBMS

**Tension Batterie**
* [x] 48 volt
* [x] 24 volt
* [ ] 12 volt

<br /><br />
---
## Installation
---

L'installation de ce module complémentaire est assez simple et ne diffère pas en
comparaison avec l’installation de tout autre module complémentaire Home Assistant.

1. Ajouter le dépot "https://github.com/NOLAK22/smartphoton-ha-addon/" dans la boutique des modules complémentaires
1. Cliquez sur le bouton "Installer" pour installer le module complémentaire..
1. Configurer votre installation dans le menu configuration.
1. Démarrez le module complémentaire "Smartphoton".
1. Vérifiez les journaux de "Smartphoton" pour voir si tout s'est bien passé.


<br /><br />
---
## Onduleur
---  
# Description des paramètres de configuration

## listonduleur
Liste contenant la configuration d’un ou plusieurs onduleurs.

Chaque élément de la liste représente un onduleur avec ses paramètres de connexion et de fonctionnement.

---

**exemple**
```yaml
- chemin: "false"
```
ou pour une communication avec onduleur en usb

```yaml
- chemin: /dev/serial/by-id/usb-Prolific_Technology_Inc._ATEN_USB_to_Serial_Bridge_EQDPb115818-if00-port0
  type: serial
  onduleur: voltronic
  battTension: 48
```

ou pour une communication avec onduleur en ip ou elfin

```yaml
- chemin: 192.168.1.252:8888
  type: ip
  onduleur: voltronic
  battTension: 48
```

---

## chemin
**Type :** string  
Chemin du périphérique utilisé pour la communication avec l’onduleur  
(port série USB sous Linux ou convertisseur réseau).

### Récupérer le chemin via l’interface graphique (USB)

1. Branchez l’onduleur en USB.
2. Ouvrez **Paramètres système**.
3. Allez dans **Matériel**.
4. Cliquez sur **Tout le matériel**.
5. Repérez votre adaptateur USB-Série.

Il sera de la forme :

/dev/serial/by-id/usb-XXXX-if00-port0

---

### Cas d’un convertisseur Réseau → RS232

Si vous utilisez un adaptateur Ethernet vers RS232 (serveur série réseau),  
le champ `chemin` doit contenir l’adresse IP du périphérique.

Il sera de la forme :

192.168.1.50:4001

- `192.168.1.50` → adresse IP du convertisseur
- `4001` → port TCP utilisé pour la communication série

Dans ce cas, la communication ne passe plus par `/dev/serial/` mais directement par le réseau.

---

## type <span style="color:red; font-weight:bold;">Obligatoire</span>
**Type :** string   
Indique le mode de connexion utilisé pour communiquer avec l’onduleur.  


### Valeurs possibles

- `false`  
  → Communication désactivée. (pas d'onduleur compatible)

- `serial`  
  → Communication via port série USB.  
  Le paramètre `chemin` doit contenir :  
  /dev/serial/by-id/usb-XXXX-if00-port0

- `ip`  
  → Communication via réseau (convertisseur Ethernet → RS232).  
  Le paramètre `chemin` doit contenir une adresse IP et port :  

  192.168.1.50:4001

---

## onduleur
**Type :** string  
Spécifie la marque ou le protocole de l’onduleur utilisé.

---

## battTension
**Type :** string  
Tension nominale du parc batterie en volts.  
Exemple : `"48"`

---

## multionduleur (désactivé)
**Type :** boolean  
Ce paramètre **ne fonctionne plus** et est désactivé.  
Il n’a plus d’effet sur la configuration.

- `true` → plusieurs onduleurs  
- `false` → un seul onduleur

---

## full
**Type :** boolean  
Active ou désactive le mode complet de récupération des données.  

Certains onduleurs, notamment les modèles dérivés ou plus anciens, **ne sont pas compatibles avec les nouvelles commandes** et les calculs CRC à la volée.  
Dans ces cas, il est recommandé de **désactiver le mode complet** (`full: false`) pour assurer une communication stable.

---

## interval
**Type :** integer  
Intervalle d’interrogation de l’onduleur.  
Unité : secondes.

**Par défaut :** 2 secondes.  
Augmentez ce temps si votre communication échoue trop souvent.
<br /><br />

| Paramètre        | Type       | Valeurs possibles / Format                     | Description / Remarques                                                                 |
|-----------------|-----------|-----------------------------------------------|-----------------------------------------------------------------------------------------|
| listonduleur     | liste     | Contient un ou plusieurs objets ci-dessous   | Liste de configuration des onduleurs.                                                   |
| └─ chemin        | string    | `/dev/serial/by-id/usb-XXXX-if00-port0` (USB) <br> `192.168.1.50:4001` (IP réseau) | Chemin du périphérique pour communiquer avec l’onduleur. USB ou réseau.                 |
| └─ type          | string    | `false` <br> `serial` <br> `ip`             | Mode de connexion. **Obligatoire**. `false` = désactivé, `serial` = USB, `ip` = réseau. |
| └─ onduleur      | string    | `false` <br> `voltronic`                     | Marque ou protocole de l’onduleur. Peut être désactivé (`false`).                        |
| └─ multionduleur | boolean   | `true` <br> `false`                           | Désactivé, n’a plus d’effet.                                                        |
| └─ battTension   | string    | `48` <br> `24` <br> `12`                     | Tension nominale du parc batterie en volts.                                             |
| └─ full          | boolean   | `true` <br> `false`                           | Active le mode complet de récupération des données.                                     |
| interval         | float     | Entre 0.5 et 10                               | Intervalle d’interrogation de l’onduleur (secondes). Par défaut : 2. Augmenter si la communication échoue. |


Information importante : Les 4 premiers ports sont réservés pour le port série.
Vous pouvez ajouter une connexion IP sur l’un de ces ports, mais dans ce cas, le port série correspondant ne fonctionnera plus.
Pour les autres onduleurs, vous pouvez ajouter autant d’IP que nécessaire.

- onduleur 1 serial ou ip
```yaml
- onduleur 1 serial ou ip ou false
- onduleur 2 serial ou ip ou false
- onduleur 3 serial ou ip ou false
- onduleur 4 serial ou ip ou false
- onduleur 5 ip ou false
- onduleur 6 ip ou false

```
<br /><br />


---
## Batterie
---

### Option: `Choix port Liste batterie ou listbatterie`
Choisir du port usb de la batterie. ("false" pour ne pas l'utiliser)<br />
Chemin : ip ou serial. (<ip>:<port>) ou /dev/serial/by-id/<nom du serial><br />
Type : ip ou serial<br />
Batterie : choix de la batterie. false ou pylontech<br />
nbSlave : Nombre de batterie en esclave (jkbms seulement)


<br /><br />
**exemple**
```yaml
- chemin: "false"
```
ou pour une communication avec batterie en usb

```yaml
- chemin: /dev/serial/by-id/usb-Prolific_Technology_Inc._ATEN_USB_to_Serial_Bridge_EQDPb115818-if00-port0
  type: serial
  batterie: pylontech
```

ou pour une communication avec batterie en ip ou elfin

```yaml
- chemin: 192.168.1.252:8888
  type: ip
  batterie: pylontech
```

<br /><br />
**Options disponibles**

<table width="100%" cellspacing="0" cellpadding="6" border="1">
  <thead>
    <tr>
      <th>Clé</th>
      <th>Chemin</th>
      <th>Type</th>
      <th>Batterie</th>
      <th>NbSlave</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Nom</strong></td>
      <td>chemin</td>
      <td>type</td>
      <td>batterie</td>
      <td>nbSlave</td>
    </tr>
    <tr>
      <td><strong>Valeur par défaut</strong></td>
      <td>false</td>
      <td>serial</td>
      <td>pylontech</td>
      <td>1</td>
    </tr>
    <tr>
      <td><strong>Obligatoire</strong></td>
      <td>oui</td>
      <td>oui</td>
      <td>oui</td>
      <td>non</td>
    </tr>
    <tr>
      <td><strong>Pylontech</strong></td>
      <td>Adresse IP<br /> chemin serial</td>
      <td>ip<br /> serial</td>
      <td>false<br /> pylontech</td>
      <td>1</td>
    </tr>
    <tr>
      <td><strong>JKBMS</strong></td>
      <td>Adresse IP,<br /> chemin serial</td>
      <td>ip<br /> rs485</td>
      <td>false<br /> jkbms</td>
      <td>1<br /> à <br /> 15</td>
    </tr>
  </tbody>
</table>


**Intervalle** <br />
Temps d'attente en secondes entre chaque requête. Remarque : évitez de descendre en dessous de 6. Si vous avez des timeouts fréquents, augmentez ce nombre. 


**JKBMS** <br />
Les commandes sont affiché mais ne sont pas activé
<br /><br />
---
## Nom des entités ou nameEntities
---

Permet de personnalisé les noms des entités onduleur.

<br /><br />
---
## MQTT (obligatoire)
---
Vous devez avoir un broker mqtt (vous pouvez l'intaller via la boutique des module complémentaire. [Addon Mosquitto broker][addon-mqtt])
Il sera ensuite indispenssable d'ajouter intégration mqtt (voir doc mqtt)


### Option: 
**mqttadresse** Adresse de votre broker

**mqttport** port broker

**mqttuser** utilisateur de connexion 

**mqttpass** mot de passe de connexion
<br /><br />



## Changelog & Releases
---

`MAJOR.MINOR.PATCH`

- `MAJOR`: Incompatible or major changes.
- `MINOR`: Backwards-compatible new features and enhancements.
- `PATCH`: Backwards-compatible bugfixes and package updates.


## Support
---
- [Github][depot-mqtt]
- [Site][site]
- [Forum][forum]
- [Documentations Github][documentation]


## Authors & contributors
---
Smartphoton, Jean-luc / Alexis / Romain / Khamel / Samuel

The original setup of this repository is by [Franck Nijhof][frenck].




[addon-badge]: https://my.home-assistant.io/badges/supervisor_addon.svg
[addon-licence]: https://domosimple.eu/licence.php
[addon-config]: http://domosimple.eu/onduleur/
[addon]: https://my.home-assistant.io/redirect/supervisor_addon/?addon=a0d7b954_nodered&repository_url=https%3A%2F%2Fgithub.com%2Fhassio-addons%2Frepository
[addon-mqtt]: https://my.home-assistant.io/redirect/supervisor_addon/?addon=core_mosquitto&repository_url=https%3A%2F%2Fgithub.com%2Fhassio-addons%2Frepository
[depot-mqtt]: https://github.com/jean-luc1203/smartphoton-ha-addon/
[site]: https://smartphoton.fr/
[forum]: http://domosimple.eu/forum/
[documentation]: https://github.com/jean-luc1203/Smartphoton-Documentation
[alpine-packages]: https://pkgs.alpinelinux.org/packages
[contributors]: https://github.com/hassio-addons/addon-node-red/graphs/contributors
[discord-ha]: https://discord.gg/c5DvZ4e
[discord]: https://discord.me/hassioaddons
[forum]: https://community.home-assistant.io/t/home-assistant-community-add-on-node-red/55023?u=frenck
[frenck]: https://github.com/frenck
[issue]: https://github.com/hassio-addons/addon-node-red/issues
[node-red-nodes]: https://flows.nodered.org/?type=node&num_pages=1
[nodered-docs]: https://nodered.org/docs
[nodered]: https://nodered.org
[npm-packages]: https://www.npmjs.com
[reddit]: https://reddit.com/r/homeassistant
[releases]: https://github.com/hassio-addons/addon-node-red/releases
[semver]: http://semver.org/spec/v2.0.0.htm
