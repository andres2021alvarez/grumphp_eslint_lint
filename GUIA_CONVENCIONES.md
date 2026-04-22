# Guía de Convenciones y Calidad (GrumPHP)

Este proyecto utiliza **GrumPHP** para asegurar la calidad del código y la consistencia en el flujo de trabajo. Aquí tienes los puntos clave para que tus commits sean siempre exitosos.

## 1. Nomenclatura de Ramas
GrumPHP bloquea commits directos a `master` o ramas con nombres genéricos.
- **Formato permitido:** `(feature|bugfix|hotfix|release|chore|test)/nombre-descriptivo`
- **Ejemplo:** `git checkout -b feature/setup-linters`

## 2. Mensajes de Commit
Los mensajes deben ser concisos para mantener la legibilidad del historial.
- **Regla de oro:** El asunto (primera línea) no debe superar los **72 caracteres**.
- **Ejemplo correcto:** `feat: add eslint and stylelint configurations`
- **Ejemplo incorrecto:** `feat: initialize project with GrumPHP, PHPStan, and dependency configuration` (Demasiado largo)

## 3. Requerimientos de `composer.json`
Antes de hacer un commit, asegúrate de que:
1. El archivo tenga definidos los campos `"name"`, `"description"` y `"license"`.
2. El archivo esté **normalizado** (ordenado según el estándar).
   - **Comando:** `composer normalize`

## 4. Herramientas de Análisis
Al ejecutar `git commit`, GrumPHP lanzará automáticamente:
- **PHP:** PHPMD, PHPCS, PHPStan, PHPCPD.
- **JS/CSS:** ESLint, Stylelint.
- **Formatos:** JSONLint, YamlLint, XMLLint.

---

## Solución de Problemas Comunes

### "Matched blacklist rule: master"
Estás intentando commitear en la rama principal. Crea una rama de característica:
`git checkout -b feature/mi-tarea`

### "Please keep the subject <= 72 characters"
Tu mensaje de commit es muy largo. Acórtalo o usa `git commit -m "Título corto" -m "Descripción extendida aquí..."`.

### "composer.json is not normalized"
Ejecuta `composer normalize` para corregir el orden de las dependencias.

---
*Nota: Si necesitas saltarte los checks en un caso de extrema emergencia, puedes usar `git commit --no-verify`, pero esto no es recomendable.*
