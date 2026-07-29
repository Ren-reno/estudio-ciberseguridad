# Roadmap Cloud Security — Formato de sesiones de 1 hora

**Cómo usar este documento:** cada fila de las tablas es UNA sesión de estudio (45-60 min). No se hace un módulo entero por día — se hace una fila. Cada sesión tiene un gancho de entrada (conecta con la anterior) y un gancho de salida (conecta con la siguiente), para que el conocimiento se arme como cadena y no como bloques sueltos.

**Los laboratorios avanzados de cada módulo NO se hacen sesión a sesión junto con la teoría.** Se hacen al final del módulo, ya con todas las piezas teóricas conectadas: primero se genera un enunciado fijo con plan de sub-sesiones (una sola vez), y después se ejecuta cada sub-sesión de 1h por separado. Ver la sección "Cómo se trabajan los labs" más abajo.

---

## Cómo empezar cada sesión (léelo una vez, después es automático)

**Cada sesión es una conversación NUEVA, no una continuación del chat anterior.** Esto es a propósito: si acumulás 20 sesiones en un mismo chat, cada vez pesa más contexto viejo que no aporta a la lección de hoy. El `progreso.md` del repo reemplaza esa memoria — es portable, funciona igual en Claude, ChatGPT, o cualquier otro LLM, y no depende de que la conversación siga viva ni de que el repo esté en una máquina en particular (con `git pull` lo tenés actualizado donde sea).

**Flujo de cada sesión:**
1. Abrí una conversación nueva.
2. No hace falta pegar nada de entrada — el prompt de abajo ya incluye la URL del repo, y le pide al LLM que la consulte solo si tiene herramientas para hacerlo (si no, te va a pedir que le pegues progreso.md).
3. Usá el prompt de abajo.
4. Al terminar, Claude te entrega un archivo `.patch` con formato de parche de email de Git (header `From:`/`Date:`/`Subject:` + el diff), listo para `git am`. Trae el nuevo `sesiones/sesion-N.N.md` ya escrito y la línea de `progreso.md` ya actualizada — no hace falta que copies ni edites nada a mano.
5. Aplicalo con 1 solo comando (aplica el diff Y crea el commit atribuido a vos en el mismo paso):
   ```bash
   git am sesion-N.N.patch
   ```

**Header de autoría fijo** que debe llevar todo patch generado, primeras líneas del archivo:
```
From: Ren-reno <reinaldo.codoceo@inacapmail.cl>
Date: [fecha del día]
Subject: [PATCH] sesion N.N: [tema breve]
```

Un commit por sesión, ya atribuido a vos, te da un historial real y verificable de tu propio avance. Lo único manual de acá en adelante es lo que solo vos podés escribir: tu resolución de ejercicios si querés guardarla aparte, y la bitácora de los labs (ver sección de labs más abajo).

**Si el patch falla al aplicar** (por ejemplo porque tu `progreso.md` real quedó distinto al que Claude asumió), `git am` te va a avisar del conflicto y te va a dejar en medio de un am a resolver — corré `git am --abort` para cancelar limpio, pegale a Claude tu `progreso.md` real, y te regenera el patch contra ese estado.

### Prompt de inicio de sesión

```
Mi repo de estudio está en: https://github.com/Ren-reno/estudio-ciberseguridad

Si tenés herramientas para acceder a internet (bash con git, web fetch, un conector de
GitHub, o similar), cloná o consultá ese repo vos mismo y leé roadmap.md y progreso.md
directamente desde ahí — no hace falta que te los pegue.

Si NO tenés forma de acceder a internet o repos, decime explícitamente "no puedo acceder
al repo, pegame progreso.md y la sección relevante de roadmap.md" y esperá a que te los
pase, en vez de inventar o asumir contenido que no tenés.

Mirá la fila "Próxima sesión a hacer" de progreso.md para saber en qué sesión voy,
y el roadmap para ver el contenido exacto de esa fila (columna "Contenido de la sesión").

Si progreso.md tiene, para el módulo de hoy, un diagnóstico concepto por concepto de una
sesión de verificación previa, leelo y usalo para calibrar: lo marcado como "sin cobertura
previa" hay que definirlo desde cero; lo marcado como impreciso hay que corregir
puntualmente, no repetir la clase completa.

Arrancá SIEMPRE por la versión más elemental posible, no la completa. No asumas vocabulario
técnico que no haya aparecido antes en mi progreso.md o en esta misma sesión — la primera
vez que uses un término nuevo, definilo en una frase simple antes de construir algo sobre
él. Subí la dificultad de a poco dentro de la sesión, no de entrada. Si notás que vas a
meter más de 2-3 conceptos nuevos seguidos, parate y preguntame si hace falta desglosarlo
más.

Vamos a hacer esa sesión. El contenido de HOY es únicamente lo que dice esa fila —
no el módulo completo, no lo que sigue después.

Formato obligatorio:
- 2 min: gancho conectando con la sesión anterior (mirá qué quedó anotado en progreso.md)
- 15-20 min: explicación de ESE concepto solo, sin desviarte a temas relacionados
- 20-25 min: un ejercicio chico y concreto sobre este concepto (NO el lab completo del módulo)
- 5 min: cierre explicando por qué esto conecta con lo que sigue

Si en el camino surge una idea relacionada pero fuera de esto, decime
"anotalo para después" y seguimos — no la desarrolles ahora aunque sea interesante.
Al final, generame un patch (.patch) en formato de parche de email de Git, con header:
From: Ren-reno <reinaldo.codoceo@inacapmail.cl>
Date: [fecha de hoy]
Subject: [PATCH] sesion N.N: [tema]

El patch debe incluir sesiones/sesion-[N.N].md (resumen de la sesión en markdown) y la
línea correspondiente actualizada en progreso.md. Quiero poder aplicarlo con git am
directamente, sin copiar texto a mano.

Esta sesión termina en 60 minutos reales, cronometrados.
```

## Cómo se trabajan los labs (enunciado fijo + sub-sesiones de 1h)

Los labs grandes de cada módulo (2-3 sesiones según el caso) se resuelven en dos pasos, no uno:

**Paso 1 — Una sola vez, al terminar la última sesión de teoría del módulo:** pedís el enunciado del lab más un plan de cómo se parte en sub-sesiones de 1h. Esto se guarda en `labs/modulo-N/enunciado.md` y **no se vuelve a tocar** — es la consigna fija.

```
Terminé toda la teoría del Módulo [X]. Dame el enunciado completo del lab de este módulo
(objetivo, entregable, criterio de éxito — igual de exigente que en el roadmap original,
sin recortar alcance) y un plan de cómo dividirlo en sub-sesiones de 60 min.

Para cada sub-sesión definí: qué parte puntual se resuelve hoy, y qué debe quedar
"cerrado" al final de esa hora (aunque el lab completo siga abierto).

No me des la solución de ninguna parte del lab, solo el enunciado y el plan de sub-sesiones.
Generame esto como patch en formato de parche de email de Git, con header:
From: Ren-reno <reinaldo.codoceo@inacapmail.cl>
Date: [fecha de hoy]
Subject: [PATCH] lab modulo N: enunciado

Debe incluir labs/modulo-[X]/enunciado.md, para aplicar con git am.
```

**Paso 2 — Al empezar cada sub-sesión del lab:** le pasás el enunciado fijo + la bitácora de avance (`labs/modulo-N/bitacora.md`, que vos actualizás al final de cada sub-sesión con qué lograste y dónde quedaste). Vos resolvés — Claude no te da la solución, solo puede confirmar si tu enfoque va bien o corregir si te trabás en algo puntual.

```
Te paso el enunciado del lab de Módulo [X] y mi bitácora de avance.
Hoy toca la sub-sesión [N] según el plan: [pegá qué corresponde a esa sub-sesión].

Yo resuelvo esto solo. Tu rol hoy es: confirmarme si mi enfoque va bien cuando te lo
cuente, o señalarme el error si me trabo — pero no me des la solución ni los pasos,
dejame llegar yo. Si me trabo más de 10-15 min en el mismo punto, ahí sí dame una pista
(no la respuesta completa).

Al final decime qué anotar en la bitácora: qué quedó resuelto, dónde quedé, qué sigue
en la próxima sub-sesión.

Esta sub-sesión termina en 60 minutos reales, cronometrados.
```

Esto mantiene los labs con la misma profundidad que tienen en el roadmap original (nada se recorta), pero cada sub-sesión individual sí respeta el límite de 1h con un cierre concreto — nunca es "una hora libre a ver hasta dónde llego".

**Antes de cualquier commit que incluya output de un lab (Fase 4-5 sobre todo):** revisá que no haya credenciales, IPs reales, ni nombres de host propios en lo que vas a subir. El `.gitignore` del repo ya excluye los formatos más obvios (`.pem`, `.tfstate`, capturas de tráfico), pero un output pegado a mano en un `.md` no lo filtra el `.gitignore` — eso lo revisás vos antes de commitear.

---

## Mecanismos de refuerzo (3 tipos de sesión extra)

Además de las sesiones normales de teoría y los labs, hay tres tipos de sesión que se insertan en puntos fijos de la secuencia. Resuelven algo que el gancho de entrada/salida no cubre: ese gancho solo conecta con la sesión inmediatamente anterior, no reactiva nada de varios módulos atrás. Sin esto, el contenido del Módulo 1 va a estar bastante olvidado para cuando llegues al Módulo 17.

Revisá la tabla de la última sección de este documento antes de cada sesión nueva para saber si hoy toca teoría normal, lab, o uno de estos tres.

### A) Repaso espaciado

Se hace después del lab de los Módulos 2, 6, 10, 14 y 18 — nunca sobre el módulo recién cerrado ni el anterior a ese (esos siguen frescos por el lab), sino sobre el par de módulos anterior a esos dos.

```
Vamos a hacer una Sesión de Repaso Espaciado del roadmap de Cloud Security, después de cerrar el Módulo [X].

Elegí vos 3-4 conceptos de los Módulos [módulos a repasar según la tabla] — sin decírmelos antes de preguntarlos.

Formato obligatorio (60 min):
- 30-35 min: preguntame los conceptos uno por uno. No des la respuesta ni pistas hasta que yo
  responda algo (aunque esté incompleto o mal) o me trabe más de 1 minuto. Recién ahí corregís y explicás.
- 15-20 min: para cada concepto que salió flojo, un mini-refuerzo — no una clase completa, solo
  la parte que falló.
- 5-10 min: cerrá con qué quedó firme y qué anotamos en preguntas pendientes para reforzar más adelante.

Al final generame un patch en formato de parche de email de Git (header From/Date/Subject
como en las demás sesiones, From: Ren-reno <reinaldo.codoceo@inacapmail.cl>) con
progreso.md actualizado: marcá este repaso como hecho en la
sección de mecanismos de refuerzo, y agregá a preguntas pendientes lo que haya quedado flojo.

No hay ejercicio nuevo ni gancho de salida — es pura recuperación. Termina en 60 minutos reales, cronometrados.
```

### B) Limpieza de preguntas pendientes

Se hace después del lab de los Módulos 4, 8, 12, 16 y 20. Es el único momento donde el archivo de "preguntas pendientes" de `progreso.md`/`notas/` se revisa y se cierra — sin esto, esa lista solo crece y no se resuelve nunca.

```
Vamos a hacer una Sesión de Limpieza de Preguntas Pendientes, después de cerrar el Módulo [X].

Te paso el contenido completo de mi archivo de preguntas pendientes: [pegar acá].

Formato obligatorio (60 min):
- 5-10 min: de toda la lista, elegimos juntos las 2-3 preguntas más relevantes para lo que viene
  (priorizá las que conecten con los próximos 2 módulos, si se puede identificar).
- 35-40 min: desarrollamos esas 2-3 preguntas con la misma profundidad que una sesión de teoría
  normal. No hace falta que estén relacionadas entre sí.
- 10 min: marcá como resueltas las que cerramos hoy, dejá el resto tal cual para la próxima limpieza.
  Si quedan más de 6-7 sin resolver, avisame — se están acumulando más rápido de lo que se cierran.

Al final generame un patch en formato de parche de email de Git (header From/Date/Subject,
From: Ren-reno <reinaldo.codoceo@inacapmail.cl>) con progreso.md actualizado: marcá esta limpieza como hecha, y
actualizá la lista de preguntas pendientes (quitando las resueltas, dejando el resto).
```

### C) Chequeo de bases (única vez, antes de Fase 5)

Se hace después del lab del Módulo 15 (cierre de Fase 4), antes de arrancar el Módulo 16. Es más que una sesión de repaso — es un gate real: si las bases de Fases 1-4 no están firmes, no tiene sentido entrar a AWS todavía.

```
Vamos a hacer un Chequeo de Bases antes de arrancar Fase 5 (Cloud Security AWS).

Hacéme 8-10 preguntas de aplicación (no de definición) que crucen conceptos de al menos 2 de las
Fases 1-4 en la misma pregunta. Ejemplo del tipo que buscamos: "¿por qué un Security Group en AWS
va a ser stateful, si ya sé que TCP lo es y UDP no?" — no "¿qué es un Security Group?".

Formato (60 min):
- 45 min: las 8-10 preguntas, una por una, mismo criterio que en el repaso espaciado (no des la
  respuesta hasta que yo responda o me trabe).
- 15 min: contamos cuántas salieron bien.

Regla de corte:
- 7 o más de 10 bien → seguimos directo al Módulo 16.
- Menos de 7 → no arrancamos Fase 5 todavía. Identificamos qué fase específica (1, 2, 3 o 4) quedó
  floja y planificamos 1-2 sesiones de refuerzo antes de tocar AWS. Esto no es un fracaso — es
  exactamente para esto que existe el chequeo: mejor encontrarlo acá que a mitad del Módulo 17.

Al final generame un patch en formato de parche de email de Git (header From/Date/Subject,
From: Ren-reno <reinaldo.codoceo@inacapmail.cl>) con progreso.md actualizado: marcá el chequeo como hecho con el
resultado (X/10), y si el corte dio negativo, agregá a preguntas pendientes qué fase reforzar.
```

### C.1) Chequeo de bases — variante temprana (Módulos 1-4, previo a arrancar el roadmap)

Se usa cuando ya existe avance previo real en las bases (Módulos 1-4) hecho fuera de este
sistema, para evitar repetir de cero lo que ya está sólido sin arriesgarse a saltar sobre un
hueco no detectado. Mismo mecanismo que C, aplicado antes de la Sesión 1.1 en vez de antes
de Fase 5.

```
Vamos a hacer un Chequeo de Bases sobre Módulos 1-4 (TCP/IP, Subnetting/routing, DNS/HTTP,
Linux) antes de arrancar el roadmap. Tengo avance previo real en estos temas, documentado en
progreso.md (sección "Avance previo").

Hacéme 8-10 preguntas de aplicación (no de definición) que crucen conceptos de al menos 2 de
estos 4 módulos en la misma pregunta. Ejemplo del tipo que buscamos: "¿por qué ARP necesita
broadcast si ya existe una tabla de routing basada en IP?" — no "¿qué es ARP?".

Formato (60 min):
- 45 min: las 8-10 preguntas, una por una. No des la respuesta ni pistas hasta que yo responda
  algo (aunque esté incompleto o mal) o me trabe más de 1 minuto. Recién ahí corregís y explicás.
- 15 min: contamos cuántas salieron bien.

Regla de corte:
- 7 o más de 10 bien → saltamos directo a Módulo 5, marcando Módulos 1-4 como completados.
- Menos de 7 → identificamos qué módulo(s) específicos (no los 4 completos) quedaron flojos,
  y planificamos 1-2 sesiones de refuerzo solo en esos antes de Módulo 5.

Al final generame un patch en formato de parche de email de Git (header From/Date/Subject,
From: Ren-reno <reinaldo.codoceo@inacapmail.cl>) con progreso.md actualizado: marcá este
chequeo como hecho con el resultado (X/10), actualizá "Próxima sesión a hacer" según el
resultado, y si corresponde marcá Módulos 1-4 como completados en la sección correspondiente.
```

### C.2) Repaso de verificación Módulos 1-4 (una vez, después de C.1 si el resultado dio bajo)

4 sesiones, una por módulo, más cortas que una sesión de teoría normal — verifican si el
avance previo real está firme en cada módulo específico, sin repetir la teoría completa.
Reemplaza el chequeo cruzado de C.1 cuando ese resultado no fue suficiente para decidir con
confianza qué saltar.

**Instrucción especial "saltar", válida SOLO en estas 4 sesiones (1.rev a 4.rev):** si en
cualquier momento el usuario escribe "saltar", Claude no debe autorellenar el resultado
como dominado sin verificar. En su lugar hace 1 sola pregunta corta (2-3 min) sobre el
concepto de esa sesión. Si se responde bien, ahí sí autorellena resumen/bitácora/progreso y
se avanza. Si se responde mal o con duda, se sigue con el formato normal de la sesión — el
"saltar" no debe usarse para maquillar un hueco real, solo para ahorrar trámite cuando algo
ya está firme. Esta instrucción NO aplica a ninguna sesión fuera de este bloque de 4.

```
Vamos a hacer la sesión de Repaso de Verificación [N].rev, Módulo [X] — [nombre del módulo].

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
este repaso, y si el módulo completo quedó firme, marcalo como completado.
```

---

# FASE 1 — Infraestructura base

## MÓDULO 1 — TCP/IP a nivel de ingeniería

| # | Contenido de la sesión | Gancho de salida |
|---|---|---|
| 1.1 | Three-way handshake: por qué sincroniza números de secuencia, no es solo un saludo | ¿Qué pasa si alguien predice esos números? |
| 1.2 | Session hijacking por predicción de secuencia + anatomía de un segmento TCP: flags SYN/ACK/FIN/RST/PSH/URG | Cada flag se puede usar mal — ¿cómo? |
| 1.3 | Weaponización de flags: SYN flood, RST injection, idle scan con Nmap | ¿Por qué UDP no tiene nada de esto? |
| 1.4 | TCP stateful vs UDP stateless, y por qué esto importa en firewalls | Los sistemas se pueden identificar por cómo responden... |
| 1.5 | IP TTL como fingerprinting de sistemas operativos + fragmentación como evasión de IDS | Ya tenés toda la teoría — ahora se construye |

**Detalle por sesión (objetivo, prerrequisitos, conceptos nuevos) — plantilla nueva, se aplica de acá en adelante a medida que se arman los módulos siguientes:**

- **1.1** — *Objetivo:* explicar en tus palabras por qué el three-way handshake sincroniza números de secuencia y no es solo un saludo de conexión. *Prerrequisitos:* ninguno formal (primera sesión del módulo) — pero la verificación de julio 2026 mostró que el handshake se conocía solo de nombre, sin el mecanismo; arrancar resumiéndolo en 2-3 líneas antes de construir sobre él. *Conceptos nuevos:* three-way handshake, número de secuencia (ISN), sincronización de estado en TCP.
- **1.2** — *Objetivo:* explicar qué es la predicción de ISN y qué hace cada flag (SYN/ACK/FIN/RST/PSH/URG) de un segmento TCP. *Prerrequisitos:* handshake y número de secuencia (1.1). La verificación dio 0/3 en session hijacking — no dar por sabida la distinción on-path/off-path, definirla explícitamente. *Conceptos nuevos:* predicción de ISN, hijacking on-path vs off-path, flags TCP.
- **1.3** — *Objetivo:* explicar el mecanismo real de un SYN flood (no solo "satura la red") y qué hacen RST injection e idle scan. *Prerrequisitos:* flags TCP y su función normal (1.2). La verificación mostró el SYN flood explicado como "agota la red" en vez de "agota el backlog de conexiones semiabiertas" — corregir esa imprecisión de forma explícita, no repetirla. *Conceptos nuevos:* SYN flood (backlog de conexiones semiabiertas), RST injection, idle scan.
- **1.4** — *Objetivo:* explicar por qué un firewall trata TCP y UDP distinto, y qué implica para las reglas que se escriben. *Prerrequisitos:* flags y comportamiento de conexión de TCP (1.1-1.3). *Conceptos nuevos:* TCP stateful, UDP stateless, tabla de estados de un firewall.
- **1.5** — *Objetivo:* explicar cómo el TTL de un paquete IP identifica el sistema operativo de origen, y cómo la fragmentación evade un IDS. *Prerrequisitos:* conceptos básicos de IP; si "IDS" no se definió antes, definirlo en una frase antes de hablar de evadirlo. *Conceptos nuevos:* TTL como fingerprint de SO, fragmentación IP como evasión de IDS.

**Lab del módulo (2-3 sesiones aparte):** scanner de puertos con raw sockets en Python, sin librerías de alto nivel, comparado en paralelo con Wireshark sobre una VM local.

---

## MÓDULO 2 — Subnetting, routing y arquitectura de redes

| # | Contenido de la sesión | Gancho de salida |
|---|---|---|
| 2.1 | Por qué CIDR reemplazó a classful y qué implica para segmentación de redes | ¿Cómo sabe un router a dónde mandar cada paquete? |
| 2.2 | Tabla de routing y longest prefix match | Con esto ya podés diseñar subredes reales |
| 2.3 | VLSM y diseño de subnetting para una red corporativa | El diseño no alcanza si no está aislado — ¿qué lo aísla? |
| 2.4 | NAT como mecanismo de seguridad accidental y sus límites + VLANs (segmentación lógica vs física) | Hay un protocolo viejo que no tiene ninguna autenticación... |
| 2.5 | ARP en profundidad: sin autenticación, y por qué eso es catastrófico en redes planas | ¿Qué puede hacer un atacante en tu mismo segmento /24? |
| 2.6 | Cómo un atacante en tu segmento puede redireccionar tráfico sin que lo notes | Ya tenés la arquitectura completa — ahora se implementa |

**Lab del módulo (2-3 sesiones aparte):** diseño de arquitectura de 3 zonas (DMZ, red interna, servidores críticos) con cálculo de bloques CIDR y réplica con iptables.

---

## MÓDULO 3 — DNS a nivel forense y HTTP/S en profundidad

| # | Contenido de la sesión | Gancho de salida |
|---|---|---|
| 3.1 | Jerarquía DNS completa: del root al authoritative server, qué pasa en cada salto | Los registros DNS filtran más de lo que parece |
| 3.2 | Registros con implicación de seguridad no obvia: SPF mal configurado (email spoofing), TXT records | Hay un tipo de registro que, si lo abandonás, te pueden robar el subdominio |
| 3.3 | CNAME abandonado → subdomain takeover | ¿Cómo se previene el cache poisoning de raíz? |
| 3.4 | DNSSEC: firmas criptográficas contra cache poisoning, y por qué solo ~30% de dominios lo usa | DNS no es el único protocolo que evolucionó — HTTP también |
| 3.5 | HTTP/2 y HTTP/3 (QUIC): multiplexación y las superficies de ataque que introduce | Hasta los CDNs modernos tienen su propia versión del cache poisoning |
| 3.6 | Cache poisoning en CDNs (Cloudflare) vs DNS clásico | Ya tenés todo para reconstruir infraestructura ajena sin tocarla |

**Lab del módulo (1-2 sesiones aparte):** OSINT completo sobre un dominio usando solo dig, dnsx, subfinder — reconstruir infraestructura sin visitar el sitio.

---

## MÓDULO 4 — Linux como sistema administrable

| # | Contenido de la sesión | Gancho de salida |
|---|---|---|
| 4.1 | Filesystem hierarchy standard desde la perspectiva de un atacante post-explotación: `/etc/shadow`, `/etc/sudoers` | `/proc` y `/var/log` guardan más de lo que pensás |
| 4.2 | `/proc` y `/var/log` como fuentes de información crítica | Un servicio puede sobrevivir un reinicio del sistema — ¿cómo? |
| 4.3 | Systemd y su implicación en persistencia de malware | Los permisos de Linux no son solo rwx |
| 4.4 | Modelo de capabilities (`CAP_NET_RAW`, `CAP_SYS_ADMIN`) como alternativa a setuid | Hay un vector de persistencia clásico y muy simple |
| 4.5 | Crontabs como vector de persistencia | El acceso remoto es la puerta más común — hay que blindarla |
| 4.6 | SSH hardening: `sshd_config`, clave pública vs contraseña, por qué fail2ban solo no alcanza | Ya tenés todo para auditar un sistema real |

**Lab del módulo (2-3 sesiones aparte):** auditoría completa de una VM mal configurada — identificar 8+ misconfiguraciones, documentar vector de explotación de cada una, script Bash idempotente que corrija todo.

---

# FASE 2 — Seguridad de infraestructura clásica
*Prerequisito: labs de Fase 1 entregados.*

## MÓDULO 5 — Criptografía aplicada a la seguridad

| # | Contenido de la sesión | Gancho de salida |
|---|---|---|
| 5.1 | Por qué MD5 y SHA-1 están rotos: qué es una colisión criptográfica en términos reales | Hay dos formas de cifrar, y TLS usa las dos juntas |
| 5.2 | Simétrica (AES-256) vs asimétrica (RSA/ECDSA): por qué se combinan en TLS | El problema es cómo compartir la clave sin que nadie la vea |
| 5.3 | El problema del intercambio de claves y cómo Diffie-Hellman lo resuelve | La NSA archivó tráfico cifrado esperando una clave que nunca sirvió — ¿por qué? |
| 5.4 | Perfect Forward Secrecy: por qué inutiliza el tráfico archivado | Un certificado no es solo un candado, es una cadena de confianza |
| 5.5 | Certificados X.509: estructura, CA chain of trust, Certificate Transparency logs | Hay ataques que no rompen el cifrado, rompen la versión |
| 5.6 | Ataques de downgrade (POODLE, BEAST, LOGJAM) y su mitigación | Ya tenés la teoría — ahora se configura un servidor real, mal y bien |

**Lab del módulo (1-2 sesiones aparte):** Nginx con TLS inseguro → auditoría con testssl.sh/sslyze con CVEs → configuración correcta → demostración con Wireshark de que el downgrade ya no funciona.

---

## MÓDULO 6 — OWASP Top 10 con explotación real

| # | Contenido de la sesión | Gancho de salida |
|---|---|---|
| 6.1 | Por qué las inyecciones (SQLi, Command Injection, XSS) siguen siendo el vector más prevalente: confusión entre datos y código | El control de acceso roto subió al primer lugar del ranking — ¿por qué? |
| 6.2 | Broken Access Control: por qué es hoy la vulnerabilidad #1 | En la nube hay una vulnerabilidad que vale más que todas las demás juntas |
| 6.3 | SSRF: cómo llegar al endpoint de metadatos de EC2 (169.254.169.254) y robar credenciales IAM completas | Deserializar datos ajenos puede ser tan peligroso como ejecutar su código |
| 6.4 | Insecure Deserialization como RCE casi garantizado | Una sola categoría explica el 80% de los compromisos reales |
| 6.5 | Security Misconfiguration: por qué es la causa raíz más común | Ya tenés la teoría de 5 vectores — ahora se explotan de verdad |

**Lab del módulo (2 sesiones aparte):** DVWA o WebGoat en Docker, pentest de caja negra, explotar 5+ vulnerabilidades del Top 10, documentar payload + causa raíz + mitigación en código + impacto de negocio en informe ejecutivo.

---

## MÓDULO 7 — Linux hardening y threat hunting manual

| # | Contenido de la sesión | Gancho de salida |
|---|---|---|
| 7.1 | Defensa en profundidad: cada capa (filesystem, red, proceso, usuario) debe fallar de forma independiente | Hay un mecanismo de control obligatorio que va más allá de los permisos normales |
| 7.2 | AppArmor vs SELinux: Mandatory Access Control como última línea contra escalación de privilegios | Cuando alguien ya está adentro, los logs cuentan la historia |
| 7.3 | Análisis forense de logs: qué buscar en `/var/log/auth.log`, `/var/log/syslog`, journald | Hay señales de compromiso que no están en ningún log |
| 7.4 | Indicadores de compromiso: SUID inesperados, crontabs ocultos, fileless malware, conexiones no reconocidas | Se puede auditar cada llamada al sistema, literalmente |
| 7.5 | `auditd` como sistema de monitoreo de syscalls | Ya tenés todo para reconstruir un ataque desde cero, sin saber qué pasó |

**Lab del módulo (2-3 sesiones aparte):** VM comprometida hace 72h, sin contexto previo — reconstruir línea temporal completa del ataque solo con logs y análisis forense. Informe con evidencia numerada.

---

## MÓDULO 8 — Firewalls, IDS/IPS y análisis de tráfico avanzado

| # | Contenido de la sesión | Gancho de salida |
|---|---|---|
| 8.1 | Packet filter vs stateful inspection vs NGFW: diferencia arquitectural | Un firewall perimetral no te salva si el atacante ya está adentro |
| 8.2 | Por qué el perímetro no protege contra movimiento lateral en red plana | El orden de las reglas de un firewall puede crear un agujero sin que lo notes |
| 8.3 | iptables/nftables: cadenas INPUT/OUTPUT/FORWARD y por qué el orden importa | Hay dos formas de detectar intrusos, y los atacantes conocen una de ellas |
| 8.4 | Snort/Suricata: firmas vs anomalías, y por qué los atacantes estudian las firmas públicas | Wireshark entre miles de paquetes necesita filtros quirúrgicos |
| 8.5 | Wireshark en modo forense: filtros de display avanzados para aislar comportamiento malicioso | Ya tenés todo para cazar un ataque real en una captura |

**Lab del módulo (2 sesiones aparte):** analizar un PCAP con ataque real, escribir firma Snort/Suricata que lo detecte, implementar regla iptables que lo hubiera bloqueado.

---

# FASE 3 — Aplicaciones web y APIs
*La capa donde vive el 90% de las vulnerabilidades en producción real.*
*Prerequisito: labs de Fase 2 entregados.*

## MÓDULO 9 — HTTP avanzado, APIs REST y seguridad de APIs

| # | Contenido de la sesión | Gancho de salida |
|---|---|---|
| 9.1 | HTTP como protocolo stateless: cómo cookies, tokens y sesiones construyen estado sobre él | Hay un flujo de autorización con ataques específicos en cada paso |
| 9.2 | OAuth 2.0 y OpenID Connect: el flujo completo | Open redirect, CSRF y token leakage atacan pasos distintos del mismo flujo |
| 9.3 | Ataques específicos a OAuth: open redirect, CSRF en authorization endpoint, token leakage vía Referer | Las APIs modernas tienen su propio Top 10, y no es el mismo que el web |
| 9.4 | OWASP API Security Top 10 2023, foco en BOLA/IDOR como el más prevalente | Hay un peligro en dejar que el cliente mande cualquier campo |
| 9.5 | Mass assignment: los peligros del binding automático de parámetros | GraphQL tiene una función que es un mapa completo del sistema, gratis |
| 9.6 | GraphQL introspection como herramienta de reconnaissance | Ya tenés la teoría — ahora auditás una API real |

**Lab del módulo (2 sesiones aparte):** OWASP crAPI/dvAPI en Docker, rol de security reviewer de API bancaria — encontrar IDOR + broken authentication + mass assignment, con PoC, impacto y corrección en pseudocódigo para cada uno.

---

## MÓDULO 10 — Autenticación, sesiones y gestión de identidad

| # | Contenido de la sesión | Gancho de salida |
|---|---|---|
| 10.1 | Por qué las contraseñas están fundamentalmente rotas, y cómo bcrypt/Argon2 mitigan fuerza bruta offline | Hay un token que se puede modificar y el servidor a veces le cree |
| 10.2 | JWT: estructura completa (header.payload.signature) | El ataque más simple a JWT es decirle al servidor "no verifiques nada" |
| 10.3 | Ataque `alg:none` y confusión RS256/HS256 | JWT sirve para probar identidad, no siempre para decidir permisos — la diferencia importa |
| 10.4 | Diferencia entre JWT para autenticación vs autorización | Las sesiones también se pueden secuestrar sin tocar la contraseña |
| 10.5 | Session fixation, session riding (CSRF), impacto de cookies sin HttpOnly/Secure/SameSite | Un código de 6 dígitos por SMS es más débil de lo que parece |
| 10.6 | MFA: por qué TOTP > SMS OTP, y cómo se ataca vía SIM swapping / SS7 + intro a FIDO2/WebAuthn | Ya tenés todo para atacar y defender JWT en un entorno real |

**Lab del módulo (1-2 sesiones aparte):** Burp Suite Community — decodificar JWT, intentar `alg:none`, falsificar rol admin modificando payload, documentar qué funcionó y por qué, luego configurar validación correcta en servidor.

---

## MÓDULO 11 — Python para seguridad ofensiva y defensiva

| # | Contenido de la sesión | Gancho de salida |
|---|---|---|
| 11.1 | Por qué Python domina en seguridad: librerías de red de bajo nivel, scripting rápido, uso en herramientas ofensivas reales | Hay una librería que te deja construir paquetes desde cero, byte a byte |
| 11.2 | Scapy: construcción de paquetes arbitrarios (la misma técnica de hping3) | Interactuar con APIs a mano no escala — hay que automatizarlo |
| 11.3 | Requests para interacción con APIs y automatización de fuzzing | Los logs esconden IOCs si sabés qué patrón buscar |
| 11.4 | Parsing de logs con regex y extracción de IOCs | El hardening también se puede automatizar, no solo el ataque |
| 11.5 | Subprocess y os para automatización de hardening | Ya tenés todas las piezas — ahora se arma una herramienta completa |

**Lab del módulo (2 sesiones aparte):** herramienta de auditoría desde cero — DNS + enumeración de subdominios, port scan con banner grabbing, verificación de headers de seguridad HTTP, reporte JSON clasificado por severidad. Código modular y documentado.

---

# FASE 4 — DevOps/SecOps e Infraestructura como Código
*El contexto donde va a vivir tu seguridad cloud.*
*Prerequisito: labs de Fase 3 entregados.*

## MÓDULO 12 — Docker y seguridad de contenedores

| # | Contenido de la sesión | Gancho de salida |
|---|---|---|
| 12.1 | Por qué los contenedores no son VMs: el kernel compartido y qué implica en el modelo de amenazas | Namespaces y cgroups aíslan, pero tienen límites |
| 12.2 | Namespaces y cgroups como mecanismo de aislamiento, y sus límites | Las imágenes a veces cargan secretos que nadie quiso publicar |
| 12.3 | Análisis de imágenes para secretos embebidos (hardcoded credentials, private keys) | Hay un archivo que, si lo tocás, equivale a ser root del host |
| 12.4 | Docker socket (`/var/run/docker.sock`) como vector de escalación de privilegios | `--privileged` no es un flag inocente |
| 12.5 | Container escape: `--privileged`, host mounts peligrosos, capabilities no restringidas | Ya tenés todo para escanear y endurecer imágenes reales |

**Lab del módulo (1-2 sesiones aparte):** 3 imágenes vulnerables — escanear con Trivy (CVEs críticas), buscar secretos con `dive`, construir versión hardened con mínimo privilegio, demostrar que un escape que antes funcionaba ya no funciona.

---

## MÓDULO 13 — CI/CD seguro, Git y gestión de secretos

| # | Contenido de la sesión | Gancho de salida |
|---|---|---|
| 13.1 | El pipeline CI/CD como superficie de ataque de alto valor: compromiso de pipeline = compromiso de producción | El ataque a SolarWinds se puede replicar en GitHub Actions — ¿cómo? |
| 13.2 | Supply chain attacks: el caso SolarWinds aplicado a GitHub Actions | `git rm` no borra nada del historial real |
| 13.3 | Git history como vector de filtración de secretos | Los repos públicos filtran credenciales de nube todo el tiempo, sin que nadie lo note al toque |
| 13.4 | Secret scanning: por qué tokens de GitHub, AWS keys y certificates aparecen constantemente en repos públicos | El análisis estático puede atrapar la vulnerabilidad antes de que exista en producción |
| 13.5 | SAST integrado en pipelines + signing de commits con GPG | Ya tenés todo para armar un pipeline seguro de punta a punta |

**Lab del módulo (2 sesiones aparte):** pipeline GitHub Actions completo — secret scanning (truffleHog/git-secrets), SAST con Semgrep, Dependabot, build+push de imagen Docker. Más: repo con 5 vulnerabilidades intencionales en el pipeline para identificar y corregir.

---

## MÓDULO 14 — Terraform e Infraestructura como Código segura

| # | Contenido de la sesión | Gancho de salida |
|---|---|---|
| 14.1 | Por qué IaC es imprescindible para seguridad cloud: reproducibilidad, auditabilidad, detección de drift | El archivo que guarda el estado de tu infraestructura puede filtrar secretos en texto plano |
| 14.2 | Terraform state como vector de ataque | Hay tres misconfiguraciones que aparecen en casi todos los incidentes cloud reales |
| 14.3 | Misconfiguraciones comunes: S3 buckets públicos, security groups 0.0.0.0/0, roles IAM con wildcard | El análisis estático de IaC atrapa esto antes de aplicar el código |
| 14.4 | tfsec y Checkov para análisis estático de configuraciones IaC | El estado remoto también necesita su propio candado |
| 14.5 | Remote state con S3 + DynamoDB para locking: el modelo correcto | Ya tenés todo para escribir infraestructura segura de punta a punta |

**Lab del módulo (2-3 sesiones aparte):** Terraform completo en AWS/LocalStack — VPC con subnets públicas/privadas, security groups segmentados, EC2 privado, ALB público, IAM de mínimo privilegio. Debe pasar tfsec sin críticos. Después: versión con misconfiguraciones para detectar a mano antes de correr tfsec.

---

## MÓDULO 15 — Kubernetes y seguridad de orquestación

| # | Contenido de la sesión | Gancho de salida |
|---|---|---|
| 15.1 | Arquitectura de Kubernetes desde la perspectiva del atacante: API server, RBAC, etcd | Cada pod trae un token montado automáticamente — y eso es un problema |
| 15.2 | Service accounts: por qué el token automático en cada pod es un vector de privilege escalation | Por defecto, todo pod puede hablar con todo pod |
| 15.3 | Network policies: por qué el default viola el mínimo privilegio | Un contenedor puede tener flags que lo dejan escapar del aislamiento |
| 15.4 | Security contexts: runAsNonRoot, readOnlyRootFilesystem, allowPrivilegeEscalation | Ya tenés todo para explotar y luego blindar un cluster real |

**Lab del módulo (2-3 sesiones aparte):** cluster local (kind/minikube) con RCE en una app desplegada — desde el container comprometido, explorar hasta dónde se puede llegar (token de service account, API de K8s, otros namespaces). Después: aplicar RBAC + network policies + securityContext y repetir demostrando que cada vector está bloqueado.

---

# FASE 5 — Cloud Security (AWS)
*El destino. Llegás acá con bases sólidas o llegás sin entender nada — por eso el Chequeo de Bases (sección "Mecanismos de refuerzo" al inicio de este documento) antes de arrancar el Módulo 16.*

## MÓDULO 16 — AWS: arquitectura y modelo de seguridad compartida

| # | Contenido de la sesión | Gancho de salida |
|---|---|---|
| 16.1 | Shared responsibility model con precisión técnica: dónde está la frontera real en EC2, Lambda, RDS, S3 | Una sola cuenta no alcanza para gobernar una organización entera |
| 16.2 | AWS Organizations, SCPs y Control Tower como arquitectura de gobierno multi-cuenta | Cada recurso de AWS tiene una identidad única, y las políticas se basan en eso |
| 16.3 | Modelo de recursos: ARN, políticas basadas en identidad vs recurso, condiciones | Hay un servicio que audita literalmente cada llamada a la API, en todas las regiones |
| 16.4 | CloudTrail como sistema de auditoría, y por qué importa en regiones que ni usás | La configuración también se puede vigilar en tiempo real, no solo las acciones |
| 16.5 | AWS Config para detección de misconfiguraciones en tiempo real + Security Hub como centralizador | Ya tenés todo para levantar una cuenta con el baseline correcto |

**Lab del módulo (1-2 sesiones aparte):** cuenta AWS free tier desde cero — MFA en root y usuario IAM, usuario de mínimo privilegio (no root), CloudTrail multi-región, billing alarm, AWS Config con reglas básicas. Documentar cada decisión con su justificación.

---

## MÓDULO 17 — IAM en profundidad y privilege escalation en AWS

| # | Contenido de la sesión | Gancho de salida |
|---|---|---|
| 17.1 | Anatomía completa de una política IAM: Effect, Action, Resource, Condition, y los wildcards peligrosos | El orden de evaluación de Allow/Deny no es intuitivo, y las SCPs le ganan a todo |
| 17.2 | Modelo de evaluación de políticas de AWS: orden de Allow/Deny, precedencia de SCPs | Hay una combinación de dos permisos aparentemente inocentes que te da control total |
| 17.3 | Privilege escalation en AWS: `iam:PassRole` + `ec2:RunInstances` como vector clásico | Otras dos técnicas documentadas hacen lo mismo por caminos distintos |
| 17.4 | Más vectores: `iam:CreatePolicyVersion`, `lambda:InvokeFunction` sobre funciones con rol privilegiado | Las credenciales no siempre están donde uno espera buscarlas |
| 17.5 | Credential exposure: metadata service de EC2 (IMDSv1 vs IMDSv2), env vars en Lambda, SSM Parameter Store | Ya tenés todo para mapear rutas de escalación reales |

**Lab del módulo (2 sesiones aparte):** usuario con política deliberadamente mal configurada — mapear privilege escalation paths con Pacu o AWS CLI manual, demostrar al menos 2 rutas hacia AdministratorAccess, luego diseñar la política de mínimo privilegio que las elimine sin romper funcionalidad legítima.

---

## MÓDULO 18 — VPC, networking cloud y seguridad perimetral en AWS

| # | Contenido de la sesión | Gancho de salida |
|---|---|---|
| 18.1 | VPC como red definida por software: cómo CIDR/routing/segmentación de Fase 1 se aplican acá con abstracción | Hay dos tipos de firewall en AWS y se comportan distinto |
| 18.2 | Security Groups (stateful, nivel instancia) vs NACLs (stateless, nivel subnet) | Cada conexión que entra o sale queda registrada, si lo activás |
| 18.3 | VPC Flow Logs: formato completo, uso para detectar reconnaissance y exfiltración | Conectar redes entre sí trae sus propios riesgos de "de más" |
| 18.4 | VPC Peering y Transit Gateway: los riesgos de conectividad transitiva + PrivateLink como modelo correcto | El endpoint de metadatos vuelve a aparecer, ahora en el contexto de red |
| 18.5 | SSRF hacia el metadata service de EC2 como el vector más crítico en cloud | Ya tenés todo para desplegar y verificar una arquitectura segmentada real |

**Lab del módulo (2 sesiones aparte):** VPC de 3 tiers con Terraform (pública+ALB, privada+EC2, aislada+RDS), security groups de mínimo privilegio, demostrar con AWS CLI que comprometer el ALB no da acceso directo a RDS, VPC Flow Logs como evidencia.

---

## MÓDULO 19 — Explotación de misconfiguraciones cloud reales

| # | Contenido de la sesión | Gancho de salida |
|---|---|---|
| 19.1 | Errores más frecuentes en producción real: S3 públicos, Lambda con secretos en env vars, RDS público, SGs 0.0.0.0/0 en SSH/RDP | El caso Capital One 2019 es el ejemplo de manual de esto |
| 19.2 | Análisis del caso Capital One 2019: SSRF + S3 público = brecha masiva | Un ataque cloud sigue una secuencia predecible de pasos |
| 19.3 | La kill chain en un ataque cloud: recon OSINT → credential discovery → initial access → priv esc → persistence → exfiltración | Hay herramientas hechas específicamente para automatizar esta cadena |
| 19.4 | Arsenal ofensivo cloud: Pacu (explotación AWS), ScoutSuite (auditoría), Prowler (compliance) | Ya tenés toda la teoría — ahora se ejecuta la kill chain completa |

**Lab del módulo (2-3 sesiones aparte):** CloudGoat o flaws.cloud — desde una clave IAM expuesta con permisos limitados, completar la kill chain hasta exfiltrar datos de un S3 privado. Cada paso documentado con comando exacto, respuesta de la API, y qué debería haber detectado un Blue Team en CloudTrail.

---

## MÓDULO 20 — Detección, respuesta a incidentes y SecOps cloud

| # | Contenido de la sesión | Gancho de salida |
|---|---|---|
| 20.1 | Por qué los IOCs tradicionales (hashes, IPs) valen menos que los IOBs (Indicators of Behavior) en infraestructura efímera | Hay un IDS nativo de AWS que analiza tres fuentes distintas a la vez |
| 20.2 | GuardDuty: tipos de findings, cómo funciona internamente (VPC Flow Logs + CloudTrail + DNS) | Correlacionar findings de varios servicios necesita un lugar central |
| 20.3 | Security Hub para correlación de findings | La respuesta a incidentes en cloud tiene las mismas 5 fases, pero se ven distinto |
| 20.4 | Incident response: las 5 fases clásicas aplicadas a cloud, diferencias con IR tradicional | Se puede investigar sin apagar nada, incluso la memoria |
| 20.5 | Forensics en cloud: adquisición de evidencia sin apagar la instancia, snapshots EBS | Ya tenés todo para investigar 72 horas de ataque solo con logs |

**Lab del módulo (2-3 sesiones aparte, cierre del programa):** CloudTrail logs (JSON) de un ataque de 72h — queries en Athena/jq para identificar primer acceso, reconstruir secuencia completa, determinar recursos/datos comprometidos, escribir reglas de detección (EventBridge/GuardDuty custom). Informe de IR completo como entregable final.

---

## Dónde se insertan los mecanismos de refuerzo

| Después del lab de... | Sesión nueva | Antes de arrancar... |
|---|---|---|
| Módulo 2 | Repaso espaciado (Módulo 1) | Módulo 3 |
| Módulo 4 | Limpieza de preguntas pendientes | Módulo 5 |
| Módulo 6 | Repaso espaciado (Módulos 3-4) | Módulo 7 |
| Módulo 8 | Limpieza de preguntas pendientes | Módulo 9 |
| Módulo 10 | Repaso espaciado (Módulos 7-8) | Módulo 11 |
| Módulo 12 | Limpieza de preguntas pendientes | Módulo 13 |
| Módulo 14 | Repaso espaciado (Módulos 11-12) | Módulo 15 |
| Módulo 15 | Chequeo de bases Fase 4→5 | Módulo 16 |
| Módulo 16 | Limpieza de preguntas pendientes | Módulo 17 |
| Módulo 18 | Repaso espaciado (Módulos 15-16) | Módulo 19 |
| Módulo 20 | Limpieza de preguntas pendientes (cierre) | Fin del programa |

Los números de esta tabla (cada 4 módulos, 2 conceptos por módulo repasado, umbral de 7/10 en el chequeo de bases) son un punto de partida razonable, no una regla fija. Si en la práctica el repaso queda corto o sobra tiempo, ajustalos — lo único que importa es que el mecanismo exista y se use, no el número exacto.

## Recordatorio de uso

- **1 sesión = 1 fila de la tabla.** No avances de fila sin cronómetro puesto.
- **Cada sesión, conversación nueva** — el `progreso.md` es tu memoria portable, no el historial del chat.
- **El lab del módulo es aparte**, y solo cuando terminaste todas las filas de teoría de ese módulo.
- Si en medio de una sesión te surge una pregunta interesante fuera de la fila de hoy: va a la sección de "preguntas pendientes" de `progreso.md`, y seguís. Esas preguntas son material para sesiones futuras, no para expandir la de hoy — y sí tienen un momento asignado para cerrarse (ver tabla de arriba).
- Total estimado: ~95 sesiones de teoría + ~40-50 de laboratorio + 11 sesiones de refuerzo (5 repasos, 5 limpiezas, 1 chequeo de bases) = ~146-156 sesiones de ~1h. A 1h/día, esto es un programa de varios meses — y eso está bien, porque es sostenible.
