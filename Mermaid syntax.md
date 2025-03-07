
# About Mermaid

**Mermaid lets you create diagrams and visualizations using text and code.**

It is a JavaScript based diagramming and charting tool that renders Markdown-inspired text definitions to create and modify diagrams dynamically.

> If you are familiar with Markdown you should have no problem learning Mermaid's Syntax.


Mermaid is a JavaScript based diagramming and charting tool that uses Markdown-inspired text definitions and a renderer to create and modify complex diagrams. The main purpose of Mermaid is to help documentation catch up with development.

---

# indice



---

## Diagram Types

## Flowchart

##### Code:

mermaid

```
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
```

```mermaid
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
```

Ejemplo de cuadros simples. Clickenado el símbolo <> en la esquina superior derecha se ve el código fuente.

---

### Direction flow

flowchart LR indica que el gráfico se representa de izquierda a derecha.
```mermaid
---
title: Gráfico
---
flowchart LR
	primerCuadro["texto dentro del cuadro"]
	segundoCuadro["`item 1
	item2
	item3`"]
	primerCuadro --> segundoCuadro
```


flowchart RL para invertir el flujo.
```mermaid
---
title: Gráfico
---
flowchart RL
	primerCuadro["texto dentro del cuadro"]
	segundoCuadro["`item 1
	item2
	item3`"]
	primerCuadro --> segundoCuadro
```

flowchart TD indica que el gráfico se realizará de arriba hacia abajo.

```mermaid
---
	title:Ejemplo
---
	flowchart TD
		primero["arriba hacia..."]
		segundo["abajo!"]
		primero --> segundo
```


>[!abstract] Possible orientations: 
>TB - Top to bottom
>TD - Top-Down
>BT - Bottom-Top
>RL - Right to left
>LR - Left to right 

---
### Node shapes
Se define la id del primer recuadro, y entre corchetes [] se ingresa lo que va dentro del cuadro.
Finalmente se marcan las relaciones entre los cuadros entre sus IDs.

#### Round edges
```mermaid
flowchart LR
	id1("esto es un nodo con border redondeados")
```

#### Stadium-shape
```mermaid
flowchart LR
	id2([esto está en un nodo con forma de boton html])
```


#### Subrutine
```mermaid
flowchart LR
	id1[["Esto involucra una subrutina"]]
```

#### Cylindrical
```mermaid
flowchart LR
	base1[("♥ base de datos")]
```


#### Circle
```mermaid
flowchart LR
	id1(("circle form shape"))
```

#### Asymmetric
```mermaid
flowchart LR
	cuadro1>"Esto va dentro de una 'bandera'"]
```

#### Rhombus
```mermaid
flowchart TB
 id2{forma romboide}
```

#### Hexagon
```mermaid
flowchart LR
	id1{{nodo de forma hexagonal}}
```

#### Parallelogram 1

```mermaid
flowchart LR
	parallelogram[\"texto unicode dentro del paralelo ♥"\]
```

#### Parallelogram alt

```mermaid
	flowchart LR
		paralleloAlt[/"paralelo alternativo"/]
```

#### Trapezoid
```mermaid
flowchart LR
	trapezoide[/"♠texto dentro del Trapezoide unicode ♦"\]
```

#### Trapezoid alt
```mermaid
	flowchart LR
		trapezoidAlt[\"texto dentro del trapezoide alt"/]
```

#### Double-Circle
```mermaid
	flowchart LR
		doublecircle(("texto unicode dentro del circulo doble"))
```

### Expanded Node shapes
Mermaid now supports a general syntax for defining shape types to accommodate the growing number of shapes. This syntax allows you to assign specific shapes to nodes using a clear and flexible format:

```
A@{ shape: rect }
```

This syntax creates a node A as a rectangle. It renders in the same way as `A["A"]`, or `A`.

#### EXAMPLES Flowchart with New Shapes

```mermaid
	flowchart LR 
		A@{ shape: manual-file, label: "File Handling"}
		
		B@{ shape: stadium, label: "david shape"}

		A --> B
```

### Link beetween nodes

```
Arrow link   A --> B

Open link    A --- B

Text on link A-- Texto! ---B
			 A---|This is texto!|B

Link with arrow head and text A-->|Texto|B

Dotted link  A-.->B;

Dotted with text A-. texto! .-> B

Thick link  A ==> B

Thick with text A == texto! ==> B

Invisible link A ~~~ B

Chaining of links A -- texto --> B -- texto2 --> C

Multiple chaining of links A --> B & C --> D

Multiple links A & B --> C & D

```

#### New arrow types

```
	flowchart LR
		A --o B
```
```mermaid
	flowchart LR
		A["texto nivel1"];
		B["texto nivel2"]
		A --o B
```


```
	flowchart LR
		A --x B
```
```mermaid
	flowchart LR
		A["A not b"];
		B["is not by A"];
		A --x B
```

#### Multidirectional arrows

```mermaid
flowchart LR
    A o--o B
    B <--> C
    C x--x D
```


#### Minimum length of a link

Each node in the flowchart is ultimately assigned to a rank in the rendered graph, i.e. to a vertical or horizontal level (depending on the flowchart orientation), based on the nodes to which it is linked. By default, links can span any number of ranks, but you can ask for any link to be longer than the others by adding extra dashes in the link definition.

In the following example, two extra dashes are added in the link from node _B_ to node _E_, so that it spans two more ranks than regular links:

```mermaid
flowchart TD 
A[Start] --> B{Is it?} 
B -->|Yes| C[OK] 
C --> D[Rethink] 
D --> B 
B ---->|No| E[End]
```

For dotted or thick links, the characters to add are equals signs or dots, as summed up in the following table:

|Length|1|2|3|
|---|---|---|---|
|Normal|`---`|`----`|`-----`|
|Normal with arrow|`-->`|`--->`|`---->`|
|Thick|`===`|`====`|`=====`|
|Thick with arrow|`==>`|`===>`|`====>`|
|Dotted|`-.-`|`-..-`|`-...-`|
|Dotted with arrow|`-.->`|`-..->`|`-...->`|

#### Special characters that break syntax

It is possible to put text within quotes in order to render more troublesome characters. As in the example below:

##### Code:

mermaid

```
flowchart LR
    id1["This is the (text) in the box"]
```

#### Entity codes to escape characters

It is possible to escape characters using the syntax exemplified here.

##### Code:


```
    flowchart LR
        A["A double quote:#quot;"] --> B["A dec char:#9829;"]
```

Numbers given are base 10, so `#` can be encoded as `#35;`. It is also supported to use HTML character names.

Lastly, you can customize with css and classes, the diagram style colors, borders, etc.


----

## Sequence diagram

>[!info] A Sequence diagram is an interaction diagram that shows how processes operate with one another and in what order.

Full example:
```
sequenceDiagram
    participant Alice
    participant Bob
    Alice->>John: Hello John, how are you?
    loop HealthCheck
        John->>John: Fight against hypochondria
    end
    Note right of John: Rational thoughts <br/>prevail!
    John-->>Alice: Great!
    John->>Bob: How about you?
    Bob-->>John: Jolly good!
```

```mermaid
sequenceDiagram
    participant Alice
    participant Bob
    Alice->>John: Hello John, how are you?
    loop HealthCheck
        John->>John: Fight against hypochondria
    end
    Note right of John: Rational thoughts <br/>prevail!
    John-->>Alice: Great!
    John->>Bob: How about you?
    Bob-->>John: Jolly good!
```


---

#### Syntax

 * Participants

The participants can be defined implicitly as in the first example on this page. The participants or actors are rendered in order of appearance in the diagram source text. Sometimes you might want to show the participants in a different order than how they appear in the first message. It is possible to specify the actor's order of appearance by doing the following:

```
sequenceDiagram
    participant Alice
    participant Bob
    Bob->>Alice: Hi Alice
    Alice->>Bob: Hi Bob
```

```mermaid
sequenceDiagram
    participant Alice
    participant Bob
    Bob->>Alice: Hi Alice
    Alice->>Bob: Hi Bob

```

----

#### Actors

If you specifically want to use the actor symbol instead of a rectangle with text you can do so by using actor statements as per below.

```mermaid
sequenceDiagram
actor Ew
actor PFlook
Ew ->>PFlook: "Debemos poner más pppoers!"
PFlook ->>Ew: "Oiga, estoy tratando de comer mi almuerzo"
```



---

#### Aliases

The actor can have a convenient identifier and a descriptive label.

```
sequenceDiagram
    participant A as Alice
    participant J as John
    A->>J: Hello John, how are you?
    J->>A: Great!
```


---

#### Actor Creation and Destruction (v10.3.0+)[​](https://mermaid.js.org/syntax/sequenceDiagram.html#actor-creation-and-destruction-v10-3-0)

It is possible to create and destroy actors by messages. To do so, add a create or destroy directive before the message.

```
create participant B
A --> B: Hello
```

Create directives support actor/participant distinction and aliases. The sender or the recipient of a message can be destroyed but only the recipient can be created.

```
sequenceDiagram
    Alice->>Bob: Hello Bob, how are you ?
    Bob->>Alice: Fine, thank you. And you?
    create participant Carl
    Alice->>Carl: Hi Carl!
    create actor D as Donald
    Carl->>D: Hi!
    destroy Carl
    Alice-xCarl: We are too many
    destroy Bob
    Bob->>Alice: I agree
```


```mermaid
sequenceDiagram
    Alice->>Bob: Hello Bob, how are you ?
    Bob->>Alice: Fine, thank you. And you?
    create participant Carl
    Alice->>Carl: Hi Carl!
    create actor D as Donald
    Carl->>D: Hi!
    destroy Carl
    Alice-xCarl: We are too many
    destroy Bob
    Bob->>Alice: I agree
```

---

#### Grouping / Box.

The actor(s) can be grouped in vertical boxes. You can define a color (if not, it will be transparent) and/or a descriptive label using the following notation:
```
box Aqua Group Description
... actors ...
end
box Group without description
... actors ...
end
box rgb(33,66,99)
... actors ...
end
box rgba(33,66,99,0.5)
... actors ...
end
```

example:

```mermaid
    sequenceDiagram
    box rgb(0, 170, 90) Alice & John
    participant A
    participant J
    end
    box Yellow Another Group
    participant B
    participant C
    end
    A->>J: Hello John, how are you?
    J->>A: Great!
    A->>B: Hello Bob, how is Charley?
    B->>C: Hello Charley, how are you?
```

---

#### Messages.

Messages can be of two displayed either solid or with a dotted line.

```
[Actor][Arrow][Actor]:Message text
```

There are ten types of arrows currently supported:

|Type|Description|
|---|---|
|`->`|Solid line without arrow|
|`-->`|Dotted line without arrow|
|`->>`|Solid line with arrowhead|
|`-->>`|Dotted line with arrowhead|
|`<<->>`|Solid line with bidirectional arrowheads (v11.0.0+)|
|`<<-->>`|Dotted line with bidirectional arrowheads (v11.0.0+)|
|`-x`|Solid line with a cross at the end|
|`--x`|Dotted line with a cross at the end|
|`-)`|Solid line with an open arrow at the end (async)|
|`--)`|Dotted line with a open arrow at the end (async)|

---

#### Activations.

It is possible to activate and deactivate an actor. (de)activation can be dedicated declarations:

```
sequenceDiagram
    Alice->>John: Hello John, how are you?
    activate John
    John-->>Alice: Great!
    deactivate John
```


```mermaid
sequenceDiagram
    Alice->>John: Hello John, how are you?
    activate John
    John-->>Alice: Great!
    deactivate John
```

---

#### Notes.

It is possible to add notes to a sequence diagram. This is done by the notation Note \[ right of | left of | over ] \[Actor]: Text in note content

example
```
sequenceDiagram
    participant John
    Note right of John: Text in note
```

```mermaid
sequenceDiagram
    participant John
    Note right of John: Text in note
```

* Note spanning two participants

```
sequenceDiagram
    Alice->John: Hello John, how are you?
    Note over Alice,John: A typical interaction
```

```mermaid
sequenceDiagram
    Alice->John: Hello John, how are you?
    Note over Alice,John: A typical interaction
```
* Linebreaks can be added to Note and Messages:

```
sequenceDiagram
    Alice->John: Hello John,<br/>how are you?
    Note over Alice,John: A typical interaction<br/>But now in two lines
```

```mermaid
sequenceDiagram
    Alice->John: Hello John,<br/>how are you?
    Note over Alice,John: A typical interaction<br/>But now in two lines
```

* Line breaks in Actor names requires aliases:

```
sequenceDiagram
    participant Alice as Alice<br/>Johnson
    Alice->John: Hello John,<br/>how are you?
    Note over Alice,John: A typical interaction<br/>But now in two lines
```

```mermaid
sequenceDiagram
    participant Alice as Alice<br/>Johnson
    Alice->John: Hello John,<br/>how are you?
    Note over Alice,John: A typical interaction<br/>But now in two lines
```


#### Loops.

It is possible to express loops in a sequence diagram. This is done by the notation

```
sequenceDiagram
    Alice->John: Hello John, how are you?
    loop Every minute
        John-->Alice: Great!
    end
```

```mermaid
sequenceDiagram
    Alice->John: Hello John, how are you?
    loop Every minute
        John-->Alice: Great!
    end
```


#### Alt.

It is possible to express alternative paths in a sequence diagram. This is done by the notation

```
alt Describing text
... statements ...
else
... statements ...
end
```

or if there is sequence that is optional (if without else).

```
opt Describing text
... statements ...
end
```

Example
```mermaid
sequenceDiagram
    Alice->>Bob: Hello Bob, how are you?
    alt is sick
        Bob->>Alice: Not so good :(
    else is well
        Bob->>Alice: Feeling fresh like a daisy
    end
    opt Extra response
        Bob->>Alice: Thanks for asking
    end

```


#### Parallel.

It is possible to show actions that are happening in parallel.

```
sequenceDiagram
    par Alice to Bob
        Alice->>Bob: Hello guys!
    and Alice to John
        Alice->>John: Hello guys!
    end
    Bob-->>Alice: Hi Alice!
    John-->>Alice: Hi Alice!

```

```mermaid
sequenceDiagram
    par Alice to Bob
        Alice->>Bob: Hello guys!
    and Alice to John
        Alice->>John: Hello guys!
    end
    Bob-->>Alice: Hi Alice!
    John-->>Alice: Hi Alice!
```


It is also possible to nest parallel blocks.
```
sequenceDiagram
    par Alice to Bob
        Alice->>Bob: Go help John
    and Alice to John
        Alice->>John: I want this done today
        par John to Charlie
            John->>Charlie: Can we do this today?
        and John to Diana
            John->>Diana: Can you help us today?
        end
    end
```


#### Critical Region

It is possible to show actions that must happen automatically with conditional handling of circumstances.
**It is also possible to have no options at all**

This is done by the notation

```
critical [Action that must be performed]
... statements ...
option [Circumstance A]
... statements ...
option [Circumstance B]
... statements ...
end
```


Example:

```mermaid
sequenceDiagram
    critical Establish a connection to the DB
        Service-->DB: connect
    option Network timeout
        Service-->Service: Log error
    option Credentials rejected
        Service-->Service: Log different error
    end
```



#### Break.

It is possible to indicate a stop of the sequence within the flow (usually used to model exceptions).

This is done by the notation

```
break [something happened]
... statements ...
end
```

Example: 

```
sequenceDiagram
    Consumer-->API: Book something
    API-->BookingService: Start booking process
    break when the booking process fails
        API-->Consumer: show failure
    end
    API-->BillingService: Start billing process
```



#### Background Highlighting.

It is possible to highlight flows by providing colored background rects. This is done by the notation

```
rect COLOR
... content ...
end
```

The colors are defined using rgb and rgba syntax.

```
rect rgb(0, 255, 0)
... content ...
end
```

```
rect rgba(0, 0, 255, .1)
... content ...
end
```

Example:
```mermaid
sequenceDiagram
    participant Alice
    participant John

    rect rgb(191, 223, 255)
    note right of Alice: Alice calls John.
    Alice->>+John: Hello John, how are you?
    rect rgb(200, 150, 255)
    Alice->>+John: John, can you hear me?
    John-->>-Alice: Hi Alice, I can hear you!
    end
    John-->>-Alice: I feel great!
    end
    Alice ->>+ John: Did you want to go to the game tonight?
    John -->>- Alice: Yeah! See you there.


```



#### Actor Menus

Actors can have popup-menus containing individualized links to external pages. For example, if an actor represented a web service, useful links might include a link to the service health dashboard, repo containing the code for the service, or a wiki page describing the service.

This can be configured by adding one or more link lines with the format:

```
link <actor>: <link-label> @ <link-url>
```

Example:

```mermaid
sequenceDiagram
    participant Google
    participant User
    link Google: web@https://www.google.com
    link Google: Wiki@https://wiki.google.com
    link User: Dashboard@https://dashboard.contoso.com/john
    link User: Wiki@https://wiki.contoso.com/john
    Google->>User: Search box
    User-->>Google: Input search term
    Google-)User: Query Results
```

There is an advanced syntax that relies on JSON formatting. If you are comfortable with JSON format, then this exists as well.

This can be configured by adding the links lines with the format:
```
links <actor>: <json-formatted link-name link-url pairs>
```

```mermaid
sequenceDiagram
	participant Google
	participant User
	links Google: {"Web": "https://www.google.com", "Wiki": "https://wiki.google.com"}
```



----

## Gantt diagram

##### Code:

mermaid

```
gantt
dateFormat  YYYY-MM-DD
title Adding GANTT diagram to mermaid
excludes weekdays 2014-01-10

section A section
Completed task            :done,    des1, 2014-01-06,2014-01-08
Active task               :active,  des2, 2014-01-09, 3d
Future task               :         des3, after des2, 5d
Future task2               :         des4, after des3, 5d
```


```mermaid
gantt
dateFormat  YYYY-MM-DD
title Adding GANTT diagram to mermaid
excludes weekdays 2014-01-10

section A section
Completed task            :done,    des1, 2014-01-06,2014-01-08
Active task               :active,  des2, 2014-01-09, 3d
Future task               :         des3, after des2, 5d
Future task2               :         des4, after des3, 5d
```

ejemplo
```mermaid
gantt
dateFormat YYYY-MM-DD
title Llamadas de soporte
excludes weekdays 2025-01-11

section botmaker
migracion iptv             :done, des1, 2025-01-01, 2025-01-25
falta de link              :active, des2, 2025-01-01, 15d
migracion internet         :       des3, after des2, 10d
```

---

## Class diagram.

##### Code:

mermaid

```
classDiagram
Class01 <|-- AveryLongClass : Cool
Class03 *-- Class04
Class05 o-- Class06
Class07 .. Class08
Class09 --> C2 : Where am i?
Class09 --* C3
Class09 --|> Class07
Class07 : equals()
Class07 : Object[] elementData
Class01 : size()
Class01 : int chimp
Class01 : int gorilla
Class08 <--> C2: Cool label
```

```mermaid
classDiagram
Class01 <|-- AveryLongClass : Cool
Class03 *-- Class04
Class05 o-- Class06
Class07 .. Class08
Class09 --> C2 : Where am i?
Class09 --* C3
Class09 --|> Class07
Class07 : equals()
Class07 : Object[] elementData
Class01 : size()
Class01 : int chimp
Class01 : int gorilla
Class08 <--> C2: Cool label
```

---

## Git graph.

##### Code:

commit id:"12345"
commit tag:"algun tag"
branch (nombre de nueva rama)
checkout (nombre de la rama a seguir)
commit type:[HIGHLIGHT / REVERSE / NORMAL]

mermaid

```
    gitGraph
       commit
       commit
       branch develop
       commit
       commit
       commit
       checkout main
       commit
       commit
```

```mermaid
    gitGraph
       commit
       commit
       branch develop
       commit
       commit
       commit
       checkout main
       commit
       commit
```


```mermaid
	gitGraph
			commit "david"
			commit id:"735024"
			branch menuContextual
			commit tag:"giordano"
			commit 
			checkout main
			commit type:HIGHLIGHT 
			commit
			checkout main
			commit
			commit
			
```

















