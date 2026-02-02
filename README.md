
# 📊 End-to-End Data Engineering Project  
## Amazon Prime – Azure Lakehouse (DEV / PROD)

---
<img width="1335" height="682" alt="image" src="https://github.com/user-attachments/assets/8ff9670c-3f95-4024-af20-0e372f9bfb52" />


---

## 🧠 Descripción del Proyecto

Este proyecto implementa una **solución End-to-End de Data Engineering en Azure**, diseñada para simular un **entorno empresarial real**, aplicando separación de ambientes **DEV / PROD**, arquitectura **Lakehouse con patrón Medallion (Bronze, Silver, Gold)**, seguridad basada en identidades y consumo analítico mediante **Azure Synapse Serverless y Power BI**.

El dataset utilizado corresponde a **Amazon Prime Titles**.  
El consumo final se realiza **sin accesos directos al Data Lake**, siguiendo buenas prácticas de gobierno y seguridad de datos.


---

## 🎯 Objetivo General

Diseñar e implementar una solución completa de **Data Engineering en Azure**, cubriendo ingestión, transformación, almacenamiento, seguridad, automatización y consumo analítico, siguiendo estándares profesionales.

---

## 🎯 Objetivos Específicos

- Implementar separación **DEV / PROD** a nivel de recursos, identidades y datos  
- Automatizar despliegues de **Azure Data Factory** y **Azure Databricks** mediante **CI/CD**  
- Aplicar arquitectura **Medallion (Bronze, Silver, Gold)** usando **Delta Lake**  
- Gestionar secretos y credenciales de forma segura con **Azure Key Vault**  
- Exponer datos analíticos mediante **Azure Synapse Serverless SQL**  
- Consumir datos desde **Power BI** usando autenticación segura (**Microsoft Entra ID**)  

---

## 🏗️ Arquitectura General

**Flujo de datos:**

GitHub (CSV)
↓
Azure Data Factory (Copy Activity)
↓
ADLS Gen2 (Bronze)
↓
Azure Databricks (PySpark + Delta Lake)
↓
ADLS Gen2 (Silver / Gold)
↓
Azure Synapse Serverless SQL (Views)
↓
Power BI

markdown
Copiar código

---

## 🧱 Arquitectura Medallion

### 🟤 Bronze Layer
- Ingesta de datos crudos desde GitHub (CSV)
- Sin transformaciones de negocio
- Persistencia en **ADLS Gen2**
- Esquema original preservado

### ⚪ Silver Layer
- Limpieza y normalización de datos
- Conversión explícita de tipos
- Manejo de valores nulos
- Eliminación de duplicados
- Transformación de campos de duración (`duration_value`, `duration_unit`)
- Implementación de **SCD Tipo 1** usando `MERGE` sobre **Delta Lake**

### 🟡 Gold Layer
- Datos listos para análisis
- Tablas Delta optimizadas para consumo BI
- Estructura pensada para consultas analíticas
- Fuente oficial para Synapse y Power BI

---

## 🧰 Tecnologías Utilizadas

- **Azure Data Factory**
- **Azure Data Lake Storage Gen2**
- **Azure Databricks**
- **Delta Lake**
- **Azure Synapse Analytics (Serverless SQL Pool)**
- **Azure Key Vault**
- **Microsoft Entra ID**
- **GitHub Actions (CI/CD con OIDC)**
- **Power BI**
- **PySpark**
- **SQL**

---

## 🔐 Seguridad y Gobierno de Datos

- ❌ No se utilizan credenciales hardcodeadas
- ✅ Autenticación basada en **Managed Identity**
- ✅ Secretos almacenados en **Azure Key Vault**
- ✅ Control de accesos mediante **RBAC + ACL**
- ✅ Separación estricta de permisos entre DEV y PROD
- ✅ Power BI accede únicamente a través de **Synapse Serverless**

---

## 🔁 CI/CD y Automatización

### Azure Data Factory
- Desarrollo en entorno DEV
- Versionamiento en GitHub
- Despliegue automático a PROD mediante:
  - GitHub Actions
  - ARM Templates
  - Parámetros dinámicos por ambiente

### Azure Databricks
- Repositorios Git sincronizados
- Separación de notebooks DEV / PROD
- Secret Scopes por entorno
- Integración con CI/CD

---

## 📊 Capa Analítica – Azure Synapse Serverless

- Creación de **vistas SQL** sobre datos en ADLS Gold
- Lectura mediante `OPENROWSET`
- No se crean tablas físicas
- Costo optimizado (pay-per-query)
- Punto único de acceso analítico

Ejemplo conceptual:
sql
SELECT *
FROM OPENROWSET(
    BULK 'amazon_prime_titles/',
    DATA_SOURCE = 'adls_gold',
    FORMAT = 'PARQUET'
) AS rows;

---

📈 Consumo en Power BI
Conexión mediante Azure Synapse Serverless SQL
Autenticación con Microsoft Entra ID
Sin acceso directo al Data Lake
Compatible con Import Mode o DirectQuery
Modelo preparado para análisis y visualización

---

🚀 Resultado Final
Pipeline ETL completamente funcional
Arquitectura escalable y segura
Datos listos para análisis
Solución alineada a prácticas reales de la industria
Proyecto listo para portafolio profesional

---

🧠 Principales Aprendizajes
Diseño de arquitectura Lakehouse en Azure
Implementación correcta de seguridad (IAM, ACL, Key Vault)
Uso de Synapse Serverless como capa de consumo
Automatización de despliegues con CI/CD
Integración completa entre Data Engineering y BI

---

👤 Autor
Yonathan Montenegro Martínez
Data Engineer | Analytics Engineer

---

📅 Fecha
Enero 2026

---
