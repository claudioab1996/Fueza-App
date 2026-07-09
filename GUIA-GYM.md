# Fuerza V2 — Guía de despliegue y uso

App personal de registro de entrenamiento de fuerza. Mismo patrón que la PWA de nutrición: local-first, sin cuentas, sin servidores, datos 100% tuyos.

## Archivos

| Archivo | Qué es |
|---|---|
| `index.html` | Toda la app (HTML + CSS + JS, ~128 KB) |
| `sw.js` | Service worker → funcionamiento offline real |
| `manifest.webmanifest` | Metadatos de la PWA |
| `icon-180.png` / `icon-512.png` | Icono de la app |

A diferencia de la app de nutrición, aquí hay 5 archivos en vez de 1: el service worker no puede vivir dentro del HTML (limitación del navegador) y es lo que garantiza que la app abra sin internet en el gimnasio. El flujo de despliegue es idéntico.

## Despliegue (GitHub Pages)

1. Crea un repositorio nuevo (ej. `fuerza`) o una carpeta en el que ya usas.
2. Sube los 5 archivos a la raíz (o a una carpeta, manteniendo rutas relativas).
3. Activa GitHub Pages: Settings → Pages → rama `main`.
4. Abre la URL en Safari del iPhone → Compartir → **Añadir a pantalla de inicio**.
5. Abre la app una vez con conexión (el service worker cachea todo). Desde ahí funciona sin internet.

⚠️ **Misma advertencia que la app de nutrición:** los datos viven en IndexedDB de Safari. Borrar historial de navegación, eliminar el icono o cambiar la URL de despliegue destruye los datos locales. **Exporta el JSON de respaldo con frecuencia** (Ajustes → Copia de seguridad completa).

## Nuevo en la V2.1

- **Crono siempre visible:** el temporizador de la sesión queda fijo bajo el encabezado al hacer scroll durante el entrenamiento.
- **Superseries corregidas:** al desenlazar un ejercicio (o quitarlo), el compañero que quedaba solo se desmarca automáticamente — un grupo de superserie ya no puede quedar con un único miembro.
- **Descripción de ejecución en los 138 ejercicios:** al abrir un ejercicio, una nota breve de técnica (postura, recorrido, errores a evitar).
- **Convención de registro del peso, visible en cada ejercicio y durante el entreno:** peso total (barra/máquina), por mancuerna (escribe el peso de UNA), por lado (unilaterales: series y peso por lado), o corporal (registra solo el lastre; en asistidas, el contrapeso). En ejercicios propios puedes fijarla manualmente.
- **Pictogramas refinados:** press inclinado, sentadilla, crunch y gemelos redibujados para mayor claridad.

## Nuevo en la V2

**Planes y rutinas desde cero**
- Crea rutinas sin necesidad de entrenar primero: nombre, ejercicios, series×reps objetivo y peso opcional
- Agrúpalas en planes (ej. "Rutina 2026") con desplegable, renombrado y edición completa
- Superseries también dentro del editor de rutinas

**Programas preestablecidos (8)**
- Full Body 3 días (hipertrofia y fuerza 5×5), Torso/Pierna 4 días (hipertrofia y fuerza), Push/Pull/Legs 6 y 3 días, Powerbuilding 4 días e Híbrido 5 días
- Plantillas genéricas basadas en principios con amplio respaldo: frecuencia 2x por músculo, 10–20 series semanales, sobrecarga progresiva
- "Adoptar" copia el programa como plan tuyo, 100% editable

**Ilustraciones y activación muscular**
- 24 pictogramas de patrón de movimiento (empuje horizontal/inclinado/vertical, tracción vertical/horizontal, bisagra, sentadilla, etc.) visibles en biblioteca, selector y editor
- Cada ejercicio muestra su mapa de activación: el cuerpo anatómico coloreado por predominancia (ej. remo con barra: dorsales 35%, espalda alta 28%, bíceps 15%, lumbares 12%…)
- La espalda se dividió en **dorsales** y **espalda alta** (14 grupos musculares en total)

**Biología más precisa**
- La biblioteca creció a ~138 ejercicios (muchas más variantes de máquina: press convergente/Hammer en 3 ángulos, remos por agarre y altura, Smith, unilaterales…)
- Cada ejercicio tiene activación ponderada por músculo, incluyendo impactos ligeros (el peso muerto reparte fatiga entre 7 grupos), y el mapa de recuperación y las series semanales por músculo usan esos pesos

**Calendario de entrenamiento**
- Vista mensual en Progreso: días entrenados marcados, toque para abrir el detalle, contador mensual y racha de días consecutivos

**Cuerpo anatómico rediseñado**
- Silueta orgánica con regiones musculares curvas (adiós rectángulos), usada en el mapa de frescura y en la activación por ejercicio

**Migración automática desde V1**
- Los datos existentes se migran solos al abrir: "espalda" → dorsales, ejercicios propios ganan mapa de activación, y las rutinas antiguas se agrupan en el plan "Mis rutinas". Las copias JSON de V1 también se importan sin problema.

## Qué incluye desde la V1

**Registro sin fricción**
- Marcar una serie = 1 toque (los valores de la sesión anterior vienen precargados)
- Swipe a la izquierda para borrar una serie
- Tipos de serie tocando el número: Normal → C (calentamiento) → D (drop set) → F (al fallo)
- Peso, reps y RPE por serie
- Superseries: botón ⛓ enlaza un ejercicio con el anterior
- Pantalla activa (Wake Lock) durante el entrenamiento
- Temporizador de descanso automático al completar cada serie, con vibración y pitido, ajustable ±15s

**Inteligencia y recuperación**
- Check-in diario de readiness (sueño, dolor, energía, 1–5) → ajusta las cargas sugeridas (−10% a +2.5%)
- Mapa corporal de frescura muscular (frente/espalda): cada serie efectiva suma fatiga al músculo principal (y la mitad a los secundarios) que se disipa en 72 h
- Sugerencia por ejercicio: si el RPE de la última sesión fue ≤7.5, propone progresión de +2.5%, redondeada a tus discos

**Analítica**
- Curva histórica de 1RM estimada por ejercicio (Epley o Brzycki, configurable)
- Tonelaje semanal (últimas 8 semanas)
- Series efectivas por músculo en los últimos 7 días, con referencia 10–20
- Detección y celebración de PRs (peso máximo y 1RM estimada) en el momento
- Rutinas: guarda cualquier entrenamiento como plantilla, o repite el último con un toque

**Herramientas**
- Biblioteca de ~100 ejercicios en español (músculo principal, secundarios, equipamiento, descanso sugerido)
- Ejercicios personalizados y edición de cualquiera (notas técnicas, descanso propio)
- Calculadora de discos con visualización de la barra (barra y discos configurables)

**Datos**
- Exportación CSV (`fecha;ejercicio;musculo;equipo;serie;tipo;peso_kg;reps;rpe;e1rm_est;superserie`)
- Copia de seguridad JSON completa + importación (fusiona, no borra)

## Integración con el ecosistema

Esta app sigue el patrón **capa de datos antes que capa de agente**: acumula datos estructurados ahora, y el futuro Agente de Salud Física los consumirá después vía el flujo ya establecido (exportar → enviar al bot de Telegram). El CSV está pensado para pre-computar resúmenes (tonelaje semanal, PRs, series por músculo) antes de pasarlos a Claude, igual que con el agente de finanzas.

Puede convivir con los CSV de Heavy: si ya tienes historial ahí, el formato de importación JSON permite migrarlo con un script pequeño (pendiente para cuando lo necesites).

## Ideas para V2 (cuando la V1 esté validada con datos reales)

- Importador de historial desde Heavy (CSV → JSON de Fuerza)
- Objetivos de series semanales por músculo, configurables
- Notas por serie y fotos de ajustes de máquina
- Gráfico de volumen por músculo a lo largo del tiempo
- Autorregulación más fina (doble progresión: reps antes que peso)
