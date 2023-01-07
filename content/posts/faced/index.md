+++
title = "Faced"
description = "A simple and fast face recognition system"
date = 2023-07-01
path="faced"
template="page.html"

[taxonomies]
categories = ["tech"]
tags = ["face-recognition"]

[extra]
metadata_image = "/face.png"
+++

{% cover(src="face.png") %}
Face Recognition
{% end %}

### Creating a Face Recognition System in Go

Go is a popular programming language that is known for its simplicity, efficiency, and concurrency support. In this blog, we will look at how to create a face recognition system using Go and the Kagami Go Face library.

### Prerequisites
Before we begin, there are a few prerequisites that you will need to have in order to follow along:

- A basic understanding of Go programming
- A working installation of Go on your machine
- A webcam or other means of capturing video input

### Step 1: Setting Up Kagami Go Face
Kagami Go Face is a Go library for facial recognition and detection. It is built on top of the popular OpenCV library, and provides a simple and easy-to-use interface for Go developers.

To get started with Kagami Go Face, you will need to install it on your machine. The easiest way to do this is to use go get:

``` go get -u github.com/Kagami/go-face ```
This will install Kagami Go Face and all of its dependencies. You can then import it into your Go code by adding the following line at the top of your file:

``` import "github.com/Kagami/go-face" ```
### Step 2: Capturing Video Input
The first step in creating our face recognition system is to capture video input from the webcam. We can do this using the VideoCapture function from Kagami Go Face:

```
webcam, err := face.NewWebcam()
if err != nil {
    fmt.Println(err)
    return
}
defer webcam.Close()
```

This will create a new Webcam object that is connected to the default webcam (which is usually device 0). We can then use this object to capture frames from the webcam and process them.

### Step 3: Detecting Faces
Next, we will use Kagami Go Face to detect faces in the video frames. Kagami Go Face provides a number of different algorithms for face detection, including Haar cascades and Deep Learning.

For this example, we will use a Haar cascade:


``` detector := face.NewCascadeDetector("haarcascade_frontalface_default.xml") ```


This will create a new CascadeDetector object and load the Haar cascade XML file. We can then use this object to detect faces in the video frames.

### Step 4: Recognizing Faces
Once we have detected the faces in the video frames, we can use Kagami Go Face's face recognition algorithms to recognize them. Kagami Go Face provides several different algorithms for face recognition, including Eigenfaces, Fisherfaces, and LBPH.

For this example, we will use the LBPH algorithm:
```
recognizer := face.NewLBPHRecognizer()
defer recognizer.Close()

// Train the recognizer on a dataset of known faces
if err := recognizer.Train(faceData, labels); err != nil {
    fmt.Println(err)
    return
}
```
This will create a new LBPHRecognizer object and train it on a dataset of known faces. We can then use this object to recognize the faces in the video frames.

### Step 5: Displaying Results
Finally, we will display the results of the face recognition on the screen. This can be done using the PutText function from Kagami Go Face:
```
for {
    frame, _ := webcam.Read()
    if frame.Empty() {
        continue
    }

    // Detect and recognize faces in the frame
    rects, names, _ := recognizer.Recognize(frame)
    for i, r := range rects {
        // Display the name of the recognized face
        gocv.PutText(&frame, names[i], image.Pt(r.Min.X, r.Min.Y-20), gocv.FontHersheyPlain, 1.2, color.RGBA{0, 0, 255, 0}, 2)
        // Draw a rectangle around the face
        gocv.Rectangle(&frame, r, color.RGBA{0, 0, 255, 0}, 2)
    }

    // Display the frame
    window.IMShow(frame)
    if window.WaitKey(1) >= 0 {
        break
    }
}
```
This will loop through the detected and recognized faces, displaying the name of each face and drawing a rectangle around it. The resulting video stream will show the recognized faces in real-time.

Conclusion
Creating a face recognition system in Go with Kagami Go Face is a relatively simple and straightforward process. By following the steps outlined above, you can build a powerful and efficient face recognition system that can be used.

### References

- [Kagami Go Face](https://github.com/shikharvashistha/faced)