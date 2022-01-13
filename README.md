# VPC Conexión VPN ☁🖥
***IBM Cloud® VPN for VPC*** proporciona una solución sencilla pero potente para redes *VPN* altamente escalables y robustas de sitio a sitio. Este servicio *VPN* ofrece una combinación de seguridad estándar del sector y opciones de cifrado así como soporte para autenticación de clave precompartida. El servicio también proporciona la posibilidad de añadir y eliminar con rapidez las conexiones *VPN* con la opción de uso de configuraciones predefinidas.

La presente guía está enfocada en la creación de una *VPN* para *VPC* junto con la respectiva configuración de las políticas de Fase 1 (IKE) y de Fase 2 (IPsec). 

<br />

## Índice  📰
1. [Pre-Requisitos](#Pre-Requisitos-pencil)
2. [Datos de Configuración VPN](#Datos-de-Configuración-VPN-cloud)
3. [Crear VPN basada en rutas](#Crear-VPN-basada-en-rutas-computer)
   * [Crear políticas IKE](#Crear-políticas-IKE-wrench)
   * [Crear políticas IPsec](#Crear-políticas-IPsec-hammer_and_wrench)
   * [Configurar políticas creadas en VPN](#Configurar-políticas-creadas-en-VPN-gear)
4. [Crear VPN basada en políticas](#Crear-VPN-basada-en-políticas-computer)
5. [Ejercicio]
7. [Referencias](#Referencias-mag)
8. [Autores](#Autores-black_nib)
<br />

## Pre-Requisitos :pencil:
* Contar con una cuenta en <a href="https://cloud.ibm.com/"> IBM Cloud </a>.
* Contar con una *VPC* y una subred.
<br />

## Datos de Configuración VPN :cloud:

### IP Peer
| ***INFORMACIÓN DEL DISPOSITIVO GATEWAY DE VPN*** | ***REMOTO (PROVEEDOR)*** |
|     :---:      |     :---:      |
| IP Peer  | 169.47.83.154 |
<br />

### FASE 1 - Políticas IKE

| ***PROPIEDADES DEL TÚNEL*** | ***REMOTO (PROVEEDOR)*** |
| :---         |     :---:      |
| Encryption Scheme  | IKE v2 |
| Diffie-Hellman Group  | 19  |
| Encryption Algorithm | Aes256 |
| Hashing Algorithm | Sha256 |
| Lifetime (for renegotiation) | 28800 |
<br />

### FASE 2 - Políticas IPsec
| ***PROPIEDADES DEL TÚNEL*** | ***REMOTO (PROVEEDOR)*** |
| :---         |     :---:      |
| Encryption Algorithm | Aes256  |
| Authentication Algorithm | Sha512 |
| Perfect Forward Secrecy | disable |
| Diffie-Hellman Group | 2 |
| Lifetime (for renegotiation) | 3600 |
<br />

## Crear VPN basada en rutas :computer:
El primer paso consiste en crear la *VPN* basada en rutas. Para ello, realice los pasos que se muestran a continuación:

1. En la sección de ```Red``` seleccione la opción ```Pasarelas VPN``` y de click en el botón ```Crear```. Una vez le aparezca la ventana para la configuración y creación de la *VPN*, complete lo siguiente:
* ```Nombre```: asigne un nombre exclusivo para la *VPN*.
* ```Grupo de recursos```: seleccione el grupo de recursos en el cual va a trabajar (el mismo correspondiente a la *VPC*).
* ```Ubicación```: seleccione la ubicación en la cual desea implementar la *VPN* (la misma correspondiente a la *VPC*).
* ```Nube privada virtual```: seleccione la *VPC* con la cual está trabajando.
* ```Subred```: seleccione la subred con la cual está trabajando.
* ```Modalidad```: seleccione la opción ```Basada en rutas```.
<br />

A continuación habilite la opción ```Nueva conexión VPN para VPC``` y complete los campos que salen a continuación:
<br />

**Detalles de conexión**.
* ```Nombre de conexión VPN```: asigne un nombre exclusivo para la conexión de la *VPN*.
* ```Dirección de pasarela de igual```: complete el campo con la dirección IP porporcionada en [IP Peer](#IP-Peer). 
* ```Pre-shared Key (clave precompartida)```: asigne una clave que establezca junto con el cliente.
<br />

**Detección de igual caído**.
* No modifique los parámetros. Deje los valores establecidos por defecto.
<br />

**Políticas**.
* No modifique los parámetros. Deje los valores establecidos por defecto.
<br />

<p align="center"><img width="700" src="https://github.com/emeloibmco/VPC-Conexion-VPN/blob/main/Imagenes/vpn.gif"></p>

Cuando ya tenga todos los campos configurados de click en el botón ```Crear pasarela VPN```.
<br />

2. Espere unos minutos mientras la *VPN* es desplegada y asegúrese de tener seleccionada la región en la cual la implementó.
<br />

>NOTA: Luego de crear la *VPN* basada en rutas debe completar los siguientes procedimientos
   * [Crear políticas IKE](#Crear-políticas-IKE-wrench)
   * [Crear políticas IPsec](#Crear-políticas-IPsec-hammer_and_wrench)
   * [Configurar políticas creadas en VPN](#Configurar-políticas-creadas-en-VPN-gear)
<br />

## Crear políticas IKE :wrench:
Una vez ha configurado la *VPN*, se deben crear las politicas IKE, de acuerdo a los datos de configuración especificados en la tabla [FASE 1 - Políticas IKE](#FASE-1---Políticas-IKE), para esto complete los siguientes pasos:
1. En la sección de ```Infraestructura de VPC``` seleccione la opción ```Pasarelas VPN```>```Políticas IKE``` y posteriormente de click en el botón ```Crear```. Una vez le aparezca la ventana para la configuración y creación de la *Política IKE*, complete lo siguiente:  
* ```Nombre```: asigne un nombre exclusivo para la *Política IKE*.
* ```Grupo de recursos```: seleccione el grupo de recursos en el cual va a trabajar (el mismo seleccionado en la creación de la *VPN*).
* ```Ubicación```: seleccione la ubicación en la cual desea implementar la Política (la misma seleccionada en la creación de la *VPN*).

Los siguientes parámetros se escogen de acuerdo a lo especificado en la tabla [FASE 1 - Políticas IKE](#FASE-1---Políticas-IKE):
* ```Versión de IKE```:2
* ```Autenticación```: Sha512
* ```Cifrado```: Aes256
* ```Grupo Diffie-Hellman ```: 19
* ```Tiempo de vida de la clave```: 28800

Cuando ya tenga todos los campos configurados de click en el botón ```Crear política IKE```.
<p align="center"><img width="700" src="https://github.com/emeloibmco/VPC-Conexion-VPN/blob/main/Imagenes/ike.gif"></p>

2. Espere unos minutos mientras la *Política IKE* es desplegada y asegúrese de tener seleccionada la región en la cual la implementó.
<br />

## Crear políticas IPsec :hammer_and_wrench:
El siguiente paso es crear las politicas IPsec, de acuerdo a los datos de configuración especificados en la Tabla [FASE 2 - Políticas IPsec](#FASE-2---Políticas-IPsec), para esto complete los siguientes pasos:
1. En la sección de ```Infraestructura de VPC``` seleccione la opción ```Pasarelas VPN```>```Políticas IPsec``` y posteriormente de click en el botón ```Crear```. Una vez le aparezca la ventana para la configuración y creación de la *Política IPsec*, complete lo siguiente:  
* ```Nombre```: asigne un nombre exclusivo para la *Política IPsec*.
* ```Grupo de recursos```: seleccione el grupo de recursos en el cual va a trabajar (el mismo seleccionado en la creación de la *VPN*).
* ```Ubicación```: seleccione la ubicación en la cual desea implementar la Política (la misma seleccionada en la creación de la *VPN*).

Los siguientes parámetros se escogen de acuerdo a lo especificado en la tabla [FASE 2 - Políticas IPsec](#FASE-2---Políticas-IPsec):
* ```Autenticación```: Sha512
* ```Cifrado```: Aes256
* ```Secreto de reenvio perfecto```: Inhabilitado
* ```Tiempo de vida de la clave```: 3600

Cuando ya tenga todos los campos configurados de click en el botón ```Crear política IPsec```.
<p align="center"><img width="700" src="https://github.com/emeloibmco/VPC-Conexion-VPN/blob/main/Imagenes/ipsec.gif"></p>

2. Espere unos minutos mientras la *Política IPsec* es desplegada y asegúrese de tener seleccionada la región en la cual la implementó.
<br />

## Configurar políticas creadas en VPN :gear:
1. Por último dirijase a ```Pasarelas VPN``` e ingrese a la *VPN* que se creo anteriormente, al final de la pantalla encontrará  ```Conexiones VPN```, ingrese a la conexión que tuvo que crear cuando aprovisionó la *VPN*.
2. En ```Visión general``` > ```Detalles de conexión VPN``` edite las políticas *IKE* e *IPsec* y seleccione las que creó anteriormente, recuerde guadar los cambios.
> NOTA: La conexión aparece como inactiva, debido a que se debe gestionar la conexión del lado del cliente. 
<p align="center"><img width="700" src="https://github.com/emeloibmco/VPC-Conexion-VPN/blob/main/Imagenes/añadirpoliticas.gif"></p>
<br />

## Crear VPN basada en políticas :computer:
Para crear una *VPN* basada en políticas complete los pasos que se muestran a continuación:

1. En la sección de ```Red``` seleccione la opción ```Pasarelas VPN``` y de click en el botón ```Crear```. Una vez le aparezca la ventana para la configuración y creación de la *VPN*, complete lo siguiente:
* ```Nombre```: asigne un nombre exclusivo para la *VPN*.
* ```Grupo de recursos```: seleccione el grupo de recursos en el cual va a trabajar (el mismo correspondiente a la *VPC*).
* ```Ubicación```: seleccione la ubicación en la cual desea implementar la *VPN* (la misma correspondiente a la *VPC*).
* ```Nube privada virtual```: seleccione la *VPC* con la cual está trabajando.
* ```Subred```: seleccione la subred con la cual está trabajando.
* ```Modalidad```: seleccione la opción ```Basada en políticas```.

A continuación habilite la opción ```Nueva conexión VPN para VPC/Create VPN Connection for VPC``` y complete los campos que salen a continuación:
<br />

**Detalles de conexión/Connection details**.
* ```Nombre de conexión VPN/VPN connection name```: asigne un nombre exclusivo para la conexión de la *VPN*.
* ```Dirección de pasarela de igual/Peer gateway address```: complete el campo con la dirección IP porporcionada en [IP Peer](#IP-Peer). 
* ```Pre-shared Key (clave precompartida)```: asigne una clave que establezca junto con el cliente.
* ```Local IBM CIDRs```: enumere los CIDR de esta VPC de IBM, que desea conectar a través del túnel VPN.
* ```Peer CIDRs```: enumere los CIDR detrás del peer gateway a la que desea conectarse a través del túnel VPN.
<br />

**Detección de igual caído/Dear peer detection**.
* No modifique los parámetros. Deje los valores establecidos por defecto.
<br />

**Políticas/Policies**.
* ```IKE Policy```:
  * De click en la opción ```Create IKE Policy```.
  * ```Name```: asigne un nombre exclusivo.
  * ```Resource group```: seleccione el grupo de recursos.
  * ```Región```: seleccione la región.
  * ```IKE version```: indique la versión, en este caso 1.
  * ```Authentication```: seleccione el valor de autenticación, en este caso ```sha256```.
  * ```Encryption```: seleccione el tipo de cifrado, en esta caso ```aes256```.
  * ```Diffie-Hellman Group```: indique el valor correspondiente, en este caso 5.
  * ```Key lifetime```: indique el valor correspondiente, en este caso ```36000```.
  * Presione el botón ```Create IKE policy```.

* ```IPsec Policy```:
  * De click en la opción ```Create IPsec Policy```.
  * ```Name```: asigne un nombre exclusivo.
  * ```Resource group```: seleccione el grupo de recursos.
  * ```Región```: seleccione la región.
  * ```Authentication```: seleccione el valor de autenticación, en este caso ```sha256```.
  * ```Encryption```: seleccione el tipo de cifrado, en esta caso ```aes256```.
  * Habilite la opción ```Perfect Forward Secrecy```.
  * ```Diffie-Hellman Group```: indique el valor correspondiente, en este caso 2.
  * ```Key lifetime```: indique el valor correspondiente, en este caso ```10800```.
  * Presione el botón ```Create IPsec policy```.

<br />

Cuando ya tenga todos los campos configurados de click en el botón ```Crear pasarela VPN/Create VPN gateway```.
<br />

<p align="center"><img width="700" src="https://github.com/emeloibmco/VPC-Conexion-VPN/blob/main/Imagenes/vpnp.gif"></p>

<br />

## Ejercicio
para el ejercicio presentado en el <a href="https://github.com/emeloibmco/Gateway-Appliance-Juniper-vSRX-version-20.4"> repositorio </a> en donde se presentan los pasos a seguir para establecer una conexión entre una VPN en VPC y un servicio de Juniper en una cuenta de IBM Cloud distinta. Se debe tener en cuenta la siguiente configuración para las políticas```IKE Policy```
<br />


<p align="center"><img width="700" src="https://github.com/emeloibmco/VPC-Conexion-VPN/blob/main/Imagenes/Ejercicio.png"></p>

<br />
## Referencias :mag:
* <a href="https://cloud.ibm.com/docs/vpc?topic=vpc-using-vpn"> VPC using VPN </a>.
* <a href="https://cloud.ibm.com/docs/vpc?topic=vpc-vpn-adding-connections&interface=ui"> Adding connections to a VPN gateway </a>.
<br />

## Autores :black_nib:
Equipo IBM Cloud Tech Sales Colombia.
