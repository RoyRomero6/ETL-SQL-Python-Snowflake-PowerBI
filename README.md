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

![Conexión a Oracle y consulta]<img width="1010" height="540" alt="Image" src="https://github.com/user-attachments/assets/dd68e5ec-b358-42dd-81e0-b61159fc8abc" />

> 🔒 **Nota:** Las credenciales (usuario, contraseña y DSN) han sido ocultadas manualmente en la captura para mantener la seguridad del proyecto.

---
