# Detección Robusta de Deepfakes mediante Augmentation Adversarial 🛡️

Proyecto final para la asignatura **Redes Neuronales y Deep Learning** del Máster en Economía, Finanzas y Computación (UNIA).

**Autor:** Fernando Gomez Jimenez  
**Docente:** Amaya Nogales Gómez  

##  Resumen del Proyecto
Los detectores de deepfakes actuales logran precisiones del 99% en entornos de laboratorio, pero colapsan bajo degradación de imagen (compresión en redes sociales) debido al **Shortcut Learning** (sobreajuste al ruido de alta frecuencia de las GAN). 

Este proyecto propone y evalúa un *pipeline* de **Data Augmentation Adversarial** (ruido gaussiano y compresión JPEG) para forzar a las redes a aprender representaciones geométricas causales (anatomía facial) en lugar de atajos espectrales.

##  Arquitecturas Evaluadas
Se implementó un diseño A/B testing sobre dos modelos mediante TensorFlow/Keras:
1. **CNN Custom (Scratch):** Arquitectura de 455k parámetros con bloques `Conv2D` + `BatchNormalization` + `MaxPooling2D`, utilizando `GlobalAveragePooling2D` para mitigar el riesgo de sobreajuste masivo.
2. **EfficientNetB0 (Transfer Learning):** Uso de pesos de ImageNet con un *fine-tuning* selectivo protegiendo las estadísticas de las capas Batch Normalization.

## Resultados Clave
Bajo un test de estrés progresivo (JPEG 70 + Ruido 5%):
* **Reducción de Falsos Negativos:** El modelo robusto disminuyó los errores críticos en un **87.3%** (CNN) y un **83.5%** (EfficientNet).
* **Explicabilidad Visual (Grad-CAM):** Se corrigió el sesgo atencional, desplazando la activación de la red desde el fondo espurio hacia los ojos y boca del sujeto.
* **Optimización Operativa:** AUC > 0.97 bajo estrés, con ajuste dinámico del umbral (Métrica de Youden) para responder a una matriz de pagos de ciberseguridad asimétrica.

## 📂 Contenido del Repositorio
* Notebook con la ingesta (tf.data), entrenamiento A/B, test de estrés y análisis Grad-CAM.
* Documento técnico estilo IEEE (5 páginas).
* Diapositivas de la sustentación.

Dataset original utilizado: [140k Real and Fake Faces (Kaggle)](https://www.kaggle.com/datasets/xhlulu/140k-real-and-fake-faces).
