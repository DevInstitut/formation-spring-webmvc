# @ResponseBody
  
```java
@RequestMapping(value = "/client/{clientId}", method = RequestMethod.GET)
@ResponseBody // parser l'objet Client
public Client findClient(@PathVariable int clientId) {
  return clientService.get(clientId);
}
```