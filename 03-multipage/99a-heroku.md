# Déploiement Heroku

Heroku est une plateforme de déploiement d'applications.

## Branche production

* Créer une branche de production

```
git checkout -b production
```

## Configuration déploiement Heroku

* Modifier le fichier `pom.xml` dans la rubrique `<build>`.

```xml
    <build>
		<finalName>paie</finalName>
		<pluginManagement>
			<plugins>
				<plugin>
					<artifactId>maven-war-plugin</artifactId>
					<configuration>
						<failOnMissingWebXml>false</failOnMissingWebXml>
					</configuration>
				</plugin>
			</plugins>
		</pluginManagement>
		
		<!-- PARTIE A AJOUTER -->
		<plugins>
			<plugin>
				<groupId>org.apache.maven.plugins</groupId>
				<artifactId>maven-dependency-plugin</artifactId>
				<version>3.0.2</version>
				<executions>
					<execution>
						<phase>package</phase>
						<goals>
							<goal>copy</goal>
						</goals>
						<configuration>
							<artifactItems>
								<artifactItem>
									<groupId>com.github.jsimone</groupId>
									<artifactId>webapp-runner</artifactId>
									<version>8.5.27.0</version>
									<destFileName>webapp-runner.jar</destFileName>
								</artifactItem>
							</artifactItems>
						</configuration>
					</execution>
				</executions>
			</plugin>
		</plugins>
	</build>
```

* Modifier le fichier `pom.xml` pour ajouter la dépendance vers le driver `postgresql` :

```java
<dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
    <version>42.1.1</version>
    <scope>runtime</scope>
</dependency>
```

* Supprimer les dépendances vers les drivers `MYSQL`, `MariadDB` et `H2`, s'il existent.

* Ajouter un fichier `Procfile` à la racine du dépôt Git avec le contenu suivant :

```
web: java $JAVA_OPTS -jar target/dependency/webapp-runner.jar --port $PORT target/*.war
```
* Créer une nouvelle source de données `dev.paie.config.HerokuDBConfig` comme suit :

```java
package dev.paie.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.jdbc.datasource.DriverManagerDataSource;

import javax.sql.DataSource;
import java.net.URI;
import java.net.URISyntaxException;

@Configuration
public class HerokuDBConfig {

    @Bean
    public DataSource dataSource() throws URISyntaxException {

        URI dbUri = new URI(System.getenv("DATABASE_URL"));

        String username = dbUri.getUserInfo().split(":")[0];
        String password = dbUri.getUserInfo().split(":")[1];
        String dbUrl = "jdbc:postgresql://" + dbUri.getHost() + ':' + dbUri.getPort() + dbUri.getPath() + "?sslmode=require";


        DriverManagerDataSource dataSource = new DriverManagerDataSource();
        dataSource.setUrl(dbUrl);
        dataSource.setUsername(username);
        dataSource.setPassword(password);

        return dataSource;
    }

}
```

* Configurer votre application pour que ce soit cette source de données qui soit prise en compte au démarrage de l'application Web.

* Commiter et Pusher la nouvelle branche sur votre dépôt

## Configuration déploiement Heroku

## Déploiement Heroku

* Aller sur le site d'Heroku : https://www.heroku.com/ et Cliquer sur `Signup`.

![](images/heroku-1.png)

* Remplir le formulaire d'inscription.

![](images/heroku-2.png)

* Cliquer sur `Create new App`.

![](images/heroku-3.png)

* Donner un nom unique à l'application.

![](images/heroku-4.png)

* Cliquer sur Github, se connecter à Github

![](images/heroku-5.png)

* Sélectionner votre projet (version fork)

![](images/heroku-6.png)

* Activer le déploiement automatique en cliquant sur `Enable Automatic Deploys`.

![](images/heroku-7.png) 

* Cliquer sur `Deploy Branch`.

![](images/heroku-8.png)

* Pour visualiser les logs, cliquer sur `More > View logs`.

![](images/heroku-10.png)


Les données sont stockées dans une base PostgreSQL automatiquement configurée par Heroku.

Les informations de connexion sont consultables dans la rubrique `Resource` (en cliquant sur la base de données).

![](images/heroku-11.png)

Si vous souhaitez visualiser le contenu de la base de données distante, vous pouvez installer le client [PgAdmin](https://www.pgadmin.org/).
