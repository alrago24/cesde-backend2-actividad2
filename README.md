# 🧪 Laboratorio: Documentación de Pruebas de API REST

 Esta actividad debe documentarse íntegramente en este archivo `README.md`. Por cada punto, el estudiante debe ejecutar la petición indicada y completar los espacios en blanco con la **Respuesta del Servidor** y el **Código de Estado** real obtenido en su entorno local.

---

## 🚀 Guía de Pruebas y Documentación

### 1. Crear un nuevo estudiante

* **Método:** `POST`
* **URL:** `http://localhost:8080/api/students`
* **Cuerpo de la Petición (JSON):**

```json
{
  "firstName": "Ana",
  "lastName": "García",
  "email": "ana.garcia@estudiante.com",
  "birthDate": "2001-03-12",
  "phone": "3004445566"
}

```

* **Respuesta del Servidor (Completar):**

```json
{
    "firstName": "Ana",
    "lastName": "García",
    "email": "ana.garcia@estudiante.com",
    "birthDate": "2001-03-12",
    "id": 1,
    "phone": "3004445566"
}

```

* **Código de Estado (Status Code):** `201 Created`

---

### 2. Obtener la lista completa

* **Método:** `GET`
* **URL:** `http://localhost:8080/api/students`
* **Respuesta del Servidor (Completar):**

```json
[
    {
        "firstName": "Ana",
        "lastName": "García",
        "email": "ana.garcia@estudiante.com",
        "birthDate": "2001-03-12",
        "id": 1,
        "phone": "3004445566"
    }
]

```

* **Código de Estado (Status Code):** `200 OK`

---

### 3. Buscar estudiante por ID (Existente)

* **Método:** `GET`
* **URL:** `http://localhost:8080/api/students/1`
* **Respuesta del Servidor (Completar):**

```json
{
    "firstName": "Ana",
    "lastName": "García",
    "email": "ana.garcia@estudiante.com",
    "birthDate": "2001-03-12",
    "id": 1,
    "phone": "3004445566"
}

```

* **Código de Estado (Status Code):** `200 OK`

---

### 4. Buscar estudiante por Email

* **Método:** `GET`
* **URL:** `http://localhost:8080/api/students/email/ana.garcia@estudiante.com`
* **Respuesta del Servidor (Completar):**

```json
{
    "firstName": "Ana",
    "lastName": "García",
    "email": "ana.garcia@estudiante.com",
    "birthDate": "2001-03-12",
    "id": 1,
    "phone": "3004445566"
}

```

* **Código de Estado (Status Code):** `200 OK`

---

### 5. Actualizar datos del estudiante

* **Método:** `PUT`
* **URL:** `http://localhost:8080/api/students/1`
* **Cuerpo de la Petición (JSON):**

```json
{
  "firstName": "Ana María",
  "lastName": "García",
  "email": "ana.garcia@estudiante.com",
  "birthDate": "2001-03-12",
  "phone": "3119998877"
}

```

* **Respuesta del Servidor (Completar):**

```json
{
    "firstName": "Ana María",
    "lastName": "García",
    "email": "ana.garcia@estudiante.com",
    "birthDate": "2001-03-12",
    "id": 1,
    "phone": "3119998877"
}

```

* **Código de Estado (Status Code):** `200 OK`

---

### 6. Escenario de Error: Buscar ID inexistente

* **Método:** `GET`
* **URL:** `http://localhost:8080/api/students/999`
* **Respuesta del Servidor (Completar):**

```json


```

* **Código de Estado (Status Code):** `404 Not Found`

---

### 7. Eliminar el registro

* **Método:** `DELETE`
* **URL:** `http://localhost:8080/api/students/1`
* **Respuesta del Servidor (Completar):**

```json


```

* **Código de Estado (Status Code):** `204 No Content`

---

## 📝 Cuestionario de Análisis

**Instrucciones:** Responda las siguientes preguntas basándose en su experiencia durante el laboratorio y el código del proyecto.

1. **¿Cuál es la diferencia entre los códigos de estado 200 y 201? ¿En qué endpoints se obtuvieron cada uno?**
* *Respuesta:*
El estado 201 hace referencia a una respuesta de creación de un recurso exitosa (POST) y el estado 200 (GET) hace referencia solo a una consulta procesada de forma exitosa.
El estado 201 se obtuvo del endpoint POST
El estado 200 se obtuvo del endpoint GET

2. **En el escenario de error (punto 6), ¿qué información devuelve la API y por qué es importante para un desarrollador frontend recibir un código 404 en lugar de un código 500?**
* *Respuesta:*
La API solo devuelve un estado 404 Not Found sin información en el cuerpo de JSON. Es importante recibir un codigo 404 porque permite diferenciar un recurso inexistente y un estado 500 hace referencia una falla de servidor o un fallo.

3. **¿Qué sucede en la base de datos PostgreSQL cuando se ejecuta con éxito la petición DELETE? (Explique brevemente en términos de persistencia).**
* *Respuesta:*
La fila no se elimina físicamente del disco al instante y como "muerta" o PostgreSQL invisible para futuras transacciones y permite que otras consultas que empezaron antes de tu DELETE sigan viendo los datos de forma consistente.


4. **Si intentara crear un estudiante con el mismo email que ya existe en la base de datos, ¿qué cree que sucedería y qué código de error sería el más adecuado para devolver?**
* *Respuesta:*
El sistema bloqueará la acción, mostrando un error de duplicidad (ej. "el correo ya existe"). El código HTTP más adecuado es 409 Conflict (Conflicto), ya que indica que la solicitud no puede procesarse debido a un conflicto con el estado actual del servidor (el correo ya está registrado).


5. **¿Por qué utilizamos el método PUT para actualizar y no el método POST? ¿Cuál es la convención técnica detrás de esta decisión?**
* *Respuesta:*

Usamos PUT para actualizar porque le da seguridad a la red: si hay un fallo de conexión y tu aplicación de Spring vuelve a intentar la petición automáticamente, el PUT garantiza que no vas a romper nada ni a crear basura en tu base de datos PostgreSQL, mientras que un POST podría causar duplicados.

La convención técnica detrás de esta decisión es la Idempotencia.

