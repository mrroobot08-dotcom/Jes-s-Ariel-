# Carrito de compras para el cafetín del SENA (Industria)

## 1. Planteamiento del problema
En el cafetín del SENA (Industria) se forman **filas largas** y se presentan **demoras** especialmente en horas pico. Además, al tomar pedidos de forma manual pueden ocurrir **errores** (confundir productos o cantidades) y también se vuelve más difícil organizar la **entrega** cuando hay muchos pedidos al tiempo.

Esto pasa principalmente porque el proceso depende de la atención directa en el punto (anotar, cobrar, organizar el turno y entregar). En momentos de alta demanda se acumulan personas, se pierde tiempo y aumenta el riesgo de confusión.

> Nota: en esta primera versión (MVP) me enfoco en el **pedido + turno/tiempo de recogida + estados del pedido**. La integración de **pagos en línea reales** queda para la Fase 2.



## 2. Objetivo general
Construir e implementar un sistema digital de pedidos para el cafetín, que permita a los usuarios seleccionar productos desde su dispositivo, programar un tiempo de recogida y confirmar pedidos con un código único, con el fin de reducir filas, disminuir errores y mejorar la gestión y entrega de los pedidos.



## 3. Objetivos específicos
1. Implementar el flujo mínimo del usuario: **catálogo → carrito → confirmación del pedido**, con cálculo de totales y generación de código.
2. Implementar la selección de **turno/tiempo estimado de recogida** para organizar mejor la entrega.
3. Desarrollar un **panel del cafetín** para ver pedidos y actualizar su estado (Recibido → En preparación → Listo → Entregado).

---

## 4. Alcance

### Incluye (MVP – Fase 1)
- Menú/catálogo de productos.
- Carrito (agregar, quitar, cambiar cantidades).
- Confirmar pedido y generar **código único** (número o QR).
- Selección de **turno/tiempo** (10/15/20 min o una hora).
- Panel del cafetín para ver pedidos y **cambiar estados**.
- Control básico de productos (crear/editar/desactivar).

### No incluye (por ahora – Fase 2 y 3)
- Pasarela de pagos real (Wompi/PayU/MercadoPago).
- Facturación.
- Inventario avanzado (movimientos, alertas, proveedores, kardex).
- App móvil nativa.
- Notificaciones push.
- Reportes/analítica.

---

## 5. Requerimientos

### 5.1 Requerimientos Funcionales (RF) — MVP (Fase 1)
- **RF01:** El usuario puede ver el catálogo de productos.
- **RF02:** El usuario puede ver el detalle del producto (precio y descripción opcional).
- **RF03:** El usuario puede agregar productos al carrito.
- **RF04:** El usuario puede modificar el carrito (cambiar cantidad/eliminar).
- **RF05:** El sistema calcula subtotal y total automáticamente.
- **RF06:** El usuario debe seleccionar un **turno/tiempo** antes de confirmar el pedido.
- **RF07:** El usuario puede confirmar el pedido y el sistema lo registra con sus datos completos.
- **RF08:** Al confirmar el pedido, el sistema genera un **código único**.
- **RF09:** El cafetín puede ver los pedidos en un panel (código, total, turno/tiempo y estado).
- **RF10:** El cafetín puede cambiar el estado del pedido: Recibido → En preparación → Listo → Entregado.

### 5.2 Requerimientos Funcionales (Mejora)
- **RF11:** El usuario puede usar búsqueda o filtros para encontrar productos más rápido.

### 5.3 Requerimientos No Funcionales (RNF)
- **RNF01 (Usabilidad):** La interfaz debe ser clara y fácil de entender desde el primer uso.
- **RNF02 (Rendimiento):** El sistema debe responder rápido al navegar, modificar el carrito y confirmar pedidos.
- **RNF03 (Disponibilidad):** Debe funcionar durante el horario del cafetín.
- **RNF04 (Seguridad básica):** El panel del cafetín debe estar protegido (al menos con acceso básico).
- **RNF05 (Integridad):** Si un pedido ya está “Entregado”, no debe poder modificarse.

### 5.4 Reglas de negocio (RN)
- **RN01:** Cuando se confirma un pedido, inicia en estado **“Recibido”**.
- **RN02:** No se puede confirmar un pedido sin seleccionar turno/tiempo.
- **RN03:** El código del pedido debe ser único.
- **RN04:** Estados permitidos: Recibido → En preparación → Listo → Entregado.
- **RN05:** El panel del cafetín debe mostrar el turno/tiempo para organizar mejor la preparación.

---

## 6. Priorización MoSCoW (MVP con turno/tiempo)
**Must (sí o sí en el MVP):**
- Catálogo
- Carrito
- Confirmar pedido
- Código del pedido
- Turno/tiempo
- Panel cafetín
- Cambio de estado

**Should (si hay tiempo):**
- Búsqueda/filtros

**Could (más adelante):**
- Historial de pedidos
- Favoritos

**Won’t (por ahora):**
- Pagos en línea reales
- Facturación
- Inventario avanzado
- App nativa
- Notificaciones push
- Reportes/analítica

---

## 7. Mockup inicial (baja fidelidad)
Para cumplir el entregable, dejé el mockup en la carpeta:

- `/docs/mockups/mockup.jpg` *(o link si lo hice en Figma/draw.io)*

Pantallas mínimas:
1) Catálogo  
2) Carrito + turno/tiempo  
3) Confirmación (código)  
4) Panel cafetín (lista + estados)

---

## 8. Backlog / Plan de trabajo (Historias de usuario)
> Estimación: **S / M / L**

- **HU01 (S):** Como usuario quiero ver el catálogo para elegir productos.  
  **Criterios:** lista con nombre/precio, solo activos, botón agregar.

- **HU02 (S):** Como usuario quiero ver el detalle del producto para decidir.  
  **Criterios:** nombre, precio, descripción opcional, disponibilidad.

- **HU03 (S):** Como usuario quiero agregar productos al carrito para armar mi pedido.  
  **Criterios:** se agrega y aumenta cantidad si repito producto.

- **HU04 (S):** Como usuario quiero cambiar cantidades o eliminar productos del carrito.  
  **Criterios:** total se actualiza, no cantidades menores a 1.

- **HU05 (S):** Como usuario quiero ver el total calculado del pedido.  
  **Criterios:** subtotal por item y total general.

- **HU06 (M):** Como usuario quiero seleccionar un turno/tiempo para organizar la recogida.  
  **Criterios:** obligatorio antes de confirmar, se guarda en pedido.

- **HU07 (M):** Como usuario quiero confirmar el pedido para que el cafetín lo reciba.  
  **Criterios:** crea pedido con estado “Recibido”.

- **HU08 (M):** Como usuario quiero un código del pedido para reclamarlo.  
  **Criterios:** código único visible y almacenado.

- **HU09 (M):** Como cafetín quiero ver pedidos en un panel para prepararlos.  
  **Criterios:** muestra código, turno/tiempo, total, estado.

- **HU10 (M):** Como cafetín quiero cambiar el estado del pedido para controlar el proceso.  
  **Criterios:** respeta flujo de estados, se actualiza en el panel.

- **HU11 (S):** Como usuario quiero buscar o filtrar productos para encontrarlos rápido.  
  **Criterios:** buscar por nombre, filtro por categoría si existe.

---

## 9. Modelo de datos (propuesto)

### Relaciones
- **Producto (1) → (N) DetallePedido**
- **Pedido (1) → (N) DetallePedido**

### Producto
- id (PK)
- nombre
- descripcion (opcional)
- precio
- activo (boolean)
- stock (opcional)
- created_at

### Pedido
- id (PK)
- codigo (único)
- fecha_hora
- turno_tiempo
- estado (RECIBIDO / PREPARANDO / LISTO / ENTREGADO)
- total
- cliente_nombre (opcional)

### DetallePedido
- id (PK)
- pedido_id (FK)
- producto_id (FK)
- cantidad
- precio_unitario
- subtotal

---

## 10. Estructura sugerida del repositorio
- `README.md`
- `docs/mockups/` (mockup en imagen o link)
- `docs/backlog.md` (opcional)
- `docs/modelo_datos.md` (opcional)
- `backend/` y `frontend/` (si se implementa)

