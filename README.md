# Cloud Security — bitácora de estudio

Repositorio de estudio del roadmap de Cloud Security Engineer. Estudiante de Analista Programador,
en tránsito hacia especialización en seguridad cloud.

## Estructura

```
├── roadmap.md          # Los 20 módulos partidos en sesiones de ~1h
├── progreso.md          # Estado actual: última sesión, checklist de módulos
├── sesiones/             # Notas de cada sesión de teoría (1 archivo por sesión)
├── labs/                 # Entregables de los laboratorios de cada módulo
└── notas/                # Preguntas pendientes, apuntes sueltos, cosas para revisar
```

## Cómo se estudia esto

Cada fila del `roadmap.md` es una sesión de 45-60 min con cronómetro. El `progreso.md` es la
fuente de verdad de en qué sesión voy — se actualiza al final de cada sesión, y es lo que le
paso a cualquier LLM al empezar una conversación nueva, para no depender de historial de chat.

Metodología completa explicada en `roadmap.md`.

## Nota de seguridad

Este repo es público. El `.gitignore` está configurado para excluir credenciales, outputs crudos
de comandos (nmap, wireshark, etc.) que puedan exponer datos reales, y archivos de estado de
Terraform. Cualquier output de lab que se documente acá está transcrito a mano con datos
sensibles reemplazados por placeholders.
