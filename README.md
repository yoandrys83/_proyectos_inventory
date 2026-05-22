# Sistema de Gestión de Inventario — v6.1 INTEGRADA

> Esta versión incorpora todas las funcionalidades de `inventario-v6-FINAL` más las mejoras avanzadas de `inventario-v6.1-FUNCIONALIDADES-AVANZADAS`.

---

## 🆕 Novedades en v6.1

| Funcionalidad | Descripción |
|---|---|
| 💱 **Monedas Dinámicas** | Agrega, edita o desactiva monedas desde la UI sin tocar código |
| 🧾 **Historial de Pagos Editable** | Visualiza, edita y elimina pagos con recálculo automático |
| 🔗 **Monedas Relacionales** | `productos` y `deudas` usan `moneda_id` (FK) en lugar de ENUM |
| 📡 **API de Monedas** | CRUD completo vía `/api/monedas` |
| 🔄 **Triggers de Sincronía** | Columna `moneda` (legacy) se sincroniza automáticamente |

---

## 🚀 Instalación Rápida

### 1. Base de Datos (instalación limpia)

```bash
mysql -u root -p < database_v6_1_COMPLETA.sql
```

> Si venías de una versión anterior, ejecuta primero:
> ```bash
> mysqldump -u root -p inventario_db > backup_antes_v6.1.sql
> ```

### 2. Variables de Entorno

Crea `.env.local` en la raíz:

```env
DB_HOST=localhost
DB_USER=root
DB_PASSWORD=tu_contraseña
DB_NAME=inventario_db
DB_PORT=3306
```

### 3. Instalar y Ejecutar

```bash
npm install
npm run dev
# → http://localhost:3000
```

---

## 📁 Estructura del Proyecto

```
inventario-v6-integrado/
├── app/
│   ├── api/
│   │   ├── monedas/route.ts          ← NUEVO v6.1
│   │   ├── pagos/route.ts            ← ACTUALIZADO v6.1
│   │   └── ... (resto de APIs)
│   └── page.tsx                      ← ACTUALIZADO con nuevas tabs
├── components/
│   ├── HistorialPagosPage.tsx        ← NUEVO v6.1
│   ├── MonedasPage.tsx               ← NUEVO v6.1
│   └── ... (resto de componentes)
├── types/index.ts                    ← ACTUALIZADO con tipos Moneda
└── database_v6_1_COMPLETA.sql        ← BASE DE DATOS INTEGRADA ⭐
```

---

## 🗄️ Cambio Clave en BD: ENUM → Tabla Relacional

**Antes (v6):**
```sql
productos.moneda = ENUM('USD', 'CUP', 'EUR')   -- Fijo, no extensible
```

**Ahora (v6.1):**
```sql
productos.moneda_id → monedas.id               -- Dinámico y extensible
```

La columna `moneda` (texto) se mantiene como legado y se sincroniza mediante triggers.

---

## 💱 Agregar Nueva Moneda

**Desde la interfaz:** Ir a pestaña **"Monedas"** → Nueva Moneda → Código + Nombre + Símbolo → Guardar.

**Desde SQL:**
```sql
INSERT INTO monedas (codigo, nombre, simbolo, activa, orden_visualizacion)
VALUES ('MXN', 'Peso Mexicano', '$', TRUE, 4);
```

---

## 🧾 Historial de Pagos Editable

- **Editar monto/notas:** doble clic → editar → Enter
- **Eliminar pago:** clic en 🗑️ → confirmar
- El estado de la deuda se **recalcula automáticamente**

---

## ⚠️ Notas

- Hacer backup antes de migrar
- Monedas en uso no se pueden eliminar (solo desactivar)
- Cambios en pagos son permanentes

---

**Versión:** 6.1 INTEGRADA | **Estado:** ✅ COMPLETO | **Fecha:** 13 Feb 2026
