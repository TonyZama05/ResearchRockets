# 🚀 Research Rockets — SSOT

**Sistema de Seguimiento de Operaciones** para el Fondo BBVA de la Clínica de Inversión, Tec de Monterrey.

**URL del equipo:** `https://[tu-usuario].github.io/research-rockets/`

---

## Setup inicial (una sola vez — lo hace un integrante)

### 1. Crear el repositorio en GitHub

```bash
git clone https://github.com/[tu-usuario]/research-rockets.git
cd research-rockets
# Copia los archivos de este repo aquí
git add .
git commit -m "feat: SSOT inicial"
git push origin main
```

### 2. Activar GitHub Pages

1. Ve a **Settings → Pages**
2. Source: **Deploy from a branch**
3. Branch: `main` / `/ (root)`
4. Click **Save**
5. En ~2 minutos tu SSOT está en `https://[tu-usuario].github.io/research-rockets/`

### 3. Crear el proyecto Firebase

1. Ve a [console.firebase.google.com](https://console.firebase.google.com)
2. **Crear un proyecto** → nombre: `research-rockets-fondo`
3. **Build → Firestore Database → Crear base de datos**
   - Modo: **Prueba** (30 días sin restricciones — suficiente para la clínica)
   - Región: `us-central1`
4. **Configuración del proyecto** (⚙️) → **Tus apps** → ícono `</>` → Registrar app como `ssot`
5. Copia el objeto `firebaseConfig` — lo necesitas en el paso siguiente

### 4. Conectar Firebase en el SSOT

1. Abre `https://[tu-usuario].github.io/research-rockets/`
2. Ve a **Configuración** en el sidebar
3. En la sección **Sincronización Firebase**, pega el JSON:

```json
{
  "apiKey": "AIzaSy...",
  "authDomain": "research-rockets-fondo.firebaseapp.com",
  "projectId": "research-rockets-fondo",
  "storageBucket": "research-rockets-fondo.appspot.com",
  "messagingSenderId": "123456789",
  "appId": "1:123456789:web:abc123"
}
```

4. Click **Guardar y conectar Firebase**
5. El punto en la barra superior debe volverse 🟢 **Sincronizado**
6. **Comparte este mismo JSON** con todo el equipo (WhatsApp/Slack) para que todos se conecten

---

## Flujo de trabajo del equipo

```
Cualquier integrante registra una orden
    → se guarda en Firebase en ~500ms
    → todos los demás lo ven automáticamente
    → sin recargar la página
```

## Actualizar el SSOT (cuando hay cambios de código)

```bash
# Edita index.html con la nueva versión
git add index.html
git commit -m "feat: actualización SSOT [descripción]"
git push origin main
# GitHub Pages se actualiza automáticamente en ~1-2 minutos
```

Los datos en Firebase son independientes del código — actualizar el HTML **no borra las órdenes**.

---

## Estructura del proyecto

```
research-rockets/
├── index.html          ← El SSOT completo (todo en un archivo)
├── README.md           ← Este archivo
└── .github/
    └── workflows/
        └── deploy.yml  ← Auto-deploy en cada push
```

## Reglas de Firebase recomendadas

Una vez terminada la clínica, cambia las reglas de Firestore de "modo prueba" a:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /fondos/{fondoId} {
      allow read, write: if true; // Cambiar por auth si se quiere más seguridad
    }
  }
}
```

---

## Integrantes

| Nombre | Rol |
|--------|-----|
| Tony Zamarripa | Líder técnico |
| ... | ... |

**Clínica Empresarial BBVA · Tec de Monterrey · 2026**
