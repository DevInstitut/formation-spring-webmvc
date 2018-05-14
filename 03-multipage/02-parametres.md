# Paramètres des méthodes de contrôleur

Les types de paramètres possibles :

|||
|:-:|:-:|
|HttpServletRequest, HttpServletResponse, HttpSession|Requête, Réponse et Session de l'API Servlet|
|@PathVariable|Récupère une partie de l'url et la place dans le paramètre annoté.|
|@RequestParam|Récupère un paramètre de requête web (GET ou POST)|
|@RequestHeader|Récupère un header de requête web|
|@RequestBody|Accède au corps de la requête|
|Model|Classe contenant le modèle objet et permet son enrichissement avant transmission à la vue|


## API Servlet
* Récupérer la requête, la réponse et la session de l'API Servlet.

```java
@Controller
@RequestMapping("/pizzas")
public class PizzaController {

    @RequestMapping(method = RequestMethod.GET)
    public String bonjour(HttpServletRequest request, HttpServletResponse response, HttpSession session) {
        // Du code
    }
}
```

Les	paramètres	de méthode sont	automatiquement valorisés

## @PathVariable
* Récupérer une information dans le chemin de la requête

```java
@Controller
@RequestMapping("/pizzas")
public class PizzaController {

    @RequestMapping(path = "/{nom}", method = RequestMethod.GET)
    public String bonjour(@PathVariable String nom) {
        // Du code
    }
}
```
Le	nom	de	la	variable	correspond	au	nom	du	paramètre.

## Autres exemples de paramètres d'entrée

```java
@RequestMapping(method = RequestMethod.GET)
public String methode(@RequestParam("id") int id, Model model) {
...
}
@RequestMapping("/info")
public void info(@RequestHeader("Accept-Encoding") String encoding,
@RequestHeader("Keep-Alive") long keepAlive) {
...
}
@RequestMapping(value="/pizzas/{id}", method=RequestMethod.GET)
public void post(@PathVariable String id) {
...
}
```