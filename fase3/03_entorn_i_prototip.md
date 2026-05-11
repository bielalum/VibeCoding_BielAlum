# Fase 3: Entorn i prototip

## 1. IDE utilitzat i configuració bàsica
Per al desenvolupament d'aquest projecte he utilitzat el motor de videojocs **Godot Engine**, concretament la versió **4.6.2**. He escollit aquest entorn per la seva facilitat i potència en el desenvolupament 2D i la seva bona integració amb el llenguatge **GDScript**.

**Configuració realitzada:**
* **Resolució de pantalla:** He ajustat la vista (*viewport*) a **1920x1024 píxels**. Aquesta mida és ideal per a una quadrícula de blocs de 64x64, ja que permet tenir exactament 30 blocs d'amplada i 16 d'alçada sense talls visuals.
* **Sistema de Tiles:** S'ha configurat un `TileSet` amb físiques actives per permetre les col·lisions automàtiques amb les parets.
* **Controls:** S'ha configurat el mapa d'entrades per respondre a les tecles de direcció (fletxes) del teclat.

## 2. Decisions inicials d’implementació
En aquesta fase inicial, s'han pres decisions clau per garantir la jugabilitat:
* **Disseny de passadissos:** S'ha establert una amplada estàndard de **3 blocs** per als passadissos. Això permet que el personatge es mogui amb fluïdesa i deixa espai suficient per afegir enemics o objectes en fases posteriors.
* **Nodes de física:** El jugador s'ha implementat amb un node `CharacterBody2D`. S'ha triat aquest node perquè ofereix un control precís sobre el moviment i la detecció de col·lisions mitjançant codi.
* **Modularitat:** L'ús de `TileMap` permet modificar el nivell de forma ràpida i eficient sense haver de reubicar objectes de col·lisió individualment.

## 3. Captures de pantalla

### Jerarquia de nodes a l'editor
![Jerarquia de nodes](imatges/jerarquia.png)

### Laberint complet dissenyat al TileMap
![Laberint complet](imatges/laberint.png)

### Codi player.gd (moviment i col·lisions)
![Codi del jugador](imatges/codijugador.png)

### Joc en execució amb el personatge a l'interior
![Joc en execució](imatges/joc.png)

## 4. Condicions mínimes i evidències
Actualment, el projecte disposa d'un **prototip funcional** que compleix amb els requisits mínims d'aquesta fase:
* **Entorn:** Existeix un laberint tancat amb una ruta definida i col·lisions actives.
* **Personatge:** El jugador pot controlar el logotip de Godot i moure'l per tot el laberint.
* **Col·lisions:** El sistema detecta correctament les parets, impedint que el personatge surti dels límits establerts o travessi els murs interns.
