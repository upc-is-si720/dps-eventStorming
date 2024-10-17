# The Bounded Context Canvas

El **Bounded Context Canvas** es una herramienta colaborativa para diseñar y documentar el diseño de un `Bounded Context`.

Si no está seguro de qué es un `Bounded Context`, puede consultar la [DDD Reference](https://www.domainlanguage.com/ddd/reference/) y [Martin Fowler's article](https://martinfowler.com/bliki/BoundedContext.html).

El Canvas lo guía a través del proceso de diseño de un `Bounded Context` al solicitarle que considere y tome decisiones sobre los elementos clave de su diseño, desde el nombre hasta las responsabilidades, pasando por su interfaz pública y sus dependencias.

![alt text](assets/bounded-context-canvas-v5.jpg "The Bounded Context Canvas V5")

## Resumen

- [How to Use](#how-to-use)
- [Section Definition](#section-definitions)
- [Example](#example)
- [Tools](#tools)
- [Design Tips](#design-tips)
- [Additional Resources](#additional-resources)
- [Translations](#translations)
- [Contributors](#contributors)
- [Contributions and Feedback](#contributions-and-feedback)

## How to Use

>Para comenzar rápidamente con el `Bounded Context Canvas`, complete el `canvas` en el orden en que se presentan en [Section Definitions](#section-definitions)

Comience con el `name` y la `description` del `canvas` para aclarar su razón de ser y las responsabilidades clave en una o dos oraciones. Luego, puede completar las otras secciones del `canvas` en cualquier orden. Puede diseñar de afuera hacia adentro comenzando con el `inbound communication` o de adentro hacia afuera comenzando con los `business rules` y `domain language`.

Es posible que no tenga toda la información que necesita para completar ciertas secciones del `canvas`. En tal caso, deberá usar otras técnicas de modelado para encontrar la información que necesita.

### Alternative Formats

El formato predeterminado del `Bounded Context Canvas` que se muestra arriba no es el único formato, a continuación se muestran otros. No dude en experimentar también con formatos nuevos y novedosos.

- [Use Case Swimlanes](https://medium.com/nick-tune-tech-strategy-blog/bounded-context-canvas-recipe-use-case-swimlanes-11ca647175d3): Este estilo organiza la sección de `communication` en carriles que muestran la secuencia en la que ocurren las interacciones utilizando el formato: *message in* -> *decision(s) made* -> *message(s) out*


## Section Definitions

Aquí hay una breve explicación de cada sección del `canvas`.

### Name

Nombrar es difícil. Escribir el nombre de su `context` y lograr un acuerdo como equipo determinará cómo diseñar el `context`.

### Purpose

Unas pocas oraciones que describen el por qué y el qué del contexto en `business language`. No hay detalles técnicos aquí.

Escribir el `purpose` lo obliga a articular claramente los pensamientos difusos y a garantizar que todos en el equipo estén en la misma página.

Describa el `purpose` desde un `business perspective`; también puede nombrar a los actores clave para quienes el `bounded context` brinda valor.

### Strategic Classification
How important is this context to the success of your organisation?: 

- core domain: a key strategic initiative
- supporting domain: necessary but not a differentiator
- generic: a common capability found in many domains

What role does the context play in your business model:

- revenue generator: people pay directly for this
- engagement creator: users like it but they don't pay for it
- compliance enforcer: protects your business reputation and existence

How evolved is the concept (see [Wardley Maps](https://medium.com/wardleymaps)):

- genesis: new unexplored domain
- custom built: companies are building their own versions
- product: off-the-shelf versions exist with differentiation
- commodity: highly-standardised versions exist

> For detailed descriptions of genesis, custom built, product, and commodity see [Wardley Maps Evolution definitions](https://twitter.com/swardley/status/989211014485901316/photo/1).

For help filling in this section of the canvas, see [Core Domain Charts](https://github.com/ddd-crew/core-domain-charts).

### Domain Roles
How can you characterise the behaviour of this bounded context? Does it receive high volumes of data and crunch them into insights - an analysis context? Or does it enforce a workflow - an execution context? Identifying the different roles a context plays can help to avoid coupling responsibilities.

Check out Alberto Brandolini's [Bounded Context Archetypes](https://medium.com/@cyrillemartraire/collaborative-construction-by-alberto-brandolini-an-archetype-of-bounded-contexts-bea640bbb5b) and Rebecca Wirfs-Brock's [Object Role Stereotypes](http://www.wirfs-brock.com/PDFs/A_Brief-Tour-of-RDD.pdf) for a deeper analysis of this space. The [Model Traits worksheet](resources/model-traits-worksheet.md) contains community-generated examples of roles (model traits was the former name for domain roles).

### Inbound Communication

Inbound communication represents collaborations that are initiated by other collaborators.

#### Messages

Messages are the information that one collaborator sends to another. There are three types of conversation that can occur between bounded contexts. A request to do something (a command), a request for some information (a query), or notification that something has happened (an event).

The word message is used in the general sense and not tied to any implementation. No message bus or asynchronous workflow is obligatory. A command, for example, could simply be posting data from an HTML form as a HTTP POST command.

#### Collaborators

Collaborators are other systems or sub-systems that send messages to this context. They can be other bounded contexts, frontends (web or mobile), or something else.

If the Bounded Context owns the user interface (e.g. [micro-frontend](https://martinfowler.com/articles/micro-frontends.html)) then the collaborator type is direct user interaction.

![Collaborator types](resources/collaborator-types.jpeg)

#### Relationship Type

The relationship type between two bounded contexts indicates how the models and teams influence each other. See [Context Mappping](https://github.com/ddd-crew/context-mapping) to learn about relationship types.

#### Organising Into Swimlanes

Collaborators can be organised into horizontal swim lanes showing the messages that they send.

![Collaborator example](resources/collaborator-example.jpeg)

### Outbound Communication

Outbound communication represents collaborations that are initiated by this context to interact with other collaborators. The same message types and notations apply as inbound communication.

### Ubiquitous Language
What are the key domain terms that exist within this context, and what do they mean?

### Business Decisions
What are the key business rules and policies within this context?

### Assumptions
You will never make design decisions having a full knowledge about everything in your domain. Most design happens based on assumptions and it is highly recommended to make them explicit. This can be done in this section of the Bounded Context Design Canvas.

### Verification Metrics 
Domain Driven Design is about an iterative approach towards modelling and design based on continuous learning. Metrics can help you
gathering valuable input for those learnings (think about build-measure-learn). Think about metrics that you and your team can define in order to gather learnings if the chosen boundaries of your bounded context are a good fit or not. 

You can collect those metrics for instance from:

- Your CI / CD environments
- Tools like JIRA
- From your live systems

### Open Questions
If you have questions that no one in the room can answer while running a workshop you can enter them into this section of the canvas. This way you can make sure that no open questions get lost but you can also get a visual indicator how certain the team is regarding the design of a given bounded context. Many questions are a good indicator towards a high degree of uncertainty.

## Example
Below a filled-in version of the Bounded Context Canvas.
![BCExample](resources/BCCanvasExample.jpg)

## Tools
Here are some tools that can help you to use the Bounded Context Canvas.

### HTML Version
A [HTML version of the canvas](tools/html-version/README.md) you can edit in a browser and version in source control alongside your code. Contributed by [Nelson da Costa](https://github.com/baruica).

### Miro Version
A free [MiroHQ template](https://miro.com/miroverse/category/newly-added/the-bounded-context-canvas) of the Bounded Context Canvas.

The current version of the template on Miroverse is v4 at the moment. In the meantime, you can download a Miro board backup [here from this repository](resources/bounded-context-canvas-v5-miro.rtb)

### draw.io Version
A [draw.io template of the canvas](tools/drawio-svg-version/README.md) containing the Bounded Context Canvas as template.

### Excalidraw Version
A [Excalidraw template of the canvas](tools/excalidraw-version/README.md) containing the Bounded Context Canvas as template.

## Design Tips

By making the important elements of a bounded context's design visible on the canvas, you can more easily challenge and improve the design. Here are some tips help you challenge and improve a design.

> Please feel free to create a Pull Request sharing your tips.

### General Tips

1. Experiment by moving something on the canvas to another context. How is the design affected?

### Interface Design Tips

The public interface of a bounded context is its contract with the rest of the system. Contracts have a big impact on collaborators and are hard to change, so good design is vital. Here are some tips to help you critique the design of a bounded context's interface.

1. Are the names of messages coherent with each other and the description of the context?
2. Is each message type optimal (e.g. should a command be an event)?
3. Is the interface too big (too many unique message types)?
4. Is the context exposing too much of its internals?
5. Do any messages seem like they should belong elsewhere?


## Additional Resources

- [Bounded Context Canvas V3: Simplifications and Additions](https://medium.com/nick-tune-tech-strategy-blog/bounded-context-canvas-v2-simplifications-and-additions-229ed35f825f)

- [Extending the Bounded Context Canvas with BDD Examples](https://xebia.com/blog/extending-the-bounded-context-canvas-with-bdd-examples/)

## Translations

All resources are available [in French](translations/fr/resources) and in [Portuguese](/translations/pt/resources).

## Contributors

Thanks to all [existing and future contributors](https://github.com/ddd-crew/bounded-context-canvas/graphs/contributors) and to the following individuals who have all contributed to the Bounded Context Canvas:

- [Kenny Baas](https://github.com/Baasie)
- [Kim Lindhard](https://github.com/kim-lindhard-dfds)
- [Michael Plöd](https://github.com/mploed)
- [Maxime Sanglan-Charlier](https://twitter.com/__maxs__)

A significant contribution to the Bounded Context Canvas was the inspiration of the [Business Model Canvas](https://www.strategyzer.com/canvas/business-model-canvas).

## Contributions and Feedback

The Bounded Context Canvas is freely available for you to use. In addition, your feedback and ideas are welcome to improve the canvas or to create new versions. 

Feel free to also send us a pull request with your examples or with new translations.

[![CC BY 4.0][cc-by-shield]][cc-by]

This work is licensed under a [Creative Commons Attribution 4.0 International
License][cc-by].

[![CC BY 4.0][cc-by-image]][cc-by]

[cc-by]: http://creativecommons.org/licenses/by/4.0/
[cc-by-image]: https://i.creativecommons.org/l/by/4.0/88x31.png
[cc-by-shield]: https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg
