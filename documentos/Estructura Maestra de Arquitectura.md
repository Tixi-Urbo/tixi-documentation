Perfecto. Después de revisar todo lo que hemos definido, veo algo importante:

**El esquema actual es muy bueno como inventario**, pero todavía no es un verdadero mapa arquitectónico porque no muestra las relaciones entre los elementos.

Yo haría un ajuste antes de comenzar cualquier documento formal.

---

# **TIXI — Estructura Maestra de Arquitectura**

La dividiría en 6 capas:

CAPA 1  
Actores

CAPA 2  
Dominios de Negocio

CAPA 3  
Pantallas

CAPA 4  
Estados

CAPA 5  
Entidades

CAPA 6  
Integraciones

---

# **CAPA 1 — ACTORES**

PASAJERO

CONDUCTOR

ADMINISTRACIÓN

---

# **CAPA 2 — DOMINIOS DE NEGOCIO**

Esto es algo que todavía no habíamos formalizado explícitamente.

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

Estos dominios serán muy útiles cuando organicemos backend, frontend y Supabase.

---

# **CAPA 3 — PANTALLAS**

## **PASAJERO**

Home  
├─ Solicitud Inmediata  
├─ Solicitud Programada

Viaje  
├─ Esperando Conductor  
├─ Conductor en Camino  
├─ Viaje en Curso  
└─ Viaje Finalizado

Historial  
└─ Detalle de Viaje

Notificaciones

Perfil

Calificaciones

---

## **CONDUCTOR**

Home

Marketplace  
└─ Detalle Solicitud

Ruta en Construcción

Ruta Cerrada

Ruta Activa

Ruta Finalizada

Historial  
└─ Detalle Ruta

Wallet  
├─ Historial Financiero  
└─ Reportar Depósito

Notificaciones

Incidencias  
├─ Crear Incidencia  
└─ Detalle Incidencia

Perfil

---

## **ADMINISTRACIÓN**

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

# **CAPA 4 — ESTADOS**

## **Driver**

OFFLINE  
ONLINE  
BUSY  
SUSPENDED

## **Route**

BUILDING  
CLOSED  
ACTIVE  
FINISHED  
CANCELLED

## **Booking**

CREATED  
ACCEPTED  
CONFIRMED  
PICKED\_UP  
DELIVERED  
ABSENT  
CANCELLED

## **Wallet**

ACTIVE  
LOW\_BALANCE  
RESTRICTED

## **Topup Request**

PENDING  
APPROVED  
REJECTED

## **Incident**

OPEN  
IN\_REVIEW  
WAITING\_FOR\_DRIVER  
RESOLVED  
REJECTED

## **Notification**

UNREAD  
READ

---

# **CAPA 5 — ENTIDADES**

## **Operación**

DRIVERS  
VEHICLES  
PASSENGERS

ROUTES  
BOOKINGS  
ROUTE\_EVENTS

RATINGS

## **Comunicación**

NOTIFICATIONS

## **Incidencias**

INCIDENTS  
INCIDENT\_MESSAGES

## **Finanzas**

WALLETS  
TRANSACTIONS  
TOPUP\_REQUESTS

## **Administración**

ADMIN\_USERS  
SYSTEM\_SETTINGS

---

# **CAPA 6 — INTEGRACIONES**

## **Backend**

Supabase

## **Frontend**

React Native  
Expo

## **Estado y Datos**

Zustand  
React Query  
Supabase Realtime

## **Mapas**

react-native-maps  
expo-location

## **Comunicación**

Push Notifications  
WhatsApp  
Llamadas Telefónicas

## **Observabilidad**

Analytics  
Crash Reporting

---

# **Lo que detecto que todavía no está formalmente modelado**

Hay 4 áreas que aparecen en las pantallas pero no tienen todavía una definición arquitectónica propia:

### **Perfil del Conductor**

Datos personales  
Vehículo  
Documentos  
Configuración  
Privacidad

### **Perfil del Pasajero**

Datos personales  
Preferencias  
Calificaciones  
Configuración  
Privacidad

### **Roles Administrativos**

Super Admin  
Operaciones  
Finanzas  
Soporte

### **Configuración Global**

Comisión por pasajero

Saldo mínimo operativo

Parámetros operativos

Parámetros financieros

Parámetros de seguridad

---

