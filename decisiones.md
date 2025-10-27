# Decisiones de Desarrollo - TP05 DevOps CI/CD Pipelines 
 
## 1. Configuración del Entorno 
 
1) Ya tenía configurado mi self-hosted agent en mi MacBook (ubicado en ~/myagent) 
   - Pool: Default 
   - Estado: funcionando correctamente 
   - Nombre del agente: Santos-MacBook 
 
2) Verifiqué el estado: 
cd ~/myagent 
./run.sh 
El agente quedó escuchando jobs y conectado al servidor de Azure DevOps. 
 
3) Me logueé en Azure CLI: 
az login 
Seleccioné la suscripción Azure for Students y la suscripción quedó activa. 
 
4) Creé los recursos cloud para los entornos de QA y Producción: 
az group create --name tp05-rg --location eastus 
az appservice plan create --name tp05-plan --resource-group tp05-rg --sku B1 --is-linux 
az webapp create --name tp05-qa-app --resource-group tp05-rg --plan tp05-plan 
az webapp create --name tp05-prod-app --resource-group tp05-rg --plan tp05-plan 
 
5) Configuré variables de entorno para cada ambiente: 
az webapp config appsettings set --name tp05-qa-app --resource-group tp05-rg --settings ENVIRONMENT=QA CONNECTION_STRING="Server=mydb-qa;Database=app;User Id=admin;Password=1234;" 
 
az webapp config appsettings set --name tp05-prod-app --resource-group tp05-rg --settings ENVIRONMENT=PROD CONNECTION_STRING="Server=mydb-prod;Database=app;User Id=admin;Password=abcd;" 
 

 
## 2. Estructura del Pipeline 
 
Creé un único pipeline YAML con stages: 
 
- Stage 1: Build   
  Empaqueta y publica artefactos del proyecto. 
 
- Stage 2: Deploy to QA   
  Despliega automáticamente al App Service de QA (tp05-qa-app). 
 
- Stage 3: Deploy to Production   
  Despliega a producción (tp05-prod-app) después del QA, con posibilidad de gate manual. 
 
Archivo: azure-pipelines.yml 
El pipeline usa el self-hosted agent (pool: Default) y ejecuta las etapas secuencialmente. 
 

 
## 3. Flujo de Trabajo y Validaciones 
 
1) La rama principal (main) está protegida.   
   Para actualizar el YAML, se utilizó una rama feature: 
   feature/add-release-pipeline 
   Luego se creó un Pull Request hacia main, con aprobación y merge automático. 
 
2) Ejecuté el pipeline desde la interfaz de Azure Pipelines: 
   - Build completado ✅   
   - Deploy QA completado ✅   
   - Deploy PROD completado ✅ 
 
3) El agente local reportó: 
   Job Build completed with result: Succeeded 
   Job QA_Deploy completed with result: Succeeded 
   Job PROD_Deploy completed with result: Succeeded 
 

 
## 4. Evidencias 
- Capturas de los tres stages completados correctamente en Azure DevOps.   
- Logs en la terminal confirmando ejecución exitosa.   
- QA y PROD listos con sus respectivas variables. 
 

 
## 5. Reflexión 
Este trabajo integró todo lo aprendido en DevOps: 
- Integración con recursos Cloud. 
- Uso de stages y artefactos. 
- Ejecución en agente propio. 
- Automatización del ciclo completo: build → test → deploy. 
 