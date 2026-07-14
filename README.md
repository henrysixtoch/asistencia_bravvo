# Grupo Bravvo S.A.C — Sistema de Asistencia
### Algoritmo de Cristian · Flask · Render

## Estructura
```
bravvo_asistencia/
├── app.py              ← Backend Flask + Algoritmo de Cristian
├── requirements.txt    ← Dependencias
├── Procfile            ← Comando para Render
├── templates/
│   ├── index.html      ← Vista empleado (registro de asistencia)
│   └── profesor.html   ← Panel de control del administrador
└── README.md
```

## Cómo desplegar en Render

1. Sube este proyecto a un repositorio GitHub (puede ser privado)
2. Ve a https://render.com → New → Web Service
3. Conecta tu repositorio
4. Configura:
   - **Build Command:** `pip install -r requirements.txt`
   - **Start Command:** `gunicorn app:app`
   - **Environment:** Python 3
5. Deploy → Render te da una URL pública HTTPS

## Cómo probar (escenario de la actividad)

| Dispositivo       | URL                              |
|-------------------|----------------------------------|
| Tu PC (navegador) | `https://tu-app.onrender.com/`   |
| Ubuntu VM         | `https://tu-app.onrender.com/`   |
| Panel profesor    | `https://tu-app.onrender.com/profesor` |

## Algoritmo de Cristian implementado

```
T0 = cliente registra hora local antes de enviar GET /api/tiempo
     → servidor responde con T_servidor

T1 = cliente registra hora local al recibir respuesta

RTT = T1 - T0
T_estimado = T_servidor + RTT/2   ← hora sincronizada

Incertidumbre = ±RTT/2
```

## Rutas disponibles

| Método | Ruta                  | Descripción                     |
|--------|-----------------------|---------------------------------|
| GET    | `/`                   | Formulario del empleado         |
| GET    | `/profesor`           | Panel de control                |
| GET    | `/api/tiempo`         | Hora del servidor (Cristian)    |
| POST   | `/api/registrar`      | Registrar asistencia            |
| GET    | `/api/registros`      | Listar todos los registros      |
| GET    | `/api/exportar/pdf`   | Descargar reporte PDF           |
| GET    | `/api/exportar/excel` | Descargar reporte Excel         |
| DELETE | `/api/limpiar`        | Limpiar registros de sesión     |
