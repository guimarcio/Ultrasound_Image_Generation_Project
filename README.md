# Files to be updated.
# Ultrasound_Image_Generation_Project
A final project of the Digital Signal Processing graduated course at Federal University of Minas Gerais.

https://bluebox.ippt.gov.pl/~hpiotrzk/download.html

https://www.youtube.com/watch?v=TnqUQ18_V8o

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
