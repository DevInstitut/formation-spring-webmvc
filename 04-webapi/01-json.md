# Le format JSON

JSON ou **J**ava**S**cript **O**bject **N**otation, est un format de fichier standard
permettant de transmettre des données sous la forme de paires d'attributs clé-valeur et de tableau.

## Types de base JSON

* Nombre

```json
{
  "nombre_eleves" : 12
}
```

* Chaîne de caractères

```json
{
  "prenom" : "Jean"
}
```

* Booléen

```json
{
  "actif" : true
}
```

* Tableau

```json
{
  "liste_personnes" : [
    {
      "prenom" : "Hugues",
      "age" : 42
    },
    {
      "prenom" : "Thierry",
      "age" : 46
    }
  ]
}
```

```json
[
    {
      "prenom" : "Hugues",
      "age" : 42
    },
    {
      "prenom" : "Thierry",
      "age" : 46
    }
]
```


* `null`

```json
{
  "prenom" : "Thierry",
  "age": null
}
```