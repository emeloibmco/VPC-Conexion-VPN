# VPC Conexión VPN ☁🖥
Breve descripción.
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

**FASE 1 - Políticas IKE**

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
<br />

## Crear políticas IPsec :hammer_and_wrench:
<br />

## Configurar políticas creadas en VPN :gear:
<br />

## Referencias :mag:
<br />

## Autores :black_nib:
Equipo IBM Cloud Tech Sales Colombia.
