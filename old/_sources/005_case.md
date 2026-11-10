# Módulo 5: Investigación de casos 
## Goal - Module 5
```{card} Objetivo: Investigar un inicio de sesión sospechoso
{bdg-success}`Duration: 10 min`

Multiple failed login attempts from different countries are detected, followed 
by a successful VPN login. This is the scenario you identified at the start of 
the lab. Your job is to classify the threat, investigate using a Case, and run a Playbook to block the attacker.

**Expected findings:** 
- Compromiso de credenciales
- patrón de acceso inusual desde múltiples geografías.

**Expected outcome:** 
- Clasificar como True Positive. 
- Bloquear la IP de origen mediante un playbook.
```
## Steps - Module 5
### Triage the Alert

1. Navigate to **Cases & Alerts / Alerts / Alert List**. 
1. Consider the **Target User** column and filter for the user:
   ```{code-block} text
   student_XX
   ``` 
   (e.g. `student_1`) que te ha asignado tu instructor.

   ```{warning}
   Do not investigate a user assigned to another student for this exercise — it 
   will cause confusion and cause labs to fail.
   ```

   ````{card}
   ```{image} ./_images/005_001.png
   ```
   Lista de alertas filtrada por el usuario de destino asignado
   ````

1. The **Escalated** column should show {bdg-danger}`Yes` — this means a Case 
   has already been created. Select the successful VPN login Alert, for example:
   ```{code-block} text
   Successful VPN login from student_XX at IP 102.33.134.252 from outside my country
   ```
   ```{warning}
   La dirección IP puede ser diferente en tu entorno.
   ```

1. Haz los siguientes cambios en la alerta:
   - **Severity:** High
   - **Assigned to:** you

   ````{card}
   ```{image} ./_images/005_002.png
   ```
   Campos de severidad y asignación de la alerta
   ````

1. Scroll to the bottom of the screen and review the extracted indicators. 
   Expand an external IP address indicator to review the rating.

   ````{card}
   ```{image} ./_images/005_003.png
   ```
   Indicadores extraídos con la valoración expandida
   ````
1. If you only see the FortiGuard Labs result, select the IP address and choose
   {bdg-primary-line}`Get Latest Reputaton` from the {bdg-primary}`Execute` menu.
   After a minute, check the result.
   ````{card}
   ```{image} ./_images/005_004.png
   ```
   Indicadores extraídos con la valoración expandida
   ````   
### Investigate the Case

1. Move over to **Correlations** — there should be one Case created. Click the 
   Case to pivot into it for a deeper investigation.

   ````{card}
   ```{image} ./_images/005_005.png
   ```
   Correlaciones – vista de caso vinculado
   ````

1. Asigna el caso a ti mismo.

   ````{card}
   ```{image} ./_images/005_006.png
   ```
   Campo de asignación del caso
   ````

1. At the bottom of the screen, click on **FortiAI – Case Enrichment & Impact
    Analysis**. This can take a few minutes to run.

   ````{card}
   ```{image} ./_images/005_007.png
   ```
   FortiAI Case Enrichment summary output
   ````

   ```{note}
   Al completarse, debería haber un resumen claro. The FortiAI Case Enrichment feature is often the most impactful feature for a SOC — it turns what would 
   take a human analyst 20 minutes of manual pivoting into an instant summary.
   ```

1. Scroll to the bottom of the screen, click on **Correlations**, then 
   **Alerts** to review all related alerts in more detail.

### Contención – ejecutar un playbook

1. We now need to decide on next steps. A reasonable action for this scenario 
   (and lab environment) is to contain (block) the public IP address.

1. Run (execute, from the bottom of the Case screen) the **"00 – Block Case 
   Source IP"** playbook.

1. Debería mostrarte la IP para seleccionar el bloqueo.

   ````{card}
   ```{image} ./_images/005_008.png
   ```
   Playbook – selección de IP para la acción de bloqueo
   ````

   ```{warning}
   It can take a little while for this screen to appear. **Do not** keep running
    the playbook — you will create a queue in the playbook execution.
   ```

1. Go back to the top of the Case screen and review the playbook execution to 
   confirm it executed successfully.

   ````{card}
   ```{image} ./_images/005_009.png
   ```
   Confirmación del estado de ejecución del playbook
   ````

### Close the Case

Una vez que el playbook se haya ejecutado correctamente:

1. Change the **Case Stage** to **Resolved**
1. Completa los detalles de cierre
1. Asegúrate de que todos los elementos pendientes estén cerrados

### Escalation Rules

Ahora que has trabajado un caso, entendamos cómo se agrupan las alertas en casos automáticamente.

**Escalation Rules** is a concept used within SOCaaS and now implemented in FortiSOC. Escalation Rules define the logic behind which Alerts are escalated 
and aggregated into a single Case.

Review the Escalation Rules by navigating to **Resources / Escalation Rules** 
and reviewing the **"FortiSOC – User login anomaly"**. Examine the filter 
conditions and understand how aggregation works.

```{warning}
**No hagas cambios en ninguna de estas reglas.**
```

````{card}
```{image} ./_images/005_010.png
```
Lista de reglas de escalado
````

In this example, Alerts are correlated into a Case if the Target Users match 
between Alerts and the Tags or Types match. This helps prevent an analyst from 
being swamped with dozens of individual login alerts when they are all part of 
the same attack.

````{card}
```{image} ./_images/005_011.png
```
Detalle de la regla de escalado – condiciones de filtro y lógica de agregación
````

```{card} 📌📋 SUMMARY
Has recorrido el flujo de trabajo completo de alerta a caso:
- Alert triage
- Case investigation
- FortiAI enrichment
- Playbook execution
- Case closure
- Política de escalado de alerta a caso
```
