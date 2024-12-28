# Generación y Detección de Objetos en Imágenes con Stable Diffusion y YOLO

Este notebook de Jupyter demuestra cómo generar imágenes utilizando Stable Diffusion y realizar detección de objetos usando el modelo YOLO. El notebook combina dos potentes modelos de aprendizaje profundo para crear y analizar imágenes.

## Requisitos Previos

Antes de ejecutar este notebook, asegúrate de tener:
- Una cuenta de Google Colab o un entorno local con soporte GPU
- Python 3.6 o superior
- Una cuenta de Hugging Face para acceder a los modelos

## Bibliotecas Necesarias
```
huggingface_hub
diffusers
transformers
torch
Pillow
requests
```

## Guía Paso a Paso

### 1. Configuración Inicial
- Instalación de Hugging Face Hub CLI
- Inicio de sesión en tu cuenta de Hugging Face
- Instalación de la biblioteca Diffusers para Stable Diffusion

### 2. Generación de Imágenes con Stable Diffusion
- Carga del modelo Stable Diffusion v1.5
- Traslado del modelo a GPU (CUDA) para procesamiento más rápido
- Generación de imágenes usando prompts de texto
- Guardado de imágenes generadas en almacenamiento local

Ejemplo de uso:
```python
prompt = "una foto de un astronauta montando a caballo en marte"
image = pipe(prompt).images[0]
image.save("astronauta_caballo.png")
```

### 3. Detección de Objetos con YOLO
- Instalación de la biblioteca Transformers
- Carga del modelo YOLOS-tiny y el procesador de imágenes
- Procesamiento de imágenes para detección de objetos
- Análisis de resultados con umbrales de confianza

La función `detectar_objetos` admite:
- Archivos de imagen locales
- Imágenes desde URLs
- Devuelve objetos detectados con:
  - Clase del objeto
  - Puntuación de confianza
  - Coordenadas del cuadro delimitador

## Documentación de la Función

### detectar_objetos(ruta_imagen)
Detecta objetos en imágenes utilizando el modelo YOLOS.

Parámetros:
- `ruta_imagen` (str): Ruta a imagen local o URL

Devuelve:
- Lista de diccionarios que contienen:
  - `objeto`: Clase del objeto detectado
  - `confianza`: Puntuación de confianza (0-1)
  - `ubicacion`: Coordenadas del cuadro delimitador [x1, y1, x2, y2]

## Ejemplos de Uso

1. Para imágenes locales:
```python
ruta_local = "/ruta/a/tu/imagen.png"
resultados = detectar_objetos(ruta_local)
```

2. Para imágenes desde URL:
```python
url = "http://images.cocodataset.org/val2017/000000039769.jpg"
resultados = detectar_objetos(url)
```

## Formato de Salida
Los resultados de la detección se imprimen en el siguiente formato:
```
Se detectó [objeto] con una confianza de [confianza] en la ubicación [ubicacion]
```

## Notas
- El umbral de detección de objetos está establecido en 0.9 para resultados de alta confianza
- El modelo utiliza CUDA para aceleración GPU cuando está disponible
- Las imágenes se procesan automáticamente al formato correcto para ambos modelos

## Manejo de Errores
El notebook incluye manejo de errores para:
- Errores de archivo no encontrado
- Problemas de acceso a URL
- Problemas de carga de imágenes

## Licencia
Este notebook utiliza modelos de Hugging Face:
- Stable Diffusion v1.5 (sd-legacy/stable-diffusion-v1-5)
- YOLOS-tiny (hustvl/yolos-tiny)

Por favor, asegúrate de cumplir con las respectivas licencias de los modelos al usar este notebook.
