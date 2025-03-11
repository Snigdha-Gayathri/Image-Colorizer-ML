# Automatic Image Colorization with OpenCV and Deep Learning

This repository contains a Python script that demonstrates automatic image colorization using deep learning. It leverages OpenCV's Deep Neural Network (DNN) module to load and execute a pre-trained Caffe model, effectively adding color to grayscale images.

## Overview

The project utilizes a convolutional neural network (CNN) trained to predict the chromaticity (ab) channels of an image given its luminance (L) channel. This process transforms a grayscale image into a colorized version.

## Prerequisites

Before running the script, ensure you have the following installed:

* **Python 3.x:** (Recommended)
* **NumPy:** `pip install numpy`
* **OpenCV (cv2):** `pip install opencv-python`

## Model Files

You will need the following model files, which should be placed in a `Model` folder within the project directory:

* `colorization_deploy_v2.prototxt`: The Caffe model architecture.
* `colorization_release_v2.caffemodel`: The pre-trained weights of the model.
* `pts_in_hull.npy`: Cluster centers for the ab color space.

**Where to Download the Model Files:**

* These files can be found in several places, including GitHub repositories related to the original research and OpenVINO Toolkit resources.
    * Specifically look at this github page.
        * [https://github.com/richzhang/colorization/tree/caffe/colorization/models](https://github.com/richzhang/colorization/tree/caffe/colorization/models)
        * And this one for the npy file.
        * [https://github.com/richzhang/colorization/blob/caffe/colorization/resources/pts_in_hull.npy](https://github.com/richzhang/colorization/blob/caffe/colorization/resources/pts_in_hull.npy)
    * You can also find them within repositories related to OpenCV examples, as OpenCV often provides sample code that utilizes these models.
    * The OpenVINO Toolkit also hosts these files, which can be a reliable source.
        * [https://storage.openvinotoolkit.org/repositories/datumaro/models/colorization/](https://storage.openvinotoolkit.org/repositories/datumaro/models/colorization/)
    * For the caffemodel file, this link was found to be functional.
        * [https://www.dropbox.com/scl/fi/d8zffur3wmd4wet58dp9x/colorization_release_v2.caffemodel?rlkey=iippu6vtsrox3pxkeohcuh4oy&dl=0](https://www.google.com/search?q=https://www.dropbox.com/scl/fi/d8zffur3wmd4wet58dp9x/colorization_release_v2.caffemodel%3Frlkey%3Diippu6vtsrox3pxkeohcuh4oy%26dl%3D0)

## Usage

1.  **Clone the Repository:**
    ```bash
    git clone [repository URL]
    cd [repository directory]
    ```

2.  **Place Model Files:**
    * Create a folder named `Model` in the project directory.
    * Download the model files and place them inside the `Model` folder.

3.  **Place your image:**
    * Place the image that you want to colorize in the same directory as the python script.
    * Change the `img_path` variable within the python script to the name of your image.

4.  **Run the Script:**
    ```bash
    python colorizer.py
    ```

5.  **View the Results:**
    * The script will display a window showing the original grayscale image and the colorized version side by side.
    * Press any key to close the window.

## Code Explanation

The `colorizer.py` script performs the following steps:

1.  **Load Model and Kernel:**
    * Loads the pre-trained Caffe model using `cv2.dnn.readNetFromCaffe()`.
    * Loads the cluster centers from `pts_in_hull.npy` using `numpy.load()`.

2.  **Preprocess Image:**
    * Reads the input image using `cv2.imread()`.
    * Scales the pixel values to the range [0, 1].
    * Converts the image from BGR to LAB color space using `cv2.cvtColor()`.
    * Resizes the LAB image to 224x224 pixels.
    * Extracts the L channel and performs mean subtraction.

3.  **Colorization:**
    * Sets the model input to the preprocessed L channel using `net.setInput()`.
    * Performs forward propagation to predict the ab channels using `net.forward()`.
    * Resizes the predicted ab channels to the original image dimensions.
    * Combines the original L channel with the predicted ab channels.
    * Converts the image from LAB to BGR color space.
    * Clips the pixel values to the range [0, 1] and converts them to 8-bit integers.

4.  **Display Results:**
    * Resizes the original and colorized images for display.
    * Concatenates the images horizontally using `cv2.hconcat()`.
    * Displays the combined image using `cv2.imshow()`.

## Contributing

Contributions are welcome! If you find any bugs or have suggestions for improvements, feel free to open an issue or submit a pull request.

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.
