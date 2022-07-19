# Neo4j

Dado el requerimiento detallado a continuación:

Se precisa diseñar un blog de noticias donde los usuarios registrados puedan publicar sus comentarios:

  * Cada autor tiene:
      - nombre
      - nombre de usuario (único)
      - cuenta de Twitter (única)
      - teléfono de contacto.

  * Las noticias tienen:
      - título 
      - cuerpo 
      - fecha de publicación

      - publicadas por un autor
      - puntuadas por usuarios

  * Los comentarios de las noticias tienen :
      - persona
      - comentario escrito
      - fecha 


## 1- Diseño del Modelo

1. Confeccionar y especificar el modelo de datos necesario para resolver el requerimiento.

2. Gráfico del modelo.

### Creacion de nodos

1. **Autor**

```
CREATE( A1: Autor {name: 'Nikola Tesla', username: 'Master of Lightning', account: '@lightningNetwork',  phone: '+33 1234 5678' })
CREATE( A2: Autor {name: 'bot32', username: 'bot32', account: '@bot32',  phone: '+33 1234 5678' })
CREATE( A3: Autor {name: 'bot256', username: 'bot256', account: '@bot256',  phone: '+33 1234 5678' })
CREATE( A4: Autor {name: 'bot2048', username: 'bot2048', account: 'bot2048',  phone: '+33 1234 5678' })


CREATE CONSTRAINT unique1 FOR (p:Autor) REQUIRE p.account IS UNIQUE;
CREATE CONSTRAINT unique2 FOR (p:Autor) REQUIRE p.username IS UNIQUE;
```


2. **Noticia**

```
CREATE( N1: Noticia { id: 1, titulo : 'Arranca el 2022', cuerpo : 'estallo el verano', fecha : localdatetime({year:2022, month:1, day:1, hour:00, minute:00, second:00}) }  );

CREATE( N2: Noticia { id: 2, titulo : 'LLego el otoño', cuerpo : 'falta 982 dias para el verano', fecha : localdatetime({year:2022, month:3, day:21, hour:00, minute:00, second:00}) }  );

CREATE( N3: Noticia { id: 3, titulo : 'Varados a -30°', cuerpo : 'tal como dice el titulo, una familia...', fecha : localdatetime({year:2022, month:7, day:20, hour:10, minute:20, second:12}) }  );

CREATE( N4: Noticia { id: 4, titulo : 'El gesto del Pep Guardiola con Julián Álvarez', cuerpo : 'la araña que pica...', fecha : localdatetime({year:2022, month:7, day:30, hour:23, minute:50, second:00}) }  );
```

3. **Comentario**

```
CREATE( C1: Comentario { id: 1, account: '@lightningNetwork', comentario: 'luz para todos', fecha: localdatetime({year:2022, month:1, day:1, hour:00, minute:01, second:00}) } );

CREATE( C2: Comentario { id: 2, account: '@bot32', comentario: 'sale vivaldi', fecha: localdatetime({year:2022, month:3, day:30, hour:20, minute:52, second:00}) } );

CREATE( C3: Comentario { id: 3, account: '@bot256', comentario: 'anda a encontrarlos', fecha: localdatetime({year:2022, month:7, day:20, hour:23, minute:50, second:00}) } );

CREATE( C4: Comentario { id: 4, account: '@bot2048', comentario: 'preparense', fecha: localdatetime({year:2022, month:7, day:30, hour:23, minute:52, second:00}) } );
```


4. **Relaciones**

```
// Relacion Autor-Noticia

MATCH (a: Autor { account: '@bot32'}), (n1: Noticia { titulo: 'Arranca el 2022'} ) 
CREATE (s)-[R:REDACTO]->(n1) return a,R,n1;

// Relacion Puntuacion Usuario (Autor)-Noticia

MATCH (a: Autor { account: '@bot256'}), (n1: Noticia { titulo: 'Arranca el 2022'} ) 
CREATE (a)-[R:PUNTUA {nota:7.5}]->(n1) return a,R,n1;


// Comentario Usuario (Autor)-Comentario

MATCH (a: Autor { account: '@bot256'}), (c1: Comentario {id:1} ) 
CREATE (a)-[R:COMENTA]->(c1) return a,R,n1;


// Relacion Comentario-Noticia

MATCH (n1:Noticia {id: 1}), (c1: Comentario {id:1} )
CREATE (n1)-[R:COMENTARIOS]->(c1) return n1,R,c1;

```


5. **Grafico del modelo**

```
MATCH (n) RETURN n
```






























