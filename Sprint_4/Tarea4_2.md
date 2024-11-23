# Recolección de Datos para creacion de modelo para identificar el riesgo de un credito

## 1. Fuentes

**Identificación de Fuentes:**
- Base de datos interna del banco.

**Descripción de las Fuentes:**
- La base de datos interna contiene registros de clientes, detalles financieros y datos relacionados con el historial crediticio. Esta información es recopilada por el departamento de TI mediante sistemas internos de gestión y APIs específicas.
  
## 2. Métodos de recolección de datos

**Procedimientos y Herramientas:**
- Exportación programada en formato CSV desde los sistemas internos de gestión del banco, con almacenamiento en un repositorio seguro, actualizado diariamente por el departamento de TI.

**Frecuencia de Recolección:**
- Diariamente, se debe crear un fichero automaticamente a media noche. El fichero se subira automaticamente a la nube para que el modelo pueda acceder a el.
  
**Scripts de Descarga:**

```python

import pandas as pd

csv_url = "https://CloseBank.com/internal/it/repos/11232024/bank_dataset.csv"
df = pd.read_csv(csv_url)
print(df.info())

```

## 3. Formato y estructura de los datos

**Tipos de Datos:**
- Numéricos: `age`, `balance`, `day`, `duration`, `campaign`, `pdays`, `previous`.
- Categóricos: `job`, `marital`, `education`, `default`, `housing`, `loan`, `contact`, `month`, `poutcome`, `deposit`.

**Formato de Almacenamiento:**
- Datos tabulares almacenados en archivos CSV.

## 4. Limitaciones de los datos

- Diferencias en los Tiempos de Actualización: La actualización de datos financieros y de contacto de los clientes puede variar entre los distintos sistemas del banco, lo que podría introducir inconsistencias temporales. Ya que tendremos datos diarios las inconsistencia serian de maximo 1 dia.

## 5. Consideraciones sobre Datos Sensibles

**Tipos de Datos Sensibles:**
- Información Personal Identificable (PII): `job`, `marital`, `education`.
- Información Financiera Sensible: `balance`, `loan`, `housing`, `deposit`.
- Datos Relacionados con el Historial Crediticio: `default`, `poutcome`, `pdays`, `previous`.

**Medidas de Protección:**
- **Anonimización y Pseudonimización:**
  - Aplicación de hash para los datos categóricos sensibles como `job` y codificación para `education` y `marital`.
- **Acceso Restringido:**
  - Restricción de acceso a los datos sensibles únicamente al personal autorizado que lo requiera para los fines específicos del proyecto.
- **Cumplimiento de Regulaciones:**
  - Asegurar el cumplimiento con regulaciones locales e internacionales, como la GDPR, para la protección de datos personales y financieros.
