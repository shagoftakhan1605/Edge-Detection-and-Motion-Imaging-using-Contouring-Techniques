# Motion Detection and Motion Imaging with Optical Flow

A webcam script with two modes, both based on Farneback dense optical flow in OpenCV:

1. **Motion edge detection:** outlines moving regions with green contours and shows "Motion Detected" when anything moves
2. **Motion imaging:** colours each pixel by the direction (hue) and speed (brightness) of its motion

All code is in [`edge_motion_detection.py`](edge_motion_detection.py).

---

## How It Works

**Mode 1: Motion edge detection**
* Computes optical flow between consecutive grayscale frames
* Pixels whose flow magnitude is above a threshold are marked as moving
* Outer contours of the moving regions are drawn in green on the live frame
* A **Sensitivity** trackbar (0 to 50, default 2) sets the threshold: lower values pick up smaller movements

**Mode 2: Motion imaging**
* Computes the same optical flow
* Converts each flow vector to angle and magnitude, then to an HSV image: hue = direction, saturation = full, value = normalised speed
* Shows the original frame and the colour-coded motion side by side

---

## How to Run

```bash
pip install -r requirements.txt
python edge_motion_detection.py
```

Type `1` (motion edge detection) or `2` (motion imaging) when asked, then press `q` in the video window to quit.

---

## Fix in This Version

The motion imaging hue was divided by 4 instead of 2, so directions only used half of the colour wheel. It now spans the full OpenCV hue range (0 to 179).

The previous README described Laplacian, Sobel and Canny edge detection; these are not used in the code, so that description was removed.

---

## Limitations

* Optical flow is computed on every full frame, which can be slow on large webcam images
* Camera shake is detected as motion
* No recording or saving of results

---

## Tools

Python, OpenCV, NumPy

## License

Apache License 2.0 (see [LICENSE](LICENSE)).
