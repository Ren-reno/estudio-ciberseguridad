# Sesión 1.rev — Repaso de Verificación, Módulo 1 (TCP/IP)

**Para usar mañana. Pegá esto en una conversación nueva junto con tu progreso.md actual.**

---

```
Mi repo de estudio está en: https://github.com/Ren-reno/estudio-ciberseguridad

Si tenés herramientas para acceder a internet (bash con git, web fetch, un conector de
GitHub, o similar), cloná o consultá ese repo vos mismo y leé roadmap.md y progreso.md
directamente desde ahí — no hace falta que te los pegue.

Si NO tenés forma de acceder a internet o repos, decime explícitamente "no puedo acceder
al repo, pegame progreso.md y la sección relevante de roadmap.md" y esperá a que te los
pase, en vez de inventar o asumir contenido que no tenés.

Vamos a hacer la sesión de Repaso de Verificación 1.rev, Módulo 1 — TCP/IP a nivel de ingeniería.

Tengo avance previo real en este módulo (ver progreso.md, sección "Avance previo"). El
objetivo de hoy es verificar qué tan firme está, no enseñar de cero.

Formato (30-40 min, más corto que una sesión normal):
- Elegí vos 2-3 conceptos centrales del módulo — sin decírmelos antes de preguntarlos.
- Preguntame uno por uno. No des la respuesta ni pistas hasta que yo responda algo o me
  trabe más de 1 minuto.
- Para lo que salga flojo, un mini-refuerzo de la parte que falló, no la clase completa.

Si en cualquier momento escribo "saltar": no autorellenes como dominado sin verificar.
Hacé una sola pregunta corta de ese concepto puntual. Si la respondo bien, ahí sí generá
todo automáticamente y seguimos. Si la respondo mal, seguimos con el formato normal.

Al final generame un patch en formato de parche de email de Git (header From/Date/Subject,
From: Ren-reno <reinaldo.codoceo@inacapmail.cl>) con progreso.md actualizado: resultado de
este repaso, y si el módulo completo quedó firme, marcalo como completado. Si no pudiste
acceder al repo vos mismo, decime igual qué archivo/línea debería cambiar, en texto plano,
para que yo lo aplique a mano.
```

---

## Nota de contexto (no es parte del prompt, es para vos)

Ya revisé tu avance previo real en Módulo 1 (Días 2 y 9). El handshake TCP lo viste, pero a
nivel de "saludo" (SYN = "hola quiero conectar", SYN-ACK = "ok te escucho", ACK = "perfecto")
— no a nivel de sincronización de números de secuencia ni por qué eso habilita session
hijacking, que es lo que pide la Sesión 1.1 del roadmap nuevo. Las flags TCP (FIN/RST/PSH/URG,
más allá de SYN/ACK) y su uso ofensivo (SYN flood, RST injection, idle scan) no aparecen en tu
registro anterior.

Esto no es un juicio — es información para que sepas que si Claude pregunta sobre estos dos
puntos específicos y sentís que no los tenés, es esperable, no señal de que "no estudiaste
bien" antes. Ahí no uses "saltar" — mejor dejá que la sesión normal cubra esa parte.
