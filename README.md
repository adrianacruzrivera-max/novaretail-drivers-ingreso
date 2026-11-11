# NovaRetail+ · Factores de comportamiento asociados al ingreso del cliente

Análisis exploratorio y correlacional para identificar qué comportamientos de los clientes de una plataforma de e-commerce latinoamericana se asocian con el ingreso que generan, sin confundir correlación con causalidad.

## Pregunta de negocio

El equipo de **Crecimiento y retención** de NovaRetail+ quería saber: **¿qué factores del comportamiento del cliente están más fuertemente asociados con el ingreso anual generado?**

## Datos

- **15,000 clientes** y **12 variables** (registro de 2024), sin valores nulos ni duplicados.
- Variables numéricas: edad, nivel de ingreso, visitas y compras del mes, gasto publicitario dirigido, satisfacción e ingreso generado (métrica objetivo).
- Variables binarias: membresía premium y abandono.
- Variables categóricas: tipo de dispositivo y región.

> El dataset fue provisto por el bootcamp de TripleTen y no se incluye en este repositorio.

## Metodología

1. **Preparación y diagnóstico:** revisión de tipos (corrección de `edad`), distribuciones, desbalances y supuestos documentados.
2. **Exploración visual:** heatmap de correlaciones, pairplot sobre una muestra de 2,000 clientes y scatterplots de los pares clave.
3. **Coeficientes según el tipo de variable:**
   - Pearson y Spearman para numéricas.
   - Punto-biserial para binaria vs. numérica.
   - V de Cramér para categóricas.
4. **Detección de correlaciones engañosas:**
   - Verificación de *leakage* (fuga de información) entre compras e ingreso.
   - Correlaciones dentro de segmentos (paradoja de Simpson).
   - Control por nivel de actividad.

## Hallazgos principales

| # | Hallazgo | Evidencia clave |
|---|---|---|
| 1 | Las **visitas** son el factor de comportamiento más asociado con el ingreso | r = 0.34, estable en todos los segmentos |
| 2 | La relación **gasto publicitario–ingreso** es débil y parece explicarse por las visitas | r = 0.20 en total, pero 0.00–0.07 entre clientes con un nivel de visitas parecido |
| 3 | Los clientes **premium** generan más ingreso y abandonan menos, aunque con asociaciones débiles | Ingreso de 44.6 vs. 35.3; abandono del 4.4 % vs. 16.8 % |
| 4 | Edad, nivel de ingreso, satisfacción, abandono, región y dispositivo **no se asocian** con el ingreso | \|r\| < 0.1 |
| 5 | La correlación más alta (**compras–ingreso**, r = 0.97) es un artefacto de cómo se construye la métrica | 0 compras = 0 ingreso en los 4,567 casos; ~30 de ingreso por compra |

Ningún hallazgo se presenta como causal. Cada uno incluye qué **no** se puede afirmar con estos datos, por ejemplo la causalidad inversa, la autoselección en premium o la asignación no aleatoria de la publicidad.

## Recomendaciones

- Usar las visitas como **señal temprana** para identificar clientes de alto valor.
- Medir el efecto real de la publicidad dirigida con una **prueba A/B** con grupo de control.
- Evaluar el programa premium con un **experimento controlado** antes de promoverlo masivamente.
- **Confirmar la definición y el periodo de `ingreso_anual`** con el equipo de datos, ya que su escala sugiere que podría ser mensual.

## Herramientas

Python · pandas · NumPy · SciPy (`pointbiserialr`, `chi2_contingency`) · seaborn · matplotlib · Jupyter

## Estructura del repositorio

- `NovaRetail_drivers_ingreso.ipynb` — Análisis completo con gráficos y conclusiones
- `README.md` — Este resumen
