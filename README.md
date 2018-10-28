Liga de Leyendas
----------------

Se nos pide modelar un pequeño sistema de batallas basado en el popular video juego League of Legends (a.k.a. Lol).
El sistema se basará en batallas de campeones contra oleadas de *minions*. 
No habrá, al menos de momento, batallas entre campeones (conocidas popularmente como batallas en equipo).

Las batallas están basadas en un sistema simple de ataque y defensa. 
Cuando un campeón ataca le produce una daño a la oleada de minions igual a los puntos de ataque que posee el campeón. 
Sin embargo, éste recibe a su vez un daño, producido por los minions que se defienden. El daño es igual a la cantidad de minions que conforman la oleada más un plus que es definido en cada oleada.

Parte 1: 
--------

Como se explicó antes, los campeones poseen puntos de ataque y puntos de vida, que varían de campeón en campeón. 
Cuando un campeón batalla acumula puntos de daño; los puntos de vida representan la cantidad de daño que puede resistir el campeón antes de morir. 
De esta forma, cuando los puntos de daño son iguales a los puntos de vida, al campeón se lo considera muerto. 

Para ayudar a la supervivencia del campeón, existen los bloqueos. 
Un bloqueo es la capacidad de resistir todo el daño que el campeón recibe en una batalla contra una oleada de minions. 
Esto quiere decir que, si un campeón posee un bloqueo y batallo contra una oleada de minions, en esa batalla no recibirá daño alguno.
Cada bloqueo sirve para una sola batalla y luego se pierde.

Los campeones pueden equiparse o desequiparse items. 
Esto tiene dos consecuencias:
1. Los items, al ser equipados o desequipados en el campeón, producen un efecto en el campeón (que puede ser tanto positivo como negativo). 
2. Cada item brinda, al campeón que lo tiene equipado, una cantidad de puntos de ataque y otra de puntos vida extra. 
Por lo tanto, para calcular el ataque o la vida de un campeón, debe considerarse la suma entre los puntos base propios del campeón más los que aportan los items que posee equipados.

Considerar los siguientes items que el campeón podría equiparse:
* **Anillo de Doran:** Aporta 60 puntos de vida y 15 de ataque. 
Al equiparse, el campeón recibe 5 puntos de daño y, al desequiparse, recupera 10 puntos de daño.

* **Tomo Amplificador:** Aporta el 25% de los puntos de daño total recibido por el campeón como puntos de vida y el 5% del daño total como puntos de ataque. 
Al equiparse otorga dos bloqueos al campeón, pero al desequiparse otorga 1 bloqueo y recibe 30 puntos de daño.

* **Sombrero de Rabadon:** Es una variante del Tomo Amplificador. Aporta 5 puntos más de vida que un Tomo Amplificador, y el doble de los puntos de ataque base del campeón (o sea, algo distinto de lo que aporta el Tomo Amplificador). 
Al equiparse, hace lo mismo que un Tomo Amplificador pero el campeón ademas recibe 5 puntos extra de daño. Al desequiparse, no hace nada.


Las oleadas de minions están conformadas por la cantidad de minions que la conforman.
No es necesario considerar al minion como un objeto individual, sólo la oleada, que al defenderse de un ataque provoca un daño en el campeón atacante. 
El daño que producido es igual al numero de minions que conforma la oleada, más un plus que varia de oleada en oleada.

### Tests
Realizar, como mínimo, el siguiente test:

* Crear un campeón con 50 puntos de vida y 15 de ataque. 
* Equiparlo con un anillo de Doran y un Tomo Amplificador. 
* Crear una Oleada de 10 minions **con un plus de 25 puntos de daño**.
* Hacer que el campeón ataque a la oleada de minions tres veces.
* Hacer que se desequipe, primero el Tomo Amplificador, y después el Anillo.
* Probar que el campeón esta muerto tras haberse desequipado ambos ítems.


Parte 2:
--------

En esta segunda parte contemplaremos algunos agregados al dominio.

### Las oleadas reciben daños
En esta segunda etapa las oleadas de minions, al recibir daño, reduzca su cantidad de minions en un número igual al daño recibido.
En caso de llegar a 0 el escuadrón se considera muerto. 
Cuando un campeón ataca a un escuadron muerto no recibe daño de ningún tipo ni dinero.

### Dinero
En esta nueva etapa, cada campeón posee una cantidad de dinero y los items que se puede equipar tienen un precio.
Entonces para que un campeón pueda equiparse un objeto, debe pagar el precio correspondiente.
Agregar a los campeones los métodos `comprar(item)` y `vender(item)`.
Al comprar un item, si tengo el dinero para comprarlo, gasto el dinero y me equipo el item.
Al vender un item, gano la mitad del dinero de su precio y desequipo el item.
Además, al atacar a una oleada de minions, gana una cantidad de dinero igual a la cantidad de minions eliminados de la oleada.

### Actualización de los tests
Tras haber hecho estos cambios el primer test fallara debido a que en cada ataque van muriendo minions. 
Modifique el test para que se vea reflejado el siguiente escenario:

   * Crear un campeón con 50 puntos de vida y 15 de ataque.
   * Hacer que se desequipe el Anillo de Doran.
   * Hacer que se desequipe el Tomo Amplificador.
   * Crear una oleada de 10 minions con un plus de 15 puntos de daño.
   * Hacer que el campeón ataque a la oleada de minions tres veces.
   * Hacer que se desequipe el Anillo de Doran.
   * Hacer que se desequipe el Tomo Amplificador.
   * Hacer que se equipe otro Tomo Amplificador
   * Hacer que se desequipe el otro Tomo Amplificador
   * Probar que el campeón esta muerto tras haberse desequipado.

### Modificaciones a los items euqipables
Además de precio, se pide agregar a los items equipables una habilidad _activable_, esto es, 
una habilidad que se puede activar en cualquier momento, según la siguiente descripción:

* **Anillo de Doran:** Cuesta 300, no posee habilidad activa.

* **Tomo Amplificador:** Cuesta 500 y su habilidad activa es la siguiente consiste en que, cuando el campeón posee menos de 500 de dinero, automáticamente transforma su dinero en 500. Sólo puede ser usada una vez.

* **Sombrero de Rabadon:** Cuesta 100 mas que un Tomo Amplificador.

También se pide agregar un nuevo objeto: 

* **Pocion de Vida:** No aporta puntos de ataque ni vida, su precio es 50. No hace nada al equiparse ni al desequiparse. Al activarse su habilidad activa le descuenta 50 puntos de daño al campeón y se desequipa inmediatamente.

Parte Individal:
----------------

> IMPORTANTE: A continuación se describen tres tareas. Cada integrante del grupo debera elegir una de ellas. Todos deberán continuar trabajando sobre el mismo repositorio, coordinando para que cada un pueda realizar su parte. En el momento de la entrega, obtendrán dos calificaciones, una grupal y la otra individual.
>
> En caso de que existan grupos de menos de 3 integrantes, cada integrante debe elegir sólo una tarea (y quedará una tarea sin resolver).


Campeon:
--------

Agregar los soportes. Un soporte se comporta de manera similar a un campeón pero no puede andar sólo, debe vincularse con un campeón, aunque puede cambiar de vínculo cuando lo desee.
Cada vez que ataca, reduce en 10 puntos el daño total que posee el campeón. 
Un soporte no tiene items propios y en cambio comparte el inventario con el campeón al que se presta como soporte. 
Sin embargo no comparten el monto de dinero que poseen, por lo que para poder comprar un objeto, cada utiliza su propio para hacerlo. 

> TIP: Considere usar el metodo inventario(), en vez de usar el atributo inventario en cada lugar que se use en la clase Campeon.

Crear el siguiente test:
* Crear a Draven, un campeón con 150 puntos de vida y 25 de ataque y 1000 de dinero.
* Crear a Darius, un campeón con 150 puntos de vida y 25 de ataque y 1000 de dinero.
* Crear a Janna, una soporte con 150 puntos de vida y 25 de ataque y 100 de dinero.
* Crear un ejercito de minions con 100 integrantes y 0 de plus de daño.
* Que Janna vincule a Draven para ser su soporte.
* Que el Draven ataque al ejercito de Minions.
* Que el Janna ataque al ejercito de Minions.
* Que Janna vincule a Darius para ser su soporte.
* Que el Darius ataque al ejercito de Minions.
* Que el Janna ataque al ejercito de Minions.
* Que Darius compre un Tomo Amplificador.
* Que Janna compre una pocion de vida.
* Comprobar que la oleada de minions esta muerta.
* Comprobar que el daño recibido por Draven es de 90, ya que Janna le reducio en 10 el daño total recibido.
* Comprobar que el daño recibido por Darius es de 40, ya que Janna le reducio en 10 el daño total recibido.
* Comprobar que Darius tiene 525 de dinero, por haber comprado el Tomo Amplificador.
* Comprobar que Janna tiene 100 de dinero, por haber comprado una pocion de vida.
* Comprobar que Janna tiene una pocion de vida en su inventario.
* Comprobar que Janna tiene un Tomo Amplificador en su inventario.

Objeto:
------

Crear el objeto Baston del Vacio.
A este objeto se le puede agregar objetos como materiales del baston en cualquier momento. 
* Su precio es 0
* Aporta la mitad de puntos de vida por elemento que tenga como materiales
* Suma la totalidad de puntos en ataque
* No tiene efecto al equiparse ni al desequiparse.
* Su habilidad activable es igual a las habilidades activables de todos sus materiales.

Crear el siguiente test:

* Crear un campeón con 50 puntos de vida y 15 de ataque.
* Equipar al campeón con dos anillos de doran distintos.
* Crear un Baston del Vacio y agregar como materiales una pocion de vida y un Sombrero de Rabadon.
* Equipar al campeón con el Baston del Vacio.
* Activar la habilidad del Baston del vacio.
* Comprobar que el campeon tiene 0 de daño recibido, producto de haberse recuperado los 10 puntos de daño provocados por los anillos,
  gracias a la pocion de vida dentro del Baston del Vacio.
* Comprobar que el campeon tiene 500 de dinero, gracias al Sombrero de Rabadon dentro del Baston del Vacio.

Minions:
--------

Crear la clase Ejercito de minions, que tiene un comportamiento similar a una Oleada, pero que esta compuesta por muchas oleadas de Minions.
Un ejercito de Minions esta muerto cuando todas sus oleadas estan muertas.
Cuando un ejercito de Minions recibe daño, todas sus oleadas reciben daño, mismo que cuando una oleada de minions provoca daño, todas las oleadas le provocaran daño al campeon.

Crear el siguiente test:

* Crear un campeón con 50 puntos de vida y 20 de ataque.
* Crear una oleada de Minions con 20 integrantes y un plus de daño de 5.
* Crear otra oleada de Minions con 10 integrantes y un plus de daño de 15.
* Crear un ejercito de Minions que contenga a las dos oleadas anteriormente creadas.
* Que el campeon ataque al ejercito de Minions.
* Comprobar que tanto el campeon como el Ejercito de Minions estan muertos.
