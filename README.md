# VPC Conexión VPN ☁🖥
*VPN for VPC* proporciona una solución sencilla pero potente para redes VPN altamente escalables y robustas de sitio a sitio. Este servicio VPN ofrece una combinación de seguridad estándar del sector y opciones de cifrado así como soporte para autenticación de clave precompartida. El servicio también proporciona la posibilidad de añadir y eliminar con rapidez las conexiones VPN con la opción de uso de configuraciones predefinidas.

En la presente guía, se 
<br />

## Índice  📰
1. [Pre-Requisitos](#Pre-Requisitos-pencil)
2. [Datos de Configuración VPN](#Datos-de-Configuración-VPN-cloud)
3. [Crear VPN](#Crear-VPN-computer)
4. [Crear políticas IKE](#Crear-políticas-IKE-wrench)
5. [Crear políticas IPsec](#Crear-políticas-IPsec-hammer_and_wrench)
6. [Configurar políticas creadas en VPN](#Configurar-políticas-creadas-en-VPN-gear)
7. [Referencias](#Referencias-mag)
8. [Autores](#Autores-black_nib)
<br />

## Pre-Requisitos :pencil:
* Contar con una cuenta en <a href="https://cloud.ibm.com/"> IBM Cloud </a>.
* Contar con una VPC y una subred.
<br />

## Datos de Configuración VPN :cloud:

### FASE 1 Políticas IKE

| ***PROPIEDADES DEL TÚNEL*** | ***REMOTO (PROVEEDOR)*** |
| :---         |     :---:      |
| Encryption Scheme  | IKE v2 |
| Diffie-Hellman Group  | 19  |
| Encryption Algorithm | Aes256 |
| Hashing Algorithm | Sha256 |
| Lifetime (for renegotiation) | 28800 |
<br />

**FASE 2 - Políticas IPsec**
| ***PROPIEDADES DEL TÚNEL*** | ***REMOTO (PROVEEDOR)*** |
| :---         |     :---:      |
| Encryption Algorithm | Aes256  |
| Authentication Algorithm | Sha512 |
| Perfect Forward Secrecy | disable |
| Diffie-Hellman Group | 2 |
| Lifetime (for renegotiation) | 3600 |

Pendiente IP Cliente.

<br />

## Crear VPN :computer:
<br />

## Crear políticas IKE :wrench:
Una vez a configurada la *VPN*, se deben crear las politicas IKE, de acuerdo a los datos de configuración especificados en la Tabla de Fase 1, para esto complete los siguientes pasos:
1. En la sección de ```Infraestructura de VPC``` seleccione la opción ```Pasarelas VPN```>```Políticas IKE``` y posteriormente de click en el botón ```Crear```. Una vez le aparezca la ventana para la configuración y creación de la *Política IKE*, complete lo siguiente:  
* ```Nombre```: asigne un nombre exclusivo para la *Política IKE*.
* ```Grupo de recursos```: seleccione el grupo de recursos en el cual va a trabajar (el mismo seleccionado en la creación de la *VPN*).
* ```Ubicación```: seleccione la ubicación en la cual desea implementar la Política (la misma seleccionada en la creación de la *VPN*).

Los siguientes parámetros se escogen de acuerdo a lo especificado en la tabla [FASE 1 Políticas IKE](#FASE-1-Políticas-IKE):
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
<br />

## Configurar políticas creadas en VPN :gear:
<br />

## Referencias :mag:
<br />

## Autores :black_nib:
Equipo IBM Cloud Tech Sales Colombia.
