# TP05 - DevOps CI/CD Pipeline 
 
## Objetivo 
Implementar un pipeline completo de integración y despliegue continuo (CI/CD) en Azure DevOps con self-hosted agent y despliegue a Azure Web Apps (QA y Producción). 
 

 
## Descripción del Proyecto 
Toma la aplicación del TP04 y la integra a un pipeline YAML automatizado que: 
1. Compila y publica artefactos. 
2. Despliega automáticamente a QA. 
3. Despliega a Producción. 
 

 
## Tecnologías Utilizadas 
- Azure DevOps (Pipelines + Environments) 
- Azure CLI 
- Azure App Service (QA y PROD) 
- Self-hosted agent (MacBook) 
- YAML Pipelines 
 

 
## Estructura del Pipeline 
Stages principales: 
1. Build → Construcción y publicación de artefactos. 
2. Deploy_QA → Despliegue automático al entorno QA. 
3. Deploy_PROD → Despliegue a Producción. 
 
Archivo YAML versionado en main. 
 

 
## Entornos Cloud 
| Entorno | App Service | URL | 
|----------|--------------|-----| 
| QA | tp05-qa-app | tp05-qa-app.azurewebsites.net | 
| PROD | tp05-prod-app | tp05-prod-app.azurewebsites.net | 
 

 
## Ejecución 
1. Iniciar el agente local: ~/myagent/run.sh 
2. En Azure DevOps → Pipelines → Tp04 → Run pipeline. 
3. Seleccionar rama main → Run. 
 
Resultado esperado: 
Stage 1: Build ✅ 
Stage 2: Deploy QA ✅ 
Stage 3: Deploy PROD ✅ 
 

 
## Autores 
Santos Romero Reyna, Lopez Marcos   
Ingeniería de Software III - UCC   
Año: 2025 
 