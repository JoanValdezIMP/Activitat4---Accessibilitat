# Fase 5 — Remediació i re-test

**Data:** 15 de novembre de 2026  
**Abast seleccionat:** tres findings confirmats: A11Y-01, A11Y-02 i A11Y-03. No s'ha intentat eliminar tots els findings de l'aplicació.

## Resultats automàtics abans i després

S'ha repetit l'auditoria amb `@axe-core/cli` 4.14.0, les mateixes tres rutes i un retard de càrrega de 1.500 ms.

| Pàgina | Abans | Després | Resultat |
|---|---:|---:|---|
| Home | 0 violacions | 0 violacions | Igual |
| Owners | 2 violacions | 0 violacions | Millora |
| Add Owner | 1 violació | 0 violacions | Millora |

### Findings corregits

| Finding | Abans | Després | Resultat |
|---|---|---|---|
| A11Y-01 — Contrast dels noms d'Owners | Fail: `3.98:1` (`#0d6efd` sobre `#f1f1f1`) | Pass: axe no detecta violacions de contrast. El navegador aplica `#0a58ca` en estat normal i `#084298` en hover; les ràtios calculades sobre `#f1f1f1` són `5.70:1` i `8.29:1`, respectivament ([owner-list.component.css](../src/app/owners/owner-list/owner-list.component.css)). | Corregit |
| A11Y-02 — `<h1>` a Owners | Fail: el títol era `<h2>` | Pass: “Owners” ara s'exposa com a encapçalament de nivell 1 ([owner-list.component.html](../src/app/owners/owner-list/owner-list.component.html)). | Corregit |
| A11Y-03 — `<h1>` a Add Owner | Fail: el títol era `<h2>` | Pass: “New Owner” ara s'exposa com a encapçalament de nivell 1 ([owner-add.component.html](../src/app/owners/owner-add/owner-add.component.html)). | Corregit |

Per preservar l'aparença, els nous `<h1>` utilitzen la classe visual Bootstrap `h2`.

## Validació manual i tècnica

- **Contrast i focus:** en navegar amb `Tab` fins al primer nom de propietari, l'enllaç manté un indicador de focus visible. El navegador exposa una vora de focus taronja (`rgb(229, 151, 0)`). També s'han comprovat al navegador els colors normal i hover.
- **Encapçalaments:** l'arbre accessible mostra “Owners” i “New Owner” com a `heading level 1`.
- **Build:** `npm run build` — correcte.
- **Tests:** `npm run test:ci` — 30 fitxers i 102 tests passats. La sortida inclou un avís de compilació sobre `src/polyfills.ts`, sense fallada de build ni tests.
- **axe:** les captures post-remediació de Home, Owners i Add Owner tenen zero violacions. Vegeu [axe-home-after-remediation.json](./axe-home-after-remediation.json), [axe-owners-after-remediation.json](./axe-owners-after-remediation.json) i [axe-add-owner-after-remediation.json](./axe-add-owner-after-remediation.json). Les captures originals es conserven per a la comparació.

## Findings no seleccionats

- **A11Y-04 — Alternativa de la imatge de Home:** no s'ha canviat; continua pendent decidir si la imatge és informativa o decorativa.
- **A11Y-05 — Títol de document:** no s'ha canviat en aquest cicle de tres remediacions. El títol genèric continua pendent.

L'auditoria automàtica no substitueix les comprovacions manuals ni demostra conformitat completa.
