# Formulaires

Un formulaire Spring est une page web classique.

* Spring fournit un ensemble de taglibs pour faciliter la création de formulaire et le binding de données avec la partie serveur.Création de formulaires.

* Ecriture du gestionnaire d'envoi de formulaire.

```java
@Controller
@RequestMapping("/clientForm")
public class ClientFormController {
    ....
    @RequestMapping(method = RequestMethod.GET)
    public String setupForm(Model model) {
        // Création de l'objet du modèle.
        Client client = new Client();
        //Liaison du modèle et de l'objet.
        model.addAttribute("client", client);
        //Renvoi du nom logique de la vue formulaire.
        return "clientForm";
    }
    ...
}
```

## Vue du formulaire

L'utilisation des taglibs est activée dans une JSP par la directive :

```xml
<%@ taglib prefix="form" uri="http://www.springframework.org/tags/form"%>
```

* Tous les éléments classiques des formulaires sont présents
(checkbox, textarea, ...).

* Les gestionnaires d'événements sont aussi pris en compte (onclick, ...).

* En ajout, la liaison aux données et la gestion des messages d'erreurs.


https://docs.spring.io/spring/docs/4.2.x/spring-framework-reference/html/spring-form-tld.html

## Exemple de formulaire

```html
<%-- pas besoin de définir une action, celle par défaut convient --%>
<form:form method="post" modelAttribute="client">
    <table>
        <tr>
            <td>Nom</td>
            <td><form:input path="nom" /></td>
        </tr>
        <tr>
            <td>Prenom</td>
            <td><form:input path="prenom" /></td>
        </tr>
    </table>
</form:form>
```
L'attribut modelAttribute lie les données envoyées à un objet du modèle côté serveur.
Les données retournées peupleront le bean identifié.

## Envoi de formulaire

```java
@RequestMapping(method = RequestMethod.POST)
public String submitForm(@ModelAttribute("client") Client client) {
    clientService.make(client);
    return "clientSuccess";
}
```

L'objet client est peuplé selon les données de l'attribut du modèle nommé `client`.
Cet attribut de modèle a été déclaré dans le formulaire.

