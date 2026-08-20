# CDA Revitolima — Sitio web y portales

Ecosistema digital de CDA Revitolima (Ibagué, Tolima): sitio público comercial, portal cliente y portal administrativo.

Desarrollado por **PUBLISELL NeuroMarketing Studio**.

---

## Estado actual

| Módulo | Estado |
|---|---|
| Sitio público (7 páginas) | Funcional |
| Agendamiento en línea | Funcional (datos en memoria) |
| Calculadora de tarifas | Funcional, alimentada desde administración |
| Recordatorio de vencimiento | Formulario funcional (sin envío automático) |
| Portal cliente | Funcional en modo demostración |
| Portal administrativo | Funcional en modo demostración |
| Exportación a Excel (CSV) | Funcional |
| Base de datos permanente | **Pendiente** — requiere Supabase |
| Google Calendar | **Pendiente** — requiere backend |
| WhatsApp automático | **Pendiente** — requiere WhatsApp Business API |

> **Importante:** mientras no esté conectado Supabase, los datos de los portales se reinician al recargar la página. El sitio público sí es plenamente utilizable (agendamiento, tarifas, recordatorio y WhatsApp con mensaje prellenado).

---

## Accesos de demostración

- **Portal cliente:** documento `1110512345` · placa `GRT41E`
- **Portal administrativo:** usuario `admin` · contraseña `revitolima`

Estos accesos son de prueba y desaparecen al conectar la autenticación real.

---

## Estructura

```
.
├── index.html          Aplicación completa (sitio + portales)
├── assets/
│   └── logo.png        Logo con fondo transparente
├── vercel.json         Cabeceras de seguridad y caché
├── robots.txt
├── sitemap.xml
└── README.md
```

Todo el CSS y el JavaScript están dentro de `index.html`, sin dependencias ni proceso de compilación. Se puede abrir directamente en el navegador.

---

## Publicar en Vercel desde GitHub

1. Crea un repositorio en GitHub (por ejemplo `cda-revitolima-web`) y sube estos archivos.
2. Entra a [vercel.com](https://vercel.com), inicia sesión con GitHub y elige **Add New → Project**.
3. Importa el repositorio. Vercel detecta un sitio estático: deja el framework en **Other** y **no** configures comando de compilación ni carpeta de salida.
4. Pulsa **Deploy**. En menos de un minuto tendrás una URL tipo `cda-revitolima-web.vercel.app`.

### Actualizaciones automáticas

Una vez conectado, cada cambio que subas a la rama principal se publica solo. El flujo queda así:

```
editas index.html → git commit → git push → Vercel publica
```

Cada rama distinta genera una URL de vista previa independiente, útil para mostrarle cambios al cliente sin tocar la versión publicada.

### Comandos de Git

```bash
git init
git add .
git commit -m "Sitio y portales CDA Revitolima"
git branch -M main
git remote add origin https://github.com/USUARIO/cda-revitolima-web.git
git push -u origin main
```

Para cambios posteriores:

```bash
git add .
git commit -m "Descripción del cambio"
git push
```

---

## Conectar el dominio cdarevitolima.com

1. En Vercel: **Project → Settings → Domains → Add**, escribe `cdarevitolima.com`.
2. Vercel te indicará los registros DNS. En el panel de tu proveedor de dominio:
   - Registro `A` de `@` apuntando a la IP que indique Vercel.
   - Registro `CNAME` de `www` apuntando a `cname.vercel-dns.com`.
3. La propagación tarda entre unos minutos y 24 horas. El certificado HTTPS se emite solo.

El hosting actual con WordPress puede conservarse hasta que confirmes que todo funciona. Solo cuando cambies el DNS, el dominio deja de apuntar al servidor antiguo.

**Antes de cambiar el DNS:** descarga una copia de seguridad completa del WordPress actual (archivos y base de datos) desde el panel del hosting.

---

## Datos reales configurados

- Teléfono y WhatsApp: **321 356 6313**
- Atención dominical: **8:00 a. m. – 2:00 p. m.**
- Ciudad: Ibagué, Tolima
- Servicios: revisión técnico-mecánica y de gases para carros y motos; financiación con Sistecrédito

### Pendiente de confirmar con el cliente

Estos datos se administran desde **Portal administrativo → Configuración** y no se publican con valores provisionales:

- Tarifas por tipo de vehículo y servicio (mientras estén vacías, el sitio muestra "Tarifa por confirmar" e invita a escribir por WhatsApp).
- Dirección exacta del centro (hoy solo se indica "Ibagué, Tolima" y el mapa apunta a la ciudad).
- Horarios de lunes a sábado.

---

## Próximos pasos

1. **Supabase** — base de datos permanente, autenticación con roles y almacenamiento. Convierte el prototipo en sistema operativo real.
2. **Google Calendar** — sincronización de citas en ambos sentidos.
3. **WhatsApp Business API** — confirmaciones y recordatorios automáticos.
4. **Migración a Astro** — sitio público estático optimizado, portales como aplicación.

---

## Notas técnicas

- Sin dependencias externas salvo las tipografías de Google Fonts.
- Navegación por rutas con `history.pushState`; cada página tiene título y descripción propios.
- Validado sin desbordamiento horizontal ni errores de consola en 360, 390, 768, 1366 y 1440 px.
- Exportaciones en CSV con BOM UTF-8 y separador `;`, compatibles con Excel en español.
- El logo se entrega en PNG con fondo transparente. La versión vectorial en SVG está pendiente de trazado profesional.
