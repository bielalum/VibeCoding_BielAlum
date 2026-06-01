# 🎮 Maze Protocol

Projecte desenvolupat per **Biel Alum**

---

## 📌 Descripció

**Maze Protocol** és un videojoc de plataformes 2D en format *Speedrun*. El jugador controla en Foxy, un astut personatge que ha de recórrer un laberint ple d'obstacles per recollir totes les monedes daurades i arribar a la bandera de la meta abans que el temporitzador de la interfície arribi a zero. 


---

## 🎬 Vídeo de Gameplay Comentat

A continuació es mostra l'enllaç a la demostració guiada del sistema desenvolupat, on s'expliquen les mecàniques principals, les decisions de disseny i la lògica del codi:

👉 **Fes clic aquí per veure el vídeo del Gameplay https://drive.google.com/drive/folders/1AfVpzVLlcHGtpgMhXOZzZBScJCPoipGR?usp=sharing** 

---

## 🧱 Organització del Projecte

El repositori s'ha estructurat de manera modular dividint tota la documentació oficial en diferents fases de desenvolupament:

* **Fase 1** → Idea i definició del joc
* **Fase 2** → Disseny i diagrames UML
* **Fase 3** → Implementació del joc
* **Fase 4** → Proves i Depuració
* **Fase 5** → Millores Aplicades i Futures
* **Fase 6** → Manual d'Usuari
* **Fase 7** → Manual Tècnic del Projecte

---

## 🛠️ Tecnologies Utilitzades

* **Godot Engine 4** (Motor de videojocs principal)
* **GDScript** (Llenguatge de programació orientat a nodes)
* **GitHub** (Control de versions, gestió del repositori i documentació)
* **Gemini (IA)** (Suport i assistència com a co-desenvolupador per a la refactorització de codi i revisió de text)

---

## 📂 Estructura de Fitxers del Codi

Dins del motor de joc, les entitats s'organitzen mitjançant els següents fitxers clau:
* `laberint.gd`: Control central de la partida, temporitzador i pantalles de Game Over / Victòria.
* `player.gd`: Lògica de física, moviment, salt i acció d'ajupir-se del personatge.
* `moneda.gd`: Sistema de col·lisió Area2D i destrucció del col·leccionable.
* `meta.gd`: Sistema de detecció mitjançant Grups per validar la condició de victòria.
