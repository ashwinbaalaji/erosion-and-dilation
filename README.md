# Implementation of Erosion and Dilation Using OpenCV

## Aim

To write a Python program using OpenCV to perform morphological operations such as Erosion and Dilation on an image.

The program performs the following operations:

- Image Erosion
- Image Dilation

## Software Used

- Anaconda – Python 3.7
- Jupyter Notebook / VS Code
- OpenCV (cv2)
- NumPy
- Matplotlib

## Algorithm

### Step 1:

Import the required libraries: OpenCV, NumPy, and Matplotlib.

### Step 2:

Create a blank image using NumPy.

### Step 3:

Insert text onto the image using OpenCV's text drawing function.

### Step 4:

Display the original image.

### Step 5:

Create a structuring element (kernel) of suitable size.

### Step 6: Image Erosion

- Apply the erosion operation using the created kernel.
- Remove pixels from the boundaries of foreground objects.
- Display the eroded image.

### Step 7: Image Dilation

- Apply the dilation operation using the same kernel.
- Add pixels to the boundaries of foreground objects.
- Display the dilated image.

### Step 8:

Compare the original, eroded, and dilated images.

## Program

## Developed By

**Name:** ASHWIN BAALAJI V K

**Register No:** 212225230026

## PROGRAM

### Original Image

- A text image containing characters is displayed.
- The image serves as the input for morphological processing.
```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

# Step 2: Create a blank black image
img = np.zeros((200, 600), dtype=np.uint8)

# Step 3: Insert white text on the image
cv2.putText(img, "ASHWIN", (30, 140), cv2.FONT_HERSHEY_SIMPLEX,
            3, 255, 5, cv2.LINE_AA)

# Step 4: Display the original image
plt.figure(figsize=(8, 4))
plt.imshow(img, cmap="gray")
plt.title("Original Image")
plt.axis("off")
plt.show()
```
### Erosion

- Original image is displayed.
- Eroded image is displayed.
- The thickness of the characters is reduced.
- Object boundaries shrink inward.
```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

img = np.zeros((200, 600), dtype=np.uint8)
cv2.putText(img, "ASHWIN", (30, 140), cv2.FONT_HERSHEY_SIMPLEX,
            3, 255, 5, cv2.LINE_AA)

# Step 5: Structuring element (kernel)
kernel = np.ones((5, 5), np.uint8)

# Step 6: Erosion shrinks the white text inward
eroded = cv2.erode(img, kernel, iterations=1)

plt.figure(figsize=(12, 4))
plt.subplot(1, 2, 1)
plt.imshow(img, cmap="gray")
plt.title("Original Image")
plt.axis("off")

plt.subplot(1, 2, 2)
plt.imshow(eroded, cmap="gray")
plt.title("Eroded Image")
plt.axis("off")
plt.show()
```
### Dilation

- Original image is displayed.
- Dilated image is displayed.
- The thickness of the characters increases.
- Object boundaries expand outward.
```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

img = np.zeros((200, 600), dtype=np.uint8)
cv2.putText(img, "ASHWIN", (30, 140), cv2.FONT_HERSHEY_SIMPLEX,
            3, 255, 5, cv2.LINE_AA)

# Same kernel as erosion
kernel = np.ones((5, 5), np.uint8)

# Step 7: Dilation expands the white text outward
dilated = cv2.dilate(img, kernel, iterations=1)

plt.figure(figsize=(12, 4))
plt.subplot(1, 2, 1)
plt.imshow(img, cmap="gray")
plt.title("Original Image")
plt.axis("off")

plt.subplot(1, 2, 2)
plt.imshow(dilated, cmap="gray")
plt.title("Dilated Image")
plt.axis("off")
plt.show()
```
## Output

### Original Image

- A text image containing characters is displayed.
- The image serves as the input for morphological processing.
<img width="860" height="327" alt="Screenshot 2026-11-18 102558" src="https://github.com/user-attachments/assets/ee241669-7e8d-470b-b36c-a17507acd353" />


### Erosion

- Original image is displayed.
- Eroded image is displayed.
- The thickness of the characters is reduced.
- Object boundaries shrink inward.
<img width="1223" height="227" alt="Screenshot 2026-11-18 102609" src="https://github.com/user-attachments/assets/2d8dfe3e-90ba-4f43-b805-598892339b92" />



### Dilation

- Original image is displayed.
- Dilated image is displayed.
- The thickness of the characters increases.
- Object boundaries expand outward.
<img width="1222" height="233" alt="Screenshot 2026-11-18 102620" src="https://github.com/user-attachments/assets/944ec798-bc4b-4648-94cc-5b4d591f9e5c" />



## Result

Thus, the morphological operations **Erosion** and **Dilation** are successfully implemented using OpenCV.
