# Módulo 3 - Determinar el alcance y la intención de la alerta de exploit IPS
## Goal - Module 3
```{card} Objetivo: Determinar el alcance y la intención de la alerta de exploit IPS
{bdg-success}`Duration: 15 min`

Good investigation follows the evidence. You have one suspicious IP address, 
`85.243.247.32` — your job is to understand everything that IP has been doing 
across your environment.

**Tasks:**

- Profundiza en la alerta seleccionada
- Review:
  - Source (who/what triggered it)
  - Destination (target system)
  - Timeline of activity
- Check for:
  - Repeated behaviour
  - Lateral movement
  - Alertas/eventos relacionados

**Prepara un resumen rápido:**

- What happened
- Alcance (sistemas/usuarios afectados)
- Risk level
- Cuál es un siguiente paso razonable
```

## Steps - Module 3

1. Trabajaremos con esta alerta:
   ```{code-block} text
   High Severity Inbound Permitted IPS Exploit FortiGate-ips-signature-39577 from 85.243.247.32 to 10.10.100.27
   ```
   ```{note}
   The Source IP `85.243.247.32` — we need to investigate if there are other 
   events in FortiSOC regarding this IP address.
   ```

1. Navigate to **Cases & Alerts / Search**. This opens the FortiSOC alert search 
   and analytics interface. We'll be using structured search.

1. Click on the filter line and create a new query to search for any logs where 
   the source **or** destination IP is 
   ```{code-block} text
   85.243.247.32
   ```
   Running the query over the **past 5 days**.
   ```{warning}
   Make sure to use an **OR** operator!
   ```
   ````{list-table}
   :header-rows: 1
   + - Attribute
     - Operator
     - Value
     - Next

   + - {bdg-primary-line}`Source IP`
     - {bdg-primary-line}`=`
     - ```{code-block} text
       85.243.247.32
       ```
     - {bdg-success-line}`OR`
   

   + - {bdg-primary-line}`Destination IP`
     - {bdg-primary-line}`=`
     - ```{code-block} text
       85.243.247.32
       ```
     - 
   ````
    ````{card}
    ```{image} ./_images/003_001.png
    ```
    Filtro de búsqueda estructurada de alertas de FortiSOC para la IP 85.243.247.32
    ````

1. Click {bdg-primary}`Apply & Run` to run the query and review the results. The 
   results should return several lines.

1. {bdg-primary-line}`Load` a **Display Template** to group the data by Source a
   and Destination IP. Click the {bdg-primary-line}`Change the Display Fields` 
   button.

    ````{card}
    ```{image} ./_images/003_002.png
    ```
    Plantilla de visualización que agrupa resultados por IP de origen y destino
    ````
1. Click {bdg-primary}`Apply & Run` to run the query and review the results. The 
   results should return several lines.
   ```{card}  
   {bdg-danger}`?` **What are the source and destination IPs associated with 
   `85.243.247.32`?**
   ```

1. Click the {bdg-primary-line}`Change the Display Fields`. Add the 
   `Destination TCP/UDP Port` to the display fields.
   
1. Click {bdg-primary}`Apply & Run` to run the query and review the results. The 
   results should return several lines.
   
1. Navigate to **Cases & Alerts / Alerts / Alert List**. Use the filters to look
   for other Alerts regarding IP    
   ```{code-block} text
   85.243.247.32
   ```
   Check the Related Evidence tab — there should be several related logs in 
   there. Use this information along with your analytical investigation to draw 
   a conclusion as a SOC Analyst.

```{card} 📌📋 SUMMARY
In this section you should have obtained a deeper understanding of Alerts and 
analytic basics.
```
