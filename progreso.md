# Progreso — Roadmap Cloud Security

**Última sesión completada:** 1.rev — Repaso de Verificación Módulo 1 (TCP/IP) — 2026-07-21
**Próxima sesión a hacer:** 2.rev — Módulo 2 (Subnetting/routing). Nota: Módulo 1 quedó
flojo en este repaso (no completado) — falta reforzar con sesiones 1.1-1.3 del roadmap
normal antes de darlo por firme (ver checklist abajo).

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
- [ ] 2.rev — Módulo 2 (Subnetting/routing) — resultado: __
- [ ] 3.rev — Módulo 3 (DNS/HTTP) — resultado: __
- [ ] 4.rev — Módulo 4 (Linux) — resultado: __ (ya sabemos que acá hay hueco: SUID/passwd, cadenas iptables)

---

## Cómo actualizar esto (30 segundos, al final de cada sesión)

Agregá una línea a la tabla de abajo. Sesiones de teoría (ej. "1.3") van con su detalle en
`sesiones/sesion-N.N.md`. Sub-sesiones de lab (ej. "Lab M1 - sub 2") van con su detalle en
`labs/modulo-N/bitacora.md`, no acá.

| Sesión | Tipo | Fecha | Una frase de lo que quedó / se avanzó | Notas |
|---|---|---|---|---|
| — | — | — | — | — |

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
