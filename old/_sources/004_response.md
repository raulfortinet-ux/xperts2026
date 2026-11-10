# Módulo 4 - Contener la amenaza bloqueando la IP de origen
## Goal - Module 4
````{card} Objetivo: Contener la amenaza bloqueando la IP de origen
{bdg-success}`Duration: 10 min`

La investigación te dice qué ocurrió. La respuesta es lo que haces al respecto. 
FortiSOC can execute response actions directly against connected infrastructure 
— in this case, blocking an IP on a FortiGate firewall via a Connector action.

**Goal:** 
Contain the threat associated with this alert:
```{code-block} text
High Severity Inbound Permitted IPS Exploit FortiGate-ips-signature-39577 from 85.243.247.32 to 10.10.100.27
```

**Tasks:**

- Abre la alerta de exploit IPS
- Usa el FortiGate Connector para ejecutar una acción Block IP
- Selecciona el atributo Source IP de la alerta para rellenar el destino del bloqueo

**Deliverable:**

- Recommended action
- Justificación de 1–2 frases
````

## Steps - Module 4

1. Open the Alert from the previous step (you may choose a different Alert if 
   you wish, but ensure it contains an IP address). We need to block the public 
   IP address found in this Alert.

1. At the bottom of the Alert, click **Actions**. A FortiGate Connector is 
   already configured here. We are not running a full playbook — we are 
   executing a **Connector Action** (a pre-defined action).

   ````{card}
   ```{image} ./_images/004_001.png
   ```
   Panel de acciones de alerta con conectores
   ````

   - Filter for **FortiGate** and expand the available actions.
   - Select the **"Block IP Address"** action.

   ````{card}
   ```{image} ./_images/004_002.png
   ```
   Acción Block IP Address seleccionada en el FortiGate Connector
   ````

1. Click the **IP Address** text box — this should open a window allowing you to 
   select the attribute **"Source IP"**, which will populate the IP address from
    the Alert.

   ````{card}
   ```{image} ./_images/004_003.png
   ```
   Selección del atributo Source IP para rellenar el destino del bloqueo
   ````
   
   ```{note}
   If in your environment you can't change to the `Agent` from `Self`, that 
   means, there is a connector installed on FortiSOC directly. If you can change,
   change it to `gcp_collector_agent`.
   ```

   ```{note}
   The Block IP action **could fail** because the IP address is already blocked 
   by an other student.
   ```

```{card} 📌📋 SUMMARY
En esta sección deberías haber entendido cómo ejecutar una acción de conector en una alerta.
```

