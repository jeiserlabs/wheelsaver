# [ODD] WheelSaver — Catálogo Maestro de Librerías y Servidor MCP Anti-Reinvención

> **Metodología:** ODD (One-Document-Driven Development / Gentle-AI).  
> **Abolición SDD:** Sustituye la burocracia de especificaciones multi-documento por este único documento vivo.  
> **Proyecto:** `WHEELSAVER` (Catálogo maestro de 25k+ repositorios, auditor de sobre-ingeniería y servidor MCP)  
> **Fecha:** 2026-10-25 | **Estado:** Operativo en Ecosistema

---

## 1. Objetivo y Problema (Why & What)
- **Problema:** En el desarrollo acelerado con IA, los agentes tienden a reescribir desde cero utilidades complejas (parsers, clientes, formateadores, orquestadores) reinventando la rueda, introduciendo bugs y acumulando deuda técnica.
- **Objetivo:** Proporcionar un motor local de consulta y recomendación inmediata:
  1. Base de datos SQLite curada con repositorios top de GitHub clasificados por calidad, frescura y estrellas.
  2. Servidor MCP STDIO (`mcp_server.js`) integrado en `mcp.json` para consulta instantánea por agentes sin daemons en background.
  3. CLI rápido (`wheel:search`, `wheel:top`, `wheel:stats`) integrado con LifeOS.

---

## 2. Scope Rule Estricto (Gentleman Scope)
- **Touchables:**
  - `mcp_server.js`, `mcp_helpers.js`
  - `scraper/*`, `services/*`, `cli_commands/*`
  - `tests/*`
  - `.odd/tasks/*`
- **Forbidden:**
  - Daemons residentes en memoria en idle.
  - Modificar esquemas de bases de datos sin migración atómica.

---

## 3. Guardrails Anti-Sobreingeniería (Anti-Overengineering)
- **Local-First $0 Costo:** Consultas locales ultra-rápidas a SQLite (`data/top_repos.db`).
- **Integración STDIO:** Los agentes interactúan mediante pipes estándar, liberando memoria al terminar cada llamada.

---

## 4. Tareas Atómicas Secuenciales (Tasks)
- [x] **T1: Motor de Búsqueda y Scoring:** Búsqueda por palabras clave, lenguaje y estrellas en `scraper/search.py`.
- [x] **T2: Servidor MCP STDIO:** Herramientas `search_repos`, `audit_project`, `suggest_replacements` en `mcp_server.js`.
- [x] **T3: Auditor de Sobreingeniería:** Inspección de dependencias y código ad-hoc redundante (`services/project_auditor.py`).
- [x] **T4: Suite de Pruebas:** Tests unitarios y de MCP helpers.

---

## 5. Acceptance Criteria & Oráculo Determinista
- **MCP Server Health:** `npm run wheel:health` desde LifeOS ➔ Exit 0.
- **CLI Search:** `npm run wheel:search "terminal"` ➔ Retorna repositorios relevantes.

---

## 6. Baseline de Errores Conocidos (Known Baseline)
- Ninguno activo.

---

## 7. Progreso y Evidencia In-Place
- **2026-10-25:** Metodología ODD adoptada formalmente en WHEELSAVER.
- **2026-10-28:** Evidencia medida: `npm run wheel:health` OK (instalación completa, API detenida on-demand) y catálogo/stats responden.
