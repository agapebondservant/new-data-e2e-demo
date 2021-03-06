
#### Monitoring Postgres Data (ctd)
Tanzu Postgres provides a set of scrapeable Prometheus endpoints whose metrics can be collected and forwarded to any OpenMetrics backend.

Let's demonstrate this using **Datadog** and **Wavefront**.

##### <i>With Datadog:</i>
Set up the Datadog agent for Kubernetes with Prometheus Autodiscovery enabled:
```editor:open-file
file: ~/other/resources/datadog/data-dog.yaml
```

Deploy the Datadog agent:
```execute
clear && helm repo add datadog https://helm.datadoghq.com && helm repo update && helm install datadog -f ~/other/resources/datadog/data-dog.yaml --set datadog.site='datadoghq.com' --set datadog.apiKey='{{DATA_E2E_DATADOG_API_KEY}}' datadog/datadog
```

View the System Overview dashboard:
```dashboard:open-url
url: https://app.datadoghq.com/dash/integration/system_overview
```

Next, redeploy the Datadog agent with Postgres integrations:
```execute
clear; helm uninstall datadog; sed -i "s/YOUR_SESSION_NAMESPACE/{{ session_namespace }}/g" ~/other/resources/datadog/data-dog-with-db-config.yaml && helm install datadog -f ~/other/resources/datadog/data-dog-with-db-config.yaml --set datadog.site='datadoghq.com' --set datadog.apiKey='{{DATA_E2E_DATADOG_API_KEY}}' datadog/datadog
```

(NOTE: When prompted, use the credentials below to login:)
```execute
printf "Username: {{DATA_E2E_DATADOG_USER}}\nPassword:{{DATA_E2E_DATADOG_PASSWORD}}"
```
View the Postgres dashboard (<font color="red">TODO: Complete integration so that data is populated</font>):
```dashboard:open-url
url: https://app.datadoghq.com/screen/integration/235/postgres---overview?_gl=1*oqjti6*_gcl_aw*R0NMLjE2NDUyMTkzNTEuQ2owS0NRaUFwTDJRQmhDOEFSSXNBR01tLUtINlZnZ0dZelhOSTdadV8zNlBLMENHbFpjQS1TX2FmOG40ck1zSEVrTXVFa2RpZFB5RnI4UWFBanozRUFMd193Y0I.*_ga*MTI3MDQ4ODI1OC4xNjQ1MTQwNDky*_ga_KN80RDFSQK*MTY0NTgzMDU0OC43LjEuMTY0NTgzMDU1My4w&_ga=2.224920799.418082025.1645749670-1270488258.1645140492&_gac=1.128815230.1645219351.Cj0KCQiApL2QBhC8ARIsAGMm-KH6VggGYzXNI7Zu_36PK0CGlZcA-S_af8n4rMsHEkMuEkdidPyFr8QaAjz3EALw_wcB
```

##### <i>With Wavefront:</i>
<font color="red">TODO</font>

#### Secret Management with Vault
<font color="red">TODO</font>
