# API de Ventas: TodoCamisetas (PHP Puro con MVC)

> **Examen Transversal Final de Desarrollo Backend.** Proyecto que implementa una API RESTful de alto rendimiento para el sistema de gestión de ventas de camisetas, destacando por su **arquitectura modular (MVC)** y **lógica de negocio avanzada** para la determinación dinámica de precios.

---

## Arquitectura y Tecnología Backend

Este proyecto cumple con los principios de desarrollo backend  (Resultado de Aprendizaje 1.1) y la construcción de un servicio API (Resultado de Aprendizaje 2.1).

* **Patrón de Diseño:** Implementación estricta de la arquitectura **Modelo-Vista-Controlador (MVC)** utilizando **PHP Puro** (sin frameworks). Esto garantiza la **separación de responsabilidades** (Models para datos, Controllers para la gestión HTTP).
* **Tecnología Principal:** **PHP Puro** y **MySQL** (`todocamisetas`) utilizando **PDO** para una conexión segura y eficiente.
* **Enrutamiento Avanzado:** Sistema de *routing* implementado con **expresiones regulares** (`routes/index.php`) para mapear peticiones HTTP (Resultado de Aprendizaje 1.2.1).
    * `GET /camisetas/(\d+)` -> Llama al método `show()` del `CamisetaController`.

### Endpoints y Funcionalidad REST
La API expone **3 recursos principales** con operaciones **CRUD** completas (Resultado de Aprendizaje 3.1.1):

| Recurso (Ruta) | Métodos Implementados | Propósito |
| :--- | :--- | :--- |
| `/camisetas` | **CRUD** (GET, POST, PUT, DELETE) | Gestión del inventario y datos de las camisetas. |
| `/clientes` | **CRUD** (GET, POST, PUT, DELETE) | Gestión de clientes B2B (Registro, Categorización). |
| `/tallas` | **CRUD** (GET, POST, DELETE) | Gestión de tallas disponibles (Relación N:M). |

---

## Lógica de Negocio Avanzada (Optimización)

Este proyecto evidencia la optimización de operaciones CRUD para mejorar la eficiencia (Resultado de Aprendizaje 3.2.2) a través de la lógica de descuentos:

* **Cálculo de Precio Final Dinámico:** El endpoint `GET /camisetas/{id}?cliente_id={id}` aplica la siguiente regla de negocio:
    1.  Toma como precio base el `precio_oferta` (si existe) o el `precio` regular.
    2.  Aplica el **descuento porcentual** definido para el cliente consultado (VIP/Preferencial).
    3.  El resultado se devuelve en el campo `precio_final`.
* **Validación de Integridad:** Restricción implementada para evitar la eliminación de un **Cliente** si este tiene **Camisetas asociadas** (Claves Foráneas).

## Documentación y Pruebas de Calidad

* **Documentación API (Swagger/OpenAPI 3.0):** Se incluye **`swagger.json`**, detallando todas las rutas, parámetros, y esquemas de datos. Esto cumple el requisito de que la API esté documentada de forma clara (Resultado de Aprendizaje 2.2.3).
* **Pruebas de Calidad:** Se incluye la colección de **Postman** (adjunta) para la validación de la lógica de descuentos y todas las operaciones CRUD.

---

## Estructura del Proyecto (Patrón MVC)

```

.
├── config/                        \# Conexión a la Base de Datos (database.php - PDO)
├── controllers/                   \# Lógica de Peticiones HTTP (Controladores)
├── models/                        \# Lógica de la Base de Datos (Modelos CRUD)
├── routes/                        \# Sistema de Enrutamiento por Expresiones Regulares
├── public/                        \# Punto de Entrada (index.php, .htaccess)
├── swagger/                       \# Documentación OpenAPI 3.0 (swagger.json)
├── todocamisetas.sql              \# Script de Creación e Inserción de Datos MySQL
└── README.md

```
