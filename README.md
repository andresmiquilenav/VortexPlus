# VORTEX +

Calculadora de precio de venta: costo, transporte, IVA (ON/OFF), factor como divisor,
redondeo comercial hacia arriba, precio psicológico, precio objetivo (cálculo inverso),
lista de productos, el módulo **Material de Construcción** (factor bloqueado entre 0,75
y 0,80) y una calculadora auxiliar de **Transporte** (porcentaje a partir de dos facturas,
con transferencia de un solo uso hacia General). Incluye una pantalla de acceso inicial
con credenciales fijas (sin backend, sin base de datos: es solo una barrera visual).

Es un **sitio estático de un solo archivo**: no usa framework, no tiene dependencias de
Node ni paso de build. Todo el HTML, CSS y JavaScript vive en `index.html`. El isotipo
oficial va incrustado en ese mismo archivo (como imagen en base64, usado tanto en el
encabezado como en la pantalla de acceso) para que la app funcione de forma autónoma
sin rutas a assets externos; además se incluye el archivo original en
`assets/isotipo-vortex.webp` como respaldo de marca.

## Navegación

No hay pestañas visibles. Los tres módulos (General, Material de Construcción,
Transporte) se abren exclusivamente mediante las tres burbujas negro mate con íconos
rojos (tuerca, carretilla, camión). En pantallas de 1300px de ancho o más quedan fijas
en una columna vertical a la izquierda; por debajo de ese ancho se muestran en una fila
horizontal bajo la firma del desarrollador.

## Acceso

La app muestra primero una pantalla de login. Credenciales:

- **Usuario:** `andres@falkon.cl`
- **Clave:** `123456`

Es una verificación hecha en el propio navegador (JavaScript), sin servidor ni
almacenamiento de sesión: cada vez que se recarga la página vuelve a pedir acceso.

## Estructura del proyecto

```
vortex-plus/
├── index.html              # Aplicación completa (HTML + CSS + JS)
├── assets/
│   └── isotipo-vortex.webp # Isotipo oficial VORTEX + (archivo de respaldo)
├── vercel.json              # Configuración de despliegue (sitio estático, sin build)
├── package.json             # Metadatos del proyecto (sin dependencias)
└── README.md
```

## Ejecutar en local

No requiere `npm install` (no hay dependencias). Cualquiera de estas opciones sirve:

```bash
# Opción 1: con Vercel CLI
npm i -g vercel
vercel dev

# Opción 2: cualquier servidor estático
npx serve .

# Opción 3: abrir index.html directamente en el navegador
```

## Desplegar en Vercel

1. Descomprime el ZIP.
2. Sube la carpeta a un repositorio (GitHub/GitLab/Bitbucket) o impórtala directamente
   en Vercel con `vercel` (CLI) o arrastrando la carpeta en vercel.com/new.
3. Framework Preset: **Other** (Vercel lo detecta automáticamente como sitio estático).
4. Build Command: no es necesario tocarlo — `vercel.json` ya lo deja resuelto.
5. Output Directory: raíz del proyecto (ya configurado en `vercel.json`).
6. Deploy. No requiere variables de entorno ni configuración adicional.

## Notas técnicas

- Las únicas conexiones externas son las fuentes de Google Fonts
  (`fonts.googleapis.com` / `fonts.gstatic.com`), estándar y accesibles desde cualquier
  hosting, incluido Vercel.
- Los datos que ingresa el usuario en General, Material de Construcción y Transporte
  (costo, factor, lista de productos, totales de factura, la preferencia de sonido del
  potenciómetro, etc.) se guardan en `localStorage` del navegador, por lo que persisten
  entre visitas pero son privados de cada dispositivo/navegador. El acceso (login) no se
  guarda: es solo por sesión de página.
- Los dos potenciómetros (General y Material de Construcción) usan Web Audio API para
  el clic al girar; el sonido arranca apagado y se activa con el botón 🔊/🔇.
- No hay backend, API keys ni variables de entorno involucradas. Las credenciales de
  acceso están fijas en el código del lado del cliente — es una barrera visual, no un
  sistema de autenticación real.
