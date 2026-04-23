
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

Aquest diagrama mostra l’estructura del sistema i les relacions entre les entitats del joc.

### PlantUML - Diagrama de classes

```plantuml
@startuml
class GameManager {
  - tempsRestant
  - estatJoc
  + iniciarJoc()
  + actualitzar()
  + comprovarVictoria()
  + comprovarDerrota()
  + reiniciarJugador()
}

class Jugador {
  - posicioX
  - posicioY
  - velocitat
  + moure()
  + actualitzar()
}

class Enemic {
  - posicioX
  - posicioY
  - direccio
  - velocitat
  + moure()
  + canviarDireccio()
}

class Laberint {
  - amplada
  - alçada
  - mapa
  + esColisio()
}

GameManager --> Jugador
GameManager --> Enemic
GameManager --> Laberint
@enduml
