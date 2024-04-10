<h1 align="center">Welcome to Face Tracking Project 👋</h1>

# Face Tracking

In this project, we have written a face and eye recognition program with Python

## Modules

```python
import cv2
import pyautogui as robot
```

## Usage
Loading eye and face recognition model

```python
eye_model = cv2.CascadeClassifier('haarcascade_eye.xml')
face_model = cv2.CascadeClassifier('haarcascade_frontalface_default.xml')
loop = True
```

Activating the camera and horizontalizing the image and face detection in the image and eye detection in the face image

```python
cam = cv2.VideoCapture(0)

while loop:
    _ , img = cam.read()
    
    img = cv2.flip(img, 1)
    gray = cv2.cvtColor(img,cv2.COLOR_BGR2GRAY)

    face = face_model.detectMultiScale(gray)
    
    if len(face) > 0:
        xs = face[0][0]
        ys = face[0][1]
        xs2 = xs + face[0][2]
        ys2 = ys + face[0][3]
        gray_face = gray[ys:ys2,xs:xs2]
        eye = eye_model.detectMultiScale(gray_face, minSize = (30,30), scaleFactor=1.1, minNeighbors=5)
        imgout = img.copy()
```
Draw a rectangle around the face

```python
out = cv2.rectangle(imgout, (xs,ys),(xs2,ys2),(0,250,0),3)
    
    white = (250,250,250)
    red = (0,0,250)
    rang = white
    
    mouse_x = robot.position().x
    mouse_y = robot.position().y

    if xs < 400:
        rang = red
        mouse_x -= abs(xs-400)
        robot.moveTo(mouse_x, mouse_y, 0)
    
    if xs2 > 900:
        rang = red
        mouse_x += abs(xs2 - 900)
        robot.moveTo(mouse_x, mouse_y, 0)

    if ys < 100:
        rang = red
        mouse_y -= abs(ys - 100)
        robot.moveTo(mouse_x, mouse_y, 0)

    if ys2 > 600:
        rang = red
        mouse_y += abs(ys2 - 600)
        robot.moveTo(mouse_x, mouse_y, 0)
```

Draw a border rectangle for mouse movement

```python
out = cv2.rectangle(imgout, (400,100),(900,600),rang,2)

    ic = 0
    for (xe, ye, w, h) in eye:
        ic += 1
        cv2.rectangle(imgout,(xe+xs, ye+ys), (xe+w+xs, ye+h+ys),(250,0,0),2)
        if ic == 2:
            break
    
    cv2.imshow('out',out)

    if cv2.waitKey(1) == ord('q'):
        loop = False
        cv2.destroyAllWindows()
        cam.release()
        break

robot.moveTo(0,0,0.5)
```
Get the current position of the mouse and print it

```python
po = robot.position()
print(po.x)
```

## Result

This project was written by Majid Tajanjari and the Aiolearn team, and we need your support!❤️

# تشخیص چهره

در این پروژه برنامه تشخیص چهره و چشم با پایتون نوشته ایم

## ماژول ها

```python
import cv2
import pyautogui as robot
```

## نحوه استفاده
لودینگ مدل تشخیص چهره و چشم

```python
eye_model = cv2.CascadeClassifier('haarcascade_eye.xml')
face_model = cv2.CascadeClassifier('haarcascade_frontalface_default.xml')
loop = True
```

فعال کردن دوربین و افقی کردن تصویر و تشخیص چهره در تصویر و تشخیص چشم در تصویر چهره

```python
cam = cv2.VideoCapture(0)

while loop:
    _ , img = cam.read()
    
    img = cv2.flip(img, 1)
    gray = cv2.cvtColor(img,cv2.COLOR_BGR2GRAY)

    face = face_model.detectMultiScale(gray)
    
    if len(face) > 0:
        xs = face[0][0]
        ys = face[0][1]
        xs2 = xs + face[0][2]
        ys2 = ys + face[0][3]
        gray_face = gray[ys:ys2,xs:xs2]
        eye = eye_model.detectMultiScale(gray_face, minSize = (30,30), scaleFactor=1.1, minNeighbors=5)
        imgout = img.copy()
```
رسم مستطیل دور چهره

```python
out = cv2.rectangle(imgout, (xs,ys),(xs2,ys2),(0,250,0),3)
    
    white = (250,250,250)
    red = (0,0,250)
    rang = white
    
    mouse_x = robot.position().x
    mouse_y = robot.position().y

    if xs < 400:
        rang = red
        mouse_x -= abs(xs-400)
        robot.moveTo(mouse_x, mouse_y, 0)
    
    if xs2 > 900:
        rang = red
        mouse_x += abs(xs2 - 900)
        robot.moveTo(mouse_x, mouse_y, 0)

    if ys < 100:
        rang = red
        mouse_y -= abs(ys - 100)
        robot.moveTo(mouse_x, mouse_y, 0)

    if ys2 > 600:
        rang = red
        mouse_y += abs(ys2 - 600)
        robot.moveTo(mouse_x, mouse_y, 0)
```

رسم یک مستطیل حاشیه برای حرکت ماوس

```python
out = cv2.rectangle(imgout, (400,100),(900,600),rang,2)

    ic = 0
    for (xe, ye, w, h) in eye:
        ic += 1
        cv2.rectangle(imgout,(xe+xs, ye+ys), (xe+w+xs, ye+h+ys),(250,0,0),2)
        if ic == 2:
            break
    
    cv2.imshow('out',out)

    if cv2.waitKey(1) == ord('q'):
        loop = False
        cv2.destroyAllWindows()
        cam.release()
        break

robot.moveTo(0,0,0.5)
```
رسم موقعیت فعلی ماوس و  چاپ

```python
po = robot.position()
print(po.x)
```

## نتیجه

این پروژه توسط مجید تجن جاری و تیم Aiolearn نوشته شده است و ما به حمایت شما نیازمندیم!❤️