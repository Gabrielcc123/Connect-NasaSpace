## Despliegue de "NASA 2.0" (Backend + Frontend)

El backend Express sirve el frontend estático desde `CONTROLLERFINALFINAL/frontend`. El contenedor expone el puerto 4000 y publica una sola app que incluye API y UI.

### Requisitos
- Docker 24+ y Docker Compose v2
- Clave de API `FIRMS_MAP_KEY` válida

### Preparación
1. Copia el ejemplo de variables y edítalo:
   ```bash
   cp CONTROLLERFINALFINAL/backend/.env.example CONTROLLERFINALFINAL/backend/.env
   # Edita FIRMS_MAP_KEY en ese archivo
   ```

2. (Opcional) Revisa el puerto en `CONTROLLERFINALFINAL/backend/.env` (predeterminado 4000).

### Ejecutar en producción (Linux VPS)
```bash
docker compose up -d --build
```

- App disponible en: `http://<tu-ip>:4000`
- Endpoints útiles:
  - UI: `/`
  - API info: `/api`
  - Health: `/api/health`
  - Incendios: `/api/incendios?days=3&source=VIIRS_SNPP_NRT&region=bolivia`

Logs y gestión:
```bash
docker compose logs -f
docker compose ps
docker compose restart
docker compose down        # detener
```

### Windows Server (Docker Desktop)
1. Instala Docker Desktop y habilita WSL2.
2. Clona el repo en `C:\ruta\al\proyecto`.
3. En PowerShell dentro del directorio del proyecto:
   ```powershell
   copy CONTROLLERFINALFINAL\backend\.env.example CONTROLLERFINALFINAL\backend\.env
   notepad CONTROLLERFINALFINAL\backend\.env  # agrega tu FIRMS_MAP_KEY
   docker compose up -d --build
   ```
4. Accede a `http://localhost:4000` o la IP del servidor.

### Seguridad y producción
- Coloca un proxy (Nginx/Caddy/Traefik) delante si deseas HTTPS.
- Mantén tu `.env` fuera del control de versiones.
- El rate limit está en 100 req/hora por IP (ver `server.js`). Ajusta si es necesario.

### Personalizaciones
- Cambia el puerto publicando: `- "80:4000"` en `docker-compose.yml` si quieres exponer en 80/443 (con proxy).
- Si el frontend se separa, elimina `app.use(express.static(...))` y sirve la UI con Nginx; actualiza CORS en `server.js`.


