
# 🩺 **Segmentación automática de lesiones pulmonares por COVID-19**
_Notebook con modelo U-Net para segmentación en imágenes CT_

---

## 🚀 **Resumen del flujo del notebook**

### 📂 **Carga de datos**
- Montaje de Google Drive para acceder al dataset.  
- Lectura de volúmenes NIfTI (imágenes y máscaras).  
- Selección de slices con **≥ 50 píxeles positivos** (asegura presencia de lesión).  

---

### ⚙️ **Preprocesamiento**
- Resize de cada slice a **128×128 píxeles**.  
- Normalización de intensidades a **[0,1]**.  

---

### 🔀 **División del dataset**
- División en **train / val / test** usando `train_test_split`.  
- ⚠ **División por slice, no por paciente** (puede haber mezcla de slices del mismo paciente).  

---

### 🧠 **Modelo U-Net**
- U-Net con:
  - **BatchNormalization**
  - **Dropout**
  - **Conv2DTranspose**
- Pérdida: `0.2 * BCE + 0.8 * Dice loss`  

---

### 🏋️ **Entrenamiento**
- **25 epochs**  
- Augmentación dinámica: flips, rotaciones (no se guardan nuevos archivos)  

---

### 📊 **Evaluación**
- Métricas: **Dice promedio**, **IoU promedio** en test.  
- Visualización:
  - Curvas de entrenamiento (loss, Dice)  
  - Histograma de Dice  
  - Ejemplos CT + Ground Truth + Predicción  

---

## ⚠ **Notas**
- No se implementó validación cruzada (opcional).  
- Augmentación solo en tiempo real durante el entrenamiento.  
