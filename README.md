# WATESITE Sensors service

Repositorio independiente del microservicio `sensors` extra?do de [WATESITE](https://github.com/cuentapicentral-sys/WATESITE). La historia del directorio del servicio se conserva; los m?dulos compartidos necesarios est?n incluidos para que este repositorio se pueda probar y construir de forma independiente.

## Local

```powershell
python -m pip install -r requirements.txt -r requirements-dev.txt
$env:SUPABASE_URL = "https://example.supabase.co"
$env:SUPABASE_SERVICE_ROLE_KEY = "replace_me"
python -m pytest -q
python -m uvicorn services.sensors.main:app --reload --port 8000
```

## Docker y despliegue

```powershell
docker build -t watesite-sensors:local .
docker run --rm -p 8000:8000 -e SUPABASE_URL=https://example.supabase.co -e SUPABASE_SERVICE_ROLE_KEY=replace_me watesite-sensors:local
```

El workflow valida en cada pull request y publica la imagen en GHCR al integrar en `main`. Render puede conectar directamente a este repositorio y usar `render.yaml`; el Blueprint requiere configurar `SUPABASE_URL`, `SUPABASE_SERVICE_ROLE_KEY` y `RABBITMQ_URL` en Render. No pongas esos valores en Git. El despliegue remoto y su endpoint real deben verificarse en Render; el workflow no finge haberlo confirmado.

El c?digo com?n de `services/` se copia para permitir despliegues independientes. Los cambios futuros a esos m?dulos compartidos deben sincronizarse deliberadamente con los repositorios que los usan.
