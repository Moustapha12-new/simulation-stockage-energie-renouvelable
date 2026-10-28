# Étude d'un système hybride solaire–diesel–batterie

**Simulation énergétique pour un ménage à Abuja (Nigeria) · Données 2025 · Python et Power BI**

**Groupe de travail** : Moustapha **IBRAHIM DJAMA**, **Thomas DHUNARA** et **Mariel FRESNEL**  
Formation : **ECAM-EPMI — Ingénieur en Système Électrique (ISE)**

> **État du dossier : étude pédagogique en reprise et en vérification.** Cette archive contient une base de simulation et des visuels préexistants fournis pour servir de support de travail. Les graphiques et tableaux de bord sont des **documents de référence**, pas des livrables que les trois membres du groupe déclarent avoir créés de zéro. Les calculs devront être contrôlés avant une remise.

## 1. Sujet de l'étude

L'étude porte sur l'alimentation électrique d'un ménage à partir de trois ressources : des panneaux photovoltaïques, une batterie et un groupe électrogène diesel. L'objectif est d'étudier leur complémentarité, la couverture de la demande électrique et les effets potentiels sur le recours au diesel.

Le modèle suit une logique simple : le photovoltaïque alimente en priorité la charge ; le surplus peut charger la batterie ; lorsque le soleil est insuffisant, la batterie puis le diesel complètent l'énergie requise.

![Organisation générale du traitement](illustrations/01_organisation_de_l_etude.png)

## 2. Architecture de principe

![Architecture du système hybride](illustrations/02_architecture_systeme_hybride.png)

## 3. Données et hypothèses

| Élément | Valeur ou indication |
|---|---|
| Localisation | Abuja, Nigeria |
| Période | 1er janvier au 31 décembre 2025 |
| Données solaires | NASA POWER, indicateur `ALLSKY_SFC_SW_DWN` |
| Résolution | Journalière |
| Puissance PV utilisée dans le fichier de résultats | **8 kW** |
| Demande journalière utilisée dans le fichier de résultats | **35 kWh/jour** |
| État de charge maximal observé dans les résultats | 10 kWh (à rapprocher de la capacité de batterie supposée) |

Les valeurs de puissance photovoltaïque et de demande ont été rapprochées des premières lignes du CSV fourni. Les hypothèses relatives au rendement photovoltaïque, à la consommation diesel, à la batterie et aux coûts doivent encore être documentées.

Le carnet `calculs/modele_solaire_diesel_batterie.ipynb` reprend les calculs de production solaire et de déficit, avec des chemins adaptés à cette archive. Il **ne recalcule pas à lui seul** l'ensemble des coûts, émissions et indicateurs présentés ci-dessous.

## 4. Méthode de calcul

Pour une première estimation journalière :

\[
E_{PV} \approx H \times P_{PV}
\]

avec `H` l'irradiation journalière (kWh/m²/j) et `P_PV` la puissance nominale du système (kW). Cette simplification est équivalente à négliger les pertes : un modèle plus réaliste devra intégrer un ratio de performance et les rendements de conversion.

Le déficit théorique restant pour la batterie ou le groupe électrogène est estimé par :

\[
E_{manquant} = \max(E_{charge} - E_{PV},\;0)
\]

L'analyse complète doit ensuite tenir compte des limites de charge et de décharge, de l'énergie stockée, des pertes et des paramètres de fonctionnement du groupe diesel.

## 5. Aperçu des visualisations de référence

Les captures ci-dessous sont recadrées pour préserver les graphiques sans informations personnelles. Elles représentent des **résultats de référence à confirmer**, et non une nouvelle exécution certifiée de la simulation.

### Tableau de bord général

![Tableau de bord général](illustrations/03_tableau_bord_synthese.png)

### Bilan énergétique mensuel

![Bilan énergétique mensuel](illustrations/04_bilan_energetique_mensuel.png)

### Analyse économique

![Analyse économique](illustrations/05_analyse_economique.png)

### Bilan environnemental

![Bilan environnemental](illustrations/06_bilan_environnemental.png)

### Performances de la batterie

![Performances de la batterie](illustrations/07_performances_batterie.png)

## 6. Ce qu'il reste à contrôler

- Reconstituer la simulation **complète** et retrouver, à partir des hypothèses, les colonnes concernant la batterie, la consommation diesel, les coûts et les émissions de CO₂.
- Vérifier que les unités du SOC, des économies d'énergie, des litres de diesel et des coûts sont cohérentes.
- Vérifier les hypothèses et l'origine des prix du diesel indiqués pour 2025 et 2026.
- Vérifier les agrégations et les filtres des tableaux de bord Power BI ; certaines captures sont filtrées sur une partie de l'année.
- Ajouter une analyse personnelle des résultats après comparaison avec une nouvelle simulation exécutée par le groupe.

**Attention :** les résultats du CSV de référence ont été calculés avec 8 kW et 35 kWh/jour, alors que le carnet fourni au départ utilisait 5 kW et 40 kWh/jour. Le carnet a été harmonisé pour le calcul solaire simplifié, mais la chaîne complète de calcul reste à reconstituer.

## 7. Contenu de l'archive

```text
Etude_stockage_energie_.../
├── README.md
├── dependances.txt
├── donnees/
│   └── ensoleillement_abuja_2025.csv
├── calculs/
│   └── modele_solaire_diesel_batterie.ipynb
├── resultats/
│   └── simulation_systeme_hybride.csv
├── tableaux_de_bord/
│   └── tableau_de_bord_systeme_hybride.pbix
└── illustrations/
    ├── 01_organisation_de_l_etude.png
    ├── 02_architecture_systeme_hybride.png
    ├── 03_tableau_bord_synthese.png
    ├── 04_bilan_energetique_mensuel.png
    ├── 05_analyse_economique.png
    ├── 06_bilan_environnemental.png
    └── 07_performances_batterie.png
```

La structure a été simplifiée : répertoires imbriqués supprimés, noms de fichiers francisés, doublon des résultats sans extension supprimé. Les **noms de colonnes du CSV restent identiques** afin de préserver la compatibilité avec les jeux de données et Power BI.

## 8. Ouvrir et explorer

Depuis le dossier du projet :

```bash
python -m pip install -r dependances.txt
jupyter notebook calculs/modele_solaire_diesel_batterie.ipynb
```

Exécuter les cellules du carnet dans l'ordre. Le fichier `.pbix` s'ouvre dans Power BI Desktop. Si la source CSV n'est plus trouvée lors de l'actualisation, la redéfinir vers `resultats/simulation_systeme_hybride.csv`.

## 9. Équipe et statut des documents

- **Moustapha IBRAHIM DJAMA**
- **Thomas DHUNARA**
- **Mariel FRESNEL**


