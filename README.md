# Steganography - Secure Data Hiding in Images

## Overview
This project implements **Image Steganography** by embedding a secret message directly into an image's pixel values. The message can later be extracted and decrypted using a password.

## Features
- Hide a secret message inside an image.
- Extract the hidden message from a modified image.
- Uses direct pixel value modification for data hiding.
- Supports password-based decryption.
- Works with **PNG and BMP** image formats (JPEG not recommended due to compression loss).

## Prerequisites
Ensure you have **Python 3.x** installed. Additionally, install the required dependencies:

```sh
pip install opencv-python
```

## How It Works
1. **Encoding (Hiding Data)**:
   - Loads the cover image.
   - Converts the message characters into ASCII values.
   - Modifies the pixel values of the image to store the message.
   - Saves the stego image with hidden data.

2. **Decoding (Extracting Data)**:
   - Reads the modified image.
   - Extracts the stored ASCII values from pixel data.
   - Converts ASCII values back into text.
   - Requires the correct password for decryption.

## Usage
### **Encoding a Message**
Run the script to hide a message inside an image:

```python
import cv2
import os

img = cv2.imread("lotus.jpg") 
msg = input("Enter secret message:")
password = input("Enter a passcode:")

d = {}
c = {}
for i in range(255):
    d[chr(i)] = i
    c[i] = chr(i)

m = 0
n = 0
z = 0

for i in range(len(msg)):
    img[n, m, z] = d[msg[i]]
    n = n + 1
    m = m + 1
    z = (z + 1) % 3

cv2.imwrite("encryptedImage.jpg", img)
os.system("start encryptedImage.jpg")
```

### **Decoding a Message**
Extract the hidden message from the stego image:

```python
message = ""
n = 0
m = 0
z = 0

pas = input("Enter passcode for Decryption")
if password == pas:
    for i in range(len(msg)):
        message = message + c[img[n, m, z]]
        n = n + 1
        m = m + 1
        z = (z + 1) % 3
    print("Decryption message:", message)
else:
    print("YOU ARE NOT auth")
```

## Limitations
- This method **modifies pixel values directly**, which can be visually detectable.
- The approach **assumes enough pixel space** for the message, which may not always be available.
- **Password storage is insecure** as it's stored in plaintext.

## Enhancements
To improve security and efficiency, consider:
- **Using LSB (Least Significant Bit) encoding** instead of direct pixel modification.
- **Implementing encryption (e.g., AES) before embedding the message**.
- **Using a more structured pixel traversal method** to avoid visual artifacts.

## Contributions
Feel free to contribute by opening pull requests or reporting issues!

