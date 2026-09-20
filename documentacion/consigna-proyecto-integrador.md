# Redes de Computadoras — Proyecto Integrador

## Objetivo
La realización de un proyecto en el cual se integren todos los temas que incumben a la materia. Este trabajo será defendido y explicado individualmente en la instancia correspondiente a la evaluación de fin de curso o en la instancia de integración.

---

## Presentación del Trabajo
Este trabajo será entregado con un informe del desarrollo del mismo en el cual se detallen las tecnologías utilizadas y se justifiquen las elecciones de diseño seleccionadas.

Deberá contener los siguientes apartados:
- **Introducción / Marco teórico.**
- **Diseño de capa física** (cableado estructurado, conectividad, etc.).
- **Diseño de capa de enlace** (asignación de VLANs, 802.1q, etc.).
- **Diseño de capa de red** (despliegue IP, ruteo, NAT, etc.).
- **Descripción del servicio DHCP.**
- **Descripción de servicios de capa de aplicación** implementados.
- **Emulación** (red emulada, planteo de la red en esquema reducido pero que contenga todas las redes y servicios a implementar).
- **Conclusiones**, implementaciones pendientes, dificultades encontradas, etc.
- **Tabla de Direccionamiento Estático:** Una tabla que contenga los siguientes datos sobre los equipos configurados con IP estática:

  | FQDN | FUNCIONES | IP/MÁSCARA | [VLAN] | SEDE | PISO/ÁREA | [IP PÚBLICA NAT] |
  | --- | --- | --- | --- | --- | --- | --- |
  | | | | | | | |

- **Tabla de Direccionamiento Dinámico:** Una tabla que contenga los siguientes datos sobre los equipos configurados con IP dinámica:

  | Pool DHCP | [VLAN] | SEDE | [IP PÚBLICA NAT] |
  | --- | --- | --- | --- |
  | | | | |

### Modalidad de Entrega
El trabajo consta de la entrega de un informe y de la emulación de la red en esquema reducido pero que contenga todos los servicios a implementar utilizando el programa de emulación de redes recomendado por los docentes. La confección y entrega de cada trabajo será grupal.

La entrega grupal se realizará en el campus virtual mediante un archivo comprimido zip (`N° grupo-apellidos.zip`; ejemplo: `3-pacino-pitt-dicaprio.zip`) que contenga el informe en formato PDF y el archivo del emulador `.pkt`.

Cada integrante deberá además realizar una entrega individual en formato PDF (`nombre-apellido.pdf`; ejemplo: `leonardo-dicaprio.pdf`) de un pequeño resumen de su aporte individual al trabajo y sus propias observaciones y dificultades encontradas.

Se valorará el cumplimiento de los objetivos, la calidad del informe, la preparación y la buena presentación. La colaboración y el trabajo en equipo serán importantes en la evaluación final de la presentación, la cual se evaluará tanto de forma individual como grupal.

---

## Detalle del Trabajo a Realizar
Se deberá desarrollar el proyecto de una red de datos para una compañía hidroeléctrica **"HidroNova S.A."** que cuenta con la siguiente condición geográfica y edilicia.

### Distribución Geográfica y Edilicia de HidroNova S.A.
HidroNova S.A. posee 3 sedes: la principal situada en la Ciudad Autónoma de Buenos Aires (CABA), otra en Catamarca y la última en San Salvador de Jujuy.

#### a) Sede CABA (Ciudad Autónoma de Buenos Aires)
Es un edificio de 10 pisos, de los cuales HidroNova S.A. posee y hace uso de los pisos 1º, 2º, 7º y 10º.

- **Piso 10º (Centro de Datos y Oficinas):**
  - **Centro de Datos:** Aloja 10 racks y cuenta con capacidad para 200 servidores.
  - **Departamento de Sistemas:** 30 puestos de trabajo.
  - **Oficina del Directorio:** 10 puestos de trabajo.
  - **Departamento de Logística y Transporte:** 15 puestos de trabajo.
  - **Departamento de Ingeniería:** 5 puestos de trabajo.
  - **Departamento de Desarrollo de Producto:** 15 puestos de trabajo.
  - **Departamento de Contabilidad:** 10 puestos de trabajo.
- **Piso 7º (Gerencias y Marketing):**
  - **Gerentes:** 6 puestos de trabajo.
  - **Departamento de Marketing:** 5 puestos de trabajo.
  - **Facturación y Liquidaciones:** 12 puestos de trabajo.
  - **Departamento de RRHH:** 4 puestos de trabajo.
- **Piso 2º (Medio Ambiente y Compras):**
  - **Departamento de Medio Ambiente y Sostenibilidad:** 10 puestos de trabajo.
  - **Departamento de Compras:** 10 puestos de trabajo.
- **Piso 1º (Reuniones y Atención):**
  - **Sala de Reuniones:** 8 puestos de trabajo.
  - **SUM (Salón de Usos Múltiples):** 60 puestos de trabajo.
  - **Atención al Público:** 20 puestos de trabajo.

##### Segmentación de Red (VLANs) en CABA
Las redes se encuentran segmentadas de acuerdo a los siguientes grupos de pertenencia:
- **VLAN Administración:** Facturación y Liquidaciones, Departamento de Contabilidad, Atención al Público, Departamento de RRHH y Departamento de Compras.
- **VLAN Logística:** Departamento de Logística y Transporte, Departamento de Medio Ambiente y Sostenibilidad, Departamento de Ingeniería y Departamento de Desarrollo de Producto.
- **VLAN Gerencia:** Directorio, Gerentes, Departamento de Marketing, Sala de Reuniones y SUM.
- **VLAN Sistemas y Centro de Datos:** Tienen su VLAN propia.

> [!NOTE]
> Se desea que el vínculo vertical de datos de este edificio se encuentre galvánicamente aislado, de modo de desvincular eléctricamente los mismos y aislar cualquier problema eléctrico que haya en un sector del resto de la red. Este aislamiento se logrará mediante la implementación de enlaces de fibra óptica.

#### b) Sede San Salvador de Jujuy
El edificio de Jujuy es de propiedad íntegra de HidroNova S.A. y consta de 2 pisos. Se utilizará un **único segmento de red**.

- **Piso 1º:**
  - **Producción:** 20 puestos de trabajo.
  - **Logística y Transporte:** 5 puestos de trabajo.
  - **Departamento Comercial:** 3 puestos de trabajo.
- **Piso 2º:**
  - **Departamento de Administración:** 4 puestos de trabajo.
  - **Cuarto de Servidores y Conectividad:** Aloja 16 servidores.

#### c) Sede Catamarca
El edificio de Catamarca consta de 4 pisos, de los cuales HidroNova S.A. posee y hace uso únicamente del 2º piso. Se utilizará un **único segmento de red**.

- **Piso 2º:**
  - **Producción:** 10 puestos de trabajo.
  - **Departamento Comercial:** 3 puestos de trabajo.
  - **Departamento de Administración:** 2 puestos de trabajo.
  - **Logística y Transporte:** 5 puestos de trabajo.
  - **Cuarto de Servidores y Conectividad:** Aloja 4 servidores.

---

## Conectividad
- **Enlaces entre sedes:** Todos los edificios deberán ser vinculados entre sí por enlaces Gigabit Ethernet punto a punto por fibra óptica entre routers.
- **Conexión a Internet:** La conectividad de HidroNova S.A. con Internet se realizará a través de un enlace dedicado punto a punto serial desde el edificio de CABA hasta el router del ISP. Para su configuración IP, el proveedor proporciona el segmento de red `205.32.130.0/30`.
- **Direccionamiento Público:** El proveedor ha asignado el segmento público `200.45.110.128/25`, con el cual la empresa tendrá que implementar todos los servicios de la red que interactúan con Internet. El proceso de NAT/PAT se efectuará en la sede de CABA.
- **Direccionamiento Privado:** Las subredes internas deberán ser obtenidas para la sede de CABA a partir del bloque `172.29.0.0/23`. Para el resto de las sedes (incluyendo los enlaces punto a punto entre ellas), se obtendrán a partir del bloque `192.168.145.0/24`. Se debe respetar el segmento ya asignado a CABA para una de sus subredes.

---

## Servicios y Equipamiento
El nombre de dominio de HidroNova S.A. será `hidronova.com.ar`, administrado por el Departamento de Sistemas en el DNS primario de HidroNova. Además se delegará la administración del subdominio `logistica.hidronova.com.ar` al Departamento de Logística y Transporte que administrará su propio servidor DNS primario, y lo tendrá alojado en la sala de datos de Jujuy.

Los servidores DNS primarios y secundarios deberán ser completamente configurados en el emulador (registros SOA, A, NS, varios registros CNAME, etc.).

Todos los dispositivos (PCs, laptops, smartphones, etc.), excepto aquellos equipos que proveen servicios o por algún motivo requieran IP estática, obtendrán sus configuraciones de red utilizando el protocolo DHCP.

HidroNova contará con los siguientes servicios. Salvo indicación en contrario, los servidores respectivos serán alojados en la sede CABA:

### I. Servidores Web y HTTPS
Se deben diseñar las páginas de inicio (HTML) acordes con la función de cada servidor.
1. **Servidor Web Principal (HTTP):** Contendrá como mínimo un logo (imagen), información general sobre HidroNova S.A., un enlace al listado de servicios brindados utilizando listas y tablas (al estilo del problema 1 de la práctica World Wide Web) y un enlace al servidor del Departamento de "Logística y Transporte".
2. **Servidor Web de Logística (HTTP):** Instalado en la Sede Jujuy. Brindará información sobre el departamento de "Logística y Transporte" y contendrá como mínimo un logo, información general y un enlace a un listado de sucursales.
3. **Servidor Web Seguro Logística (HTTPS):** Dedicado al Departamento de "Logística y Transporte". Contendrá como mínimo la pantalla de acceso al sistema de Gestión Logística.
4. **Servidor Web Seguro Intranet (HTTPS):** Contendrá la Intranet del sistema administrativo. Este servidor deberá ser accedido solamente por los clientes del Departamento Administrativo; para esto se deberá configurar adecuadamente el firewall local del servidor.

### II. Servicio de Correo Electrónico
- Todas las direcciones de correo electrónico serán de la forma `usuario@hidronova.com.ar`.
- En el emulador se deberá configurar el servidor de correo con al menos 3 usuarios de distintas redes virtuales y sedes con sus respectivos clientes.

### III. Puntos de Acceso Wireless
- Todos los edificios contarán en cada uno de sus pisos con puntos de acceso wireless con los que se ofrecerán servicio a laptops, tablets, smartphones, etc.
- Su identificación en la red (SSID) será `"HN-2026"`.

### IV. Impresoras y Telefonía IP
- Cada piso tendrá al menos una impresora de red accesible y utilizable por todos los usuarios de ese piso. Algunas serán wireless y otras conectadas por cable.
- Todas las oficinas contarán con al menos un teléfono IP conectado a la red y a una PC.

> [!TIP]
> Se deberá tener en cuenta la distribución de los distintos servicios en los equipos físicos prestando atención a la distribución de la carga, la seguridad y fiabilidad de la red.

---

## Ruteo IP
- **Ruteo Principal:** Todos los equipos deberán utilizar rutas estáticas.
- **Desafío Adicional:** En caso de querer utilizar protocolos de ruteo dinámico (RIP, OSPF, etc.) a modo de desafío personal, se deberá entregar una segunda versión del trabajo con esta implementación.
