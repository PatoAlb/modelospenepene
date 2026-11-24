# Plan de trabajo colaborativo — Entrega 3 MSS

> **Universidad El Bosque · Ingeniería de Sistemas · Modelos y Simulación de Sistemas**  
> **Entrega 3: Relación estructura–comportamiento, dominancia de ciclos y diseño de estrategias**  
> **Fecha límite:** 23 de noviembre de 2026, **antes de las 23:55 (hora de Colombia)**.  
> **Estado:** documento de coordinación; las explicaciones son hipótesis a verificar con el modelo y **no sustituyen simulaciones ni evidencias**.

## 0. Objetivo y reparto justo

Se divide el desarrollo en **dos frentes de responsabilidad comparables**:

| Equipo | Responsabilidad principal | Qué produce |
| --- | --- | --- |
| **Parte A — Diagnóstico estructural y experimentos** | Primera parte de la guía: análisis de ciclos, curva base, brecha de flujos, desactivación y variación paramétrica | Sección de análisis, tablas de escenarios, gráficas de experimentos y conclusiones de dominancia |
| **Parte B — Diseño de estrategias y evaluación** | Segunda parte de la guía: estrategias viables, puntos de apalancamiento de Meadows, implementación en Vensim y comparación de escenarios | Sección de estrategias, ecuaciones modificadas, gráficas comparativas y conclusiones de intervención |

**Equidad real:** ambos frentes requieren trabajo escrito **y** experimental en Vensim; ninguno se queda solamente redactando. Cada frente documenta, cita, ejecuta, exporta resultados y revisa la consistencia de su apartado. La integración, revisión final y sustentación son compartidas.

**Asignación:** coloquen los nombres de las personas de cada frente aquí y en el documento final. No se asume qué integrante trabaja en cada uno.

- Parte A: **[nombres por asignar]**
- Parte B: **[nombres por asignar]**
- Revisión final y envío: **[responsable por asignar]**

---

## 1. Contexto indispensable del proyecto (leer ambas partes)

### 1.1 Problema y propósito

El proyecto estudia la **evolución del uso problemático de internet/plataformas de contenido en adolescentes**, con un modelo de **dinámica de sistemas construido en Vensim**. La pregunta es cómo los mecanismos de **enganche y personalización del contenido**, junto con la **preocupación social, regulación, supervisión parental e intervención profesional**, pueden incrementar o reducir la proporción de adolescentes con dificultades.

El modelo distingue por sexo dos **acumulaciones**:

- `Proporcion mujeres con dificultad`, con flujo de entrada `Inicio dificultad mujeres` y flujo de salida `Recuperacion mujeres`.
- `Proporcion hombres con dificultad`, con flujo de entrada `Inicio dificultad hombres` y flujo de salida `Recuperacion hombres`.

La **variable de interés del informe** es `Uso problematico promedio`. Es una variable auxiliar agregada a partir de las proporciones; **no debe tratarse como una acumulación independiente ni atribuírsele flujos propios**. Analizarla exige contrastar la evolución de **ambas acumulaciones** y sus entradas/salidas.

Otros elementos visibles del diagrama actual son: `Personalizacion del contenido`, `Efecto de la personalizacion`, `Atractivo del contenido`, `Atractivo base de las plataformas`, `Factor de enganche`, `Exposicion del contenido`, `Preocupacion social`, `Respuesta institucional`, `Tiempo de respuesta institucional`, `Respuesta regulatoria`, `Efecto de la regulacion`, `Supervision parental`, `Intervencion profesional`, `Tiempo intervencion profesional`, `Indice de apoyo`, `Factor de recuperacion`, y las tasas de inicio y recuperación por sexo. **Los nombres exactos deben verificarse en el archivo .mdl**, pues aquí se usan nombres legibles del diagrama y de conversaciones previas.

### 1.2 Diagrama y ciclos marcados

El diagrama compartido en el equipo etiqueta cinco ciclos: **R1, R2, B1, B2 y B3**.

- **R1 (hipótesis):** atractivo del contenido → enganche → nuevos casos → uso problemático → personalización/atractivo; efecto reforzador.
- **R2 (hipótesis):** uso problemático → personalización → atractivo y exposición → nuevos casos → uso problemático; efecto reforzador.
- **B1 (hipótesis):** preocupación social → respuesta institucional → supervisión/apoyo/recuperación → disminución de dificultades; compensador.
- **B2 (hipótesis):** preocupación social → regulación → reducción de atractivo/exposición → menor inicio de dificultades; compensador.
- **B3 (hipótesis):** preocupación social → intervención profesional → índice de apoyo/recuperación → menores dificultades; compensador.

**IMPORTANTE:** las etiquetas y descripciones anteriores provienen del diagrama y de una primera lectura. **No están matemáticamente confirmadas.** Para el literal 2.a, reconstruir cada camino cerrado completo, anotar signos de cada flecha y comprobar polaridad mediante producto de signos; comprobar además si alguna relación pertenece a otro ciclo o no cierra realmente. Si se detectan errores, documentar y corregir el diagrama antes de experimentar.

### 1.3 Resultado de simulación base ya disponible

Se compartió una gráfica de `Uso problematico promedio` para **2014–2030**, con tendencia de **crecimiento desacelerado hacia estabilización**. Valores **aproximados visuales, no exportados de Vensim**:

| Tramo tentativo | Evolución observada |
| --- | --- |
| 2014–2018 | de ~0,17 a ~0,57; incremento fuerte |
| 2018–2024 | continúa creciendo hacia ~0,67, pero con pendiente decreciente |
| 2024–2030 | se aproxima a ~0,68, con variación pequeña |

**Cuidado:** los tramos son solo una clasificación visual. La guía exige identificar etapas **con apoyo de la brecha absoluta entre flujos de entrada y salida**; todavía faltan las gráficas de los cuatro flujos. La estabilización a ~0,68 **no significa que el problema se haya solucionado**, y la curva sola **no prueba dominancia de ningún ciclo**. No presentar estos números aproximados como resultados exactos.

### 1.4 Criterios de modelación y rigor

- Conservar el **escenario base** intacto. Realizar experimentos en copias del .mdl o mediante parámetros e interruptores para volver al caso base.
- Verificar que cada nivel esté acotado de forma física y conceptualmente razonable (proporciones entre 0 y 1), los flujos tengan unidades compatibles (por ejemplo, **1/año** multiplicado por proporción; evitar mezclar `Year` y `año` en la comprobación de unidades de Vensim) y las ecuaciones no generen valores negativos no deseados.
- La estructura exacta y parámetros actuales no están adjuntos a este repositorio al crear este plan. **No asumir valores iniciales, constantes, fórmulas, signo de vínculos ni resultados que no se puedan verificar en el .mdl.**
- **No modificar dos mecanismos a la vez** cuando la prueba intenta aislar un ciclo; si los ciclos comparten variables, reconocer que puede ser imposible desactivar uno de forma completamente independiente sin introducir un interruptor específico.
- Guardar para cada experimento: propósito, cambio exacto, línea base, gráfico/tabla, interpretación y conclusión; etiquetar archivos con nombres inequívocos y unidades.

---

## 2. PARTE A — Diagnóstico, análisis estructural y dominancia de ciclos

**Objetivo del frente:** explicar **por qué** la variable `Uso problematico promedio` sigue una curva de crecimiento desacelerado y cuáles relaciones causales son relevantes en distintos tramos, mediante evidencia reproducible.

### A1. Revisar el modelo y el documento anterior (primera parte, numeral 1)

- [ ] Recuperar **primera y segunda entrega** y verificar consistencia con el modelo Vensim actual.
- [ ] Registrar errores corregidos, cambios del modelo, unidades, condiciones iniciales y horizonte 2014–2030.
- [ ] Entregar un párrafo breve sobre ajustes necesarios, sin copiar la totalidad de las entregas anteriores.

### A2. Polaridad y función de todos los ciclos (literal 2.a)

- [ ] Copiar/adjuntar una imagen legible del modelo y marcar **cada circuito completo**.
- [ ] Crear tabla `Ciclo | cadena causal cerrada | signos (+/-) | producto de signos | reforzador/compensador | función`.
- [ ] Revisar **R1, R2, B1, B2, B3** uno por uno; verificar si existen otros circuitos relevantes.
- [ ] Corregir interpretaciones o etiquetas que no coincidan con las flechas/ecuaciones.
- [ ] Aclarar cómo cada ciclo influye en el inicio de dificultades o en la recuperación y por qué su efecto puede tener retrasos.

### A3. Curvas base y etapas de evolución (literal 2.b)

- [ ] Exportar gráfica **base** de `Uso problematico promedio` (2014–2030).
- [ ] Exportar gráfica de `Inicio dificultad mujeres` y `Recuperacion mujeres` **en la misma escala** (misma unidad).
- [ ] Exportar gráfica de `Inicio dificultad hombres` y `Recuperacion hombres` **en la misma escala**.
- [ ] Si es posible, construir series `Brecha mujeres = ABS(Inicio dificultad mujeres - Recuperacion mujeres)` y `Brecha hombres = ABS(Inicio dificultad hombres - Recuperacion hombres)`; **además registrar el signo de la diferencia original**, porque el valor absoluto por sí solo no dice si el nivel crece o disminuye.
- [ ] Delimitar etapas apoyándose en los flujos y no solo en la curva promedio; indicar intervalos y valores aproximados o exactos según exportación.

**Clave matemática:** para cada sexo, `variación del nivel = flujo de inicio - flujo de recuperación`. Si entrada > salida, el nivel sube; si entrada ≈ salida, tiende a estabilizarse; si entrada < salida, desciende. Verificar cómo se calcula el promedio antes de sumar o promediar brechas.

### A4. Desactivar ciclos y probar dominancia (literal 2.c)

- [ ] Definir un experimento por cada ciclo **verificado** (R1, R2, B1, B2, B3), cuando su aislamiento sea técnicamente viable.
- [ ] Documentar el interruptor/ecuación exacta para desactivarlo **sin destruir las relaciones comunes con otros ciclos**.
- [ ] Comparar el escenario base contra cada intervención, principalmente en `Uso problematico promedio`; complementar con niveles y flujos.
- [ ] Evaluar cambios en pendiente inicial, momento de desaceleración, valor en 2030 y forma de la curva.
- [ ] Para cada experimento escribir: **(i) objetivo, (ii) evidencia, (iii) análisis de resultados, (iv) conclusión sobre explicación del comportamiento**.
- [ ] Distinguir entre **dominancia demostrada**, **apoyo parcial** y **resultado inconcluso**: un cambio fuerte al desconectar un mecanismo sugiere relevancia, pero no demuestra por sí solo dominancia exclusiva.

**Formato reutilizable para cada prueba:**

```text
Prueba A4-X — Ciclo [nombre]
Objetivo: comprobar si [ciclo] contribuye a [etapa y rasgo concreto].
Implementación: se cambió [ecuación/parámetro] de [base] a [prueba].
Evidencia: [nombre de gráfica/captura con las dos corridas].
Resultados: [diferencia cuantitativa y/o cualitativa observada].
Interpretación: [qué mecanismo explica la diferencia].
Conclusión: [respalda/no respalda/no permite determinar dominancia en etapa X].
```

### A5. Repetir usando variación paramétrica (literal 2.d)

- [ ] Elegir parámetros asociados a los mismos ciclos (por ejemplo, sensibilidad del enganche, efecto de personalización, intensidad de regulación, tiempo de respuesta, apoyo profesional), **solo después de comprobar sus ecuaciones reales**.
- [ ] Crear escenarios **bajo/base/alto** con rangos justificables, de un parámetro a la vez si se busca atribución causal.
- [ ] Mantener consistentes horizonte, condiciones iniciales y definición de variable de interés.
- [ ] Mostrar gráficas comparativas, tabla de parámetros usados y cambios en las etapas y el nivel final.
- [ ] Contrastar resultados con la desactivación: coincidencias, contradicciones, límites e incertidumbre.

### A6. Síntesis (literal 2.e, máximo 500 palabras)

- [ ] Redactar **un solo párrafo de hasta 500 palabras** que integre: estructura causal, etapas identificadas mediante brechas de flujos, pruebas de desactivación y variaciones paramétricas.
- [ ] No asignar dominancia de ciclos si no hay evidencia experimental que la respalde.
- [ ] Entregar al otro frente una **nota de hallazgos**: ciclos y parámetros más influyentes, límites del modelo y condiciones del caso base.

**Entregables de Parte A:** texto listo para integrar, tabla de ciclos, tablas de pruebas, gráficas comparativas, copia del modelo experimental y síntesis ≤500 palabras.

---

## 3. PARTE B — Estrategias, apalancamiento e implementación

**Objetivo del frente:** justificar **cómo modificar** los mecanismos del modelo mediante **una o máximo dos estrategias viables**, comparar resultados contra el escenario base y describir quién podría aplicarlas fuera del modelo.

### B1. Revisar el marco de decisión (segunda parte, numeral 1.i)

- [ ] Recuperar la **hipótesis dinámica** y los criterios bajo la óptica de **Koen** formulados en la **primera entrega**; citar su redacción real, **no inventarlos**.
- [ ] Revisar la lectura **Olaya et al. (2018), `Designing Systemic Policies: Zombies in the Classroom`**, y los puntos de apalancamiento de **Donella Meadows**; agregar fuentes completas y verificables.
- [ ] Definir el **tomador de decisión real** de cada estrategia (por ejemplo, colegio, autoridad educativa, institución de salud o plataforma) y distinguir lo que **sí** controla de lo que no.
- [ ] Registrar restricciones, actores involucrados, costos/recursos, demora de implementación y posibles efectos no deseados.

### B2. Diseñar una o dos estrategias coordinadas (numeral 1.i–ii)

Propuestas de trabajo **por validar y adaptar a las ecuaciones existentes**:

**Estrategia 1 — Protección digital y regulación del contenido.**
- Objetivo: reducir el mecanismo de enganche y exposición que favorece el inicio de dificultades.
- Posibles decisiones reales: acuerdos de uso responsable de plataformas en colegios, alfabetización digital, límites o configuración de recomendaciones, protocolos de aviso y participación familiar; separar lo ejecutable por un colegio de lo que exigiría una autoridad o plataforma.
- Posible implementación en Vensim: modificar el efecto regulatorio sobre `Atractivo del contenido` o el factor de exposición/enganche mediante un parámetro de intensidad; verificar si la intervención ya está modelada por `Respuesta regulatoria` y `Efecto de la regulacion`.
- Evidencia: comparación de inicio de dificultades en ambos sexos y cambio del promedio.

**Estrategia 2 — Detección temprana y acompañamiento profesional/familiar.**
- Objetivo: mejorar la recuperación y reducir la permanencia de adolescentes con dificultades.
- Posibles decisiones reales: tamizaje, formación a orientadores, rutas de derivación, seguimiento y apoyo a familias, con protección de datos.
- Posible implementación en Vensim: incrementar el apoyo que modifica `Factor de recuperacion`, reforzar `Intervencion profesional` o disminuir `Tiempo intervencion profesional` dentro de valores justificables.
- Evidencia: comparación de `Recuperacion mujeres`, `Recuperacion hombres`, niveles por sexo y promedio.

Estas son **hipótesis de política**, no estrategias evaluadas todavía. La decisión final de usar una o dos depende de la viabilidad y de las simulaciones.

### B3. Incluir y evidenciar puntos de apalancamiento (numeral 1.ii)

**Obligatorio:** entre la(s) estrategia(s) debe existir **al menos un punto** del grupo **Dinámica de acumulaciones y realimentación (10, 9, 8, 7, 6)** y **al menos uno** del grupo **Trascendentales (5, 4, 3, 2, 1)**. No basta con escribir los números: se debe explicar **qué cambia estructuralmente** y **qué decisión lo materializa**.

**Mapa inicial para contrastar con Meadows y el .mdl:**

| Punto sugerido | Grupo | Aplicación potencial | Cómo evidenciarlo |
| --- | --- | --- | --- |
| **8 — Intensidad de los ciclos compensadores** | Dinámica | Hacer más eficaz la recuperación mediante apoyo y acompañamiento | Cambiar relación apoyo → factor de recuperación; comparar flujos |
| **7 — Ganancia de ciclos reforzadores** | Dinámica | Reducir realimentación por personalización y atractivo | Cambiar intensidad del mecanismo, comparar crecimiento |
| **5 — Reglas del sistema** | Trascendentales | Protocolos institucionales de detección, acceso a apoyo y protección digital | Describir regla concreta, actor que la adopta y traducción al modelo |
| **4 — Autoorganización** | Trascendentales | Capacidad institucional/familiar de ajustar intervenciones según señales tempranas | Solo usar si se modela o argumenta una capacidad real de cambiar la estructura, no solo aumentar un parámetro |

**Precaución:** disminuir una constante no demuestra automáticamente un punto trascendental. Se requiere justificar reglas, capacidades, objetivos o cambio de paradigma real y cómo se representa explícitamente o mediante supuestos en el modelo. Revisar la numeración precisa de Meadows al redactar.

### B4. Implementar y evaluar escenarios (numeral 1.iii)

- [ ] Guardar **escenario base** con parámetros originales.
- [ ] Modelar la estrategia 1, la 2 (si se escogen ambas) y opcionalmente el escenario combinado, con **interruptores/variables explícitas** que permitan volver a la línea base.
- [ ] Documentar ecuaciones o parámetros modificados, valores anteriores/nuevos, unidades y justificación.
- [ ] Comparar en **un mismo gráfico** `Uso problematico promedio` base vs. intervención(es), siempre 2014–2030.
- [ ] Evaluar por separado `Proporcion mujeres con dificultad`, `Proporcion hombres con dificultad`, sus inicios y recuperaciones para explicar **por qué se altera la acumulación**.
- [ ] Medir cuando se pueda: valor final en 2030, diferencia absoluta, variación porcentual respecto del caso base (si el denominador es distinto de cero), tiempo de respuesta y consecuencias no deseadas.
- [ ] Explicar por qué una estrategia es **viable y consistente con las restricciones**. Identificar responsables y pasos reales, no confundir un cambio en una ecuación con una política automáticamente implementable.
- [ ] Vincular resultados con el diagnóstico de Parte A; si ese diagnóstico cambia, revisar las estrategias.

**Formato de resultados por estrategia:**

```text
Estrategia B4-X — [nombre]
Problema y mecanismo objetivo: ...
Tomador de decisión y actores: ...
Punto(s) de Meadows y justificación: ...
Acciones reales concretas: ...
Cambios en Vensim (ecuación, valor base y valor intervenido): ...
Gráfica(s) base vs. escenario: ...
Impacto sobre inicio, recuperación y proporción promedio: ...
Restricciones, incertidumbres y posibles efectos secundarios: ...
Conclusión de efectividad: ...
```

### B5. Cierre y coordinación de la integración

- [ ] Redactar la conclusión de las estrategias **solo** después de correr escenarios.
- [ ] Entregar al frente A los cambios de ecuaciones, hallazgos y resultados para comprobar coherencia causal.
- [ ] Preparar argumentos para la sustentación: quién actúa, qué variable cambia, qué ciclo afecta y qué mejora medible se espera.

**Entregables de Parte B:** texto listo para integrar, matriz Meadows, descripción operacional de políticas, tablas de parámetros, gráficas comparativas y modelo intervenido.

---

## 4. Integración compartida: documento final, archivo .mdl y sustentación

La guía solicita **un artículo académico completo** que incorpore las **dos primeras entregas corregidas** más el trabajo nuevo, y un archivo de Vensim con la interfaz para experimentos y estrategias.

### 4.1 Archivo final a entregar

Carpeta comprimida: **`EntregaFinal_MSS.zip`**, que contenga:

1. **Documento Word o PDF**, máximo **3000 palabras**, estilo artículo académico; incluir planteamiento y modelo previos, análisis, pruebas, estrategias, resultados, discusión, conclusiones y referencias en **IEEE o APA**.
2. **Archivo `.mdl` de Vensim**, con modelo funcional y evidencia/interfaz del diseño de experimentos y estrategias.

**Entrega:** 23 de noviembre de 2026 **antes de las 23:55** en el Aula Virtual; **solo una persona** del grupo sube el ZIP. Incluir nombres completos de **todos los integrantes en Word y Vensim**.

### 4.2 Revisión conjunta obligatoria

- [ ] Integrar ambas partes en **un único documento de máximo 3000 palabras**; evitar duplicar contexto.
- [ ] No sacrificar las dos entregas anteriores: incorporar sus componentes indispensables **corregidos y resumidos**.
- [ ] Todas las figuras tienen título, numeración, fuente («elaboración propia con Vensim») y se citan en el texto.
- [ ] Referenciar adecuadamente datos, artículos, lecturas, software y supuestos; no colocar bibliografía que no se consultó realmente.
- [ ] Verificar ortografía, coherencia de unidades, etiquetas, nombres de variables y consistencia entre figuras y narrativa.
- [ ] Probar que el `.mdl` **abre y simula**, permite reproducir línea base y escenarios y no presenta errores de unidades.
- [ ] Revisar que todo resultado numérico del informe **corresponda a una corrida real**.
- [ ] Exportar `.docx`/`.pdf`, generar `.zip`, revisar el ZIP y confirmar el envío.

### 4.3 Reparto de revisión cruzada

- **Parte A revisa Parte B:** que las intervenciones apunten a ciclos/relaciones reales y que los cambios sean compatibles con la hipótesis dinámica.
- **Parte B revisa Parte A:** que cada afirmación de dominancia esté respaldada por una simulación y que se puedan explicar las estrategias a partir del diagnóstico.
- **Ambos:** revisar el límite de palabras y ensayar la sustentación (estructura → comportamiento → experimento → estrategia → mejora y límites).

### 4.4 Propuesta de estructura breve del artículo

1. Título, autores, resumen y palabras clave.
2. Introducción: problema, alcance, evidencia y propósito del modelo (integración entrega 1).
3. Metodología: hipótesis dinámica, diagramas, niveles/flujos y validación previa (integración entrega 2).
4. Análisis estructura–comportamiento y dominancia (Parte A).
5. Diseño, implementación y evaluación de estrategias (Parte B).
6. Discusión, limitaciones y conclusiones.
7. Referencias.

**Guía de extensión orientativa** (revisar el cómputo final): 700–900 palabras de contexto y metodología; 800–950 de Parte A; 800–950 de Parte B; 150–250 de conclusiones, más el espacio necesario para el resto según reglas de conteo de la asignatura. **El total nunca debe superar 3000.**

---

## 5. Organización para que ambos trabajen en paralelo

Repositorio al crear este documento: **sin archivos previos**. Por eso es urgente subir el modelo `.mdl`, los dos documentos anteriores y las gráficas base. Sugerencia de estructura:

```text
/
├── PLAN_TRABAJO_ENTREGA3.md        ← este archivo
├── modelo/
│   ├── base/                      ← .mdl original sin cambios
│   ├── experimentos_A/            ← pruebas de ciclos
│   └── estrategias_B/             ← escenarios de intervención
├── documentos/
│   ├── entrega_1_y_2/             ← versiones previas
│   ├── parte_A.md
│   ├── parte_B.md
│   └── entrega_final.docx
├── evidencias/
│   ├── parte_A/
│   └── parte_B/
└── referencias/
```

**Reglas de coordinación:**

1. No editar el mismo `.mdl` simultáneamente. Cada frente trabaja sobre **copia del modelo base**; designar a una persona para la integración final de Vensim.
2. Acordar los **valores del escenario base** y documentarlos antes de experimentar, para que A y B comparen el mismo punto de partida.
3. Usar ramas separadas (`parte-a-analisis` y `parte-b-estrategias`) o archivos por frente. No sobrescribir resultados ajenos.
4. Nombrar gráficas con `base`, identificador de experimento/estrategia y variable; colocar fecha o versión de la corrida en notas.
5. Cuando se confirme un cambio importante, comunicarlo al otro frente; las pruebas de dominancia y los escenarios de estrategias **deben usar el mismo modelo validado**.
6. Si falta evidencia, escribir **PENDIENTE**. **No inventar cifras, cambios experimentales, referencias bibliográficas ni causalidad demostrada.**

### Fuentes mínimas que deben verificar y citar

- **Guía oficial**: «Entrega 3 — Diseño de estrategias», Universidad El Bosque, curso Modelos y Simulación de Sistemas (documento suministrado al equipo).
- **Donella Meadows**, *Leverage Points: Places to Intervene in a System* (verificar datos editoriales de la versión consultada).
- **Olaya et al. (2018)**, *Designing Systemic Policies: Zombies in the Classroom* (verificar autores, publicación y referencia completa).
- **William Braun (2002)**, *The System Archetypes*, **si** efectivamente se utilizan arquetipos.
- **OEDA / ESTUDES**, para datos empíricos **si se usan realmente**; no asumir que los datos representan Colombia.
- Referencias de las entregas anteriores y **Vensim** como herramienta metodológica.

### Prioridad inmediata antes del cierre

1. **Subir .mdl y entregas 1–2** al repositorio.
2. **Parte A:** sacar gráficas de inicios y recuperaciones y empezar pruebas de dominancia.
3. **Parte B:** definir una o dos estrategias **modelables** y correr comparaciones.
4. **Integrar y revisar:** artículo ≤3000 palabras, modelo reproducible y ZIP final.

> **Nota de honestidad metodológica:** hasta ahora hay una imagen del diagrama y una gráfica de la variable agregada, pero **no** están aportadas las series de flujos, corridas de desactivación, resultados de variación paramétrica ni resultados de estrategias. Este plan identifica exactamente esas evidencias faltantes para evitar conclusiones no sustentadas.
