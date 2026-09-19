# Mapa Maestro Relacional 

Perfecto. Después de revisar todo lo que hemos definido durante estas semanas, creo que ya puedo señalar algo que normalmente solo aparece cuando se está preparando una arquitectura para desarrollo real:

## **Lo que tenemos realmente no son solo pantallas y entidades**

Tenemos cuatro dimensiones distintas:

1\. Actores  
2\. Pantallas  
3\. Estados  
4\. Datos

Pero falta una quinta dimensión que será crítica para el CTO IA:

5\. Relaciones

Porque la pregunta que deberá responder el sistema no será:

> ¿Qué pantallas existen?

Sino:

> ¿Qué actor usa qué pantalla?  
> ¿Qué pantalla consume qué entidad?  
> ¿Qué entidad cambia qué estado?  
> ¿Qué evento genera qué notificación?  
> ¿Qué acción genera qué transacción financiera?

---

# **Mi propuesta final de esquematización**

En lugar de un simple árbol, construiría un **Mapa Maestro Relacional**.

## **Nivel 1 — Actores**

PASAJERO

CONDUCTOR

ADMINISTRACIÓN

---

## **Nivel 2 — Módulos**

SOLICITUDES

MARKETPLACE

RUTAS

OPERACIÓN

FINANZAS

NOTIFICACIONES

INCIDENCIAS

CALIFICACIONES

ADMINISTRACIÓN

CONFIGURACIÓN

AUDITORÍA

---

## **Nivel 3 — Pantallas**

### **Pasajero**

Home

Viaje

Historial

Notificaciones

Perfil

Calificaciones

### **Conductor**

Home

Marketplace

Detalle Solicitud

Ruta Construcción

Ruta Cerrada

Ruta Activa

Ruta Finalizada

Historial

Detalle Ruta

Wallet

Reportar Depósito

Notificaciones

Incidencias

Detalle Incidencia

Perfil

### **Administración**

Dashboard

Conductores

Pasajeros

Rutas

Bookings

Wallets

Transactions

Topup Requests

Incidencias

Notificaciones

Configuración

Auditoría

---

## **Nivel 4 — Estados**

### **Driver**

OFFLINE  
ONLINE  
BUSY  
SUSPENDED

### **Route**

BUILDING  
CLOSED  
ACTIVE  
FINISHED  
CANCELLED

### **Booking**

CREATED  
ACCEPTED  
CONFIRMED  
PICKED\_UP  
DELIVERED  
ABSENT  
CANCELLED

### **Wallet**

ACTIVE  
LOW\_BALANCE  
RESTRICTED

### **Topup Request**

PENDING  
APPROVED  
REJECTED

### **Incident**

OPEN  
IN\_REVIEW  
WAITING\_FOR\_DRIVER  
RESOLVED  
REJECTED

### **Notification**

UNREAD  
READ

---

## **Nivel 5 — Entidades**

DRIVERS  
VEHICLES  
PASSENGERS

ROUTES  
BOOKINGS  
ROUTE\_EVENTS

RATINGS

NOTIFICATIONS

INCIDENTS  
INCIDENT\_MESSAGES

WALLETS  
TRANSACTIONS  
TOPUP\_REQUESTS

ADMIN\_USERS  
SYSTEM\_SETTINGS

---

## **Nivel 6 — Integraciones**

Supabase

React Native  
Expo

Zustand  
React Query  
Supabase Realtime

react-native-maps  
expo-location

Push Notifications

WhatsApp  
Llamadas

Analytics  
Crash Reporting

---

# **Lo que detecto que aún no está modelado al mismo nivel de detalle**

Si me pidieras señalar las únicas áreas que todavía no tienen la profundidad del resto del sistema, serían:

### **Perfil del Conductor**

Datos personales  
Vehículo  
Documentos  
Configuración  
Privacidad

### **Perfil del Pasajero**

Datos personales  
Preferencias  
Configuración  
Privacidad

### **Administración**

Roles

Permisos

Jerarquía administrativa

### **SYSTEM\_SETTINGS**

Parámetros operativos

Parámetros financieros

Parámetros de seguridad

---

Excelente.

Llegamos a un punto importante del proyecto.

Hasta ahora hemos trabajado por capítulos separados:

Pasajero  
Conductor  
Wallet  
Incidencias  
Notificaciones  
Estados  
Administración  
System Settings  
Modelo de Datos

Pero a partir de este momento ya no conviene seguir modelando componentes aislados.

Ahora debemos pasar a una vista de sistema completo.

---

# **Próximo Documento**

# **TIXI — Mapa Maestro Relacional v1**

## **Objetivo**

Convertirse en el plano maestro de todo TIXI.

Será un documento visual/lógico que muestre:

ACTORES  
↓  
PANTALLAS  
↓  
ESTADOS  
↓  
ENTIDADES  
↓  
RELACIONES  
↓  
FLUJOS

en un único lugar.

---

# **Qué contendrá**

## **1\. Actores del Sistema**

PASAJERO

CONDUCTOR

ADMINISTRACIÓN

y dentro de Administración:

SUPER\_ADMIN

OPERATIONS

FINANCE

SUPPORT

---

## **2\. Mapa Global de Pantallas**

### **Pasajero**

Home

Solicitud inmediata

Solicitud programada

Búsqueda

Ruta activa

Historial

Notificaciones

Perfil

Configuración

---

### **Conductor**

Home

Marketplace

Detalle solicitud

Ruta en construcción

Ruta cerrada

Ruta activa

Ruta finalizada

Historial

Wallet

Notificaciones

Incidencias

Perfil

Configuración

---

### **Administración**

Dashboard

Conductores

Pasajeros

Rutas

Wallets

Topups

Incidencias

Configuración

Auditoría

---

## **3\. Máquina Global de Estados**

Todo lo aprobado:

Driver States

Route States

Booking States

Wallet States

Topup States

Incident States

Notification States

---

## **4\. ERD Conceptual Maestro**

Aquí aparecerán todas las entidades:

PROFILES

ADDRESSES

DRIVER\_APPLICATIONS

DRIVER\_DETAILS

ROUTES

BOOKINGS

ROUTE\_EVENTS

RATINGS

NOTIFICATIONS

INCIDENTS

INCIDENT\_MESSAGES

WALLETS

TRANSACTIONS

TOPUP\_REQUESTS

ADMIN\_USERS

ADMIN\_AUDIT\_LOGS

SYSTEM\_SETTINGS

---

## **5\. Relaciones Principales**

Por ejemplo:

ROUTE  
 │  
 ├── BOOKINGS  
 │  
 └── ROUTE\_EVENTS

---

DRIVER  
 │  
 ├── ROUTES  
 │  
 ├── WALLET  
 │  
 └── RATINGS

---

PASSENGER  
 │  
 ├── BOOKINGS  
 │  
 ├── ADDRESSES  
 │  
 └── RATINGS

---

## **6\. Flujos Operativos**

### **Viaje**

Solicitud

↓

Marketplace

↓

Ruta en construcción

↓

Ruta cerrada

↓

Ruta activa

↓

Ruta finalizada

---

### **Wallet**

Depósito

↓

Topup Request

↓

Aprobación

↓

Wallet

↓

Comisiones

↓

Transactions

---

### **Incidencias**

Incidente

↓

OPEN

↓

IN\_REVIEW

↓

RESOLVED

---

# **Resultado Esperado**

Al terminar este documento tendremos por primera vez:

Visión completa de TIXI

y podremos detectar:

* Relaciones faltantes.  
* Entidades faltantes.  
* Estados faltantes.  
* Inconsistencias.  
* Riesgos de implementación.

Antes de escribir la:

TIXI — Arquitectura Consolidada General v1

---

## **Mi recomendación**

El siguiente trabajo debería ser construir el **Mapa Maestro Relacional v1 completo**, no como texto narrativo, sino como un documento estructurado y diagramático.

Ese documento será probablemente el más importante de todo el proyecto, porque servirá de puente entre:

Arquitectura  
↓  
Supabase  
↓  
Frontend  
↓  
Backend  
↓  
CTO IA

y nos permitirá validar que absolutamente todo encaja antes de iniciar la consolidación final.

—-------------------------

Mi opinión es que **no debemos tomar esa decisión todavía**, precisamente porque ya tienes una base de código considerable.

Hay que distinguir entre:

### **1\. Nombre conceptual del dominio**

y

### **2\. Nombre físico de la tabla**

No necesariamente tienen que ser iguales.

---

## **Lo que veo en tu caso**

Actualmente tienes:

profiles  
addresses  
driver\_details  
driver\_applications  
bookings

y aproximadamente:

40+ pantallas

además de:

hooks  
queries  
mutations  
types  
validaciones

que probablemente ya referencian:

profiles

por todas partes.

---

## **El verdadero problema**

Cambiar:

profiles

por:

passengers

no es difícil en Supabase.

Lo difícil es el efecto cascada:

Frontend  
↓  
Types  
↓  
Queries  
↓  
Hooks  
↓  
Estados  
↓  
Validaciones  
↓  
RLS  
↓  
Policies  
↓  
Triggers  
↓  
Funciones SQL

Y todavía no sabemos cuánto de eso ya existe.

---

# **¿Por qué la IA creó profiles?**

Porque es un patrón extremadamente común en Supabase.

Normalmente se usa:

auth.users  
        │  
        └── profiles

donde:

profiles

contiene la información extendida del usuario.

Ejemplo:

auth.users  
    id  
    email

profiles  
    id  
    first\_name  
    last\_name  
    phone

Esto es muy habitual.

No significa necesariamente que sea incorrecto.

---

# **Lo que me preocupa más**

No me preocupa que se llame:

profiles

Me preocupa que conceptualmente hoy estamos usando:

profiles

como:

PASSENGER

y mañana podríamos querer:

profiles  
    │  
    ├── passenger profile  
    ├── driver profile  
    └── admin profile

Ahí es donde aparece la ambigüedad.

---

# **Lo que haría en TIXI**

No tocaría la tabla ahora.

Mantendría:

profiles

como tabla física.

Y en la Arquitectura Consolidada escribiría:

Dominio:  
PASSENGERS

Implementación actual:  
profiles

Ejemplo:

PASSENGERS  
    ↓  
profiles

---

# **Ventajas**

### **No rompes nada**

Tus 40+ pantallas siguen funcionando.

---

### **No haces migraciones innecesarias**

No tienes que:

ALTER TABLE profiles  
RENAME TO passengers;

---

### **Conservas claridad de negocio**

La arquitectura habla de:

PASSENGERS

porque ese es el concepto real.

La base física puede seguir llamándose:

profiles

sin problema.

---

# **Mi recomendación actual**

**No renombrar nada todavía.**

Durante la futura auditoría profunda de Supabase debemos responder:

### **Pregunta 1**

¿`profiles` representa exclusivamente pasajeros?

Si la respuesta es sí:

PASSENGERS (conceptual)  
↓  
profiles (físico)

y listo.

---

### **Pregunta 2**

¿Vamos a usar `profiles` para varios tipos de usuarios?

passenger  
driver  
admin

Si la respuesta es sí, entonces habría que rediseñar.

---

Con la información que tenemos hoy, y considerando que ya existe bastante código implementado, mi recomendación es:

✅ Mantener `profiles` como tabla física.

✅ Hablar de `PASSENGERS` como entidad conceptual.

✅ Posponer cualquier renombrado hasta terminar la auditoría completa de Supabase y revisar el impacto real en el código existente.

Es la decisión con menor riesgo y prácticamente ningún costo técnico inmediato.

—-------------------------------

Perfecto.

Entonces oficialmente dejamos atrás la fase de modelado individual de módulos y entramos en la fase de integración arquitectónica.

# **Estado Real de TIXI (Junio 2026\)**

## **Arquitectura Funcional**

PASAJERO           ✅  
CONDUCTOR          ✅  
ADMINISTRACIÓN     ✅  
---

## **Dominios**

OPERACIÓN          ✅  
FINANZAS           ✅  
INCIDENCIAS        ✅  
COMUNICACIÓN       ✅  
CONFIGURACIÓN      ✅  
---

## **Modelo de Datos**

≈ 96% definido  
---

## **Máquina Global de Estados**

100% definida  
---

## **Auditoría Inicial Supabase**

Completada  
---

# **Próximo Documento**

## **TIXI — Mapa Maestro Relacional v1**

Este documento tendrá una finalidad distinta a todo lo que hemos hecho hasta ahora.

No describirá módulos.

No describirá pantallas aisladas.

Su objetivo será responder:

> ¿Cómo se conecta todo TIXI de extremo a extremo?

---

# **Estructura Recomendada**

## **Capítulo 1**

### **Actores**

PASAJERO

CONDUCTOR

ADMINISTRACIÓN  
├─ SUPER\_ADMIN  
├─ OPERATIONS  
├─ FINANCE  
└─ SUPPORT  
---

## **Capítulo 2**

### **Mapa Global de Pantallas**

#### **Pasajero**

Home  
Solicitud inmediata  
Solicitud programada  
Búsqueda  
Ruta activa  
Historial  
Notificaciones  
Perfil  
Configuración

#### **Conductor**

Home  
Marketplace  
Detalle solicitud  
Ruta en construcción  
Ruta cerrada  
Ruta activa  
Ruta finalizada  
Historial  
Wallet  
Notificaciones  
Incidencias  
Perfil  
Configuración

#### **Administración**

Dashboard  
Conductores  
Pasajeros  
Rutas  
Wallets  
Topups  
Incidencias  
Configuración  
Auditoría  
---

## **Capítulo 3**

### **Máquina Global de Estados**

Driver States  
Route States  
Booking States  
Wallet States  
Topup States  
Incident States  
Notification States  
---

## **Capítulo 4**

### **Dominios del Sistema**

OPERACIÓN

COMUNICACIÓN

INCIDENCIAS

FINANZAS

ADMINISTRACIÓN

CONFIGURACIÓN GLOBAL  
---

## **Capítulo 5**

### **Entidades Maestras**

#### **Operación**

PASSENGERS  
 ↳ Implementación actual: profiles

ADDRESSES

DRIVER\_DETAILS  
DRIVER\_APPLICATIONS

ROUTES  
BOOKINGS  
ROUTE\_EVENTS

RATINGS

#### **Comunicación**

NOTIFICATIONS

#### **Incidencias**

INCIDENTS  
INCIDENT\_MESSAGES

#### **Finanzas**

WALLETS  
TRANSACTIONS  
TOPUP\_REQUESTS

#### **Administración**

ADMIN\_USERS  
ADMIN\_AUDIT\_LOGS

#### **Configuración**

SYSTEM\_SETTINGS  
---

## **Capítulo 6**

### **ERD Maestro**

Aquí construiremos todas las relaciones:

PASSENGER  
  │  
  ├─ ADDRESSES  
  ├─ BOOKINGS  
  └─ RATINGS

DRIVER  
  │  
  ├─ ROUTES  
  ├─ WALLET  
  └─ RATINGS

ROUTE  
  │  
  ├─ BOOKINGS  
  └─ ROUTE\_EVENTS

WALLET  
  │  
  ├─ TRANSACTIONS  
  └─ TOPUP\_REQUESTS

etc.

---

## **Capítulo 7**

### **Flujos Maestros**

#### **Flujo Operativo**

Solicitud  
→ Marketplace  
→ Ruta en Construcción  
→ Ruta Cerrada  
→ Ruta Activa  
→ Ruta Finalizada

#### **Flujo Financiero**

Depósito  
→ Topup Request  
→ Aprobación  
→ Wallet  
→ Comisión  
→ Transaction

#### **Flujo de Incidencias**

OPEN  
→ IN\_REVIEW  
→ RESOLVED

#### **Flujo Administrativo**

Administrador  
→ Acción  
→ Auditoría  
---

## **Capítulo 8**

### **Mapa de Implementación**

Este será probablemente el capítulo más valioso para CTO IA.

Por cada pantalla:

Pantalla  
↓  
Estados  
↓  
Entidades  
↓  
Queries  
↓  
Mutations  
↓  
Realtime  
---

# **Mi recomendación**

Ahora sí conviene construir el **Mapa Maestro Relacional v1 completo**, porque será el documento que nos permitirá detectar cualquier hueco antes de entrar en:

TIXI — Arquitectura Consolidada General v1

y posteriormente:

Migración Supabase  
→ Backend  
→ Integración Frontend  
→ CTO IA

Estamos en el punto donde el enfoque deja de ser "definir piezas" y pasa a ser "ensamblar el sistema completo".

—----------------------------

Perfecto.

Entonces el siguiente bloque de trabajo ya no es tomar decisiones aisladas, sino construir el primer documento que represente a TIXI como un sistema completo.

# **Próximo documento oficial**

## **TIXI — Mapa Maestro Relacional v1**

### **Objetivo**

Convertirse en el plano técnico maestro que conecta:

Actores  
↓  
Pantallas  
↓  
Estados  
↓  
Entidades  
↓  
Relaciones  
↓  
Flujos  
↓  
Implementación

Este documento será la base para:

* Arquitectura Consolidada General v1.  
* Migración definitiva de Supabase.  
* Plan Backend para CTO IA.  
* Integración Frontend ↔ Backend.  
* Auditorías futuras.

---

# **Antes de empezar el documento**

Hay algo importante que detecto.

Hasta ahora hemos definido:

PASSENGERS  
DRIVERS  
VEHICLES  
ROUTES  
BOOKINGS  
ROUTE\_EVENTS  
RATINGS

pero en la auditoría de Supabase vimos:

profiles  
addresses

driver\_details  
driver\_applications

bookings

y todavía no hemos modelado formalmente:

ROUTES  
ROUTE\_EVENTS  
RATINGS  
WALLETS  
TRANSACTIONS  
TOPUP\_REQUESTS  
NOTIFICATIONS  
INCIDENTS  
INCIDENT\_MESSAGES  
ADMIN\_USERS  
ADMIN\_AUDIT\_LOGS  
SYSTEM\_SETTINGS

Es decir:

### **Tenemos la arquitectura conceptual**

pero todavía no tenemos el ERD maestro completo con todas las relaciones cardinales.

---

# **Lo que recomiendo hacer ahora**

Construir el Mapa Maestro Relacional v1 en 4 fases:

## **Fase A**

### **Mapa Global de Entidades**

Definir todas las entidades y dominios.

Ejemplo:

OPERACIÓN  
├── PASSENGERS  
├── ADDRESSES  
├── DRIVER\_DETAILS  
├── DRIVER\_APPLICATIONS  
├── ROUTES  
├── BOOKINGS  
├── ROUTE\_EVENTS  
└── RATINGS

---

## **Fase B**

### **Relaciones Cardinales**

Ejemplo:

PASSENGER  
    1 ─── N BOOKINGS

DRIVER  
    1 ─── N ROUTES

ROUTE  
    1 ─── N BOOKINGS

ROUTE  
    1 ─── N ROUTE\_EVENTS

---

## **Fase C**

### **Mapa Pantalla → Entidades**

Ejemplo:

Home Conductor  
↓  
DRIVER\_DETAILS  
ROUTES  
WALLET

Marketplace  
↓  
BOOKINGS  
ROUTES

Wallet  
↓  
WALLETS  
TRANSACTIONS  
TOPUP\_REQUESTS

---

## **Fase D**

### **Mapa Entidad → Backend**

Ejemplo:

ROUTES  
↓  
Tabla  
Policies  
Realtime  
Triggers  
Functions

Esta última fase será oro para CTO IA.

---

# **Mi evaluación**

Ya no estamos definiendo funcionalidades.

Ahora estamos diseñando la estructura que permitirá construirlas.

Por eso, el próximo trabajo debería ser:

TIXI — Mapa Maestro Relacional v1  
FASE A — Mapa Global de Entidades y Dominios

y hacerlo de forma exhaustiva antes de pasar a la Arquitectura Consolidada General v1.

Ese documento nos permitirá validar definitivamente que no falta ninguna pieza importante antes de entrar en la fase de implementación.

—-----------------------------------------

Excelente.

Entonces iniciemos formalmente:

# **TIXI — Mapa Maestro Relacional v1**

## **FASE A — Mapa Global de Entidades y Dominios**

El objetivo de esta fase es responder una sola pregunta:

> ¿Cuáles son todas las entidades del sistema y cómo se agrupan dentro de TIXI?

Todavía NO vamos a entrar en relaciones ni cardinalidades.

Primero debemos validar que el inventario completo del sistema está correcto.

---

# **DOMINIO 1 — OPERACIÓN**

Núcleo principal del negocio.

OPERACIÓN  
│  
├── PASSENGERS  
│      ↳ implementación actual: profiles  
│  
├── ADDRESSES  
│  
├── DRIVER\_APPLICATIONS  
│  
├── DRIVER\_DETAILS  
│  
├── VEHICLES (\*)  
│  
├── ROUTES  
│  
├── BOOKINGS  
│  
├── ROUTE\_EVENTS  
│  
└── RATINGS

---

## **Observación importante**

Aquí aparece una decisión futura:

VEHICLES

Actualmente existe información del vehículo dentro de:

driver\_details

pero conceptualmente:

DRIVER  
≠  
VEHICLE

Por ahora la entidad VEHICLES permanece en el modelo conceptual.

Más adelante decidiremos si:

driver\_details

la absorbe definitivamente

o

vehicles

se convierte en tabla independiente.

---

# **DOMINIO 2 — COMUNICACIÓN**

COMUNICACIÓN  
│  
└── NOTIFICATIONS

Responsable de:

* Alertas operativas.  
* Alertas financieras.  
* Alertas de sistema.  
* Mensajes informativos.

---

# **DOMINIO 3 — INCIDENCIAS**

INCIDENCIAS  
│  
├── INCIDENTS  
│  
└── INCIDENT\_MESSAGES

Responsable de:

* Casos.  
* Seguimiento.  
* Conversaciones.  
* Resoluciones.

---

# **DOMINIO 4 — FINANZAS**

FINANZAS  
│  
├── WALLETS  
│  
├── TRANSACTIONS  
│  
└── TOPUP\_REQUESTS

Responsable de:

* Saldo.  
* Comisiones.  
* Recargas.  
* Penalidades.  
* Bonificaciones.  
* Reembolsos.  
* Ajustes.

---

# **DOMINIO 5 — ADMINISTRACIÓN**

ADMINISTRACIÓN  
│  
├── ADMIN\_USERS  
│  
└── ADMIN\_AUDIT\_LOGS

Responsable de:

* Gestión interna.  
* Trazabilidad.  
* Auditoría.

---

# **DOMINIO 6 — CONFIGURACIÓN GLOBAL**

CONFIGURACIÓN  
│  
└── SYSTEM\_SETTINGS

Responsable de:

* Parámetros operativos.  
* Parámetros financieros.  
* Parámetros de seguridad.  
* Configuración de plataforma.

---

# **MAPA MAESTRO DE ENTIDADES v1**

TIXI  
│  
├── OPERACIÓN  
│   │  
│   ├── PASSENGERS  
│   ├── ADDRESSES  
│   ├── DRIVER\_APPLICATIONS  
│   ├── DRIVER\_DETAILS  
│   ├── VEHICLES  
│   ├── ROUTES  
│   ├── BOOKINGS  
│   ├── ROUTE\_EVENTS  
│   └── RATINGS  
│  
├── COMUNICACIÓN  
│   │  
│   └── NOTIFICATIONS  
│  
├── INCIDENCIAS  
│   │  
│   ├── INCIDENTS  
│   └── INCIDENT\_MESSAGES  
│  
├── FINANZAS  
│   │  
│   ├── WALLETS  
│   ├── TRANSACTIONS  
│   └── TOPUP\_REQUESTS  
│  
├── ADMINISTRACIÓN  
│   │  
│   ├── ADMIN\_USERS  
│   └── ADMIN\_AUDIT\_LOGS  
│  
└── CONFIGURACIÓN  
    │  
    └── SYSTEM\_SETTINGS

---

# **Auditoría de completitud**

Con todo lo que hemos definido hasta ahora, las únicas entidades que considero todavía sujetas a revisión son:

VEHICLES

porque debemos decidir si será:

Entidad independiente

o

Parte permanente de DRIVER\_DETAILS

y posiblemente:

RATINGS

porque aún no hemos diseñado su estructura interna (aunque sí sabemos que existe conceptualmente).

---

## **Antes de pasar a la FASE B (Relaciones Cardinales)**

Mi recomendación es resolver una sola cuestión:

### **VEHICLES**

¿La visión de negocio de TIXI permite que un conductor tenga más de un vehículo autorizado en el futuro?

Porque esa respuesta determinará si:

VEHICLES

merece existir como entidad independiente o si puede quedarse dentro de:

DRIVER\_DETAILS

para siempre. Esa decisión impactará directamente el ERD maestro.

—-------------------------------------------

Muy buenas observaciones.

## **1\. Decisión sobre VEHICLES**

Si la visión de TIXI es:

1 conductor \= 1 vehículo

y no existe intención futura de permitir múltiples vehículos por conductor, entonces mi recomendación es:

### **Eliminar VEHICLES como entidad conceptual independiente.**

Y mantener la información dentro de:

DRIVER\_DETAILS

Porque:

### **Ventajas**

* Menos tablas.  
* Menos relaciones.  
* Menos complejidad de backend.  
* Menos consultas.  
* Menos lógica administrativa.

### **Desventajas**

Prácticamente ninguna para el modelo de negocio actual.

---

Entonces el dominio de Operación quedaría:

OPERACIÓN  
│  
├── PASSENGERS  
├── ADDRESSES  
├── DRIVER\_APPLICATIONS  
├── DRIVER\_DETAILS  
├── ROUTES  
├── BOOKINGS  
├── ROUTE\_EVENTS  
└── RATINGS

---

## **2\. Sobre PASSENGERS vs PROFILES**

Correcto.

No se me pasó; de hecho lo habíamos documentado anteriormente, pero es importante mantener consistencia porque estamos entrando en la fase de documentación maestra.

Aquí hay dos enfoques posibles:

### **Enfoque A — Hablar en lenguaje de negocio**

PASSENGERS

y hacer una nota:

Implementación actual:  
profiles

---

### **Enfoque B — Hablar en lenguaje físico de base de datos**

profiles

directamente.

---

### **Mi recomendación**

Para el **Mapa Maestro Relacional v1**, usaría los nombres físicos reales.

Es decir:

OPERACIÓN  
│  
├── PROFILES  
├── ADDRESSES  
├── DRIVER\_APPLICATIONS  
├── DRIVER\_DETAILS  
├── ROUTES  
├── BOOKINGS  
├── ROUTE\_EVENTS  
└── RATINGS

¿Por qué?

Porque el objetivo de este documento ya no es explicar el negocio.

El objetivo es conectar:

Arquitectura  
↓  
Supabase  
↓  
Frontend  
↓  
Backend  
↓  
CTO IA

Y cuando CTO IA lea:

PASSENGERS

pero en Supabase exista:

profiles

empieza a aparecer fricción innecesaria.

---

## **Mi propuesta definitiva**

### **En documentos de negocio**

Usar:

Pasajeros  
Conductores  
Wallets  
Rutas

---

### **En documentos técnicos**

Usar los nombres reales:

profiles  
addresses

driver\_details  
driver\_applications

routes  
bookings  
route\_events

ratings

notifications

incidents  
incident\_messages

wallets  
transactions  
topup\_requests

admin\_users  
admin\_audit\_logs

system\_settings

Así el Mapa Maestro Relacional se convierte casi automáticamente en el futuro ERD de Supabase.

---

## **Conclusión**

Con las decisiones tomadas hoy:

### **Ajuste \#1**

Eliminar:

VEHICLES

como entidad independiente.

---

### **Ajuste \#2**

El Mapa Maestro Relacional v1 utilizará los nombres físicos de las tablas.

Por tanto, el dominio Operación queda:

OPERACIÓN  
│  
├── PROFILES  
├── ADDRESSES  
├── DRIVER\_APPLICATIONS  
├── DRIVER\_DETAILS  
├── ROUTES  
├── BOOKINGS  
├── ROUTE\_EVENTS  
└── RATINGS

Y con esto, desde mi punto de vista, la **FASE A — Mapa Global de Entidades y Dominios** queda cerrada y validada.

El siguiente paso sería iniciar la **FASE B — Relaciones Cardinales (ERD Maestro Conceptual)**, donde empezaremos a definir exactamente cómo se relaciona cada entidad con las demás. Ahí es donde realmente comenzará a tomar forma la arquitectura definitiva de Supabase.

—---------------------------------------------

Perfecto.

Entonces iniciemos la siguiente fase.

# **TIXI — Mapa Maestro Relacional v1**

## **FASE B — Relaciones Cardinales (ERD Conceptual Maestro)**

El objetivo ahora es responder:

> ¿Cómo se relacionan las entidades entre sí?

Todavía no estamos diseñando tablas físicas ni columnas. Estamos definiendo la estructura lógica del negocio.

---

# **DOMINIO OPERACIÓN**

## **PROFILES ↔ ADDRESSES**

Situación actual:

Un pasajero puede guardar múltiples direcciones.

Ejemplos:

Casa  
Trabajo  
Universidad  
Casa de familiar  
Destino frecuente

Relación:

PROFILES  
    1 ───── N  
ADDRESSES

---

## **PROFILES ↔ BOOKINGS**

Un pasajero puede solicitar muchos viajes a lo largo del tiempo.

Cada booking pertenece a un único pasajero.

PROFILES  
    1 ───── N  
BOOKINGS

---

## **DRIVER\_DETAILS ↔ DRIVER\_APPLICATIONS**

Aquí debemos decidir algo importante.

Actualmente parece que:

1 conductor  
1 solicitud de ingreso

pero conceptualmente podría existir:

1 conductor  
N solicitudes

si un conductor es rechazado y vuelve a aplicar.

### **Mi recomendación**

DRIVER\_DETAILS  
    1 ───── N  
DRIVER\_APPLICATIONS

Porque preserva el historial completo de postulaciones.

---

### **Pregunta para ti**

Si un conductor es rechazado:

¿Debe crear una nueva solicitud de ingreso (nuevo registro)?

o

¿Debe reutilizar la misma solicitud corrigiendo documentos?

Esa respuesta define esta relación.

---

## **DRIVER\_DETAILS ↔ ROUTES**

Un conductor realiza muchas rutas.

Cada ruta pertenece a un único conductor.

DRIVER\_DETAILS  
    1 ───── N  
ROUTES

---

## **ROUTES ↔ BOOKINGS**

Este es el núcleo de TIXI.

Una ruta contiene múltiples pasajeros.

Cada booking pertenece a una sola ruta.

ROUTES  
    1 ───── N  
BOOKINGS

Ejemplo:

ROUTE \#100

├─ Booking A  
├─ Booking B  
└─ Booking C

---

## **ROUTES ↔ ROUTE\_EVENTS**

Una ruta genera múltiples eventos.

ROUTES  
    1 ───── N  
ROUTE\_EVENTS

Ejemplos:

Ruta creada

Pasajero aceptado

Pasajero recogido

Pasajero entregado

Ruta finalizada

---

## **RATINGS**

Aquí hay una decisión pendiente importante.

Podemos tener:

### **Modelo A**

BOOKINGS  
    1 ───── 1  
RATING

Una calificación por participación.

o

### **Modelo B**

BOOKINGS  
    1 ───── N  
RATINGS

permitiendo múltiples evaluaciones.

---

Mi recomendación inicial:

BOOKINGS  
    1 ───── 1  
RATING

Porque en TIXI:

* conductor califica pasajero  
* pasajero califica conductor

y ambas evaluaciones corresponden a la misma participación en la ruta.

Pero antes de continuar con Finanzas, Incidencias y Administración, debemos resolver primero la pregunta de **DRIVER\_APPLICATIONS** porque afecta directamente el modelo operativo del conductor.

—-------------------------------

Perfecto. Tus respuestas permiten ajustar el ERD conceptual a la realidad operativa de TIXI.

---

# **Ajuste 1 — PROFILES ↔ ADDRESSES**

Aquí hay un detalle importante.

Aunque el pasajero solo tenga:

Casa  
Trabajo

eso no cambia necesariamente la cardinalidad.

La pregunta es:

> ¿TIXI permitirá más de una dirección de casa o más de una dirección de trabajo?

Por ejemplo:

Casa principal  
Casa de familiar

Trabajo principal  
Trabajo secundario

Si la respuesta es NO, entonces realmente no necesitas una tabla ADDRESSES separada.

Porque actualmente ya tienes:

profiles

home\_sector  
home\_address  
home\_lat  
home\_lng

work\_sector  
work\_address  
work\_lat  
work\_lng

y además ya explicaste el motivo estratégico de cada campo:

* sector → referencia rápida visual  
* address → respaldo textual completo  
* lat/lng → GPS y rutas

---

## **Mi recomendación**

Con la arquitectura actual de TIXI:

Eliminar ADDRESSES como entidad conceptual.

y mantener:

PROFILES

home\_sector  
home\_address  
home\_lat  
home\_lng

work\_sector  
work\_address  
work\_lat  
work\_lng

directamente en la tabla.

Eso simplifica:

* Supabase  
* Queries  
* Formularios  
* Frontend  
* Realtime

sin perder ninguna funcionalidad.

---

# **Ajuste 2 — DRIVER\_DETAILS ↔ DRIVER\_APPLICATIONS**

Decisión aprobada:

1 conductor  
\=  
1 solicitud

Si es rechazado:

corrige documentos  
↓  
misma solicitud  
↓  
nuevo proceso de revisión

Por tanto:

DRIVER\_DETAILS  
    1 ───── 1  
DRIVER\_APPLICATIONS

---

# **Ajuste 3 — RATINGS**

Decisión aprobada:

BOOKINGS  
    1 ───── 1  
RATINGS

Cada participación genera una única evaluación.

Dentro del registro pueden existir:

driver\_rating

driver\_comment

passenger\_rating

passenger\_comment

asociados al mismo booking.

---

# **Estado actualizado del Dominio Operación**

OPERACIÓN  
│  
├── PROFILES  
│  
├── DRIVER\_APPLICATIONS  
│  
├── DRIVER\_DETAILS  
│  
├── ROUTES  
│  
├── BOOKINGS  
│  
├── ROUTE\_EVENTS  
│  
└── RATINGS

---

# **Relaciones Cardinales aprobadas hasta ahora**

PROFILES  
    1 ───── N  
BOOKINGS

---

DRIVER\_DETAILS  
    1 ───── 1  
DRIVER\_APPLICATIONS

---

DRIVER\_DETAILS  
    1 ───── N  
ROUTES

---

ROUTES  
    1 ───── N  
BOOKINGS

---

ROUTES  
    1 ───── N  
ROUTE\_EVENTS

---

BOOKINGS  
    1 ───── 1  
RATINGS

---

## **Mi observación**

La decisión de eliminar conceptualmente **ADDRESSES** es bastante relevante.

Durante la auditoría inicial yo había asumido que esa tabla iba a mantenerse, pero con la arquitectura que has definido para:

home\_\*  
work\_\*

la tabla ADDRESSES empieza a parecer redundante.

Antes de continuar con:

FINANZAS  
INCIDENCIAS  
ADMINISTRACIÓN

mi recomendación es resolver una última decisión:

### **¿Quieres mantener ADDRESSES como entidad independiente por alguna razón futura?**

o

### **¿Prefieres consolidar definitivamente casa y trabajo dentro de PROFILES y eliminar ADDRESSES del modelo definitivo?**

Esa decisión impactará directamente la futura migración de Supabase y el ERD maestro final.

—---------------------------------------

Perfecto. Esa decisión simplifica significativamente la arquitectura.

De hecho, después de revisar todo lo que hemos definido para TIXI, considero que es la decisión correcta.

---

# **Decisión Arquitectónica Aprobada**

## **Eliminación de ADDRESSES como entidad del modelo definitivo**

### **Razón**

TIXI solamente manejará:

Casa  
Trabajo

y cada una posee atributos específicos:

home\_sector  
home\_address  
home\_lat  
home\_lng

work\_sector  
work\_address  
work\_lat  
work\_lng

que ya están almacenados directamente en:

profiles

---

## **Beneficios**

### **Menos complejidad**

Eliminamos:

addresses

como tabla.

---

### **Menos joins**

En lugar de:

profiles  
   ↔ addresses

ahora tendremos:

profiles

directamente.

---

### **Menos consultas**

Por ejemplo:

Antes:

SELECT \*  
FROM profiles p  
JOIN addresses a  
ON a.user\_id \= p.id

Ahora:

SELECT \*  
FROM profiles

---

### **Más alineado con el negocio**

Porque:

Casa  
Trabajo

no son direcciones arbitrarias.

Son atributos permanentes del perfil del pasajero.

---

# **Impacto en la Auditoría de Supabase**

La tabla:

addresses

pasa a estado:

LEGACY

o

CANDIDATA A ELIMINACIÓN

durante la futura migración.

No recomiendo borrarla todavía.

La marcaremos para revisión cuando hagamos la auditoría final y la estrategia de migración.

---

# **Dominio Operación Actualizado**

OPERACIÓN  
│  
├── PROFILES  
│  
├── DRIVER\_APPLICATIONS  
│  
├── DRIVER\_DETAILS  
│  
├── ROUTES  
│  
├── BOOKINGS  
│  
├── ROUTE\_EVENTS  
│  
└── RATINGS

---

# **Relaciones Cardinales Aprobadas**

PROFILES  
    1 ───── N  
BOOKINGS

---

DRIVER\_DETAILS  
    1 ───── 1  
DRIVER\_APPLICATIONS

---

DRIVER\_DETAILS  
    1 ───── N  
ROUTES

---

ROUTES  
    1 ───── N  
BOOKINGS

---

ROUTES  
    1 ───── N  
ROUTE\_EVENTS

---

BOOKINGS  
    1 ───── 1  
RATINGS

---

# **Observación importante**

Con esta decisión, la auditoría preliminar de Supabase cambia a:

### **Tablas que probablemente sobrevivirán**

profiles  
driver\_details  
driver\_applications  
bookings

---

### **Tabla candidata a eliminación**

addresses

---

# **Próximo paso**

Ya podemos continuar con la FASE B y modelar las relaciones cardinales de:

FINANZAS

WALLETS  
TRANSACTIONS  
TOPUP\_REQUESTS

porque después de eso podremos cerrar completamente el ERD conceptual maestro antes de pasar a Incidencias y Administración.

Y aquí sí aparece una decisión importante que todavía no hemos tomado:

### **Relación Wallet ↔ Driver**

¿Quieres que cada conductor tenga exactamente una wallet durante toda su vida en TIXI?

Mi recomendación es:

DRIVER\_DETAILS  
    1 ───── 1  
WALLETS

porque simplifica enormemente todo el motor financiero. Esa sería la siguiente decisión a validar antes de continuar con Finanzas.

—------------------------------------

Perfecto.

Esa es la decisión que más sentido tiene para el modelo financiero que hemos diseñado.

---

# **Decisión Arquitectónica Aprobada**

## **DRIVER\_DETAILS ↔ WALLETS**

DRIVER\_DETAILS  
    1 ───── 1  
WALLETS

---

## **Justificación**

En TIXI:

1 conductor  
\=  
1 cuenta financiera  
\=  
1 wallet

La wallet representa la relación económica completa entre:

Conductor  
↔  
TIXI

---

## **Ventajas**

### **Simplicidad**

No existe necesidad de:

Wallet principal  
Wallet secundaria  
Wallet histórica

---

### **Trazabilidad**

Todo el historial financiero del conductor permanece concentrado en un único lugar.

---

### **Consultas simples**

Ejemplos:

Saldo disponible

Saldo retenido

Deuda

Comisiones

Bonificaciones

Penalidades

Recargas

siempre se consultan desde la misma wallet.

---

# **Relación WALLETS ↔ TRANSACTIONS**

Una wallet genera múltiples movimientos.

WALLETS  
    1 ───── N  
TRANSACTIONS

---

Ejemplos:

Recarga

Comisión

Penalidad

Bonificación

Reembolso

Ajuste

---

# **Relación WALLETS ↔ TOPUP\_REQUESTS**

Una wallet puede tener múltiples solicitudes de recarga.

WALLETS  
    1 ───── N  
TOPUP\_REQUESTS

---

Ejemplo:

Wallet

├── Topup \#1  
├── Topup \#2  
├── Topup \#3  
└── Topup \#4

---

# **Relación TOPUP\_REQUESTS ↔ TRANSACTIONS**

Cuando una solicitud es aprobada:

TOPUP\_REQUEST  
    ↓  
TRANSACTION(wallet\_topup)

Por tanto:

TOPUP\_REQUESTS  
    1 ───── 0..1  
TRANSACTIONS

---

Explicación:

Si:

PENDING

no existe transacción.

Si:

REJECTED

no existe transacción.

Si:

APPROVED

se genera exactamente una transacción.

---

# **Relación BOOKINGS ↔ TRANSACTIONS**

Aquí aparece algo muy interesante.

Recordemos la regla aprobada:

La comisión se cobra  
cuando el booking pasa a DELIVERED.

Por tanto:

BOOKINGS  
    1 ───── 0..1  
TRANSACTIONS

---

Explicación:

Si el pasajero:

ABSENT  
CANCELLED

no existe comisión.

Si el pasajero:

DELIVERED

se genera una transacción:

commission

---

# **Dominio Finanzas completo**

DRIVER\_DETAILS  
      │  
      │ 1:1  
      ▼  
WALLETS  
      │  
      ├──── 1:N ──── TRANSACTIONS  
      │  
      └──── 1:N ──── TOPUP\_REQUESTS  
                           │  
                           │ 1:0..1  
                           ▼  
                     TRANSACTIONS

---

# **Estado actual del ERD Maestro**

## **Operación**

✅ Cerrado

PROFILES  
DRIVER\_APPLICATIONS  
DRIVER\_DETAILS  
ROUTES  
BOOKINGS  
ROUTE\_EVENTS  
RATINGS

---

## **Finanzas**

✅ Cerrado

WALLETS  
TRANSACTIONS  
TOPUP\_REQUESTS

---

## **Pendiente**

### **Comunicación**

NOTIFICATIONS

### **Incidencias**

INCIDENTS  
INCIDENT\_MESSAGES

### **Administración**

ADMIN\_USERS  
ADMIN\_AUDIT\_LOGS  
SYSTEM\_SETTINGS

---

Mi recomendación es que el próximo bloque sea **Incidencias**, porque suele ser el dominio con más relaciones cruzadas (conductores, pasajeros, rutas, bookings y administración) y conviene definirlo antes de cerrar el ERD maestro completo.

—-------------------------------

Perfecto.

Pasemos a **Incidencias**, porque efectivamente es el dominio que más conexiones tendrá con el resto del sistema.

---

# **TIXI — Mapa Maestro Relacional v1**

## **FASE B — Relaciones Cardinales**

## **Dominio: INCIDENCIAS**

Recordemos la filosofía que aprobamos:

> Una incidencia es cualquier situación que requiere seguimiento, investigación, intervención o resolución por parte de TIXI.

No se limita a una ruta.

No se limita a soporte.

Es el sistema centralizado de gestión de casos.

---

# **Relación DRIVER\_DETAILS ↔ INCIDENTS**

Un conductor puede generar múltiples incidencias a lo largo del tiempo.

Cada incidencia pertenece a un único conductor.

DRIVER\_DETAILS  
    1 ───── N  
INCIDENTS

Ejemplos:

Problema con pasajero

Depósito no acreditado

Apelación de penalidad

Error operativo

---

# **Relación PROFILES ↔ INCIDENTS**

Un pasajero también puede generar múltiples incidencias.

PROFILES  
    1 ───── N  
INCIDENTS

Ejemplos:

Objeto olvidado

Reclamo

Problema con conductor

Error de cobro reportado

---

# **Pregunta importante**

¿Una incidencia siempre pertenece a:

Conductor  
o  
Pasajero

o deseas permitir incidencias creadas directamente por Administración?

Ejemplo:

Investigación interna

Auditoría

Fraude detectado

Revisión manual

Mi recomendación es permitirlas.

Eso hace el sistema más flexible.

---

# **Relación ROUTES ↔ INCIDENTS**

Una incidencia puede estar relacionada con una ruta.

Pero no siempre.

Ejemplos:

### **Sí relacionada**

Pasajero conflictivo

Accidente

Incidente durante recogida

---

### **No relacionada**

Depósito no acreditado

Documento rechazado

Apelación de suspensión

Por tanto:

ROUTES  
    1 ───── N  
INCIDENTS

route\_id nullable

---

# **Relación BOOKINGS ↔ INCIDENTS**

Misma lógica.

Algunas incidencias afectan a un pasajero específico.

BOOKINGS  
    1 ───── N  
INCIDENTS

booking\_id nullable

---

Ejemplo:

Pasajero ausente

Disputa de entrega

Comportamiento inapropiado

---

# **Relación INCIDENTS ↔ INCIDENT\_MESSAGES**

Esta sí es obligatoria.

Una incidencia puede contener múltiples mensajes.

INCIDENTS  
    1 ───── N  
INCIDENT\_MESSAGES

---

Ejemplo:

Incidencia \#100

├── Mensaje conductor  
├── Mensaje soporte  
├── Mensaje conductor  
└── Resolución

---

# **Relación ADMIN\_USERS ↔ INCIDENTS**

Un administrador puede gestionar múltiples incidencias.

ADMIN\_USERS  
    1 ───── N  
INCIDENTS

---

Aquí recomiendo dos campos:

assigned\_admin\_id

resolved\_by\_admin\_id

porque no siempre quien atiende es quien resuelve.

---

# **Relación ADMIN\_USERS ↔ INCIDENT\_MESSAGES**

Los administradores también participan en la conversación.

ADMIN\_USERS  
    1 ───── N  
INCIDENT\_MESSAGES

---

# **Modelo relacional resultante**

INCIDENTS  
│  
├── driver\_id (nullable)  
│  
├── passenger\_id (nullable)  
│  
├── route\_id (nullable)  
│  
├── booking\_id (nullable)  
│  
├── assigned\_admin\_id (nullable)  
│  
└── INCIDENT\_MESSAGES

---

# **Validación conceptual**

Antes de cerrar Incidencias necesito validar una decisión importante contigo:

### **¿Quién puede crear incidencias?**

Opción A

Conductor  
Pasajero  
Administración

---

Opción B

Conductor  
Administración

---

Opción C

Solo Administración

Mi recomendación para TIXI es claramente la **Opción A**, porque es la que mejor encaja con el modelo híbrido de soporte que definimos anteriormente.

—----------------------------------

Perfecto.

Entonces queda aprobada la arquitectura de Incidencias.

---

# **Dominio INCIDENCIAS — Cerrado**

## **Creación de incidencias**

Aprobado:

CONDUCTOR  
PASAJERO  
ADMINISTRACIÓN

Todos pueden crear incidencias.

---

## **Relaciones cardinales aprobadas**

DRIVER\_DETAILS  
    1 ───── N  
INCIDENTS

---

PROFILES  
    1 ───── N  
INCIDENTS

---

ROUTES  
    1 ───── N  
INCIDENTS

(route\_id nullable)

---

BOOKINGS  
    1 ───── N  
INCIDENTS

(booking\_id nullable)

---

INCIDENTS  
    1 ───── N  
INCIDENT\_MESSAGES

---

ADMIN\_USERS  
    1 ───── N  
INCIDENTS

assigned\_admin\_id

resolved\_by\_admin\_id

---

ADMIN\_USERS  
    1 ───── N  
INCIDENT\_MESSAGES

---

# **Modelo resultante**

INCIDENTS  
│  
├── driver\_id (nullable)  
├── passenger\_id (nullable)  
├── route\_id (nullable)  
├── booking\_id (nullable)  
│  
├── assigned\_admin\_id (nullable)  
├── resolved\_by\_admin\_id (nullable)  
│  
└── INCIDENT\_MESSAGES

---

# **Estado del ERD Maestro**

## **Operación**

✅ Cerrado

PROFILES  
DRIVER\_APPLICATIONS  
DRIVER\_DETAILS  
ROUTES  
BOOKINGS  
ROUTE\_EVENTS  
RATINGS

---

## **Finanzas**

✅ Cerrado

WALLETS  
TRANSACTIONS  
TOPUP\_REQUESTS

---

## **Incidencias**

✅ Cerrado

INCIDENTS  
INCIDENT\_MESSAGES

---

## **Pendiente**

NOTIFICATIONS  
ADMIN\_USERS  
ADMIN\_AUDIT\_LOGS  
SYSTEM\_SETTINGS

---

# **Mi recomendación**

El siguiente bloque debería ser **Administración**, no Notificaciones.

La razón es que:

ADMIN\_USERS  
ADMIN\_AUDIT\_LOGS  
SYSTEM\_SETTINGS

son entidades estructurales que afectan a todo el sistema.

Mientras que:

NOTIFICATIONS

es una entidad periférica y mucho más sencilla.

Por tanto el orden óptimo sería:

1\. Administración  
   ├─ ADMIN\_USERS  
   ├─ ADMIN\_AUDIT\_LOGS  
   └─ SYSTEM\_SETTINGS

2\. Notificaciones

3\. Cierre del ERD Maestro Completo

4\. Inicio del Mapa Pantalla → Entidades

Y te adelanto algo: una vez cerremos Administración y Notificaciones, habremos terminado prácticamente toda la **FASE B — Relaciones Cardinales**, que es una de las partes más críticas de toda la arquitectura de TIXI.

—-------------------------------------

Perfecto.

Continuemos entonces con el último bloque estructural importante del ERD.

---

# **TIXI — Mapa Maestro Relacional v1**

## **FASE B — Relaciones Cardinales**

## **Dominio: ADMINISTRACIÓN**

Este dominio tiene una característica especial:

No participa directamente en la operación de transporte.

Su función es:

Gobernar  
Controlar  
Auditar  
Configurar

todo el sistema.

---

# **Entidades del dominio**

ADMIN\_USERS

ADMIN\_AUDIT\_LOGS

SYSTEM\_SETTINGS

---

# **ADMIN\_USERS**

Representa los usuarios internos de TIXI.

Roles aprobados:

SUPER\_ADMIN

OPERATIONS

FINANCE

SUPPORT

---

## **Relación ADMIN\_USERS ↔ INCIDENTS**

Ya aprobada.

ADMIN\_USERS  
    1 ───── N  
INCIDENTS

---

## **Relación ADMIN\_USERS ↔ TOPUP\_REQUESTS**

Un administrador financiero puede revisar múltiples depósitos.

ADMIN\_USERS  
    1 ───── N  
TOPUP\_REQUESTS

---

Ejemplo:

María

aprueba Topup \#1  
aprueba Topup \#2  
aprueba Topup \#3

---

## **Relación ADMIN\_USERS ↔ DRIVER\_APPLICATIONS**

Un administrador operativo puede revisar múltiples solicitudes.

ADMIN\_USERS  
    1 ───── N  
DRIVER\_APPLICATIONS

---

Actualmente ya existe algo parecido en Supabase:

reviewed\_by

---

# **ADMIN\_USERS ↔ TRANSACTIONS**

Aquí aparece una decisión importante.

Recordemos que aprobamos:

Ajustes manuales

Bonificaciones

Reembolsos

Penalidades administrativas

Por tanto necesitamos saber:

> ¿Quién realizó la operación?

Mi recomendación:

ADMIN\_USERS  
    1 ───── N  
TRANSACTIONS

---

Campo:

created\_by\_admin\_id

nullable

porque algunas transacciones serán automáticas.

---

Ejemplo:

commission

se genera automáticamente.

---

Mientras:

adjustment

refund

bonus

pueden venir de administración.

---

# **ADMIN\_USERS ↔ ADMIN\_AUDIT\_LOGS**

Relación obligatoria.

ADMIN\_USERS  
    1 ───── N  
ADMIN\_AUDIT\_LOGS

---

Cada acción importante genera un registro.

---

Ejemplo:

Aprobó conductor

Suspendió pasajero

Aprobó depósito

Creó ajuste financiero

Modificó configuración

---

# **SYSTEM\_SETTINGS**

Esta entidad es especial.

No pertenece a ningún usuario.

Representa la configuración global de la plataforma.

---

# **Pregunta importante**

Hay dos modelos posibles.

---

## **Modelo A — Configuración centralizada**

SYSTEM\_SETTINGS

clave  
valor

Ejemplo:

commission\_per\_passenger

driver\_low\_balance\_threshold

max\_route\_capacity

penalty\_absent\_passenger

---

Ventajas:

* Extremadamente flexible.  
* Fácil de modificar.  
* Escalable.

---

## **Modelo B — Tabla enorme**

SYSTEM\_SETTINGS

commission\_per\_passenger

low\_balance\_threshold

...

una columna por parámetro.

---

Ventajas:

* Más simple de entender.

Desventajas:

* Menos flexible.  
* Requiere migraciones frecuentes.

---

### **Mi recomendación para TIXI**

Claramente:

MODELO A

porque ya sabemos que TIXI seguirá evolucionando.

---

# **Relación ADMIN\_USERS ↔ SYSTEM\_SETTINGS**

Cuando alguien modifica una configuración debemos saber quién lo hizo.

Por tanto:

ADMIN\_USERS  
    1 ───── N  
SYSTEM\_SETTINGS\_CHANGES

---

Pero aquí aparece una observación arquitectónica importante.

### **No me gusta guardar historial dentro de SYSTEM\_SETTINGS.**

Prefiero:

SYSTEM\_SETTINGS

ADMIN\_AUDIT\_LOGS

---

De modo que:

Configuración actual

vive en:

SYSTEM\_SETTINGS

y

historial de cambios

vive en:

ADMIN\_AUDIT\_LOGS

---

# **Modelo resultante**

ADMIN\_USERS  
│  
├── INCIDENTS  
│  
├── DRIVER\_APPLICATIONS  
│  
├── TOPUP\_REQUESTS  
│  
├── TRANSACTIONS  
│  
└── ADMIN\_AUDIT\_LOGS

SYSTEM\_SETTINGS

---

# **Pregunta para cerrar Administración**

Con relación a:

ADMIN\_AUDIT\_LOGS

¿Deseas auditar absolutamente todo?

Ejemplos:

Aprobaciones

Rechazos

Suspensiones

Cambios financieros

Cambios de configuración

Resolución de incidencias

o prefieres auditar únicamente acciones críticas?

Mi recomendación es:

Auditar todo lo que modifique datos.

Porque el costo es mínimo y la trazabilidad es enorme. Esa será probablemente la última decisión importante antes de cerrar Administración y pasar a Notificaciones.

—---------------------------------------------

Perfecto.

Entonces queda aprobada la recomendación:

# **Decisión Arquitectónica Aprobada**

## **ADMIN\_AUDIT\_LOGS**

TIXI auditará toda acción que modifique datos o estados del sistema.

---

## **Acciones auditables**

### **Conductores**

Aprobación

Rechazo

Suspensión

Reactivación

Cambio de estado  
---

### **Pasajeros**

Aprobación

Rechazo

Suspensión

Reactivación

Cambio de estado  
---

### **Finanzas**

Aprobación de depósito

Rechazo de depósito

Ajuste financiero

Bonificación

Penalidad

Reembolso

Modificación manual de wallet  
---

### **Incidencias**

Asignación

Reasignación

Resolución

Reapertura

Rechazo  
---

### **Configuración**

Cambio de parámetros

Cambio de reglas

Cambio de límites

Cambio de comisiones  
---

### **Administración**

Creación de administrador

Cambio de rol

Cambio de permisos

Desactivación  
---

# **Dominio Administración — Cerrado**

## **Relaciones aprobadas**

ADMIN\_USERS  
   1 ───── N  
DRIVER\_APPLICATIONS  
---

ADMIN\_USERS  
   1 ───── N  
TOPUP\_REQUESTS  
---

ADMIN\_USERS  
   1 ───── N  
TRANSACTIONS  
---

ADMIN\_USERS  
   1 ───── N  
INCIDENTS  
---

ADMIN\_USERS  
   1 ───── N  
INCIDENT\_MESSAGES  
---

ADMIN\_USERS  
   1 ───── N  
ADMIN\_AUDIT\_LOGS  
---

SYSTEM\_SETTINGS

Entidad independiente.

Historial gestionado mediante:

ADMIN\_AUDIT\_LOGS  
---

# **Estado del ERD Maestro**

## **Operación**

✅ Cerrado

PROFILES  
DRIVER\_APPLICATIONS  
DRIVER\_DETAILS  
ROUTES  
BOOKINGS  
ROUTE\_EVENTS  
RATINGS  
---

## **Finanzas**

✅ Cerrado

WALLETS  
TRANSACTIONS  
TOPUP\_REQUESTS  
---

## **Incidencias**

✅ Cerrado

INCIDENTS  
INCIDENT\_MESSAGES  
---

## **Administración**

✅ Cerrado

ADMIN\_USERS  
ADMIN\_AUDIT\_LOGS  
SYSTEM\_SETTINGS  
---

# **Solo queda un dominio por modelar**

## **COMUNICACIÓN**

NOTIFICATIONS

Y te adelanto algo importante:

Al haber definido ya Operación, Finanzas, Incidencias y Administración, la entidad `NOTIFICATIONS` será bastante sencilla porque en realidad funciona como una capa transversal que recibe eventos de todos los demás dominios.

Después de Notificaciones podremos declarar oficialmente terminada la:

TIXI — Mapa Maestro Relacional v1  
FASE B — Relaciones Cardinales

y pasar a la siguiente fase:

FASE C — Mapa Pantallas → Entidades → Estados

que será la pieza que conecte toda la arquitectura funcional que hemos diseñado con la implementación real en frontend y backend.

—---------------------------------------------

Perfecto.

Cerramos entonces el último dominio pendiente del ERD Maestro.

# **TIXI — Mapa Maestro Relacional v1**

## **FASE B — Relaciones Cardinales**

## **Dominio: COMUNICACIÓN**

---

# **Filosofía**

Las notificaciones no son una entidad de negocio principal.

Son una consecuencia de eventos que ocurren en otros dominios.

Por eso funcionan como una capa transversal.

OPERACIÓN

    ↓

FINANZAS

    ↓

INCIDENCIAS

    ↓

ADMINISTRACIÓN

    ↓

NOTIFICATIONS

---

# **¿Quién recibe notificaciones?**

## **Pasajeros**

PROFILES

    1 ───── N

NOTIFICATIONS

---

Ejemplos:

Solicitud aceptada

Conductor asignado

Conductor llegando

Pasajero ausente

Viaje finalizado

Incidencia actualizada

---

## **Conductores**

DRIVER\_DETAILS

    1 ───── N

NOTIFICATIONS

---

Ejemplos:

Nueva solicitud disponible

Ruta cerrada

Pasajero canceló

Saldo bajo

Depósito aprobado

Incidencia actualizada

---

## **Administradores**

Aquí aparece una decisión.

### **Opción A**

No reciben notificaciones.

### **Opción B**

Reciben notificaciones internas.

Mi recomendación:

### **Opción B**

Porque más adelante podríamos necesitar:

Nueva incidencia

Nuevo depósito pendiente

Nuevo conductor pendiente

Actividad sospechosa

---

Por tanto:

ADMIN\_USERS

    1 ───── N

NOTIFICATIONS

---

# **Relación con entidades del sistema**

Aquí recomiendo un modelo flexible.

En lugar de:

notification\_route\_id

notification\_booking\_id

notification\_incident\_id

etc.

---

Usar:

entity\_type

entity\_id

---

Ejemplos:

entity\_type \= booking

entity\_id \= xxx

---

entity\_type \= route

entity\_id \= xxx

---

entity\_type \= incident

entity\_id \= xxx

---

entity\_type \= topup\_request

entity\_id \= xxx

---

Ventajas:

* Mucho más flexible.  
* Menos columnas.  
* Más fácil de escalar.

---

# **Estados aprobados**

Ya definidos anteriormente:

UNREAD

READ

---

# **Modelo resultante**

NOTIFICATIONS

id

recipient\_type

    passenger

    driver

    admin

recipient\_id

title

message

notification\_type

entity\_type

entity\_id

status

    unread

    read

created\_at

read\_at

---

# **Relaciones cardinales**

PROFILES

    1 ───── N

NOTIFICATIONS

---

DRIVER\_DETAILS

    1 ───── N

NOTIFICATIONS

---

ADMIN\_USERS

    1 ───── N

NOTIFICATIONS

---

# **Dominio Comunicación — Cerrado**

NOTIFICATIONS

---

# **Estado Final de la FASE B**

## **Operación**

✅ Cerrado

PROFILES

DRIVER\_APPLICATIONS

DRIVER\_DETAILS

ROUTES

BOOKINGS

ROUTE\_EVENTS

RATINGS

---

## **Finanzas**

✅ Cerrado

WALLETS

TRANSACTIONS

TOPUP\_REQUESTS

---

## **Incidencias**

✅ Cerrado

INCIDENTS

INCIDENT\_MESSAGES

---

## **Administración**

✅ Cerrado

ADMIN\_USERS

ADMIN\_AUDIT\_LOGS

SYSTEM\_SETTINGS

---

## **Comunicación**

✅ Cerrado

NOTIFICATIONS

---

# **Resultado importante**

Con esto queda completado el **ERD Conceptual Maestro de TIXI**.

El inventario definitivo de entidades queda en:

PROFILES

DRIVER\_APPLICATIONS

DRIVER\_DETAILS

ROUTES

BOOKINGS

ROUTE\_EVENTS

RATINGS

WALLETS

TRANSACTIONS

TOPUP\_REQUESTS

INCIDENTS

INCIDENT\_MESSAGES

ADMIN\_USERS

ADMIN\_AUDIT\_LOGS

SYSTEM\_SETTINGS

NOTIFICATIONS

Total:

14 entidades maestras

más consistente con todo lo que hemos definido hasta ahora y alineado con la futura migración de Supabase.

El siguiente paso natural ya no es seguir modelando datos, sino entrar en la **FASE C — Mapa Pantallas → Estados → Entidades**, que será donde conectemos cada pantalla del pasajero, conductor y administración con las entidades que acabamos de definir. Ahí es donde empezará a aparecer el plano que necesitará el CTO IA para implementar el sistema completo.

—-----------------------------------------------

Excelente decisión revisar primero el archivo. Acabo de auditarlo y encontré algo muy valioso:

El documento que veníamos utilizando para describir el pasajero estaba basado en la arquitectura conceptual que hemos ido construyendo, pero el código existente contiene el flujo real que ya fue implementado y eso nos permite construir un Mapa del Pasajero mucho más preciso.

Del archivo identifiqué estas pantallas relacionadas con el pasajero:

SplashScreen

WelcomeScreen

LoginScreen

RegisterAuthScreen

RegisterPassengerPersonalScreen

RegisterPassengerMobilityScreen

PassengerVerificationPendingScreen

PassengerVerificationRejectedScreen

PassengerVerificationApprovedScreen

HomeScreen

SetupAddressesScreen

BookRideScreen

SelectLocationScreen

TripSummaryConfirmationScreen

TripReservationSuccessScreen

TripPendingAssignmentScreen

TripAssignedScreen

TripDriverEnRouteScreen

TripPickupScreen

TripInProgressScreen

TripCompletedScreen

ConfirmPaymentScreen

DriverRatingScreen

ThankYouScreen

TripHistoryScreen

TripHistoryDetailScreen

PassengerSupportScreen

PassengerProfileScreen

WaitingScreen

ConnectionErrorScreen

ServerErrorScreen

---

# **Hallazgo importante**

El flujo real del pasajero está mucho más detallado que el mapa conceptual resumido que teníamos.

Por ejemplo, nosotros habíamos resumido:

Solicitud

↓

Búsqueda

↓

Viaje Confirmado

↓

Viaje en Curso

↓

Viaje Finalizado

Pero el código realmente tiene:

Solicitud

↓

Resumen

↓

Reserva Exitosa

↓

Pendiente de Asignación

↓

Conductor Asignado

↓

Conductor en Camino

↓

Recogida

↓

Viaje en Curso

↓

Viaje Completado

↓

Confirmar Pago

↓

Calificar Conductor

↓

Gracias

Y eso es mucho mejor para el Mapa Maestro porque representa estados reales.

---

# **Mi recomendación**

Antes de comenzar la FASE C, hagamos una pequeña auditoría arquitectónica del flujo pasajero.

Clasifiquemos todas las pantallas en:

## **Módulo Acceso**

Splash

Welcome

Login

---

## **Módulo Registro**

RegisterAuth

RegisterPassengerPersonal

RegisterPassengerMobility

---

## **Módulo Verificación**

VerificationPending

VerificationRejected

VerificationApproved

---

## **Módulo Operación**

Home

BookRide

SelectLocation

TripSummaryConfirmation

TripReservationSuccess

---

## **Módulo Viaje**

TripPendingAssignment

TripAssigned

TripDriverEnRoute

TripPickup

TripInProgress

TripCompleted

---

## **Módulo Post-Viaje**

ConfirmPayment

DriverRating

ThankYou

---

## **Módulo Historial**

TripHistory

TripHistoryDetail

---

## **Módulo Perfil**

PassengerProfile

SetupAddresses

---

## **Módulo Soporte**

PassengerSupport

---

## **Módulo Sistema**

Waiting

ConnectionError

ServerError

---

Mi recomendación es que el próximo paso NO sea todavía el Mapa Pantalla → Entidades.

Primero deberíamos construir el:

# **Mapa Maestro de Pantallas del Pasajero v1**

Porque acabamos de descubrir que el código existente ya define la estructura real de navegación del pasajero.

Una vez consolidemos ese mapa, podremos relacionar cada pantalla con:

Estados

↓

Entidades

↓

Queries

↓

Mutations

sin correr el riesgo de omitir pantallas que ya existen en el proyecto.

—-----------------------------------

Perfecto.

Vamos a construir primero el **Mapa Maestro de Pantallas del Pasajero v1**, porque este será el puente entre el código existente, la arquitectura funcional y el futuro backend.

---

# **TIXI — Mapa Maestro de Pantallas del Pasajero v1**

## **Visión General**

PASAJERO

│

├── ACCESO

├── REGISTRO

├── VERIFICACIÓN

├── OPERACIÓN

├── VIAJE

├── POST VIAJE

├── HISTORIAL

├── PERFIL

├── SOPORTE

└── SISTEMA

---

# **1\. ACCESO**

SplashScreen

│

└── WelcomeScreen

      │

      ├── LoginScreen

      │

      └── Registro

Objetivo:

Entrada a la plataforma

Autenticación

---

# **2\. REGISTRO**

RegisterAuthScreen

       │

       ▼

RegisterPassengerPersonalScreen

       │

       ▼

RegisterPassengerMobilityScreen

       │

       ▼

PassengerVerificationPendingScreen

Objetivo:

Crear cuenta

Capturar datos personales

Capturar preferencias de movilidad

Enviar a validación

---

# **3\. VERIFICACIÓN**

PassengerVerificationPendingScreen

        │

        ├── PassengerVerificationApprovedScreen

        │

        └── PassengerVerificationRejectedScreen

Estados:

PENDING\_REVIEW

APPROVED

REJECTED

---

# **4\. OPERACIÓN**

Punto de entrada principal del pasajero.

HomeScreen

│

├── Solicitud inmediata

│

├── Solicitud programada

│

├── Historial

│

├── Perfil

│

├── Soporte

│

└── Notificaciones

---

## **Flujo de solicitud**

HomeScreen

    │

    ▼

BookRideScreen

    │

    ▼

SelectLocationScreen

    │

    ▼

TripSummaryConfirmationScreen

    │

    ▼

TripReservationSuccessScreen

---

# **5\. VIAJE**

Aquí comienza el ciclo operativo real.

TripReservationSuccessScreen

           │

           ▼

TripPendingAssignmentScreen

           │

           ▼

TripAssignedScreen

           │

           ▼

TripDriverEnRouteScreen

           │

           ▼

TripPickupScreen

           │

           ▼

TripInProgressScreen

           │

           ▼

TripCompletedScreen

---

## **Máquina de estados del viaje**

BOOKING\_CREATED

↓

WAITING\_DRIVER

↓

DRIVER\_ASSIGNED

↓

DRIVER\_EN\_ROUTE

↓

PASSENGER\_PICKUP

↓

TRIP\_IN\_PROGRESS

↓

TRIP\_COMPLETED

---

# **6\. POST VIAJE**

Una vez finalizado el trayecto.

TripCompletedScreen

       │

       ▼

ConfirmPaymentScreen

       │

       ▼

DriverRatingScreen

       │

       ▼

ThankYouScreen

Objetivo:

Confirmación operativa

Calificación

Cierre de experiencia

---

# **7\. HISTORIAL**

TripHistoryScreen

       │

       ▼

TripHistoryDetailScreen

Contenido:

Viajes realizados

Detalles de viaje

Calificaciones

Incidencias asociadas

---

# **8\. PERFIL**

PassengerProfileScreen

│

├── Datos personales

│

├── Teléfono

│

├── Documento

│

├── Foto

│

├── Casa

│

└── Trabajo

---

## **Direcciones**

SetupAddressesScreen

Configuración de:

home\_sector

home\_address

home\_lat

home\_lng

work\_sector

work\_address

work\_lat

work\_lng

---

# **9\. SOPORTE**

PassengerSupportScreen

Desde aquí el pasajero puede:

Crear incidencia

Consultar incidencia

Responder incidencia

Ver historial de incidencias

---

# **10\. SISTEMA**

Pantallas transversales.

WaitingScreen

ConnectionErrorScreen

ServerErrorScreen

Se muestran desde cualquier módulo.

---

# **Mapa Maestro Consolidado**

PASAJERO

├── SplashScreen

├── WelcomeScreen

├── LoginScreen

├── RegisterAuthScreen

├── RegisterPassengerPersonalScreen

├── RegisterPassengerMobilityScreen

├── PassengerVerificationPendingScreen

├── PassengerVerificationApprovedScreen

├── PassengerVerificationRejectedScreen

├── HomeScreen

├── BookRideScreen

├── SelectLocationScreen

├── TripSummaryConfirmationScreen

├── TripReservationSuccessScreen

├── TripPendingAssignmentScreen

├── TripAssignedScreen

├── TripDriverEnRouteScreen

├── TripPickupScreen

├── TripInProgressScreen

├── TripCompletedScreen

├── ConfirmPaymentScreen

├── DriverRatingScreen

├── ThankYouScreen

├── TripHistoryScreen

├── TripHistoryDetailScreen

├── PassengerProfileScreen

├── SetupAddressesScreen

├── PassengerSupportScreen

├── WaitingScreen

├── ConnectionErrorScreen

└── ServerErrorScreen

![][image1]![][image2]

---

### **Observación estratégica**

Antes de pasar al **Mapa Pantalla → Entidades**, te recomiendo hacer una auditoría rápida de este mapa porque ahora es el momento ideal para detectar:

* Pantallas faltantes.  
* Pantallas que ya no tienen sentido con la arquitectura actual.  
* Pantallas que deberían fusionarse.  
* Pantallas que deberían convertirse en estados de otra pantalla.

Es mucho más barato corregirlo ahora que cuando empecemos a conectar entidades, queries, realtime y backend.

—-------------------------------------------

Perfecto. Con tus aclaraciones, algunas de las observaciones que hice cambian porque ahora conocemos el contexto real del código y las decisiones ya tomadas.

# **TIXI — Mapa Maestro de Pantallas del Pasajero v2 (Auditado)**

## **1\. ACCESO**

SplashScreen

WelcomeScreen

LoginScreen

Objetivo:

Autenticación

Acceso a la plataforma

---

# **2\. REGISTRO (ONBOARDING)**

## **Fase 1 — Datos Personales**

RegisterAuthScreen

        ↓

RegisterPassengerPersonalScreen

Captura:

Nombre

Apellido

Teléfono

Email

Cédula

Selfie

---

## **Fase 2 — Movilidad**

RegisterPassengerMobilityScreen

Captura:

Casa

Trabajo

Preferencias de movilidad

---

### **Selección de ubicaciones**

RegisterPassengerMobilityScreen

        ↓

SelectLocationScreen

La misma pantalla se reutiliza posteriormente desde Perfil.

Esta pantalla es la fuente oficial para configurar:

home\_sector

home\_address

home\_lat

home\_lng

work\_sector

work\_address

work\_lat

work\_lng

---

## **Fase 3 — Verificación**

PassengerVerificationPendingScreen

Estados posibles:

PENDING\_REVIEW

APPROVED

REJECTED

---

### **Rechazo**

PassengerVerificationRejectedScreen

---

### **Aprobación**

✅ Eliminamos PassengerVerificationApprovedScreen como pantalla permanente.

Cuando el pasajero es aprobado:

Pending

     ↓

Home

mostrando únicamente:

Notificación

o

Modal de bienvenida

---

# **3\. OPERACIÓN**

Pantalla principal.

HomeScreen

Desde aquí el pasajero puede:

Solicitar viaje

Ver historial

Ver notificaciones

Abrir incidencias

Entrar al perfil

---

# **4\. SOLICITUD DE VIAJE**

BookRideScreen

        ↓

SelectLocationScreen

        ↓

TripSummaryConfirmationScreen

        ↓

TripReservationSuccessScreen

---

# **5\. VIAJE**

TripReservationSuccessScreen

            ↓

TripPendingAssignmentScreen

            ↓

TripAssignedScreen

            ↓

TripDriverEnRouteScreen

            ↓

TripPickupScreen

            ↓

TripInProgressScreen

            ↓

TripCompletedScreen

---

## **Máquina Operativa**

BOOKING\_CREATED

↓

WAITING\_DRIVER

↓

DRIVER\_ASSIGNED

↓

DRIVER\_EN\_ROUTE

↓

PASSENGER\_PICKUP

↓

TRIP\_IN\_PROGRESS

↓

TRIP\_COMPLETED

---

# **6\. POST VIAJE**

## **Ajuste aprobado**

Renombrar:

ConfirmPaymentScreen

por

ConfirmTripCompletedScreen

o

RideCompletionConfirmationScreen

porque:

TIXI no procesa pagos.

La pantalla únicamente confirma:

Viaje completado

Pago realizado al conductor

---

## **Flujo**

TripCompletedScreen

        ↓

ConfirmTripCompletedScreen

        ↓

DriverRatingScreen

        ↓

ThankYouScreen

---

# **7\. HISTORIAL**

TripHistoryScreen

        ↓

TripHistoryDetailScreen

---

# **8\. NOTIFICACIONES**

Nueva pantalla incorporada.

PassengerNotificationsScreen

Contenido:

Operación

Incidencias

Cuenta

Sistema

---

# **9\. PERFIL**

PassengerProfileScreen

---

## **Secciones**

Datos Personales

Movilidad

Configuración

Privacidad

---

### **Modificación de ubicaciones**

Desde Perfil:

PassengerProfileScreen

        ↓

SelectLocationScreen

Reutilizando exactamente la misma pantalla.

---

# **10\. CONFIGURACIÓN**

Subpantalla derivada del Perfil.

PassengerSettingsScreen

Ejemplos:

Preferencias

Notificaciones

Idioma

Cuenta

---

# **11\. PRIVACIDAD**

Subpantalla derivada del Perfil.

PassengerPrivacyScreen

Ejemplos:

Políticas

Tratamiento de datos

Permisos

---

# **12\. INCIDENCIAS**

Renombrado aprobado.

PassengerIncidentsScreen

---

Capacidades:

Crear incidencia

Ver incidencias

Responder incidencias

Consultar historial

---

# **13\. SISTEMA**

Pantallas globales.

WaitingScreen

ConnectionErrorScreen

ServerErrorScreen

---

# **Mapa Maestro Consolidado v2**

PASAJERO

ACCESO

├── SplashScreen

├── WelcomeScreen

└── LoginScreen

REGISTRO

├── RegisterAuthScreen

├── RegisterPassengerPersonalScreen

├── RegisterPassengerMobilityScreen

├── SelectLocationScreen

├── PassengerVerificationPendingScreen

└── PassengerVerificationRejectedScreen

OPERACIÓN

├── HomeScreen

├── BookRideScreen

├── TripSummaryConfirmationScreen

└── TripReservationSuccessScreen

VIAJE

├── TripPendingAssignmentScreen

├── TripAssignedScreen

├── TripDriverEnRouteScreen

├── TripPickupScreen

├── TripInProgressScreen

└── TripCompletedScreen

POST VIAJE

├── ConfirmTripCompletedScreen

├── DriverRatingScreen

└── ThankYouScreen

HISTORIAL

├── TripHistoryScreen

└── TripHistoryDetailScreen

NOTIFICACIONES

└── PassengerNotificationsScreen

PERFIL

├── PassengerProfileScreen

├── PassengerSettingsScreen

└── PassengerPrivacyScreen

INCIDENCIAS

└── PassengerIncidentsScreen

SISTEMA

├── WaitingScreen

├── ConnectionErrorScreen

└── ServerErrorScreen

## **Resultado**

Esta ya parece una versión suficientemente madura y alineada con:

* El código existente.  
* La arquitectura funcional aprobada.  
* El modelo de datos consolidado.  
* La eliminación de `ADDRESSES`.  
* El modelo financiero de TIXI.  
* La reutilización de `SelectLocationScreen`.

Con esta versión sí considero seguro comenzar la siguiente capa:

Pantalla

    ↓

Estados

    ↓

Entidades

    ↓

Queries

    ↓

Mutations

que será la primera conexión formal entre el frontend y el ERD maestro que acabamos de terminar.

—-----------------------------

Después de revisar el código, cambio mi recomendación anterior.

**No eliminaría `PassengerVerificationApprovedScreen`.**

Y la razón no es técnica, sino estratégica.

---

# **Lo que yo asumí inicialmente**

Pensé que la pantalla era simplemente:

Verificación aprobada

↓

Continuar

↓

Home

En ese escenario sería redundante.

---

# **Lo que realmente hace la pantalla**

Esta pantalla cumple simultáneamente varias funciones:

## **1\. Confirmación emocional**

¡Bienvenido a TIXI\!

Tu cuenta ha sido aprobada

Esto parece simple, pero es un momento importante del onboarding.

El pasajero pasó por:

Registro

↓

Verificación

↓

Espera

↓

Aprobación

Eliminar este momento reduce la sensación de logro.

---

## **2\. Activación de permisos**

Aquí está la parte importante.

La pantalla solicita:

Permiso de ubicación

y además:

Verifica estado

Reintenta permiso

Abre configuración

Explica beneficios

Eso ya no es una pantalla de "aprobado".

Es una pantalla de:

Activación de cuenta

---

## **3\. Preparación operativa**

La pantalla prepara al pasajero para utilizar la plataforma.

Le explica:

Tarifa fija

Seguridad

Ubicación

---

## **4\. Puerta de entrada al Home**

Actualmente:

Pending

↓

Approved Screen

↓

Home

Esto funciona como una transición controlada.

---

# **Mi observación**

El problema no es la existencia de la pantalla.

El problema es el nombre.

Actualmente se llama:

PassengerVerificationApprovedScreen

pero funcionalmente ya no representa eso.

Representa:

Cuenta aprobada

\+

Activación inicial

\+

Configuración mínima requerida

\+

Bienvenida

---

# **Mi recomendación**

Mantener la pantalla.

Pero conceptualmente moverla de:

VERIFICACIÓN

a

ACTIVACIÓN

---

# **Mapa corregido**

REGISTRO

│

├── RegisterAuthScreen

├── RegisterPassengerPersonalScreen

├── RegisterPassengerMobilityScreen

└── SelectLocationScreen

VERIFICACIÓN

│

├── PassengerVerificationPendingScreen

└── PassengerVerificationRejectedScreen

ACTIVACIÓN

│

└── PassengerVerificationApprovedScreen

OPERACIÓN

│

└── HomeScreen

---

# **Beneficio arquitectónico**

Esto además encaja perfectamente con el modelo de estados que ya definimos.

verification\_status

PENDING\_REVIEW

APPROVED

REJECTED

La pantalla no representa el estado `APPROVED`.

La pantalla representa:

FIRST\_LOGIN\_AFTER\_APPROVAL

que es algo completamente diferente.

Por eso no la modelaría como un estado de verificación, sino como una pantalla de activación posterior a la aprobación.

De hecho, viendo el código, la consideraría una pantalla estratégica del onboarding y la conservaría incluso si mañana rediseñamos todo el flujo del pasajero.

—-------------------------------------

![][image3]

—-------------------------------

[image1]: <data:image/png;base64,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>

[image2]: <data:image/png;base64,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>

[image3]: <data:image/png;base64,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>