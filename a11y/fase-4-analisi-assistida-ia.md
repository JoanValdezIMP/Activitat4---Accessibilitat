# Fase 4 — Anàlisi assistida amb IA generativa

**Data:** 15 de novembre de 2026  
**Entrades:** resultats d'axe de la fase 1 i validació manual de la fase 2, consolidats a la fase 3.

## Mètode i privadesa

La IA s'ha utilitzat per interpretar les evidències locals, agrupar causes repetides, proposar correccions i identificar quines necessiten confirmació manual. No s'han enviat dades a serveis externs. La validació de l'alumne i la decisió final s'han recollit per a cada finding; la IA no substitueix aquesta decisió.

## Comparació entre proposta i validació

| Finding | Proposta de la IA | Validació de l'alumne | Decisió final |
|---|---|---|---|
| A11Y-01 — Contrast dels noms d'Owners | Ajustar el color dels enllaços perquè assoleixi almenys 4,5:1 sobre el fons i comprovar els estats normal, hover i focus. | Correcta | Aplicar a la fase 5 |
| A11Y-02 — `<h1>` a Owners | Fer que “Owners” sigui l'encapçalament principal (`<h1>`) i conservar una jerarquia coherent. | Correcta | Aplicar a la fase 5 |
| A11Y-03 — `<h1>` a Add Owner | Fer que “New Owner” sigui l'encapçalament principal (`<h1>`) i conservar una jerarquia coherent. | Correcta | Aplicar a la fase 5 |
| A11Y-04 — Alternativa de la imatge de Home | Si és informativa, descriure el gos i el gat; si és decorativa, usar `alt=""`. Confirmar-ne la funció abans de triar l'alternativa. | Parcial | Revisar: falta decidir si la imatge és informativa o decorativa |
| A11Y-05 — Títol de document | Definir un títol que identifiqui la vista actual, mantenint el nom de l'aplicació si és útil. | Correcta | Aplicar a la fase 5 |

## Validació de l'anàlisi

- **A11Y-01:** la recomanació aborda el contrast mesurat de `3.98:1` i el criteri WCAG 1.4.3. La fase 5 haurà de comprovar el contrast resultant i els estats interactius; no es fixa un color sense mesurar-lo.
- **A11Y-02 i A11Y-03:** la recomanació corregeix l'estructura observada. `page-has-heading-one` és una regla *best-practice* d'axe; no s'atribueix un criteri WCAG específic.
- **A11Y-04:** la proposta és parcial perquè el text alternatiu correcte depèn de la funció de la imatge. La discrepància entre la fotografia i “pets logo” està confirmada, però la decisió entre una descripció informativa i `alt=""` requereix criteri de contingut.
- **A11Y-05:** la validació de l'alumne accepta la proposta de títols específics per vista. La relació amb WCAG 2.4.2 és plausible; la fase 5 haurà de comprovar que cada títol descriu realment el propòsit de la pàgina.

Les prioritats de la fase 3 es mantenen: A11Y-01 alta i els altres findings mitjana. No s'ha modificat el codi en aquesta fase.
