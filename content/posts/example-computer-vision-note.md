+++
date = '2026-11-01'
draft = false
title = 'OpenCV uses BGR, not RGB'
tags = ['computer-vision', 'opencv']
+++

`cv2.imread()` loads images as **BGR**, not RGB, for historical reasons
(early camera hardware/codec vendors used that channel order). If you're
mixing OpenCV with `matplotlib` or `PIL`, convert first:

```python
import cv2

img_bgr = cv2.imread("photo.jpg")
img_rgb = cv2.cvtColor(img_bgr, cv2.COLOR_BGR2RGB)
```

Forgetting this swap is a classic source of "why do my colors look wrong"
bugs.
