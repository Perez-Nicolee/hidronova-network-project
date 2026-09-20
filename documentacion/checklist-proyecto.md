# Checklist de Implementación - HidroNova S.A.
## Proyecto Integrador Redes de Computadoras 1S2026

**Estado actual del .pkt:** 124 dispositivos, 115 conexiones

---

## FASE 1: INFRAESTRUCTURA FÍSICA Y TOPOLOGÍA

### 1.1 Sede CABA (172.29.0.0/23)
- [ ] **Edificio**
  - [X] ~~Router CABA (conectado a switches de piso, enlaces de fibra a sedes y serial al ISP)~~
  - [X] ~~Switches de piso (uno por piso con departamentos)~~
  - [X] ~~PCs por departamento (configurados con IP estática o DHCP)~~
  - [ ] Access Points inalámbricos (configurados con SSID y WPA2)
  - [ ] IP Phones (configurados)
  - [ ] Printers (configurados)

- [ ] **Conexión entre edificios CABA**
  - [X] ~~Fibra óptica configurada entre edificios~~
  - [X] ~~Interfaces de fibra configuradas en routers/switches~~

### 1.2 Sede Jujuy (192.168.145.0/26)
- [X] ~~Router Jujuy~~
- [X] ~~Switches de piso~~
- [X] ~~PCs por departamento~~
- [X] ~~Access Points inalámbricos~~
- [X] ~~IP Phones~~
- [X] ~~Printers~~
- [X] ~~Conexión WAN a CABA (Fibra óptica Gigabit)~~

### 1.3 Sede Catamarca (192.168.145.64/26)
- [X] ~~Router Catamarca~~
- [X] ~~Switches de piso~~
- [X] ~~PCs por departamento~~
- [ ] Access Points inalámbricos
- [X] ~~IP Phones~~
- [ ] Printers
- [X] ~~Conexión WAN a CABA (Fibra óptica Gigabit)~~

### 1.4 Segmento Público / Internet
- [ ] Router Internet (ISP)
- [ ] Interfaz serial hacia CABA (205.32.130.0/30)
- [ ] Servidor que simula Google (IP: 64.223.190.94)
- [ ] Switch Google
- [ ] DNS Local Resolver Google (8.8.8.8)
- [ ] PC Google (para pruebas)

---

## FASE 2: DIRECCIONAMIENTO IP Y VLANs

### 2.1 Subneteo y VLANs CABA
- [X] ~~VLAN 10: Administración~~
- [X] ~~VLAN 20: Logistica~~
- [X] ~~VLAN 30: Gerencia~~
- [X] ~~VLAN 40: Sistemas y Centro de Datos~~

### 2.2 Direccionamiento Jujuy (Único segmento plano)
- [X] ~~Configurar red local Jujuy: 192.168.145.0/26 (32 puestos + servidores + APs/Printers)~~

### 2.3 Direccionamiento Catamarca (Único segmento plano)
- [X] ~~Configurar red local Catamarca: 192.168.145.64/26 (20 puestos + servidores + APs/Printers)~~

### 2.4 Segmentos WAN (Interconexión de routers)
- [X] ~~WAN Fibra CABA-Jujuy: 192.168.145.128/30~~
- [X] ~~WAN Fibra CABA-Catamarca: 192.168.145.132/30~~
- [X] ~~WAN Fibra Jujuy-Catamarca: 192.168.145.136/30~~
- [ ] WAN Serial CABA-Internet: 205.32.130.0/30

### 2.5 Segmentación de Servidores
- [X] ~~Servidores CABA (VLAN 40): Subred 172.29.0.0/24~~
- [X] ~~Servidores Jujuy (Locales): IPs asignadas dentro del rango 192.168.145.0/26 (ej: DNS Logística, Web Logística)~~

---

## FASE 3: CONFIGURACIÓN DE SWITCHES

### 3.1 Configuración VLANs en Switches
- [X] ~~Crear todas las VLANs en switches de CABA~~
- [X] ~~Asignar puertos de acceso a VLANs correspondientes~~
- [X] ~~Configurar puertos trunk entre switches y routers~~

### 3.2 Trunking
- [X] ~~Configurar trunk entre Router Core y Switches~~
- [X] ~~Configurar trunk entre switches interconectados~~
- [ ] Verificar que las VLANs pasen por los trunks

### 3.3 Switches de Piso
- [X] ~~Configurar switchport mode access en puertos de PCs~~
- [X] ~~Configurar switchport access vlan [ID] en cada puerto~~
- [X] ~~Configurar puertos de Access Points~~
- [X] ~~Configurar puertos de IP Phones~~
- [X] ~~Configurar puertos de Printers~~

---

## FASE 4: CONFIGURACIÓN DE ROUTERS

### 4.1 Router CABA (Unificado)
- [X] ~~Configurar subinterfaces para cada VLAN de CABA (VLANs 10, 20, 30, 40)~~
- [X] ~~Asignar IPs a subinterfaces (gateways de cada VLAN)~~
- [X] ~~Configurar encapsulation dot1Q en subinterfaces de CABA~~
- [X] ~~Configurar interfaz WAN Fibra hacia Jujuy (192.168.145.129/30)~~
- [X] ~~Configurar interfaz WAN Fibra hacia Catamarca (192.168.145.133/30)~~
- [X] ~~Configurar interfaz WAN Serial hacia ISP (205.32.130.1/30)~~
- [X] ~~Habilitar interfaces (no shutdown)~~

### 4.2 Router Jujuy
- [X] ~~Configurar interfaz WAN Fibra hacia CABA (192.168.145.130/30)~~
- [X] ~~Configurar interfaz WAN Fibra hacia Catamarca (192.168.145.137/30)~~
- [X] ~~Configurar interfaz Gigabit Ethernet hacia LAN Jujuy (192.168.145.1/26)~~

### 4.3 Router Catamarca
- [X] ~~Configurar interfaz WAN Fibra hacia CABA (192.168.145.134/30)~~
- [X] ~~Configurar interfaz WAN Fibra hacia Jujuy (192.168.145.138/30)~~
- [X] ~~Configurar interfaz Gigabit Ethernet hacia LAN Catamarca (192.168.145.65/26)~~

### 4.4 Router Internet (ISP)
- [ ] Configurar interfaz serial hacia CABA (205.32.130.2/30)
- [ ] Configurar interfaz hacia servidor Google (64.223.190.1/24)

---

## FASE 5: RUTEO ESTÁTICO

### 5.1 Rutas en Router CABA
- [X] ~~Ruta hacia red Jujuy (192.168.145.0/26) vía 192.168.145.130~~
- [X] ~~Ruta hacia red Catamarca (192.168.145.64/26) vía 192.168.145.134~~
- [X] ~~Ruta por defecto (0.0.0.0 0.0.0.0) hacia Internet vía ISP (205.32.130.2)~~

### 5.2 Rutas en Router Jujuy
- [X] ~~Ruta por defecto (0.0.0.0 0.0.0.0) hacia CABA vía 192.168.145.129 (para salida a Internet y CABA)~~
- [X] ~~Ruta hacia Catamarca (192.168.145.64/26) vía 192.168.145.138 (enlace directo por fibra)~~

### 5.3 Rutas en Router Catamarca
- [X] ~~Ruta por defecto (0.0.0.0 0.0.0.0) hacia CABA vía 192.168.145.133 (para salida a Internet y CABA)~~
- [X] ~~Ruta hacia Jujuy (192.168.145.0/26) vía 192.168.145.137 (enlace directo por fibra)~~

### 5.4 Rutas en Router Internet (ISP)
- [ ] Ruta hacia red pública de HidroNova (200.45.110.128/25) vía 205.32.130.1 (IP externa de CABA)
- [ ] *Nota: No configurar rutas hacia subredes privadas RFC 1918 (172.29.x.x o 192.168.x.x)*

---

## FASE 6: NAT (Network Address Translation)

### 6.1 Configuración NAT en Router CABA
- [X] ~~Configurar interfaz inside (subinterfaces de VLANs y puertos hacia sedes remotas)~~
- [X] ~~Configurar interfaz outside (puerto serial hacia Internet)~~
- [X] ~~Crear ACL para redes internas permitidas (172.29.0.0/23 y 192.168.145.0/24)~~
- [X] ~~Configurar NAT overload (PAT) asociando la ACL con la IP pública del puerto serial~~
- [X] ~~Configurar NAT estático para el Servidor Web Principal (IP interna -> IP pública del bloque asignado)~~
- [X] ~~Configurar NAT estático para el Servidor de Correo (IP interna -> IP pública)~~
- [ ] Verificar traducción NAT desde redes internas a Internet

---

## FASE 7: SERVICIOS DHCP

### 7.1 DHCP Server CABA (Centralizado en IP 172.29.0.70/23)
- [X] ~~Habilitar servicio DHCP en el servidor de CABA~~
- [X] ~~Crear pool para cada VLAN de CABA (Administración, Logística, Gerencia, Sistemas)~~
- [X] ~~Configurar gateway por defecto y DNS server en cada pool de CABA~~
- [X] ~~Excluir IPs de servidores y de interfaces de routers en cada subred~~

### 7.2 DHCP en Sede Jujuy (Único segmento)
- [X] ~~Configurar pool para Jujuy (en servidor DHCP CABA o localmente en Router Jujuy)~~
- [X] ~~Configurar gateway por defecto (192.168.145.1) y DNS en el pool~~

### 7.3 DHCP en Sede Catamarca (Único segmento)
- [X] ~~Configurar pool para Catamarca (en servidor DHCP CABA o localmente en Router Catamarca)~~
- [X] ~~Configurar gateway por defecto (192.168.145.65) y DNS en el pool~~

### 7.4 DHCP Relay (Si se centraliza el servicio en el servidor DHCP CABA)
- [X] ~~Configurar ip helper-address en subinterfaces de Router CABA (si el servidor está en VLAN Sistemas)~~
- [X] ~~Configurar ip helper-address en la interfaz LAN de Router Jujuy apuntando a la IP 172.29.0.70~~
- [X] ~~Configurar ip helper-address en la interfaz LAN de Router Catamarca apuntando a la IP 172.29.0.70~~
- [X] ~~Verificar asignación automática de IPs en todas las sedes~~

---

## FASE 8: SERVICIOS DNS

### 8.1 DNS ROOT Server (Simulado en Internet)
- [X] ~~Configurar IP: 193.0.14.129/24~~
- [X] ~~Configurar registros NS para root (.)~~
- [X] ~~Configurar registros A para root servers~~
- [X] ~~Habilitar servicio DNS~~

### 8.2 DNS .ar / .com.ar Server (Simulado en Internet)
- [X] ~~Configurar IP: 200.108.148.50/24~~
- [X] ~~Configurar registros NS para .ar~~
- [X] ~~Configurar delegación para hidronova.com.ar apuntando a los DNS de la empresa~~
- [X] ~~Habilitar servicio DNS~~

### 8.3 DNS Local Resolver Google (Simulado en Internet)
- [X] Configurar IP: 8.8.8.8/24
- [X] Configurar root hints
- [X] Habilitar servicio DNS

### 8.4 DNS Local Resolver CABA (Interno)
- [X] ~~Configurar IP: 172.29.0.66/23~~
- [X] ~~Configurar root hints para resolver dominios de Internet~~
- [X] ~~Configurar forwarders hacia el servidor DNS Primario para la zona interna~~
- [X] ~~Habilitar servicio DNS~~

### 8.5 DNS Primario CABA (Autoritativo para hidronova.com.ar)
- [X] ~~Configurar IP: 172.29.0.4/23~~
- [X] ~~Crear registros A para servidores web y de correo en CABA~~
- [X] ~~Configurar delegación para el subdominio logistica.hidronova.com.ar apuntando al DNS de Jujuy~~
- [X] ~~Habilitar servicio DNS~~

### 8.6 DNS Secundario CABA (Réplica de hidronova.com.ar)
- [X] ~~Configurar IP: 172.29.0.5/23~~
- [X] ~~Configurar transferencia de zona desde el DNS Primario CABA~~
- [X] ~~Habilitar servicio DNS~~

### 8.7 DNS Primario Logística y Transporte (Alojado en Jujuy)
- [X] ~~Configurar IP: 192.168.145.10/26 (En la sede Jujuy)~~
- [X] ~~Crear registros A para servidores locales (ej. Web Jujuy en 192.168.145.6)~~
- [X] ~~Configurar zona autoritativa para logistica.hidronova.com.ar~~
- [X] ~~Habilitar servicio DNS~~

---

## FASE 9: SERVIDORES WEB

### 9.1 Web Principal (Sede CABA)
- [ X] Configurar IP
- [ X] Habilitar servicio HTTP
- [ X] Diseñar index.html (logo, info general, links a servicios)
- [ X] Configurar registro A (www.hidronova.com.ar) en DNS Primario CABA

### 9.2 Web Logística y Transporte (Sede Jujuy - Segundo Servidor Web)
- [ X] Configurar IP (Ubicado físicamente en la sala de datos de Jujuy)
- [X ] Habilitar servicio HTTP
- [ X] Diseñar index.html (info del departamento de L y T, listado de sucursales)
- [ X] Configurar registro A (logistica.hidronova.com.ar o similar) en DNS de Jujuy

### 9.3 Web Seguro L y T (Sede CABA - Primer Servidor HTTPS)
- [X ] Configurar IP: 172.29.0.7/23
- [X ] Habilitar servicio HTTPS
- [X ] Diseñar index.html (pantalla de acceso al sistema de gestión de logística)
- [X ] Configurar registro A (secure-logistica.hidronova.com.ar) en DNS Primario

### 9.4 Web Intranet ADM (Sede CABA - Segundo Servidor HTTPS)
- [X ] Configurar IP: 172.29.0.8/23
- [ X] Habilitar servicio HTTPS
- [X ] Diseñar index.html (intranet administrativa)
- [X ] Configurar registro A (intranet.hidronova.com.ar) en DNS Primario
- [X ] Configurar firewall local para restringir acceso solo a clientes de la VLAN Administración

---

## FASE 10: SERVICIO DE CORREO

### 10.1 Servidor de Correo (Sede CABA)
- [X] ~~Configurar IP: 172.29.0.11/23~~
- [X] ~~Habilitar SMTP (puerto 25) y POP3 (puerto 110)~~
- [X] ~~Configurar dominio de correo: hidronova.com.ar~~
- [X] ~~Crear cuentas de usuario para pruebas (mínimo 3 de distintas VLANs/sedes)~~
- [X] ~~Configurar registro MX (mail.hidronova.com.ar) en DNS Primario CABA~~
- [X] ~~Configurar registro A (mail.hidronova.com.ar) en DNS Primario CABA~~

---

## FASE 11: CONFIGURACIÓN DE CLIENTES

### 11.1 PCs con IP Estática
- [ ] Configurar IP, máscara, gateway, DNS en cada PC
- [ ] Verificar conectividad

### 11.2 PCs con DHCP
- [ ] Configurar para obtener IP automáticamente
- [ ] Verificar que reciban IP del servidor DHCP
- [ ] Verificar conectividad

### 11.3 Laptops
- [ ] Configurar para DHCP
- [ ] Verificar conectividad inalámbrica

### 11.4 Access Points
- [ ] Configurar SSID
- [ ] Configurar WPA2-PSK key
- [ ] Configurar IP de gestión
- [ ] Verificar conectividad inalámbrica

### 11.5 IP Phones
- [ ] Configurar IPs
- [ ] Verificar conectividad

### 11.6 Printers
- [ ] Configurar IPs
- [ ] Verificar que sean alcanzables desde PCs

---

## FASE 12: SEGURIDAD

### 12.1 ACLs (Access Control Lists)
- [ ] Crear ACLs para restringir acceso entre VLANs
- [ ] Aplicar ACLs en interfaces de router
- [ ] Verificar que las ACLs funcionen correctamente

### 12.2 Firewall en Servidores
- [ ] Configurar reglas de firewall en servidores web
- [ ] Configurar reglas de firewall en servidor de correo
- [ ] Configurar reglas de firewall en otros servidores
- [ ] Permitir solo tráfico necesario (puertos 80, 443, 25, 110, etc.)

### 12.3 Seguridad Inalámbrica
- [X] ~~Verificar que WPA2 esté configurado en todos los APs~~

### 12.4 Seguridad de Switches
- [ ] Deshabilitar puertos no utilizados
- [ ] Configurar port security si es necesario
- [ ] Configurar storm control

---

## FASE 13: PRUEBAS DE CONECTIVIDAD

### 13.1 Pruebas de Ping
- [ ] Ping entre PCs de la misma VLAN
- [ ] Ping entre PCs de diferentes VLANs (misma sede)
- [ ] Ping entre PCs de diferentes sedes
- [ ] Ping desde PCs internas a Internet (Google)
- [ ] Ping desde PC Google a servidores internos

### 13.2 Pruebas de DNS
- [ ] nslookup www.hidronova.com.ar desde PC interna
- [ ] nslookup mail.hidronova.com.ar
- [ ] nslookup de dominios externos desde PC interna
- [ ] Verificar resolución recursiva

### 13.3 Pruebas de Web
- [ ] Acceder a http://www.hidronova.com.ar desde PC interna
- [ ] Acceder a https://www.hidronova.com.ar (si aplica)
- [ ] Acceder a web de Logística y Transporte
- [ ] Acceder a web segura
- [ ] Acceder a intranet

### 13.4 Pruebas de Correo
- [ ] Enviar correo entre cuentas del mismo dominio
- [ ] Enviar correo a cuenta externa (si es posible)
- [ ] Recibir correo desde cuenta externa

### 13.5 Pruebas de DHCP
- [ ] Verificar que PCs reciban IP automáticamente
- [ ] Verificar que reciban gateway correcto
- [ ] Verificar que reciban DNS correcto
- [ ] Verificar renew/release de IPs

### 13.6 Pruebas de NAT
- [ ] Verificar que tráfico interno se traduzca a IP pública
- [ ] Verificar conectividad a Internet
- [ ] Verificar que no se pueda acceder desde Internet a servidores internos (sin port forwarding)

### 13.7 Pruebas de Ruteo
- [ ] traceroute desde CABA a Jujuy
- [ ] traceroute desde CABA a Catamarca
- [ ] traceroute desde Jujuy a Catamarca
- [ ] traceroute desde red interna a Internet

### 13.8 Pruebas de ACLs
- [ ] Verificar que ACLs bloqueen tráfico no permitido
- [ ] Verificar que ACLs permitan tráfico autorizado

---

## FASE 14: DOCUMENTACIÓN

### 14.1 Tabla de Direccionamiento IP
- [ ] Documentar todas las subnets utilizadas
- [ ] Documentar rangos de IPs para cada VLAN
- [ ] Documentar IPs de gateways
- [ ] Documentar IPs de servidores

### 14.2 Tabla de VLANs
- [ ] Documentar ID de cada VLAN
- [ ] Documentar nombre de cada VLAN
- [ ] Documentar rango de IPs asociado
- [ ] Documentar puertos asignados

### 14.3 Tabla de Ruteo Estático
- [ ] Documentar todas las rutas estáticas configuradas
- [ ] Documentar destino, máscara, siguiente salto
- [ ] Documentar en qué router está configurada

### 14.4 Tabla de DHCP Pools
- [ ] Documentar nombre de cada pool
- [ ] Documentar rango de IPs
- [ ] Documentar gateway y DNS
- [ ] Documentar exclusiones

### 14.5 Tabla de DNS Records
- [ ] Documentar registros A creados
- [ ] Documentar registros MX
- [ ] Documentar registros NS
- [ ] Documentar registros CNAME

### 14.6 Diagrama de Topología
- [ ] Generar diagrama completo de la red
- [ ] Incluir todas las IPs y interfaces
- [ ] Incluir VLANs y trunks
- [ ] Incluir conexiones WAN

### 14.7 Informe Técnico
- [ ] Describir arquitectura de red
- [ ] Describir servicios implementados
- [ ] Describir configuración de seguridad
- [ ] Incluir capturas de pantalla de pruebas
- [ ] Documentar problemas encontrados y soluciones

---

## FASE 15: VALIDACIÓN FINAL

### 15.1 Validación de Consigna
- [ ] Verificar que se cumplan todos los requisitos de la consigna
- [ ] Verificar que todas las sedes estén implementadas
- [ ] Verificar que todos los servicios estén funcionando
- [ ] Verificar que la documentación esté completa

### 15.2 Validación de Funcionalidad
- [ ] Ejecutar todas las pruebas de conectividad
- [ ] Verificar que no haya errores en validación del proyecto
- [ ] Verificar que no haya conflictos de IP
- [ ] Verificar que no haya puertos duplicados

### 15.3 Validación de Documentación
- [ ] Revisar que todas las tablas estén completas
- [ ] Revisar que el diagrama sea claro y completo
- [ ] Revisar que el informe técnico sea coherente
- [ ] Verificar ortografía y formato

### 15.4 Preparación para Entrega
- [ ] Guardar proyecto final
- [ ] Hacer backup del .pkt
- [ ] Exportar documentación a PDF
- [ ] Verificar que todo esté listo para presentar

---

## NOTAS IMPORTANTES

### IPs Críticas a Verificar
- **Router Internet (ISP):** 193.0.14.1 (vía servidor Google), 205.32.130.2 (vía CABA)
- **Router CABA (IP Externa):** 205.32.130.1
- **DNS ROOT (Internet):** 193.0.14.129
- **DNS .ar (Internet):** 200.108.148.50
- **DNS Local Resolver Google:** 8.8.8.8
- **Google Simulator (Servidor):** 64.223.190.94
- **DNS Local Resolver CABA:** 172.29.0.66/23
- **DNS Primario CABA:** 172.29.0.4/23
- **DNS Secundario CABA:** 172.29.0.5/23
- **DNS Primario Logística y Transporte (Jujuy):** 192.168.145.10/26
- **Web Principal (CABA):** 172.29.0.3/23
- **Web Logística y Transporte (Jujuy):** 192.168.145.6/26
- **Web Seguro L y T (CABA):** 172.29.0.7/23
- **Web Intranet ADM (CABA):** 172.29.0.8/23
- **Correo Server (CABA):** 172.29.0.11/23
- **DHCP Server (CABA):** 172.29.0.70/23

### Segmentos WAN (Fibra Óptica e Internet)
- **WAN Fibra CABA-Jujuy:** 192.168.145.128/30
- **WAN Fibra CABA-Catamarca:** 192.168.145.132/30
- **WAN Fibra Jujuy-Catamarca:** 192.168.145.136/30
- **WAN Serial Internet (CABA-ISP):** 205.32.130.0/30

### Bloques de Red Principales
- **CABA:** 172.29.0.0/23 (510 hosts útiles - segmentado en VLANs 10, 20, 30, 40)
- **Jujuy:** 192.168.145.0/26 (62 hosts útiles - segmento plano único)
- **Catamarca:** 192.168.145.64/26 (62 hosts útiles - segmento plano único)

---

## ESTADO ACTUAL (A completar durante la auditoría)

### Dispositivos sin Configurar
- [ ] Listar PCs sin IP
- [ ] Listar PCs sin gateway
- [ ] Listar switches sin VLANs configuradas
- [ ] Listar routers sin rutas configuradas

### Dispositivos con Configuración Incorrecta
- [ ] Listar dispositivos con IPs fuera de rango
- [ ] Listar dispositivos con gateway incorrecto
- [ ] Listar dispositivos con DNS incorrecto

### Servicios sin Configurar
- [ ] Listar servicios faltantes
- [ ] Listar servicios mal configurados

### Conectividad Pendiente
- [ ] Listar conexiones faltantes
- [ ] Listar rutas faltantes
- [ ] Listar ACLs faltantes

---

**Última actualización:** [Fecha]
**Responsable:** [Nombre]
