# Ideas centrales — el hilo que conecta todo el roadmap

## Por qué existe este documento

`roadmap.md` tiene el índice de 150+ sesiones repartidas en 20 módulos y 5 fases, y `progreso.md` tiene el estado de avance. Ninguno de los dos responde una pregunta distinta: ¿por qué estas cosas van juntas? Un programa que puede tomar años se siente como una lista de temas sueltos si no hay algo que conecte la sesión de hoy con la de hace ocho meses. Este documento es ese hilo — no repite contenido de roadmap.md, apunta a él.

## Los patrones que se repiten en cada fase

No son 40 conceptos nuevos por fase — son 4 ideas que se repiten una y otra vez, en una capa de abstracción distinta cada vez. Reconocerlas es lo que hace que el módulo 17 se sienta familiar en vez de nuevo.

**1. Superficie de ataque / límite de confianza.** Cada capa tiene una frontera entre "confiable" y "no confiable", y ahí vive casi todo lo que se estudia. Aparece primero en el three-way handshake de TCP (1.1): el sistema confía en que quien responde el ACK es quien dice ser. Se repite en ARP sin autenticación (2.5), en que un firewall perimetral no protege una vez cruzado el límite (8.2), en que el kernel compartido —no el contenedor— es el límite real de aislamiento (12.1), y llega a su forma más pura en AWS: la identidad IAM es el límite de confianza (16-17). El "perímetro de red" del Módulo 1 termina siendo "perímetro de identidad" en Fase 5.

**2. La cadena del atacante (kill chain).** Reconocimiento → acceso inicial → escalación de privilegios → persistencia → exfiltración. Se nombra recién en 19.3, pero se practica mucho antes: el OSINT sobre DNS (Módulo 3) es reconocimiento, la predicción de ISN (1.2) es acceso inicial, sudoers o SUID mal configurado (4.1, 4.4) es escalación, systemd o crontab (4.3, 4.5) es persistencia. Al llegar al Módulo 19 no hay un concepto nuevo — hay un nombre para algo ya practicado seis veces en capas distintas.

**3. Misconfiguración por encima de vulnerabilidad exótica.** La causa más común de una brecha real no es un exploit sofisticado, es alguien configurando mal algo que ya existía. Arranca en `/etc/sudoers` (4.1): la regla no falla por un bug, falla porque alguien le dio más alcance del necesario. Se repite como causa raíz #1 del OWASP Top 10 (6.5), en las misconfiguraciones de Terraform (14.3), y llega a su caso de manual en el Módulo 19: Capital One 2019 fue un SSRF más un S3 público — dos configuraciones, no una vulnerabilidad nueva.

**4. Defensa en profundidad.** Ninguna capa sola alcanza. Se nombra en 7.1, pero el roadmap entero está construido sobre la idea: firewall + iptables + MAC + auditd (Módulos 1, 7, 8) es el mismo principio que Security Groups + NACLs + IAM de mínimo privilegio + GuardDuty en Fase 5. Cada fase nueva no reemplaza a la anterior — le agrega una capa.

## Mapa de las 5 fases

- **Fase 1 — Infraestructura base (Módulos 1-4).** Cómo funcionan las cosas por dentro, todavía sin ningún ángulo de "nube": TCP/IP, redes, DNS, Linux. Es el idioma que todo lo demás asume que ya se habla.
- **Fase 2 — Seguridad de infraestructura clásica (Módulos 5-8).** La misma infraestructura de Fase 1, ahora con el lente de qué la protege y qué la rompe: criptografía, OWASP Top 10, hardening de Linux, firewalls e IDS.
- **Fase 3 — Aplicaciones web y APIs (Módulos 9-11).** Las mismas ideas de confianza y superficie de ataque, aplicadas a la capa donde vive la mayoría de las vulnerabilidades reales: HTTP, autenticación, y Python como herramienta.
- **Fase 4 — DevOps/SecOps e IaC (Módulos 12-15).** Las mismas ideas, aplicadas a cómo se construye y despliega software hoy: contenedores, CI/CD, Terraform, Kubernetes.
- **Fase 5 — Cloud Security AWS (Módulos 16-20).** Todo lo anterior convergiendo en un solo lugar. La nube no introduce ideas nuevas — las junta todas bajo el modelo de responsabilidad compartida.

## Glosario vivo

No duplica el "Detalle por sesión" de cada módulo en roadmap.md — eso queda ahí. Esto es solo para los términos que atraviesan varias fases y conviene tener a mano sin ir a buscarlos:

- **Superficie de ataque / límite de confianza** — frontera entre lo confiable y lo no confiable en cualquier capa (red, host, app, contenedor, cuenta cloud).
- **Kill chain** — recon → acceso inicial → escalación → persistencia → exfiltración.
- **Misconfiguración vs. vulnerabilidad** — la mayoría de las brechas reales son alguien configurando mal una función existente, no un exploit nuevo.
- **Defensa en profundidad** — ninguna capa sola alcanza; se combinan capas independientes.
- **Mínimo privilegio** — cada identidad (usuaria, servicio, rol) con exactamente el acceso que necesita, ni un permiso más.
