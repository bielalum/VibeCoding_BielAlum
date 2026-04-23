# 02 - Model del joc

## 1. Components principals del joc

El joc està format per diversos components que interactuen entre si per crear l’experiència de joc:

- Sistema de control del jugador (moviment amb teclat)
- Sistema de laberint (estructura de parets i camins)
- Sistema d’enemics amb moviment automàtic
- Sistema de temps (compte enrere)
- Sistema de col·lisions (parets i enemics)
- Sistema d’estats del joc (jugant, victòria, derrota)

Aquests components defineixen l’arquitectura general del joc i permeten separar responsabilitats.

---

## 2. Entitats identificades

Les entitats principals del sistema són:

- **Jugador**
- **Enemic**
- **Laberint**
- **Joc (GameManager)**

Aquestes entitats representen els elements clau del joc i estructuren la seva lògica interna.

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
- alcada
- parets (estructura del mapa)

### Joc (GameManager)
- tempsRestant
- estat (jugant / victoria / derrota)
- jugador
- enemics

---

## 4. Accions, mètodes o funcions principals

### Jugador
- moure(direccio)
- actualitzarPosicio()

### Enemic
- moure()
- canviarDireccio()

### Laberint
- esColisio(posicio)

### Joc (GameManager)
- iniciarJoc()
- actualitzar()
- comprovarVictoria()
- comprovarDerrota()
- reiniciarJugador()

---

## 5. Explicació del diagrama de classes

### Diagrama de classes

```plantuml
@startuml
class Jugador {
  posicioX
  posicioY
  velocitat
  moure()
}

class Enemic {
  posicioX
  posicioY
  direccio
  velocitat
  moure()
}

class Laberint {
  amplada
  alcada
  parets
  esColisio()
}

class Joc {
  tempsRestant
  estat
  iniciarJoc()
  actualitzar()
  comprovarVictoria()
  comprovarDerrota()
}

Joc --> Jugador
Joc --> Enemic
Joc --> Laberint
@enduml
