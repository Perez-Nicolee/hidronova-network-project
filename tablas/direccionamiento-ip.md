# Tabla de Direccionamiento IP para Servidores

A continuación se detalla la asignación de direcciones IP estáticas (tanto internas como públicas) para los servidores del proyecto, garantizando que todos sean accesibles desde el exterior mediante traducción de direcciones (NAT/PAT) o, en caso de servidores internos, restringiendo su acceso al ámbito privado.

> [!NOTE]
> Dado que el bloque de direcciones IP públicas asignado comienza en `200.45.110.128`, se asume que esta dirección representa el identificador de red. Por lo tanto, la primera dirección IP pública utilizable para hosts externos es `200.45.110.129`.

| Nombre Servidor | IP Estática Interna | IP Estática Pública |
| :--- | :--- | :--- |
| Web Principal | 172.29.0.3 | 200.45.110.129 |
| DNS Primario Público | 172.29.0.4 | 200.45.110.130 |
| DNS Secundario Público | 172.29.0.5 | 200.45.110.131 |
| Server Correo | 172.29.0.11 | 200.45.110.132 |
| Web Logística y Transporte | 192.168.145.2 | 200.45.110.133 |
| DNS Primario Logistica Publico | 192.168.145.3 | 200.45.110.134 |
| DNS Secundario Logistica Publico | 192.168.145.4 | 200.45.110.135 |
| DNS Primario Logistica PRIVADO | 192.168.145.5 | N/A |
| DNS Secundario Logistica PRIVADO | 192.168.145.6 | N/A |
| Web Gestion Logistica Interna | 172.29.0.7 | N/A |
| Web Intranet Administración | 172.29.0.8 | N/A |
| Servidor DHCP | 172.29.0.12 | N/A |
| DNS Local Resolver | 172.29.0.13 | N/A |
| DNS Primario Privado | 172.29.0.14 | N/A |
| DNS Secundario Privado | 172.29.0.15 | N/A |
