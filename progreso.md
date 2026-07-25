# Progreso — Roadmap Cloud Security

**Última sesión completada:** 1.1 — Three-way handshake (Módulo 1) — 2026-08-04
**Próxima sesión a hacer:** 1.2 (Módulo 1 — ver orden de refuerzo abajo).

Con el cierre del bloque de 4 repasos de verificación (1.rev-4.rev), ningún módulo quedó
firme — los 4 requieren refuerzo puntual antes de seguir con el roadmap normal (Módulo 5 en
adelante). Orden de ataque, del más al menos fundacional (para que ninguna sesión nueva
tenga que adivinarlo ni elegir por inercia):

1. **Módulo 1** (sesiones 1.1-1.3) — el más fundacional; los huecos de Módulos 2-4 se apoyan
   en estos conceptos.
2. **Módulo 2** (sesiones 2.2, 2.5-2.6)
3. **Módulo 3** (sesiones 3.2, 3.5-3.6)
4. **Módulo 4 completo** (sesiones 4.1-4.6, por decisión del usuario dado el resultado 0/3 —
   ver detalle en checklist abajo)

---

## Avance previo (antes de este roadmap) — Días 1-13, mayo-junio 2026

Antes de este sistema hubo ~13 días de estudio con contenido real cubierto, documentado en
`0x1_Cibersecurity.7z`. Mapeo aproximado a los módulos de este roadmap:

- **Módulo 1 (TCP/IP):** Días 1, 2, 9 — modelo TCP/IP, encapsulación, capas, lab de tráfico
  con Wireshark (quedó inconcluso según diario del Día 2).
- **Módulo 2 (Subnetting/routing):** Días 9-11 — FLSM, VLSM, CIDR, NAT, ARP, lab de routing
  con network namespaces (profundizado, incluye conceptos de Docker/Kubernetes por curiosidad
  lateral).
- **Módulo 3 (DNS/HTTP):** Días 3, 4, 5, 12, 13 — jerarquía DNS, registros (A, CNAME, MX, TXT,
  SPF/DMARC), HTTP/HTTPS, TLS, lab de DNS forense (llegó hasta desafío 4).
- **Módulo 4 (Linux):** Días 6, 7, 8 — filesystem, permisos, chmod/chown, procesos, puertos,
  servicios.

**Nota de ritmo:** Días 1-10 con sesiones acotadas (Pomodoro). A partir del Día 11 el ritmo se
disparó (un solo archivo de preguntas del Día 11 llegó a 860 líneas) — mismo patrón que este
roadmap nuevo está diseñado para evitar. Antes de arrancar Módulo 5, se hace un Chequeo de
Bases sobre Módulos 1-4 para decidir qué repasar y qué saltar, en vez de repetir todo de cero.

---

## Chequeo de Bases — Módulos 1-4 (previo a arrancar el roadmap)

Variante temprana del mecanismo de "Chequeo de Bases" (normalmente usado en la transición
Fase 4→5), aplicada acá para aprovechar el avance previo sin arriesgar huecos no detectados.

- [x] Hecho — resultado: 4.5 / 10 — fecha: 2026-07-20
- Regla de corte: 7+ → saltar directo a Módulo 5. Menos de 7 → identificar qué módulo(s)
  específicos reforzar antes de avanzar (no repetir los 4 completos).
- Resultado real: sólido en Módulos 2 y 3 (con hueco puntual en TLS/certificados, tema de
  Módulo 5). Módulo 1 sin cobertura real en el chequeo (ninguna pregunta lo cubrió a fondo).
  Módulo 4 con hueco claro (SUID/passwd, cadenas de iptables).

**Decisión:** en vez de confiar en una muestra chica de 8 preguntas repartidas en 4 módulos,
se hace 1 sesión de repaso corto por cada uno de los 4 módulos antes de decidir qué saltar
y qué reforzar. Ver "Repaso de verificación Módulos 1-4" abajo.

---

## Repaso de verificación Módulos 1-4 — instrucción especial "saltar"

**Solo válido para estas 4 sesiones de repaso (1.rev, 2.rev, 3.rev, 4.rev). No aplica a
ninguna otra sesión del roadmap de acá en adelante — esto no se repite en Módulos 5+.**

En cada una de estas 4 sesiones, si en cualquier momento escribo la palabra **"saltar"**,
la instrucción para Claude es:

1. NO autorellenar el resultado como si el concepto estuviera dominado sin haberlo puesto
   a prueba. "Saltar" ahorra el trabajo MANUAL de bitácora/resumen/progreso.md — no
   reemplaza la verificación.
2. En su lugar, Claude hace **una sola pregunta corta de verificación** (2-3 min, no la
   sesión completa) sobre el concepto que tocaba esa sesión.
3. Si la respondo bien → Claude autorellena el resto (resumen de sesión, línea de
   progreso.md, bitácora) dando el concepto por cubierto, y seguimos a la siguiente sesión
   de repaso sin más trámite.
4. Si la respondo mal o dudo mucho → Claude NO autorellena nada. Seguimos con la sesión de
   repaso normal (formato completo) en ese concepto puntual, porque eso indica que el hueco
   es real, igual que pasó con Módulo 4 en el chequeo cruzado de hoy.

El objetivo de "saltar" es ahorrar tiempo administrativo cuando algo genuinamente ya está
firme, no maquillar un hueco para avanzar más rápido en el papel.

### Checklist de las 4 sesiones

- [x] 1.rev — Módulo 1 (TCP/IP) — resultado: flojo (2026-07-21), 0/3 conceptos firmes —
  (1) session hijacking por predicción de ISN: identificó "suplantación" en general pero
  sin la distinción off-path/on-path que es lo que vuelve grave el ataque; (2) mecanismo
  de SYN flood: agotamiento de RAM identificado correctamente, pero mecanismo impreciso
  (agota el backlog de conexiones semi-abiertas, no "capacidad de red"); (3) diferencia
  FIN vs RST y por qué RST injection es la herramienta ofensiva preferida: sin cobertura
  previa. No se marca Módulo 1 como completado. Pendiente reforzar con sesiones 1.1
  (profundizar ataque off-path), 1.2 (session hijacking + anatomía completa de flags) y
  1.3 (SYN flood, RST injection, idle scan) del roadmap normal antes de reintentar
  verificación.
- [x] 2.rev — Módulo 2 (Subnetting/routing) — resultado: flojo (2026-07-22), 1/3 conceptos
  firmes — (1) diseño VLSM para una red corporativa con requerimientos de hosts dispares
  (192.168.10.0/24 → 4 subredes de distinto tamaño): correcto de punta a punta, sin dudas;
  (2) longest prefix match en tabla de routing con rutas superpuestas: identificó el criterio
  de "pertenencia a la red" pero no el desempate por prefijo más específico cuando varias
  rutas matchean el mismo destino — mecanismo impreciso; (3) por qué ARP sin autenticación
  permite a un atacante en el mismo segmento interceptar tráfico: identificó que el ataque usa
  solicitudes ARP falsificadas y que la tabla se actualiza, pero sin el mecanismo preciso
  (respuestas ARP aceptadas sin verificación / ARP gratuito) ni la consecuencia (cache
  poisoning → MITM sin que las víctimas lo perciban). No se marca Módulo 2 como completado.
  Pendiente reforzar con sesiones 2.2 (tabla de routing y longest prefix match) y 2.5-2.6
  (ARP en profundidad, ARP spoofing y redirección de tráfico en el mismo segmento) del
  roadmap normal antes de reintentar verificación.
- [x] 3.rev — Módulo 3 (DNS/HTTP) — resultado: flojo (2026-07-22), 1/3 conceptos firmes —
  (1) por qué SPF solo (sin DMARC) casi nunca alcanza para bloquear un correo con el `From:`
  visible falsificado: identificó que SPF influye en spam vs no-spam y que DMARC es "el
  siguiente paso", pero sin el mecanismo preciso (SPF valida el envelope sender/Return-Path,
  no el `From:` visible; sin DMARC no hay política publicada ni exigencia de alineación entre
  ambos) — imprecisión de mecanismo; (2) subdomain takeover vía CNAME abandonado: correcto de
  punta a punta — el atacante reclama en el proveedor externo el recurso al que apunta el
  CNAME huérfano, y DNS no verifica que el destino siga siendo dueño del recurso; (3) qué
  vulnerabilidad nueva introduce la multiplexación de HTTP/2 sobre una sola conexión TCP: sin
  cobertura previa (HTTP/2 Rapid Reset — abuso de apertura/cancelación masiva de streams
  dentro de una sola conexión, evadiendo los límites de rate-limiting basados en conexiones
  que sí existían en HTTP/1.1). No se marca Módulo 3 como completado. Pendiente reforzar con
  sesiones 3.2 (SPF/DMARC y alineación) y 3.5-3.6 (HTTP/2-HTTP/3, superficies de ataque y
  cache poisoning en CDNs) del roadmap normal antes de reintentar verificación.
- [x] 4.rev — Módulo 4 (Linux) — resultado: flojo (2026-07-22), 0/3 conceptos firmes —
  (1) bit SUID y por qué es vector de escalación de privilegios: identificó el efecto general
  ("da permisos de root") pero de forma circular, sin el mecanismo (el `exec()` fija el EUID
  del proceso al dueño del archivo, independiente del UID real de quien lo invocó — cualquier
  falla del binario se hereda con ese EUID) — imprecisión de mecanismo; (2) systemd como
  mecanismo de persistencia (unit file con `ExecStart=`/`WantedBy=` + `systemctl enable`):
  sin cobertura previa; (3) crontab como mecanismo de persistencia recurrente, y por qué eso
  es distinto de systemd (que arranca una vez en el boot vs. re-ejecución en cada intervalo):
  sin cobertura previa. No se marca Módulo 4 como completado. **Decisión (2026-07-22, tras
  ver el resultado 0/3): en vez de refuerzo puntual, se cursa el Módulo 4 completo (sesiones
  4.1 a 4.6 del roadmap normal), no solo los 3 puntos flojos detectados hoy** — el avance
  previo de este módulo era el más genérico de los 4 (sin ángulo de seguridad específico) y
  solo se testearon 3 de las 6 sesiones, dejando 4.2 (`/proc`/`/var/log`), 4.4 (capabilities)
  y 4.6 (SSH hardening) sin verificar. Reintentar verificación al terminar las 6 sesiones.

  **Cierre del bloque de 4 repasos (1.rev-4.rev):** completado en su totalidad. Resultado
  consolidado — Módulo 1: 0/3 firmes, Módulo 2: 1/3, Módulo 3: 1/3, Módulo 4: 0/3. Ningún
  módulo se marca como completado. El resultado confirma el 4.5/10 del Chequeo de Bases
  cruzado (C.1) — no fue una muestra pesimista, fue representativa del estado real. Antes de
  continuar con el roadmap normal (Módulo 5 en adelante) corresponde reforzar los huecos
  puntuales listados en cada ítem de este checklist, módulo por módulo.

---

## Cómo actualizar esto (30 segundos, al final de cada sesión)

Agregá una línea a la tabla de abajo. Sesiones de teoría (ej. "1.3") van con su detalle en
`sesiones/sesion-N.N.md`. Sub-sesiones de lab (ej. "Lab M1 - sub 2") van con su detalle en
`labs/modulo-N/bitacora.md`, no acá.

| Sesión | Tipo | Fecha | Una frase de lo que quedó / se avanzó | Notas |
|---|---|---|---|---|
| 1.1 | Teoría | 2026-08-04 | Three-way handshake: mecanismo de ISN y por qué hacen falta 3 pasos — sólido, cálculo de ack correcto en las 2 direcciones del ejercicio | Etiquetó el número de ACK como "seq" (valor correcto, nombre no) — repasar la distinción antes de sumar flags nuevas en 1.2 |

---

## Labs en curso (enunciado ya generado, sub-sesiones pendientes)

Cuando arrancás el lab de un módulo, agregalo acá para saber en qué sub-sesión vas sin tener
que abrir `labs/modulo-N/bitacora.md` cada vez.

| Módulo | Sub-sesión actual | Total planeadas |
|---|---|---|
| — | — | — |

---

## Mecanismos de refuerzo (marcar cuando se hacen)

- [ ] Repaso espaciado — Módulo 1 (después del lab de Módulo 2)
- [ ] Limpieza de pendientes #1 (después del lab de Módulo 4)
- [ ] Repaso espaciado — Módulos 3-4 (después del lab de Módulo 6)
- [ ] Limpieza de pendientes #2 (después del lab de Módulo 8)
- [ ] Repaso espaciado — Módulos 7-8 (después del lab de Módulo 10)
- [ ] Limpieza de pendientes #3 (después del lab de Módulo 12)
- [ ] Repaso espaciado — Módulos 11-12 (después del lab de Módulo 14)
- [ ] Chequeo de bases Fase 4→5 (después del lab de Módulo 15) — resultado: __ / 10
- [ ] Limpieza de pendientes #4 (después del lab de Módulo 16)
- [ ] Repaso espaciado — Módulos 15-16 (después del lab de Módulo 18)
- [ ] Limpieza de pendientes #5 — cierre (después del lab de Módulo 20)

---

## Preguntas pendientes (las que surgen en sesión y no se desarrollan ahí)

Cuando en una sesión te digan "anotalo para después", va acá. Se revisan y cierran en las
sesiones de "Limpieza de pendientes" (ver tabla de arriba) — no quedan colgadas para siempre.

- (vacío por ahora)

---

## Módulos completados

- [ ] Módulo 1 — TCP/IP a nivel de ingeniería
- [ ] Módulo 2 — Subnetting, routing y arquitectura de redes
- [ ] Módulo 3 — DNS a nivel forense y HTTP/S en profundidad
- [ ] Módulo 4 — Linux como sistema administrable
- [ ] Módulo 5 — Criptografía aplicada a la seguridad
- [ ] Módulo 6 — OWASP Top 10 con explotación real
- [ ] Módulo 7 — Linux hardening y threat hunting manual
- [ ] Módulo 8 — Firewalls, IDS/IPS y análisis de tráfico avanzado
- [ ] Módulo 9 — HTTP avanzado, APIs REST y seguridad de APIs
- [ ] Módulo 10 — Autenticación, sesiones y gestión de identidad
- [ ] Módulo 11 — Python para seguridad ofensiva y defensiva
- [ ] Módulo 12 — Docker y seguridad de contenedores
- [ ] Módulo 13 — CI/CD seguro, Git y gestión de secretos
- [ ] Módulo 14 — Terraform e Infraestructura como Código segura
- [ ] Módulo 15 — Kubernetes y seguridad de orquestación
- [ ] Módulo 16 — AWS: arquitectura y modelo de seguridad compartida
- [ ] Módulo 17 — IAM en profundidad y privilege escalation en AWS
- [ ] Módulo 18 — VPC, networking cloud y seguridad perimetral en AWS
- [ ] Módulo 19 — Explotación de misconfiguraciones cloud reales
- [ ] Módulo 20 — Detección, respuesta a incidentes y SecOps cloud
