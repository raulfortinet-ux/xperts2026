# Módulo 1 - Confirmar que FortiSOC está sano y recibiendo datos
## Goal - Module 1
```{card} Objetivo: Confirmar que FortiSOC está sano y recibiendo datos
{bdg-success}`Duration: 10–15 min`

**Tasks:**

- Confirmar que el SIEM está ingiriendo logs de una fuente de datos activa
- Confirmar que Analyzer está recibiendo logs de dispositivos
- Validar que el conector de SOAR está sano
- Comprender qué ofrece la gestión de inteligencia de amenazas (TIM)
- Localizar al menos una alerta
```

## SIEM

There are 3 ways to validate events are flowing into the SIEM module — work 
through each in turn.

```{note}
También se genera una alerta cuando no se reciben logs de un dispositivo en un intervalo de tiempo personalizable, pero no se cubrirá en esta sección.
```

1. **Collector** – Navigate to **SIEM / Settings / Health**

   ```{card}  
   {bdg-danger}`?` **What is the Collector health and last file received time?**
   ^^^
   The last file received timestamp should be very recent — this indicates logs 
   are actively being uploaded to FortiSOC.
   ```

   ```{note}
   Don't worry if the Event Status of the SIEM collector is not Normal. It is a
   lab environment, not a production one.
   ```

1. **CMDB** – Navigate to **SIEM / CMDB / select the Collector**

   ```{card} 
   {bdg-danger}`?` **Revisa los dispositivos y comprueba si el Event Status es Normal.**
   ```

    ````{card}
    ```{image} ./_images/001_001.png
    ```
    SIEM CMDB – vista del collector
    ````

1. **Analytics** – Navigate to **Cases & Alerts / Search / Load a report** for 
   the Top Reporting Devices

   ```{card}  
   {bdg-danger}`?` **¿Los dispositivos top de reporte coinciden con lo que viste en el CMDB?**
   ^^^
   Deberías ver nombres de dispositivos coherentes y volúmenes de logs relativos.
   ```


    ````{card}
    ```{image} ./_images/001_002.png
    ```
    Analytics – informe de dispositivos top de reporte
    ````

    ````{card}
    ```{image} ./_images/001_003.png
    ```
    Analytics – volúmenes de logs por dispositivo
    ````
## Analyzer

Analyzer almacena y analiza logs específicamente de dispositivos Fortinet Fabric. Valida que esté conectado y recibiendo datos.



1. **Device Status** – Navigate to **Analyzer / Device Manager**

   ```{card}  
   {bdg-danger}`?` **What is the device status and last time logs were 
   received?**
   ```

    ````{card}
    ```{image} ./_images/001_004.png
    ```
    Analyzer – Device Manager
    ````
1. **View Fabric Logs** – Navigate to **Analyzer / Log View**

    ````{card}
    ```{image} ./_images/001_005.png
    ```
    Analyzer – Log View
    ````
    ```{note}
    On a customer deployment, you would use this view to confirm that FortiGate 
    or other Fabric devices have been correctly onboarded.
    ```


## SOAR

Los playbooks en SOAR automatizan acciones de respuesta. Para que un playbook funcione, los conectores de los que depende deben estar sanos. El objetivo aquí es validar que los conectores están configurados.

1.  Navigate to **Automation / Connectors**. Find the **FortiGuard IOC 
    Connector** and verify it shows a healthy state.

    ````{card}
    ```{image} ./_images/001_006.png
    ```
    SOAR – vista de salud de conectores
    ````

    El componente SOAR también ingiere alertas de los componentes SIEM y Analyzer.
1. Navigate to **Automation / Data Ingestion**.
1. Select the **FortiSIEM Connector** and review the expanded settings. 
   ```{danger} No hagas ningún cambio.
   ```

    ````{card}
    ```{image} ./_images/001_007.png
    ```
    SOAR – ajustes de ingesta del FortiSIEM Connector
    ````
   ```{card}  
   {bdg-danger}`?` **How frequently is the SOAR polling for new Alerts from the 
   SIEM?**
   ^^^
   This value controls how quickly an analyst sees a new Alert in the SOAR after 
   it was generated in the SIEM.
   ```


## Gestión de inteligencia de amenazas

TIM enriquece las alertas comprobando automáticamente si las IP, dominios y hashes de una alerta son amenazas conocidas. Sin TIM, un analista debe investigar manualmente cada indicador. En este módulo se puede usar el FortiGuard IOC Connector, así como otros conectores de inteligencia de amenazas.

1. Click on **Gestión de inteligencia de amenazas** left menu and review the available 
   options.
    ````{card}
    ```{image} ./_images/001_008.png
    ```
    Gestión de inteligencia de amenazas overview
    ````

````{list-table}
+ - Section 
  - Description 


+ - **Indicators** 
  - Extracted from Alerts. Click an indicator for more details, then view the    
    playbook that extracted the indicators via the playbook icon (top right). 
    Consulta las alertas y casos asociados al indicador. 

+ - **Dashboards** 
  - Pantalla de estado con estadísticas actuales de los indicadores. 

+ - **Threat Intel Search** 
  - Busca indicadores. Introduce la dirección IP:
    ```{code-block} text
    208.91.114.100
    ```
    ```{card}  
    {bdg-danger}`?` **What risk level is assigned to this indicator?**
    ```
    ```{note}
    This is the same IP you will encounter in the later labs — keep it in mind.
    ```

+ - **Threat Intel Feed** 
  - Lista completa de todos los indicadores. 

+ - **Intelligence** 
  - View the latest FortiGuard threat intel by industry or actor. The **Feed 
    Configuration** tab (far right) is where additional threat feeds can be integrated. 

+ - **MITRE ATT&CK** 
  - Details on groups, tactics, and techniques. This information can be 
    referenced by playbooks to enrich Alerts. 
````
## Identifying Alerts

Alerts in FortiSOC are under the **Cases & Alerts** section. Your task is to 
explore the alerts and find a specific alert of interest.

Navigate to **Cases & Alerts / Alerts / Alert List**.

### Tarea 1 — Alerta de fuga de datos

Localiza una alerta con estos filtros:
````{list-table}
+ - **Type**
  - {bdg-primary-line}`Data Leakage`
    
+ - **Source** 
  - ```{code-block} text
    Fortinet FortiSIEM
    ```
````

Un buen ejemplo que buscar es:

```{code-block} bash
Office365 mailbox login by partha.kaushik@example.com from Canada using 208.91.114.100
```

````{card}
```{image} ./_images/001_009.png
```
Ejemplo de alerta de fuga de datos
````

```{card}  
{bdg-danger}`?` **Desde la alerta, responde a las siguientes preguntas:**
^^^
1. Where can you see the event/log that caused the Alert to trigger? What 
   section of the GUI is this under?
1. ¿Dónde puedes ver los indicadores extraídos?
1. If you do not see any indicators, this may be due to the Alert type. Try 
   finding an Alert with an IP address in the name — these Alerts are more 
   likely to have the indicator extracted.
1. Review what playbooks were executed for the Alert. Click the **Playbooks** tab
   on the Alert. What playbooks are executed automatically? If you do not see playbooks, look at historical playbook logs.
```

### Tarea 2 — Alerta de acceso no autorizado

Localiza una alerta con estos filtros:
````{list-table}
+ - **Type**
  - ```{code-block} text
    Unauthorized Access
    ```

+ - **Source** 
  - ```{code-block} text
    Fortinet FortiAnalyzer
    ```
````
Busca la alerta sospechosa de autenticación multigeográfica del usuario: 
```{code-block} text
demo
```

Selecciona una de las alertas que te parezcan interesantes, por ejemplo:

```{code-block} text
Suspicious successful authentication from multiple geo locations for user: demo
```

```{card}  
{bdg-danger}`?` **Y responde a las siguientes preguntas:**
^^^
1. ¿Cuáles son las IP de origen y destino en la alerta?
1. Are there any malicious indicators? If yes, where does the malicious 
   indicator originate from? (Name one if there are multiple.)
1. ¿Se han desencadenado alertas con el mismo indicador malicioso?
1. ¿Puedes explicar qué ocurrió en la alerta? ¿Qué usuario está afectado?
```

```{card} 📌📋 SUMMARY
En esta sección deberías haber entendido: el monitoreo del estado de eventos en SIEM o Analyzer, los conectores de SOAR y la búsqueda de alertas.
```
