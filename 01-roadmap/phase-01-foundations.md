
# 🧭 Ahora sí: FASE 1

# Phase 1 — Foundations of AI Evaluation & RAG Reliability

Mi propuesta inicial es que esta fase sea de aproximadamente:

## **8 semanas**

Con una dedicación máxima aproximada de:

> **10–12 horas semanales**

Total aproximado:

> **80–96 horas**

Pero el objetivo no será "estudiar durante ocho semanas".

El objetivo será:

# 🎯 Objetivo de la Fase 1

> **Construir una base práctica para investigar, evaluar y mejorar sistemas LLM/RAG mediante experimentos reproducibles.**

Al terminar esta fase deberías poder decir, con evidencia:

> **I can design and run reproducible experiments to evaluate the quality of an LLM/RAG system, identify failures, and implement regression tests.**

Esto es mucho más importante que poder decir:

> "He terminado un curso de RAG."

---

# 1️⃣ Capacidades prioritarias

Durante esta fase necesitamos desarrollar **cinco capacidades**.

## A. Entender cómo funcionan los sistemas LLM

No necesitamos convertirte ahora en investigador de deep learning.

Necesitas entender suficientemente:

* tokens;
* context windows;
* prompting;
* temperature;
* sampling;
* embeddings;
* limitations de los LLM;
* alucinaciones;
* determinismo vs variabilidad.

### Objetivo

Poder formular hipótesis sobre por qué un sistema LLM produce determinados resultados.

---

# B. Fundamentos de RAG

Necesitamos entender el pipeline:

```text
Documents
     ↓
Chunking
     ↓
Embeddings
     ↓
Vector Store
     ↓
Retrieval
     ↓
Context
     ↓
LLM
     ↓
Answer
```

Debes comprender especialmente dónde puede fallar cada etapa.

Por ejemplo:

```text
Bad documents
        ↓
Bad chunks
        ↓
Bad embeddings
        ↓
Wrong retrieval
        ↓
Bad context
        ↓
Bad answer
```

Esto conecta directamente con tu futuro posicionamiento.

---

# C. AI Evaluation

Esta probablemente es la capacidad **más importante de la Fase 1**.

Debes aprender:

* qué significa evaluar un sistema AI;
* cómo construir un evaluation dataset;
* métricas básicas;
* test cases;
* expected behaviour;
* reproducibility;
* comparación A/B;
* evaluación de retrieval;
* evaluación de respuestas.

Conceptualmente:

```text
SYSTEM CHANGE
      ↓
RUN EVALUATION
      ↓
MEASURE
      ↓
COMPARE
      ↓
REGRESSION?
      ↓
DECISION
```

Aquí tu experiencia en QA Automation empieza a convertirse directamente en ventaja competitiva.

---

# D. Failure Analysis

No queremos simplemente medir:

> "Score = 0.78"

Queremos aprender a preguntar:

> **¿Por qué?**

Por tanto, debes empezar a clasificar fallos.

Ejemplos:

### Retrieval failures

* documento relevante no recuperado;
* chunk incorrecto;
* ranking incorrecto;
* contexto incompleto;
* ruido excesivo.

### Generation failures

* hallucination;
* answer unsupported by context;
* incomplete answer;
* incorrect synthesis;
* failure to follow instructions.

Esta capacidad será una parte importante de tu futura identidad profesional.

---

# E. Regression Testing for AI

Aquí hacemos una conexión muy directa con QA Automation.

El concepto:

```text
Failure discovered
       ↓
Reproduce
       ↓
Create test case
       ↓
Fix system
       ↓
Automate evaluation
       ↓
Prevent regression
```

Esta será probablemente una de las áreas donde puedes diferenciarte más rápidamente.

---

# 2️⃣ Qué NO estudiaremos todavía

Esto es extremadamente importante.

Durante la Fase 1 **NO vamos a intentar aprender**:

❌ Deep Learning desde cero en profundidad.

❌ Matemáticas avanzadas de transformers.

❌ Entrenamiento de modelos.

❌ Fine-tuning.

❌ Multi-agent systems complejos.

❌ Todas las frameworks de AI.

❌ MLOps completo.

❌ Kubernetes.

❌ Cloud architecture avanzada.

❌ General cybersecurity.

❌ Pentesting.

❌ Bug bounty.

❌ Certificaciones por acumular.

No porque sean inútiles.

Sino porque **no son el cuello de botella actual** para tu transición.

---

# 3️⃣ El proyecto práctico de la Fase 1

La Fase 1 necesita un proyecto central.

No cinco proyectos.

## 🧪 Corpus Studio — Evaluation Laboratory v0.1

El objetivo será construir un pequeño laboratorio reproducible.

Algo conceptualmente así:

```text
                CORPUS
                   │
                   ▼
              RAG SYSTEM
                   │
                   ▼
             EVALUATION
                   │
        ┌──────────┴──────────┐
        ▼                     ▼
   RETRIEVAL              ANSWER
   EVALUATION            EVALUATION
        │                     │
        └──────────┬──────────┘
                   ▼
            FAILURE ANALYSIS
                   │
                   ▼
            REGRESSION TESTS
```

No necesitamos construir una aplicación comercial.

Necesitamos construir:

> **Un sistema experimental que podamos medir y romper.**

---

# 4️⃣ Experimento central de la Fase 1

Quiero que la fase tenga una pregunta experimental clara.

Por ejemplo:

> **How do chunking strategies affect retrieval quality and answer quality in a small RAG system?**

Esta pregunta es excelente porque permite trabajar simultáneamente:

* corpus;
* chunking;
* retrieval;
* evaluation;
* métricas;
* experimentos A/B;
* failure analysis;
* documentación.

## El experimento

```text
SAME CORPUS
     │
     ├── Strategy A
     │
     ├── Strategy B
     │
     └── Strategy C
             │
             ▼
       RETRIEVAL TESTS
             │
             ▼
       ANSWER EVALUATION
             │
             ▼
       FAILURE ANALYSIS
             │
             ▼
          RESULTS
```

Este experimento puede convertirse posteriormente en:

1. código en **Corpus Studio**;
2. metodología en **Awesome Corpus Engineering**;
3. una publicación técnica en inglés;
4. potencialmente material para una contribución futura.

Eso es **alto leverage**.

---

# 5️⃣ Papel de cada repositorio

## Corpus Studio

Durante Fase 1:

```text
Experiment infrastructure
+
RAG system
+
Evaluation dataset
+
Metrics
+
Experiment results
+
Regression tests
```

---

## Awesome Corpus Engineering

No vamos a intentar llenarlo de contenido artificialmente.

Solo añadiremos conocimiento derivado del trabajo real.

Posibles primeros artefactos:

```text
Chunking Strategy Evaluation Checklist

RAG Retrieval Failure Taxonomy

Corpus Quality Questions Before Building a RAG System
```

Regla:

> **No invent documentation for the sake of documentation.**

Primero experimentamos.

Después generalizamos.

---

# 6️⃣ Evidencia profesional que debe producir la fase

Al final de la Fase 1 deberíamos tener aproximadamente:

### 🧪 1 experimento reproducible

Con:

* pregunta;
* hipótesis;
* metodología;
* variables;
* resultados.

### 📊 1 evaluation dataset

Pequeño pero bien documentado.

### 🔬 Comparación A/B/C

Al menos dos estrategias comparadas.

### 🐛 Failure taxonomy inicial

Con fallos reales encontrados.

### 🤖 Regression tests iniciales

Algunos casos automatizados.

### 📖 1 artefacto reutilizable

En Awesome Corpus Engineering.

### ✍️ 1 publicación técnica

En inglés.

No necesariamente larga.

Pero basada en:

```text
Question
↓
Experiment
↓
Results
↓
Failures
↓
Lessons
```

---

# 7️⃣ Criterios para terminar la Fase 1

No terminamos simplemente porque hayan pasado ocho semanas.

Terminamos cuando puedas demostrar:

### Capability 1

Puedes explicar un pipeline RAG y sus principales puntos de fallo.

### Capability 2

Puedes diseñar un evaluation dataset básico.

### Capability 3

Puedes ejecutar una comparación experimental reproducible.

### Capability 4

Puedes medir retrieval quality.

### Capability 5

Puedes identificar y clasificar fallos.

### Capability 6

Puedes convertir un fallo encontrado en un regression test.

### Capability 7

Puedes comunicar los resultados técnicamente en inglés.

---

# 📚 Ahora sí: qué debe hacer el Learning Planner

Ahora ya tenemos suficiente dirección estratégica.

El Learning Planner debe recibir **un encargo concreto**, no una petición vaga.

Yo le daría esta misión:

> Design an 8-week learning plan, approximately 10–12 hours per week, to develop the capabilities required for Phase 1: Foundations of AI Evaluation & RAG Reliability.

Y proporcionarle:

### Required capabilities

```text
LLM fundamentals

RAG fundamentals

Embeddings and vector retrieval

AI evaluation

Evaluation datasets

Retrieval metrics

Failure analysis

Regression testing for AI systems

Reproducible experimentation
```

### Practical objective

```text
Build a small reproducible RAG evaluation laboratory
inside Corpus Studio.
```

### Scope constraints

```text
Do not prioritize:

Deep Learning theory
Model training
Fine tuning
Complex agents
MLOps
Kubernetes
Cloud architecture
General cybersecurity
```

### Expected outcome

```text
A reproducible experiment comparing
different chunking strategies and measuring
their impact on retrieval and answer quality.
```

---

# Mi recomendación para nuestro siguiente movimiento

Yo haría ahora **dos acciones concretas**:

## Acción 1 — Registrar oficialmente la Fase 1

Crearíamos en tu repositorio:

```text
01-roadmap/
    phase-01-foundations.md
```

Ese documento se convierte en el contrato de la fase.

## Acción 2 — Enviar el encargo al Learning Planner

Con esta estrategia ya definida, el Learning Planner puede crear el calendario concreto.

---

Y hay una decisión adicional que quiero introducir desde el principio:

> **El Coordinator debe hacer revisiones periódicas, no esperar al final de una fase.**

Mi propuesta sería un **Project Review cada 2 semanas**:

```text
What did we learn?

What did we build?

What evidence did we produce?

What failed?

What changed strategically?

What should we stop doing?

What is next?
```

Así mantenemos el proyecto dirigido, incluso aunque haya varios chats trabajando en paralelo.

**Mi recomendación: el siguiente paso es registrar esta Fase 1 oficialmente en tu repositorio y, después, llevar el encargo estratégico al Learning Planner.**
