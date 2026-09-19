

# **DOCUMENTO MAESTRO DE RUTA ACTIVA v1.0**

## **1\. Objetivo**

Ruta Activa es el centro operacional del conductor.

Su objetivo es permitir que el conductor ejecute una ruta previamente construida, gestionando:

* Recogidas.  
* Ausencias.  
* Cancelaciones.  
* Navegación.  
* Entregas.  
* Cobros.  
* Calificaciones.

Toda la operación debe realizarse desde una única pantalla principal que cambia de estado según el momento operativo.

---

# **2\. Actores**

## **Conductor**

Responsable de ejecutar la ruta.

Puede:

* Seleccionar la siguiente parada.  
* Navegar hacia ella.  
* Confirmar llegadas.  
* Confirmar abordajes.  
* Marcar ausencias.  
* Confirmar cobros.  
* Calificar pasajeros.

---

## **Pasajero**

Recibe:

* Notificación de conductor asignado.  
* Notificación de llegada.  
* Notificación de cancelación.  
* Notificación de penalidad.  
* Confirmación de finalización.

---

## **Sistema**

Responsable de:

* Mantener estados.  
* Actualizar la ruta.  
* Gestionar penalidades.  
* Enviar notificaciones.  
* Registrar eventos.

---

# **3\. Filosofía Operacional**

Tixi NO funciona como Uber Pool.

La lógica aprobada es:

Primero recoger pasajeros  
↓  
Después entregar pasajeros

Por tanto la ruta tiene dos fases claramente diferenciadas.

---

# **4\. Fase 1 — Recolección**

Objetivo:

Completar la ocupación de la ruta.

Estados posibles:

* Pendiente recoger.  
* En navegación.  
* Llegó.  
* Esperando.  
* A bordo.  
* Ausente.  
* Cancelado.

---

# **5\. Fase 2 — Distribución**

Comienza cuando ya no existen recogidas pendientes.

Objetivo:

Completar los trayectos.

Estados posibles:

* Pendiente entregar.  
* En navegación.  
* Llegó a destino.  
* Cobro pendiente.  
* Completado.

---

# **6\. Regla Fundamental de Navegación**

El sistema genera una ruta sugerida.

Sin embargo:

> El conductor tiene control total sobre el orden operativo.

Puede seleccionar cualquier parada pendiente.

Ejemplos:

### **Recogidas**

Juan  
María  
Pedro

Puede decidir:

Pedro  
↓  
Juan  
↓  
María

---

### **Destinos**

Juan  
María  
Pedro

Puede decidir:

María  
↓  
Pedro  
↓  
Juan

---

# **7\. Estados de una Solicitud**

## **Pending Pickup**

Pendiente de recogida.

---

## **Arrived**

Conductor llegó.

---

## **Waiting**

Esperando pasajero.

Temporizador:

3 minutos.

---

## **On Board**

Pasajero abordó.

---

## **No Show**

Ausente.

Penalidad:

DOP 100\.

---

## **Cancelled**

Cancelado por pasajero.

---

## **Pending Dropoff**

Pendiente de entrega.

---

## **Arrived Destination**

Llegó al destino.

---

## **Payment Pending**

Esperando cobro.

---

## **Completed**

Finalizado.

---

# **8\. Máquina de Estados**

## **Recogida exitosa**

Pending Pickup  
↓  
Arrived  
↓  
Waiting  
↓  
On Board  
↓  
Pending Dropoff

---

## **Ausencia**

Pending Pickup  
↓  
Arrived  
↓  
Waiting  
↓  
No Show  
↓  
Penalidad  
↓  
Eliminado de la ruta

---

## **Cancelación**

Pending Pickup  
↓  
Cancelled  
↓  
Eliminado de la ruta

---

## **Entrega normal**

Pending Dropoff  
↓  
Arrived Destination  
↓  
Payment Pending  
↓  
Completed

---

# **9\. Eventos del Sistema**

## **Evento: Llegué**

Puede activarse:

### **Manual**

Botón:

Llegué

---

### **Automático**

Geocerca:

50 metros.

---

## **Evento: Abordó**

Activación manual.

Botón:

Pasajero abordó

---

## **Evento: Ausente**

Activación manual.

Botón:

Ausente

Requiere confirmación.

---

## **Evento: Cobro confirmado**

Activación manual.

Botón:

Confirmar cobro

---

## **Evento: Finalización manual**

Permite terminar un trayecto antes del destino programado.

Condición:

Cobro completo obligatorio.

---

# **10\. Casos Borde**

## **Llegué por error**

Solución:

Botón:

Cancelar llegada

Disponible durante 60 segundos.

---

## **Pasajero cancela durante la ruta**

Acciones:

* Eliminar parada.  
* Recalcular sugerencia.  
* Notificar conductor.  
* Aplicar penalidad.

---

## **Conductor pierde conexión**

La pantalla debe continuar operativa con caché local.

Al recuperar conexión:

Sincronización automática.

---

## **GPS perdido**

Mostrar:

Ubicación no disponible

Permitir continuar operación manual.

---

## **Cierre accidental de la app**

Al abrir nuevamente:

Retomar Ruta Activa

---

# **11\. Información que debe mostrar Ruta Activa**

## **Bloque 1**

Mapa.

---

## **Bloque 2**

Resumen de ruta.

* Pasajeros abordados.  
* Pasajeros pendientes.  
* Pasajeros completados.  
* Ganancia acumulada.  
* Ganancia proyectada.

---

## **Bloque 3**

Paradas pendientes.

Recogidas y destinos.

---

## **Bloque 4**

Próxima parada seleccionada.

* Tipo.  
* Nombre.  
* Dirección.  
* ETA.  
* Distancia.

---

## **Bloque 5**

Acción principal.

Ejemplos:

Llegué

Pasajero abordó

Ausente

Confirmar cobro

---

# **12\. Arquitectura Visual Recomendada**

┌───────────────────────┐  
│        MAPA           │  
└───────────────────────┘

Resumen de ruta

Próxima parada seleccionada

Acción principal

Paradas pendientes

Pasajeros

---

# **13\. Conclusiones de Arquitectura**

Después del análisis, la recomendación es:

### **Mantener una sola pantalla principal**

Ruta Activa.

---

### **No crear pantallas separadas para**

* Llegué.  
* Esperando.  
* Abordó.  
* Ausente.  
* Cobro.  
* Calificación.  
* Destino alcanzado.

---

### **Implementar estados dentro de Ruta Activa**

Esto:

* Reduce navegación.  
* Reduce errores operativos.  
* Facilita la conducción.  
* Simplifica el desarrollo.  
* Mantiene el foco en la operación.

---

### **Próximo paso recomendado**

Antes de abrir Figma, realizar una **auditoría funcional de este documento** para detectar:

1. Casos borde que aún falten.  
2. Información necesaria en cada estado.  
3. Acciones que puedan generar errores.  
4. Reglas de negocio adicionales.

Una vez validado, entonces pasamos a diseñar las variantes visuales de **Ruta Activa** en Figma.

