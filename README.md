# 🌾 Brown Spot Detection in Rice Plants  

Este repositorio contiene el desarrollo de un modelo de **Visión por Computador** basado en **Transformers de Visión (ViT, Swin Transformer v2, DeiT)** para la detección temprana de la enfermedad **mancha parda (Bipolaris oryzae)** en plantas de arroz.  

La investigación aborda la disminución en la producción arrocera del Huila (Colombia) causada por el cambio climático y enfermedades, proponiendo un sistema robusto y confiable para apoyar la agricultura de precisión.  

---

## 📑 Contenido
- [Descripción](#-descripción)  
- [Metodología](#-metodología)  
- [Resultados](#-resultados)  
- [Dataset](#-dataset)  
- [Modelos](#-modelos)  
- [Cómo usar](#-cómo-usar)  
- [Autores](#-autores)  
- [Referencias](#-referencias)  

---

## 📖 Descripción  

El modelo se centra en identificar lesiones características de la **mancha parda** en las hojas del arroz. Se trabajó con un dataset balanceado y segmentado mediante técnicas de procesamiento digital de imágenes y *data augmentation*.  

Se entrenaron y evaluaron arquitecturas de última generación:  
- **Vision Transformer (ViT)**  
- **Swin Transformer v2**  
- **Data-efficient Image Transformer (DeiT)**  

---

## 🔬 Metodología  

1. **Construcción del dataset** (10 clases: brown spot, bacterial leaf blight, tungro, healthy, etc.)  
2. **Preprocesamiento**: estandarización (224×224 px), segmentación Otsu, aumento de datos (rotaciones y escalado).  
3. **Entrenamiento**: división en 70% train, 20% validación, 10% test.  
4. **Evaluación**: métricas de exactitud, recall y F1-score.  
5. **Comparación de modelos** en términos de precisión y tiempo de inferencia.  

---

## 📊 Resultados  

- **Swin Transformer v2** alcanzó **99.82% de exactitud** con tiempos de inferencia de 1.8 ms.  
- **ViT** logró 99.35% en entrenamiento, aunque mostró tendencia al sobreajuste.  
- **DeiT** obtuvo 99.36% con buen balance entre rendimiento y generalización.  

📌 El modelo **Swin Transformer v2** fue seleccionado como el más robusto para la tarea.  

---

## 📂 Dataset  

El dataset balanceado y segmentado está disponible en Google Drive:  
👉 [Descargar Dataset](https://drive.google.com/drive/folders/1GB8j59CuCg9faKSWBPGcBXNdrZW89kl2?usp=sharing)  

---

## 🤖 Modelos  

Los modelos entrenados pueden descargarse en el siguiente enlace:  
👉 [Modelos Entrenados](https://drive.google.com/drive/folders/1NMPIkHfrRijAAdw59Ajh3VkUGDugRUN0?usp=sharing)  

---

## ⚙️ Cómo usar  

1. Clonar este repositorio:  
   ```bash
   git clone https://github.com/usuario/rice-brown-spot-detection.git
   cd rice-brown-spot-detection
   ```

2. Instalar dependencias:  
   ```bash
   pip install -r requirements.txt
   ```

3. Cargar un modelo preentrenado:  
   ```python
   import torch
   from torchvision import transforms
   from PIL import Image
   
   # Cargar modelo guardado
   model = torch.load("modelos/swin_v2_best.pth")
   model.eval()
   
   # Procesar imagen
   transform = transforms.Compose([
       transforms.Resize((224,224)),
       transforms.ToTensor()
   ])
   img = Image.open("sample_leaf.jpg")
   input_tensor = transform(img).unsqueeze(0)
   
   # Predicción
   output = model(input_tensor)
   predicted_class = output.argmax(dim=1)
   print("Clase predicha:", predicted_class.item())
   ```

---

## 👥 Autores  


- **Dubán Estiben Cardozo Osorio** – Universidad Surcolombiana  
- **Nicolás Calderón** – Universidad Surcolombiana  

---

