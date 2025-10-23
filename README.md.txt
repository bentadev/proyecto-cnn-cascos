# 🧠 Detección de Cascos de Seguridad con CNN

Este proyecto utiliza una Red Neuronal Convolucional (CNN) simple, construida con Keras y TensorFlow, para clasificar imágenes e identificar si los trabajadores están usando su casco de seguridad.

Este repositorio contiene el código y el análisis del proyecto: Redes Neuronales.

---

## ⚠️ Problema a Resolver

El objetivo es desarrollar un sistema basado en redes neuronales que permita detectar si un trabajador de la construcción utiliza o no casco de seguridad, a partir de una imagen. Esto sienta las bases para un sistema de seguridad inteligente en obras, con el fin de prevenir accidentes laborales.

---

## 🚀 Resultados Principales

Tras el análisis inicial, se detectó un sobreajuste (overfitting) en el modelo base. Se aplicaron técnicas de regularización para solucionarlo:

1. Data Augmentation (Aumento de datos)
2. Dropout (Apagado de neuronas)
3. Early Stopping (Detención temprana)

El modelo final, entrenado con estas técnicas, alcanzó una precisión del 75.56% en el conjunto de Test, demostrando que es capaz de generalizar correctamente a nuevos datos.

---

## 🛠️ Cómo Usar este Proyecto

Sigue estos pasos para ejecutar el proyecto en tu propia máquina.

### ⚙️ 1. Requisitos Previos

Asegúrate de tener Python 3.x. Clona este repositorio e instala las dependencias usando el archivo 'requirements.txt':

```bash
pip install -r requirements.txt

---

### 📊 2. Dataset (Configuración de la API de Kaggle)

Este notebook está diseñado para conectarse directamente a la API de Kaggle y descargar el dataset automáticamente.

Al ejecutar las primeras celdas, el script te pedirá que ingreses tu usuario y tu llave (key) de la API de Kaggle.

Para obtener tus credenciales:
1. Ve a tu perfil de Kaggle y entra a la sección "Account" (Cuenta).
2. Desplázate hacia abajo hasta la sección "API" y haz clic en "Create New API Token".
3. Esto descargará un archivo kaggle.json. Ábrelo con cualquier editor de texto.
4. Dentro de ese archivo verás tu "username" y tu "key".
5. Copia y pega esos dos valores en el notebook cuando te los pida.

---

## 🚀 Ejecutar el Análisis

Para ver el proceso completo, desde la carga de datos hasta la evaluación final, abre y ejecuta el notebook principal: /notebooks/deteccion_cascos_cnn.ipynb

---

## 👥 Autores

Este proyecto fue desarrollado por:

Martin: https://github.com/bentadev
Maria: https://github.com/yanin-dev
Rosmery: https://github.com/ros-arango
Micaela: https://github.com/MICAELA-IA