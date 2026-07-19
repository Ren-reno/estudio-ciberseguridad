# Sesión 1.1 — Three-way handshake

*Este archivo es un EJEMPLO de formato, usado para probar el sistema de patches. No refleja
progreso real todavía — progreso.md sigue en "Próxima sesión a hacer: 1.1" hasta que hagas
la sesión de verdad.*

**Módulo 1 — TCP/IP a nivel de ingeniería**

## Concepto del día
El three-way handshake (SYN → SYN-ACK → ACK) no es un simple "saludo" entre cliente y
servidor. Su función real es sincronizar los números de secuencia (ISN, Initial Sequence
Number) que cada lado va a usar para ordenar los bytes del flujo TCP.

## Por qué importa
Cada lado elige un ISN pseudo-aleatorio. Si ese número fuera predecible, un atacante que
no está en la ruta del tráfico (no puede ver los paquetes reales) podría igual calcular
qué ISN va a usar el servidor y falsificar paquetes como si viniera del cliente legítimo.

## Ejercicio de la sesión
Se armó a mano la secuencia de 3 paquetes de un handshake (flags, números de secuencia,
números de ACK) para una conexión hipotética, verificando que cada ACK sea seq+1 del
paquete anterior.

## Gancho hacia la sesión 1.2
Si predecir el ISN te deja falsificar paquetes, ¿qué pasa específicamente cuando alguien
lo logra? Eso es session hijacking — tema de la próxima sesión, junto con el resto de
las flags TCP (ACK/FIN/RST/PSH/URG).

## Pendiente anotado
Ninguno esta sesión.
