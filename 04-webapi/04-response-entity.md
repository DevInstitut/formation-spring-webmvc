# ResponseEntity

```java
@RequestMapping("/handle")
// Le type retour est ResponseEntity
// Cette structure permet de paramétrer la réponse HTTP (status, entêtes, ...)
public ResponseEntity<String> handle() {
    HttpHeaders responseHeaders = new HttpHeaders();
    responseHeaders.set("MyResponseHeader", "MyValue");
    return new ResponseEntity<String>("Hello World", responseHeaders, HttpStatus.CREATED);
}
```