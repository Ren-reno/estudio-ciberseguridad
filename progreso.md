# Progreso — Roadmap Cloud Security

**Última sesión completada:** —
**Próxima sesión a hacer:** pendiente de Chequeo de Bases Módulos 1-4 (ver sección abajo)

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

- [ ] Hecho — resultado: __ / 10 — fecha: __
- Regla de corte: 7+ → saltar directo a Módulo 5. Menos de 7 → identificar qué módulo(s)
  específicos reforzar antes de avanzar (no repetir los 4 completos).

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
