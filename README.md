# Administración de Endpoints con Action1

Implementación de una solución de administración centralizada de endpoints mediante **Action1**, integrada con una infraestructura de Active Directory sobre Windows Server 2025.

El laboratorio utiliza dos clientes Windows 11 LTSC unidos al dominio `mydomain.com`. A través de Action1, se realizaron tareas de administración remota, consulta de inventarios de hardware y software, gestión de actualizaciones, despliegue de aplicaciones y ejecución de scripts de PowerShell.

![](https://i.imgur.com/AQqKGoo.png)

## Entorno

- **Endpoint Management Platform:** Action1
- **Server:** Windows Server 2025
- **Clients:** 2 × Windows 11 LTSC
- **Domain:** `mydomain.com`
- **Directory Service:** Active Directory Domain Services (AD DS)
- **Endpoint Management:** Action1 RMM
- **Management Tasks:** Software Deployment, Script Deployment, Windows Update Management

## Integración con Active Directory

Se preparó el entorno de Active Directory para facilitar el despliegue remoto de los agentes y la posterior administración de los equipos mediante Action1.

Se creó una OU específica denominada `Action1 Deployment`, destinada a organizar los equipos que serían incorporados a la plataforma.

### Configuración de Directivas de Grupo (GPO)

Se configuraron dos GPOs para habilitar las condiciones necesarias para el despliegue remoto:

- **SMB traffic for remote deployment:** configuración de las reglas de firewall necesarias para permitir el tráfico SMB utilizado durante el despliegue remoto.
- **svc_action1:** incorporación de la cuenta de servicio `svc_action1` al grupo local de administradores de los equipos cliente, proporcionando los privilegios necesarios para las operaciones de despliegue.

<table width="100%" align="center">
  <tr>
    <td align="center">
      <img src="https://i.imgur.com/VvAqgZf.png" width="100%">
      <br>
      <em>OU Action1 Deployment y organización de los equipos destinados a la administración remota.</em>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="https://i.imgur.com/jo0EJLE.png" width="100%">
      <br>
      <em>Configuración de la GPO para permitir el tráfico SMB necesario para el despliegue remoto.</em>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="https://i.imgur.com/8C9cxKz.png" width="100%">
      <br>
      <em>Configuración de la GPO para agregar la cuenta svc_action1 al grupo local de administradores de los equipos cliente.</em>
    </td>
  </tr>
</table>

## Despliegue de Action1 Agents

Se utilizó el procedimiento de despliegue remoto desde el Domain Controller para instalar los agentes de Action1 en los equipos del laboratorio.

Durante la preparación se configuraron los permisos administrativos y las reglas de firewall necesarias para permitir la operación.

Una vez instalados, ambos agentes se registraron correctamente en la consola de Action1, dejando los equipos disponibles para su administración centralizada.

<table width="100%" align="center">
  <tr>
    <td align="center">
      <img src="https://i.imgur.com/CrhRuMc.png" width="100%">
      <br>
      <em>Configuración del despliegue remoto del agente de Action1 mediante la cuenta svc_action1.</em>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="https://i.imgur.com/R0LsOO7.png" width="100%">
      <br>
      <em>Equipos cliente registrados en la consola de Action1.</em>
    </td>
  </tr>
</table>

## Inventario de Endpoints

Se utilizó la funcionalidad de inventario de Action1 para consultar información de los endpoints administrados.

La plataforma permite recopilar información del hardware y del software instalado, facilitando la identificación y el seguimiento de los equipos.

<table width="100%" align="center">
  <tr>
    <td align="center">
      <img src="https://i.imgur.com/XrlQiP6.png" width="100%">
      <br>
      <em>Vista general del inventario de endpoints administrados.</em>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="https://i.imgur.com/uJuzXxe.png" width="100%">
      <br>
      <em>Información de hardware recopilada desde uno de los equipos cliente.</em>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="https://i.imgur.com/BzWEMsh.png" width="100%">
      <br>
      <em>Inventario de aplicaciones y software instalado en un endpoint.</em>
    </td>
  </tr>
</table>

## Grupos de Endpoints

Se crearon los siguientes grupos de endpoints para organizar los equipos y simular una estructura de administración por sucursales:

- `ARG Branch`
- `USA Branch`
- `All Branches`

Estos grupos permiten aplicar tareas de administración a equipos específicos o a todos los endpoints del entorno.

## Administración de Actualizaciones de Windows

Se utilizaron las funcionalidades de administración de actualizaciones de Action1 para consultar y gestionar las actualizaciones disponibles en los equipos cliente.

Se realizó una prueba de instalación desde la consola centralizada y posteriormente se verificó la aplicación de las actualizaciones en el endpoint correspondiente.

## Despliegue de Software

Se utilizó la funcionalidad de despliegue de software para instalar aplicaciones de forma remota en los equipos administrados.

El procedimiento permitió seleccionar el software desde la plataforma, configurar el despliegue y comprobar el resultado en los endpoints de destino.

### Despliegue de Notepad++

En el primer ejemplo se desplegó Notepad++ en los endpoints pertenecientes al grupo `ARG Branch`.

<table width="100%" align="center">
  <tr>
    <td align="center">
      <img src="https://i.imgur.com/GOAws7R.png" width="100%">
      <br>
      <em>Verificación de que Notepad++ no se encontraba instalado previamente.</em>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="https://i.imgur.com/0l1lyuC.png" width="100%">
      <br>
      <em>Selección y configuración del despliegue remoto de software en el grupo ARG Branch.</em>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="https://i.imgur.com/cs98QQY.png" width="100%">
      <br>
      <em>Detalles del proceso de despliegue en Action1.</em>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="https://i.imgur.com/ZulC2Re.png" width="100%">
      <br>
      <em>Resultado del despliegue y verificación de la instalación desde Action1.</em>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="https://i.imgur.com/Sj3TjqM.png" width="100%">
      <br>
      <em>Verificación de la instalación directamente desde el equipo cliente.</em>
    </td>
  </tr>
</table>

### Despliegue de VLC Media Player

En un segundo ejemplo se desplegó VLC Media Player en todos los endpoints del grupo `All Branches`. Posteriormente, se realizó una desinstalación remota para comprobar también esa funcionalidad.

<table width="100%" align="center">
  <tr>
    <td align="center">
      <img src="https://i.imgur.com/hMJT67u.png" width="100%">
      <br>
      <em>Selección y configuración del despliegue remoto de software en el grupo All Branches.</em>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="https://i.imgur.com/lO5GFrG.png" width="100%">
      <br>
      <em>Detalles del proceso de despliegue en Action1.</em>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="https://i.imgur.com/C0gbIMu.png" width="100%">
      <br>
      <em>Verificación de la instalación desde Action1 en CLIENT1.</em>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="https://i.imgur.com/QO93lHK.png" width="100%">
      <br>
      <em>Verificación de la instalación desde Action1 en CLIENT2.</em>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="https://i.imgur.com/dgHm214.png" width="100%">
      <br>
      <em>Verificación de la instalación directamente desde los equipos cliente.</em>
    </td>
  </tr>
</table>

Para comprobar la funcionalidad de desinstalación, se siguió el mismo procedimiento y se verificó posteriormente la eliminación del software.

<table width="100%" align="center">
  <tr>
    <td align="center">
      <img src="https://i.imgur.com/wSMNBNP.png" width="100%">
      <br>
      <em>Detalles del proceso de desinstalación en Action1.</em>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="https://i.imgur.com/a1OeBAL.png" width="100%">
      <br>
      <em>Verificación de la desinstalación mediante el inventario de software de los endpoints.</em>
    </td>
  </tr>
</table>

## Ejecución Remota de Scripts

Se probó la funcionalidad de ejecución remota de scripts integrada en Action1, utilizando scripts de PowerShell disponibles en la plataforma.

Esto permitió ejecutar tareas administrativas desde la consola centralizada y consultar los resultados de ejecución en los equipos administrados.

<table width="100%" align="center">
  <tr>
    <td align="center">
      <img src="https://i.imgur.com/bZUVNAW.png" width="100%">
      <br>
      <em>Detalles del script seleccionado.</em>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="https://i.imgur.com/x5A67yX.png" width="100%">
      <br>
      <em>Detalles del proceso de ejecución del script.</em>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="https://i.imgur.com/jGVm98X.png" width="100%">
      <br>
      <em>Resultado de la ejecución del script en el endpoint seleccionado.</em>
    </td>
  </tr>
</table>

**Nota:** La ejecución de scripts personalizados quedó pendiente de habilitación debido a un proceso de verificación de la cuenta de Action1. Las pruebas documentadas corresponden a los scripts integrados disponibles en la plataforma.

## Conclusiones y Consideraciones

El laboratorio permitió integrar una solución RMM (*Remote Monitoring and Management*) con una infraestructura de Active Directory, incorporando los equipos cliente a una plataforma centralizada de administración.

Se pusieron en práctica tareas de administración remota, consulta de inventarios, gestión de actualizaciones, despliegue y desinstalación de aplicaciones, y ejecución de scripts de PowerShell.

Durante la preparación del entorno también fue necesario revisar las políticas de grupo, los privilegios administrativos y las reglas de firewall para resolver inconvenientes relacionados con el despliegue remoto.

Como posible ampliación, queda pendiente habilitar la ejecución de scripts personalizados una vez completado el proceso de verificación de la cuenta.

Este laboratorio completa los proyectos anteriores, incorporando una herramienta de administración centralizada de endpoints sobre la infraestructura virtualizada y el dominio Active Directory previamente implementados.
