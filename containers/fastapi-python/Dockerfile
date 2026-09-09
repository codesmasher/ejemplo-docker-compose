FROM python:3.11-slim

# Evita que Python genere archivos .pyc y fuerza la salida de logs sin buffer
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

WORKDIR /app

# Solo copiamos e instalamos dependencias en la imagen
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Exponemos el puerto de Uvicorn
EXPOSE 8000

# El comando se ejecuta sobre la carpeta /app que vendrá montada por el volumen
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000", "--reload"]