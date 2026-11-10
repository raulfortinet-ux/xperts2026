# Módulo 2 - Identificar qué alertas merecen investigación
## Goal - Module 2
```{card} Objetivo: Identificar qué alertas merecen investigación
{bdg-success}`Duration: 10 min`

Triage is one of the most important skills in a SOC. With thousands of alerts a 
day, an analyst must quickly separate the noise from the genuine threats. This mission focuses on that prioritisation skill.

**Tasks:**

- Revisa las alertas actuales
- Selecciona las alertas principales que merecen investigación
- Comprende las políticas de escalado
- Classify each alert:
  - Manage the status
  - Severity (High / Medium / Low)
```

## Steps - Module 2

1. Go to the **Alert Summary** page.

    ````{card}
    ```{image} ./_images/002_001.png
    ```
    Alert Summary page
    ````
1. Click on {bdg-primary-line}`Input` on the top right corner and set the time
   range to the last 12 hours.

1. Focus on the **Top 20 Impacted Hosts** and click on the first device name. 
   Esto debería llevarte a la vista de alerta (Alert View).

1. Observe the filter than click on {bdg-primary}`Clear Filter Criteria`
1. Create another filter by clicking on {bdg-primary}`Create Advanced Filter` 
   button on the right: 
    `````{list-table}
    + - Name
      - ```{code-block} text
        Hostname is 100D_OT
        ```

    + - Field
      - {bdg-primary-line}`Assets`

    + - Field
      - ````{list-table}
        + - Field
          - Operator
          - Value

        + - {bdg-primary-line}`Reporting Device Name`
          - {bdg-primary-line}`Equals`
          - - if you are in the FAZ workshop
              ```{code} text
              100D_OT
              ```
            - if you are in other
              ```{code} text
              ORDERS-ERP
              ```
        ````
    `````

    ````{card}
    ```{image} ./_images/002_002.png
    ```
    Eliminando el filtro de dos horas
    ````
1. Save the filter as a user with the {bdg-primary}`Save as User` button. Close
   the advanced filter dialogue box.
   ```{danger}
   ¡Por favor, no guardes el filtro en el sistema, solo para tu usuario!
   ``` 
1. Elige el filtro creado by clicking on the down arrow, next to the filter 
   button on the top right of the alert list, and choose the filter.
    ````{card}
    ```{image} ./_images/002_003.png
    ```
    Elige el filtro creado
    ````

1. Find the Alert:
   ```{code-block} text
   High Severity Inbound Permitted IPS Exploit FortiGate-ips-signature-39577 from 85.243.247.32 to 10.10.100.27
   ```
   ```{card}  
   {bdg-danger}`?` **Has this Alert been Escalated?**
   ```

1. Scroll down until the details part and choose **Correlation** tab, then the
   **Case** tab. You can easily go to the related case by click on the name of 
   it.

    ````{card}
    ```{image} ./_images/002_004.png
    ```
    Find the Case
    ````

1. Go back to the **Alert Details** tab. Review the SLA Details and Alert Status 
   sections. These are used by the Analyst to manage the Alert, assign to other Analysts, and track status.

    ````{card}
    ```{image} ./_images/002_005.png
    ```
    Secciones de SLA y estado de la alerta
    ````

```{card}  
{bdg-danger}`?` **Xpert Challenge**
^^^
Encuentra una alerta diferente (que no haya sido escalada) y escálala: esto crea un nuevo caso para que el analista trabaje en él.
```

```{card} 📌📋 SUMMARY
En esta sección deberías haber entendido dónde encontrar alertas, el filtrado básico y la gestión de alertas.
```
