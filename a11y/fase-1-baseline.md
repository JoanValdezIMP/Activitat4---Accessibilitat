# Fase 1 — Auditoria automàtica (baseline)

**Data:** 15 de novembre de 2026  
**Abast:** Home (`/`), Owners (`/petclinic/owners`) i Add Owner (`/petclinic/owners/add`)  
**Entorn:** frontend local a `http://localhost:4200`, Chrome i ChromeDriver 157.0.8103.78, `@axe-core/cli` i axe-core 4.14.0.  
**Execució:** CLI en mode headless, amb un retard de càrrega de 1.500 ms i la configuració predeterminada de regles.

## Resultats

| Pàgina | Violacions | Impacte | Finding principal | Prioritat inicial |
|---|---:|---|---|---|
| Home | 0 | — | Cap violació detectada per axe en aquesta càrrega | Sense finding automàtic |
| Owners | 2 | Serious / Moderate | `color-contrast`: 10 noms d’owners amb contrast 3.98:1; falta un `<h1>` | Alta / Mitjana |
| Add Owner | 1 | Moderate | `page-has-heading-one`: falta un `<h1>`; el títol “New Owner” és `<h2>` | Mitjana |

La violació `color-contrast` d’Owners afecta els 10 enllaços dels noms de propietaris: contrast `3.98:1` (`#0d6efd` sobre `#f1f1f1`), per sota del mínim `4.5:1` indicat per axe. El resultat porta el tag `wcag143`, corresponent a WCAG 1.4.3 (Contrast mínim). La violació `page-has-heading-one` afecta l’element `html` i requereix un encapçalament de nivell 1; axe la classifica com a `best-practice`, sense associar-li cap criteri WCAG concret. Els impactes són els indicats per axe i les prioritats són inicials.

La taula reflecteix la captura d’Owners amb dades del backend disponible. La primera captura, sense backend, s’ha conservat separadament.

## Evidències

- [axe-home.json](./axe-home.json)
- [axe-owners-data-loaded.json](./axe-owners-data-loaded.json) — Owners amb 10 registres carregats.
- [axe-owners.json](./axe-owners.json) — primera captura d’Owners, sense dades.
- [axe-add-owner.json](./axe-add-owner.json)

Cada fitxer conserva el resultat JSON complet d’axe, inclosos els nodes afectats, selectors, tags, passades, elements no verificables i marca temporal.

## Mètode i limitacions

Les tres auditories s’han executat amb `@axe-core/cli`. Per fer-ho, s’ha utilitzat el ChromeDriver 157.0.8103.78 compatible amb el navegador instal·lat i s’han desat els resultats JSON complets.

Els resultats automàtics no substitueixen les comprovacions manuals ni demostren conformitat completa.

## Incidència d’entorn: API de propietaris

- **Símptoma inicial:** el frontend responia a `http://localhost:4200`, però una petició a `http://localhost:9966/petclinic/api/owners` no obtenia resposta.
- **Configuració verificada:** l’URL base de l’API és `http://localhost:9966/petclinic/api/` ([environment.ts](../src/environments/environment.ts)); `OwnerService` hi consulta el recurs `owners` ([owner.service.ts](../src/app/owners/owner.service.ts)).
- **Resolució:** s’ha iniciat el backend local `spring-petclinic-rest`. `GET /petclinic/actuator/health` retorna `UP` i `GET /petclinic/api/owners` retorna HTTP 200 amb 10 registres. El frontend mostra 10 files.
- **Comanda d’inici:** des de `backend/spring-petclinic-rest`, definir `JAVA_HOME` al JDK instal·lat i executar `.\mvnw.cmd spring-boot:run`.
- **Impacte inicial:** la primera captura d’Owners no tenia dades; per això s’ha conservat [axe-owners.json](./axe-owners.json) i s’ha generat [axe-owners-data-loaded.json](./axe-owners-data-loaded.json) com a auditoria complementària amb la taula carregada.
- **Estat:** resolt a l’entorn local en iniciar el backend; no s’ha modificat el codi de l’API.

