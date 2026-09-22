# ESP32-CAM Traffic Signs for Micro-Robotics (ESP32-TSMR)

Este repositorio contiene un dataset de visión computacional orientado al guiado autónomo de un vehículo robótico terrestre a escala[cite: 2]. El objetivo funcional del agente inteligente es detectar y clasificar tres señales de control de tráfico y maniobra en interiores desde la perspectiva de un microcontrolador.

## Ficha Técnica del Dataset
* **Dispositivo de Captura:** Módulo ESP32-CAM (Sensor CMOS OmniVision OV2640) montado a 8.5 cm del suelo[cite: 2].
* **Resolución Nativa:** 640x480 píxeles (proporción 4:3, espacio sRGB, formato JPEG)[cite: 2].
* **Total de Imágenes e Instancias:** 721 imágenes reales a color y 721 cajas delimitadoras anotadas (promedio de 1 instancia por cuadro).
* **Clases (3 mutuamente excluyentes):** `0: Izquierda`, `1: Derecha`, `2: Alto`[cite: 2].
* **Formato de Anotación:** Estándar YOLO (Darknet / TXT) para desacoplar las anotaciones de posibles cambios en la resolución de captura.
* **Herramienta de Etiquetado:** LabelImg v1.8.6[cite: 2].

## Partición y Balance de Datos
El dataset cuenta con una partición dividida metodológicamente para el entrenamiento de arquitecturas de aprendizaje profundo:
* **Entrenamiento (Train):** 573 imágenes (79.5%)[cite: 2].
* **Validación (Valid):** 92 imágenes (12.8%)[cite: 2].
* **Prueba (Test):** 56 imágenes (7.8%)[cite: 2].

Distribución cuantitativa de instancias:
* **Izquierda:** 187 instancias[cite: 2].
* **Derecha:** 228 instancias[cite: 2].
* **Alto:** 306 instancias[cite: 2].

## Metodología de Adquisición
Para garantizar la diversidad del conjunto de datos y prevenir sesgos de sobreajuste (*overfitting*), la captura consideró variaciones sistemáticas:
* **Distancia y escala:** Tomas cortas (15 cm), medias (40 cm) y largas (80 cm)[cite: 2].
* **Ángulo de ataque:** Variaciones de perspectiva oblicua desde -35° hasta +35°[cite: 2].
* **Iluminación:** Escenarios con iluminación cenital directa, luz difusa tenue y contraluz severo[cite: 2].
* **Aumento de datos:** El dataset se complementó con imágenes de internet para incrementar la variabilidad[cite: 2].

## Validación Experimental (YOLOv7)
Para demostrar la viabilidad y solidez técnica de este dataset, se entrenó la arquitectura YOLOv7 durante 160 épocas de optimización estocástica[cite: 2]. El modelo logró una discriminación interclase sin confusiones mutuas (matriz de confusión con diagonal casi perfecta) y alcanzó las siguientes métricas globales sobre el conjunto independiente de validación[cite: 2]:
* **Precisión (Precision):** 96.79%[cite: 2].
* **Exhaustividad (Recall):** 100.00%[cite: 2].
* **mAP@0.5:** 99.55%[cite: 2].
* **mAP@0.5:0.95:** 86.32%[cite: 2].

## Estructura del Repositorio
El repositorio sigue el esquema de directorios esperado por YOLOv7:
* Carpetas principales: `train/`, `valid/`, y `test/`[cite: 2].
* Cada partición contiene sus respectivas subcarpetas `images/` y `labels/`[cite: 2].
* Archivo de metadatos `signals.yaml` con la definición de las rutas y el número de clases ($nc=3$)[cite: 2].
