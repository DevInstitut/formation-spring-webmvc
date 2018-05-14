# Configuration via `web.xml`

## Contrôleur frontal

La servlet Spring officie comme Front Contrôleur (point d'entrée redirecteur).


```xml
<web-app>
    <servlet>
        <!-- Fichier de configuration Spring par défaut	<nom-servlet>-servlet.xml. Ici :dispatcher-servlet.xml -->
        <servlet-name>dispatcher</servlet-name>
        <!-- Contrôleur	principal de Spring	MVC -->
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <load-on-startup>1</load-on-startup>
    </servlet>
    <servlet-mapping>
        <servlet-name>dispatcher</servlet-name>
        <url-pattern>/mvc</url-pattern>
    </servlet-mapping>
</web-app>
```


Par défaut, le fichier de définition Spring portant le nom de <servlet-name>-servlet.xml est chargé depuis le répertoire WEB-INF.

Le nom de cette ressource est configurable en ajoutant :

```xml
<init-param>
    <param-name>contextConfigLocation</param-name>
    <param-value>/WEB-INF/config/web-application-config.xml</param-value>
</init-param>
```

# Contexte Général de Spring

Le contexte général de Spring ajouté par `listener`.

Il s'agit d'un listener de type "ServletContextListener" (création et destruction de contexte de servlet).

```xml
<listener>
    <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
</listener>
```