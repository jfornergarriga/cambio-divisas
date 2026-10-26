# Especificaciones Técnicas: Integración de Divisas

## 1. Descripción General
La aplicación utiliza el servicio de **Frankfurter** para obtener datos de tipos de cambio de divisas tanto actuales como históricos. Se ha elegido este servicio porque proporciona datos fiables (de más de 105 bancos centrales oficiales) y es de código abierto.

## 2. Características de la API (Frankfurter)
Para interactuar con la API de Frankfurter, los desarrolladores deben tener en cuenta las siguientes características técnicas:

*   **Arquitectura:** API RESTful.
*   **Autenticación:** **NO requerida.** No se necesita generar ni enviar ninguna "API Key" en las cabeceras (headers).
*   **Límites de uso:** Sin cuotas ni límites mensuales. Totalmente gratuita.
*   **Método de petición:** Todas las consultas se realizan a través de peticiones HTTP `GET` estándar.
*   **Formato de respuesta:** Todos los datos se devuelven en formato `JSON`.
*   **URL Base:** `https://api.frankfurter.dev/v2`

---

## 3. Endpoints y Construcción de Peticiones

Cualquier cliente (frontend, backend o script) se comunicará con la aplicación realizando peticiones GET a la URL Base más el endpoint correspondiente. A continuación se detallan los casos de uso necesarios para la aplicación:

### A. Obtener los tipos de cambio más recientes
Devuelve las cotizaciones actuales de todas las divisas disponibles tomando como base el Euro (EUR) por defecto.
*   **Ruta:** `/rates`
*   **Ejemplo de petición:** `GET https://api.frankfurter.dev/v2/rates`

### B. Conversión directa entre dos monedas
Devuelve el valor exacto actual de una moneda respecto a otra.
*   **Ruta:** `/rate/{moneda_base}/{moneda_objetivo}`
*   **Ejemplo de petición:** `GET https://api.frankfurter.dev/v2/rate/eur/usd`
    *(Obtiene a cuánto equivale 1 Euro en Dólares estadounidenses).*

### C. Consulta de datos históricos de un día específico
Devuelve las cotizaciones de una fecha exacta en el pasado.
*   **Ruta:** `/rates`
*   **Parámetros URL (Query string):**
    *   `date`: Fecha en formato `YYYY-MM-DD`.
    *   `base` (Opcional): Moneda base (ej. `usd`).
    *   `quotes` (Opcional): Monedas específicas separadas por comas que queremos consultar.
*   **Ejemplo de petición:** `GET https://api.frankfurter.dev/v2/rates?date=1999-01-04&base=usd&quotes=gbp,jpy`

### D. Consulta de histórico por rango de fechas (Series Temporales)
Ideal para pintar gráficas de evolución de una moneda en el tiempo.
*   **Ruta:** `/rates`
*   **Parámetros URL (Query string):**
    *   `from`: Fecha de inicio en formato `YYYY-MM-DD`.
    *   `to`: Fecha de fin en formato `YYYY-MM-DD`.
    *   `base` (Opcional): Moneda base.
    *   `quotes` (Opcional): Monedas objetivo.
    *   `group` (Opcional): Permite agrupar los datos (ej. `month` para medias mensuales).
*   **Ejemplo de petición:** `GET https://api.frankfurter.dev/v2/rates?from=2026-01-01&to=2026-01-31&base=eur&quotes=usd`

---

## 4. Estructura de la Respuesta JSON

Al realizar cualquiera de las peticiones anteriores, la API devolverá un objeto JSON estándar. El código de la aplicación debe estar preparado para parsear esta estructura.

**Ejemplo de respuesta al consultar `/rate/eur/usd`:**

```json
{
  "amount": 1.0,
  "base": "EUR",
  "date": "2026-10-23",
  "rates": {
    "USD": 1.0815
  }
}
```

**Procesamiento en la App:**
1. Realizar la petición GET asíncrona.
2. Leer el campo `rates` dentro del JSON.
3. Extraer el valor numérico correspondiente a la clave de la moneda solicitada (ej. `rates.USD`).
4. Mostrar este valor en la interfaz de usuario de la aplicación.