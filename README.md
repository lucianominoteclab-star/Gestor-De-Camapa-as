# Campaign Manager — Discador OmniLeads

Herramienta para gestionar bases de leads, mergear resultados del discador y armar campañas filtradas. Vive en GitHub Pages y guarda los datos en Google Sheets via Apps Script (100% gratis).

---

## Arquitectura

```
GitHub Pages (index.html)
        ↕ fetch()
Google Apps Script (Web App gratuita)
        ↕
Google Sheets (base de datos en tu Drive)
```

---

## Setup en 4 pasos

### Paso 1 — Crear la Google Sheet

1. Abrí [Google Sheets](https://sheets.google.com) y creá una hoja nueva
2. Llamala **"Campaign Manager"** (o el nombre que quieras)
3. Copiá la URL — la necesitás en el paso 2

---

### Paso 2 — Configurar Apps Script

1. En la Sheet, andá a **Extensiones → Apps Script**
2. Borrá el código que aparece por defecto
3. Pegá todo el contenido de `Code.gs` (está en este repo)
4. Guardá con `Ctrl+S`

**Deployar como Web App:**
1. Clic en **Implementar → Nueva implementación**
2. Tipo: **Aplicación web**
3. Ejecutar como: **Yo (tu cuenta)**
4. Quién tiene acceso: **Cualquier usuario**
5. Clic en **Implementar**
6. Copiá la **URL de la aplicación web** — la vas a pegar en la app

> ⚠️ La primera vez te va a pedir que autorices los permisos de Google. Es normal, aceptá.

---

### Paso 3 — Subir a GitHub Pages

1. Creá un repo nuevo en GitHub (ej: `campaign-manager`)
2. Subí `index.html` y `README.md`
3. Andá a **Settings → Pages**
4. Source: **Deploy from a branch → main → / (root)**
5. Guardá. En 1-2 minutos tu app va a estar en:
   `https://TU_USUARIO.github.io/campaign-manager`

---

### Paso 4 — Conectar la app

1. Abrí tu app en GitHub Pages
2. En el sidebar inferior, pegá la URL del Apps Script
3. Clic en **Conectar**
4. Si dice "Conectado ✓" → todo listo

---

## Uso diario

### Subir base nueva
1. Andá a **Cargar datos**
2. Subí el CSV original (columnas: Nombre, Correo, numero_de_telefono, Numero_de_telefono_de_WhatsApp, Carrera)
3. Se guarda automáticamente en la Google Sheet

### Mergear resultados OmniLeads
1. Exportá el CSV desde OmniLeads al finalizar la jornada
2. Andá a **Cargar datos → Resultados OmniLeads**
3. Subí el CSV — se mergea por número de teléfono y actualiza Calificación, Contactación e Intentos en Drive

### Armar campaña
1. Andá a **Armar campaña**
2. Filtrá por carrera, calificación, contactación e intentos
3. Poné un nombre a la campaña
4. **Exportar CSV** → descarga lista para subir al discador

### Dashboard
Se actualiza automáticamente con los datos de Drive al conectarse.

---

## Columnas del CSV

| Columna | Origen | Descripción |
|---|---|---|
| Nombre | Vos | Nombre del lead |
| Correo | Vos | Email |
| numero_de_telefono | Vos | Teléfono principal |
| Numero_de_telefono_de_WhatsApp | Vos | WhatsApp |
| Carrera | Vos | Carrera de interés |
| Calificación | OmniLeads | DESCARTE / BUZON / AGENDADO PARA SEGUIMIENTO |
| Contactación | OmniLeads | Contactado / Contestador / Cliente no atiende / etc |
| Intentos | OmniLeads | Cantidad de intentos realizados (0-3+) |

---

## Estructura del repo

```
campaign-manager/
├── index.html     # App completa (frontend)
├── Code.gs        # Backend Google Apps Script
└── README.md      # Este archivo
```

---

## Notas

- El historial de campañas se guarda en `localStorage` del browser y también se registra en la Sheet (hoja HISTORIAL)
- Si usás la app sin conectar Apps Script, funciona igual pero solo en modo local (sin persistencia en Drive)
- El merge es acumulativo: podés subir resultados parciales varias veces, siempre pisa con los datos más nuevos
