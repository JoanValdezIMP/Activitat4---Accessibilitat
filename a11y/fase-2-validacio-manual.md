# Fase 2 — Validació manual

**Data:** 15 de novembre de 2026  
**Pàgines:** Home (`/`), Owners (`/petclinic/owners`) i Add Owner (`/petclinic/owners/add`).

## Metodologia

S’han inspeccionat les pàgines renderitzades al navegador. La navegació amb `Tab` i `Shift+Tab` s’ha reproduït amb el teclat del navegador; s’ha observat l’element enfocat i, per al focus, els estils calculats. Els noms accessibles dels camps i les alternatives de les imatges s’han contrastat amb l’arbre accessible i el contingut HTML. No s’ha utilitzat cap lector de pantalla.

## Resultats

| ID | Comprovació | Pàgina | Resultat | Evidència |
|---|---|---|---|---|
| MAN-01 | Navegació amb teclat | Home, Owners i Add Owner | Pass | `Tab` arriba als enllaços i botons de navegació i als controls disponibles. Amb l’API disponible, també arriba als 10 enllaços de propietaris i al botó Add Owner d’Owners. `Shift+Tab` recorre els controls enrere. A Add Owner, el botó de submit està deshabilitat amb el formulari buit i, per tant, no rep focus. |
| MAN-02 | Ordre del focus | Home, Owners i Add Owner | Pass | El focus recorre primer la navegació horitzontal d’esquerra a dreta i després el contingut en ordre visual. Owners segueix el formulari de cerca, les 10 files de la taula i Add Owner. Add Owner segueix First Name, Last Name, Address, City, Telephone i Back. |
| MAN-03 | Focus visible | Owners i Add Owner | Pass | Després de deixar acabar la transició visual, els enllaços, botons i camps mostren un indicador. Als camps `lastName` i `firstName` es veu una vora verda (`rgb(109, 179, 63)`) i una ombra exterior de focus de 3,2 px. |
| MAN-04 | Labels del formulari | Add Owner | Pass | Els cinc camps tenen un `<label>` associat pel parell `for`/`id`; el navegador n’exposa els noms First Name, Last Name, Address, City i Telephone. |
| MAN-05 | Títols i text alternatiu | Home, Owners i Add Owner | Fail | Home té `<h1>` i `<h2>`. Owners i Add Owner només tenen un `<h2>` (“Owners” i “New Owner”). La imatge principal de Home mostra un gos i un gat, però l’alternativa és “pets logo”, que no descriu la fotografia; els logotips del peu sí que tenen text alternatiu. |

## Limitacions

Durant la primera inspecció, l’API no responia; després d’iniciar el backend s’han carregat i recorregut amb teclat 10 propietaris. No s’ha provat amb lector de pantalla.
