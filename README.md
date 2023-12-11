# Arnold's Cat Map in Google Colab
## Overview
This repository provides an in-depth exploration of Arnold's Cat Map 🐱🗺️ in the Google Colab environment. Arnold's Cat Map is a chaotic mathematical transformation, and this project enables users to implement, visualize, and analyze its effects on grayscale images. The code includes functionalities for loading images, generating histograms, applying the cat map transformation, and comparing original and transformed images.

## Step by step
### Step 1: Import Libraries
```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
import urllib.request
from google.colab.patches import cv2_imshow
from random import randint
from PIL import Image
from PIL import ImageOps
from scipy.stats import Entropy 
```

### Step 2: Load and Display an Image
```python
img = cv2.imdecode(np.asarray(bytearray(urllib.request.urlopen('image_url').read()), dtype=np.uint8), 0)
plt.imshow(img, 'gray')
```
For example, I used this picture:
![download](https://github.com/mohammadnabia/Arnold-cat-map/assets/53332753/ad41fd3a-4f30-4f3f-98ff-0d8786a0a58e)
|:--:|

### Step 3: Define Histogram Function
```python
def draw_hist(x_axis, input):
    figsize = (5, 5)
    fig, ax = plt.subplots(figsize=figsize)
    plt.bar(x_axis, input, width=input.shape[0] / (x_axis[-1] - x_axis[0] + 1))
    return fig, ax
```

### Step 4: Plot Histogram
```python
hist = cv2.calcHist([img], [0], None, [256], [0, 256])
plt.hist(img.ravel(), bins=256, range=(0, 256))
plt.title('Grayscale Histogram')
plt.xlabel('Pixel Intensity')
plt.ylabel('Frequency')
plt.show()
```
![download](https://github.com/mohammadnabia/Arnold-cat-map/assets/53332753/e496c020-9537-4235-a779-1203793adb48)
|:--:| 
| *The grayscale histogram of our image* |

### Step 5: Apply Arnold's Cat Map Transformation
```python
def arnold_cat_map(image, iterations):
    # ... (as provided in your original code)
    return image

ACMimg = arnold_cat_map(img, 10)
plt.imshow(ACMimg, 'gray')
```
![download](https://github.com/mohammadnabia/Arnold-cat-map/assets/53332753/982e01a0-55f7-4ed7-9d82-66e0e9d626e4)
|:--:| 
| *The transformed image* |

### Step 6: Plot Transformed Image and Histogram
```python
hist = cv2.calcHist([ACMimg], [0], None, [256], [0, 256])
plt.subplot(221), plt.imshow(img, 'gray'), plt.title('Original')
plt.subplot(222), plt.imshow(ACMimg, 'gray'), plt.title('Arnolds cat map image')
plt.subplot(223), plt.hist(img.ravel(), bins=256, range=(0, 256)), plt.title('Original histo')
plt.subplot(224), plt.hist(ACMimg.ravel(), bins=256, range=(0, 256)), plt.title('Arnolds cat map histo')
```

![download](https://github.com/mohammadnabia/Arnold-cat-map/assets/53332753/60909416-18c8-40b7-bcc3-6d2505fcba59)
|:--:| 
| *comparing the original photo's histogram with the transformed one* |

### Step 7: Calculate Entropy
```python
pixel_probOrg = cv2.calcHist([img], [0], None, [256], [0, 256]) / img.size
pixel_probACM = cv2.calcHist([ACMimg], [0], None, [256], [0, 256]) / ACMimg.size

entropy_valOrg = entropy(pixel_probOrg, base=2)
entropy_valACM = entropy(pixel_probACM, base=2)

print("Entropy of the ORG image:", entropy_valOrg, "\nEntropy of the ACM image:", entropy_valACM)
```

## Usage
Follow the provided code snippets to explore and understand the implementation of Arnold's Cat Map. Experiment with different images and iterations and analyze the resulting histograms and entropy values.

## Conclusion
Upon analyzing the results of Arnold's Cat Map transformation, it becomes evident that the histogram and entropy values of the transformed image bear remarkable similarities to those of the original image. This intriguing resemblance can be attributed to the deterministic nature of Arnold's Cat Map algorithm.

### Similar Histograms
The visual inspection of histograms reveals a notable correlation between the grayscale distribution of the original and transformed images. The structural integrity of the image is preserved through the cat map transformation, leading to histogram similarities.

### Consistent Entropy
The entropy values, a measure of information content, exhibit consistency between the original and transformed images. The deterministic and reversible nature of Arnold's Cat Map ensures that information entropy is maintained, contributing to the observed similarity.

In summary, the preservation of structural features and information entropy underscores the effectiveness of Arnold's Cat Map in maintaining critical characteristics during the transformation process.
  
## License
This project is licensed under the MIT License. You can use, modify, and distribute the code as the license permits.

---

Have a cheery coding! 👾
