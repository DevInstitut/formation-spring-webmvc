# Récupérer un objet

La requête vers `https://jsonplaceholder.typicode.com/posts/1` produit un résultat de la forme :

```json
{
  "userId": 1,
  "id": 1,
  "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
  "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"
}
```

Nous pouvons alors créer une classe qui est à l'image de cette représentation :

```java
class Post {
    Integer id;
    Integer userId;
    String title;
    String body;
    
    // + Getters et Setters
}
```

Puis utiliser l'outil `RestTemplate` :

```java
RestTemplate rt = new RestTemplate();
Post result = rt.getForObject("https://jsonplaceholder.typicode.com/posts/{id}", Post.class, 1);
```