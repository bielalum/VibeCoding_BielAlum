# 02 - Model del joc

## 1. Components principals del joc

El joc està format per diversos components que treballen conjuntament per gestionar el funcionament global:

- Control del jugador (entrada per teclat i moviment)
- Sistema de laberint (estructura de parets i espais)
- Sistema d’enemics amb moviment automàtic
- Sistema de temps (compte enrere)
- Sistema de col·lisions (parets i enemics)
- Sistema d’estats del joc (jugant, victòria, derrota)

Aquests components permeten dividir el joc en parts més simples i organitzades.

---

## 2. Entitats identificades

Les entitats principals del sistema són:

- **Jugador** → element controlat per l’usuari  
- **Enemic** → obstacles mòbils que poden fer perdre al jugador  
- **Laberint** → espai del joc amb parets i camins  
- **Joc (GameManager)** → controla el flux global del joc  

Aquestes entitats representen els elements clau necessaris per al funcionament del videojoc.

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

Aquest diagrama representa l’estructura del sistema i les relacions entre les diferents entitats del joc.

La classe **Joc (GameManager)** és l’element central que controla el flux de la partida i gestiona la resta d’objectes. Les classes **Jugador** i **Enemic** representen els elements que es mouen dins del laberint, mentre que la classe **Laberint** defineix l’espai i les col·lisions.

Les relacions mostren que el joc conté i coordina la resta d’entitats, cosa que permet una separació clara de responsabilitats i facilita la implementació posterior.

![diagrama-classes](imatges/diagrama_classes.png)

---

## 6. Explicació del diagrama de comportament

### Diagrama d’activitat

Aquest diagrama mostra el flux del joc i el funcionament del bucle principal durant la partida.

El procés comença amb l’inici del joc i entra en un bucle que es repeteix mentre l’estat sigui “jugant”. En cada iteració es llegeix l’entrada del jugador, s’actualitza la seva posició, es mouen els enemics i es redueix el temps restant.

Després es comproven les condicions del joc:
- si el jugador toca un enemic, es reinicia la seva posició  
- si arriba a la sortida, el joc passa a estat de victòria  
- si el temps s’esgota, el joc passa a estat de derrota  

Aquest diagrama reflecteix directament el bucle de joc definit a la fase 1.

![diagrama-comportament](imatges/diagrama_comportament.png)

---
