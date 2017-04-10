# Working with AVFoundation - Recording & Saving Video & Audio

### Objectives

- Record and save assets(video, audio, images) with AVFoundation
- Export recorded assets

## AVCaptureSession

Coordinates the flow of data between inputs and outputs.
A single session of AVCaptureSession can handle multiple inputs and outputs (you do not need to create multiple sessions)

![Capture session](avcapturesession.png)

```swift
var captureSession = AVCaptureSession()
```

### Starting and Stopping a session

Starting an AVCaptureSessions allows data to flow between the input and output connections

### AVCaptureConnection

It represents a connection between an input and an output to an AVCaptureSession

### AVCaptureDevice

### AVCaptureInput

### AVCaptureOutput


### Video Capture Preview

To show a user a preview of the video capture, you will need to use a AVCaptureVideoPreviewLayer.

You can set the preview layer's session to your instance of AVCaptureSession
