
# 02 - Model del joc

## 1. Components principals del joc

El joc està format per diversos sistemes que treballen conjuntament per garantir el funcionament global:

- Sistema de control del jugador (moviment amb teclat)
- Sistema de laberint (estructura de parets i passadissos)
- Sistema d’enemics amb moviment automàtic
- Sistema de temporitzador (compte enrere)
- Sistema de col·lisions (parets, enemics i sortida)
- Sistema d’estats del joc (jugant, victòria, derrota)

---

## 2. Entitats identificades

Les entitats principals del sistema són:

- **Jugador**
- **Enemic**
- **Laberint**
- **GameManager**

---

## 3. Atributs clau de cada entitat

### Jugador
- posicioX  
- posicioY  
- velocitat  

### Enemic
- posicioX  
- posicioY  
- direccio  
- velocitat  

### Laberint
- amplada  
- alçada  
- mapa  

### GameManager
- tempsRestant  
- estatJoc  
- jugador  
- enemics  

---

## 4. Accions, mètodes o funcions principals

### Jugador
- moure(direccio)
- actualitzar()

### Enemic
- moure()
- canviarDireccio()

### Laberint
- esColisio(posicio)

### GameManager
- iniciarJoc()
- actualitzar()
- comprovarVictoria()
- comprovarDerrota()
- reiniciarJugador()

---

## 5. Explicació del diagrama de classes

El diagrama de classes representa l’estructura del sistema i com es relacionen les diferents entitats del joc.

La classe **GameManager** és el nucli del sistema, ja que controla el flux del joc i coordina la resta d’elements. El **Jugador** és l’element controlat per l’usuari, mentre que els **Enemics** són elements autònoms que representen el perill dins del laberint. El **Laberint** defineix l’espai del joc i gestiona les col·lisions.

Aquest disseny permet separar responsabilitats i facilita la implementació posterior en Godot.

### Aquest es el codi que he enganxat a PlantUML:

```plantuml
@startuml

class GestorJoc {
  - tempsRestant : float
  - estatJoc : String
  + iniciarJoc()
  + actualitzar()
  + comprovarVictoria()
  + comprovarDerrota()
}

class Jugador {
  - posicio : Vector2
  - velocitat : float
  + moure(direccio)
  + reiniciarPosicio()
}

class Enemic {
  - posicio : Vector2
  - direccio : Vector2
  - velocitat : float
  + moure()
  + canviarDireccio()
}

class Laberint {
  - parets : List
  - posicioSortida : Vector2
  + hiHaColisio(posicio) : boolean
  + esSortida(posicio) : boolean
}

class Temporitzador {
  - tempsRestant : float
  + restarTemps()
  + esTempsAcabat() : boolean
}

GestorJoc --> Jugador
GestorJoc --> Enemic
GestorJoc --> Laberint
GestorJoc --> Temporitzador

Jugador --> Laberint
Enemic --> Laberint

@enduml
```
---


## 6. Explicació del diagrama de comportament

El diagrama de comportament representa el flux principal del joc durant una partida, és a dir, el bucle de joc.

El joc comença amb la inicialització i entra en un bucle mentre l’estat sigui “jugant”. En cada iteració es llegeix el moviment del jugador, s’actualitza la seva posició, es mouen els enemics i es redueix el temps restant.

Després es comproven les condicions del joc:

- si el jugador toca un enemic → es reinicia la seva posició  
- si arriba a la sortida → victòria  
- si el temps arriba a zero → derrota  

### Aquest es el codi que he enganxat a PlantUML:
```plantuml
@startuml

start

:Iniciar joc;
:Inicialitzar jugador, enemics i temporitzador;

while (Joc en marxa?) is (Sí)

  :Llegir entrada del jugador;
  :Moure jugador;

  :Moure enemics;

  :Reduir temps;

  if (Jugador toca enemic?) then (Sí)
    :Reiniciar posició del jugador;
  endif

  if (Jugador arriba a la sortida?) then (Sí)
    :Victòria;
    stop
  endif

  if (Temps <= 0?) then (Sí)
    :Derrota;
    stop
  endif

endwhile

stop

@enduml
```
