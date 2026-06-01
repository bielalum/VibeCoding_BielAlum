# Fase 7: Manual Tècnic del Projecte

Aquest document està pensat per a desenvolupadors o persones que vulguin entendre com està estructurat el videojoc per dins, quina és l'arquitectura de nodes utilitzada a Godot, la lògica dels scripts i com es podria mantenir o ampliar el codi en el futur.

---

## 1. Arquitectura i Organització del Projecte

El projecte s'ha desenvolupat seguint l'arquitectura de programació orientada a components i nodes de **Godot Engine 4**. El joc està organitzat en una escena principal que engloba les diferents entitats (jugador, mapa, interfície i col·leccionables).

### Fitxers principals i responsabilitats

A la taula següent es detallen els fitxers de codi font més importants del projecte i la seva funció dins de la lògica del motor:

| Fitxer de Codi | Node Associat | Tipus de Node Base | Responsabilitat / Funció Principal                                                                                    |
| :------------- | :------------ | :----------------- | :-------------------------------------------------------------------------------------------------------------------- |
| `laberint.gd`  | `Laberint`    | `Node2D`           | Script principal que controla l'estat del joc (pausa, victòria, derrota) i el temporitzador visual (HUD).             |
| `player.gd`    | `Player`      | `CharacterBody2D`  | Gestiona la física del personatge: moviment horitzontal, gravetat, salts, detecció de terra i activació d'animacions. |
| `moneda.gd`    | `Moneda`      | `Area2D`           | Detecta quan el jugador passa per sobre del col·leccionable, avisa la consola i s'allibera de la memòria.             |
| `meta.gd`      | `Meta`        | `Area2D`           | Comprova mitjançant un sistema de grups si queden monedes al mapa per activar o denegar la pantalla de victòria.      |

![Estructura arxius](https://raw.githubusercontent.com/bielalum/VibeCoding_BielAlum/main/imatges/arxius.png)
---

## 2. Funcionament del Codi i Connexions

Les diferents parts del programa es comuniquen combinant referències directes a l'arbre de nodes (`@onready`) i el sistema de senyals asíncrons (*Signals*) clàssic de Godot.

### 1. Sistema d'Estats i Temporitzador (`laberint.gd`)

El script central s'encarrega d'actualitzar la interfície d'usuari a cada fotograma gràcies a la funció `_process(_delta)`. Obté els segons restants del node `Timer` del motor amb la propietat `.time_left` i els injecta com a text a la pantalla. Si el valor arriba a zero, blinda el joc executant una pausa total:

* `get_tree().paused = true` (atura el moviment de la resta de nodes).
* `pantalla_derrota.visible = true` (fa aparèixer el CanvasLayer visual).

---

### 2. Física i Animacions del Personatge (`player.gd`)

S'utilitza `_physics_process(delta)` per garantir un moviment regular a 60 FPS sense dependre de la potència del processador. La mecànica d'ajupir-se s'executa tallant la velocitat en l'eix X (`velocity.x = 0`) i forçant la reproducció de l'animació `"ajupir-se"` mitjançant el node `AnimatedSprite2D`, la qual cosa impedeix caminar mentre es manté premuda la fletxa avall.

---

### 3. Connexió Segura de la Victòria (`meta.gd`)

En lloc de dependre de variables globals o de buscar cadenes de text que poden fallar, la meta utilitza el motor de grups de Godot. Quan es llança el senyal `_on_body_entered`, s'executa la línia:

```gdscript
var monedas_restantes = get_tree().get_nodes_in_group("monedas")
```

Això demana al motor una llista en temps real de totes les monedes que queden vives a la memòria. Si la mida de la llista (`.size()`) és zero, es crida de forma ascendent a la funció de guanyar del pare (`get_parent().ganar_partida()`).

---

## 3. Decisions Tècniques Importants

### Ús de CanvasLayer independent

Les pantalles de Victòria, Derrota i el text del Temps estan col·locats dins d'un node **CanvasLayer**. Això garanteix que la interfície s'organitzi en una capa de renderitzat superior i es quedi fixa a la pantalla de la finestra sense importar com es mogui la càmera darrere del jugador pel laberint.

### Mode de Procés dels Botons en Always

Com que les pantalles finals utilitzen la funció de pausa del motor (`paused = true`), es va haver de canviar explícitament el mode de processat del node **TextureButton** de *Inherit* a *Always*. D'aquesta manera, el botó segueix escoltant els clics de l'usuari encara que la física general del videojoc estigui completament congelada.

---

## 4. Ampliació i Manteniment Futur

El projecte s'ha dissenyat de manera modular perquè es pugui ampliar fàcilment sense haver de reescriure l'estructura central del codi:

### Afegir nous nivells

Com que la meta fa servir la funció `get_tree().reload_current_scene()` per reiniciar, es podria canviar fàcilment per `get_tree().change_scene_to_file("res://Nivell2.tscn")` per carregar un mapa completament nou un cop recollides les monedes.

### Implementació d'enemics

Per afegir enemics, es podria crear una nova escena basada en un `Area2D` amb un script que detectés el `Player`. En lloc de fer un `queue_free()`, es podria restar temps al temporitzador del laberint com a penalització, convertint el joc en un *speedrun amb pressió constant*.

### Escalat de col·leccionables

Gràcies al sistema de **Grups** implementat, afegir més monedes no requereix modificar el codi. Només cal col·locar-les al mapa des de l'editor de Godot i assignar-les al grup `monedas`.

---

## 5. Conclusions

L'arquitectura del projecte permet una separació clara entre lògica del jugador, sistema de joc i interfície. Això facilita el manteniment, la depuració i l'ampliació futura del videojoc.

El sistema basat en nodes i grups de Godot ha demostrat ser robust i escalable, permetent corregir errors inicials i afegir funcionalitats noves sense afectar l'estructura general del projecte.
