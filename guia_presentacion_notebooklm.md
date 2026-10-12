# Ciberseguridad en la era cuántica

## Documento consolidado para Google NotebookLM

Este archivo reúne el contenido completo de la guía general, las 38 diapositivas, las notas del presentador y el taller práctico de Qiskit. Está preparado como fuente para generar un resumen de audio o podcast en NotebookLM.

- Presentación pública: https://brun3y.github.io/quantum-and-cybersecurity/
- Autor: Edgar Bruney Castañeda Torres · Qiskit Advocate
- Fecha de la presentación: octubre de 2026
- Duración prevista: 60 minutos

---

## Guía general del proyecto

Presentación interactiva en español sobre fundamentos de computación cuántica, la amenaza a la criptografía de clave pública, estándares poscuánticos y migración criptográfica.

## Ver la presentación

**https://brun3y.github.io/quantum-and-cybersecurity/**

La charla incluye un taller para crear el estado de Bell Φ⁺ con Qiskit, ejecutarlo en un simulador y enviarlo a una QPU real de IBM Quantum.

La diapositiva 8 reproduce un video oficial de IBM Research desde YouTube y requiere conexión a internet.

## Material del taller

- [`taller_estado_bell.ipynb`](presentacion/taller_estado_bell.ipynb)

La API key de IBM debe almacenarse en Colab Secrets como `IBM_QUANTUM_API_KEY`; nunca debe incluirse directamente en el notebook.

## Controles de la presentación

- `←` / `→`: navegar.
- `N`: notas del presentador.
- `F`: pantalla completa.
- `T`: cronómetro.
- `?`: ayuda.

Los activos visuales adaptados de Qiskit Advocate Library conservan su licencia Apache 2.0 en `presentacion/ASSET-LICENSE.txt`.

---

# Contenido de la presentación

## Diapositiva 1: Ciberseguridad en la era cuántica

*Sección: Apertura · Tiempo sugerido: 0.5 min*

Computación cuántica × ciberseguridad 60 min

### Ciberseguridad en la era cuántica

De los qubits a una estrategia de migración —y a un procesador cuántico real.

*Visual: Ilustración de una persona trabajando frente a una computadora cuántica.*

Edgar Bruney Castañeda Torres · Qiskit Advocate Octubre 2026

### Notas del presentador

Objetivo. Abrir con el resultado: al terminar, la audiencia podrá distinguir la amenaza real del ruido mediático, nombrar los estándares PQC y ejecutar un estado de Bell. Aclara que el taller no “rompe RSA”; enseña el modelo de cómputo.

---

## Diapositiva 2: ¿Y si ya lo copiaron?

*Sección: Apertura · Tiempo sugerido: 1 min*

La pregunta incómoda Ahora

¿Y si ya
lo copiaron?

Un atacante no necesita descifrar hoy. Puede capturar hoy y esperar a tener la capacidad mañana.

“Harvest now, decrypt later” Fuente: CISA · NSA · NIST, 2023

### Notas del presentador

Pide que piensen en el dato más antiguo que su organización todavía debe mantener secreto. No se trata de predecir la fecha exacta de una máquina criptográficamente relevante: la vida útil del dato ya pone el reloj en marcha.

---

## Diapositiva 3: Ruta de 60 minutos

*Sección: Apertura · Tiempo sugerido: 0.5 min*

Ruta de 60 minutos Teoría → riesgo → acción → código

01 Intuición cuántica y Qiskit 8 min

02 La amenaza a la criptografía 10 min

03 Defensa poscuántica 8 min

04 Migración y agilidad criptográfica 7 min

05 Preguntas, fuentes y recursos 5 min

06 Taller: estado de Bell y cierre 22 min

El plan original sumaba 100 minutos; esta versión cabe en una hora. Ritmo sugerido

### Notas del presentador

Usa esta diapositiva para poner expectativas. El cronómetro integrado inicia con la tecla T. El taller conserva el bloque más largo porque es el ancla memorable.

---

## Diapositiva 4: Computación cuántica

*Sección: 01 · Fundamentos · Tiempo sugerido: 0.3 min*

01 8 min

Primero, la intuición

#### Computación cuántica

01

Superposición · entrelazamiento · arquitectura · Qiskit

### Notas del presentador

Transición: “Antes de hablar de la amenaza, necesitamos dos ideas y una arquitectura”.

---

## Diapositiva 5: Bit vs qubit

*Sección: 01 · Fundamentos · Tiempo sugerido: 1.2 min*

Bit vs qubit Modelo de información

Clásico

0 o 1

Un bit tiene un valor definido al leerlo.

Cuántico

α|0⟩ + β|1⟩

Un qubit es un estado; al medir obtenemos un resultado clásico con probabilidades.

|α|² + |β|² = 1 No es “un bit misterioso”: es amplitud, fase y medición.

### Notas del presentador

Evita decir que “el qubit es 0 y 1 al mismo tiempo” sin matiz. Las amplitudes son complejas; sus módulos al cuadrado dan probabilidades. La fase relativa, aunque invisible en una medición directa, permite interferencia.

---

## Diapositiva 6: Superposición

*Sección: 01 · Fundamentos · Tiempo sugerido: 1.4 min*

Superposición Interferencia

#### No son “muchas respuestas gratis”

El algoritmo diseña interferencia: amplifica amplitudes útiles y cancela otras antes de medir.

H|0⟩ = (|0⟩ + |1⟩)/√2

Una compuerta Hadamard prepara probabilidades 50/50 en la base computacional.

Cada shot produce solo 0 o 1; muchos shots revelan la distribución.

Idea clave: amplitudes primero, probabilidades al medir. IBM Quantum Learning

### Notas del presentador

Analogía breve: dos ondas pueden sumarse o cancelarse. El beneficio cuántico surge de estructurar esas interferencias; no de leer todos los caminos simultáneamente.

---

## Diapositiva 7: Entrelazamiento

*Sección: 01 · Fundamentos · Tiempo sugerido: 1.4 min*

Entrelazamiento Correlación no separable

|Φ⁺⟩ = (|00⟩ + |11⟩)/√2

El sistema completo tiene una descripción precisa; cada qubit por separado no tiene un estado puro independiente.

≈50%

00

≈50%

11

Resultados correlacionados. No permite enviar información más rápido que la luz.

Esto es lo que construiremos en el taller. Base Z

### Notas del presentador

Matiz importante: ver 00/11 no prueba por sí solo el entrelazamiento; una mezcla clásica puede producir el mismo histograma en Z. Para demostrarlo rigurosamente hay que medir correlaciones en bases incompatibles o realizar tomografía/testigos. En el taller diremos “evidencia de correlación compatible con el estado preparado”.

---

## Diapositiva 8: ¿Cómo se ve una computadora cuántica?

*Sección: 01 · Fundamentos · Tiempo sugerido: 1.2 min*

[Módulos criogénicos de IBM para computación cuántica tolerante a fallos](https://www.youtube.com/watch?v=wwMI6IhvwE0)

¿Cómo se ve una computadora cuántica? Hardware real

#### No es solo un chip. Es un sistema.

Criogenia, cableado de microondas, electrónica de control, QPU y cómputo clásico trabajando juntos.

La QPU opera dentro de una infraestructura diseñada para aislar y controlar estados cuánticos. [Video: IBM Research, 2026 ↗](https://www.youtube.com/watch?v=wwMI6IhvwE0)

### Notas del presentador

Deja que el video corra unos segundos antes de hablar. Señala que la estructura visible corresponde principalmente a la infraestructura criogénica y de control: el procesador cuántico es una parte pequeña del sistema. Estos módulos de IBM Research muestran trabajo orientado a escalar computación tolerante a fallos; no representan por sí solos una CRQC disponible hoy.

---

## Diapositiva 9: Ecosistema

*Sección: 01 · Fundamentos · Tiempo sugerido: 1.4 min*

Ecosistema IBM Quantum + Qiskit

##### Mapear

Expresar el problema en circuitos y observables.

##### Optimizar

Transpilar a la ISA, conectividad y compuertas de la QPU.

##### Ejecutar

Usar primitivas como Sampler o Estimator.

##### Analizar

Interpretar distribuciones, ruido e incertidumbre.

Qiskit SDK construye y transforma. IBM Quantum Platform autentica, agenda y ejecuta en QPUs.

El taller recorre las cuatro etapas. quantum.cloud.ibm.com

### Notas del presentador

Qiskit es software abierto para circuitos, operadores y primitivas. El servicio de cómputo de IBM da acceso a hardware. Evita llamar a Qiskit “lenguaje”: es un SDK/ecosistema.

---

## Diapositiva 10: La amenaza criptográfica

*Sección: 02 · Amenaza · Tiempo sugerido: 0.3 min*

02 10 min

La deuda ya existe

#### La amenaza criptográfica

02

Datos longevos · Shor · impacto real

### Notas del presentador

Transición: “El riesgo no comienza cuando aparezca la máquina; comienza cuando un dato capturado hoy siga siendo valioso entonces”.

---

## Diapositiva 11: Capturar ahora, descifrar después

*Sección: 02 · Amenaza · Tiempo sugerido: 1.6 min*

Capturar ahora, descifrar después HNDL

##### Hoy

Interceptar tráfico o robar archivos cifrados.

##### Espera

Conservar lo que mantenga valor: historiales, diseños, diplomacia.

##### CRQC

Descifrar material protegido con criptografía pública vulnerable.

La variable urgente no es solo “cuándo llega la computadora”, sino cuánto tiempo debe vivir el secreto.

CRQC = computadora cuántica criptanalíticamente relevante CISA · NSA · NIST

### Notas del presentador

CISA/NSA/NIST recomiendan inventario y hoja de ruta desde 2023. HNDL afecta principalmente confidencialidad de datos históricos; para firmas, el riesgo futuro se centra además en suplantación y actualizaciones falsas cuando exista capacidad.

---

## Diapositiva 12: Tres historias de pérdida

*Sección: 02 · Amenaza · Tiempo sugerido: 1.5 min*

Tres historias de pérdida Escenarios de riesgo, no incidentes cuánticos reportados

✚

##### Salud

Expedientes con décadas de vigencia permiten extorsión, fraude o discriminación.

confidencialidad

◇

##### Propiedad intelectual

Diseños, fórmulas y estrategia pierden ventaja competitiva años después del robo.

valor económico

⌁

##### Gobierno

Comunicaciones diplomáticas o de seguridad revelan fuentes, alianzas y decisiones.

impacto sistémico

Priorizar por sensibilidad × longevidad × exposición. Modelo de amenaza

### Notas del presentador

No presentes estos ejemplos como ataques cuánticos ocurridos. Son escenarios plausibles para el ejercicio de riesgo. Pide a la audiencia identificar cuál existe en su sector.

---

## Diapositiva 13: El mapa de impacto

*Sección: 02 · Amenaza · Tiempo sugerido: 2 min*

El mapa de impacto Shor

##### Problema matemático

Factorización entera
RSA

Logaritmo discreto
DH · DSA · ECC

→

##### Algoritmo de Shor

Tiempo polinómico en una computadora cuántica tolerante a fallos suficientemente grande.

Impacta intercambio de claves, cifrado asimétrico y firmas. Shor, FOCS 1994

### Notas del presentador

RSA depende de la dificultad de factorizar. ECC y Diffie-Hellman dependen de variantes del logaritmo discreto. Shor resuelve ambas familias. Precisión: TLS usa típicamente RSA/ECDSA para autenticación y ECDHE para acuerdo; el contenido se cifra simétricamente después.

---

## Diapositiva 14: Shor sin humo

*Sección: 02 · Amenaza · Tiempo sugerido: 1.8 min*

Shor sin humo Intuición

1

##### Reformular

Convertir factorización/log discreto en búsqueda de periodo.

2

##### Superponer

Evaluar coherentemente una función periódica.

3

##### Interferir

La QFT concentra amplitud en información del periodo.

4

##### Recuperar

Posprocesamiento clásico deriva factores o la clave.

La ventaja viene de la estructura algebraica, no de “probar todas las claves”. QFT = transformada cuántica de Fourier

### Notas del presentador

Esta explicación basta para audiencia general. Si preguntan: la parte cuántica estima un periodo; fracciones continuas y máximo común divisor completan la factorización. No intentes prometer fechas o números fijos de qubits.

---

## Diapositiva 15: Calibrar el riesgo

*Sección: 02 · Amenaza · Tiempo sugerido: 1.8 min*

Calibrar el riesgo Ni pánico ni espera

#### Hoy no existe una CRQC pública

El Bell state de dos qubits no escala mágicamente a romper RSA‑2048.

Sí: inventariar, probar PQC, exigir hoja de ruta a proveedores y diseñar agilidad.

No: afirmar que “todo el cifrado está roto”. Shor amenaza clave pública; Grover ofrece una aceleración cuadrática sobre búsqueda simétrica.

Práctica común: claves simétricas robustas (p. ej., AES‑256) y migración de RSA/ECC hacia PQC.

Riesgo futuro + migración lenta = trabajo presente. NIST PQC

### Notas del presentador

Un ataque de Grover ideal reduce aproximadamente de 2^k a 2^(k/2) consultas, pero con costos físicos significativos. Evita simplificar a “AES‑128 roto”; la recomendación práctica depende del perfil y estándares aplicables.

---

## Diapositiva 16: Criptografía poscuántica

*Sección: 03 · Defensa · Tiempo sugerido: 0.3 min*

03 8 min

Defender sin una QPU

#### Criptografía poscuántica

03

Algoritmos clásicos · nuevos supuestos · estándares finales

### Notas del presentador

Transición: “La defensa principal no requiere computadoras cuánticas”.

---

## Diapositiva 17: PQC en una frase

*Sección: 03 · Defensa · Tiempo sugerido: 1.5 min*

PQC en una frase Criptografía clásica

Nuevas matemáticas.
Las mismas computadoras.

##### Resiste

Ataques conocidos de computadoras clásicas y cuánticas.

##### Reemplaza

Acuerdo/encapsulación de claves y firmas vulnerables.

##### No es QKD

No requiere enlaces cuánticos ni hardware fotónico especial.

PQC suele combinarse con cifrado simétrico para los datos. NIST

### Notas del presentador

Diferencia KEM/cifrado: ML-KEM establece un secreto compartido; un AEAD simétrico cifra los datos. Diferencia PQC/QKD: PQC es software/protocolos clásicos; QKD distribuye claves mediante propiedades físicas y tiene otro modelo operativo.

---

## Diapositiva 18: Estándares NIST finalizados

*Sección: 03 · Defensa · Tiempo sugerido: 2.4 min*

Estándares NIST finalizados 13 ago 2024

[FIPS 203 — consultar estándar oficial](https://doi.org/10.6028/NIST.FIPS.203)

##### ML‑KEM

Encapsulación de claves basada en retículas modulares. Principal opción para establecer secretos.

antes Kyber

[FIPS 204 — consultar estándar oficial](https://doi.org/10.6028/NIST.FIPS.204)

##### ML‑DSA

Firma digital basada en retículas modulares. Principal estándar de firmas PQC.

antes Dilithium

[FIPS 205 — consultar estándar oficial](https://doi.org/10.6028/NIST.FIPS.205)

##### SLH‑DSA

Firma sin estado basada en hashes. Alternativa con supuestos matemáticos distintos.

antes SPHINCS+

NIST: listos para uso; no es necesario esperar futuros estándares. FIPS 203 · 204 · 205

### Notas del presentador

ML significa “Module-Lattice” (retículas modulares): ML-KEM es un mecanismo de encapsulación de claves y ML-DSA es un algoritmo de firma digital. No llames a los tres “algoritmos de cifrado”: uno es KEM y dos son firmas. FIPS 206/FN-DSA sigue una ruta separada. HQC fue seleccionado en 2025 como KEM de respaldo, pero no reemplaza la recomendación de empezar con los estándares finales.

---

## Diapositiva 19: Cómo encaja en un sistema

*Sección: 03 · Defensa · Tiempo sugerido: 1.8 min*

Cómo encaja en un sistema Patrón híbrido

##### Identidad

ML‑DSA / SLH‑DSA autentica artefactos y mensajes.

›

##### Secreto

ML‑KEM encapsula una clave compartida.

›

##### Datos

AES‑GCM o ChaCha20‑Poly1305 cifra el volumen.

Durante la transición, combinaciones híbridas clásica + PQC reducen el riesgo de depender de una sola familia.

La composición del protocolo importa tanto como el algoritmo. Validar bibliotecas y perfiles aprobados

### Notas del presentador

“Híbrido” debe estar definido por un protocolo: ambos secretos deben combinarse correctamente. No inventar concatenaciones. Usar implementaciones de proveedores y perfiles estandarizados; probar tamaño de mensajes, latencia, certificados, HSM y observabilidad.

---

## Diapositiva 20: Costo de cambiar

*Sección: 03 · Defensa · Tiempo sugerido: 1.5 min*

Costo de cambiar La capa olvidada

PQC no es
buscar y reemplazar.

- Claves, firmas y certificados más grandes

- Protocolos, MTU, almacenamiento y rendimiento

- PKI, HSM, firmware, arranque seguro y CI/CD

- Dependencias embebidas y terceros

- Interoperabilidad, rollback y telemetría

Por eso la migración empieza con descubrimiento. CISA Quantum‑Readiness

### Notas del presentador

Da un ejemplo: cambiar una firma afecta certificados, validadores, formato de artefactos, dispositivos con buffers pequeños y procesos de recuperación. El inventario debe incluir dónde, para qué y por cuánto tiempo se usa criptografía.

---

## Diapositiva 21: Migración y agilidad

*Sección: 04 · Migración · Tiempo sugerido: 0.3 min*

04 7 min

Convertir incertidumbre en decisiones

#### Migración y agilidad

04

Inventario · Mosca · hoja de ruta

### Notas del presentador

Transición: “No podemos gestionar una fecha incierta; sí podemos gestionar exposición, dependencia y tiempo de migración”.

---

## Diapositiva 22: Agilidad criptográfica

*Sección: 04 · Migración · Tiempo sugerido: 1.6 min*

Agilidad criptográfica Capacidad, no producto

#### Cambiar sin reconstruir todo

Políticas, interfaces y datos permiten sustituir algoritmos, parámetros, claves y proveedores con seguridad.

- Descubrible: SBOM/CBOM y dueños claros

- Configurable: algoritmos fuera del código de negocio

- Observable: saber qué negoció cada conexión

- Probable: suites duales, canarios y rollback

- Gobernable: políticas y fechas de retiro

Meta: reducir el tiempo Y de la desigualdad de Mosca. Crypto agility

### Notas del presentador

La agilidad no significa permitir cualquier algoritmo; significa poder cambiar dentro de una política segura. Un “toggle” sin inventario, telemetría ni pruebas puede aumentar el riesgo.

---

## Diapositiva 23: Desigualdad de Mosca

*Sección: 04 · Migración · Tiempo sugerido: 2.5 min*

Desigualdad de Mosca X + Y > Z → exposición

X + Y > Z

- X vida secreta del dato

- Y tiempo para migrar

- Z tiempo hasta una CRQC

X · vida del dato 10 años

Y · migración 5 años

Z · llegada CRQC 12 años

15 > 12 · La confidencialidad entra en zona de riesgo.

Herramienta de priorización, no pronóstico exacto. Mosca, 2015

### Notas del presentador

Haz que la audiencia proponga X e Y. Z es incierto: trabaja con escenarios conservador/base/optimista. Si X+Y supera Z, material capturado durante la migración puede sobrevivir hasta el momento de descifrado. Para firmas y autenticidad, adaptar el análisis a la vida útil de la confianza/artefacto.

---

## Diapositiva 24: Primeros 90 días

*Sección: 04 · Migración · Tiempo sugerido: 2.6 min*

Primeros 90 días Hoja de ruta

01

##### Patrocinar

Equipo, alcance, riesgo aceptable y datos longevos.

02

##### Inventariar

Algoritmo, uso, ubicación, dueño, proveedor y fecha de retiro.

03

##### Priorizar

X + Y vs escenarios Z; exposición externa y criticidad.

04

##### Pilotar

TLS/VPN/PKI/código firmado en laboratorio; medir y documentar.

Pregunta a cada proveedor: qué, cuándo, cómo y con qué rollback. CISA · NIST

### Notas del presentador

Entregables: registro criptográfico, mapa de dependencias, matriz de riesgo, criterios de compra y dos pilotos. La primera meta no es migrar todo: es obtener visibilidad y bajar incertidumbre.

---

## Diapositiva 25: ¿Qué dato no puede esperar?

*Sección: 05 · Preguntas y recursos · Tiempo sugerido: 3.8 min*

05 · Preguntas 5 min

¿Qué dato
no puede
esperar?

*Visual: Ilustración de dos personas colaborando.*

Guía de estudio y notebook incluidos en esta carpeta. Gracias

### Notas del presentador

Invita preguntas sobre tres carriles: tecnología cuántica, riesgo/estrategia y código. Si no hay preguntas, usa la pregunta de la diapositiva para pedir un ejemplo del público.

---

## Diapositiva 26: Fuentes esenciales

*Sección: Apéndice · Tiempo sugerido: 0 min*

Fuentes esenciales Apéndice

##### Normas y migración

- NIST, FIPS 203 / 204 / 205 (2024)

- NIST, “Releases First 3 Finalized PQC Standards” (2024; act. 2025)

- CISA/NSA/NIST, “Quantum‑Readiness” (2023)

- M. Mosca, IACR ePrint 2015/1075

- P. Shor, FOCS 1994, DOI 10.1109/SFCS.1994.365700

##### Qiskit y taller

- IBM Quantum Docs, “Run your first circuit on hardware”

- IBM Quantum Docs, “Initialize the service in an untrusted environment”

- IBM Quantum Docs, “Save your login credentials”

- Qiskit Advocate Library, QC/Qiskit Foundations (2025)

- Consulta la guía de estudio para URLs y notas completas.

Fuentes consultadas el 6 oct 2026. Apéndice · fuera del tiempo

### Notas del presentador

Esta diapositiva no forma parte del minuto a minuto; úsala para responder o dejarla como respaldo.

---

## Diapositiva 27: Tu siguiente circuito empieza aquí

*Sección: Comunidad · Tiempo sugerido: 0 min*

Tu siguiente circuito empieza aquí Entrada gratuita

28–29 OCT · GUADALAJARA + ONLINE

#### Qiskit Fall Fest GDL 2026

Dos días de charlas, talleres y laboratorios cuánticos para aprender, construir y conectar.

28 oct · AstraZeneca GITC
29 oct · En línea
150 lugares presenciales

[Código QR para registrarse al Qiskit Fall Fest GDL 2026](https://quantum-guild-gdl.github.io/qiskit_fall_fest_gdl/)

Escanea y reserva tu lugar

Zapopan, Jalisco · Evento comunitario sin costo

quantum-guild-gdl.github.io/qiskit_fall_fest_gdl/ · Nos vemos en el Fall Fest

### Notas del presentador

Invita a la audiencia a continuar aprendiendo en comunidad. El 28 de octubre es presencial en AstraZeneca GITC Guadalajara, en Zapopan; el 29 de octubre es en línea. Ambas modalidades son gratuitas y el acceso presencial está limitado a 150 lugares. Deja unos segundos para escanear el QR.

---

## Diapositiva 28: Llévate la presentación

*Sección: Recursos · Tiempo sugerido: 0 min*

Llévate la presentación Escanea

#### Continúa explorando

Abre la presentación, consulta las fuentes y descarga el notebook del estado de Bell.

brun3y.github.io/quantum-and-cybersecurity/

*Visual: Código QR para abrir la presentación en GitHub Pages.*

Presentación pública · GitHub Pages Notebook incluido

### Notas del presentador

Deja esta diapositiva proyectada al terminar. El QR abre la versión pública del deck; desde el repositorio los asistentes también pueden descargar el notebook.

---

## Diapositiva 29: Taller: estado de Bell

*Sección: 06 · Taller · Tiempo sugerido: 0.3 min*

06 22 min

De la abstracción al hardware

#### Taller: estado de Bell

06

Colab · Qiskit · simulador · QPU real

### Notas del presentador

Ten abierto el notebook antes de la charla. Ejecuta el simulador primero para garantizar el resultado. El hardware real es bonus sujeto a acceso, cuota y cola.

---

## Diapositiva 30: Objetivo observable

*Sección: 06 · Taller · Tiempo sugerido: 1.3 min*

Objetivo observable Φ⁺

|00⟩ → H → CX
→ (|00⟩+|11⟩)/√2

#### Dos puertas. Una correlación.

Esperamos ≈50% 00 y ≈50% 11.

El hardware real añade resultados espurios por ruido.

Corrección del notebook original: sin X(1). Estado de Bell Φ⁺

### Notas del presentador

El notebook compartido incluía X(1), que produce Ψ+ y resultados 01/10. Esta versión elimina X para que coincida con 00/11. Si quieres mostrar ambos, ejecuta primero Φ+ y luego agrega X(1) antes de H.

---

## Diapositiva 31: 0 · Preparación

*Sección: 06 · Taller · Tiempo sugerido: 2 min*

0 · Preparación Google Colab

#### Abre y copia

[Notebook compartido ↗](https://colab.research.google.com/drive/1LM8asOQzPBiZdKB0A8eIs1a5qil_V29X)

Archivo → Guardar una copia en Drive. Ejecuta las celdas en orden.

```python
# Celda 1 · instalar
!pip install -q \
  'qiskit[visualization]' \
  qiskit-aer \
  qiskit-ibm-runtime

# Si Colab lo pide:
# Entorno de ejecución → Reiniciar sesión
```

Plan B: el simulador funciona sin cuenta de IBM. 2 min

### Notas del presentador

Pide a asistentes instalar mientras explicas la cuenta. Para un taller estable, entrega también el notebook local corregido incluido con estos materiales.

---

## Diapositiva 32: 1 · API key sin exponerla

*Sección: 06 · Taller · Tiempo sugerido: 3 min*

1 · API key sin exponerla IBM Quantum Platform

1. Entra a quantum.cloud.ibm.com e inicia sesión.

2. Crea una instancia en Instances (plan disponible).

3. En Home/Dashboard, crea y copia tu API key de 44 caracteres.

4. Opcional: copia el CRN de la instancia.

5. En Colab, abre 🔑 Secrets y crea IBM_QUANTUM_API_KEY. Activa acceso del notebook.

Nunca pegues la clave en una celda ni la publiques. IBM considera Colab un entorno no confiable: revoca/rota la clave al terminar si fue temporal.

```python
from google.colab import userdata
api_key = userdata.get("IBM_QUANTUM_API_KEY")
```

Guía oficial: IBM · “Initialize the service in an untrusted environment” 3 min

### Notas del presentador

IBM advierte que en una máquina pública o nube externa se debe evitar persistir credenciales y cambiar la clave tras el uso. Colab Secrets evita que aparezca en el notebook, pero no convierte el entorno en confiable. Si usan CRN, guárdenlo como un segundo secret IBM_QUANTUM_CRN.

---

## Diapositiva 33: 2 · Construir Φ⁺

*Sección: 06 · Taller · Tiempo sugerido: 2.5 min*

2 · Construir Φ⁺ Qiskit

```python
from qiskit import QuantumCircuit

bell = QuantumCircuit(2)
bell.h(0)        # superposición
bell.cx(0, 1)    # entrelazamiento
bell.measure_all()

bell.draw("mpl")
```

q₀

q₁

H

Orden: H crea amplitudes; CX correlaciona; medir produce bits. 2.5 min

### Notas del presentador

Recorre estado por estado: |00⟩ → (|00⟩+|10⟩)/√2 en convención conceptual q0 primero; CNOT → Bell Φ+. Advierte que Qiskit muestra bitstrings en orden clásico de mayor a menor índice; como 00/11 son simétricos, aquí no confunde el resultado.

---

## Diapositiva 34: 3 · Simular primero

*Sección: 06 · Taller · Tiempo sugerido: 3 min*

3 · Simular primero Sin cola · sin credenciales

```python
from qiskit_aer import AerSimulator
from qiskit import transpile
from qiskit.visualization import plot_histogram

sim = AerSimulator()
compiled = transpile(bell, sim)
result = sim.run(compiled, shots=1024).result()
counts_sim = result.get_counts()

print(counts_sim)
plot_histogram(counts_sim)
```

≈512

00

0

01

0

10

≈512

11

No tiene que ser exactamente 512/512: el muestreo fluctúa.

Checkpoint: si aparecen 01/10, revisa si quedó X(1). 3 min

### Notas del presentador

Este bloque es deliberadamente simple y estable. El simulador ideal confirma lógica. 1024 shots da variación binomial; lo importante es correlación y ausencia ideal de 01/10.

---

## Diapositiva 35: 4 · Ejecutar en una QPU real

*Sección: 06 · Taller · Tiempo sugerido: 4 min*

4 · Ejecutar en una QPU real IBM Quantum Compute

```python
from qiskit_ibm_runtime import (
  QiskitRuntimeService, SamplerV2 as Sampler
)
from qiskit.transpiler import generate_preset_pass_manager

service = QiskitRuntimeService(token=api_key)
backend = service.least_busy(
  operational=True, simulator=False
)

pm = generate_preset_pass_manager(
  backend=backend, optimization_level=1
)
isa_bell = pm.run(bell)

sampler = Sampler(mode=backend)
job = sampler.run([isa_bell], shots=1024)
print("Job:", job.job_id())
```

#### Mapear → optimizar → ejecutar

El transpiler adapta nuestras puertas a la conectividad y al conjunto de instrucciones del dispositivo elegido.

La cola, cuota o disponibilidad pueden impedir el vivo. Conserva el ID del trabajo y usa el simulador como ruta segura.

Si usas CRN: QiskitRuntimeService(token=api_key, instance=crn) 4 min + cola

### Notas del presentador

Antes de enviar, imprime backend.name. No fijes un backend en el material: la flota cambia. Guardar job_id permite recuperar después con service.job(job_id). La guía oficial usa Qiskit Patterns y least_busy.

---

## Diapositiva 36: 5 · Leer el resultado

*Sección: 06 · Taller · Tiempo sugerido: 2.5 min*

5 · Leer el resultado SamplerV2

```python
pub_result = job.result()[0]
counts_qpu = pub_result.data.meas.get_counts()

print(counts_qpu)
plot_histogram(
  [counts_sim, counts_qpu],
  legend=["Simulador", "QPU"]
)
```

48%

00

3%

01

2%

10

47%

11

Ilustrativo: tus porcentajes dependerán de calibración, mapeo y shots.

Ruido ≠ fracaso: es el dispositivo físico entrando en escena. 2.5 min

### Notas del presentador

Errores de lectura y de compuertas producen algo de 01/10. Evita decir “nunca” en hardware real. Un histograma en Z es una demostración pedagógica de correlación; la prueba rigurosa del entrelazamiento requiere más bases.

---

## Diapositiva 37: Plan de contingencia en vivo

*Sección: 06 · Taller · Tiempo sugerido: 3.4 min*

Plan de contingencia en vivo La demo no manda

##### Falla instalación

Reinicia sesión; ejecuta imports desde cero. Verifica versiones.

##### Falla autenticación

Confirma acceso del secret, API key activa e instancia/región.

##### Hay cola

Muestra job ID, corre Aer y enseña una captura previa de QPU.

##### No hay resultados

Recupera después con service.job(job_id).

##### Salen 01/10

Pocos: ruido. Cerca de 50/50: probablemente quedó X(1).

##### Pregunta difícil

El histograma Z muestra correlación, no certifica por sí solo entrelazamiento.

Ensaya con el mismo navegador, cuenta y red del evento. Checklist del facilitador

### Notas del presentador

Cierra el taller repitiendo el pipeline: circuito, transpilación, primitive, resultado. Pide a una persona describir por qué el simulador y la QPU difieren.

---

## Diapositiva 38: Tres ideas para llevar

*Sección: Cierre · Tiempo sugerido: 1.2 min*

Tres ideas para llevar Cierre

01

La amenaza es a la criptografía pública y al tiempo de vida de los datos.

02

La defensa ya tiene estándares: ML‑KEM, ML‑DSA y SLH‑DSA.

03

La decisión de hoy es inventario + agilidad + pilotos, no adivinar una fecha.

Y dos puertas bastaron para tocar una QPU real. De la teoría a la acción

### Notas del presentador

Frase final: “No necesitamos saber el día exacto en que llegue una CRQC para saber qué debemos hacer el lunes”.

---

# Guía práctica: estado de Bell Φ⁺

A continuación se reproduce íntegramente el contenido fuente del notebook incluido con la presentación. Las celdas están en su orden original.

# Estado de Bell Φ⁺ — simulador y QPU real de IBM

Taller para la charla **Ciberseguridad en la era cuántica**. Ejecuta las celdas en orden. El circuito prepara $|\Phi^+\rangle=(|00\rangle+|11\rangle)/\sqrt{2}$.

> Seguridad: no pegues una API key en una celda. Usa Colab Secrets y revoca/rota una clave temporal al terminar.

## 1. Instalar dependencias
Si Colab lo solicita después, reinicia la sesión y continúa desde la siguiente celda.

### Celda de código 3

```python
!pip install -q 'qiskit[visualization]' qiskit-aer qiskit-ibm-runtime
```

## 2. Importar y verificar versiones

### Celda de código 5

```python
import qiskit, qiskit_aer, qiskit_ibm_runtime
from qiskit import QuantumCircuit, transpile
from qiskit.visualization import plot_histogram
from qiskit_aer import AerSimulator
from qiskit.transpiler import generate_preset_pass_manager
from qiskit_ibm_runtime import QiskitRuntimeService, SamplerV2 as Sampler

print('qiskit:', qiskit.__version__)
print('qiskit-aer:', qiskit_aer.__version__)
print('qiskit-ibm-runtime:', qiskit_ibm_runtime.__version__)
```

## 3. Construir el estado de Bell Φ⁺

1. Iniciamos en $|00\rangle$.
2. H sobre q₀ crea superposición.
3. CX correlaciona q₁ con q₀.
4. Medimos ambos qubits.

Esperamos aproximadamente 50% `00` y 50% `11`.

### Celda de código 7

```python
bell = QuantumCircuit(2)
bell.h(0)       # Superposición
bell.cx(0, 1)   # Entrelazamiento
bell.measure_all()
bell.draw('mpl')
```

## 4. Ejecutar primero en el simulador local
Este checkpoint no requiere cuenta, API key ni cola.

### Celda de código 9

```python
simulator = AerSimulator()
compiled = transpile(bell, simulator)
result_sim = simulator.run(compiled, shots=1024).result()
counts_sim = result_sim.get_counts()

print(counts_sim)
plot_histogram(counts_sim)
```

## 5. Preparar acceso seguro a IBM Quantum

1. Entra a https://quantum.cloud.ibm.com/ y crea/selecciona una instancia.
2. Desde Home/Dashboard crea una API key y cópiala.
3. En la barra lateral de Colab abre **Secrets** (🔑).
4. Crea `IBM_QUANTUM_API_KEY` y habilita acceso del notebook.
5. Opcional: guarda el CRN como `IBM_QUANTUM_CRN`.

> IBM considera una nube externa un entorno no confiable. No uses `save_account()` aquí ni publiques el secreto.

### Celda de código 11

```python
from google.colab import userdata

api_key = userdata.get('IBM_QUANTUM_API_KEY')
service = QiskitRuntimeService(token=api_key)

# Si necesitas una instancia específica, reemplaza la línea anterior por:
# crn = userdata.get('IBM_QUANTUM_CRN')
# service = QiskitRuntimeService(token=api_key, instance=crn)
```

## 6. Elegir una QPU, transpilar y enviar
Guarda el Job ID. La cola y la cuota dependen de tu plan.

### Celda de código 13

```python
backend = service.least_busy(operational=True, simulator=False)
print('Backend:', backend.name)

pm = generate_preset_pass_manager(backend=backend, optimization_level=1)
isa_bell = pm.run(bell)

sampler = Sampler(mode=backend)
job = sampler.run([isa_bell], shots=1024)
job_id = job.job_id()
print('Job ID:', job_id)
```

## 7. Recuperar y comparar los resultados
En una QPU real pueden aparecer `01` y `10` por ruido.

### Celda de código 15

```python
pub_result = job.result()[0]
counts_qpu = pub_result.data.meas.get_counts()

print(counts_qpu)
plot_histogram(
    [counts_sim, counts_qpu],
    legend=['Simulador', 'QPU real'],
)
```

## 8. Recuperar un trabajo anterior (opcional)

### Celda de código 17

```python
# Sustituye por un ID guardado si cerraste la sesión:
# old_job = service.job('TU_JOB_ID')
# old_counts = old_job.result()[0].data.meas.get_counts()
# plot_histogram(old_counts)
```

## Interpretación

- El simulador ideal produce solo `00` y `11` (con fluctuación estadística).
- La QPU puede producir algunos `01`/`10` por errores de puertas, lectura y decoherencia.
- Un histograma en la base Z muestra correlación compatible con Φ⁺, pero no certifica por sí solo el entrelazamiento.
- Si ves casi 50% `01` y 50% `10`, revisa si agregaste `x(1)`: eso prepara Ψ⁺.

---

## Fin del documento

Fuente consolidada a partir de README.md, presentacion/index.html y presentacion/taller_estado_bell.ipynb.
