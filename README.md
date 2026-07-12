# API Gateway

Componente tecnico de entrada para EcoMarket SPA. Centraliza el acceso REST hacia los microservicios y expone un punto unico de entrada para clientes como Postman, Frontend Web o Caja POS.

## Responsable

| Campo                 | Detalle                 |
| --------------------- | ----------------------- |
| Responsable principal | Ignacio Valeria         |
| Componente            | API Gateway             |
| Rama de trabajo       | `feature/api-gateway`   |
| Base de datos         | No aplica               |
| Puerto local          | `8081`                  |
| URL base local        | `http://localhost:8081` |

## Que hace

- Expone un punto unico de entrada para el backend.
- Redirige solicitudes REST hacia el microservicio correspondiente segun el path.
- Mantiene rutas ordenadas por dominio.
- Expone endpoints Actuator para validacion tecnica.

## Que no hace

- No implementa logica de negocio.
- No tiene base de datos propia ni entidades JPA.
- No reemplaza a los microservicios de dominio.

## Tecnologias

- Java 25
- Spring Boot 4.0.7
- Spring Cloud Gateway WebFlux (reactivo)
- Spring Cloud 2025.1.2
- Spring Actuator
- Maven

## Configuracion

```text
src/main/resources/application.yml
```

```yaml
server:
  port: 8081
spring:
  application:
    name: api-gateway
```

## Como ejecutar

```powershell
.\mvnw.cmd spring-boot:run
```

## Como probar

```powershell
.\mvnw.cmd clean test
```

## Orden recomendado de ejecucion

```text
1. Iniciar MySQL o XAMPP.
2. Levantar los microservicios necesarios.
3. Levantar el API Gateway.
4. Consumir endpoints desde Postman usando http://localhost:8081.
```

## Rutas configuradas

| Ruta Gateway              | Microservicio destino          | Puerto interno |
| ------------------------- | ------------------------------ | -------------- |
| `/api/auth/**`            | MS Usuarios e Identidad        | `8083`         |
| `/api/usuarios/registro`  | MS Usuarios e Identidad        | `8083`         |
| `/api/usuarios/clientes/**` | MS Usuarios e Identidad      | `8083`         |
| `/api/productos/**`       | MS Catalogo                    | `8084`         |
| `/api/categorias/**`      | MS Catalogo                    | `8084`         |
| `/api/resenas/**`         | MS Catalogo                    | `8084`         |
| `/api/inventario/**`      | MS Inventario y Abastecimiento | `8085`         |
| `/api/inventario/productos/**` | MS Inventario y Abastecimiento | `8085`    |
| `/api/pedidos/**`         | MS Pedidos y Ventas            | `8086`         |
| `/api/ventas/**`          | MS Pedidos y Ventas            | `8086`         |
| `/api/pedidos/devoluciones/**` | MS Pedidos y Ventas       | `8086`         |
| `/api/pedidos/reclamaciones/**` | MS Pedidos y Ventas      | `8086`         |
| `/api/envios/**`          | MS Logistica de Envios         | `8087`         |
| `/api/rutas/**`           | MS Logistica de Envios         | `8087`         |
| `/api/admin/tiendas/**`   | MS Administracion y Soporte    | `8088`         |
| `/api/admin/metricas/**`  | MS Administracion y Soporte    | `8088`         |
| `/api/admin/alertas/**`   | MS Administracion y Soporte    | `8088`         |
| `/api/admin/respaldos/**` | MS Administracion y Soporte    | `8088`         |
| `/api/soporte/tickets/**` | MS Administracion y Soporte    | `8088`         |
| `/api/v1/reportes/**`     | MS Reportes                    | `8089`         |
| `/api/v1/kpis/**`         | MS Reportes                    | `8089`         |

## Ejemplos de uso mediante Gateway

```http
POST http://localhost:8081/api/auth/login
```

```http
GET http://localhost:8081/api/productos
```

```http
GET http://localhost:8081/api/inventario/productos
```

```http
GET http://localhost:8081/api/pedidos
```

```http
GET http://localhost:8081/api/envios
```

```http
GET http://localhost:8081/api/admin/tiendas
```

```http
GET http://localhost:8081/api/v1/reportes
```

```http
GET http://localhost:8081/actuator/health
```

## Documentacion relacionada

- [Rutas del API Gateway](https://github.com/Nachovn12/ecomarket-spa-docs/blob/main/docs/api-gateway-rutas.md)
- [Arquitectura de microservicios](https://github.com/Nachovn12/ecomarket-spa-docs/blob/main/docs/arquitectura/arquitectura-microservicios.md)
- [Comunicacion REST entre servicios](https://github.com/Nachovn12/ecomarket-spa-docs/blob/main/docs/integracion/comunicacion-rest-entre-servicios.md)
- [Repositorio de documentacion](https://github.com/Nachovn12/ecomarket-spa-docs)
