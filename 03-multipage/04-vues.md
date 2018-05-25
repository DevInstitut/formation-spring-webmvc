# Gestion des vues

* Les classes d'implémentation de l'interface `ViewResolver` fournissent le mécanisme de sélection des vues selon un identifiant logique retourné par la méthode gestionnaire du controller.

* La plus courante d'utilisation avec les JSPs est InternalResourceViewResolver qui extrait la ressource depuis un chemin fabriqué avec le nom logique.

* Le nom logique est préfixé et suffixé pour fournir le chemin de la vue.

Exemple :

```xml
<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
    <property name="prefix" value="/WEB-INF/views/" />
    <property name="suffix" value=".jsp" />
</bean>
```

Le contrôleur est chargé de sélectionner la vue consécutive à un traitement.

Pour cela , il renvoie un nom logique en fin de traitement.

La nature polymorphique du type de retour implique différents moyens de sélection de la vue.

```java
@RequestMapping("/helloWorld")
public ModelAndView helloWorld() {
    ModelAndView mav = new ModelAndView();
    mav.setViewName("helloWorld");
    mav.addObject("message", "Hello World!"); // donnée envoyée à la vue
    return mav;
}

@RequestMapping("/helloWorld")
public String helloWorld() {
    return "helloWorld";
}
```

Au regard de la configuration du `ViewResolver` précédent, la vue sélectionnée sera le fichier `/WEB-INF/views/helloword.jsp`.

Dans l'exemple précédent, la méthode `helloWorld` fournit à la vue les données par le biais du modèle transmis.

La classe ModelAndView gère non seulement le nom logique de la vue mais aussi le modèle de la vue.

Depuis la vue, l'attribut du modèle est directement référençable comme tout bean exposé à une page web.

## Exemple

Un contrôleur :

```java

@Controller
public class PeopleController {
    
    @RequestMapping(method=RequestMethod.GET,value="list")
    public ModelAndView listPeople() {
        ModelAndView mav = new ModelAndView();
        List<Person> people = personDao.getPeople();
        mav.addObject("people",people); // alimentation du modèle
        mav.setViewName("list");
        return mav;
    }
}
```

Une vue (`/WEB-INF/views/list.jsp`) :

```xml

<c:forEach items="${people}" var="person">
    <a href="edit?id=${person.id}">
        ${person.id} - ${person.firstName} ${person.lastName}
    </a>
    <br/>
</c:forEach>
```