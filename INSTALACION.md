# 📘 Guía de Instalación Paso a Paso

## Requisitos del Sistema

Antes de comenzar, asegúrate de tener instalado:

1. **Node.js** (versión 18 o superior)
   - Descarga desde: https://nodejs.org/
   - Verifica la instalación: `node --version`

2. **MySQL** (versión 5.7 o superior)
   - Descarga desde: https://dev.mysql.com/downloads/mysql/
   - O usa XAMPP/WAMP que incluyen MySQL

## Paso 1: Preparar la Base de Datos

### Opción A: Usando línea de comandos

```bash
# Conectarse a MySQL
mysql -u root -p

# Importar la base de datos
mysql -u root -p < database.sql
```

### Opción B: Usando phpMyAdmin

1. Abre phpMyAdmin en tu navegador
2. Crea una nueva base de datos llamada `inventario_db`
3. Selecciona la base de datos
4. Ve a la pestaña "Importar"
5. Selecciona el archivo `database.sql`
6. Haz clic en "Continuar"

### Opción C: Usando MySQL Workbench

1. Abre MySQL Workbench
2. Conecta a tu servidor MySQL
3. Ve a Server → Data Import
4. Selecciona "Import from Self-Contained File"
5. Busca el archivo `database.sql`
6. Haz clic en "Start Import"

## Paso 2: Configurar el Proyecto

### 2.1 Extraer los Archivos

Descomprime el proyecto en una carpeta de tu elección, por ejemplo:
- Windows: `C:\inventario-nextjs`
- Mac/Linux: `~/inventario-nextjs`

### 2.2 Configurar Variables de Entorno

1. En la carpeta del proyecto, copia el archivo `.env.example` y renómbralo a `.env.local`

2. Abre `.env.local` con un editor de texto y configura tus credenciales:

```env
DB_HOST=localhost
DB_USER=root
DB_PASSWORD=tu_contraseña_mysql
DB_NAME=inventario_db
DB_PORT=3306
```

**Importante**: Reemplaza `tu_contraseña_mysql` con tu contraseña real de MySQL.

## Paso 3: Instalar Dependencias

Abre una terminal o símbolo del sistema en la carpeta del proyecto:

### Windows (CMD o PowerShell)
```cmd
cd C:\inventario-nextjs
npm install
```

### Mac/Linux (Terminal)
```bash
cd ~/inventario-nextjs
npm install
```

Este proceso descargará e instalará todas las dependencias necesarias. Puede tomar varios minutos.

## Paso 4: Ejecutar la Aplicación

### Modo Desarrollo (para probar)

```bash
npm run dev
```

Abre tu navegador en: `http://localhost:3000`

### Modo Producción (para uso real)

```bash
npm run build
npm start
```

## Paso 5: Configurar como Servicio (Opcional)

### Windows - Crear Acceso Directo

1. Crea un archivo `iniciar.bat` en la carpeta del proyecto:

```batch
@echo off
cd /d "%~dp0"
npm start
pause
```

2. Haz doble clic en `iniciar.bat` para ejecutar la aplicación

### Linux/Mac - Crear Script de Inicio

1. Crea un archivo `iniciar.sh`:

```bash
#!/bin/bash
cd "$(dirname "$0")"
npm start
```

2. Dale permisos de ejecución:
```bash
chmod +x iniciar.sh
```

3. Ejecuta: `./iniciar.sh`

## Solución de Problemas Comunes

### Error: "Cannot find module"
**Solución**: Ejecuta `npm install` nuevamente

### Error: "ECONNREFUSED" al conectar a MySQL
**Solución**: 
- Verifica que MySQL esté ejecutándose
- Confirma que la contraseña en `.env.local` sea correcta
- Asegúrate de que el puerto 3306 no esté bloqueado

### Error: "Port 3000 already in use"
**Solución**: 
- Cierra otras aplicaciones que usen el puerto 3000
- O cambia el puerto en `package.json`:
  ```json
  "dev": "next dev -p 3001"
  ```

### La aplicación carga pero no muestra datos
**Solución**:
- Verifica que la base de datos se importó correctamente
- Revisa las credenciales en `.env.local`
- Mira la consola del navegador (F12) para ver errores

## Verificación de la Instalación

Si todo funciona correctamente, deberías ver:

1. ✅ Dashboard con tarjetas de resumen
2. ✅ Pestaña de Productos con la tabla
3. ✅ Pestaña de Clientes
4. ✅ Pestaña de Deudas
5. ✅ Pestaña de Reportes

## Acceso desde Otras Computadoras en la Red Local

Para acceder desde otras computadoras en tu red:

1. Encuentra tu IP local:
   - Windows: `ipconfig` (busca IPv4)
   - Mac/Linux: `ifconfig` o `ip addr`

2. En otras computadoras, accede a: `http://TU_IP:3000`
   - Ejemplo: `http://192.168.1.100:3000`

3. Asegúrate de que el firewall permita el puerto 3000

## Backup y Seguridad

### Hacer Backup de la Base de Datos

```bash
mysqldump -u root -p inventario_db > backup.sql
```

### Restaurar Backup

```bash
mysql -u root -p inventario_db < backup.sql
```

### Recomendaciones de Seguridad

1. 🔒 Cambia la contraseña predeterminada de MySQL
2. 🔒 No compartas tu archivo `.env.local`
3. 🔒 Haz backups regulares de la base de datos
4. 🔒 Mantén Node.js actualizado

## Siguientes Pasos

Una vez instalado:

1. **Registra Productos**: Ve a la pestaña Productos y agrega tu inventario
2. **Registra Clientes**: Agrega tus clientes en la pestaña Clientes
3. **Crea Deudas**: Registra ventas a crédito desde la pestaña Deudas
4. **Genera Reportes**: Explora los reportes disponibles

## Contacto y Soporte

Para ayuda adicional:
- Revisa el archivo README.md
- Consulta la documentación de Next.js: https://nextjs.org/docs
- Documentación de MySQL: https://dev.mysql.com/doc/

---

¡Feliz gestión de inventario! 🎉
