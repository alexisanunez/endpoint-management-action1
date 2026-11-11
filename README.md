# Endpoint Management with Action1

Implementación de una solución de administración centralizada de endpoints mediante Action1, integrada con un entorno de Active Directory sobre Windows Server 2025.

El laboratorio utiliza dos clientes Windows 11 LTSC unidos al dominio `mydomain.com`, permitiendo administrar los equipos de forma remota, consultar inventarios de hardware y software, gestionar actualizaciones de Windows, desplegar aplicaciones y ejecutar scripts de PowerShell.

![](https://i.imgur.com/AQqKGoo.png)

## Environment

- **Endpoint Management Platform:** Action1
- **Server:** Windows Server 2025
- **Clients:** 2 × Windows 11 LTSC
- **Domain:** `mydomain.com`
- **Directory Service:** Active Directory Domain Services (AD DS)
- **Endpoint Management:** Action1 RMM
- **Deployment:** Software Deployment, Script Deployment, Windows Updates

## Active Directory Integration

Se preparó el entorno de Active Directory para facilitar el despliegue remoto y la administración de los equipos mediante Action1.

Se creó una OU específica denominada `Action1 Deployment`, destinada a centralizar los equipos administrados por la plataforma.

### Configuración de Group Policy

Se configuraron dos GPOs para permitir las operaciones de despliegue remoto:

- **SMB traffic for remote deployment:** configuración de las reglas de firewall necesarias para permitir el tráfico SMB utilizado durante el despliegue remoto.
- **svc_action1:** incorporación de la cuenta de servicio `svc_action1` al grupo local de administradores de los equipos cliente, proporcionando los privilegios necesarios para las operaciones administrativas remotas.

<table width="100%" align="center">
  <tr>
    <td align="center">
      <img src="PEGAR_LINK_GPO_OU_ACTION1" width="100%">
      <br>
      <em>OU Action1 Deployment y organización de los equipos destinados a la administración remota.</em>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="PEGAR_LINK_GPO_SMB" width="100%">
      <br>
      <em>Configuración de la GPO para permitir el tráfico SMB necesario para el despliegue remoto.</em>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="PEGAR_LINK_GPO_SVC_ACTION1" width="100%">
      <br>
      <em>Configuración de la cuenta svc_action1 como administrador local de los equipos cliente.</em>
    </td>
  </tr>
</table>

## Action1 Agent Deployment

Se preparó el despliegue de los agentes de Action1 en los equipos del laboratorio para incorporarlos a la plataforma de administración centralizada.

Durante el proceso se revisaron los permisos administrativos y las reglas de firewall necesarias para permitir la comunicación y el despliegue remoto.

Una vez instalados los agentes, ambos clientes quedaron registrados en la consola de Action1 y disponibles para su administración.

<table width="100%" align="center">
  <tr>
    <td align="center">
      <img src="PEGAR_LINK_METODO_DEPLOYMENT" width="100%">
      <br>
      <em>Configuración del procedimiento de despliegue del agente de Action1.</em>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="PEGAR_LINK_ACTION1_ENDPOINTS" width="100%">
      <br>
      <em>Equipos cliente registrados en la consola de Action1.</em>
    </td>
  </tr>
</table>

## Endpoint Inventory

Se utilizó la funcionalidad de inventario de Action1 para consultar información de los endpoints administrados.

La plataforma permite recopilar información del hardware y software instalado, facilitando la identificación y el seguimiento de los equipos.

<table width="100%" align="center">
  <tr>
    <td align="center">
      <img src="PEGAR_LINK_INVENTORY_OVERVIEW" width="100%">
      <br>
      <em>Vista general del inventario de endpoints administrados.</em>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="PEGAR_LINK_HARDWARE_INVENTORY" width="100%">
      <br>
      <em>Información de hardware recopilada desde uno de los equipos cliente.</em>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="PEGAR_LINK_SOFTWARE_INVENTORY" width="100%">
      <br>
      <em>Inventario de aplicaciones y software instalado en el endpoint.</em>
    </td>
  </tr>
</table>

## Windows Update Management

Se utilizaron las funcionalidades de administración de actualizaciones de Action1 para consultar y gestionar las actualizaciones disponibles en los equipos cliente.

Se realizó una prueba de instalación de actualizaciones desde la consola centralizada, verificando posteriormente su aplicación en el endpoint correspondiente.

<table width="100%" align="center">
  <tr>
    <td align="center">
      <img src="PEGAR_LINK_UPDATES_OVERVIEW" width="100%">
      <br>
      <em>Estado de las actualizaciones disponibles para los endpoints administrados.</em>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="PEGAR_LINK_UPDATE_DEPLOYMENT" width="100%">
      <br>
      <em>Configuración y ejecución de una tarea de instalación de actualizaciones.</em>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="PEGAR_LINK_UPDATE_RESULT" width="100%">
      <br>
      <em>Verificación del resultado de la operación de actualización en el cliente.</em>
    </td>
  </tr>
</table>

## Software Deployment

Se utilizó la funcionalidad de despliegue de software para instalar aplicaciones de forma remota en los equipos administrados.

El procedimiento permitió seleccionar el software desde la plataforma, configurar el despliegue y comprobar su instalación en el endpoint de destino.

<table width="100%" align="center">
  <tr>
    <td align="center">
      <img src="PEGAR_LINK_SOFTWARE_DEPLOYMENT" width="100%">
      <br>
      <em>Selección y configuración del despliegue remoto de software.</em>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="PEGAR_LINK_SOFTWARE_RESULT" width="100%">
      <br>
      <em>Resultado del despliegue y verificación de la instalación en el equipo cliente.</em>
    </td>
  </tr>
</table>

## Script Deployment

Se probó la funcionalidad de ejecución remota de scripts integrada en Action1, utilizando scripts PowerShell disponibles en la plataforma.

Esto permitió ejecutar tareas administrativas directamente desde la consola y comprobar su resultado en los equipos administrados.

<table width="100%" align="center">
  <tr>
    <td align="center">
      <img src="PEGAR_LINK_SCRIPT_SELECTION" width="100%">
      <br>
      <em>Selección y configuración de un script PowerShell para su ejecución remota.</em>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="PEGAR_LINK_SCRIPT_EXECUTION" width="100%">
      <br>
      <em>Resultado de la ejecución del script en el endpoint seleccionado.</em>
    </td>
  </tr>
</table>

**Nota:** La ejecución de scripts personalizados quedó pendiente de habilitación por un proceso de verificación de la cuenta de Action1. Las pruebas documentadas corresponden a los scripts integrados disponibles en la plataforma.

## Conclusions and Considerations

El laboratorio permitió integrar una solución RMM con una infraestructura de Active Directory, incorporando los equipos cliente a una plataforma centralizada de administración.

Se pusieron en práctica tareas de administración remota, consulta de inventarios, gestión de actualizaciones, despliegue de aplicaciones y ejecución de scripts PowerShell.

Durante la preparación del entorno también fue necesario revisar las políticas de grupo, los privilegios administrativos y las reglas de firewall para resolver inconvenientes relacionados con el despliegue remoto.

Como posible ampliación, queda pendiente habilitar la ejecución de scripts personalizados una vez completado el proceso de verificación de la cuenta.

Este laboratorio completa el entorno desarrollado en los proyectos anteriores, incorporando una herramienta de administración centralizada de endpoints sobre la infraestructura virtualizada y el dominio Active Directory previamente implementados.
