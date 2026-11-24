# Registro de seguridad · Sistema Alumnos

Estudiante: ____________________   Repositorio: ____________________   Fecha: __________

Completa este registro a medida que avanzas. Cada fila debe poder seguirse hasta un **build de Jenkins**
y un **commit** (usa el identificador `VULN-xx` en el mensaje del commit).

## 1. Revisiones de seguridad realizadas


| # | Etapa del SDLC | Herramienta / técnica | Build | Resultado (resumen) |
|---|---|---|---|---|
| R1 | Código (SAST) | Bandit en Codespaces | Pendiente | Análisis inicial: 2 High, 2 Medium y 1 Low. Análisis posterior: 0 hallazgos en 205 líneas. |
| R2 | Dependencias (SCA) | pip-audit | Pendiente | Análisis pendiente de ejecución. |
| R3 | Pruebas dinámicas (DAST) | OWASP ZAP sobre staging | Pendiente | Escaneo pendiente de ejecución. |
| R4 | Revisión manual | Lectura de app.py | No aplica | Se revisaron consultas SQL, autenticación, credenciales y configuración de Flask. |
| R5 | Producción | Grafana + Prometheus | Pendiente | Verificación de métricas e incidentes pendiente. |

## 2. Vulnerabilidades identificadas y corregidas


| ID | Vulnerabilidad (CWE) | Detectada por | Ubicación | Riesgo | Corrección aplicada | Commit | Build que lo verifica |
|---|---|---|---|---|---|---|---|
| VULN-01 | Inyección SQL (CWE-89) | Bandit B608 | app.py:205 | Medio | Consulta parametrizada con SQLite y manejo seguro de errores. | Pendiente | Pendiente |
| VULN-02 | Uso de MD5 (CWE-327) | Bandit B324 | app.py:221 | Alto | Reemplazo por check_password_hash de Werkzeug. | Pendiente | Pendiente |
| VULN-03 | Contraseña fija (CWE-798) | Bandit B105 | app.py:20 | Bajo | Credenciales externas mediante Docker Secrets. | Pendiente | Pendiente |
| VULN-04 | Depuración habilitada (CWE-94) | Bandit B201 | app.py:241 | Alto | Desactivación de debug=True. | Pendiente | Pendiente |
| VULN-05 | Exposición de interfaces (CWE-605) | Bandit B104 | app.py:241 | Medio | Servidor de desarrollo limitado a 127.0.0.1. | Pendiente | Pendiente |


(Agrega las filas que necesites.)

## 3. Resultados de OWASP ZAP

| Alerta de ZAP | Riesgo | URL de ejemplo | VULN relacionada | Cómo se mitiga | ¿Mitigada? Build |
|---|---|---|---|---|---|
| | | | | | |

## 4. Monitoreo e incidentes


| Hora aproximada | Panel / métrica | Qué se observó | Entorno | Clasificación | Acción de respuesta | Verificación |
|---|---|---|---|---|---|---|
| 23:35–23:38 (23/11) | login_fallidos_total | Incremento de intentos fallidos durante ZAP | Staging | Evento de seguridad de prueba | Revisión de logs Flask y resultados DAST | Logs y build Jenkins #4 |
| 24/11 (verificación) | up | Producción no respondía (0) | Producción | Incidente de disponibilidad | Diagnóstico de Gunicorn y mantenimiento del bloqueo de despliegue | Prometheus confirmó up=0; pendiente recuperación |
| 24/11 (verificación) | up | Staging no respondía (0) | Staging | Incidente de disponibilidad | Reinicio de staging mediante deploy.sh | Endpoint /health respondió; Prometheus up=1 |


## 5. Gestión de dependencias

| Paquete | Versión inicial | Vulnerabilidades (IDs) | Versión final | Origen del cambio (PR de Dependabot / manual) | ¿Pruebas, pip-audit y ZAP siguen OK? Build |
|---|---|---|---|---|---|
| Flask | 2.2.2 | | | | |
| Werkzeug | 2.2.2 | | | | |
| Jinja2 | 3.1.2 | | | | |
| gunicorn | 21.2.0 | | | | |
| prometheus-client | 0.17.1 | | | | |

## 6. Trazabilidad

Pega aquí (o adjunta) el `TRAZABILIDAD.md` del último build y completa un recorrido por cada actividad del pipeline:

| Actividad | Hallazgo | Build que lo detectó | Commit / PR que lo resolvió | Build que lo verificó | Versión en producción |
|---|---|---|---|---|---|
| Revisión de seguridad (Bandit) | | #__ | | #__ | |
| Prueba automatizada (OWASP ZAP) | | #__ | | #__ | |
| Gestión de dependencias (Dependabot) | | #__ | PR #__ | #__ | |
