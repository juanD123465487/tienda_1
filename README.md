# TiendaPOS — Fase 2 (base técnica)

Base de desarrollo local para TiendaPOS con Fastify, TypeScript y PostgreSQL. Esta entrega prepara la estructura y las comprobaciones iniciales; **no es todavía un POS listo para cobrar ventas reales**.

## Qué incluye

- Backend Fastify + TypeScript.
- Validación de variables de entorno con Zod.
- Conexión PostgreSQL con `pg` y comprobación de salud de la base de datos.
- Migraciones SQL versionadas y script de semillas de desarrollo.
- Esquema inicial para usuarios/roles, productos/categorías, proveedores/entradas, cajas/turnos, ventas/pagos, movimientos de inventario y auditoría.
- PostgreSQL local opcional mediante Docker Compose.
- Prototipos originales copiados sin modificación a `prototipos/`.

## Requisitos

- Node.js 20 o superior y npm.
- PostgreSQL 15 o superior, o Docker Desktop/Engine para iniciar PostgreSQL con Compose.

## Inicio rápido (Windows PowerShell)

1. Instala Node.js LTS y Docker Desktop, si vas a usar Compose.
2. Abre PowerShell en la carpeta raíz `TiendaPOS-Fase2`.
3. En la raíz del proyecto, copia `.env.example` como `.env`; cambia `POSTGRES_PASSWORD` por una contraseña larga.
4. Copia `backend/.env.example` como `backend/.env` y verifica que `DATABASE_URL` use el mismo usuario, contraseña, base de datos y puerto del `.env` raíz.
5. Desde la carpeta raíz del proyecto, inicia PostgreSQL:

   ```powershell
   docker compose up -d db
   ```

6. Entra a `backend` e instala dependencias:

   ```powershell
   cd backend
   npm install
   ```

7. Ejecuta la migración y los datos de ejemplo:

   ```powershell
   npm run db:migrate
   npm run db:seed
   ```

8. Inicia el servidor:

   ```powershell
   npm run dev
   ```

9. Comprueba en el navegador:
   - `http://localhost:3000/health`
   - `http://localhost:3000/api/v1/health` (esta segunda ruta comprueba también PostgreSQL).

Para compilar y ejecutar la versión compilada: `npm run build` y `npm start`.

## Linux

Los mismos comandos funcionan en una terminal Bash. Asegúrate de que el usuario tenga permisos para usar Docker, si eliges esa opción.

## Acceso desde las dos cajas

Cuando el servidor esté en marcha, las cajas deben estar en la misma red local. En la configuración posterior del frontend se usará la dirección LAN del computador servidor, por ejemplo `http://192.168.1.20:3000` (es solo un ejemplo; no copies esa IP sin comprobar la tuya). Configura el firewall para permitir únicamente la red local y no publiques el puerto en internet.

## Seguridad y límites de esta fase

- No hay inicio de sesión ni permisos aplicados a rutas todavía.
- No hay endpoints para crear ventas o descontar inventario.
- Los productos de ejemplo son ficticios y deben reemplazarse antes de operar.
- No se debe usar en producción hasta implementar autenticación, autorización, transacciones de venta, cierre de caja, copias automáticas verificadas, monitoreo y pruebas.
- El `.env` contiene secretos locales y no debe compartirse ni subirse al repositorio.
- La copia de prototipos conserva el estado de origen; la UI todavía no está conectada a la API.

## Comandos

Desde `backend/`:

- `npm run dev` — servidor de desarrollo.
- `npm run typecheck` — verificación TypeScript.
- `npm run build` — compilar.
- `npm start` — servidor compilado.
- `npm run db:migrate` — ejecutar migraciones pendientes.
- `npm run db:seed` — cargar ejemplos de desarrollo.

Consulta `documentacion/ALCANCE-FASE-2.md` y `documentacion/DECISIONES-TECNICAS.md`.
