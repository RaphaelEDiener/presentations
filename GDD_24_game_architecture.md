# Sind ECS Systeme? 

**Eine Architektonische Analyse von Codestrukturen im Bezug auf Spieleentwicklung**

`QR Code zu Slides`

note:

- Begrüßung
- Link zu Slides: Anfang & Ende

## Abstract

In dem Vortrag gehe ich auf die Grundlegenden unterschiede in verschiedenen Programmierparadigmen 
(Objekt orientiert, Klassen orientiert, Funktional, Data orientiert) ein. 
Als Sprungbrett nehme ich als die Zentrale frage, 
wann wir in der Spieleentwicklung Systeme entwickeln (wie Beschrieben in System Dynamics) wollen 
und was der Effekt auf Flexibilität ist. 
Dafür schauen wir uns die Kopplungsbeziehungen inherent in populären Notationssystemen und Frameworks an. 
(Bsp: Ecs in Unity, Unreal scripting, reines C++, Rust, ...). 
Beispielsweise sind Rust, OCaml und andere funktionale Sprachen gut geeignet für datenorientierte 
und funktionale Programmierung. 
Auf der anderen Seite sind Sprachen auf dem Beam geeignet um Objektorientierte Systeme zu bauen. 
Sprachen wie Zig, C++, Kotlin, ... liegen an einem Mittelpunkt und können mit Frameworks 
oder Eigenaufwand für beides genutzt werden unter Akzeptanz von Overhead. 
Nehmen wir Sprachen wie C, arbeiten wir in so restriktiven Notationssystemen für die Präsentierten Konzepte, 
dass eine Umsetzung praktisch nicht zu empfehlen ist. 
(Fallbeispiel: Errorhandling mit Monads auf dem Stack). 
Dies ist in Sprachen wir Rust und Kotlin der unterstützte und empfohlene Weg. 
Die Antwort ist natürlich nicht, das X besser ist als Y, sondern unter welcher Voraussetzung 
ein Ansatz mehr Sinn macht als ein Anderer. 
Ein stark gekoppeltes Datenmodel in Daten orientierten Architekturen kann wunder für Performance wirken, 
macht aber einen Pivot wären der Entwicklung exponentiell schwerer je näher man am Release ist. 
Ein extrem schwach gekoppeltes Objektorientiertes System wird immer langsamer sein, 
aber brauch weniger explizite Performancepflege um eine akzeptable Grundgeschwindigkeit zu erreichen 
und ist auch noch spät im Entwicklungsprozess drastisch veränderbar. 
Falls noch Zeit in der Präsentation ist, 
will ich auch auf generelle Mindsetshifts hinweisen, 
welche nötig sing, um mit der Architektur arbeiten zu können, 
statt gegen sie anzukämpfen.

---

## *Wer bin ich*

Raphael Diener

- Archibus Solutions Center 
- 5 Jahre Gamedev als Hobby
- Unreal, Unity, Bevy, Pygame/Pyglet, Godot und from-scratch.
- Großer Programmiersprachen Nerd
- gamedevwiki.net

note:



---

### Sind ECS Systeme? - Eine Architektonische Analyse von Codestrukturen im Bezug auf Spieleentwicklung

note:

---

### Sind ***ECS*** ***Systeme***? - Eine ***Architektonische*** Analyse von Codestrukturen im Bezug auf Spieleentwicklung

note:

---

# System

note:

- Systems Thinking definition weil in der mitte.

---

# System

1. A *system* is a whole that consists of two or more *parts*, 
   each of which can affect the *property* or *behaviour* of the whole.
2. None of the *parts* has an independent effect on the whole.
   How each part effects the whole, *depends* on what the other parts are doing.

*- Dr. Russell Ackoff*

note:

- Beispiel: Auto

### Sind ***ECS*** ***Systeme***? - Eine ***Architektonische*** Analyse von Codestrukturen im Bezug auf Spieleentwicklung

note:

---

---

# Architektur

note:

---

# Architektur

Architecure is the stuff that's hard to change.

*- unbekannt*

note:

- Architektur sind die Dinge, welche sich nicht ändern
  - weil sie stuktur sinde
  - weil sie sich nicht ändern lassen
- Zitat von Kent Beck? Dylan Beattie? Martin Fowler?

---

# Architektur

Architects live in the first derivative

*- Gregor Hohpe*

note:

- Architektur beschreibt unsere agilität
- -> entwicklungsgeschwindigkeit

---

![](./tweet_game_dev_chaos.jpeg)

note:

- Möglichkeiten im Entwicklungsprozess werden von Architektur bestimmt

---

### Sind ***ECS*** ***Systeme***? - Eine ***Architektonische*** Analyse von Codestrukturen im Bezug auf Spieleentwicklung

note:

---

# ECS

note:

- ECS ist eine überladene Abkürzung
- Weshalb nach diesen Slides die Abkürzung nicht mehr benutzt wird

---

# ECS

1. Entity Component Sysmtes

note:

- Architektur
- Gliederung Entities, Components, Systems

---

![](./ESC_Architecture.svg)

note:

- Components sind the Grundbausteine
- Entities sind aus diesen zusammengesetzt
- Systeme updaten die Entities


---

# ECS

1. Entity Component Sysmtes
2. Entity Component System

note:

- Entity component system als motor
- Engine ist englisch für motor

---

![](./unity_ecs_thumbnail.jpg)

note:

- Wenn leute ECS und Unity in einem Satz sagen, 
  reden sie meistens die Engine, nicht das Architekturmuster
- In unity besteht diese Engine aus 4 Bestantteilen
- Das Architekturmuster brauch davon nichts.

---

# ECS

1. Entity Component Sysmtes
2. Entity Component System

note:

- Recap

---

### Sind ***ECS*** ***Systeme***? - Eine ***Architektonische*** Analyse von Codestrukturen im Bezug auf Spieleentwicklung

note:

- Hausaufgaben gemacht
- Können Frage beantworten

---

### Sind ***ECS*** ***Systeme***?

| Entity Component Sysmtes | Entity Component System |
|--------------------------|-------------------------|
|                          |                         |

note:

- Können wir mit Entity Component Sysmtes - Systeme bauen?

---

### Sind ***ECS*** ***Systeme***?

| Entity Component Sysmtes | Entity Component System |
|--------------------------|-------------------------|
|          Ja              |                         |

note:

- Ja. Weil der Core Gameplay loop in einem Spiel is meißtens ein System.

---

### Sind ***ECS*** ***Systeme***?

| Entity Component Sysmtes | Entity Component System |
|--------------------------|-------------------------|
|          Ja              |          Nein           |

note:

- ECSystem sind keine systeme. 
  Wie der Motorblock im Auto.
- Talk vorbei joke


---

### ~~Sind ***ECS*** ***Systeme***?~~ - Eine ***Architektonische*** Analyse von Codestrukturen im Bezug auf Spieleentwicklung

note:

- Was sind die Architektonischen eigenschaften von ECS?
- Wollen wir überhaupt systeme programmieren?
- Was für andere Wege gibt es, Systeme in Code zu modelieren?

---

1. Write
2. Agree
3. Read
4. Modify
5. Execute
6. Debug

note:

-> write - how quick to write
-> Agree - ...
-> *...*

- Vor und nachteile müssen quatifizeirbar sein.
- Casey Muratori
- Schnell zu schreiben
- Eindeutig
- schnell zu lesen
- einfach zu verändern
- Schnell auszuführen
- Einfach zu debuggen (doppelt. bereits in 2 & 3)

---

```c
1 + 2
```

note:

- guter code
- idempotent
- klar lesbar
- schnell auszuführen, weil compiler optimierung
- pure/functional - alles konstant

- Coder der so simple ist, ist gut
- inflexible. nur integer, immer der selbe
- erste ableitung = 0

---

```
fn application(func, value) -> func(value)
```

note:

- super flexible
- aber in den meisten language primitives enthalten
- wollen gesundes mittelmaß

---

```c
typedef struct {
    int x;
    int y;
} Enemy;

typedef struct {
    int x;
    int y;
} Player;

Enemy enemies[] = {...};
Player player = {...};

void move_enemies(Enemy* enemies, size_t len) {
    for (size_t i = 0; i < len; i++) {
        enemies[i].x--;
    }
}

void move_player(Player* player) {
    player->x++;
}

void gravity_player(Player* player) {
    player->y -= player->y > 0 ? 1 : 0;
}
void gravity_enemies(Enemy* enemies, size_t len) {
    for (size_t i = 0; i < len; i++) {
        enemies[i].y -= enemies[i].y > 0 ? 1 : 0;
    }
}

```

note:

- ground up
- simpelste modelierung
- viele abstrahierungen möglich
1. Write - yes
2. Agree - yes
3. Read - yes
6. Debug - yes
5. Execute - meh
4. Modify - nope
- ja, code kann so nicht laufen, 
  aber er muss auf slides passen.

---

```c
typedef struct {
    int x;
    int y;
} Enemy;

typedef struct {
    int x;
    int y;
} Player;

DEFINE_DA(Enemy);
EnemyDa enemies = new_da(...);
Player player = {...};

void move(EnemyDa enemies) {
    for (size_t i = 0; i < enemies.count; i++) {
        enemies.ptr[i].x--;
    }
}
void move_player(Player* player) {
    player->x++;
}
void gravity_player(Player* player) {
    player->y -= player->y > 0 ? 1 : 0;
}
void gravity_enemies(EnemyDa enemies) {
    for (size_t i = 0; i < enemies.count; i++) {
        enemies.ptr[i].y -= enemies.ptr[i].y > 0 ? 1 : 0;
    }
}

```

note:

---

```c
typedef struct {
    int x;
    int y;
} Entity;

DEFINE_DA(Entity);
DEFINE_SLICE(Entity);
EntityDa entities = new_da(...);
EntitySlice enemies = new_da(...);
Entity* player = {...};

void move_enemies(EntitySlice enemies) {
    for (size_t i = 0; i < enemies.count; i++) {
        enemies.ptr[i].x--;
    }
}
void move_player(Entity* player) {
    player->x++;
}
void gravity(EntityDa entities) {
    for (size_t i = 0; i < entities.count; i++) {
        entities.ptr[i].y -= entities.ptr[i].y > 0 ? 1 : 0;
    }
}

```

note:

- better generelized
- worse in flexibility
  - players und enemies sind distinct - entwickeln sich unterschiedlich

---

```c
enum EntityType {
  PLAYER,
  ENEMY
};
typedef struct {
    int x;
    int y;
} EnemyData;
typedef struct {
    int x;
    int y;
} PlayerData;
typedef struct {
    EntityType type;
    union {
        EnemyData enemy_data;
        PlayerData player_data;
    }
} Entity;

DEFINE_SLICE(Entitiy);
DEFINE_DA(Entitiy);
EntityDa entities = new_da(...);
EntitySlice enemies = new_da(...);
Entity* player = {...};

void move_enemies(EntitySlice enemies) {
    for (size_t i = 0; i < enemies.count; i++) {
        enemies.ptr[i].x--;
    }
}
void move_player(Entity* player) {
    player->x++;
}
void gravity(EntityDa entities) {
    for (size_t i = 0; i < entities.count; i++) {
        entities.ptr[i].y -= entities.ptr[i].y > 0 ? 1 : 0;
    }
}


```

note:
- entities wie im ECS
- genauso general wie vorher
- umgefähr selbe performance
- player/enemy genauso einfach änderbar wie davor
- wenn spiel so strukturiert 
  -> bereits bessere perfomance als 99% aller "indie" spiele (meiner erfahrung nach)

---

# Class

TODO: picture casey cycle measurement

note:

- klassen als struct mit virtual method table
- signature-polymorphism benötigt deutlich mehr cycles um @ runtime aufgelöst zu werden
  - plus vererbung, welche lookup braucht

---

TODO: image of Memory levels 

note:

- erklähren der mem hirachy
- jeh mehr platz wir einnehmen -> mehr cache misses -> mehr verschwendete cycles.
- performance ist nicht alles, wie sieht coupling aus?

---

# I don't need performance, PC's are fast and my game is small

note:

- BS argument
  - case study: bloons td -> capped at lv 300 weil performance
  - multiplayer: rollback code
  - halbwegs gute physics colisions
  - parickel
  - Kikaninchen app - imput lag -> schwer zu spielen für target audience
- nicht: hab ich performance problem -> wann habe ich performance probleme
- sind lehrer im raum? 
  -> hab einen kurs belegt on 0 sekunden wurden mit performance oder testing verbacht.
  - nicht verwunderlich, dass spiele so niedrige qualität haben, wenn so gelehrt wird.

---

TODO: diagram of game state + functions

note:

- case 1: coupling overload
- bsp: gamestate struct
- jede function mutiert den game-state
- problem: game logic verteilt sich überall hin, weil es keine encapsulation gibt / klare grenzen

---

TODO: mach daraus class

---

TODO: interface mit der god-class diagram

note:

- interfaces als schneller und einfacher weg das problem zu lösen
- bester schritt im refactoring
- an keiner stelle mehr auf Klassen arbeiten, nurnoch auf interface

---

TODO: pull out classes and partially compose game state

note:

- der refactor ist für die logic unsichtbar, weil interfaces
---

TODO: inheritance 

note:

- beobachtung:
  - gute inheritance folgt liskov und ist selten
    - problem: wenn wir liskov folgen 
      -> modular -> gut
      & -> douplication -> bad
  - inheritance ist ein baum
    - problem: nicht alle spiele so modelierbar
  - in diesem stil sind functionen "mutating"
    - schwer object state zu testen oder zu conzeptualisieren
- deshalb composition > inheritance
  - modular und weniger douplication
  - beziehungen modelierbar als gerichteter graph
  - immutabile style -> einfach testbar and verständlich
    - compiler sind schlau -> wenig performance impact

---

# OOP? 

note:

- nicht das kind mit dem badewasser wegschütten
- was ist mit OOP nach Alan Kay?

---

TODO: postulates of small talk

note:
- erster blick = performance nightmare
- zweiter blick, ein 1:1 model um systeme zu bauen

---


note:

- wie sieht ein object in der einfachsten, low level impl aus?

---


























