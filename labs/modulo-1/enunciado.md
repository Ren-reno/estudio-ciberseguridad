# Lab Módulo 1 — Scanner de puertos con raw sockets

*Este archivo es un EJEMPLO de cómo queda el enunciado + plan de sub-sesiones, generado con
el prompt de "Paso 1" del roadmap. Sirve de referencia de formato — el enunciado real de tu
Módulo 1 se genera cuando termines las sesiones 1.1 a 1.5.*

## Objetivo

Dada una máquina virtual en tu red local, determinar qué servicios corren enviando y
analizando manualmente paquetes TCP con raw sockets en Python — sin usar `nmap` ni
librerías de alto nivel (nada de `python-nmap`, `scapy` queda para el Módulo 11).

## Entregable

- Script Python funcional que envíe paquetes TCP manualmente construidos y analice las
  respuestas (SYN-ACK, RST, timeout).
- Captura de Wireshark tomada en paralelo mientras corre el script.
- Explicación escrita (puede ir en este mismo archivo, sección "Mi resolución" al final)
  de por qué ciertos puertos responden con RST y otros con SYN-ACK.

## Criterio de éxito

Poder explicar, sin mirar el script, qué le pasa a un paquete SYN cuando llega a un puerto
cerrado vs uno abierto, y mostrarlo reflejado tanto en tu script como en la captura de
Wireshark.

## Plan de sub-sesiones (60 min cada una)

| Sub-sesión | Qué se resuelve hoy | Qué queda "cerrado" al final |
|---|---|---|
| 1 | Armar el socket raw en Python y construir a mano un paquete SYN válido (headers IP + TCP) | El paquete se arma y se puede imprimir/inspeccionar su estructura byte a byte, aunque todavía no se envíe |
| 2 | Enviar el paquete a la VM objetivo y capturar la respuesta cruda (sin analizarla todavía) | Tenés al menos una respuesta cruda capturada de un puerto abierto y una de uno cerrado |
| 3 | Parsear la respuesta (distinguir SYN-ACK de RST) y correr Wireshark en paralelo para comparar | El script ya clasifica puertos como abiertos/cerrados, y tenés la captura de Wireshark como evidencia |
| 4 (si hace falta) | Escanear un rango chico de puertos (no todo el rango, 10-20 puertos alcanza) y escribir la explicación final | Entregable completo: script + captura + explicación |

## Mi resolución

*(esto lo completás vos a medida que avanzás — código, capturas, explicación final)*
