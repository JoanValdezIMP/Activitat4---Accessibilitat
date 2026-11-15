# Fase 6 — Automatització bàsica amb Playwright + axe-core

**Data:** 15 de novembre de 2026  
**Objectiu:** convertir una auditoria d’accessibilitat en una prova repetible i automatitzada.

## Prova creada

S’ha creat una prova mínima a [../e2e/a11y-owners.e2e-spec.ts](../e2e/a11y-owners.e2e-spec.ts):

```ts
import { test, expect } from '@playwright/test';
import AxeBuilder from '@axe-core/playwright';

test('Owners page should have no axe violations', async ({ page }) => {
  await page.goto('/petclinic/owners');

  const results = await new AxeBuilder({ page }).analyze();

  expect(results.violations).toEqual([]);
});
```

La configuració de Playwright ja existia a [../playwright.config.ts](../playwright.config.ts), així que no s’ha necessitat una configuració addicional.

## Dependència afegida

S’ha instal·lat `@axe-core/playwright` per poder executar l’auditoria des de Playwright:

```bash
npm install -D @axe-core/playwright
```

## Execució i resultat

Comanda executada:

```bash
npx playwright test e2e/a11y-owners.e2e-spec.ts --reporter=line
```

Resultat real:

- **1 test executat**
- **1 test superat**
- **0 violacions detectades** a `/petclinic/owners`

Aquest resultat és vàlid perquè la pàgina de Owners ha quedat neta després de la remediació de la fase 5. La prova demostra el cicle detectar → validar → corregir → re-test en un format automatitzable i repetible.

## Observació

Si la pàgina hagués continuat amb violations, la prova hauria fallat i el resultat hagués estat útil per documentar quines regles les desencadenaven. Aquí, la prova confirma que l’Owners page ja no genera violacions d’axe en aquest estat.
