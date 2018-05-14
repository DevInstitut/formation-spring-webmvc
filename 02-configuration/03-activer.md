# Activer Spring Web MVC

Activer	Spring MVC avec `@EnableWebMvc`.

Exemple de configuration :

```java
@Configuration
@EnableWebMvc
@ComponentScan("fr.pizzeria.spring.mvc.controller")
public class PizzeriaSpringConfig {
}
```