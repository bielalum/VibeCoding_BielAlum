# Fase 4: Proves i Depuració

En aquest document es troben totes les proves que he anat fent al videojoc per assegurar-me que funciona bé, els errors que s'han detectat durant el desenvolupament i com els he solucionat.

---

## 1. Taula de Casos de Prova

He dissenyat un total de 5 casos de prova per comprovar certs punts del joc (moviment, temps, col·leccionables i condicions de final de partida).

| ID     | Objectiu de la prova                         | Condicions inicials                              | Entrada / Acció                                     | Resultat esperat                                                                    | Resultat obtingut                                                     | Conclusió    |
| :----- | :------------------------------------------- | :----------------------------------------------- | :-------------------------------------------------- | :---------------------------------------------------------------------------------- | :-------------------------------------------------------------------- | :----------- |
| **01** | Comprovar el moviment i l'acció d'ajupir-se. | Joc iniciat, personatge quiet a terra.           | Prem fletxes esquerra/dreta i després fletxa avall. | El personatge s'ha de moure, girar i, en prémer avall, quedar-se quiet i ajupir-se. | El personatge es mou, gira i s'ajup correctament tallant el moviment. | **CORRECTE** |
| **02** | Recollida de monedes.                        | Monedes actives al mapa.                         | El jugador camina per sobre d'una moneda.           | La moneda ha de desaparèixer instantàniament i sumar-se al sistema.                 | La moneda es desapareix al tocar-la.                      | **CORRECTE** |
| **03** | Final de temps (Derrota).                    | Joc iniciat amb el cronòmetre corrent.           | Esperar sense fer res que el temps arribi a 0.      | El joc s'ha de pausar i ha d'aparèixer la pantalla de Game Over.                    | El joc es pausa i surt la imatge de derrota a les 0:00.               | **CORRECTE** |
| **04** | Intentar guanyar sense monedes.              | Queden monedes al mapa per recollir.             | El jugador va directe a la bandera de meta.         | La meta ha de bloquejar la victòria perquè encara queden monedes al laberint.       | El jugador passa per sobre de la meta i no passa res, el joc segueix. | **CORRECTE** |
| **05** | Condició de Victòria.                        | Totes les monedes del mapa han estat recollides. | El jugador toca la bandera de meta.                 | El joc es pausa i apareix la pantalla lila de "Victory".                            | Apareix la pantalla de victòria correctament.                         | **CORRECTE** |

---

## 2. Documentació d'Incidències Reals

Durant les proves de testeig he trobat problemes de lògica i disseny que he hagut de corregir per poder acabar el joc. Aquestes han sigut dues incidències:

### Incidència 1: El botó de reiniciar no deixava fer-se petit i no funcionava

* **Com es va detectar:** Quan es passava la pantalla de Game Over o Victòria, vaig intentar fer petit el botó verd de reiniciar. El recuadre vermell de Godot es feia petit, però la imatge es quedava gegant cap a fora. A més, en fer-li clic un cop el joc fallava, el botó no feia res.

* **Causa:** La imatge original tenia massa resolució i el `Stretch Mode` de la textura estava en mode *Keep* per defecte. A més, com que el joc es pausava (`get_tree().paused = true`), el motor de Godot també adormia els botons i no detectava els clics.

* **Solució:** Vaig anar a l'inspector del `TextureButton`, vaig activar la propietat `Ignore Texture Size` i vaig canviar el mode d'estirament a `Scale`. Després vaig anar a la propietat `Process` de les pantalles i vaig posar el mode en `Always` perquè els botons funcionin encara que el joc estigui congelat.

![Configuració del TextureButton i Process Always](imatges/texturebutton_process_always.png)

* **Comprovació:** Vaig tornar a iniciar el joc, vaig deixar que s'acabès el temps i al sortir la pantalla de derrota, el botó es veia a la mida perfecta i al fer-hi clic es reiniciava la partida correctament.

---

### Incidència 2: La meta donava la victòria abans d'hora sense agafar monedes

* **Com es va detectar:** En fer una prova caminant directe cap a la bandera de la meta sense agafar cap moneda, el joc em treia directament el cartell de Victòria i em donava la partida per guanyada.

* **Causa:** El script original de la meta (`meta.gd`) buscava les monedes a través d'un bucle que comprovava si el nom del node de la moneda coincidia exactament en minúscules (`moneda`). Com que a l'editor els nodes s'havien duplicat amb majúscules (`Moneda2`, `Moneda3`), el codi no les trobava, feia un recompte de 0 i donava la victòria de manera errònia.

* **Solució:** Vaig canviar l'estratègia de programació i vaig fer servir el sistema de **Grups** de Godot, que és molt més segur. Vaig ficar totes les monedes dins d'un grup anomenat `monedas` des de l'editor i vaig modificar el codi de la meta perquè funciones així:

```gdscript
extends Area2D

func _on_body_entered(body):
	if body.name == "Player":
		# Recompte automàtic de nodes actius dins del grup oficial
		var monedas_restantes = get_tree().get_nodes_in_group("monedas")
		
		# Si la llista està buida, el jugador realment ha agafat tot
		if monedas_restantes.size() == 0:
			get_parent().ganar_partida()
		else:
			print("Encara queden monedes per recollir!")
```

* **Comprovació:** Vaig iniciar la partida i vaig anar directe a la meta sense agafar res. El personatge passava per sobre de la bandera, no passava res i a la consola sortia el missatge d'avís. Només em va deixar guanyar quan el mapa estava totalment sense monedes.

---

## 3. Conclusió

Les proves realitzades han permès validar correctament les mecàniques principals del videojoc, garantint que el moviment del personatge, la recollida de monedes, el sistema de temps, les condicions de derrota i la pantalla de victòria funcionen com jo volia.
