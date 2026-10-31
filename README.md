# Carte Enedis Linky V2

[![HACS Custom](https://img.shields.io/badge/HACS-Custom-orange.svg)](https://hacs.xyz/docs/faq/custom_repositories)
[![Release](https://img.shields.io/github/v/release/Marlboro62/content-card-linky-v2?include_prereleases)](https://github.com/Marlboro62/content-card-linky-v2/releases)

La carte Linky **classique** ([content-card-linky](https://github.com/MyElectricalData/content-card-linky)), compatible avec **MyElectricalData V2** (add-on « MyElectricalData new », mode client local) comme avec la V1.

🎮 **[Essayer la démo en ligne](https://marlboro62.github.io/content-card-linky-v2/docs/demo.html)** : la vraie carte avec des données simulées, sans installer Home Assistant. Elle permet de comparer les exports V1 et V2, les modes de calcul des prix, et les situations Tempo et EcoWatt.

## Captures

Dans Home Assistant, avec l'export MyElectricalData V2 et une offre Tempo :

<img src="https://raw.githubusercontent.com/Marlboro62/content-card-linky-v2/main/images/carte-tempo.png" alt="Carte Enedis Linky V2 dans Home Assistant : consommation, prix Tempo calculés, EcoWatt et jours Tempo restants" width="400">

L'éditeur visuel en français, avec le calcul des prix :

<img src="https://raw.githubusercontent.com/Marlboro62/content-card-linky-v2/main/images/editeur-prix.png" alt="Éditeur visuel de la carte, section Prix" width="700">

Thème clair avec le camembert Tempo (démo) :

<img src="https://raw.githubusercontent.com/Marlboro62/content-card-linky-v2/main/images/demo-clair-camembert.png" alt="Carte en thème clair avec le camembert Tempo" width="400">

## Ce qui change par rapport à la carte d'origine (1.5.6)

Le détail complet est dans les [notes de la version 0.2.0](https://github.com/Marlboro62/content-card-linky-v2/releases/tag/v0.2.0).

- **EcoWatt** : les 24 cases et la ligne des heures s'affichent avec l'export V2. Les heures au format `0h 00min` (V2) et `00 h` (V1) sont lues toutes les deux ([MyElectricalData/myelectricaldata_new#190](https://github.com/MyElectricalData/myelectricaldata_new/issues/190)).
- **EcoWatt** : le niveau `0` (production décarbonée chez RTE) s'affiche en vert.
- **Tempo** : les jours restants s'affichent au format `288 / 300`, avec la V1 comme avec la V2.
- **Période annuelle personnalisée** : l'évolution annuelle suit `annual_period_start` quand l'export le fournit.
- **Camembert Tempo** (option `showTempoPieChart`) : répartition de la consommation en 6 parts, bleu, blanc et rouge en HC et en HP. Avec la V2, il est calculé sur l'historique publié (31 jours).
- Nouveau type de carte, `custom:content-card-linky-classic` : elle peut être installée à côté de la carte d'origine.

## Installation

### Via HACS

1. HACS → menu ⋮ → **Dépôts personnalisés**.
2. Dépôt : `https://github.com/Marlboro62/content-card-linky-v2`, type **Tableau de bord** (Lovelace).
3. Installez **Carte Enedis Linky V2**, puis faites Ctrl+F5 dans le navigateur.

Pour une version bêta, activez d'abord « Afficher les versions bêta » dans la fiche de la carte dans HACS.

### Manuellement

Copiez le contenu du dossier `dist` dans `www/community/content-card-linky-v2/`, puis ajoutez la ressource :

```yaml
url: /local/community/content-card-linky-v2/content-card-linky-v2.js
type: module
```

## Configuration

La carte se configure dans l'éditeur visuel. En YAML, avec les entités de l'export Home Assistant de MyElectricalData V2 (`<pdl>` est votre numéro de point de livraison) :

```yaml
type: custom:content-card-linky-classic
entity: sensor.myelectricaldata_linky_<pdl>_consumption
titleName: LINKY
nbJoursAffichage: "7"
showEcoWatt: true
showEcoWattJ12: true
ewEntity: sensor.myelectricaldata_ecowatt_j0
ewEntityJ1: sensor.myelectricaldata_ecowatt_j1
ewEntityJ2: sensor.myelectricaldata_ecowatt_j2
showTempo: true
tempoEntityInfo: sensor.myelectricaldata_tempo_info
tempoEntityJ0: sensor.myelectricaldata_tempo_today
tempoEntityJ1: sensor.myelectricaldata_tempo_tomorrow
```

Le type est `content-card-linky-classic` et non `content-card-linky-v2` : ce nom est déjà réservé par la [carte Linky New](https://github.com/Marlboro62/content-card-linky-new).

Si vous avez changé le préfixe des entités dans l'export (`entity_prefix`), adaptez les noms en conséquence.

### Venir de la carte d'origine

Dans le YAML de la carte, remplacez `type: custom:content-card-linky` par `type: custom:content-card-linky-classic`. Les options sont les mêmes.

### Options

| Option | Défaut | Rôle |
| --- | --- | --- |
| `entity` | | Capteur de consommation MyElectricalData (obligatoire) |
| `titleName` | `LINKY` | Titre |
| `nbJoursAffichage` | `7` | Nombre de jours d'historique |
| `showHistory` | `true` | Historique sur plusieurs jours |
| `showHeader` | `true` | En-tête (consommation de la veille) |
| `showPeakOffPeak` | `true` | Répartition heures pleines / heures creuses |
| `showPrice` | `true` | Prix de l'historique |
| `showDayPrice` | `false` | Prix par jour |
| `showDayPriceHCHP` | `false` | Prix HC / HP par jour |
| `showDayHCHP` | `false` | Consommation HC / HP par jour |
| `showDayMaxPower` | `false` | Puissance maximale, avec dépassement signalé |
| `showDayName` | `long` | Jours de la semaine : `short`, `narrow` ou `long` |
| `showCurrentMonthRatio` | `true` | Évolution du mois en cours |
| `showMonthRatio` | `true` | Évolution du mois précédent |
| `showWeekRatio` | `false` | Évolution de la semaine |
| `showYesterdayRatio` | `false` | Évolution de la veille |
| `showYearRatio` | | Évolution annuelle |
| `showTitle` | `false` | Affiche le titre |
| `showIcon` | `false` | Icône Linky |
| `showInTableUnit` | `false` | Unités dans le tableau |
| `showTitleLign` | `false` | Titre de chaque ligne |
| `showError` | `true` | Messages d'erreur |
| `showEcoWatt` | `false` | EcoWatt du jour (`ewEntity`) |
| `showEcoWattJ12` | `false` | EcoWatt du lendemain et du surlendemain (`ewEntityJ1`, `ewEntityJ2`) |
| `showTempo` | `false` | Tempo : couleurs du jour et du lendemain, jours restants |
| `showTempoPieChart` | `false` | Camembert de la consommation Tempo en 6 parts |

### Prix : Base, HC/HP et Tempo

Quand l'export ne fournit pas les coûts (`-1`, par exemple avec une offre Tempo), la carte les calcule elle-même : coût du jour en en-tête, lignes Prix, Prix HC et Prix HP de l'historique. Ces réglages sont aussi dans la section **Prix** de l'éditeur visuel.

| Option | Rôle |
| --- | --- |
| `priceMode` | `auto` (défaut), `base`, `hchp`, `tempo` ou `export` |
| `kWhPrice` | Prix du kWh en Base : nombre (`0.2016`) ou entité (`input_number.prix_base`) |
| `kWhPriceHC` / `kWhPriceHP` | Prix du kWh en heures creuses et en heures pleines : nombres ou entités |
| `tempoPrices` | Prix Tempo, à renseigner seulement pour remplacer les capteurs `sensor.myelectricaldata_tempo_price_*` : `blue_hc`, `blue_hp`, `white_hc`, `white_hp`, `red_hc`, `red_hp` (nombres ou entités) |

- **`auto`** : la carte complète seulement les coûts absents de l'export. Elle utilise `kWhPriceHC` et `kWhPriceHP` s'ils sont renseignés, sinon `kWhPrice`, sinon les prix Tempo publiés par l'export selon la couleur de chaque jour.
- **`base`**, **`hchp`** ou **`tempo`** : la carte calcule tous les coûts avec cette formule, et remplace ceux de l'export.
- **`export`** : la carte affiche les coûts de l'export tels quels, comme la carte d'origine.

En Tempo, le coût d'un jour vaut HC × prix HC de sa couleur + HP × prix HP de sa couleur. Il faut pour cela que l'export publie la répartition HC/HP du jour (`dailyweek_HC` et `dailyweek_HP`).

```yaml
# Exemple : prix HC/HP saisis à la main
priceMode: hchp
kWhPriceHC: 0.1696
kWhPriceHP: 0.2146
```

## Limites connues avec la V2

- Le **camembert Tempo** lit les attributs `tempo_percentage_*` de la V1. L'export V2 ne les publie pas : la carte calcule alors la répartition sur l'historique publié (31 jours), et non sur l'année.
- La **période annuelle personnalisée** dépend de l'attribut `annual_period_start`, absent de l'export V2 : l'évolution annuelle suit alors l'année civile.

## Support

Bugs et demandes : [issues GitHub](https://github.com/Marlboro62/content-card-linky-v2/issues). Masquez votre numéro de PDL dans les captures.

## Merci

Cette carte reprend [content-card-linky](https://github.com/MyElectricalData/content-card-linky) de MyElectricalData, elle-même basée sur le travail de [@saniho](https://github.com/saniho/content-card-linky). Licence MIT.

## Nom du projet et forks

Ce dépôt est la seule source officielle de **Carte Enedis Linky V2** (releases, HACS, support),
maintenu par [Marlboro62](https://github.com/Marlboro62).

La licence MIT autorise à copier, modifier et redistribuer le code. Si vous publiez une version modifiée :

- gardez les mentions de copyright du fichier [`LICENSE`](https://github.com/Marlboro62/content-card-linky-v2/blob/main/LICENSE) (© Nicolas Bourasseau et © Marlboro62) ;
- **donnez-lui un autre nom** et d'autres types de carte (`custom:content-card-linky-classic` sont ceux de ce dépôt) :
  Home Assistant ne peut pas charger deux cartes du même type, et personne ne doit confondre les deux versions dans HACS ;
- ne la présentez pas comme la version officielle et n'orientez pas vers ce dépôt les demandes
  de support qui concernent votre version.

Une correction ou une idée ? Les **pull requests** et les **issues** sont les bienvenues ici :
elles profitent à tous les utilisateurs.
