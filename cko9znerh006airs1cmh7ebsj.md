## Make beautiful pencil sketches using OpenCV in 9 lines of code

For this simple project we will use  [OpenCV](https://opencv.org/)  in Python.

It is a library using which we can develop real-time computer vision applications. It mainly focuses on image processing, video capture and analysis including features like face detection and object detection.

But before that....

### A bit of backstory
When I was in 7th grade (3 years ago), I used to play with this photo editing software called " [GIMP](https://www.gimp.org/) ". (short for GNU Image Manipulation Software)

Using a couple of clever techniques, I would make sketches out of images like what you saw in the thumbnail.


### Let's see how this process works.

- You take an image

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1619984592141/rAqt04cPZ.png)

- Convert it to grayscale

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1619984602580/_O9gwlCYo.png)

- Invert the grayscaled image

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1619984610480/ypuOmpcpH.png)

- Blur the inverted image

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1619984622303/vjNHIGXXW.png)

- Subtract the grayscaled image from the blurred inverted image

et voilà !

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1619984634641/uJkUA3dGN.png)

I figured that I could automate this process using OpenCV, let see the code and how it works.



```py
import cv2
# Importing the OpenCV libarary

img = cv2.imread('image.jpg')
#Reading the image

img_gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
#Converting the image to grayscale


img_invert = cv2.bitwise_not(img_gray)
#Inverting the grayscaled image

img_smoothing = cv2.GaussianBlur(img_invert, (21, 21),sigmaX=0, sigmaY=0)
#Blurring the inverted image

def dodge(x, y):
    return cv2.divide(x, 255 - y, scale=256)
final_img = dodge(img_gray, img_smoothing)
#Subtracting the blurred iamge from the orignal image

cv2.imwrite('img.jpg', final_img)
#Writing the final output to a a file
```

Just like that in 9 lines of code, you can easily create skteches using OpenCV and Python!

Here's the Github repository with this  [code](https://github.com/PrasoonPratham/Sketches-with-Python) .


