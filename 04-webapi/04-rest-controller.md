# @RestController

```java
@RestController = @Controller + @ResponseBody
```

@RestController se positionne sur une classe.

```java
@RestController
public class PizzaResource {
    
    @RequestMapping(value = "/client/{clientId}", method = RequestMethod.GET)
    // @ResponseBody // plus besoin de mettre cette annotation
    public Client findClient(@PathVariable int clientId) {
        return new Client ("Hugues", 12);
    }

}
```