  ---
   
Arquitectura Multi-tenant (multi inquilinos)

Este diseño lógico y físico de una app en la nube está pensado para compartirse entre múltiples clientes (tenants) mediante una suscripción periódica, garantizando seguridad, aislamiento de datos y alta escalabilidad.

- **Capa de cliente (frontend)**: interfaz web o móvil de acceso rápido mediante navegadores, optimizada con redes de distribución de contenido (CDN).
- **Puerta de enlace (API Gateway)**: Punto de entrada único que enruta peticiones, maneja el control de acceso y detecta el identificador de cada *tenant*
- **Capa de lógica (backend)**: Servicios modulares o microservicios que procesan las reglas de negocio de forma independiente.
- **Capa de Datos (Base de datos)**: Almacenamiento central o distribuido adaptado al modelo de multi-tenencia elegido.

Modelos de multi-tenants
- **Base de datos compartida, esquemas compartidos:** Todos los clientes usan las mismas tablas; un campo `tenant_id` separa los registros. Es económico y fácil de iniciar, pero más complejo de auditar.
- **Base de datos compartida, esquemas separados:** Cada cliente tiene su propio esquema dentro de la misma instancia de base de datos. Ofrece un mejor aislamiento lógico.
- **Base de datos dedicada (Single-tenant):** Cada cliente grande o corporativo posee su propia infraestructura exclusiva por motivos de seguridad estricta o cumplimiento normativo.

**Buenas prácticas de diseño**

- **Seguridad y Aislamiento:** Validar el contexto del _tenant_ en cada petición para evitar filtraciones de datos entre cuentas.

- **Escalabilidad horizontal:** Diseñar los servicios sin estado (_stateless_) para añadir recursos de cómputo de manera automática según la demanda.

- **Observabilidad:** Monitorear logs, métricas y rendimiento por usuario o empresa para detectar cuellos de botella rápidamente. 

![vide](https://www.youtube.com/watch?v=B8qMVVgj0uM&t=332)

