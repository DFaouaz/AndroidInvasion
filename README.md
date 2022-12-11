# Android Invasion
Este es un proyecto del Master de Desarrollo de Videojuegos de la Universidad Complutense de Madrid (2022-2023).
El juego consiste en prototipar la funcionalidad principal de un FPS y un Third Person y combinarlos.
El objetivo es:
- Al iniciar tienes que llevar al personaje al edificio que se encuentra en medio del desierto
- Una vez dentro empezará el juego principal.
- Hay que sobrevivir el ataque de los androides mientras destruyes los prototipos.
- Cuando destruyas todos los prototipos, pasas el siguiente nivel de dificultad.
- Repite la misma partida incrementando el nivel de dificultad hasta que ya no puedas sobrevivir.

# Controles

- WASD para moverse
- Raton para apuntar
- Click izquierdo para disparar
- Click derecho para cambiar el tipo de projectil
- Tecla G para rellenar toda la municion (projectiles normales y granadas)

# Proceso de produccion

Durante el desarrollo se ha tomado la plantilla inicial y se han ido implementando las funcionalidades
de la siguiente manera:
- Implementacion de los controles que se van a usar en el proyecto.
- Implementacion y conexion de los controles con las mecanicas principales del personaje
    - Movimiento (correr) hacia delante y un lado (con opcion de sprint)
    - Salto con cancelacion de salto en medio del aire
    - Apuntado
    - Disparo de projectiles
    - Cheat code con la tecla G (rellena la municion al maximo)
    - Cambio de projectiles (entre projectil normal y granadas)
- Implementacion del comportamiento de las puertas
    - Se ha hecho que si un cuerpo fisico entra en el volumen de afecto de la puerta, esta se abra. 
    - Siempre que tenga algun cuerpo fisico dentro de dicho volumen, se mantendra abierta incluso dicho cuerpo fisico no es el jugador.
- Implementacion del comportamiento de los projectiles normales
    - Si colisiona con algo que implemente la interfaz de Android, aplica un impacto. 
    - Si es un cuerpo fisico, se da un impulso. 
    - Finalmente, se destruye.
- Implementacion del comportamiendo de los enemigos
    - Si estan muy cerca del jugador, le aplican daño de manera progresiva.
- Implementacion del comportamiento de las granadas
    - Si colisiona con algo que implemente la interfaz de Android, explota (aplicando X numero de impactos). 
    - Si es un cuerpo fisico, se da un impulso.
    - Si no ha explotado previamente, al pasar X tiempo termina haciendolo.
    - Finalmente, se destruye con particulas de explosion.
- Implementacion del comportamiento de los Spawners.
    - Cada X tiempo, spawnea un enemigo.
- Implementacion del comportamiento de los actores que implementan la interfaz Androide
    - Los enemigos restan un punto de vida por cada impacto y si pierden toda la vida, mueren (activando efectos de particulas y ragdoll)
    - Los spawners restan un punto de vida por cada impacto y se destruyen si se le acaban todos los puntos de vida (dejando de spawnear).
    - Los prototipos (objetivos del juego) avisan al GameMode de que han sido golpeados para actualizar el estado de la partida.
- Se ha implementado la gestion del nivel en el GameMode.
    - Cuando el numero de targets restantes llega a 0, se inicializa el nivel de nuevo con un pequeño cambio en la dificultad (los spawners spawnean el doble de rapido respecto al nivel anterior).
    - Si es el primer nivel, lanzamos una cinematica de presentacion.
- Se ha implementado el GameInstance
    - Inicializamos el numero de nivel en el que estamos segun si se carga partida o se inicia una partida nueva
    - Gestionamos el guardado y carga de partida.

Finalmente, se ha implementado la funcionalidad y diseño de la interfaz de usuario:
- Se ha implementado el menu principal
    - El boton de Cargar partida, solo se habilita si existe alguna partida guardada para cargar
    - El boton de Nueva partida, que inicia el juego desde el nivel 0 y carga la escena del desierto.
    - El botno de Salir, que cierra el juego.
- Se ha implementado el HUD del jugador
    - Las barras de vida y stamina se actualizan con un bind de funcion.
    - El numero de targets se actualiza con un bind de funcion
    - El numero de municion se actualiza con un bind de propiedad
    - El numero de granadas se actializa con un bin de propiedad


# Features adicionales

- Se ha implementado la posibilidad de sprint-ar
- Se ha hecho que los projectiles elijan el color de forma aleatoria
- Se ha hecho que las lamparas elijan el color de forma aleatoria
- Implementacion de paquetes de municion
    - Al recoger, te da granadas o projectiles dependiendo de como esten configurados.
    - Los verdes dan projectiles normales
    - Los rojos/naranjas dan granadas.
- Se ha modificado la interfaz para indicar que tipo de projectil esta seleccionado.
    - Se marca en verde el nombre del projectil que se va a disparar.