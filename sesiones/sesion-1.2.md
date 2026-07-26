# Sesión 1.2 — Session hijacking por predicción de ISN + anatomía de flags TCP

**Módulo 1 — TCP/IP a nivel de ingeniería**
**Fecha:** 2026-08-05

## Concepto del día — hijacking on-path vs off-path
Un Atacante que quiere hacerse pasar por un Cliente confiable frente a un Servidor tiene
que completar un three-way handshake entero fingiendo ser ese cliente. Si está on-path
(puede ver el tráfico real, por ejemplo vía un man-in-the-middle), lee el ISN real del
Servidor directamente — no necesita adivinar nada. Si está off-path (sin ningún acceso a
la red de ninguna de las 2 partes), tiene que adivinar el ISN que va a proponer el
Servidor en su SYN-ACK — que nunca le llega a él, sino al Cliente real — y mandar el ACK
final a ciegas.

## Concepto del día — anatomía de un segmento TCP
Un segmento no tiene un solo "tipo": lleva un conjunto de flags de 1 bit, y puede tener
varias prendidas a la vez (SYN-ACK ya era un ejemplo de esto). Las 6 flags: SYN (arrancar
conexión), ACK (confirmo recepción — presente en casi todos los segmentos después del SYN
inicial, no solo durante el handshake), FIN (cerrar ordenadamente), RST (cortar de golpe,
sin trámite), PSH (entregar los datos ya, sin bufferear) y URG (datos marcados urgentes).

## Ejercicio de la sesión
Pregunta 1 (FIN-ACK): identificó FIN correctamente ("cerrar ordenadamente"). En ACK hubo
una imprecisión puntual: lo describió como confirmación específica del three-way handshake,
cuando en realidad ACK confirma la recepción de los datos/estado más reciente en general —
en un FIN-ACK, que aparece al final de la conexión, no está "reconfirmando" el handshake
(que ya pasó hace rato), sino la última información intercambiada. Corregido en la sesión,
usando el mismo patrón que SYN-ACK: 2 señales en 1 segmento.

Pregunta 2 (on-path/off-path aplicado): identificó correctamente off-path y la necesidad de
adivinar el ISN. Precisión menor: no especificó de cuál de las 2 partes — es el ISN de
quien responde al mensaje falsificado (el Servidor, en el escenario dado), no el propio.
Corregido en la sesión.

## Gancho hacia la sesión 1.3
Cada flag que hoy se definió por su uso "normal" también se puede usar mal: un RST se puede
fabricar para cortar de golpe una conexión ajena sin ser parte de ella (RST injection); un
SYN se puede mandar en cantidad industrial sin completar nunca el handshake, para agotar los
recursos de un servidor (SYN flood) — conectando directo con la "sincronización de estado"
de 1.1: cada SYN que llega deja al servidor con una conexión a medio abrir, ocupando memoria.
1.3 va por SYN flood, RST injection e idle scan.

## Pendiente anotado
Ninguno nuevo. Lo de 1.1 (etiqueta seq/ack) no volvió a aparecer hoy — se puede dar por
resuelto.
