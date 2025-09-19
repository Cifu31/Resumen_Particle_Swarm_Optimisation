# Resumen_Particle_Swarm_Optimisation
# Resumen — *Particle Swarm Optimisation: A Historical Review Up to the Current Developments* (Entropy, 2020)

## ¿Qué es PSO?

El **Particle Swarm Optimisation (PSO)** es un algoritmo de optimización inspirado en el comportamiento social (p. ej., bandadas de aves). Cada *partícula* representa una solución candidata y actualiza su **velocidad** y **posición** combinando (i) su mejor experiencia personal (*pbest*) y (ii) la mejor solución conocida por el grupo (*gbest*). Es simple, no requiere gradientes y funciona bien en funciones objetivo complejas, pero puede sufrir **convergencia prematura** y **pérdida de diversidad**.

## Evolución histórica

Desde los trabajos fundacionales de **Kennedy y Eberhart (1995)**, PSO creció hasta convertirse en una familia amplia de variantes. La revisión organiza estas líneas de desarrollo para ayudar a elegir la versión adecuada según el tipo de problema (restricciones, multimodalidad, múltiples objetivos, costo por evaluación, recursos de cómputo).

## Ajustes para estabilidad y convergencia

* **Peso de inercia (ω)**: controla el balance exploración–explotación; suele **decrecer** durante las iteraciones.
* **Factor de constricción (K)**: alternativa con garantías de estabilidad (parámetros típicos ϕ≈4.1, K≈0.7298).
* **Límite de velocidad (Vmax)**: evita explosiones de velocidad; valores muy altos “sobrevuelan” óptimos, muy bajos estancan.
* **Topologías de vecindario**: anillo, estrella, von Neumann o dinámicas; vecindarios **pequeños** favorecen diversidad en paisajes difíciles.
* **Búsqueda local alrededor de gbest (p. ej., GCPSO)**: útil para salir del estancamiento.

## Variantes representativas

* **FIPS (Fully Informed PSO)**: cada partícula se guía por **todos** sus vecinos (promedio ponderado), no solo por el mejor.
* **APSO (Adaptive PSO)**: detecta estados evolutivos (exploración, explotación, convergencia, salto) y **adapta** parámetros; puede mutar gbest de forma controlada.
* **CPSO / cooperativo**: divide dimensiones en **sub-enjambres** cooperantes (útil en alta dimensionalidad).
* **Niching / multi-swarm / species-based**: separa el enjambre en **nichos** para seguir **múltiples óptimos** y fusiona/absorbe sub-enjambres cuando se acercan.

## Problemas con restricciones (COP)

Estrategias comunes:

* **Penalizaciones** (estáticas o dinámicas) que transforman el problema en no restringido (requieren calibración).
* **Preservación de soluciones factibles (FSM)** para no “perder” factibilidad.
* **Proyección/fly-back**: devuelve la partícula a la región válida (útil salvo óptimos en el borde).

## Optimización multiobjetivo (MOPSO)

Extiende PSO con:

* **Repositorio externo** de **soluciones no dominadas** (frente de Pareto).
* **Mecanismos de diversidad** (p. ej., mutaciones suaves, selección por distancia) para cubrir el frente.
  Correr PSO por objetivo de forma independiente rara vez produce frentes Pareto de calidad.

## Multimodalidad (múltiples óptimos)

* **Niching / multi-swarm** para seguir varios óptimos en paralelo.
* **Transformaciones** (stretching/deflection/repulsion) que “repelen” del óptimo encontrado para explorar otros (cuidado con mínimos artificiales).
* **Vecindarios por distancia y centros de masa** para separar regiones de búsqueda.

## Hibridaciones y paralelización

* **Híbridos con GA/DE/SA/ACO** y operadores evolutivos (selección, *crossover*, mutaciones gaussiana/Cauchy) para inyectar diversidad y mejorar explotación.
* **PSO paralelo (PPSO)**: multi-CPU/GPU, esquemas *master–slave*, grano fino/grueso y **MapReduce**. La ejecución **asíncrona** suele mejorar el aprovechamiento de hardware cuando la evaluación es costosa.

## Guía rápida 

* **Búsqueda general con estabilidad**: PSO con **ω decreciente** o **factor de constricción**.
* **Varios óptimos relevantes**: **niching/multi-swarm**; considerar transformaciones si sabes cuántos óptimos buscas.
* **Múltiples objetivos**: **MOPSO** con repositorio y control de diversidad.
* **Restricciones complejas**: penalización bien calibrada o **proyección**; conservar factibles (FSM).
* **Alta dimensión / evaluaciones costosas**: **CPSO/cooperativo** + **paralelización** (idealmente asíncrona).
* **Atascos frecuentes**: **APSO** (adaptación de estados) o **búsqueda local** tipo GCPSO.

## Idea central

PSO ya no es un único algoritmo, sino un **ecosistema**. No existe una variante universalmente mejor: la elección debe **alinearse con la estructura del problema** (multimodalidad, restricciones, número de objetivos) y con los **recursos de cómputo** disponibles.
