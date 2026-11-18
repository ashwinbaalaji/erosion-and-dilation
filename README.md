#  Lane Detection

##  Aim

To implement a basic lane detection pipeline using OpenCV by completing missing code segments at specified locations.

---

## Learning Objective

* Understand each stage of image processing
* Learn how to build a complete computer vision pipeline
* Practice writing code in guided sections

**Important Instruction:**
👉 Write code **ONLY in places marked as `# Your Code Here`**
👉 Do NOT modify any other part of the code

---
##  Instructions

* Fill ONLY in `# Your Code Here` sections
* Do NOT change existing code
* Run step-by-step
* Verify outputs

##  Software Used

* Anaconda – Python 3.7
* Jupyter Notebook / VS Code
* OpenCV (cv2)
* NumPy
* Matplotlib

---

##  Developed By

* **Name:** ASHWIN BAALAJI V K
* **Register No:** 212225230026

##  Algorithm & Explanation

---

###  Step 1: Import Libraries

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
```

---

###  Step 2: Read the Image

```python
img = cv2.imread("Screenshot 2026-11-18 103935.png")
```

---

###  Step 3: Convert to Grayscale

```python
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
```

---

###  Step 4: Display Images

```python
plt.subplot(1, 2, 1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title("Original Image")
plt.axis("off")

plt.subplot(1, 2, 2)
plt.imshow(gray, cmap="gray")
plt.title("Grayscale Image")
plt.axis("off")
plt.show()
```

---

###  Step 5: Thresholding

```python
threshold = int(np.percentile(gray, 90))
print("Threshold used:", threshold)
_, thresh = cv2.threshold(gray, threshold, 255, cv2.THRESH_BINARY)

plt.figure(figsize=(6, 5))
plt.imshow(thresh, cmap="gray")
plt.title("Thresholded Image")
plt.axis("off")
plt.show()
```

---

###  Step 6: Region of Interest (ROI)

```python
height, width = thresh.shape

# Trapezoid covering the road ahead
polygon = np.array([[
    (0, height),
    (width, height),
    (int(0.55 * width), int(0.6 * height)),
    (int(0.45 * width), int(0.6 * height))
]], dtype=np.int32)

mask = np.zeros_like(thresh)
cv2.fillPoly(mask, polygon, 255)
masked = cv2.bitwise_and(thresh, mask)

plt.figure(figsize=(6, 5))
plt.imshow(masked, cmap="gray")
plt.title("ROI Masked Image")
plt.axis("off")
plt.show()
```

---

### Step 7: Edge Detection (Canny)

```python
edges = cv2.Canny(masked, 50, 150)

plt.figure(figsize=(6, 5))
plt.imshow(edges, cmap="gray")
plt.title("Edge Detected Image")
plt.axis("off")
plt.show()
```

---

###  Step 8: Gaussian Blur

```python
blur = cv2.GaussianBlur(edges, (5, 5), 0)

plt.figure(figsize=(6, 5))
plt.imshow(blur, cmap="gray")
plt.title("Smoothed Image")
plt.axis("off")
plt.show()
```

---

###  Step 9: Hough Transform

```python
lines = cv2.HoughLinesP(blur, 1, np.pi / 180, threshold=50,
                        minLineLength=50, maxLineGap=150)

line_img = np.zeros_like(img)
if lines is not None:
    lines = lines.reshape(-1, 4)
    for x1, y1, x2, y2 in lines:
        cv2.line(line_img, (x1, y1), (x2, y2), (0, 255, 0), 3)

plt.figure(figsize=(6, 5))
plt.imshow(cv2.cvtColor(line_img, cv2.COLOR_BGR2RGB))
plt.title("Detected Lines")
plt.axis("off")
plt.show()
```

---

### Step 10: Lane Detection Logic

```python
left_fit = []
right_fit = []

if lines is not None:
    for x1, y1, x2, y2 in lines.reshape(-1, 4):
        if x1 == x2:
            continue
        slope = (y2 - y1) / (x2 - x1)
        intercept = y1 - slope * x1
        # Image y-axis points down: left lane has negative slope, right lane positive
        if slope < -0.3:
            left_fit.append((slope, intercept))
        elif slope > 0.3:
            right_fit.append((slope, intercept))

def make_points(y_bottom, y_top, fit):
    slope, intercept = fit
    x_bottom = int((y_bottom - intercept) / slope)
    x_top = int((y_top - intercept) / slope)
    return (x_bottom, y_bottom, x_top, y_top)

h = img.shape[0]
y_bottom = h
y_top = int(h * 0.6)

lane_img = np.zeros_like(img)

if len(left_fit) > 0:
    x1, y1, x2, y2 = make_points(y_bottom, y_top, np.mean(left_fit, axis=0))
    cv2.line(lane_img, (x1, y1), (x2, y2), (0, 0, 255), 8)

if len(right_fit) > 0:
    x1, y1, x2, y2 = make_points(y_bottom, y_top, np.mean(right_fit, axis=0))
    cv2.line(lane_img, (x1, y1), (x2, y2), (0, 0, 255), 8)

final = cv2.addWeighted(img, 0.8, lane_img, 1, 0)

plt.figure(figsize=(8, 6))
plt.imshow(cv2.cvtColor(final, cv2.COLOR_BGR2RGB))
plt.title("Final Lane Detection Output")
plt.axis("off")
plt.show()
```

---

##  Expected Output

* Original image

<img width="331" height="236" alt="image" src="https://github.com/user-attachments/assets/512bcbb0-b18a-4403-8151-6e246854ff8f" />


* Grayscale image

<img width="332" height="233" alt="image" src="https://github.com/user-attachments/assets/31a3ef15-4289-4a28-811a-552f8ea05ffe" />


* Thresholded image

<img width="484" height="341" alt="download" src="https://github.com/user-attachments/assets/0117d749-a4c1-46f4-b6a3-d751bdf2e584" />

* ROI masked image

<img width="484" height="341" alt="download" src="https://github.com/user-attachments/assets/65f146e6-91ef-430c-837f-cd193cb370fa" />


* Edge detected image

<img width="484" height="341" alt="download" src="https://github.com/user-attachments/assets/d2151a18-e9e6-425c-abcc-e6b10dbd68ac" />


* Smoothed image

<img width="484" height="341" alt="download" src="https://github.com/user-attachments/assets/9af8bec2-5c79-4950-b158-c320d05f97ed" />


* Detected lines

<img width="484" height="341" alt="download" src="https://github.com/user-attachments/assets/28a2577d-3d02-41dc-904f-122c5933e5a9" />

* Final lane detection output

<img width="640" height="440" alt="download" src="https://github.com/user-attachments/assets/c9b838c1-6da1-4f6f-8dbc-affcda974b06" />



---



---

## Result

Thus, the lane detection pipeline is successfully implemented by completing the missing code sections. The system detects and highlights lane lines effectively.

---


