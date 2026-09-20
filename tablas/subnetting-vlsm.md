# Tabla de Subneteo

| VLAN | Red | Máscara | Rango de hosts | Broadcast |
| :--- | :--- | :--- | :--- | :--- |
| **Sistemas + Centro de Datos** | 172.29.0.0 | /24 (255.255.255.0) | 172.29.0.1 - 172.29.0.254 | 172.29.0.255 |
| **Gerencia** | 172.29.1.0 | /25 (255.255.255.128) | 172.29.1.1 - 172.29.1.126 | 172.29.1.127 |
| **Administración** | 172.29.1.128 | /26 (255.255.255.192) | 172.29.1.129 - 172.29.1.190 | 172.29.1.191 |
| **Logística** | 172.29.1.192 | /26 (255.255.255.192) | 172.29.1.193 - 172.29.1.254 | 172.29.1.255 |

## Sedes y Enlaces WAN

| Sede / Enlace | Red | Máscara | Rango de hosts | Broadcast | Notas |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Sede Jujuy** | 192.168.145.0/26 | /26 (255.255.255.192) | 192.168.145.1 - 192.168.145.62 | 192.168.145.63 | 32 puestos de trabajo + 16 servidores + APs/Impresoras (necesita 50-60 IPs) |
| **Sede Catamarca** | 192.168.145.64/26 | /26 (255.255.255.192) | 192.168.145.65 - 192.168.145.126 | 192.168.145.127 | 20 puestos de trabajo + 4 servidores + APs/Impresoras |
| **Enlace WAN CABA - Jujuy** | 192.168.145.128/30 | /30 (255.255.255.252) | 192.168.145.129 - 192.168.145.130 | 192.168.145.131 | Red Punto a Punto (IPs útiles: 2) |
| **Enlace WAN CABA - Catamarca** | 192.168.145.132/30 | /30 (255.255.255.252) | 192.168.145.133 - 192.168.145.134 | 192.168.145.135 | Red Punto a Punto (IPs útiles: 2) |
| **Enlace WAN Jujuy - Catamarca** | 192.168.145.136/30 | /30 (255.255.255.252) | 192.168.145.137 - 192.168.145.138 | 192.168.145.139 | Red Punto a Punto (IPs útiles: 2) |
