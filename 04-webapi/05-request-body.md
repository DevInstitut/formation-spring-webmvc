# @RequestBody

```java
@RestController
public class ClientController {
    
    // Récupérer un objet Client au format JSON par exemple
    public Message create(@RequestBody Client client, HttpServletResponse response) {
        //....
    }
}
```

Le corps de la requête HTTP pourrait être :

```json
{
  "prenom" : "Hugues",
  "age": 44
}
```