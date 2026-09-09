# yovito.shop

Sitio estático de Yovito. Sin build, sin dependencias: son tres archivos que se
suben tal cual a GitHub Pages.

```
index.html   la página completa (HTML + CSS + JS en un solo archivo)
404.html     página de error
CNAME        le dice a GitHub Pages que el dominio es yovito.shop
.nojekyll    evita que GitHub procese el sitio con Jekyll
```

---

## 1. Publicarlo en GitHub Pages (5 minutos, $0)

1. Crea un repositorio nuevo llamado **`yovito`** en tu cuenta `zunzord`.
   Puede ser público (GitHub Pages gratis exige público en cuentas Free).
2. Sube estos archivos a la raíz del repositorio, en la rama `main`.
   Desde la web: *Add file → Upload files*, arrastra los cuatro y confirma.
   Desde tu máquina:

   ```bash
   git init
   git add .
   git commit -m "Sitio inicial de Yovito"
   git branch -M main
   git remote add origin https://github.com/zunzord/yovito.git
   git push -u origin main
   ```

3. En el repo: **Settings → Pages**.
   - *Source*: `Deploy from a branch`
   - *Branch*: `main` / carpeta `/ (root)` → **Save**
4. En esa misma pantalla, en *Custom domain*, escribe `yovito.shop` y guarda.
   (El archivo `CNAME` ya lo deja puesto, así que puede aparecer solo.)
5. Espera a que GitHub verifique el dominio y marca **Enforce HTTPS**.
   El certificado tarda entre unos minutos y 24 horas en emitirse.

Mientras el dominio no apunte todavía, el sitio ya se ve en
`https://zunzord.github.io/yovito/`.

---

## 2. Cambiar el DNS en Hostinger

Hoy `yovito.shop` apunta a Shopify (`23.227.38.65`) y la tienda ya no existe,
por eso el navegador muestra un error de certificado. Hay que reemplazar esos
registros.

En **hPanel → Dominios → yovito.shop → DNS / Nameservers → Registros DNS**:

**Borra** todo registro `A` o `CNAME` que apunte a Shopify
(`23.227.38.65`, `23.227.38.74`, `shops.myshopify.com`).

**Crea** estos cuatro registros A para la raíz:

| Tipo | Nombre | Apunta a          | TTL   |
|------|--------|-------------------|-------|
| A    | `@`    | `185.199.108.153` | 14400 |
| A    | `@`    | `185.199.109.153` | 14400 |
| A    | `@`    | `185.199.110.153` | 14400 |
| A    | `@`    | `185.199.111.153` | 14400 |

**Y uno para el www:**

| Tipo  | Nombre | Apunta a         | TTL   |
|-------|--------|------------------|-------|
| CNAME | `www`  | `zunzord.github.io.` | 14400 |

Opcional, si quieres IPv6, agrega también cuatro registros `AAAA` en `@`:
`2606:50c0:8000::153`, `2606:50c0:8001::153`, `2606:50c0:8002::153`,
`2606:50c0:8003::153`.

El cambio tarda entre 15 minutos y unas horas en propagarse.

---

## 3. Encender el formulario de correo

El formulario está listo pero apagado a propósito: mientras no haya servicio de
correo configurado, la página muestra “Muy pronto” en vez de un formulario que
no funciona.

Para encenderlo, abre `index.html`, busca cerca del final:

```js
var SUSCRIPCION_URL = "";
```

y pega ahí la URL de tu formulario:

- **Buttondown** (gratis hasta 100 suscriptores) →
  `https://buttondown.email/api/emails/embed-subscribe/TU_USUARIO`
- **MailerLite** (gratis hasta 1.000) → la `action` del formulario embebido
- **Formspree** (gratis, 50 envíos/mes) → `https://formspree.io/f/TU_ID`

Guarda, sube el cambio, y el formulario aparece solo.

---

## 4. Cambiar el contenido

Todo el texto está en `index.html` en español y en claro; no hay plantillas.
Las tres tarjetas de proyectos tienen un marcador **“Foto pendiente”**:
reemplaza cada bloque `<svg>…</svg>` por
`<img src="fotos/nombre.jpg" alt="descripción">` cuando tengas las fotos
reales, y borra la línea `<span class="slot">Foto pendiente</span>`.

Recuerda las reglas acordadas: solo el apodo, sin apellido, sin escuela,
sin fachada de la casa, y ella decide qué se publica.
