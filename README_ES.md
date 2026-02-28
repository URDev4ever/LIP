<h1 align="center">LIP: Logic Injection Payloads</h1>
<p align="center">
  🇺🇸 <a href="README.md"><b>English</b></a> |
  🇪🇸 <a href="README_ES.md">Español</a>
</p>
<h3 align="center">
Una colección curada de payloads de inyección lógica, confusión de tipos y casos límite, diseñada para romper suposiciones inseguras en la lógica de las aplicaciones.
</h3>

Este repositorio se enfoca en escenarios donde las entradas son técnicamente válidas, pero semánticamente inesperadas, lo que deriva en bypass de autenticación, problemas de autorización, abuso de funcionalidades o lógica de negocio rota.

A diferencia de los payloads de inyección clásicos (SQLi, XSS, etc.), estos payloads apuntan a **cómo el código *piensa***, no a cómo parsea.

---

## Propósito

Las aplicaciones modernas suelen depender de:

* Coerción implícita de tipos
* Chequeos truthy / falsy
* Comparaciones débiles (`==`)
* Validación incompleta
* Suposiciones sobre la forma o el estado de la entrada

Este repositorio existe para ayudar a:

* Identificar fallas lógicas
* Probar condicionales inseguros
* Explorar casos límite que eluden restricciones previstas
* Demostrar por qué la validación estricta es importante

---

## Estructura del Repositorio

Los payloads están agrupados por **categoría lógica**, no por clase de vulnerabilidad.

```
LIP/
├── arrays-objects/
├── auth/
├── booleans/
├── edge-cases/
├── null-state/
└── numbers/
```

Cada carpeta contiene:

* `cases.txt` – Escenarios lógicos realistas con comportamiento esperado vs comportamiento roto
* `variants.txt` – Valores de payload reutilizables para inyectar y probar

---

## Descripción de Categorías

### Arrays y Objetos

Payloads que explotan suposiciones sobre el tipo y la estructura de la entrada.

Objetivos comunes:

* Chequeos de roles
* Flags de permisos
* Comparaciones de objetos
* Verificaciones de existencia de arrays

Se enfoca en:

* Arrays vs strings
* Objetos vs primitivos
* Chequeos de constructor
* Contenedores vacíos vs no vacíos

---

### Autenticación y Autorización

Payloads diseñados para bypassear o confundir la lógica de autenticación.

Objetivos comunes:

* Verificaciones de login
* Validación de sesión
* Aplicación de roles
* Flags de autenticación

Destaca problemas con:

* Strings no vacíos
* Igualdad débil
* Valores truthy aceptados como autenticados
* Falta de chequeos estrictos de tipo

---

### Booleanos

Apunta a lógica que depende de suposiciones booleanas.

Problemas comunes:

* `"false"` evaluado como truthy
* `1 == true`
* Arrays y objetos pasando chequeos booleanos
* Lógica de negación con comportamientos inesperados

Útil para:

* Feature flags
* Toggles de administrador
* Controles de acceso

---

### Casos Límite

Payloads que explotan valores invisibles o poco comunes.

Incluye:

* Bytes nulos
* Caracteres de ancho cero
* Caracteres BOM
* Espacios en blanco al final
* Notación científica
* Rarezas de parsing

Estos valores suelen evadir:

* Lógica de trimming
* Normalización de mayúsculas/minúsculas
* Parsing numérico

---

### Confusión de Null y Estado

Se enfoca en estados faltantes, indefinidos o inesperados.

Apunta a lógicas como:

* `if (value)`
* `if (!value)`
* `value != "banned"`
* `data && data.id`

Impactos comunes:

* TypeErrors
* Concesión incorrecta de accesos
* Aceptación de estados inválidos

---

### Números

Payloads que abusan de la lógica y comparaciones numéricas.

Incluye:

* Casos límite de cero (`-0`, `0.0`)
* Precisión de coma flotante
* `NaN` e `Infinity`
* Límites de overflow de enteros
* Coerción de tipos con strings y booleanos

Suele afectar:

* Precios
* Límites
* Cooldowns
* Contadores
* Cuotas

---

## Dónde es Útil (Resumen)

Estos payloads son aplicables en muchos escenarios reales, incluyendo:

* **Puntos de entrada en aplicaciones web**
  Formularios, parámetros de query, cuerpos JSON, headers, cookies y claims de JWT.

* **Manipulación de requests HTTP**
  Modificación de requests válidos usando herramientas como Burp Suite, ZAP o mitmproxy para inyectar tipos o estados inesperados.

* **Testing de lógica en APIs**
  Detección de suposiciones rotas en APIs REST o GraphQL sin enforcement estricto de esquemas.

* **Pruebas de bypass de autenticación y autorización**
  Explotación de chequeos débiles basados en truthiness, igualdad laxa o validación inexistente.

* **Abuso de lógica de negocio**
  Romper flujos relacionados con pagos, límites, cooldowns, feature flags o control de acceso.

* **Fuzzing de casos límite (enfocado en lógica)**
  Fuzzing semántico orientado a errores lógicos en lugar de crashes.

* **Testing del límite de confianza cliente ↔ servidor**
  Cuando existe validación en frontend pero la validación backend es incompleta o inexistente.

* **CTFs, wargames y laboratorios**
  Ideal para desafíos centrados en fallas lógicas en lugar de inyecciones clásicas.

* **Code review y desarrollo seguro**
  Identificación de condicionales peligrosos y mejora de prácticas de programación defensiva.

---

## Filosofía de Uso

Este repositorio no está pensado para ser:

* Un kit de exploits listo para usar
* Un framework de ataque automatizado

Sí está pensado para ser:

* Una referencia de testing
* Una herramienta para pensar
* Un checklist para romper lógica

Usá los payloads para:

1. Identificar suposiciones en el código
2. Desafiar esas suposiciones
3. Observar comportamientos no deseados
4. Corregir la falla lógica de raíz

---

## Disclaimer

Este repositorio se proporciona **únicamente con fines educativos, defensivos y de testing de seguridad autorizado**.

No utilices estos payloads contra sistemas que no poseas o para los que no tengas permiso explícito.

El autor no asume responsabilidad por el mal uso.

---

Hecho con <3 por URDev.
