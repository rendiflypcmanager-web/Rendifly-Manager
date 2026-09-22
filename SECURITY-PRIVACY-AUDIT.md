# Auditoría actual de privacidad, protección de datos, seguridad y documentación  
## Rendifly Manager — estado posterior a las mejoras de Beta 2

**Fecha de revisión:** 21 de septiembre de 2026  
**Alcance:** implementación actual del proyecto Rendifly Manager.  
**Modo:** auditoría de solo lectura. No se modificó ningún archivo durante esta revisión.  
**Criterio:** cuando existe una diferencia entre la documentación y el código, prevalece el comportamiento real de la implementación.

---

# 1. Resumen del estado actual

Rendifly Manager funciona actualmente como una aplicación local de Windows.

## Funciones activas

Actualmente están activas las siguientes funciones:

- Monitorización local del equipo.
- Lectura de CPU, RAM, GPU, almacenamiento y batería.
- Lectura de procesos activos.
- Lectura de aplicaciones de inicio.
- Lectura de controladores y configuraciones de Windows.
- Lectura de contadores globales de red.
- Gestión local de preferencias.
- Almacenamiento de configuración en `%APPDATA%\Rendifly`.
- Logs locales rotatorios.
- Historial local de notificaciones.
- Gestión del inicio automático mediante el registro de Windows.
- Funciones de limpieza y optimización.
- Gestión y finalización de procesos.
- Apertura controlada de configuraciones y sitios externos.
- Feedback mediante el cliente de correo del usuario o Gmail.

## Funciones desactivadas actualmente

La IA externa está desactivada mediante:

`feature_flags.py`

```python
EXTERNAL_AI_ENABLED = False
```

Mientras esta bandera permanezca desactivada, el flujo normal no debería:

- Validar API keys externas.
- Conectarse a Gemini.
- Conectarse a proveedores compatibles con OpenAI.
- Enviar preguntas del usuario a terceros.
- Enviar contexto del equipo a proveedores de IA.
- Ejecutar búsquedas web automáticas mediante DuckDuckGo.

## Funciones preparadas para el futuro

El código contiene infraestructura para:

- Google Gemini.
- Proveedores compatibles con OpenAI.
- Búsqueda web con DuckDuckGo.
- Contexto técnico del equipo para el asistente.
- Validación de endpoints HTTPS.
- Consentimiento separado para IA.
- Protección de API keys mediante Windows DPAPI.

Estas funciones están preparadas, pero no están disponibles en el flujo normal actual porque la integración externa permanece desactivada.

---

# 2. Política de privacidad

## 2.1 Qué hace realmente el código

La aplicación no utiliza actualmente:

- Sistema de cuentas.
- Backend propio de usuarios.
- Base de datos remota.
- Servicio propio de analítica.
- SDK de publicidad.
- Servicio propio de telemetría.
- Servidor HTTP público de Rendifly.

La aplicación procesa localmente información técnica del equipo y guarda determinados datos en el perfil del usuario.

La recopilación local se realiza principalmente en:

- `monitor.py`
- `metrics.py`
- `hardware/`
- `manager.py`
- `config.py`

La aplicación puede leer información del sistema, mostrarla en la interfaz y utilizarla internamente para recomendaciones y funciones de optimización.

## 2.2 Documentación existente

Actualmente existen:

- `PRIVACY.md`
- `TERMS.md`
- `LICENSE`
- `THIRD-PARTY-NOTICES.md`

La política de privacidad describe que:

- La aplicación funciona principalmente de forma local.
- Los datos técnicos normalmente permanecen en el equipo.
- No existe telemetría centralizada activa.
- La IA externa está desactivada en la versión actual.
- El feedback puede utilizar proveedores externos de correo.

## 2.3 Diferencias entre documentación e implementación

La documentación coincide con la arquitectura local actual.

Sin embargo, `PRIVACY.md` todavía contiene placeholders para:

- Nombre del responsable.
- Correo de privacidad.
- Fecha de entrada en vigor.
- Revisión legal.
- Información específica de jurisdicción.

Por tanto, la documentación es técnicamente coherente, pero todavía no está lista para una distribución pública definitiva.

## 2.4 Qué falta

Falta completar:

- Nombre real del responsable.
- Organización responsable.
- Correo de privacidad.
- Fecha de entrada en vigor.
- Jurisdicción.
- Política de retención.
- Derechos del usuario.
- Procedimiento de acceso.
- Procedimiento de eliminación.
- Procedimiento de exportación.
- Información completa sobre el feedback recibido por correo.
- Revisión legal para los mercados donde se distribuya la aplicación.

## 2.5 Riesgos

- El usuario no tiene todavía un contacto real para ejercer derechos.
- La política no define completamente los plazos de retención.
- La política futura de IA podría quedarse obsoleta si se activa la funcionalidad sin actualizar la documentación.
- La política no debe publicarse con los placeholders actuales.

**Prioridad:** Alta antes de la distribución pública.

## 2.6 Solución recomendada

Completar `PRIVACY.md` con información real sobre:

1. Responsable del tratamiento.
2. Contacto.
3. Datos recopilados.
4. Finalidad.
5. Base legal, cuando corresponda.
6. Retención.
7. Eliminación.
8. Proveedores externos.
9. Transferencias internacionales.
10. Derechos del usuario.
11. Fecha de vigencia.
12. Historial de cambios.

---

# 3. EULA, términos de uso y licencia

## 3.1 Qué hace realmente el código

La aplicación contiene funciones que pueden:

- Consultar hardware.
- Consultar procesos.
- Finalizar procesos.
- Limpiar archivos.
- Modificar configuraciones de inicio.
- Consultar y modificar opciones de energía.
- Consultar configuraciones de Windows.
- Abrir configuraciones del sistema.
- Abrir sitios externos autorizados.
- Gestionar perfiles.
- Preparar feedback.
- Configurar proveedores de IA en futuras versiones habilitadas.

No existe actualmente un sistema que obligue al usuario a aceptar términos antes de abrir la aplicación o usar sus funciones.

## 3.2 Documentación existente

Existe:

- `LICENSE`
- `TERMS.md`

El instalador referencia ambos documentos mediante:

`RendiflyManager.iss`

```ini
LicenseFile=..\LICENSE
InfoBeforeFile=..\TERMS.md
```

## 3.3 Coincidencia

La licencia MIT está presente como archivo distribuible.

Los términos de uso existen, pero todavía son un borrador porque contienen placeholders para:

- Propietario.
- Contacto legal.
- Fecha.
- Jurisdicción.
- Condiciones legales específicas.

## 3.4 Qué falta

Falta completar:

- Identidad legal del propietario.
- Contacto legal.
- Jurisdicción aplicable.
- Condiciones de la versión Beta.
- Responsabilidad del usuario al modificar Windows.
- Condiciones sobre servicios externos.
- Condiciones sobre IA.
- Condiciones sobre feedback.
- Avisos legales de dependencias.

## 3.5 Riesgos

- El instalador puede mostrar documentos todavía incompletos.
- No quedan definidas completamente las responsabilidades sobre limpieza o finalización de procesos.
- La versión Beta no tiene todavía un marco contractual final.
- El usuario puede interpretar la licencia MIT como sustituto de los términos de uso, aunque cumplen funciones distintas.

**Prioridad:** Alta.

## 3.6 Solución recomendada

Completar `TERMS.md`, revisarlo legalmente y verificar que la versión mostrada por el instalador sea la correcta.

---

# 4. Datos recopilados por la aplicación

## 4.1 Hardware y sistema

La aplicación puede leer localmente:

- CPU.
- Número de núcleos.
- Número de hilos.
- Uso de CPU.
- RAM total.
- RAM utilizada.
- GPU.
- Información de `nvidia-smi`, cuando está disponible.
- Sistema operativo.
- Tiempo de actividad.
- Temperaturas.
- Estado de batería.
- Capacidad de batería.

Archivos relacionados:

- `monitor.py`
- `cpu.py`
- `gpu.py`
- `battery.py`
- `ram.py`

## 4.2 Almacenamiento

La aplicación puede leer:

- Letras de unidad.
- Capacidad.
- Espacio libre.
- Uso de almacenamiento.
- Lecturas.
- Escrituras.

Archivos relacionados:

- `storage.py`
- `monitor.py`

## 4.3 Procesos y software

La aplicación puede leer:

- Procesos activos.
- Nombres de procesos.
- Consumo de memoria.
- Estado de procesos.
- Aplicaciones de inicio.
- Información de controladores.
- Algunas configuraciones de Windows.

Archivos relacionados:

- `manager.py`
- `startup.py`
- `drivers.py`
- `windows_config.py`

## 4.4 Red

La aplicación puede leer contadores globales agregados:

- Bytes enviados.
- Bytes recibidos.

No se confirmó que lea:

- Contenido de paquetes.
- Historial de navegación.
- Dominios visitados.
- Contenido de comunicaciones.
- Todas las direcciones de destino.

Archivos relacionados:

- `network.py`
- `metrics.py`

## 4.5 Datos introducidos por el usuario

La aplicación puede recibir:

- Nombre introducido durante el onboarding.
- Preferencias.
- Idioma.
- Tema.
- Color.
- Preferencias de monitorización.
- Configuración de notificaciones.
- Configuración del asistente.
- Texto escrito en feedback.
- Nombre de una captura seleccionada.
- Preguntas del asistente.

## 4.6 Coincidencia documental

La documentación describe de forma general la monitorización de CPU, RAM, GPU, disco y batería.

No enumera de forma completa:

- Procesos.
- Aplicaciones de inicio.
- Controladores.
- Contadores de red.
- Temperaturas.
- Consultas a `nvidia-smi`.
- Todos los datos que formarían parte del contexto de IA si se habilitara.

**Prioridad:** Media para el uso local.  
**Prioridad:** Alta si estos datos se envían a terceros.

## 4.7 Solución recomendada

Añadir una tabla formal de inventario:

| Categoría | Datos | Finalidad | Persistencia | Sale del equipo actualmente |
|---|---|---|---|---|
| Hardware | CPU, RAM, GPU, batería | Mostrar el estado del equipo | Principalmente memoria | No |
| Almacenamiento | Capacidad y espacio libre | Mostrar uso del disco | Principalmente memoria | No |
| Procesos | Nombre y memoria | Gestión y explicación | Memoria y posibles logs | No |
| Configuración | Preferencias y estado | Personalización | JSON local | No |
| Feedback | Tipo, detalle y texto | Soporte | Cliente de correo | Solo si el usuario envía |
| IA externa | Pregunta y contexto técnico | Respuesta externa | Según proveedor | Desactivado actualmente |

---

# 5. Datos almacenados localmente

## 5.1 Ubicación

La aplicación utiliza:

```text
%APPDATA%\Rendifly
```

La persistencia se gestiona mediante:

- `app.py`
- `persistence.py`

## 5.2 Archivos identificados

El código utiliza los siguientes archivos:

- `settings.json`
- `runtime.json`
- `notification_history.json`
- `rendifly.log`
- Backups rotatorios de los logs.
- Archivos temporales utilizados para guardado atómico.

## 5.3 Datos almacenados

Puede almacenarse:

- Nombre del usuario.
- Preferencias.
- Idioma.
- Tema.
- Color.
- Inicio automático.
- Inicio minimizado.
- Preferencias de bandeja.
- Intervalos de monitorización.
- Notificaciones.
- Perfiles.
- Estado de onboarding.
- Estado del proveedor de IA.
- Estado de validación.
- Consentimiento de IA.
- API key protegida mediante DPAPI.
- Historial de notificaciones.
- Errores y trazas de aplicación.

## 5.4 Protección de la API key

La API key se protege mediante Windows DPAPI en:

`config.py`

La API key protegida no se devuelve a la interfaz en:

`api.py`

La configuración utiliza escritura temporal y sustitución atómica en:

`persistence.py`

## 5.5 Eliminación de datos

Existe una función para borrar datos locales:

`config.py`

También existe una API expuesta:

`api.py`

La función intenta eliminar los archivos del directorio de datos y restablecer la configuración en memoria.

## 5.6 Limitaciones

La eliminación local:

- No es borrado seguro de bajo nivel.
- No puede eliminar copias de seguridad externas.
- No puede eliminar backups del sistema operativo.
- Puede dejar archivos bloqueados si se produce un error.
- No establece ACL personalizadas.
- No cifra todos los logs ni todos los archivos de configuración.

**Prioridad:** Media.

## 5.7 Solución recomendada

Documentar:

- Cada archivo.
- Su finalidad.
- Retención.
- Forma de eliminación.
- Dependencia de DPAPI.
- Limitaciones de borrado.
- Comportamiento al desinstalar.
- Comportamiento al conservar datos durante una actualización.

---

# 6. Datos enviados a Internet

## 6.1 Servicios propios

No se encontró:

- Servidor HTTP propio.
- API central de Rendifly.
- Base de datos remota.
- Sistema de cuentas.
- Servicio de analítica.
- Servicio propio de telemetría.

## 6.2 Destinos externos presentes en el código

El código contiene referencias a:

- Google Gemini.
- Proveedores compatibles con OpenAI.
- DuckDuckGo HTML.
- Gmail.
- Cliente de correo mediante `mailto:`.
- Sitios oficiales de Microsoft.
- Sitios de fabricantes.
- URIs de configuración de Windows.

Archivos relacionados:

- `provider.py`
- `gemini_client.py`
- `openai_client.py`
- `api.py`

## 6.3 Estado actual de la IA

La integración externa está bloqueada por:

`feature_flags.py`

Cuando está desactivada, las funciones de configuración y validación responden con un estado equivalente a `coming_soon`.

Actualmente no debería producirse:

- Envío de preguntas a Gemini.
- Envío de preguntas a OpenAI-compatible.
- Envío de hardware a proveedores externos.
- Envío de procesos.
- Búsquedas web automáticas.

## 6.4 Feedback por Internet

El feedback no se envía a un servidor propio de Rendifly.

La aplicación prepara:

- Un mensaje `mailto:`.
- Una composición de Gmail.

El usuario debe revisar y enviar manualmente el mensaje.

## 6.5 Riesgos futuros

Si se activa la IA sin controles adicionales, podrían enviarse:

- Preguntas del usuario.
- Contexto de hardware.
- Sistema operativo.
- Procesos.
- RAM.
- Discos.
- Batería.
- Temperaturas.
- Métricas del equipo.

Aunque el código ya separa validación y consentimiento, antes de activar la función debe verificarse toda la experiencia visual de consentimiento.

**Prioridad:** Alta antes de activar IA.  
**Prioridad:** Media mientras la IA permanezca desactivada.

## 6.6 Solución recomendada

Antes de activar la IA:

- Mantenerla desactivada por defecto.
- Mostrar un aviso específico.
- Mostrar el proveedor.
- Mostrar el endpoint.
- Mostrar el modelo.
- Mostrar las categorías que se enviarán.
- Permitir enviar solo la pregunta.
- Permitir desactivar contexto de procesos.
- Permitir desactivar contexto de hardware.
- Permitir desactivar contexto de almacenamiento.
- Documentar retención.
- Documentar transferencias internacionales.
- Documentar uso de datos por los proveedores.
- Mostrar enlaces a las políticas externas.

---

# 7. Sistema de feedback

## 7.1 Comportamiento real

El frontend solicita:

- Tipo de problema.
- Detalle.
- Descripción.
- Selección opcional de una captura.

Implementación:

- `feedback.js`
- `api.py`

El cuerpo del correo incluye:

- Tipo de problema.
- Detalle.
- Descripción.
- Nombre de la captura seleccionada.

## 7.2 Capturas

La captura:

- No se lee.
- No se procesa.
- No se adjunta automáticamente.
- No se envía a un servidor.
- Solo se incluye su nombre en el mensaje.

## 7.3 Envío

El usuario puede utilizar:

- Cliente de correo predeterminado.
- Gmail.

El usuario debe revisar y enviar manualmente el mensaje.

## 7.4 Documentación existente

La interfaz indica que los comentarios se utilizan para:

- Análisis.
- Resolución de problemas.
- Mejora de la experiencia.

También recomienda no incluir información personal.

## 7.5 Diferencias documentales

La interfaz no explica claramente:

- Que se abre una aplicación externa.
- Que el mensaje no se envía automáticamente.
- Que la captura no se adjunta.
- Quién recibe el mensaje.
- Cuánto tiempo se conserva.
- Cómo solicitar eliminación.
- Qué datos deben evitarse.

## 7.6 Riesgos

El usuario puede incluir accidentalmente:

- Contraseñas.
- API keys.
- Tokens.
- Rutas locales.
- Nombres de usuario.
- Nombres de archivos privados.
- Información corporativa.
- Datos personales.

**Prioridad:** Media.

## 7.7 Solución recomendada

Mostrar un aviso como:

> Se preparará un correo para `rendiflypcmanager@gmail.com`. El mensaje no se enviará automáticamente. La captura seleccionada no se adjunta actualmente; solo se incluirá su nombre. No incluyas contraseñas, tokens, API keys, información personal ni datos confidenciales.

---

# 8. Logs y diagnósticos

## 8.1 Comportamiento real

Los logs se guardan en:

```text
%APPDATA%\Rendifly\rendifly.log
```

La implementación se encuentra en:

`logging_service.py`

Características:

- Rotación de logs.
- Aproximadamente 5 MB por archivo.
- Hasta tres backups.
- Registro de errores.
- Registro de excepciones.
- Tracebacks completos mediante `exc_info`.

## 8.2 Información que podría aparecer

Según el error, los logs podrían incluir:

- Rutas locales.
- Nombres de archivos.
- Nombres de procesos.
- Módulos.
- Endpoints.
- Detalles del sistema.
- Mensajes de bibliotecas externas.

No se observó logging rutinario de:

- API keys completas.
- Prompts completos.
- Respuestas completas del asistente.
- Contenido de capturas.

## 8.3 Historial de notificaciones

El historial se gestiona en:

`notifications.py`

Puede almacenar:

- Título.
- Mensaje.
- Tipo.
- Icono.
- Fecha.
- Estado de lectura.

## 8.4 Documentación existente

La documentación menciona la ubicación de los logs, pero no define claramente:

- Retención temporal.
- Borrado automático.
- Contenido exacto.
- Redacción.
- Acceso de otros procesos.
- Diferencia entre logs de desarrollo y producción.

## 8.5 Riesgos

La rotación limita el tamaño, pero no establece un periodo temporal de conservación.

Los logs pueden revelar información técnica del equipo a otros procesos que se ejecuten bajo el mismo usuario.

**Prioridad:** Media.

## 8.6 Solución recomendada

- Definir retención por tiempo.
- Redactar rutas.
- Redactar datos sensibles.
- Evitar registrar objetos completos.
- Añadir eliminación desde la interfaz.
- Eliminar todos los backups al borrar datos.
- Añadir pruebas que garanticen que las API keys nunca aparecen en logs.
- Separar logs de desarrollo y producción.

---

# 9. Configuración del usuario

## 9.1 Datos configurables

La configuración puede contener:

- Nombre.
- Preferencias.
- Idioma.
- Tema.
- Color.
- Inicio con Windows.
- Inicio minimizado.
- Minimizar a la bandeja.
- Cerrar a la bandeja.
- Intervalo de monitorización.
- Historial de monitorización.
- Notificaciones.
- Proveedor de IA.
- Estado `validated`.
- Estado `allow_ai`.
- Estado del onboarding.
- Perfiles.
- Runtime.
- `send_diagnostics`.

Evidencia:

`config.py`

## 9.2 Estado de privacidad

La configuración inicial establece:

```python
"allow_ai": False
"send_diagnostics": False
"validated": False
```

El código separa:

- Validación técnica del proveedor.
- Consentimiento para permitir el uso externo.

Esto se implementa en:

- `config.py`
- `api.py`

## 9.3 Riesgos

- El usuario puede no distinguir entre configurar una API key y permitir transferencias.
- `send_diagnostics` existe, pero no se encontró un flujo funcional de envío.
- Las preferencias pueden sobrevivir a una reinstalación.
- Los datos pueden permanecer en backups del sistema operativo.

**Prioridad:** Media.

## 9.4 Solución recomendada

- Mostrar el estado de cada opción.
- Mostrar qué datos se almacenan.
- Mostrar qué datos salen del equipo.
- Añadir exportación.
- Añadir eliminación selectiva.
- Marcar `send_diagnostics` como no disponible mientras no exista su implementación.
- Informar claramente cuando una opción afecta a transferencias externas.

---

# 10. Consentimiento y transparencia

## 10.1 Controles existentes

Actualmente existen:

- `allow_ai=False` por defecto.
- Feature flag global desactivada.
- Función para otorgar consentimiento.
- Función para revocar consentimiento.
- Separación entre `validated` y `allow_ai`.
- Mensaje de funcionalidad futura cuando la IA está desactivada.
- Feedback iniciado manualmente por el usuario.

## 10.2 Aspectos pendientes

No se verificó una pantalla completa que muestre, antes de la primera transferencia:

- Proveedor.
- Endpoint.
- Modelo.
- Categorías de datos.
- Finalidad.
- Retención.
- Transferencias internacionales.
- Enlaces a políticas externas.
- Mecanismo de revocación.

## 10.3 Riesgos

La configuración actual es conservadora, pero la transparencia sería insuficiente si la IA se habilitara sin ampliar la interfaz.

**Prioridad:** Alta antes de activar IA.  
**Prioridad:** Media mientras permanezca desactivada.

## 10.4 Solución recomendada

Implementar un flujo que:

1. Muestre los datos que se enviarían.
2. Muestre el proveedor.
3. Muestre el endpoint.
4. Permita aceptar o cancelar.
5. Permita seleccionar categorías.
6. Guarde la versión del aviso aceptado.
7. Permita revocar el consentimiento.
8. Muestre el estado de consentimiento en Configuración.

---

# 11. Permisos y acceso al sistema

## 11.1 Funciones con acceso al sistema

La aplicación utiliza:

- `psutil`.
- WMI.
- Registro de Windows.
- `powercfg`.
- APIs de procesos.
- APIs de batería.
- APIs de hardware.
- Acceso a archivos temporales.
- Registro `HKCU`.
- Funciones de limpieza.
- Funciones de finalización de procesos.
- Creación de accesos directos.
- Instalación en `Program Files`.

El inicio automático utiliza:

```text
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run
```

## 11.2 Instalador

El instalador requiere administrador:

`RendiflyManager.iss`

```ini
PrivilegesRequired=admin
```

No se observó evidencia de que la aplicación principal requiera elevación permanente durante toda su ejecución.

## 11.3 Buenas prácticas presentes

- La configuración se almacena fuera de `Program Files`.
- El inicio automático utiliza HKCU.
- Las llamadas revisadas a procesos utilizan `shell=False`.
- Las URIs externas están restringidas.
- No se confirmó un servidor HTTP local.
- No se confirmó ejecución arbitraria de comandos desde una entrada directa del usuario.

## 11.4 Riesgos

La aplicación puede:

- Finalizar procesos.
- Cambiar energía.
- Modificar el registro.
- Eliminar archivos.
- Cambiar aplicaciones de inicio.

El usuario necesita información clara antes de ejecutar acciones con efectos persistentes o destructivos.

**Prioridad:** Media.

## 11.5 Solución recomendada

Documentar:

- Qué permisos necesita cada función.
- Qué acciones requieren administrador.
- Qué acciones son reversibles.
- Qué procesos pueden finalizarse.
- Qué archivos pueden eliminarse.
- Qué cambios del registro se realizan.
- Cómo deshacer cada cambio.
- Qué funciones son opcionales.

---

# 12. Seguridad del puente WebView2 y frontend

## 12.1 Comportamiento real

La aplicación expone un puente JavaScript-Python mediante pywebview:

`app.py`

El frontend puede invocar métodos nativos relacionados con:

- Hardware.
- Procesos.
- Limpieza.
- Configuración.
- Energía.
- Registro.
- IA.
- Feedback.
- Apertura de recursos externos.

## 12.2 Mejoras realizadas

Se corrigió el renderizado del contenido del asistente en:

`assistant.js`

Ahora el contenido se escapa antes de insertarse en HTML.

También se filtran URLs de fuentes y se escapan atributos HTML.

## 12.3 Riesgos restantes

- El puente expone numerosas funciones nativas.
- La seguridad depende de que solo se cargue contenido local confiable.
- No se verificó una política CSP completa.
- La navegación externa debe mantenerse restringida.
- Las funciones destructivas necesitan confirmación visible.

**Prioridad:** Media.

## 12.4 Solución recomendada

- Aplicar una Content Security Policy estricta.
- No cargar contenido remoto en la vista principal.
- Separar APIs destructivas.
- Confirmar acciones sensibles.
- Utilizar métodos específicos en vez de una API genérica de URI.
- Mantener WebView2 actualizado.
- Reducir la superficie del puente JavaScript-Python.

---

# 13. Seguridad del instalador

## 13.1 Comportamiento real

El instalador utiliza Inno Setup.

Características:

- Instalación en `Program Files`.
- Requiere administrador.
- Puede crear accesos directos.
- Puede iniciar la aplicación después de instalar.
- Muestra la licencia.
- Muestra los términos.
- Permite conservar o eliminar datos durante la desinstalación.

Archivos:

- `RendiflyManager.iss`
- `build-installer.ps1`

## 13.2 Firma digital

El archivo `Rendifly.spec` contiene:

```python
codesign_identity=None
```

El script de compilación permite firmar mediante variables de entorno, pero la firma no está configurada por defecto.

No hay evidencia de firma aplicada actualmente a:

- Ejecutable.
- Instalador.
- Desinstalador.

## 13.3 Hashes

El script genera hashes SHA-256 para:

- Instalador.
- Ejecutable.

Esto mejora la verificación de integridad, pero un hash sin firma no garantiza autenticidad.

## 13.4 Artefactos de compilación

El árbol contiene múltiples directorios de build y distribución históricos.

Esto puede provocar:

- Confusión entre builds.
- Empaquetado accidental de artefactos antiguos.
- Dificultad para verificar qué binario corresponde al código actual.
- Riesgo de distribuir un ejecutable no validado.

**Prioridad:** Alta antes de distribución pública.

## 13.5 Limitaciones actuales

- `ISCC.exe` no está instalado en el entorno revisado.
- No se generó un nuevo instalador durante esta auditoría.
- No se verificó una firma Authenticode.
- Las URLs del propietario, soporte y actualizaciones todavía son placeholders.
- Los binarios existentes no deben considerarse automáticamente equivalentes al código actual.

## 13.6 Solución recomendada

- Usar un directorio limpio para cada release.
- Limpiar builds anteriores.
- Firmar ejecutable, instalador y desinstalador.
- Publicar hashes junto con la firma.
- Verificar las firmas antes de publicar.
- Generar un SBOM.
- Mantener los artefactos de distribución separados del árbol de desarrollo.

---

# 14. Actualizaciones

## 14.1 Estado real

No existe actualmente un actualizador automático confirmado.

No se encontró:

- Comprobación automática de versión.
- Descarga automática.
- Instalación silenciosa.
- Rollback.
- Verificación de firma.
- Canal beta integrado.
- Protección contra downgrade.

El `AppId` estable del instalador permite que futuras instalaciones se identifiquen como la misma aplicación, pero esto no equivale a un actualizador propio.

## 14.2 Documentación

El README describe la conservación de preferencias durante reinstalaciones y actualizaciones, pero no documenta un sistema automático de actualización.

## 14.3 Riesgo

No existe un riesgo activo de un updater inseguro porque el updater no está implementado.

Si se implementa sin controles criptográficos, podría convertirse en una vía de ejecución de código no confiable.

**Prioridad:** Media actualmente.  
**Prioridad:** Alta cuando se implemente.

## 14.4 Solución recomendada

Diseñar futuras actualizaciones con:

- HTTPS.
- Manifiesto firmado.
- Hashes.
- Firma Authenticode.
- Protección contra downgrade.
- Verificación antes de ejecutar.
- Rollback.
- Confirmación visible del usuario.
- Registro de versión instalada.

---

# 15. IA externa

## 15.1 Estado actual

La IA externa está desactivada mediante:

`feature_flags.py`

La API devuelve un estado de funcionalidad futura cuando se intenta configurar o validar el proveedor:

`api.py`

## 15.2 Código preparado

Existe código para:

- Gemini.
- OpenAI-compatible.
- Búsqueda en DuckDuckGo.
- Construcción de contexto del equipo.
- Validación de proveedores.
- Configuración de modelos.
- Gestión de API keys.

Archivos:

- `gemini_client.py`
- `openai_client.py`
- `provider.py`
- `engine.py`

## 15.3 Protecciones implementadas

- La IA está desactivada por defecto.
- El consentimiento está separado de la validación.
- Los endpoints deben utilizar HTTPS.
- Se rechazan hosts locales.
- Se rechazan IPs privadas.
- Se rechazan credenciales incrustadas en URLs.
- La API key se protege mediante DPAPI.
- La API key no se devuelve al frontend.
- La búsqueda web no recibe automáticamente el contexto completo del equipo.
- El contexto técnico ya no se describe como “anonimizado”.

## 15.4 Riesgo

El contexto técnico del equipo puede incluir información identificable o sensible aunque no incluya directamente el nombre del usuario.

Por ese motivo, no debe describirse como anonimizado por defecto.

**Prioridad:** Alta antes de activar IA.

## 15.5 Solución recomendada

Antes de activar la IA:

- Mostrar una vista previa del contexto.
- Enviar únicamente los campos seleccionados.
- Desactivar procesos por defecto.
- Desactivar letras de unidad por defecto.
- Ofrecer modo “solo pregunta”.
- Documentar proveedores.
- Documentar retención.
- Documentar transferencias internacionales.
- Mostrar advertencia antes de la primera transferencia.
- Permitir revocar el consentimiento fácilmente.

---

# 16. Dependencias y cadena de suministro

## 16.1 Estado actual

Existe:

`requirements-lock.txt`

Este archivo contiene versiones fijadas del entorno actual de compilación.

También existe:

`requirements.txt`

que mantiene dependencias con restricciones mínimas.

## 16.2 Mejora realizada

El lockfile permite reproducir con mayor precisión el entorno utilizado para una compilación.

## 16.3 Limitaciones

El lockfile:

- Es un snapshot del entorno actual.
- Incluye dependencias de desarrollo y construcción.
- No incluye hashes de paquetes.
- No equivale a una instalación con `--require-hashes`.
- No constituye un SBOM formal.
- No demuestra por sí solo que el binario existente haya sido generado exactamente con esas versiones.

**Prioridad:** Media.

## 16.4 Solución recomendada

- Separar dependencias runtime y build.
- Añadir hashes.
- Generar SBOM.
- Ejecutar análisis de vulnerabilidades.
- Registrar las versiones incluidas en cada release.
- Mantener un proceso reproducible de compilación.

---

# 17. Transparencia para el usuario

## Estado actual

La aplicación informa parcialmente sobre:

- Monitorización.
- Almacenamiento local del nombre.
- Estado futuro de la IA.
- Feedback.
- Configuración local.

Todavía debe mejorar la información sobre:

- Procesos recopilados.
- Aplicaciones de inicio.
- Controladores.
- Contadores globales de red.
- Logs.
- Retención.
- Eliminación.
- Destinatario del feedback.
- Que las capturas no se adjuntan.
- Diferencia entre validar una API key y permitir envíos.
- Proveedores externos.
- Transferencias internacionales.

**Prioridad:** Alta antes de distribución pública.

## Solución recomendada

Añadir información visible en:

- Onboarding.
- Configuración.
- Página del asistente.
- Página de feedback.
- Instalador.
- Documentación de cada release.

---

# 18. Resumen de prioridades

| Prioridad | Área | Estado actual |
|---|---|---|
| Alta | Política de privacidad | Existe, pero contiene placeholders |
| Alta | EULA y términos | Existe, pero no está finalizado legalmente |
| Alta | IA externa | Desactivada; requiere consentimiento completo antes de activarse |
| Alta | Instalador firmado | No configurado por defecto |
| Alta | Transparencia | Parcial |
| Media | Logs | Activos y rotatorios, sin retención temporal definida |
| Media | Eliminación local | Implementada, pero no es borrado seguro |
| Media | Feedback | Manual y no silencioso, pero con información incompleta |
| Media | Permisos Windows | Funcionales, pero falta una matriz de permisos |
| Media | WebView2 | Escape mejorado, pero falta CSP completa |
| Media | Dependencias | Lockfile presente, faltan hashes y SBOM |
| Media | Actualizaciones | No existe updater actual |
| Baja | `send_diagnostics` | Campo presente, pero sin envío funcional confirmado |

---

# 19. Limitaciones verificadas

Las siguientes limitaciones continúan presentes:

1. `PRIVACY.md` contiene placeholders legales.
2. `TERMS.md` contiene placeholders legales.
3. Las URLs de propietario, soporte y actualizaciones del instalador no son definitivas.
4. `ISCC.exe` no está disponible en el entorno revisado.
5. La firma Authenticode no está configurada por defecto.
6. `codesign_identity=None` continúa presente en `Rendifly.spec`.
7. El updater automático no está implementado.
8. No se verificó una compilación nueva del instalador durante esta auditoría.
9. No se verificó que los binarios existentes coincidan byte a byte con el código actual.
10. No se generó un SBOM formal.
11. El lockfile no usa hashes de paquetes.
12. No existe una política temporal detallada de retención de logs.
13. No se confirmó una CSP completa para WebView2.

---

# 20. Conclusión documental

El estado actual de Rendifly Manager es el de una aplicación de Windows principalmente local:

- La monitorización está activa localmente.
- La configuración se almacena localmente.
- Los logs se almacenan localmente.
- El historial de notificaciones se almacena localmente.
- No se encontró telemetría propia activa.
- No existe un backend central de Rendifly.
- El feedback requiere acción manual del usuario.
- La IA externa está preparada en el código, pero desactivada actualmente.
- Las API keys se protegen mediante DPAPI cuando la función está habilitada.
- La validación de proveedores y el consentimiento están separados.
- Los endpoints externos se validan para exigir HTTPS.
- El contenido del asistente se escapa antes de insertarse en HTML.
- El instalador muestra licencia y términos.
- El script genera hashes SHA-256.
- La firma Authenticode todavía no está configurada.
- La documentación legal todavía debe completarse con datos reales del propietario.
- La versión Beta 2 no está publicada ni subida.

## Estado para Beta 2

**Mejoras técnicas implementadas localmente:** sí.  
**Auditoría de privacidad actualizada:** sí.  
**Documentación legal creada:** sí.  
**Documentación legal finalizada:** no, contiene placeholders.  
**Instalador recompilado y verificado:** no.  
**Instalador firmado:** no.  
**Beta 2 publicada:** no.  
**Beta 2 subida:** no.


