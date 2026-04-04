# Backend AMAIRE - Sistema de Formularios

## 📋 Descripción

Backend Node.js + Express que maneja 3 formularios del sitio AMAIRE Residencial:
- **Formulario 1** (`lead-form-1`): Solicitud de información
- **Formulario 2** (`lead-form-2`): Descarga de brochure
- **Formulario 3** (`lead-form-3`): Contacto

## 🔧 Configuración Actual

### ✅ ACTIVO: Google Sheets
Los formularios envían datos a Google Sheets mediante Apps Script.

**URL del Script:** 
```
https://script.google.com/macros/s/AKfycbzLDT_OwG9bWbU_rHf9MdeWETksfPmN2byXwbywSYW0jutUT_SPcdC9Mn5mOxOE7FEx1Q/exec
```

**Ubicación en código:** Línea 11 de `server.js`

### ✅ ACTIVO: Salesforce
El envío a Salesforce está activo en ambos endpoints del backend.

## 📁 Estructura de Archivos

```
AMAIRE-BACKEND/
├── server.js          # Servidor principal con endpoints
├── package.json       # Dependencias del proyecto
├── public/
│   └── brochure.pdf  # PDF descargable
└── README.md         # Este archivo
```

## 🔐 Validaciones Implementadas

El backend valida:
- ✅ Nombre: Solo letras, mínimo 4 caracteres
- ✅ Teléfono: 8-10 dígitos numéricos
- ✅ Email: Formato válido
- ✅ reCAPTCHA: Token válido de Google
- ✅ Campos obligatorios: Todos los campos de Salesforce
- ✅ Aviso de privacidad: Checkbox aceptado

## 🌐 CORS Configurado

Orígenes permitidos:
- `https://amaire.mx`
- `https://amairejaver.mx`

## � Campos que se envían a Google Sheets

```javascript
{
  first_name: "Nombre del usuario",
  phone: "5512345678",
  email: "usuario@example.com",
  '00N3l00000Q7A54': "CUMBRES ALLEGRO DPTOS",  // FraccionamientoInterno
  '00N3l00000Q7A57': "Landing_Estado_Mexico",  // Fuente
  '00N3l00000Q7A4k': "Información",  // Tipo de solicitud
  '00N3l00000Q7A4n': "Medios Digitales",  // Canal de Venta
  '00N3l00000Q7A5S': "Micrositios"  // Subcanal de Venta
}
```

## �📊 Flujo de Datos

```
Frontend (formulario) 
    ↓
Backend (validación + sanitización)
    ↓
Google Sheets ✅ (activo)
    ↓
Salesforce ✅ (activo)
    ↓
Respuesta al usuario + descarga PDF (si aplica)
```

## 🛠️ Endpoints

### POST `/enviar`
- **Uso:** Formularios 1 y 3 (sin descarga)
- **Response:** `{ message: 'Formulario enviado correctamente' }`

### POST `/enviarYDescargar`
- **Uso:** Formulario 2 (con descarga de brochure)
- **Response:** `{ message: 'Formulario enviado correctamente', pdfUrl: '/brochure.pdf' }`

## 📝 Notas Importantes

1. **Google Sheets siempre estará activo** - Es el sistema principal de registro
2. **Salesforce está activo** - Se envía junto con Google Sheets
3. **El PDF debe estar en** `/public/brochure.pdf`
4. **reCAPTCHA v2** - Site key: `6LeYyF4rAAAAAHybD_FuW3g0NiJJwUX7_VnfiJLv`

## 🐛 Debugging

Si hay errores, revisa:
1. Consola del servidor: `console.error` muestra los errores
2. Network tab del navegador: Verifica la respuesta del backend
3. Google Sheets: Confirma que los datos lleguen
4. reCAPTCHA: Verifica que el token se envíe correctamente

---

**Desarrollado para:** AMAIRE Residencial  
**Última actualización:** Abril 2026
