# Guía de Instalación y Configuración: GrumPHP para Drupal

Esta guía detalla los pasos para implementar un flujo de validación pre-commit robusto, enfocado en **Drupal**, principios **SOLID** y metodologías **GreenCode**.

---

## 1. Requisitos Previos

*   **PHP** >= 8.1
*   **Composer** instalado.
*   **Node.js & NPM** instalados.
*   Repositorio **Git** inicializado.

---

## 2. Instalación de Dependencias PHP (Composer)

Ejecuta el siguiente comando para instalar GrumPHP y las herramientas de análisis estático, arquitectura y sostenibilidad:

```bash
composer require --dev phpro/grumphp \
  mglaman/phpstan-drupal \
  phpmd/phpmd \
  sebastian/phpcpd \
  ergebnis/composer-normalize
```

> [!NOTE]
> `phpmd` ayuda con **SOLID** (complejidad) y `phpcpd` detecta duplicidad para **GreenCode**.

---

## 3. Instalación de Dependencias JS/CSS (NPM)

Instala los linters y las configuraciones base de Drupal Core:

```bash
npm install --save-dev eslint \
  stylelint \
  stylelint-config-standard \
  eslint-config-airbnb-base \
  eslint-plugin-import \
  eslint-plugin-prettier \
  prettier \
  eslint-config-prettier \
  eslint-plugin-yml
```

---

## 4. Archivos de Configuración Clave

### A. `.gitignore`
Asegúrate de ignorar `node_modules` para evitar que GrumPHP intente procesarlos (lo que causa errores de memoria):

```ignore
/node_modules/
package-lock.json
```

### B. `grumphp.yml` (Raíz del proyecto)
Crea o actualiza el archivo `grumphp.yml` con las tareas automatizadas. El contenido debe incluir las secciones de `phpmd`, `phpcpd`, `phpcs`, `phpstan`, `eslint`, `stylelint`, `jsonlint`, `yamllint` y `xmllint`.

### C. `phpstan.neon` (Análisis de Drupal)
Configura PHPStan para que reconozca el núcleo de Drupal y use el nivel 8 o superior.

---

## 5. Activación de Git Hooks

Para que GrumPHP intercepte tus commits, debes inicializar los hooks:

```bash
vendor/bin/grumphp git:init
```

---

## 6. Comandos útiles

| Acción | Comando |
| :--- | :--- |
| **Ejecutar todas las pruebas** | `vendor/bin/grumphp run` |
| **Normalizar composer.json** | `composer normalize` |
| **Fix automático PHP (Drupal)** | `vendor/bin/phpcbf --standard=Drupal,DrupalPractice docroot/modules/custom` |
| **Ver estado de hooks** | `vendor/bin/grumphp git:status` |

---

## 7. Filosofía GreenCode & SOLID

El sistema ahora valida automáticamente:
- **SOLID**: A través de `phpmd` (evita clases gigantes y métodos complejos).
- **GreenCode**: A través de `phpcpd` (evita código duplicado) y el recordatorio visual al final de cada commit exitoso.

---

> [!TIP]
> Si el sistema te detiene, lee el mensaje de error: GrumPHP te dará el comando exacto para corregir el fallo (especialmente en ESLint y Stylelint con el flag `--fix`).
