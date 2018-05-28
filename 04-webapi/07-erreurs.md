#  Gérer les erreurs via des exceptions
  
```java
// @ControllerAdvice désigne un greffon appliqué aux controlleurs
@ControllerAdvice
public class RestResponseEntityExceptionHandler extends ResponseEntityExceptionHandler {

  // la méthode handleConflict est exécutée lorsqu'un contrôleur émet une exception présente
  // dans la liste définie par l'annotation @ExceptionHandler
  @ExceptionHandler(value = { IllegalArgumentException.class, IllegalStateException.class })
  protected ResponseEntity<Object> handleConflict(RuntimeException ex, WebRequest request) {
      String bodyOfResponse = "This should be application specific";
      return handleExceptionInternal(ex, bodyOfResponse,
        new HttpHeaders(), HttpStatus.CONFLICT, request);
  }
}
```