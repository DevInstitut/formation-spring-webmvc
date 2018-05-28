# ResponseEntity

```java

@RestController
public class HandleController {
    
    @RequestMapping("/handle")
    public ResponseEntity<String> handle() {
        HttpHeaders responseHeaders = new HttpHeaders();
        responseHeaders.set("MyResponseHeader", "MyValue");
        return new ResponseEntity<String>("Hello World", responseHeaders, HttpStatus.CREATED);
    }
    
}
```

Noter que le type retour de la méthode est `ResponseEntity<T>` où T désigne le type désigne la nature du contenu du corps de la réponse.

Cette structure permet de paramétrer la réponse HTTP (status, entêtes, ...)

## Personnaliser le code HTTP

```java

@RestController
public class GradeController {
    
    @GetMapping("/list")
    public ResponseEntity<List<Grade>> findAll() {
        List<Grade> allGrades = this.gradeRepo.findAll();
        
        // En précisant en "dur" le code de la réponse via la méthode statique status
        // return  ResponseEntity.status(200).body(allGrades);
        
        // HttpStatus est une énumération regroupant les codes HTTP usuels
        return ResponseEntity.status(HttpStatus.OK).body(allGrades);
    }
    
}


```

## En cas de succès

La réponse est idéalement consituée d'une réponse avec un code HTTP de la famille des 2XX.

Exemple de code HTTP 200 :

```java
@RestController
public class GradeController {

    @GetMapping("/grades")
    public ResponseEntity<List<Grade>> findAll() {
        List<Grade> allGrades = this.gradeRepo.findAll();
        
        // la méthode ok => code HTTP 200
        return ResponseEntity.ok(allGrades);
    }
}
```

Exemple de code HTTP 201 :

```java
@RestController
public class GradeController {
    
        @PostMapping("/grades")
        public ResponseEntity<Grade> create(@RequestParam("code") String code, @RequestParam("nb_heures") BigDecimal nbHeuresBase, @RequestParam("taux") BigDecimal tauxBase) {
            Grade grade = new Grade();
            grade.setCode(code);
            grade.setNbHeuresBase(nbHeuresBase);
            grade.setTauxBase(tauxBase);
            this.gradeRepo.save(grade);
    
            URI uri = MvcUriComponentsBuilder
                    .fromMethodCall(
                            MvcUriComponentsBuilder.on(DemoWebApiController.class).findGrade(grade.getCode())
                    ).build().encode().toUri();
    
            // Réponse
            //      Code = 201
            //      Entête Location = <URI>
            //      Corps = objet Grade
            return ResponseEntity.created(uri).body(grade);
        }
    
        @GetMapping("/grades/{code}")
        public ResponseEntity<Grade> findGrade(@PathVariable String code) {
            return ResponseEntity.ok(this.gradeRepo.findByCode(code));
        }
}
```