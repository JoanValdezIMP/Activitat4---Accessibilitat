# Fase 3 — Triatge i classificació dels findings

**Data:** 15 de novembre de 2026  
**Abast:** Home, Owners i Add Owner.

## Criteri de triatge

S'han consolidat els deu casos de contrast d'Owners en un únic finding perquè comparteixen la mateixa causa. La manca d'un encapçalament principal es manté separada per pàgina, ja que afecta dues pantalles i caldrà corregir-la a cadascuna. La prioritat combina l'impacte observat, l'abast i la relació amb WCAG; no és una puntuació automàtica d'axe.

## Taula consolidada

| ID | Pàgina | Problema | Origen | Impacte | Confirmat? | Prioritat |
|---|---|---|---|---|---|---|
| A11Y-01 | Owners | Els 10 enllaços amb noms de propietaris tenen contrast 3,98:1, inferior al mínim 4,5:1 per a text normal. | axe (`color-contrast`) | Pot dificultar la lectura dels noms, especialment a persones amb baixa visió. | Sí | Alta |
| A11Y-02 | Owners | La pàgina no té `<h1>`; “Owners” està marcat com a `<h2>`. | axe (`page-has-heading-one`), MAN-05 | Es perd un encapçalament principal clar per orientar-se i navegar per títols. | Sí | Mitjana |
| A11Y-03 | Add Owner | La pàgina no té `<h1>`; “New Owner” està marcat com a `<h2>`. | axe (`page-has-heading-one`), MAN-05 | Es perd un encapçalament principal clar per orientar-se i navegar per títols. | Sí | Mitjana |
| A11Y-04 | Home | La fotografia de gos i gat té l'alternativa “pets logo”, que no descriu la imatge. | Validació manual MAN-05 i HTML | Una persona que utilitza lector de pantalla rebria una descripció incorrecta. | Sí, la discrepància és observable | Mitjana |
| A11Y-05 | Home, Owners i Add Owner | Les tres rutes comparteixen el títol de document genèric “SpringPetclinicAngular”, sense identificar la pàgina actual. | Navegador i `src/index.html` | Pot dificultar distingir pestanyes i entendre la pàgina, especialment amb tecnologies d'assistència. | Sí, el mateix títol s'observa a les tres rutes | Mitjana |

## Evidència i relació amb WCAG

### A11Y-01 — Contrast dels noms d'Owners

- **Element afectat:** enllaços dels noms de propietaris a la taula d'Owners; 10 nodes a la captura amb dades.
- **Evidència:** `#0d6efd` sobre `#f1f1f1`, ràtio `3.98:1`; axe informa l'impacte *serious* i el tag `wcag143`. Vegeu [axe-owners-data-loaded.json](./axe-owners-data-loaded.json).
- **WCAG:** 1.4.3 Contrast (Minimum), nivell AA.
- **Prioritat alta:** és una violació mesurada d'un criteri WCAG i afecta tots els noms enllaçats de la llista.

### A11Y-02 i A11Y-03 — Manca d'encapçalament de nivell 1

- **Elements afectats:** `<h2>Owners</h2>` a [owner-list.component.html](../src/app/owners/owner-list/owner-list.component.html) i `<h2>New Owner</h2>` a [owner-add.component.html](../src/app/owners/owner-add/owner-add.component.html).
- **Evidència:** axe marca `page-has-heading-one` amb impacte *moderate* a Owners i Add Owner; la validació manual MAN-05 confirma la jerarquia observada. Vegeu [axe-owners-data-loaded.json](./axe-owners-data-loaded.json), [axe-add-owner.json](./axe-add-owner.json) i [fase-2-validacio-manual.md](./fase-2-validacio-manual.md).
- **WCAG:** no s'assigna un criteri WCAG concret: axe classifica aquesta regla com a *best-practice*. La prioritat mitjana reflecteix la pèrdua d'un encapçalament principal útil per orientar-se, no una violació WCAG confirmada.

### A11Y-04 — Alternativa de la imatge de Home

- **Element afectat:** `img[src="./assets/images/pets.png"]` amb `alt="pets logo"` a [welcome.component.html](../src/app/parts/welcome/welcome.component.html).
- **Evidència:** MAN-05 constata que la imatge representa un gos i un gat, no un logotip; el text alternatiu actual és inexacte.
- **WCAG:** 1.1.1 Non-text Content, nivell A, si la imatge és informativa. Si és purament decorativa, l'alternativa adequada és buida (`alt=""`). Cal decidir-ne la funció abans de triar el text final.
- **Prioritat mitjana:** l'alternativa actual pot induir a error; la correcció depèn de confirmar si la imatge aporta informació.

### A11Y-05 — Títol de document no específic

- **Element afectat:** `<title>SpringPetclinicAngular</title>` a [index.html](../src/index.html); el navegador mostra el mateix títol a les tres rutes auditades.
- **Evidència:** títol observat a Home, Owners i Add Owner; valor definit al document HTML.
- **WCAG:** relació probable amb 2.4.2 Page Titled, nivell A: el títol hauria de descriure el tema o propòsit de la pàgina. Es classifica com a finding confirmat perquè el títol és idèntic i genèric, però la decisió final ha de considerar si el nom de l'aplicació identifica prou bé la pàgina en aquest context.
- **Prioritat mitjana:** afegir el nom o propòsit de la vista ajudaria a distingir pestanyes i pàgines.

## Abast i limitacions

Els findings s'han seleccionat a partir de les evidències conservades de les fases 1 i 2 i de la inspecció del títol de document. La comprovació de focus amb teclat i les labels del formulari no han generat findings addicionals. No s'ha fet una prova amb lector de pantalla; per tant, els impactes descriuen riscos previsibles i no resultats d'una sessió amb lector.
