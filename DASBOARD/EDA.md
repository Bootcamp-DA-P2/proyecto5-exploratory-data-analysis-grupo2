# Informe de Diagnóstico y Enfoque Analítico (EDA COVID-19)

## 1. Diagnóstico de la Estructura y Tipos de Datos (.info())
Al cargar las dos fuentes principales de datos (all-states-history.csv y national-history.csv), se observa una diferencia crítica en las dimensiones y los propósitos analíticos:

* **df_states (Datos por Estado):** Cuenta con 20,780 registros y 41 columnas. Es un conjunto de datos tridimensional (Fecha x Estado x Métricas). Los tipos de datos se dividen en su mayoría en valores decimales (float64 para métricas acumuladas debido a la presencia de nulos) y enteros (int64 para los incrementos diarios).
* **df_national (Datos Nacionales):** Cuenta con 420 registros y 17 columnas. Es una serie temporal limpia y consolidada a nivel país día a día.

### Enfoque Analítico para el EDA
La columna "date" es leída inicialmente como tipo objeto (object). El primer paso obligado de limpieza consiste en transformar esta columna al tipo nativo de tiempo (pd.to_datetime(df['date'])) para permitir la segmentación correcta por meses o semanas epidemiológicas.


## 2. Gestión de Datos Ausentes (NaN)
La salida de .info() revela el comportamiento del reporte de datos públicos durante la pandemia:

* Variables genéricas acumuladas como "death" (19,930 valores no nulos) o "positive" (20,592 valores no nulos) están prácticamente completas en comparación con el total de 20,780 filas.
* Variables específicas sufren de una severa ausencia de datos: por ejemplo, "deathConfirmed" solo tiene 9,422 registros, "deathProbable" 7,593, y "negativeTestsPeopleAntibody" apenas cuenta con 972 registros.

### Enfoque Analítico para el EDA
No todos los estados federados recopilaban o desglosaban la información con los mismos criterios. Algunos estados no informaron de pruebas de antígenos o anticuerpos específicas, o no diferenciaban de forma retroactiva las muertes probables de las confirmadas. Por lo tanto, se justifica centrar los análisis e hipótesis en las variables globales (death, positive, totalTestResults) para no perder poder estadístico ni sesgar la muestra territorial.


## 3. Diagnóstico de Anomalías y Outliers (.describe())
Los estadísticos descriptivos muestran anomalías extremas introducidas por errores de reporte o ajustes retroactivos de las agencias de salud:

* **Valores Mínimos Negativos:** En df_states, la columna "hospitalizedIncrease" muestra un valor mínimo de -12,257, y en df_national la columna "hospitalizedIncrease" marca un mínimo de -2,858. Del mismo modo, "deathIncrease" llega a registrar un mínimo de -201.
* **Significado Biológico/Médico:** Estas cifras representan inconsistencias administrativas, ya que los incrementos diarios acumulados netos no pueden decrecer de forma natural en tales magnitudes.
* **Dispersiones Masivas (Desviaciones Estándar):** En df_states, la media de "positiveIncrease" es de aproximadamente 1,328 casos diarios, pero su desviación estándar es de 4,743 con un máximo de 53,749. Esto indica una distribución con colas sumamente largas y presencia de picos acumulados por retrasos de reporte en fines de semana.

### Enfoque Analítico para el EDA
El dataset original contiene ruido administrativo (días donde un estado sumaba casos atrasados de golpe o corregía dobles conteos restando valores). Para un análisis de tendencias temporales real, el EDA requiere la aplicación de un suavizado estadístico, como promedios móviles de 7 días, para diluir el impacto de estos desfases semanales.


## 4. Justificación de Modelos y Librerías Estadísticas
Para el desarrollo del análisis se incorporaron los siguientes módulos avanzados:

* **scipy.stats (stats):** Su uso se justifica para validar matemáticamente la forma de las distribuciones mediante tests de normalidad (como Shapiro-Wilk o D'Agostino) y la graficación de diagramas Q-Q Plot. Como se observa en los descriptivos (donde la mediana está lejos de la media y los máximos son elevados), las variables epidemiológicas no siguen una distribución normal, sino distribuciones asimétricas positivas (sesgadas a la derecha).
* **statsmodels.formula.api (smf):** La inclusión de modelos de fórmulas lineales (smf.ols) permite evaluar relaciones de causa-efecto de manera formal. Ayuda a estructurar regresiones y determinar el porcentaje en que se incrementaban estadísticamente las camas de UCI ocupadas (inIcuCurrently) o el uso de ventiladores (onVentilatorCurrently) por cada unidad de incremento en los casos positivos confirmados.