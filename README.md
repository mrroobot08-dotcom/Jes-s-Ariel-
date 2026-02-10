1) ¿Qué pasa hoy?
Hoy se presentan filas largas, demoras, errores en pedidos y entregas desordenadas. Esto genera que los usuarios tengan que esperar mucho tiempo para recibir su alimento o café, y además se incrementa la probabilidad de confusiones al momento de preparar o entregar.
2) En mi opinión, ¿por qué pasa?
En mi opinión, esto ocurre porque varios procesos siguen siendo manuales (tomar pedidos, organizar turnos, confirmar pagos, etc.). Al no estar digitalizados, se pierde tiempo, se cometen errores y se vuelve más difícil mantener el orden cuando hay mucha demanda.
Un problema muy visible es que los pagos son solo en efectivo, lo cual retrasa el proceso y limita a los usuarios que quieren pagar de forma digital.
3) ¿Qué aporte o solución propondrías?
Un aporte eficiente sería implementar una solución donde cualquier persona pueda hacer su pedido desde su dispositivo, pagar directamente de forma digital y además seleccionar un horario estimado o turno para pasar por su compra ayudaría mucho., Reducir filas y tiempos de espera, Disminuir errores en pedidos, Organizar mejor la atención y la entrega, Agilizar el proceso de pago.
4) ¿Qué se necesita?
Se necesita un sistema que permita:
•	Seleccionar productos (menú digital)
•	Agregar al carrito
•	Confirmar el pedido
•	Elegir un horario o turno de recogida ( 10, 15  minutos” o seleccionar una hora específica)
•	Pagar digitalmente
•	Y que el cafetín pueda gestionar estados del pedido junto con el tiempo estimado 
(Recibido, en preparación, listo para recoger (hora/turno) ,entregado)

OBJETIVO GENERAL
Construir e implementar un sistema digital de pedidos y pagos para el cafetín, que permita a los usuarios seleccionar productos desde su dispositivo, pagar en línea y programar un tiempo de recogida, con el fin de reducir filas, disminuir errores y optimizar la gestión y entrega de los pedidos.

Paso 4: Alcance 
Catálogo de productos, Carrito (agregar, quitar, cantidades), Confirmar pedido (genera código), Panel cafetín: ver pedidos y cambiar estado
Incluye
F-1
•  Menú, Carrito, Confirmación de pedido., Panel cafetín  ver pedidos y cambiar estado., Control básico de productos.

F2

Pagos en línea (pasarela: Wompi/PayU/MercadoPago), Facturación (generación de factura/recibo), Inventario avanzado (entradas/salidas, alertas, kardex básico),Usuarios y roles completos (cliente, cajero, administrador)

F3
•  App móvil nativa  Tipo de celulares
•  Notificaciones push
•  Analítica/reportes 



Pagos
•	RF11 (método de pago): El usuario elige efectivo o pago en línea.
•	RF12 (pasarela de pago): Si elige en línea, el sistema lo manda a una pasarela realiza el cobro.
•	RF13 (resultado del pago): El sistema guarda el estado del pago: aprobado / rechazado / pendiente.
•	RF14 (bloqueo de entrega por pago pendiente): Si el pago está pendiente, el sistema no deja confirmar la entrega (cuando aplique).
Facturación
•	RF15 (generar factura/comprobante): Cuando un pedido queda pagado, el sistema genera su factura o comprobante.
•	RF16 (consultar/descargar facturas): Se puede buscar facturas por fecha o por pedido y descargarlas.
•	RF17 (guardar datos de facturación): La factura guarda datos mínimos: cliente, NIT/CC opcional, total, e impuestos si aplican.
Facturación
•	RF15 (generar factura/comprobante): Cuando un pedido queda pagado, el sistema genera su factura o comprobante.
•	RF16 (consultar/descargar facturas): Se puede buscar facturas por fecha o por pedido y descargarlas.
•	RF17 (guardar datos de facturación): La factura guarda datos mínimos: cliente, NIT/CC opcional, total, e impuestos si aplican.
Inventario avanzado
•	RF18 (stock por producto): Cada producto tiene un número de unidades disponibles (stock).
•	RF19 (descontar stock por regla): El sistema resta stock cuando el pedido se confirma (o cuando pasa a “Preparando”, según la regla que definan).
•	RF20 (movimientos de inventario): Cada cambio de stock queda registrado como entrada / salida / ajuste.
•	RF21 (alerta de stock bajo): Si el stock baja de un mínimo, el sistema lanza alerta (para reponer).
•	RF22 (proveedores y compras – fase 2): (Opcional) Permite registrar proveedores y compras para subir stock con trazabilidad.

App móvil nativa
•	RF23 (login y sesión): La app permite iniciar sesión y mantener la sesión activa.
•	RF24 (pedidos desde el celular): Desde la app el usuario puede crear pedidos (igual que en web).
•	RF25 (notificaciones): La app envía notificaciones cuando el pedido cambia de 
•	estado (Preparando”, “En camino”, “Entregado).
•	




RNF06 Seguridad de pagos
•	Cuando se procesa un pago en línea, el sistema usa tokens de la pasarela y no almacena datos sensibles de tarjeta.
RNF07 Integridad
•	Cuando una factura ya fue generada, el sistema no permite editarla; solo permite anularla dejando registro.
RNF08 Trazabilidad
•	Cuando ocurre un movimiento de inventario, el sistema guarda auditoría: qué cambió, quién lo hizo, cuándo y por qué.
RNF09 Disponibilidad y tolerancia a fallos
•	Cuando hay fallos de red/timeout en pagos, el sistema maneja reintentos, estados intermedios (pendiente) y reconciliación sin duplicar cobros.




No funcionales (RNF)

RNF06 Seguridad de pagos
•	Cuando se procesa un pago en línea, el sistema usa tokens de la pasarela y no almacena datos sensibles de tarjeta.
RNF07 Integridad
•	Cuando una factura ya fue generada, el sistema no permite editarla; solo permite anularla dejando registro.
RNF08 Trazabilidad
•	Cuando ocurre un movimiento de inventario, el sistema guarda auditoría: qué cambió, quién lo hizo, cuándo y por qué.
RNF09 Disponibilidad y tolerancia a fallos
•	Cuando hay fallos de red/timeout en pagos, el sistema maneja reintentos, estados intermedios (pendiente) y reconciliación sin duplicar cobros.
RNF-10 Usabilidad
El sistema debe contar con una interfaz intuitiva, clara y fácil de navegar, de manera que cualquier usuario pueda utilizarlo correctamente desde el primer uso, sin necesidad de capacitación previa.

RNF-11Rendimiento
El sistema debe procesar y responder a las acciones del usuario de forma rápida y eficiente, garantizando tiempos de respuesta adecuados que no afecten la experiencia del usuario ni retrasen la realización de pedidos.




Reglas de negocio (RN)
RN06
•	Cuando se intenta generar factura, el sistema solo la genera si el pago está aprobado o si el efectivo fue confirmado.
RN07
•	Cuando un pedido ya está pagado, el sistema bloquea cambios que alteren el total (productos, cantidades, descuentos).
RN08
•	Cuando se intenta confirmar un pedido y no hay stock suficiente, el sistema impide la operación para evitar stock negativo.
RN09
•	Cuando se registra un movimiento de inventario, el sistema exige tipo, fecha y responsable (si falta algo, no deja guardar).
RN10
•	Cuando se anula una factura, el sistema solicita motivo, marca la factura como anulada y conserva el historial completo.
