# 🩺 Breast Ultrasound RF Signal Processing

## 📌 Project Summary

This project was developed during the Digital Signal Processing (DSP) course at the Federal University of Minas Gerais (UFMG).
It focused on the processing and visualization of raw ultrasound radiofrequency (RF) data from breast lesion scans using classical DSP techniques.

The goal was to transform raw RF signals into interpretable ultrasound images, highlighting lesion regions and supporting medical image analysis.

The project focused on applying DSP techniques such as:

* Hilbert Transform

* Envelope detection

* Log compression (dB scale)

* Masking

* Medical image visualization

I created a video explaining the concepts of DSP and Acoustics in Ultrasonography and the project: https://www.youtube.com/watch?v=TnqUQ18_V8o

## Dataset

The [dataset](https://bluebox.ippt.gov.pl/~hpiotrzk/download.html) has 



| Field      | Data Type          | Description                                                           |
| ---------- | ------------------ | --------------------------------------------------------------------- |
| **Id**     | Integer / String   | Unique patient identifier (anonymized)                                |
| **rf1**    | Image (RF matrix)  | First ultrasound scan plane (raw radiofrequency data)                 |
| **rf2**    | Image (RF matrix)  | Second ultrasound scan plane (raw radiofrequency data)                |
| **roi1**   | Mask / Coordinates | Region of Interest (ROI) corresponding to the first scan plane (rf1)  |
| **roi2**   | Mask / Coordinates | Region of Interest (ROI) corresponding to the second scan plane (rf2) |
| **Birads** | Integer (1–6)      | BI-RADS category assigned to the exam                                 |
| **Class**  | Binary (0 or 1)    | Lesion class label: 0 = Benign, 1 = Malignant                         |

#### BI-RADS
| Category | Meaning                         | Malignancy Risk | Typical Recommendation      |
| -------- | ------------------------------- | --------------- | --------------------------- |
| **0**    | Incomplete                      | —               | Additional imaging needed   |
| **1**    | Negative                        | ~0%             | Routine screening           |
| **2**    | Benign finding                  | ~0%             | Routine screening           |
| **3**    | Probably benign                 | <2%             | Short-term follow-up        |
| **4**    | Suspicious abnormality          | 2–95%           | Consider biopsy             |
| **5**    | Highly suggestive of malignancy | >95%            | Biopsy strongly recommended |
| **6**    | Known biopsy-proven malignancy  | ~100%           | Treatment planning          |

⚙️ Signal Processing Pipeline

The main processing steps applied to the RF data:

* Depth axis calculation based on sampling frequency and speed of sound.

* Hilbert Transform was used to compute the analytic signal.

* Envelope Detection generated the absolute value of analytic signal, as known as A-mode.

* Log Compression to conversion to decibel (dB) scale.

* ROI Masking to isolate the lesion region.

* Image Visualization using grayscale colormap, as know as B-mode.
