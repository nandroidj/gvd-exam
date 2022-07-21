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

+ *Consideraciones para las consultas*: 

    * el usuario contenga el campo teléfono

    * un usuario se llame Miguel


```
CREATE( A1: Autor {name: 'Nikola Tesla', username: 'Master of Lightning', account: '@lightningNetwork',  phone: '+33 1234 5678' })
CREATE( A2: Autor {name: 'bot32', username: 'bot32', account: '@bot32',  phone: '+33 1234 5678' })
CREATE( A3: Autor {name: 'bot256', username: 'bot256', account: '@bot256',  phone: '+33 1234 5678' })
CREATE( A4: Autor {name: 'bot2048', username: 'bot2048', account: 'bot2048',  phone: '+33 1234 5678' })

CREATE( A4: Autor {name: 'Miguel Del Monte', username: 'miguele', account: '@miguele',  phone: '+54 1234 5678' })

CREATE( A5: Autor {name: 'Laro', username: 'laro91k', account: '@laro91k',  phone: '+54 1234 5678' })

CREATE CONSTRAINT unique1 FOR (p:Autor) REQUIRE p.account IS UNIQUE;
CREATE CONSTRAINT unique2 FOR (p:Autor) REQUIRE p.username IS UNIQUE;
```


2. **Noticia**

+ *Consideraciones para las consultas*: 
    
    * el titulo contenga 'o'

    * se publique en marzo o abril

    * se publique en 2019 o 2020


```
CREATE( N1: Noticia { id: 1, titulo : 'Arranca el 2022', cuerpo : 'estallo el verano', fecha: localdatetime({year:2022, month:1, day:1, hour:00, minute:00, second:00}) }  );

CREATE( N2: Noticia { id: 2, titulo : 'LLego el otoño', cuerpo : 'falta 982 dias para el verano', fecha: localdatetime({year:2022, month:3, day:21, hour:00, minute:00, second:00}) }  );

CREATE( N3: Noticia { id: 3, titulo : 'Varados a -30°', cuerpo : 'tal como dice el titulo, una familia...', fecha: localdatetime({year:2022, month:7, day:20, hour:10, minute:20, second:12}) }  );

CREATE( N4: Noticia { id: 4, titulo : 'El gesto de Pep Guardiola con Julián Álvarez', cuerpo : 'la araña que pica...', fecha: localdatetime({year:2022, month:7, day:30, hour:23, minute:50, second:00}) }  );

CREATE( N5: Noticia { id: 5, titulo : 'Varados a -30°', cuerpo : 'tal como dice el titulo, una familia...', fecha: localdatetime({year:2019, month:7, day:20, hour:10, minute:20, second:12}) }  );

CREATE( N6: Noticia { id: 6, titulo : 'El gesto de Pep Guardiola con Julián Álvarez', cuerpo : 'la araña que pica...', fecha: localdatetime({year:2020, month:7, day:30, hour:23, minute:50, second:00}) }  );

CREATE( N7: Noticia { id: 7, titulo : 'Dolar a mas de 300 pesos', cuerpo : 'estamos todos locos', fecha: localdatetime({year:2020, month:7, day:30, hour:23, minute:50, second:00}) }  );

CREATE( N8: Noticia { id: 8, titulo : 'Julian la rompio vs america', cuerpo : 'memo ochoa quien te conoce papa?', fecha: localdatetime({year:2020, month:10, day:30, hour:23, minute:50, second:00}) }  );

CREATE( N8: Noticia { id: 9, titulo : 'gvd0', cuerpo : 'gvd0', fecha: localdatetime({year:2018, month:1, day:30, hour:23, minute:50, second:00}) }  );

CREATE( N9: Noticia { id: 10, titulo : 'gvd1', cuerpo : 'gvd1', fecha: localdatetime({year:2018, month:4, day:30, hour:23, minute:50, second:00}) }  );

CREATE( N10: Noticia { id: 11, titulo : 'gvd2', cuerpo : 'gvd2', fecha: localdatetime({year:2018, month:8, day:30, hour:23, minute:50, second:00}) }  );
```

3. **Comentario**

```
CREATE( C1: Comentario { id: 1, account: '@lightningNetwork', comentario: 'luz para todos', fecha: localdatetime({year:2022, month:1, day:1, hour:00, minute:01, second:00}) } );

CREATE( C2: Comentario { id: 2, account: '@bot32', comentario: 'sale vivaldi', fecha: localdatetime({year:2022, month:3, day:30, hour:20, minute:52, second:00}) } );

CREATE( C3: Comentario { id: 3, account: '@bot256', comentario: 'anda a encontrarlos', fecha: localdatetime({year:2022, month:7, day:20, hour:23, minute:50, second:00}) } );

CREATE( C4: Comentario { id: 4, account: '@bot2048', comentario: 'preparense', fecha: localdatetime({year:2022, month:7, day:30, hour:23, minute:52, second:00}) } );
```


4. **Relacion Autor-Noticia**

```
MATCH (a2: Autor { account: '@bot32'}), (n1: Noticia { titulo: 'Arranca el 2022'} ) 
CREATE (a2)-[R:REDACTO]->(n1) return a2,R,n1;

MATCH (a: Autor { username: "Laro"}), (n: Noticia { id: 7} ) CREATE (a)-[R:REDACTO]->(n) return a,R,n;

MATCH (a: Autor { username: "Laro"}), (n: Noticia { id: 8} ) CREATE (a)-[R:REDACTO]->(n) return a,R,n;

```

5. **Relacion Puntuacion Usuario (Autor)-Noticia**

```
MATCH (a: Autor { account: '@bot256'}), (n1: Noticia { titulo: 'Arranca el 2022'} ) 
CREATE (a)-[R:PUNTUA {nota:7.5}]->(n1) return a,R,n1;

MATCH (a: Autor { account: '@bot32'}), (n1: Noticia { id: 2} ) 
CREATE (a)-[R:PUNTUA {nota:4}]->(n1) return a,R,n1;

MATCH (a: Autor { account: '@miguele'}), (n1: Noticia { id: 3} ) 
CREATE (a)-[R:PUNTUA {nota:4}]->(n1) return a,R,n1;

MATCH (a: Autor { account: '@laro91k'}), (n1: Noticia { id: 9} ) 
CREATE (a)-[R:PUNTUA {nota:4}]->(n1) return a,R,n1;

MATCH (a: Autor { account: '@laro91k'}), (n1: Noticia { id: 10} ) 
CREATE (a)-[R:PUNTUA {nota:4}]->(n1) return a,R,n1;

MATCH (a: Autor { account: '@laro91k'}), (n1: Noticia { id: 11} ) 
CREATE (a)-[R:PUNTUA {nota:4}]->(n1) return a,R,n1;
```

6. **Comentario Usuario (Autor)-Comentario**

```
MATCH (a: Autor { account: '@bot256'}), (c1: Comentario {id:1} ) 
CREATE (a)-[R:COMENTA]->(c1) return a,R,n1;


```

7. **Relacion Comentario-Noticia**

```
MATCH (n1:Noticia {id: 1}), (c1: Comentario {id:1} )
CREATE (n1)-[R:COMENTARIOS]->(c1) return n1,R,c1;


```


8. **Grafico del modelo**

```
MATCH (n) RETURN n
```

![modelo](https://github.com/nandroidj/gvd-exam/blob/main/resources/graph.svg)

## 2 - Resolver las siguientes consultas.

Colocar printscreen de cada una de ellas + resultado de la misma:


+ **Noticias**

1. Devolver las noticias cuyo título termine en “o”.
 
```
MATCH (N:Noticia) WHERE N.titulo =~".*o" RETURN N

╒══════════════════════════════════════════════════════════════════════╕
│"N"                                                                   │
╞══════════════════════════════════════════════════════════════════════╡
│{"fecha":"2022-03-21T00:00:00","titulo":"LLego el oto√±o","id":2,"cuer│
│po":"falta 982 dias para el verano"}                                  │
└──────────────────────────────────────────────────────────────────────┘
```

2. Devolver las noticias publicadas en marzo o abril.

```
MATCH (N:Noticia) WITH [item in split(N.fecha, "/") | toInteger(item)] 
AS dateComponents, N as Nb WHERE dateComponents[1]=3 OR dateComponents[1]=4
RETURN Nb

╒══════════════════════════════════════════════════════════════════════╕
│"Nb"                                                                   │
╞══════════════════════════════════════════════════════════════════════╡
│{"fecha":"2022-03-21T00:00:00","titulo":"LLego el oto√±o","id":2,"cuer│
│po":"falta 982 dias para el verano"}                                  │
└──────────────────────────────────────────────────────────────────────┘
```


3. Devolver las noticias publicadas entre los años 2019 y 2020.

```
MATCH (N:Noticia) WITH [item in split(N.fecha, "/") | toInteger(item)] 
AS dateComponents, N as Nb WHERE dateComponents[2]=2020 OR dateComponents[2]=2019
RETURN Nb

╒══════════════════════════════════════════════════════════════════════╕
│"Nb"                                                                  │
╞══════════════════════════════════════════════════════════════════════╡
│{"fecha":"2019-07-20T10:20:12","titulo":"Varados a -30¬∞","id":3,"cuer│
│po":"tal como dice el titulo, una familia..."}                        │
├──────────────────────────────────────────────────────────────────────┤
│{"fecha":"2020-07-30T23:50:00","titulo":"El gesto de Pep Guardiola con│
│ Juli√°n √Ålvarez","id":4,"cuerpo":"la ara√±a que pica..."}           │
└──────────────────────────────────────────────────────────────────────┘
```

+ **Usuarios**

4. Devolver los usuarios en los que exista el campo “teléfono”.

```
MATCH (a:Autor) WHERE a.phone <> 0 RETURN a

╒══════════════════════════════════════════════════════════════════════╕
│"a"                                                                   │
╞══════════════════════════════════════════════════════════════════════╡
│{"phone":"+33 1234 5678","name":"Nikola Tesla","account":"@lightningNe│
│twork","username":"Master of Lightning"}                              │
├──────────────────────────────────────────────────────────────────────┤
│{"phone":"+33 1234 5678","name":"bot32","account":"@bot32","username":│
│"bot32"}                                                              │
├──────────────────────────────────────────────────────────────────────┤
│{"phone":"+33 1234 5678","name":"bot256","account":"@bot256","username│
│":"bot256"}                                                           │
├──────────────────────────────────────────────────────────────────────┤
│{"phone":"+33 1234 5678","name":"bot2048","account":"bot2048","usernam│
│e":"bot2048"}                                                         │
└──────────────────────────────────────────────────────────────────────┘ 
```

5. Devolver los usuarios que, o bien tengan número de teléfono o bien,se llamen Miguel.

```
MATCH (a:Autor) WHERE a.name Contains "Miguel" RETURN a

╒══════════════════════════════════════════════════════════════════════╕
│"a"                                                                   │
╞══════════════════════════════════════════════════════════════════════╡
│{"phone":"+54 1234 5678","name":"Miguel Del Monte","account":"@miguele│
│","username":"miguele"}                                               │
└──────────────────────────────────────────────────────────────────────┘


MATCH (a:Autor) WHERE a.phone <> 0 OR a.name Contains "Miguel" RETURN a

╒══════════════════════════════════════════════════════════════════════╕
│"a"                                                                   │
╞══════════════════════════════════════════════════════════════════════╡
│{"phone":"+33 1234 5678","name":"Nikola Tesla","account":"@lightningNe│
│twork","username":"Master of Lightning"}                              │
├──────────────────────────────────────────────────────────────────────┤
│{"phone":"+33 1234 5678","name":"bot32","account":"@bot32","username":│
│"bot32"}                                                              │
├──────────────────────────────────────────────────────────────────────┤
│{"phone":"+33 1234 5678","name":"bot256","account":"@bot256","username│
│":"bot256"}                                                           │
├──────────────────────────────────────────────────────────────────────┤
│{"phone":"+33 1234 5678","name":"bot2048","account":"bot2048","usernam│
│e":"bot2048"}                                                         │
├──────────────────────────────────────────────────────────────────────┤
│{"phone":"+54 1234 5678","name":"Miguel Del Monte","account":"@miguele│
│","username":"miguele"}                                               │
└──────────────────────────────────────────────────────────────────────┘ 
```


+ **Relaciones**

6. Devolver los datos de todas las relaciones “PUNTUA” con puntuación igual a 4.

```
MATCH p=()-[r:PUNTUA]->()  WHERE r.nota=4 RETURN p LIMIT 10

╒══════════════════════════════════════════════════════════════════════╕
│"p"                                                                   │
╞══════════════════════════════════════════════════════════════════════╡
│[{"phone":"+33 1234 5678","name":"bot32","account":"@bot32","username"│
│:"bot32"},{"nota":4},{"fecha":"2022-03-21T00:00:00","titulo":"LLego el│
│ oto√±o","id":2,"cuerpo":"falta 982 dias para el verano"}]            │
├──────────────────────────────────────────────────────────────────────┤
│[{"phone":"+54 1234 5678","name":"Miguel Del Monte,"account":"@miguel │
│e","username":"miguele"},{"nota":4},{"fecha":"2022-07-20T10:20:12","ti│
│tulo":"Varados a -30¬∞","id":3,"cuerpo":"tal como dice el titulo, una │
│familia..."}]                                                         │
└──────────────────────────────────────────────────────────────────────┘ 

```

7. Devolver los datos de las relaciones “REDACTO” de las noticias publicadas en 2020 cuyo autor se llame “Laro”. 

```
MATCH (a:Autor { name:"Laro" })-[r:REDACTO]->(n:Noticia)
WITH [item in split(n.fecha, "/") | toInteger(item)] AS dateComponents, n as Nb, r as redacto
WHERE dateComponents[2]=2020
return Nb

╒══════════════════════════════════════════════════════════════════════╕
│"Nb"                                                                  │
╞══════════════════════════════════════════════════════════════════════╡
|{"fecha":"2020-07-30T23:50:00","titulo":"Dolar a mas de 300 pesos","id│
│":7,"cuerpo":"estamos todos locos"}                                   │
├──────────────────────────────────────────────────────────────────────┤
│{"fecha":"2020-10-30T23:50:00","titulo":"Julian la rompio vs america",│
│"id":8,"cuerpo":"memo ochoa quien te conoce papa?"}                   │
└──────────────────────────────────────────────────────────────────────┘ 
```

8. Devolver las cuenta de twitter de todos los usuarios que hayan puntuado noticias de 2018.

```
MATCH (a:Autor)-[r:PUNTUA]->(n:Noticia)
WITH [item in split(n.date, "/") | toInteger(item)] AS dateComponents, n as Nb,  a.account as account
WHERE dateComponents[2]=2018
return account

╒══════════════════════════════════════════════════════════════════════╕
│"account"                                                             │
╞══════════════════════════════════════════════════════════════════════╡
│"@laro91k"                                                            │
├──────────────────────────────────────────────────────────────────────┤
│"@laro91k"                                                            │
├──────────────────────────────────────────────────────────────────────┤
│"@laro91k"                                                            │
└──────────────────────────────────────────────────────────────────────┘ 
```



















