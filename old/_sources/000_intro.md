# Introduction

## Product Orientation

The lab missions that follow simulate a SOC experience, starting from 
environment validation all the way through to automated response. By the end of 
the session, you should be able to explain each core component's role to a 
customer and guide them through similar workflows.

```{card} Al final de este laboratorio podrás:

- Validar que un entorno FortiSOC está recibiendo datos
- Hacer triaje y priorizar alertas como analista de SOC
- Realizar una investigación para entender el alcance de un incidente
- Ejecutar una acción de respuesta para contener una amenaza
- Gestionar un escalado de alerta a caso y cerrar un incidente
```

You will be interfacing with FortiSOC only, not the FortiAnalyzer or FortiSIEM Collectors that generate the logs. In the lab environment we use several 
components:

- Colectores de FortiSIEM con escenarios de reproducción de eventos
- FortiAnalyzer con escenarios de reproducción de eventos
- Agentes de FortiSOAR en ejecución en colectores de FortiSIEM
- FortiGate como destino de las acciones de respuesta

````{card}
```{image} ./_images/000_001.png
```
Diagrama del entorno del laboratorio
````

## Acceso al entorno

1. **Click on** this button and go to the FortiSOC page.
    ```{button-link} https://fortisoc.forticloud.com 
    :color: primary
    :shadow:
    :expand:
    ```
 
1. **Click on** the {bdg-primary}`Login/Create Account` button.
    ````{card}
    ```{image} ./_images/000_002.png
    ```
    ````
1. **Choose** {bdg-primary-line}`IAM user`, type the `account ID`, provided by
   the instructors of the workshop and your previously registered `email address`
   and `password`, then push the {bdg-danger}`Log in as IAM user` button.
    ````{card}
    ```{image} ./_images/000_003.png
    ```
    ````

    ```{warning}
    Only use the instance allocated to your name. Using another student's 
    instance will disrupt their work and corrupt the shared lab data.
    ```

1. **Provide** the `Security Code` you've got in email then push the 
   {bdg-danger}`Go` button.
    ````{card}
    ```{image} ./_images/000_004.png
    ```
    ````

1. You might see the following page. **Click** on {bdg-info}`Enter` and you 
   will access the FortiSOC instance assigned to you for the Training.
    ````{card}
    ```{image} ./_images/000_005.png
    ```
    ````

1. After clicking Enter or maybe right after login you should now be in you
   FortiSOC instance:
    ````{card}
    ```{image} ./_images/000_006.png
    ```
    ````