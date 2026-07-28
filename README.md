# restaurants-france

[Tentative app]

> ℹ️ **`geomap-app` est un nom de travail provisoire.**

---

## Objectif du repo

Le projet est encore jeune et ses parties évoluent ensemble. Les regrouper au
même endroit me permet de partager la documentation, de versionner l'ensemble d'un
seul tenant et d'éviter la coordination pénible entre plusieurs dépôts. Si un
module gagne un jour un cycle de vie autonome (publication indépendante,
réutilisation ailleurs), il pourra être extrait dans son propre dépôt.

---

## Organisation

```text
restaurants-france/
├── data-sources/            # D'où viennent les données brutes
│   └── openstreetmap/       # Extraction OSM via Overpass  ✅ documenté
│       ├── queries/         #   requêtes Overpass QL
│       ├── scripts/         #   script d'extraction -> GeoJSON
│       └── data/            #   sorties (non versionnées)
│
├── pipeline-sirene/         # (à venir) import SIRENE + géocodage IGN
├── web/                     # (à venir) l'interface : carte Leaflet + fiches
└── docs/                    # (à venir) notes transverses, schéma de données
```

Seul le module **`data-sources/openstreetmap/`** est fourni ici. Les autres
dossiers sont des emplacements réservés : ils accueilleront le pipeline SIRENE
et l'application web au fur et à mesure.

---

## Les sources de données

| Source | Rôle | Licence |
|---|---|---|
| **OpenStreetMap** (via Overpass) | Noms d'usage, cuisine, contacts, terrasse… | ODbL |
| **SIRENE** (INSEE) | Socle administratif : SIRET, activité, adresse officielle | Licence Ouverte 2.0 |
| **Géoplateforme / IGN** | Géocodage des adresses en coordonnées GPS | — |

L'idée : SIRENE fournit une base nationale fiable et exhaustive, OpenStreetMap
l'enrichit avec des informations de terrain, et l'IGN fournit les coordonnées.

---

## Démarrage rapide (module OpenStreetMap)

```bash
cd data-sources/openstreetmap
python scripts/fetch_overpass.py --commune Toulouse
# -> data/Toulouse.geojson
```

Détails et explication de la requête : voir
[`data-sources/openstreetmap/README.md`](data-sources/openstreetmap/README.md).

---

## Licences

- **Code** : MIT (voir [`LICENSE`](LICENSE)).
- **Données** : chaque source conserve sa propre licence. Les données
  OpenStreetMap sont sous **ODbL** et imposent l'attribution
  « © les contributeurs d'OpenStreetMap ». Voir le README du module concerné.
