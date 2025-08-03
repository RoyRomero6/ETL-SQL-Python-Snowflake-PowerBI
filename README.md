# ETL-SQL-Python-Snowflake-PowerBI
Se extraen datos desde un modelo estrella sin normalización en Oracle SQL usando la librería oracledb en Python. Los datos se transforman con pandas y se exportan como CSV para cargarlos en un Data Warehouse en Snowflake. Finalmente, la información se conecta a Power BI para crear un dashboard interactivo.
## 🎯 Objetivo del Análisis
El dashboard fue diseñado para responder preguntas clave como:
- ¿Qué departamento representa el **mayor costo total**?
- ¿En qué **mes** se registró el **mayor costo**?
- ¿Ese mes coincide con el mes en el que se **contrató más personal**?
## 🔄 Pipeline de Datos 

Este proyecto implementa un flujo de datos completo desde una base Oracle hasta un dashboard visual en Power BI, pasando por procesamiento en Python y almacenamiento en Snowflake.

---

### 🗃️ 1. Extracción (Origen: Oracle SQL)

Se utiliza la librería `oracledb` en Python para conectarse a la base de datos Oracle y extraer las siguientes **tablas del área de Recursos Humanos**:

#### 🧩 Tablas en Oracle SQL

- **`departamento`**  
Contiene información sobre los distintos departamentos de la empresa.  
 <img width="627" height="477" alt="Image" src="https://github.com/user-attachments/assets/8b38898e-a02b-4de8-b14c-485a84d7c84c" />
- **`empleado`**  
Contiene los datos del personal de la organización.  
<img width="1088" height="705" alt="Image" src="https://github.com/user-attachments/assets/f6d381d4-6d49-4e3e-9c9e-8deb84a8eb7a" />
- **`costos`**  
Tabla que almacena los componentes de costo por empleado y por mes.  
<img width="638" height="699" alt="Image" src="https://github.com/user-attachments/assets/186a220a-5fe9-4c58-86f1-c3f9c64cdb5b" />  
---
## 🔌 Conexión a Oracle DB y transformación con Pandas a través de Python (`oracledb` y `pandas`)

Se utiliza la librería [`oracledb`](https://python-oracledb.readthedocs.io/en/latest/) para conectarse a la base de datos Oracle desde Python. Esta etapa del pipeline permite ejecutar consultas SQL y extraer los datos necesarios desde las tablas del modelo estrella.

📷 **Captura tabla1(Empleados): Conexión a Oracle y ejecución de una consulta simple (`SELECT * FROM empleado`) en VS Code / Jupyter Notebook:**

![Conexión a Oracle y consulta]<img width="1014" height="536" alt="Image" src="https://github.com/user-attachments/assets/722b9e09-f9e8-4e1d-afa3-eee80faf70e6" />
<img width="1012" height="540" alt="Image" src="https://github.com/user-attachments/assets/f83dfec2-7ff2-40bf-a781-16238f4831e0" />

> 🔒 **Nota:** Las credenciales (usuario, contraseña y DSN) han sido ocultadas manualmente en la captura para mantener la seguridad del proyecto.

---
## 🧪 Transformaciones con `pandas`: Tabla `empleado`

Una vez extraídos los datos de la tabla `empleado`, se utilizaron funciones de `pandas` para convertir los datos en un `DataFrame` y aplicar transformaciones como:

- Renombrar columnas para mayor claridad.
- Conversión de tipos de datos (por ejemplo, fechas).
- Cálculo de nuevas columnas, como la **antigüedad del empleado**.
- Limpieza de registros faltantes o inválidos.
 📷 **Captura: Comprobación de nulos y limpieza de datos**
<img width="1005" height="302" alt="Image" src="https://github.com/user-attachments/assets/4936e7b7-51de-415d-ba79-462b894c6a60" />
 📷 **Captura: Comprobación de unicos para contratos**
<img width="1018" height="167" alt="Image" src="https://github.com/user-attachments/assets/1a61f550-a731-4c23-b147-115010d5d623" />
 📷 **Captura: Remplazo de valores para contratos**
<img width="993" height="257" alt="Image" src="https://github.com/user-attachments/assets/14803a6e-af69-47db-9475-9bb17bb0b22c" />
<img width="971" height="395" alt="Image" src="https://github.com/user-attachments/assets/241c4c60-14aa-4a40-80c5-3d31fdebd343" />
 📷 **Captura: Segunda comprobación de unicos para contratos**
<img width="1018" height="137" alt="Image" src="https://github.com/user-attachments/assets/c81b953c-547e-4a50-a2ca-a103c5ec2d4c" />
 📷 **Captura: Comprobación de unicos para estado civil**
<img width="1016" height="138" alt="Image" src="https://github.com/user-attachments/assets/95989844-373e-4c67-a378-6d97fbe77aba" />
 📷 **Captura: Remplazo de valores para estado civil**
<img width="975" height="299" alt="Screenshot (288)" src="https://github.com/user-attachments/assets/4e76c1dd-8af2-4b0d-b468-5f08ec0604a1" />
<img width="1020" height="386" alt="Screenshot (289)" src="https://github.com/user-attachments/assets/e0c7e74b-c767-40b0-9456-3adc5e616adf" />
 📷 **Captura: Comprobación de unicos para nivel educativo**
<img width="1009" height="125" alt="Screenshot (290) - Copy" src="https://github.com/user-attachments/assets/c04df06a-8667-4120-8a44-d454604c5153" />
 📷 **Captura: Remplazo de valores para nivel educativo**
<img width="1009" height="179" alt="Screenshot (290)" src="https://github.com/user-attachments/assets/99616b3e-2a12-40cf-b714-2411a944cc8f" />
 📷 **Captura: Tabla emppleados a CSV**
<img width="1018" height="83" alt="Screenshot (292)" src="https://github.com/user-attachments/assets/77d64400-5ad9-4909-a33c-d0752e0d1efc" />
## 🧾 Transformación de la Tabla de HECHOS_EMPLEADOS:

Luego de transformar la tabla `empleado`, se procede a trabajar con la tabla `HECHOS_EMPLEADOS`, que contiene los componentes de costo asociados a cada empleado por mes.

### 🔗 Conexión y consulta de la tabla `HECHOS_EMPLEADOS`

Se realiza una conexión similar a la usada anteriormente, ahora consultando la tabla `HECHOS_EMPLEADOS`:

📷 **Captura: Conexión a Oracle y consulta de la tabla `HECHOS_EMPLEADOS`**

<img width="1015" height="613" alt="Screenshot (294)" src="https://github.com/user-attachments/assets/c3cdbbfb-9cef-4eef-92c9-b14a9bec9b11" />

---

### ❌ Eliminación de columnas innecesarias

Se eliminan columnas que no aportan al análisis o que están vacías o duplicadas.

📷 **Captura: Eliminación de columna irrelevante**
<img width="1019" height="625" alt="Screenshot (295)" src="https://github.com/user-attachments/assets/477fd3c6-e6e5-4d87-be9e-0e27ddc31729" />
---

### 🔍 Verificación de valores nulos

Se revisan los datos faltantes en cada columna:

📷 **Captura: Comprobación de valores nulos**
<img width="1011" height="377" alt="Screenshot (296)" src="https://github.com/user-attachments/assets/f6de2c8d-6097-439e-9289-88a277ea37af" />
---

### 🔢 Verificación de tipos de datos

Se comprueba que cada columna tenga el tipo de dato correcto, especialmente fechas y montos.

📷 **Captura: Tipos de datos antes y después de conversión**
<img width="1019" height="354" alt="Screenshot (297)" src="https://github.com/user-attachments/assets/f9965f97-0d0a-4706-8cc8-d67e53afeeef" />

---

### 🧬 Verificación de duplicados (ID empleado)

Se verifica que no existan registros duplicados por ID de empleado.

📷 **Captura: Detección de duplicados por ID**
<img width="1011" height="332" alt="Screenshot (298)" src="https://github.com/user-attachments/assets/8c42cb55-d66a-4536-a226-1ac482e4eda9" />

---

### 📤 Exportación como `OraHechos.csv`

Una vez finalizadas las transformaciones, se exporta el DataFrame a un archivo `.csv` con el nombre `OraHechos.csv`.

📷 **Captura: Exportación del archivo `OraHechos.csv`**
<img width="1018" height="212" alt="Screenshot (299)" src="https://github.com/user-attachments/assets/004564f6-8fb1-4e96-8eea-25d10595c9cc" />

---

## 🏢 Conexión a la tabla `departamento`

Se realiza la conexión a la base de datos Oracle utilizando la librería `oracledb` en Python para consultar la tabla `departamento`.

📷 **Captura: Conexión a Oracle y consulta de la tabla `departamento`**
<img width="1014" height="627" alt="Screenshot (300)" src="https://github.com/user-attachments/assets/4278dc30-a515-4a25-90bb-42e38d292c1c" />
<img width="1030" height="601" alt="Screenshot (301)" src="https://github.com/user-attachments/assets/af91e6ff-9832-4517-90fa-dc73195eee2b" />

---

## 🔄 Transformación y exportación a CSV

Una vez extraídos los datos, se transforma el DataFrame con `pandas` para preparar el archivo `OraDepartamento.csv`.


📷 **Captura: Exportación a `OraDepartamento.csv`**
<img width="1018" height="109" alt="Screenshot (302)" src="https://github.com/user-attachments/assets/9c5536d1-0afd-48cc-9c32-a9e0b678bff6" />





