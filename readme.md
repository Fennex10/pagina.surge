````markdown
# Página Surge – Despliegue Automático

Este repositorio contiene una página web simple en HTML que se despliega automáticamente en Surge.sh usando GitHub Actions.

---

## 🧾 Contenido del repositorio

- `index.html` — página principal con contenido de ejemplo  
- `.github/workflows/main.yaml` — configuración del flujo de trabajo (GitHub Actions) para desplegar en Surge cuando se hace push a la rama `main`

---

## 🚀 Flujo de trabajo / CI-CD

1. Haces cambios localmente en `index.html` (o agregas más archivos).  
2. Haces `git add`, `git commit` y `git push` a la rama `main`.  
3. GitHub detecta el push y ejecuta la acción definida en `.github/workflows/main.yaml`.  
4. La acción:
   - descarga el código (`actions/checkout`)
   - instala Node.js
   - instala el paquete `surge`
   - ejecuta `surge ./ --domain <tu-dominio>.surge.sh --token ${{ secrets.SURGE_TOKEN }}`
5. Si todo sale bien, tu sitio queda publicado (o actualizado) en **Surge.sh** bajo el dominio configurado.

---

## 🔧 Configuración necesaria para que funcione

### 1. Instalar `surge` localmente (para probar despliegues manuales)
```bash
npm install --global surge
````

### 2. Crear cuenta / iniciar sesión en Surge

```bash
surge login
```

Al ejecutar, te pedirá tu correo y contraseña (aunque no se visualiza mientras tipeas).

### 3. Obtener el token de Surge

```bash
surge token
```

Copia el token que genera — lo necesitarás para el siguiente paso.

### 4. Configurar el secreto en GitHub

* Ve a tu repositorio en GitHub → **Settings** → **Secrets and variables** → **Actions**
* Crea un nuevo secret:

  * **Name:** `SURGE_TOKEN`
  * **Value:** el token que obtuviste con `surge token`

### 5. Ajustar el dominio en el archivo `.github/workflows/main.yaml`

Dentro de:

```yaml
run: surge ./ --domain dewrin-pagina.surge.sh --token $SURGE_TOKEN
```

Cambia `dewrin-pagina.surge.sh` por el dominio que quieras usar (o que te haya asignado Surge). Ese será el dominio donde se verá tu página.

---

## 📦 Cómo probar localmente antes de enviar

1. Asegúrate de tener `surge` instalado:
   `surge --version`

2. Desde el directorio del proyecto, prueba:

   ```bash
   surge ./ --domain prueba-temporal.surge.sh
   ```

   Esto desplegará tu versión actual para ver que funcione correctamente antes de empujar cambios a `main`.

---

## 📎 Enlaces importantes

* GitHub Actions → para ver ejecuciones y logs
* Surge.sh → para gestionar tus dominios y ver tu página pública

---

## ✅ Resultado esperado

* Cada vez que hagas push a la rama `main`, se active el workflow
* El contenido del repo se despliegue automáticamente en Surge
* Tu página esté accesible públicamente en el dominio que configuraste
