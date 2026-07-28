# Récupérer les données geo.json de lieux via Overpass Turbo

Objectif : obtenir un fichier **GeoJSON** contenant tous les lieux spécifiques d'une
commune, en quelques clics et sans rien installer.

## Étapes

1. Ouvre le site **<https://overpass-turbo.eu>**.

2. Dans l'éditeur à gauche, **efface tout** et **colle** cette requête :

   ```overpassql
   [out:json][timeout:180];
   area["name"="Toulouse"]["admin_level"="8"]->.a;
   (
     node["amenity"="restaurant"](area.a);
     way["amenity"="restaurant"](area.a);
   );
   out center tags;
   ```

3. Pour une autre ville, remplace **`"Toulouse"`** par le nom voulu
   (ex. `"Bordeaux"`).

4. Clique sur **Exécuter** (bouton en haut à gauche).
   Les restaurants apparaissent sous forme de points sur la carte.

5. Clique sur **Exporter** (en haut), puis **télécharger → GeoJSON**.

6. Tu obtiens un fichier `export.geojson` : c'est le fichier à utiliser dans
   l'application. Renomme-le si tu veux (ex. `Toulouse.geojson`).

## Ce que fait la requête (en clair)

- `area["name"="Toulouse"]["admin_level"="8"]` → délimite la zone de recherche
  à la **commune** (en France, `admin_level=8` = commune).
- `node` et `way` avec `amenity=restaurant` → récupère les restaurants, qu'ils
  soient cartographiés comme un point ou comme un bâtiment.
- `out center tags` → renvoie **un point par restaurant** avec toutes ses infos
  (nom, cuisine, adresse…).

## Si ça ne marche pas

- **Aucun résultat** : vérifie l'orthographe exacte du nom de la commune.
- **Deux villes ont le même nom** : ajoute le code INSEE pour lever l'ambiguïté,
  par exemple `area["ref:INSEE"="31555"]->.a;` pour Toulouse.
- **Réessayer** : Le site peut rapidement être surchargé selon la requête, réessayer jusqu'à ce que le résultat soit bien pris en charge.
