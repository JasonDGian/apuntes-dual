
# 🔹 Paradigma Canary Release.
El paradigma de canary release es una estrategia de despliegue de software que minimiza el riesgo de introducir nuevas versiones al sistema. En lugar de lanzar una nueva versión a todos los usuarios de una vez, esta técnica permite lanzar la actualización a un pequeño subconjunto de usuarios primero. Si no se detectan problemas, la actualización se despliega gradualmente a más usuarios.

Aquí tienes los pasos principales del proceso de canary release:

Desplegar a una pequeña parte de usuarios: La nueva versión se despliega primero a un grupo reducido de usuarios (el "canario").

Monitorizar: Se monitorean estos usuarios para identificar cualquier problema o error.

Evaluar: Basado en el feedback y los datos recogidos, se decide si la nueva versión es estable.

Despliegue progresivo: Si todo va bien, la versión se despliega gradualmente a más usuarios hasta alcanzar el 100%.

Esta estrategia es especialmente útil en entornos de producción, ya que permite detectar y corregir problemas sin afectar a todos los usuarios simultáneamente.

# 🔹 API REST - Tipificada vs no tipificada.
Una API REST tipificada es una API que sigue ciertas reglas y especificaciones que definen claramente los tipos de datos permitidos en las solicitudes y respuestas. Estas "restricciones" ayudan a garantizar que los datos sean consistentes y correctos, lo que facilita la validación y el desarrollo.

**Ventajas de las APIs Tipificadas:**
- **Consistencia:** Al definir tipos específicos, se asegura que los datos intercambiados sean consistentes.
- **Validación:** Facilita la validación tanto en el cliente como en el servidor.
- **Documentación:** Herramientas como OpenAPI generan documentación detallada automáticamente.
- **Desarrollo más Seguro:** Reduce la posibilidad de errores durante el desarrollo.

**Limitaciones:**
- **Menos Flexibilidad:** Las restricciones pueden limitar la flexibilidad en el manejo de datos.
- **Mayor Esfuerzo Inicial:** Requiere un esfuerzo adicional para definir y mantener la especificación.

Por otro lado, una API no tipificada ofrece más flexibilidad, pero a costa de potenciales problemas de consistencia y validación de datos.

Ambas enfoques tienen sus ventajas y desventajas, y la elección depende de las necesidades específicas del proyecto.

---

Una API REST no tipificada ofrece más flexibilidad, pero a costa de potenciales problemas de consistencia y validación de datos.

**Ventajas de las APIs No Tipificadas:**
- **Flexibilidad:** Permite manejar datos de manera más libre, sin restricciones estrictas sobre los tipos de datos.
- **Simplicidad Inicial:** Puede ser más rápida de implementar inicialmente, ya que no requiere definir y mantener una especificación de tipos.
- **Adaptabilidad:** Se adapta fácilmente a cambios en los datos sin necesidad de modificar una especificación estricta.

**Limitaciones:**
- **Inconsistencia:** La falta de una especificación clara puede llevar a datos inconsistentes o incorrectos.
- **Validación:** La validación de datos puede ser más débil, aumentando el riesgo de errores en tiempo de ejecución.
- **Documentación:** La documentación puede ser menos precisa y detallada, lo que puede causar confusión entre los desarrolladores.

En resumen, una API no tipificada ofrece mayor flexibilidad en el manejo de datos, pero a costa de una mayor posibilidad de errores y problemas de consistencia. La elección entre una API tipificada y una no tipificada depende de las necesidades específicas y prioridades del proyecto.

## 🔸 Cuando tipificar y cuando no.
En resumen, la elección de usar APIs tipificadas o no tipificadas depende de los requisitos específicos de flexibilidad, consistencia y velocidad de desarrollo de cada tipo de microservicio. Los microservicios de arquitectura pueden priorizar la flexibilidad para integrarse con diversos sistemas, mientras que los microservicios de aplicación pueden priorizar la consistencia y la validación para asegurar la precisión y la integridad de los datos.

# 🔹 
