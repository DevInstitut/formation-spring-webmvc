# Notion de contrôleur

Un controller est une classe java annotée par @Controller et sert de point d'entrée à la coordination des traitements et du rendu logique.

Le mapping entre urls et traitements se réalise par apposition de l'annotation `RequestMapping` sur les méthodes gestionnaires.

```java
@Controller
@RequestMapping("/pizzas")
public class PizzaController {
    
    // Cette méthode est exécutée lorsqu'une requête
    // GET /pizzas
    // est reçue
    @RequestMapping(method = RequestMethod.GET)
    public String bonjour() {
        return "vuebonjour";
    }
    
}
```

Par	défaut,	le type retour désigne **le nom d'une vue**.

L'annotation `@ResponseBody` permet de fournir directement la réponse à la requête sans passer par une vue.

```java
@Controller
@RequestMapping("/pizzas")
public class PizzaController {

    @RequestMapping(method = RequestMethod.GET)
    @ResponseBody
    public String bonjour() {
        return "vuebonjour";
    }
}
```
Ici	un	navigateur	affichera "vuebonjour".