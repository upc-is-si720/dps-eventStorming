# EventStorming

## ¿Qué es EventStorming?

`EventStorming` es una actividad de baja tecnología para que un grupo de personas realice una lluvia de ideas y modele rápidamente un proceso empresarial. En cierto sentido, `EventStorming` es una herramienta táctica para compartir el conocimiento del dominio empresarial.

Una sesión de `EventStorming` tiene un _scope_: el `business process` que el grupo está interesado en explorar. Los participantes exploran el proceso como una serie de `domain events`, representados por notas adhesivas, a lo largo de un Timelines. Paso a paso, el modelo se mejora con conceptos adicionales (actors, commands, external systems y otros) hasta que todos sus elementos cuentan la historia de cómo funciona el proceso de negocio.

## The EventStorming Process

Un _EventStorming workshop_ se lleva a cabo generalmente en 10 pasos. Durante cada paso, el modelo se enriquece con información y conceptos adicionales.

### Paso 1: Unstructured Exploration

EventStorming comienza con una lluvia de ideas sobre los `domain events` relacionados con el _business domain_ que se está explorando. Un ***domain events*** es algo interesante que ha sucedido en el negocio. Es importante formular los `domain events` en tiempo pasado; describen cosas que ya sucedieron.

![Unstructured Exploration](/assets/images/lddd_1202.png) 

Durante este paso, todos los participantes toman un montón de notas adhesivas de color naranja, escriben los `domain events` que se les ocurren y los pegan en la superficie de modelado.

En esta etapa inicial, no hay necesidad de preocuparse por ordenar los events, o incluso por la redundancia. Este paso consiste en hacer una lluvia de ideas sobre las posibles cosas que pueden suceder en el _business domain_.

El grupo debe seguir generando `domain events` hasta que la tasa de adición de nuevos disminuya significativamente.

### Paso 2: Timelines (Línea de tiempo)

A continuación, los participantes revisan los **domain events** generados y los organizan en el orden en que ocurren en el _business domain_.

Los events deben comenzar con el "happy path scenario": el flujo que describe un escenario empresarial exitoso.

Una vez que se ha realizado la "happy path", se pueden agregar escenarios alternativos, por ejemplo, rutas en las que se encuentran errores o se toman decisiones empresariales diferentes. La ramificación del flujo se puede expresar como dos flujos que provienen del evento anterior o con flechas dibujadas en la superficie de modelado, como se muestra a continuación:

![happy path scenario](/assets/images/lddd_1203.png) 

Este paso también es el momento de corregir eventos incorrectos, eliminar duplicados y, por supuesto, agregar eventos faltantes si es necesario.

### Paso 3: Pain Points (Puntos críticos)

Una vez que haya organizado los `events` en un _timeline_, use esta vista amplia para identificar los puntos del proceso que requieren atención. Estos pueden ser cuellos de botella, pasos manuales que requieren automatización, documentación faltante o conocimiento del dominio faltante.

Es importante hacer explícitas estas ineficiencias para que sea fácil volver a ellas a medida que avanza la sesión de EventStorming o abordarlas después. Los `Pain Points` están marcados con notas adhesivas rosas rotadas (en forma de diamante), como se ilustra a continuación.

![Pain Points](/assets/images/lddd_1204.png) 

Por supuesto, este paso no es la única oportunidad para hacer un seguimiento de los `pain points`. Como facilitador, tenga en cuenta los comentarios de los participantes durante todo el proceso. Cuando surja un problema o una inquietud, documéntelo como un `pain points`.

### Paso 4: Pivotal Events (Eventos cruciales)

Una vez que tenga un `timeline` de `events` ampliada con `pain points`, busque eventos comerciales significativos que indiquen un cambio en el contexto o la fase. Estos se denominan `pivotal events` y están marcados con una barra vertical que divide los eventos anteriores y posteriores al `pivotal event`.

Por ejemplo, “shopping cart initialized,” “order initialized,” “order shipped,” “order delivered,” y “order returned” representan cambios significativos en el proceso de realización de un pedido, como se muestra a continuación:

![Pivotal Events](/assets/images/lddd_1205.png) 

Los `Pivotal Events` son un indicador de posibles **bounded context** delimitados.


### Paso 5: Commands (Comandos)

Mientras que un `domain event` describe algo que ya sucedió, un ___command___ describe qué desencadenó el evento o el flujo de eventos. Los `Commands` describen las operaciones del sistema y, a diferencia de los `domain events`, se formulan en imperativo. Por ejemplo:

- Publish campaign
- Roll back transaction
- Submit order


Los `commands` se escriben en notas adhesivas de color azul claro y se colocan en el espacio de modelado antes de los eventos que pueden producir. Si un `actor` ejecuta un `command` en particular en un rol específico, la información del `actor` se agrega al `command` en una pequeña nota adhesiva amarilla, como se ilustra a continuación. 

![Commands](/assets/images/lddd_1206.png) 

El `actor` representa una personalidad de usuario dentro del dominio empresarial, como cliente, administrador o editor.

Naturalmente, no todos los `commands` tendrán un `actor` asociado. Por lo tanto, agregue la información del `actor` solo donde sea obvio. En el siguiente paso, aumentaremos el modelo con entidades adicionales que pueden activar comandos. 


### Paso 6: Policies (Políticas)

Casi siempre, algunos `commands` se agregan al modelo pero no tienen un `actor` específico asociado con ellos. Durante este paso, busca `automation policies` que puedan ejecutar esos `commands`.

Una ***automation policy*** es un escenario en el que un evento activa la ejecución de un `command`. En otras palabras, un `command` se ejecuta automáticamente cuando ocurre un `domain event` específico.

En la superficie de modelado, las `policies` se representan como notas adhesivas de color púrpura que conectan `events` a `commands`, como se muestra a continuación en la nota adhesiva “Policy”.

![Policies](/assets/images/lddd_1207.png) 

Un `automation policy` que activa el `command` “Ship Order” cuando se observa el evento “Shipment Approved”.


Si el `command` en cuestión debe activarse solo si se cumplen algunos criterios de decisión, puede especificar los criterios de decisión explícitamente en la nota adhesiva de la `policy`. Por ejemplo, si necesita activar el `command` de escalamiento después del evento “complaint received”, pero solo si el reclamo fue recibido de un cliente VIP, puede indicar explícitamente la condición “only for VIP customers” en la nota adhesiva del `policy`.

Si los `events` y los `commands` están muy separados, puede dibujar una flecha en la superficie de modelado para conectarlos.


### Paso 7: Read Models (Modelos de lectura)

Un `read model` es la vista de datos dentro del _domain_ que el `actor` usa para tomar la decisión de ejecutar un `command`. Puede ser una de las pantallas del sistema, un informe, una notificación, etc.

Los `read models` están representados por notas adhesivas verdes con una breve descripción de la fuente de información necesaria para respaldar la decisión del `actor`. Dado que un `command` se ejecuta después de que el `actor` haya visto el `read model`, en la superficie de modelado los `read models` se posicionan antes de los comandos.

![Policies](/assets/images/lddd_1208.png) 

### Paso 8: External Systems (Sistemas externos)

Este paso trata de aumentar el modelo con `external systems`. Un ***external system*** se define como cualquier sistema que no sea parte del _domain_ que se está explorando. Puede ejecutar comandos (entrada) o puede recibir notificaciones sobre eventos (salida).

Los `external systems` están representados por notas adhesivas rosas. En la siguiente figura, el CRM (`external systems`) activa la ejecución del `command` “Ship Order”. Cuando se aprueba el envío (`event`), se comunica al CRM (`external systems`) a través de una `policy`.

![External Systems](/assets/images/lddd_1209.png) 

Al final de este paso, todos los `commands` deben ser ejecutados por `actors`, activados por `policies` o llamados por `external systems`.


### Paso 9: Aggregates (Agregados)

Una vez que todos los `events` y `commands` están representados, los participantes pueden comenzar a pensar en organizar conceptos relacionados en `aggregates`. Un ***Aggregate*** recibe `commands` y produce `events`.

Los `Aggregates` se representan como notas adhesivas amarillas grandes, con `commands` a la izquierda y `events` a la derecha, como se muestra a continuación:

![Aggregates](/assets/images/lddd_1210.png) 


### Paso 10: Bounded Contexts (Contextos delimitados)

El último paso de una sesión de `EventStorming` es buscar `aggregates` que estén relacionados entre sí, ya sea porque representan una funcionalidad estrechamente relacionada o porque están acoplados a través de `policies`. Los grupos de `aggregates` forman candidatos naturales para los límites de los `bounded contexts`, como se muestra a continuación.

![Aggregates](/assets/images/lddd_1211.png) 


## Variantes

Alberto Brandolini, el creador del taller `EventStorming`, define el `EventStorming process` como una _guía, no como reglas fijas_. Usted es libre de experimentar con el proceso para encontrar la “receta” que funcione mejor para usted.

En mi experiencia, cuando introduzco `EventStorming` en una organización, prefiero comenzar explorando el panorama general del `business domain` siguiendo los pasos 1 (chaotic exploration) a 4 (pivotal events). El modelo resultante cubre una amplia gama del `business domain` de la empresa, construye una base sólida para `ubiquitous languages` y describe los posibles límites para los `bounded contexts`.

Después de obtener el panorama general e identificar los diferentes `business processes`, continuamos facilitando una sesión de `EventStorming` dedicada para cada proceso empresarial relevante, esta vez, siguiendo todos los pasos para modelar el proceso completo.

Al final de una sesión completa de `EventStorming`, tendrá un modelo que describe los _events, commands, aggregates, e incluso posibles bounded contexts del business domain_. Sin embargo, todos estos son solo beneficios adicionales. El valor real de una sesión de `EventStorming` es el proceso en sí: el intercambio de conocimientos entre diferentes partes interesadas, la alineación de sus modelos mentales del negocio, el descubrimiento de modelos conflictivos y, por último, pero no por ello menos importante, la formulación del _ubiquitous language_.

El modelo resultante se puede adoptar como base para implementar un ***domain model*** basado en `events`. La decisión de seguir ese camino o no depende de su `business domain`. Si decide implementar el `domain model` basado en `events`, tiene los límites del `bounded context`, los `aggregates` y, por supuesto, el `blueprint` de los `domain events` necesarios.