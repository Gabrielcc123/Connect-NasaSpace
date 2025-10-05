# 🚀 Despliegue en Render.com - NASA Fire Monitor

## Pasos para desplegar en Render

### 1. Preparar el repositorio
- Sube tu proyecto a GitHub, GitLab o Bitbucket
- Asegúrate de que el archivo `render.yaml` esté en la raíz del repositorio

### 2. Crear cuenta en Render
1. Ve a [render.com](https://render.com)
2. Regístrate con tu cuenta de GitHub/GitLab
3. Conecta tu repositorio

### 3. Configurar el servicio
1. En el dashboard de Render, haz clic en "New +"
2. Selecciona "Web Service"
3. Conecta tu repositorio
4. Render detectará automáticamente el archivo `render.yaml`

### 4. Configurar variables de entorno
En la sección "Environment Variables" de Render, agrega:
```
NODE_ENV = production
PORT = 10000
FIRMS_MAP_KEY = tu_clave_de_nasa_aqui
```

### 5. Configuración del servicio
- **Name**: nasa-fire-monitor (o el nombre que prefieras)
- **Environment**: Node
- **Plan**: Free (para empezar)
- **Build Command**: `cd CONTROLLERFINALFINAL/backend && npm install`
- **Start Command**: `cd CONTROLLERFINALFINAL/backend && npm start`

### 6. Desplegar
1. Haz clic en "Create Web Service"
2. Render comenzará a construir y desplegar tu aplicación
3. El proceso tomará unos minutos

### 7. Verificar el despliegue
Una vez completado, tendrás una URL como:
`https://nasa-fire-monitor.onrender.com`

**Endpoints disponibles:**
- `https://tu-app.onrender.com/` - Interfaz web
- `https://tu-app.onrender.com/api` - Información de la API
- `https://tu-app.onrender.com/api/health` - Estado del servicio
- `https://tu-app.onrender.com/api/incendios?days=3&source=VIIRS_SNPP_NRT&region=bolivia` - Datos de incendios

## ⚠️ Consideraciones importantes

### Plan Gratuito de Render
- **Sleep mode**: La app se "duerme" después de 15 minutos de inactividad
- **Cold start**: El primer acceso después del sleep puede tardar 30-60 segundos
- **Límites**: 750 horas/mes, 512MB RAM

### Para evitar el sleep mode
1. **Plan de pago**: $7/mes elimina el sleep mode
2. **Uptime monitoring**: Usa servicios como UptimeRobot para hacer ping cada 14 minutos
3. **Cron job**: Configura un cron job que haga requests periódicos

### Monitoreo
- Render proporciona logs en tiempo real
- Puedes ver el estado del servicio en el dashboard
- Configura alertas por email si el servicio falla

## 🔧 Troubleshooting

### Error: "Build failed"
- Verifica que `package.json` tenga el script `start`
- Asegúrate de que todas las dependencias estén en `dependencies` (no `devDependencies`)

### Error: "Service failed to start"
- Revisa los logs en Render
- Verifica que `FIRMS_MAP_KEY` esté configurada
- Asegúrate de que el puerto sea dinámico (usar `process.env.PORT`)

### App se duerme frecuentemente
- Considera actualizar al plan de pago
- Implementa un endpoint de health check
- Usa un servicio de monitoreo externo

## 📈 Escalabilidad

### Para mayor tráfico
1. **Upgrade plan**: Más recursos y sin sleep mode
2. **CDN**: Usa Cloudflare para cachear assets estáticos
3. **Database**: Si necesitas persistencia, conecta una base de datos
4. **Load balancing**: Para múltiples instancias

### Optimizaciones
- Implementa cache más agresivo
- Usa Redis para cache distribuido
- Optimiza las consultas a la API de NASA
