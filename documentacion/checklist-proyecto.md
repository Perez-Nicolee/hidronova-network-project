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
  - [X] Access Points inalámbricos (configurados con SSID y WPA2)
  - [X] IP Phones (configurados)
  - [X] Printers (configurados)

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
- [X] Access Points inalámbricos
- [X] ~~IP Phones~~
- [X] Printers
- [X] ~~Conexión WAN a CABA (Fibra óptica Gigabit)~~

### 1.4 Segmento Público / Internet
- [X] Router Internet (ISP)
- [X] Interfaz serial hacia CABA (205.32.130.0/30)
- [X] Servidor que simula Google (IP: 64.223.190.94)
- [X] Switch Google
- [X] DNS Local Resolver Google (8.8.8.8)
- [X] PC Google (para pruebas)

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
- [X] WAN Serial CABA-Internet: 205.32.130.0/30

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
- [X] Verificar que las VLANs pasen por los trunks

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
- [X] Configurar interfaz serial hacia CABA (205.32.130.2/30)
- [X] Configurar interfaz hacia servidor Google (64.223.190.1/24)

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
- [X] Ruta hacia red pública de HidroNova (200.45.110.128/25) vía 205.32.130.1 (IP externa de CABA)

---

## FASE 6: NAT (Network Address Translation)

### 6.1 Configuración NAT en Router CABA
- [X] ~~Configurar interfaz inside (subinterfaces de VLANs y puertos hacia sedes remotas)~~
- [X] ~~Configurar interfaz outside (puerto serial hacia Internet)~~
- [X] ~~Crear ACL para redes internas permitidas (172.29.0.0/23 y 192.168.145.0/24)~~
- [X] ~~Configurar NAT overload (PAT) asociando la ACL con la IP pública del puerto serial~~
- [X] ~~Configurar NAT estático para el Servidor Web Principal (IP interna -> IP pública del bloque asignado)~~
- [X] ~~Configurar NAT estático para el Servidor de Correo (IP interna -> IP pública)~~
- [X] Verificar traducción NAT desde redes internas a Internet

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
- [X] Configurar IP
- [X] Habilitar servicio HTTP
- [X] Diseñar index.html (logo, info general, links a servicios)
- [X] Configurar registro A (www.hidronova.com.ar) en DNS Primario CABA

### 9.2 Web Logística y Transporte (Sede Jujuy - Segundo Servidor Web)
- [X] Configurar IP (Ubicado físicamente en la sala de datos de Jujuy)
- [X] Habilitar servicio HTTP
- [X] Diseñar index.html (info del departamento de L y T, listado de sucursales)
- [X] Configurar registro A (logistica.hidronova.com.ar o similar) en DNS de Jujuy

### 9.3 Web Seguro L y T (Sede CABA - Primer Servidor HTTPS)
- [X] Configurar IP: 172.29.0.7/23
- [X] Habilitar servicio HTTPS
- [X] Diseñar index.html (pantalla de acceso al sistema de gestión de logística)
- [X] Configurar registro A (secure-logistica.hidronova.com.ar) en DNS Primario

### 9.4 Web Intranet ADM (Sede CABA - Segundo Servidor HTTPS)
- [X] Configurar IP: 172.29.0.8/23
- [X] Habilitar servicio HTTPS
- [X] Diseñar index.html (intranet administrativa)
- [X] Configurar registro A (intranet.hidronova.com.ar) en DNS Primario
- [X] Configurar firewall local para restringir acceso solo a clientes de la VLAN Administración

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
- [X] Configurar IP, máscara, gateway, DNS en cada PC
- [X] Verificar conectividad

### 11.2 PCs con DHCP
- [X] Configurar para obtener IP automáticamente
- [X] Verificar que reciban IP del servidor DHCP
- [X] Verificar conectividad

### 11.3 Laptops
- [X] Configurar para DHCP
- [X] Verificar conectividad inalámbrica

### 11.4 Access Points
- [X] Configurar SSID
- [X] Configurar WPA2-PSK key
- [X] Configurar IP de gestión
- [X] Verificar conectividad inalámbrica

### 11.5 IP Phones
- [X] Configurar IPs
- [X] Verificar conectividad

### 11.6 Printers
- [X] Configurar IPs
- [X] Verificar que sean alcanzables desde PCs

---

## FASE 12: SEGURIDAD

### 12.1 ACLs (Access Control Lists)
- [X] Crear ACLs para restringir acceso entre VLANs
- [X] Aplicar ACLs en interfaces de router
- [X] Verificar que las ACLs funcionen correctamente

### 12.2 Firewall en Servidores
- [X] Configurar reglas de firewall en servidores web
- [X] Configurar reglas de firewall en servidor de correo
- [X] Configurar reglas de firewall en otros servidores
- [X] Permitir solo tráfico necesario (puertos 80, 443, 25, 110, etc.)

### 12.3 Seguridad Inalámbrica
- [X] ~~Verificar que WPA2 esté configurado en todos los APs~~

### 12.4 Seguridad de Switches
- [X] Deshabilitar puertos no utilizados
- [X] Configurar port security si es necesario
- [X] Configurar storm control

---

## FASE 13: PRUEBAS DE CONECTIVIDAD

### 13.1 Pruebas de Ping
- [X] Ping entre PCs de la misma VLAN
- [X] Ping entre PCs de diferentes VLANs (misma sede)
- [X] Ping entre PCs de diferentes sedes
- [X] Ping desde PCs internas a Internet (Google)
- [X] Ping desde PC Google a servidores internos

### 13.2 Pruebas de DNS
- [X] nslookup www.hidronova.com.ar desde PC interna
- [X] nslookup mail.hidronova.com.ar
- [X] nslookup de dominios externos desde PC interna
- [X] Verificar resolución recursiva

### 13.3 Pruebas de Web
- [X] Acceder a http://www.hidronova.com.ar desde PC interna
- [X] Acceder a https://www.hidronova.com.ar (si aplica)
- [X] Acceder a web de Logística y Transporte
- [X] Acceder a web segura
- [X] Acceder a intranet

### 13.4 Pruebas de Correo
- [X] Enviar correo entre cuentas del mismo dominio
- [X] Enviar correo a cuenta externa (si es posible)
- [X] Recibir correo desde cuenta externa

### 13.5 Pruebas de DHCP
- [X] Verificar que PCs reciban IP automáticamente
- [X] Verificar que reciban gateway correcto
- [X] Verificar que reciban DNS correcto
- [X] Verificar renew/release de IPs

### 13.6 Pruebas de NAT
- [X] Verificar que tráfico interno se traduzca a IP pública
- [X] Verificar conectividad a Internet
- [X] Verificar que no se pueda acceder desde Internet a servidores internos (sin port forwarding)

### 13.7 Pruebas de Ruteo
- [X] traceroute desde CABA a Jujuy
- [X] traceroute desde CABA a Catamarca
- [X] traceroute desde Jujuy a Catamarca
- [X] traceroute desde red interna a Internet

### 13.8 Pruebas de ACLs
- [X] Verificar que ACLs bloqueen tráfico no permitido
- [X] Verificar que ACLs permitan tráfico autorizado

---

## FASE 14: DOCUMENTACIÓN

### 14.1 Tabla de Direccionamiento IP
- [X] Documentar todas las subnets utilizadas
- [X] Documentar rangos de IPs para cada VLAN
- [X] Documentar IPs de gateways
- [X] Documentar IPs de servidores

### 14.2 Tabla de VLANs
- [X] Documentar ID de cada VLAN
- [X] Documentar nombre de cada VLAN
- [X] Documentar rango de IPs asociado
- [X] Documentar puertos asignados

### 14.3 Tabla de Ruteo Estático
- [X] Documentar todas las rutas estáticas configuradas
- [X] Documentar destino, máscara, siguiente salto
- [X] Documentar en qué router está configurada

### 14.4 Tabla de DHCP Pools
- [X] Documentar nombre de cada pool
- [X] Documentar rango de IPs
- [X] Documentar gateway y DNS
- [X] Documentar exclusiones

### 14.5 Tabla de DNS Records
- [X] Documentar registros A creados
- [X] Documentar registros MX
- [X] Documentar registros NS
- [X] Documentar registros CNAME


### 14.7 Informe Técnico
- [X] Describir arquitectura de red
- [X] Describir servicios implementados
- [X] Describir configuración de seguridad
- [X] Incluir capturas de pantalla de pruebas
- [X] Documentar problemas encontrados y soluciones

---

## FASE 15: VALIDACIÓN FINAL

### 15.1 Validación de Consigna
- [X] Verificar que se cumplan todos los requisitos de la consigna
- [X] Verificar que todas las sedes estén implementadas
- [X] Verificar que todos los servicios estén funcionando
- [X] Verificar que la documentación esté completa

### 15.2 Validación de Funcionalidad
- [X] Ejecutar todas las pruebas de conectividad
- [X] Verificar que no haya errores en validación del proyecto
- [X] Verificar que no haya conflictos de IP
- [X] Verificar que no haya puertos duplicados

### 15.3 Validación de Documentación
- [X] Revisar que todas las tablas estén completas
- [X] Revisar que el informe técnico sea coherente
- [X] Verificar ortografía y formato

### 15.4 Preparación para Entrega
- [X] Guardar proyecto final
- [X] Hacer backup del .pkt
- [X] Exportar documentación a PDF
- [X] Verificar que todo esté listo para presentar

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
