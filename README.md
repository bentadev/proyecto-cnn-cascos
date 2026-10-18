# 🦺 Detección de Cascos de Seguridad con CNN

![Python](https://img.shields.io/badge/Python-3.x-3776AB?logo=python&logoColor=white)
![TensorFlow](https://img.shields.io/badge/TensorFlow-Keras-FF6F00?logo=tensorflow&logoColor=white)
![Google Colab](https://img.shields.io/badge/Google%20Colab-notebook-F9AB00?logo=googlecolab&logoColor=white)

Red Neuronal Convolucional (CNN) construida con **Keras y TensorFlow** que clasifica imágenes de obras en construcción para identificar si un trabajador **usa o no casco de seguridad**.

Trabajo final de la materia **Redes Neuronales** (IFTS N°33), desarrollado en grupo.

[![Abrir en Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/bentadev/proyecto-cnn-cascos/blob/main/notebooks/deteccion_cascos_cnn.ipynb)

---

## ⚠️ Problema a resolver

En las obras en construcción el uso del casco es obligatorio, pero controlarlo de forma manual es difícil. El objetivo es desarrollar un modelo que, a partir de una imagen, indique si el trabajador **usa casco (seguro)** o **no lo usa (no seguro)**.

Este trabajo es una **prueba de concepto**: sienta las bases de un sistema de apoyo a la supervisión de seguridad laboral, pero no es un sistema listo para producción.

---

## 📊 Dataset

- **Fuente:** [Worksite Safety Monitoring Dataset](https://www.kaggle.com/datasets/lbquctrung/worksite-safety-monitoring-dataset) (Kaggle)
- **Tarea:** clasificación binaria de imágenes (seguro / no seguro)
- **Particiones:** `train`, `valid` y `test`
- **Preprocesamiento:** redimensionado a **128 × 128 px**, lotes de 32 imágenes y normalización de píxeles (0–1)

> Las imágenes **no se incluyen en este repositorio**: se descargan desde Kaggle al ejecutar el notebook. Revisá la licencia del dataset en su página.

---

## 🔬 Enfoque

El trabajo avanza en tres etapas, cada una para corregir un problema de la anterior:

| Etapa | Qué se hizo | Para qué |
|---|---|---|
| **1. Modelo base** | CNN simple de 3 bloques convolucionales, 10 épocas | Punto de partida |
| **2. Regularización** | Data Augmentation (giro horizontal, rotación y zoom) y Dropout (0,25 en los bloques convolucionales y 0,5 en la capa densa), 25 épocas | Reducir el **sobreajuste** detectado en el modelo base |
| **3. Early Stopping** | Reentrenamiento del modelo de la etapa 2 con parada temprana sobre `val_loss` (paciencia de 5 épocas, hasta 50 épocas) y recuperación de los mejores pesos | Cortar el entrenamiento cuando deja de mejorar |

El modelo final es el de la etapa 2 **reentrenado con Early Stopping**.

---

## 🧱 Arquitectura del modelo

| Capa | Detalle |
|---|---|
| `Rescaling` | Normaliza los píxeles dividiendo por 255 |
| `Data Augmentation` | `RandomFlip`, `RandomRotation(0.1)`, `RandomZoom(0.1)` (solo en entrenamiento) |
| `Conv2D` + `MaxPooling2D` + `Dropout(0.25)` | 16 filtros de 3×3 |
| `Conv2D` + `MaxPooling2D` + `Dropout(0.25)` | 32 filtros de 3×3 |
| `Conv2D` + `MaxPooling2D` + `Dropout(0.25)` | 64 filtros de 3×3 |
| `Flatten` | Pasa los mapas de características a un vector |
| `Dense(128)` + `Dropout(0.5)` | Activación ReLU |
| `Dense(1)` | Activación sigmoid: probabilidad de la clase "no seguro" |

**Entrenamiento:** optimizador Adam y pérdida `binary_crossentropy`.

---

## 🚀 Resultados

| Modelo | Accuracy entrenamiento | Accuracy validación | Accuracy test |
|---|---|---|---|
| Base | [-] | [-] | — |
| Final (regularización + Early Stopping) | [-] | [-] | **75,56 %** |

**Cómo leer estos resultados**

- La regularización (Data Augmentation, Dropout y Early Stopping) permitió **reducir la brecha entre entrenamiento y validación** frente al modelo base.
- Un **75,56 % de acierto en test** es un resultado razonable para una CNN pequeña entrenada desde cero, pero **no es suficiente para un uso real** en seguridad laboral: el modelo se equivoca en una de cada cuatro imágenes aproximadamente.

---

## 🔧 Limitaciones y próximos pasos

**Limitaciones**

- Clasifica la **imagen completa**: no localiza ni cuenta cascos, ni distingue entre varios trabajadores.
- Se entrenó con un dataset acotado y poco diverso, y falla en algunas imágenes de prueba.
- Arquitectura simple, entrenada desde cero.

**Próximos pasos**

- 🧠 **Transfer Learning** con un modelo preentrenado (MobileNetV2, VGG16 o ResNet50).
- 🖼️ Ampliar y diversificar el dataset (iluminación, ángulos, distancias, tipos de casco).
- 🎛️ Búsqueda automática de hiperparámetros con KerasTuner.
- 🔀 Aumento de datos más agresivo.
- 📏 Evaluar con precisión, recall, F1 y matriz de confusión.
- 🎯 Pasar de clasificación a **detección de objetos** (por ejemplo, YOLO) para ubicar cada casco en la imagen.

---

## ▶️ Cómo ejecutarlo

### Opción recomendada: Google Colab

1. Abrí el notebook con el botón **Abrir en Colab** de arriba.
2. Ejecutá las celdas en orden. Las primeras te piden tu **usuario y tu API key de Kaggle** para descargar el dataset.

### 🔑 Credenciales de Kaggle

1. En Kaggle, entrá a **Settings → API → Create New Token**. Se descarga un archivo `kaggle.json` con tu `username` y tu `key`.
2. Pegá esos dos valores cuando el notebook los pida.

> 🔒 **Nunca subas tu `kaggle.json` ni tu key al repositorio**, ni dejes la key escrita en una celda. Si se filtra, generá un token nuevo desde Kaggle.

### Ejecución local

```bash
git clone https://github.com/bentadev/proyecto-cnn-cascos.git
cd proyecto-cnn-cascos
pip install -r requirements.txt
jupyter notebook notebooks/deteccion_cascos_cnn.ipynb
```

El notebook usa funciones propias de Colab (por ejemplo, la subida de archivos de la sección de pruebas), así que en local hay que adaptar esa parte.

**Librerías principales:** TensorFlow / Keras, Matplotlib, Pillow y la API de Kaggle.

---

## 👥 Equipo

Proyecto desarrollado por:

| Integrante | GitHub |
|---|---|
| Martin | [@bentadev](https://github.com/bentadev) |
| Maria | [@yanin-dev](https://github.com/yanin-dev) |
| Rosmery | [@ros-arango](https://github.com/ros-arango) |
| Micaela | [@MICAELA-IA](https://github.com/MICAELA-IA) |
| Emmanuel | [@Emmaflores94](https://github.com/Emmaflores94) |
