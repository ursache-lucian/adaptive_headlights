# 🚗 Automatic Headlight Dimming Control (YOLOv8)

Acest proiect de Computer Vision utilizează inteligența artificială pentru a detecta în timp real sursele de lumină și vehiculele din trafic (faruri, stopuri, semafoare, stâlpi de iluminat). Scopul final este crearea unui sistem care poate asista comutarea automată a fazei lungi/scurte la autovehicule, sporind siguranța pe timp de noapte.

Modelul a fost antrenat folosind **YOLOv8** (You Only Look Once), rulând într-un mediu de cercetare Jupyter Notebook.

## 🛠️ Arhitectura și Pipeline-ul de Date
O parte majoră a acestui proiect a constat în construirea unui pipeline personalizat ("Data Wrangling") pentru a procesa și unifica date brute stocate local:
* **Agregare multi-format:** Scriptul combină automat două dataset-uri distincte care foloseau metode de adnotare diferite (fișiere `.csv` și `.xml` de tip PASCAL VOC).
* **Normalizare Bounding Boxes:** Conversia matematică a coordonatelor din format absolut (xmin, ymin, xmax, ymax) în formatul relativ cerut de YOLO (x_center, y_center, width, height).
* **Generare dinamică a fișierului YAML:** Crearea programatică a configurației `combined_data.yaml` pentru a mapa clasele detectate (ex: *headlight, taillight, streetlight, signal*).

## 🧠 Antrenarea Modelului (Training)
* **Algoritm:** YOLOv8 Nano (`yolov8n.pt`) - ales pentru echilibrul excelent între viteză de inferență și acuratețe.
* **Proces:** Antrenat pe parcursul a 25 de epoci, cu o rezoluție a imaginilor de 640x640 pixeli.
* **Evaluare:** Modelul extrage automat metricile de performanță (mAP50 și mAP50-95) pentru a valida calitatea detecțiilor.

## 🚀 Inferență și Testare
Proiectul include un modul robust de testare:
1. **Imagini de test:** Rularea modelului pe setul de `test` și afișarea primelor 3 predicții direct în output-ul celulelor Jupyter.
2. **Video Processing:** Modelul poate procesa un clip video complet (`AI Scene.mp4`), aplicând bounding boxes și etichete cu un grad de confidență setat manual (conf=0.40).

## 💻 Tehnologii Folosite
* **Limbaj:** Python
* **Machine Learning / Vision:** Ultralytics (YOLOv8), OpenCV (`cv2`)
* **Manipulare date & Viziualizare:** Pandas, Matplotlib, ElementTree (XML parsing)
* **Mediu:** Jupyter Notebook

## 🔧 Cum se rulează
Pentru a rula acest notebook local, instalează dependențele necesare:
```bash
pip install ultralytics opencv-python matplotlib pandas
