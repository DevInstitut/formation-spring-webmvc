# Projet Jackson

Jackson est à la base une librairie JSON pour Java.

Elle permet de transformer un objet Java en format JSON et inversement.

## Modules Core

3 modules font la fondation de Jackson :

* `Streaming` : configuration du parseur.
* `Annotations` : personnalisation du JSON généré via des annotations.
* `Databind` : mappage, sérialisation et désérialisation. Ce projet dépend de `Annotations` et `Streaming`.

## Spring MVC & Jackson

Spring Web MVC offre une intégration *naturelle* avec la librairie Jackson.

Pour permettre à Spring Web MVC de convertir automatiquement des objets Java et inversement, il faut ajouter la dépendance vers Jackson Databind.

Exemple :

```xml
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.9.3</version>
</dependency>
```