# 🩺 Breast Ultrasound RF Signal Processing

## 📌 Project Summary

This project was developed during the Digital Signal Processing (DSP) course at the Federal University of Minas Gerais (UFMG).
It focused on the processing and visualization of raw ultrasound radiofrequency (RF) data from breast lesion scans using classical DSP techniques.

The goal was to transform raw RF signals into interpretable ultrasound images, highlighting lesion regions and supporting medical image analysis.

The project focused on applying DSP techniques such as:

* Hilbert Transform and envelope calculation

* Log compression (dB scale)

* Masking

* Medical image visualization

I created a video (in portuguese) explaining the concepts of DSP and Acoustics in Ultrasonography and the project: https://www.youtube.com/watch?v=TnqUQ18_V8o

## 📁 Dataset

The dataset can be found in https://bluebox.ippt.gov.pl/~hpiotrzk/download.html. It consists of RF ultrasound data from 100 anonymized patients diagnosed with breast tumors, including both benign and malignant cases. The dataset is officially anonymized. 
The table below show the fields and the explanation for each.



| Field      | Data Type          | Description                                                           |
| ---------- | ------------------ | --------------------------------------------------------------------- |
| **Id**     | Integer / String   | Unique patient identifier (anonymized)                                |
| **rf1**    | Image (RF matrix)  | First ultrasound scan plane (raw radiofrequency data)                 |
| **rf2**    | Image (RF matrix)  | Second ultrasound scan plane (raw radiofrequency data)                |
| **roi1**   | Mask / Coordinates | Region of Interest (ROI) corresponding to the first scan plane (rf1)  |
| **roi2**   | Mask / Coordinates | Region of Interest (ROI) corresponding to the second scan plane (rf2) |
| **BI-RADS** | Integer (1–6)      | BI-RADS category assigned to the exam                                 |
| **Class**  | Binary (0 or 1)    | Lesion class label: 0 = Benign, 1 = Malignant                         |

The RF matrix consisted of many RF lines informing the variations of acoustic impedance (different tissues). 

#### BI-RADS

Breast Imaging Reporting and Data System (BI-RADS) is a classification system for breast imaging exams (mammography, ultrasound, and MRI) that standardizes radiology reports, communicates cancer risk, and guides clinical management decisions. It uses categories from 0 to 6 to indicate benign findings (0–2), suspicious findings (3–4), or malignant findings (5–6).

| Category | Meaning                         | Malignancy Risk | Typical Recommendation      |
| -------- | ------------------------------- | --------------- | --------------------------- |
| **0**    | Incomplete                      | —               | Additional imaging needed   |
| **1**    | Negative                        | ~0%             | Routine screening           |
| **2**    | Benign finding                  | ~0%             | Routine screening           |
| **3**    | Probably benign                 | <2%             | Short-term follow-up        |
| **4**    | Suspicious abnormality          | 2–95%           | Consider biopsy             |
| **5**    | Highly suggestive of malignancy | >95%            | Biopsy strongly recommended |
| **6**    | Known biopsy-proven malignancy  | ~100%           | Treatment planning          |

## ⚙️ Signal Processing Pipeline

### 🔩 Key Parameters

* Speed of sound: 1540 m/s

* Sampling frequency: 40 MHz

* Aperture width: 38 mm

🔢 Steps

The main processing steps applied to the RF data:

* Depth axis calculation based on sampling frequency and speed of sound. The depth axis was computed using the speed of sound in soft tissue (1540 m/s) and the sampling frequency (40 MHz). This conversion transforms time-domain RF signals into spatial depth information (in millimeters), allowing proper anatomical interpretation of the ultrasound data. One RF signal is shown below:

<p align="center">
  <img src="/Images/1rf.png" width="400">
</p>

* Hilbert Transform was used to compute the analytic signal. The Hilbert Transform generates the analytic representation of the RF signal, separating amplitude and phase information. This step is fundamental for envelope detection, which mimics how real ultrasound systems reconstruct image intensity.

* Envelope calculation generated the absolute value of the analytic signal, also known as A-mode. The envelope corresponds to the magnitude of the analytic signal and represents the instantaneous amplitude of the reflected ultrasound wave. This step removes high-frequency oscillations while preserving structural information from tissue interfaces.

<p align="center">
  <img src="/Images/2hilbert.png" width="400">
</p>

* Log Compression converting the signal to decibel (dB) scale. Ultrasound RF signals have a very large dynamic range. Logarithmic compression converts the envelope into a decibel scale, reducing dynamic range and improving contrast, which makes anatomical structures and lesions visually distinguishable.

<p align="center">
  <img src="/Images/3loghilbert.png" width="400">
</p>

* Image Visualization using a grayscale colormap, also known as B-mode. The log-compressed envelope is displayed as a B-mode image.
Left: Benign tumor.
Right: Malignant tumor.
Visual differences can be observed in lesion shape, boundary definition, and internal texture. Malignant lesions tend to present more irregular contours and heterogeneous internal patterns compared to benign ones.

<p align="center">
  <img src="/Images/4modoB.png" width="400"> <img src="/Images/5modoBm.png" width="400">
</p>

* ROI Masking to isolate the lesion region. The Region of Interest (ROI) mask isolates the tumor area for focused analysis.
Left: Benign tumor ROI.
Right: Malignant tumor ROI.

This step enables quantitative feature extraction restricted to the lesion, which is essential for future classification models and comparative studies between benign and malignant cases.

<p align="center">
  <img src="/Images/4.1modoBtum.png" width="400"> <img src="/Images/5.1modoBtuma.png" width="400">
</p>

## 💭 Conclusions

This project demonstrates how fundamental DSP techniques transform raw ultrasound RF signals into clinically meaningful images. The implemented pipeline replicates core steps used in real ultrasound systems and establishes a solid foundation for future lesion classification using machine learning.
