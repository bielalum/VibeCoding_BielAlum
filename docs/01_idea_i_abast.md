# 01. Idea i abast del projecte

## 1. Títol provisional del joc
Maze Protocol

---

## 2. Tipus de microvideojoc escollit
Será un joc de laberint 2D amb vista superior, on el jugador ha de trobar la sortida evitant els enemics i amb límit de temps.

---

## 3. Objectiu del joc
L’objectiu del jugador és travessar el laberint des del punt inicial fins la sortida abans de que s’esgoti el temps, evitant els enemics que es mouen de paret en paret.

---

## 4. Rol del jugador
El jugador controla un personatge dins d’un laberint 2D amb vista superior. El seu moviment consta de quatre direccions (amunt, avall, esquerra i dreta) que es faran amb les tecles del teclat, tant les fletxes com WASD.

---

## 5. Regles bàsiques
- El jugador es mou lliurement pel laberint  
- No pot travessar parets  
- Hi ha enemics que es mouen de paret en paret  
- Si el jugador toca un enemic torna a la posició inicial  
- El temps disminueix durant tota la partida fins arribar a 0  

---

## 6. Condicions de victòria i derrota
- **Victòria:** arribar a la sortida del laberint abans que s’esgoti el temps  
- **Derrota:** quan el temps arriba a 0 i no s’ha arribat a la sortida  
- Si el jugador toca un enemic, es reinicia la seva posició (torna a la posició d’inici) però el temps continua  

---

## 7. Bucle principal del joc
Durant la partida es repeteix un bucle continu en el qual el joc llegeix el moviment del jugador i actualitza la seva posició dins del laberint. Després, els enemics es mouen automàticament seguint el seu patró. A continuació, es redueix el temps restant. Finalment, es comproven les condicions de victòria (arribar a la sortida) i derrota (temps esgotat). Aquest procés es repeteix fins que es compleix alguna condició de final de partida.

---

## 8. Repte principal i dificultat
El repte principal és gestionar correctament la lògica del moviment dins d’una graella (laberint), assegurant que les col·lisions amb les parets funcionin correctament i que la detecció de contacte amb enemics i la sortida sigui precisa. La dificultat és mitjana-baixa, ja que el joc no inclou mecàniques complexes, però requereix una bona organització de la lògica.

---

## 9. Limitacions explícites
El joc no inclourà mode multijugador, 3D ni funcionalitats avançades. No hi haurà animacions pels personatges ni gràfics avançats. Es prioritzarà el funcionament i la lògica del joc per sobre de l’apartat visual.

---

## 10. Riscos tècnics
- Gestió de col·lisions amb les parets: assegurar que el jugador no pugui travessar murs dins del sistema del laberint  
- Detecció de col·lisió amb enemics: garantir que quan el jugador toca un enemic es detecti correctament i es reiniciï a la posició inicial  
- Detecció de condició de victòria: comprovar correctament quan el jugador arriba a la sortida i finalitzar el joc  

---

## 11. Exploració amb IA (mínim 2 prompts + resposta resumida)

### Prompt 1
“Diguem 5 idees per un videojoc simple 2D. Ha de tenir un bucle de joc clar, i les seves parts ben definides. Aquest és l’enunciat on ho explica tot més clarament: adjunto enunciat de l’activitat. Com veus, el més important no és el joc en si, sinó anar avançant correctament amb una bona planificació i organització.”

**Resposta de la IA resumida:**  
La IA va proposar diferents tipus de jocs com: joc de decisions, supervivència bàsica, laberints, quiz, etc. Explicant la seva dificultat, possibles riscos i temps necessari.

**Decisió:**  
Finalment he escollit el joc del laberint, perquè el considero una opció viable i simple per fer en el temps disponible i sense experiència en la creació de videojocs.

---

### Prompt 2
“Ara que he decidit quin joc fer ajuda’m a definir el bucle d’aquest, els estats del sistema i possibles problemes tècnics que pugui tenir abans de programar-lo. M’agradaria afegir enemics que reboten de paret en paret, col·lisions en les parets, i un comptador que quan arriba a zero s’acaba la partida.”

**Resposta de la IA resumida:**  
La IA va ajudar a estructurar el bucle del joc en fases (moviment del jugador, moviment dels enemics, actualització del temps i comprovació d’estats de victòria i derrota). També va identificar possibles problemes com la gestió de col·lisions i la sincronització dels estats.

**Decisió presa:**  
He utilitzat aquesta estructura per definir el disseny del joc abans de començar a programar-lo.

---

## 12. Proposta final escollida
Es manté la idea del joc del laberint 2D amb enemics, temporitzador i moviment en graella.

En quant a l’IDE, inicialment volia fer servir JavaFX, que és el que em recomanava la IA perquè li havia explicat que sé programar en Java, però per tal de tenir un entorn millor visualment vaig decidir quedar-me amb Godot.

També vaig considerar Roblox Studio, però no vaig voler complicar-me al no haver-lo fet servir mai.

---

## 13. Justificació de viabilitat
Penso que el projecte és viable dins del temps establert i potser amb algunes hores extra a casa, ja que utilitza mecàniques senzilles. El joc es basa en un sistema de graella, evitant càlculs complexos o IA avançada.

Pel que fa a Godot, aquest és un motor gràfic intuïtiu semblant a Unity, i ideal per a jocs 2D, el qual utilitza GDScript, un llenguatge similar a Python. Penso que aquesta serà una bona opció perquè és molt conegut i podré trobar molta ajuda i informació a internet fàcilment.

---

## 14. Mini pla de treball
- Definir estructura del joc i laberint  
- Implementar jugador i els seus moviments  
- Implementar col·lisions amb parets  
- Afegir enemics amb moviment simple  
- Afegir temporitzador  
- Implementar condicions de victòria i derrota  
- Proves i ajustos finals  
- Millores i refinament  

---

## 15. Eines previstes i justificació
- **Godot:** motor de desenvolupament per crear el joc 2D amb suport visual i de scripting  
- **GDScript:** llenguatge integrat de Godot, senzill i similar a Python  
- **GitHub:** control de versions i documentació del projecte  
- **IA (ChatGPT):** suport per disseny, estructura, codi i idees durant el desenvolupament  
- **YouTube:** per entendre el funcionament de Godot i com implementar algunes funcions  
