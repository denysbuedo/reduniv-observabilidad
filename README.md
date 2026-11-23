# RedUniv Observabilidad

Plataforma de observabilidad y diagnóstico de incidentes para los sistemas de RedUniv. Reúne métricas, logs, trazas, cambios de GitHub y CI/CD, despliegues verificados y tickets de soporte. Su objetivo es ubicar dónde empezó un fallo, qué operaciones afectó y qué evidencia permite confirmar la causa.

El proyecto está en **fase de diseño técnico**. El primer hito es un piloto de SGU en preproducción con HAProxy, Keycloak, PostgreSQL y las máquinas virtuales que participan en ese recorrido.

## Qué ofrecerá

- **Ficha por sistema y entorno** con salud, dependencias, instancias y versión observada.
- **Línea de tiempo de incidentes** que vincula alertas, despliegues, cambios de configuración, eventos de GitHub y reportes de la mesa de ayuda.
- **Investigación basada en evidencia** con acceso a las métricas, logs y trazas del intervalo afectado. Cada hipótesis indica qué la sustenta y qué queda por comprobar.
- **Pruebas sintéticas** de operaciones críticas, como disponibilidad e inicio de sesión, para detectar y verificar fallos desde el punto de vista del usuario.

## Arquitectura prevista

| Capa | Componentes |
| --- | --- |
| Recolección | OpenTelemetry Collector, agentes y sondas por zona |
| Métricas y alertas | Prometheus y Alertmanager |
| Logs, trazas y visualización | Loki, Tempo y Grafana |
| Catálogo, eventos e incidentes | API y worker propios con FastAPI y PostgreSQL |
| Integraciones | GitHub, pipelines de despliegue, mesa de ayuda y monitoreo existente |

## Piloto

La VM propuesta requiere **8 vCPU, 32 GiB de RAM y 450 GiB de disco SSD**, distribuidos en 50 GiB para el sistema y 400 GiB para datos. Se estiman 100 GiB externos para copias iniciales. El tamaño de producción se ajustará con la carga medida durante el piloto.

Los cinco ejercicios del piloto cubren caída de backend, fallo de identidad o conectividad, saturación de PostgreSQL, regresión tras un despliegue y pérdida de telemetría.

## Documentación

- Arquitectura, requisitos, dimensionamiento de la VM y plan de despliegue. [Proyecto técnico](PROYECTO-TECNICO-OBSERVABILIDAD-MES.md)
- Estudio de LogicMonitor, alcance funcional y método de investigación. [Propuesta de observabilidad](PROPUESTA-OBSERVABILIDAD-MES.md)
