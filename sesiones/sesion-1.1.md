# Sesión 1.1 — Three-way handshake

**Módulo 1 — TCP/IP a nivel de ingeniería**
**Fecha:** 2026-08-04

## Concepto del día
El three-way handshake (SYN → SYN-ACK → ACK) no es un simple "saludo" entre cliente y
servidor: sincroniza los números de secuencia (ISN, Initial Sequence Number) que cada lado
va a usar para ordenar los bytes del flujo TCP. Cada lado propone su propio ISN; el segundo
y el tercer mensaje llevan además un número de ACK que confirma la recepción del ISN ajeno
(ack = ISN recibido + 1).

## Por qué hacen falta 3 pasos y no 2
Si el intercambio terminara en el paso 2 (SYN-ACK), el servidor habría propuesto su ISN pero
no tendría ninguna prueba de que el cliente lo recibió. El tercer mensaje (ACK) es esa prueba.
Recién ahí ambos lados no solo conocen los dos números (propio y ajeno) sino que tienen
confirmación mutua de que el otro también los conoce — eso es la sincronización de estado.

## Ejercicio de la sesión
Cliente con ISN=4000, servidor con ISN=9000. Resultado: correcto en las 3 direcciones y en
ambos cálculos de confirmación (4001 y 9001) — el mecanismo numérico quedó firme. Precisión
pendiente: el número de confirmación (paso 2 y paso 3) se etiquetó como "seq" en vez de
"ack" (el valor era correcto, la etiqueta no). Corregido en la sesión. La pregunta conceptual
("¿a quién le falta qué información si se corta en el paso 2?") se respondió correctamente y
sin ayuda: identificó que es el servidor quien queda sin confirmación de que el cliente
recibió su ISN.

## Gancho hacia la sesión 1.2
Si predecir el ISN te deja fabricar un mensaje con el número "correcto" sin ser parte real de
la conversación, eso es la base de lo que ya se nombró en 1.rev como "suplantación". La 1.2
va a esa distinción puntual: hacerlo viendo el tráfico real (on-path, se lee el número) versus
sin verlo (off-path, hay que adivinarlo) — el hueco concreto que quedó marcado en 1.rev —
más la anatomía completa de flags (ACK/FIN/RST/PSH/URG) de un segmento TCP.

## Pendiente anotado
Repasar en 1.2, antes de sumar flags nuevas, la distinción de nombre seq/ack: seq = mi propio
número de bytes; ack = confirmación del número ajeno (ajeno + 1). El cálculo ya está firme,
falta solo la etiqueta.
