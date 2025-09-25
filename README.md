# Object Tracking and Counting Demo

## 1. Descripción
Este proyecto utiliza **YOLOv8** para detectar y trackear personas en un video, generar IDs de cada objeto y contar cuándo cruzan una línea virtual.  
Los resultados se guardan en un video con **bounding boxes** y un CSV con los eventos de cruce.

El flujo principal es:
1. Descargar un video de ejemplo (`test.mp4`).
2. Procesar el video frame por frame cada 0.5 segundos.
3. Detectar personas, asignar IDs persistentes y contar cruces de línea.
4. Generar video anotado y CSV con registros.

## 2. Requisitos
- Python >= 3.9
- ultralytics
- opencv-python-headless
- matplotlib
- yt-dlp
- torch

Instalación:
```bash
pip install -r requirements.txt
# En collab:
# pip install ultralytics opencv-python-headless matplotlib
# pip install -q yt-dlp
```
## 3. Uso
```bash
# Ejecutar el notebook o script:
python script_tracking.py # local
script_tracking.ipynb # collab
```
### Resultados generados:
- output_tracked.mp4 : Video con bounding boxes y IDs.
- counts.csv : Eventos de cruce con timestamps.
- Carpeta frames/ : Frames extraídos y anotados.

## 4. Milestones
- **Demo video**: Video final de hasta 20 segundos con bounding boxes y IDs visibles.  
- **CSV de conteos**: Registro de cruces de línea con timestamps y dirección.  
- **Reproducibilidad**: Código y requerimientos listos para ejecutar y generar resultados consistentes.  

## 5. Riesgos y mitigaciones
- **ID swapping / drift**: Los IDs de los objetos pueden cambiar entre frames o “perderse” si el tracker no mantiene persistencia.  
  *Mitigación*: Se usa tracking persistente con YOLOv8 (`persist=True`) y se procesa un frame cada 0.5 segundos para estabilidad.  

- **Bounding boxes inconsistentes**: Las boxes pueden moverse de forma errática o cambiar de tamaño inesperadamente.  
  *Mitigación*: Ajustar umbral de confianza (`conf`) y IOU (`iou`) para suavizar detecciones.  

- **Videos largos / rendimiento**: Procesar cada frame puede ser lento y consumir memoria.  
  *Mitigación*: Se analizan frames cada 0.5 segundos y se guardan frames procesados opcionales en `frames/`. 

## 6. Demo
![Demo GIF](./output_tracked.gif)
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1YvF3nS1_Yyt3dEWt5qHM9p1Yfv8x0dBb?usp=sharing)

