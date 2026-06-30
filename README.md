# Laboratorio 4: Introducción a Microsoft Fabric y Power BI

## 1. Teoría: Introducción a la Analítica de Datos en Azure (Ruta de Aprendizaje 4)

El análisis de datos es el proceso de examinar, transformar y modelar datos para descubrir información útil, extraer conclusiones y respaldar la toma de decisiones. Esta sección resume los conceptos fundamentales cubiertos en el módulo de Microsoft Learn sobre analítica en Azure.

### 1.1 Tipos de Análisis de Datos
Las organizaciones utilizan los datos para responder a diferentes tipos de preguntas empresariales. La analítica se divide en cuatro categorías principales:

1. **Análisis Descriptivo (¿Qué ocurrió?):** Se centra en resumir los datos históricos para entender el estado actual o pasado. Ejemplo: Informes de ventas mensuales.
2. **Análisis Diagnóstico (¿Por qué ocurrió?):** Explora los datos históricos para identificar las causas fundamentales de una anomalía o tendencia. Ejemplo: Investigar por qué cayeron las ventas en una región específica cruzando datos de clima y campañas de marketing.
3. **Análisis Predictivo (¿Qué es probable que ocurra?):** Utiliza modelos estadísticos y de Machine Learning (Machine Learning) para pronosticar eventos futuros basándose en patrones pasados. Ejemplo: Predecir el inventario necesario para el próximo trimestre.
4. **Análisis Prescriptivo (¿Qué acciones debemos tomar?):** Sugiere acciones específicas basadas en los modelos predictivos para optimizar los resultados. Ejemplo: Ajustar automáticamente los precios en tiempo real según la demanda.

### 1.2 Procesamiento de Datos: Lotes vs. Streaming
La ingesta y el procesamiento de los datos hacia los almacenes analíticos se puede realizar de dos formas:

* **Procesamiento por lotes (Batch):** Los datos se recopilan a lo largo del tiempo y se procesan juntos en grupos a intervalos programados (ej. cada noche). Es eficiente para grandes volúmenes donde la inmediatez no es crítica.
* **Procesamiento en flujo (Streaming):** Los datos se procesan en tiempo real o casi en tiempo real a medida que se generan (ej. telemetría de sensores, registros de servidores web, transacciones financieras).

### 1.3 Arquitecturas de Almacenamiento Analítico
Para manejar el análisis a gran escala, Azure ofrece arquitecturas especializadas, superando las limitaciones de las bases de datos relacionales tradicionales:

* **Data Warehouse (Almacenamiento de datos):** Base de datos relacional optimizada para cargas de trabajo analíticas (OLAP). Los datos están altamente estructurados (esquema al escribir) y provienen de múltiples fuentes.
* **Data Lake (Lago de datos):** Almacén que guarda cantidades masivas de datos crudos en su formato nativo (estructurado, semiestructurado o no estructurado). Usa un enfoque de "esquema al leer".
* **Data Lakehouse:** Una arquitectura moderna que combina la flexibilidad, el bajo costo y la escalabilidad de un Data Lake con las características de gestión de datos y transacciones ACID de un Data Warehouse (utilizando formatos como Delta Lake).

### 1.4 Servicios Clave de Analítica en Azure y Microsoft Fabric
* **Microsoft Fabric:** Es una plataforma unificada SaaS (Software as a Service) que agrupa toda la analítica de una empresa (Data Engineering, Data Factory, Data Science, Data Warehouse, Real-Time Analytics y Power BI) sobre una base de datos de lago compartida llamada **OneLake**.
* **Azure Synapse Analytics:** Servicio de análisis ilimitado que reúne la integración de datos, el almacenamiento de datos empresariales y el análisis de Big Data (usando pools de SQL y Apache Spark).
* **Power BI:** Plataforma interactiva de visualización de datos e inteligencia empresarial que se conecta directamente a estas fuentes masivas (como OneLake o Synapse) para generar paneles y reportes.

---

## 2. Laboratorio 4: Ejercicios Prácticos

A continuación se detalla la resolución de los ejercicios correspondientes a la integración y visualización de datos.

---

### Ejercicio 1: Aprovisionamiento del entorno analítico en Microsoft Fabric
**Objetivo:** Establecer un área de trabajo unificada y un Lakehouse como repositorio central.

1. Iniciar sesión en el portal de Microsoft Fabric (`app.fabric.microsoft.com`).
   > **<img width="1896" height="932" alt="app fabric microsoft com" src="https://github.com/user-attachments/assets/04c684f6-80e8-4506-9845-ff85fda7f14f" />**

2. Seleccionar **Áreas de trabajo** > **Nueva área de trabajo**. Nombrar el espacio (ej. `Lab-Analytics-Workspace`) y crearlo.
   > **<img width="954" height="955" alt="Captura de pantalla 2" src="https://github.com/user-attachments/assets/8c4f83d8-779c-4a25-95e2-c62359867574" />**

3. Dentro del área de trabajo, aprovisionar un nuevo recurso seleccionando **Nuevo** > **Lakehouse**.
4. Asignar el nombre `VentasLakehouse`. Fabric generará automáticamente la estructura del lago de datos.
   > **<img width="1849" height="864" alt="Captura de pantalla 4" src="https://github.com/user-attachments/assets/73011d8f-85ea-4c1d-9eca-7326896f4f3e" />**

---

### Ejercicio 2: Ingesta y transformación de datos en el Lakehouse
**Objetivo:** Cargar archivos planos históricos y convertirlos en tablas analíticas estructuradas.

1. En la vista del `VentasLakehouse`, ubicar la carpeta **Files** (Archivos) en el panel de exploración izquierdo.
2. Usar la opción **Cargar > Cargar archivos** para importar el conjunto de datos de ventas en formato `.csv` proporcionado para el laboratorio.
   > **[INSERTA AQUÍ TU CAPTURA 5: Proceso de carga del archivo CSV]**

3. Una vez que el archivo esté en OneLake, hacer clic en el menú contextual del archivo y seleccionar **Cargar en tablas** > **Nueva tabla**.
4. Nombrar la tabla como `Fact_Ventas`.
   > **[INSERTA AQUÍ TU CAPTURA 6: Cuadro de diálogo configurando la nueva tabla]**

5. Durante este proceso, Fabric convierte los datos en bruto al formato **Delta Parquet**. 
   > **[INSERTA AQUÍ TU CAPTURA 7: La tabla 'Fact_Ventas' visible dentro de la sección 'Tables']**

---

### Ejercicio 3: Visualización de datos masivos con Power BI
**Objetivo:** Conectar una herramienta de Business Intelligence directamente al modelo semántico para generar insights.

1. Cambiar la vista del `VentasLakehouse` de "Lakehouse" a **"Punto de conexión de análisis SQL"**.
   > **[INSERTA AQUÍ TU CAPTURA 8: Desplegable superior derecho cambiando la vista a SQL]**

2. En la cinta de opciones superior, seleccionar **Informes** > **Nuevo informe de Power BI**.
3. En el lienzo del informe de Power BI, expandir la tabla `Fact_Ventas` en el panel de Datos.
   > **[INSERTA AQUÍ TU CAPTURA 9: Interfaz web de Power BI con la tabla desplegada a la derecha]**

4. Crear las siguientes visualizaciones:
   * **Gráfico de columnas agrupadas:** Campos `Fecha` y `Total_Ventas`.
   * **Gráfico circular (Pie chart):** Campos `Categoria` y `Total_Ventas`.
   * **Tarjeta (Card):** Campo `Total_Ventas`.
   > **[INSERTA AQUÍ TU CAPTURA 10: Lienzo con los tres gráficos terminados]**

5. Guardar el informe como `Dashboard_Ventas_DirectLake` en el área de trabajo previamente creada.
   > **[INSERTA AQUÍ TU CAPTURA 11: Confirmación de guardado del informe en el área de trabajo]**
