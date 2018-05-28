# @ResponseBody

L'annotation `@ResponseBody` permet de fournir directement la réponse à la requête sans passer par une vue.

Si le paramètre de retour de la méthode est une classe Java alors Spring Web MVC peut transformer l'objet Java en un autre format (par exemple JSON, XML).
  
```java
@Controller
public class ClientController {
    
    @RequestMapping(value = "/client/{clientId}", method = RequestMethod.GET)
    @ResponseBody // parser l'objet Client
    public Client findClient(@PathVariable int clientId) {
        
        return new Client ("Hugues", 12);
    }
    
}
```

Le résultat produit pourrait être :

```json
{
  "prenom" : "Hugues",
  "age" : 12
}
```
