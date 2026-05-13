# V3K Landing

Landing page one-page para el software de trazabilidad V3K (cannabis/cáñamo, Argentina).

## Stack
HTML + CSS vanilla + JS mínimo. Sin frameworks, sin build, sin dependencias.

## Estructura
```
v3k-landing/
├── index.html        # one-page completa
├── css/styles.css    # sistema de diseño
├── js/main.js        # nav mobile + acordeón FAQ + año footer
├── img/
│   ├── v3k-logo.png  # logo (copia del software)
│   └── favicon.svg
└── README.md
```

## Probar localmente

**Opción 1 — doble click**
Abrí `index.html` directamente con doble click. Funciona en `file://` porque no hay módulos JS ni fetch.

**Opción 2 — servidor local**
```powershell
cd C:\Users\llama\Claudecode\v3k-landing
python -m http.server 8000
```
Luego abrí `http://localhost:8000` en el navegador.

## Antes de deployar — completar placeholders

Buscar y reemplazar en `index.html`:
- `{{WHATSAPP_NUMBER}}` → número de WhatsApp con código de país sin `+` ni espacios. Ej: `5492611234567`
- `{{CONTACT_EMAIL}}` → email de contacto. Ej: `gonzalo@v3k.com.ar`

```powershell
(Get-Content index.html) -replace '\{\{WHATSAPP_NUMBER\}\}', '5492611234567' -replace '\{\{CONTACT_EMAIL\}\}', 'gonzalo@v3k.com.ar' | Set-Content index.html
```

## Deploy

**Netlify Drop** (más simple, sin cuenta requerida para el primer deploy)
1. Abrí https://app.netlify.com/drop
2. Arrastrá la carpeta `v3k-landing/` completa
3. Recibís una URL `*.netlify.app` al instante. Después podés conectar dominio propio.

**Vercel CLI**
```powershell
npm i -g vercel
cd C:\Users\llama\Claudecode\v3k-landing
vercel --prod
```

**GitHub Pages**
```powershell
cd C:\Users\llama\Claudecode\v3k-landing
git init
git add .
git commit -m "V3K landing v1"
git branch -M main
# crear repo en github.com, copiar URL
git remote add origin https://github.com/USUARIO/v3k-landing.git
git push -u origin main
# Settings → Pages → Source: main / root
```

## Personalización rápida

- **Color primario**: editar `--color-primary` en `css/styles.css:3`. Toda la paleta se actualiza.
- **Headline del hero**: `index.html` sección `.hero h1`.
- **CTAs WhatsApp**: cambiar el mensaje pre-llenado editando el parámetro `?text=` en los `<a href="https://wa.me/...">`.

## Verificación pre-deploy

- [ ] Render en desktop (1440px) y mobile (375px)
- [ ] Click en cada CTA WhatsApp abre el chat con mensaje pre-llenado
- [ ] FAQ se expande/colapsa correctamente
- [ ] Nav mobile (≤640px) abre con el botón hamburguesa
- [ ] Lighthouse: Performance + Accessibility ≥ 95
- [ ] Reemplazaste TODOS los `{{WHATSAPP_NUMBER}}` y `{{CONTACT_EMAIL}}`
- [ ] Agregaste `og:image` real (1200x630 px) si vas a compartirla en LinkedIn/WhatsApp

## Notas

- **No incluye screenshots reales del software.** En su lugar usa 3 mockups HTML/CSS embebidos que simulan: compliance dashboard, detalle de lote y log de notificaciones RPCCI. Esto evita riesgo de filtrar datos de operadores reales.
- **Logo source**: `C:\Users\llama\Claudecode\trazabilidad\static\img\v3k-logo.png` (copiado a `img/v3k-logo.png`). Si el logo se actualiza en el software, recopiarlo.
- **Aviso legal** en el footer: *"V3K no sustituye obligaciones del licenciatario"*. Validar texto con abogado antes de uso comercial.
