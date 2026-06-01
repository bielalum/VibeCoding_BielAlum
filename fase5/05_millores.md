# Fase 5: Millores Aplicades i Futures

Aquest document detalla les millores que s'han anat introduint al videojoc un cop es va tenir la primera versió funcional bàsica. L'objectiu ha estat polir la jugabilitat, augmentar la dificultat i assegurar que el codi sigui molt més robust contra errors.

---

## 1. Millores Aplicades al Projecte

A partir del test de control de la fase anterior, s'han implementat 3 millores principals:

### Millora 1: Disseny de nivell i augment de la dificultat (Jugabilitat)
* **Problema inicial:** Al primer prototip, el laberint estava massa buit. El camí cap a la meta era molt directe, gairebé no hi havia obstacles i el jugador es podia passar el nivell en pocs segons sense cap mena de repte.
* **Millora aplicada:** Vaig refer part del mapa afegint molts més blocs de paret i obstacles físics a la pantalla. D'aquesta manera, el camí es torna molt més estret, obligant el jugador a saltar amb precisió i a esquivar camins tallats per trobar les monedes.
* **Efecte en el projecte:** Ha canviat completament l'experiència de l'usuari, ara cada error de moviment et fa perdre temps.

### Comparació abans i després

![Abans i despres](https://raw.githubusercontent.com/bielalum/VibeCoding_BielAlum/main/imatges/abans_despres.png)
---

### Millora 2: Ajust del temporitzador mitjançant testeig (Experiència de l'usuari - Speedrun)
* **Problema inicial:** El temps inicial del cronòmetre estava posat de manera aleatòria i sobrava gairebé tot el rellotge, perdent tota la gràcia del concepte "speedrun".
* **Millora aplicada:** Vaig fer moltes partides de prova cronometrades per veure quin era el temps mínim real que es trigava en agafar totes les monedes i arribar a la meta. Després d'aquest testeig, vaig ajustar el node `Timer` amb els segons exactes perquè el jugador hagi d'anar al límit de la velocitat sense cometre errades si vol guanyar.
* **Efecte en el projecte:** Afecta directament a la tensió del joc. Ara el temporitzador realment genera una sensació de pressa i repte que abans no existia.

---

### Millora 3: Refactorització del sistema de recompte (Millora de Codi)
* **Problema inicial:** La meta comprovava el text del nom de les monedes d'una en una. Si canviava una lletra majúscula a l'editor per accident, el joc es trencava i donava la victòria abans d'hora.
* **Millora aplicada:** Es va canviar tot el codi de `meta.gd` per utilitzar la funció nativa de grups de Godot (`get_tree().get_nodes_in_group("monedas")`), que comprova l'estat dels nodes d'una manera 100% segura sense importar com es diguin a l'arbre d'escenes.
* **Efecte en el projecte:** El codi és molt més net, no llança errors de validació a la consola i la condició de victòria s'ha tornat completament infalible.

---

## 2. Respostes a les preguntes

* **Quines millores has aplicat?** Millores en el disseny del mapa (obstacles), equilibri del temps d'speedrun i estabilitat del codi.
* **Per què eren necessàries?** Perquè al ser un joc curt, necessitava algo més que incentivès al jugador a jugar-hi, en aquest cas la dificultat.
* **Quina part del projecte afecten?** Afecten el disseny del nivell (`TileMap`), la interfície de control (`CanvasLayer`) i la lògica dels scripts del Laberint i la Meta.
* **Què ha canviat respecte a la versió anterior?** El joc ara és molt més difícil i divertit, els menús funcionen perfectament en qualsevol estat i el codi ja no té errors.
* **Com has comprovat que la millora funciona?** Fent partides completes de prova: morint expressament, intentant saltar-me les monedes i prement els botons per comprovar que tot funciona bé.

---

## 3. Millores Pendents

Si hagués tingut més temps per al desenvolupament d'aquest projecte, m'hauria agradat afegir les següents funcionalitats que queden pendents com a futures millores:

1. **Enemics mòbils:** Afegir petits enemics que es moguessin amb una IA simple d'esquerra a dreta. L'objectiu seria que, en tocar-los, fessin perdre temps al jugador (penalització de segons) o el fessin tornar a començar des del punt d'inici, afegint encara més dificultat a l'speedrun.
2. **Sistema de punts i Highscore:** Implementar una variable global que guardés els millors temps aconseguits de cada partida (rècord personal) mitjançant un fitxer de guardat local (`Configfile` o `FileAccess`), incentivant així a rejugar el joc per intentar superar el teu temps.
3. **Múltiples Nivells:** Crear un sistema de progressió on, en tocar la bandera amb totes les monedes, el joc passés a un "Laberint 2" amb un disseny totalment diferent i més complex, en lloc d'anar directe a la pantalla de victòria final.
