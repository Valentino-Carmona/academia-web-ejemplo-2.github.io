# La Academia — Carta digital y reservas

[![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-Deployed-brightgreen)](https://tu-usuario.github.io/la-academia/)  
[![Static Site](https://img.shields.io/badge/Static-HTML%2FCSS%2FJS-blue)](https://developer.mozilla.org/es/docs/Web)  

> **Carta digital y sistema de reservas** para el restaurante ficticio *La Academia*. Un sitio web estático, responsivo y completamente autónomo, pensado para que los comensales exploren el menú, filtren por categorías o ingredientes, y reserven su mesa en segundos a través de WhatsApp.

🌐 [**Demo en vivo**](https://valentino-carmona.github.io/academia-web-ejemplo-2.github.io/)  

---

## 📋 Tabla de Contenidos

- [Características](#-características)
- [Estructura del Proyecto](#-estructura-del-proyecto)
- [Personalización](#-personalización)
  - [Datos del local (CONFIG)](#datos-del-local-config)
  - [Carta (MENU)](#carta-menu)
- [Despliegue en GitHub Pages](#-despliegue-en-github-pages)
- [Tecnologías Utilizadas](#-tecnologías-utilizadas)
- [Buenas Prácticas de Ingeniería](#-buenas-prácticas-de-ingeniería)
- [Licencia](#-licencia)

---

## 🚀 Características

- **Carta digital completa**: Todas las categorías (pizzas, empanadas, pastas, carnes, postres, etc.) con descripciones, precios y etiquetas destacadas.
- **Búsqueda en tiempo real**: Filtra platos por nombre o ingrediente con resaltado de coincidencias.
- **Navegación por categorías**: Pestañas deslizables que permiten ver secciones específicas.
- **Reservas integradas**: Formulario que genera un mensaje pre‑rellenado y lo envía por WhatsApp (incluye código de reserva y resumen).
- **Estado de apertura**: Muestra si el local está abierto según horarios configurables.
- **Diseño responsive y atmosférico**: Paleta de colores cálida, tipografías elegantes, animaciones suaves y modo oscuro.
- **Imprimible**: La carta se puede imprimir directamente desde el navegador.
- **Accesibilidad**: Soporte para lectores de pantalla, navegación por teclado y reducción de movimiento.

---

## 🗂️ Estructura del Proyecto

El proyecto es **monolítico**: todo el código (HTML, CSS, JavaScript) reside en un único archivo `index.html`. Esto facilita el despliegue y la distribución.

```plaintext
la-academia/
└── index.html          # Página completa (estructura, estilos y lógica)
```

No se requieren dependencias externas ni servidores; la página es completamente autocontenida.

---

## 🛠️ Personalización

Toda la información del restaurante y la carta se almacena en dos objetos JavaScript dentro de la etiqueta `<script>` del archivo `index.html`. Modifícalos para adaptar el sitio a tu negocio.

### Datos del local (`CONFIG`)

Localiza el bloque `CONFIG` en el código:

```javascript
const CONFIG = {
    whatsapp: "5491131402181",          // Número sin "+", sin espacios ni guiones
    telefonoVisible: "+54 9 113 140-2181",
    direccion: "Av. Colón 1234, Córdoba",
    mapa: "https://maps.google.com/?q=Av.+Colon+1234+Cordoba",
    maxComensales: 12,
    horarios: { /* días y rangos horarios */ },
    horariosTexto: [ /* texto legible para mostrar */ ],
    turnos: [ /* opciones para el formulario de reserva */ ]
};
```

- **`whatsapp`**: Número de WhatsApp al que llegarán las reservas (solo dígitos).
- **`horarios`**: Objeto con clave `0` (domingo) a `6` (sábado). Cada día tiene un array de rangos `[hora_inicio, hora_fin]`. Usa `"24:00"` para medianoche.
- **`turnos`**: Define los bloques horarios disponibles en el formulario (ej. almuerzo y cena).

### Carta (`MENU`)

El objeto `MENU` es un array de categorías. Cada categoría tiene:

```javascript
{
  id: "pizzas",                 // Identificador único
  nombre: "Pizzas",             // Título visible
  icono: "ic-pizza",            // Icono del sprite inline
  items: [                      // Lista de platos
    { n: "Muzzarella", d: "Descripción...", p: 16500, tag: "Clásico" }
  ],
  grupos: [ /* opcional: subcategorías */ ],
  nota: { /* opcional: nota al final de la sección */ }
}
```

- **`p`**: Precio en pesos (número entero). Se formatea automáticamente.
- **`pTexto`**: Alternativa a `p` para precios variables (ej. `"Desde $18.900"`).
- **`pre`**: Prefijo para el precio (ej. `"+"` para salsas con recargo).
- **`tag`**: Etiqueta destacada que aparece junto al nombre.

Para añadir o quitar platos, simplemente edita el array correspondiente. El buscador y el contador de platos se actualizarán automáticamente.

---

## 🌐 Despliegue en GitHub Pages

GitHub Pages permite hospedar sitios estáticos de forma gratuita. Sigue estos pasos:

1. **Crea un repositorio** en GitHub (puede ser público o privado).
2. **Sube el archivo `index.html`** a la raíz del repositorio.
3. Ve a **Settings > Pages**.
4. En la sección *Branch*, selecciona `main` (o `master`) y la carpeta raíz (`/ (root)`).
5. Guarda los cambios. En pocos minutos el sitio estará disponible en:  
   `https://<tu-usuario>.github.io/<nombre-del-repo>/`

Si quieres usar un dominio personalizado, configura la opción *Custom domain* en la misma sección.

---

## 💻 Tecnologías Utilizadas

- **HTML5 semántico** – Estructura accesible.
- **CSS3** – Variables CSS, Grid, Flexbox, animaciones, `backdrop-filter` y diseño responsivo.
- **JavaScript vanilla** – Manipulación del DOM, gestión de estado, búsqueda en tiempo real y validación de formularios sin librerías externas.
- **SVG inline** – Iconos vectoriales sin peticiones HTTP adicionales.
- **Google Fonts** – Tipografías *Cormorant Garamond* y *Montserrat* para una estética elegante.
- **Intersection Observer** – Animaciones *reveal* al hacer scroll.
- **Web Storage** – No se usa, pero el estado se mantiene en memoria; se podría extender fácilmente.

---

## 🛡️ Buenas Prácticas de Ingeniería

- **Separación de datos y lógica**: La carta y la configuración están aisladas en objetos `MENU` y `CONFIG`, facilitando futuras migraciones a un backend o CMS.
- **Indexación y búsqueda eficiente**: Se genera un índice plano de todos los platos para búsquedas rápidas.
- **Accesibilidad**: Atributos `aria`, etiquetas semánticas, navegación por teclado y soporte para `prefers-reduced-motion`.
- **Rendimiento**: Sin dependencias externas (excepto fuentes de Google); carga instantánea.
- **Mantenibilidad**: Código comentado y estructurado en secciones claras.
- **Imprimible**: Estilos específicos para impresión (`@media print`) que eliminan elementos no deseados.
- **Seguridad**: Todos los textos se escapan usando `esc()` para evitar XSS (aunque no hay inputs de usuario que se reflejen directamente).
