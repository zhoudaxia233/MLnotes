**Morphological Image Processing Basics**

1. **Thresholding**: Converting a greyscale image to monochrome (binary image).  
   e.g. [Otsu Thresholding](http://www.labbookpages.co.uk/software/imgProc/otsuThreshold.html)

2. **Erosion**: it can remove thin lines and isolated dots in a binary image. The result of erosion is always a subset of the original image (w.r.t. pixels in the image).

3. **Dilation**: quite the opposite of **Erosion**.

4. **Opening**: *Erosion* first, then *Dilation*. It can be used to break narrow bridges and/or eliminate thin structures in the original image.

5. **Closing**: *Dilation* first, then *Erosion*. It can be used to fuse narrow breaks and/or eliminate small holes in the original image.

6. **Watershed Transformation**:

    6.1. Distance Transform:  
      1. [A intuitive explanation](https://homepages.inf.ed.ac.uk/rbf/HIPR2/distance.htm)
      2. [The Watershed Transform: Strategies for Image Segmentation](https://ww2.mathworks.cn/company/newsletters/articles/the-watershed-transform-strategies-for-image-segmentation.html)

    6.2. Watershed Transformation applied in image segmentation:  

      1. [Image Segmentation with Watershed Algorithm](https://opencv-python-tutroals.readthedocs.io/en/latest/py_tutorials/py_imgproc/py_watershed/py_watershed.html)

<br />

**Additional:** [this link](https://www.youtube.com/watch?v=IcBzsP-fvPo) leads to a very good video lecture about morphological image processing.
