# part-2-cnn-computer-vision
### Task 1: Problem Identification
**Image Classification** is the most appropriate problem type for the given dataset. The dataset consists of images belonging to one of four groups (normal, scratch, dent and stain). The goal is to assign a single categorical label to images (image classification) and not identifying objects with boundaries (object detection) or marking specific boundary pixels (image segmentation).

### Task 2: Dataset Exploration
The dataset is perfectly balanced with 120 images per class. This can prevent the model from developing a bias toward any specific category, which is very helpful.

### Task 3: Image Preprocessing
The dataset is pre-processed for the model training by:
- **Resizing:** all the images were made to be of uniform size. In this case, the size is kept as it's original (96x96 pixels) size
- **Normalising:** The image's pixel values are scaled  [0, 255] to [0, 1] to prevent the weights in the CNN from changing significantly.
- **Splitting:** the dataset was split into 80:20 ratio for testing and training respectively. 384 images are used for training, and 96 images are saved for validation. 
- **Data Augmentation:** since the dataset is pretty small, random flips and rotations are applied to the images during training. This artificially creates new training examples.

### Task 4: CNN Model Creation
The Convolutional neural network (CNN) was built using a sequential architecture.
- **Input Layer:** This layer is formulated to accept the normalised, three-channel colour of 96x96 resolution images.
- **Convolution Layer:** 3 layers are used. The first layer detects basic edges like scratch lines. The second layer detects complex shapes, like that of stains. The third layer detects textures like dents.
- **Pooling Layer:** `MaxPooling2D` follows each convolution to shrink data dimensions and reduce computation.
- **Danse and Output Layers:** A dense layer with `Dropout(0.5)` stops the model from memorising the images. And a 4 neuron dense layer with `activation='softmax'` to give the class probablities.

### Task 5: Model Training and Evaluation
The model was trained for 30 epochs. The training loss decreases with each epoch, meaning the the model was learning well. The training and validation accuracy rise together showing that the model is not overfitting.
The model's Validation accuracy is obtained (~97%). In the confusion matrix, the diagonal cells show high number of correct predictions.

### Task 6: CNN Concept Explanation
- **What is convolution?**  
**Convolution** is a mathematical operation where a small matrix of weights (called a *kernel* or *filter*) moves across the input image pixels. At each position, it performs element-wise multiplication and adds the results together to create a single value in a **Feature Map**. This process allows the network to scan for specific localized patterns, in this case, horizontal lines, edges, or specific textures.

- **Why is pooling used?**  
After the convolution layer finds features, the pooling layer (Max Pooling) reduces the image dimensions by keeping only the highest pixel value. Reducing data dimensions reduces the number of parameters the network needs to process next, preventing overfitting and saving memory. This essentially summarizes the image. This makes the model faster by reducing data size and helping the model recognize a "dent" no matter where it is in the image.

- **Why is ReLU commonly used in CNNs?**  
The **Rectified Linear Unit (ReLU)** activation function changes all negative pixel values to zero to maintain a constant gradient for all positive inputs, allowing deep networks to train much faster. Turning negative values to zero activates fewer neurons, making the network more efficient. It introduces "non-linearity", allowing the model to learn complex, messy real-world shapes.

- **Why are CNNs better than regular feed-forward networks for image data?**  
Regular feed-forward networks require flattening a 2D/3D image into a long 1D vector of pixels before processing. This approach destroys all spatial relationships. CNNs preserve the 2D structure of an image. CNNs use shared weights within moving filters, allowing them to preserve spatial structures.
### Task 7: Business Use Case Mapping
**Field: Manufacturing**  
This CNN mini project maps directly to visual quality control in factories. Checking items for defects manually is slow and expensive. Factory machines use high speed cameras attached on top of conveyor belts. The products roll over the conveyor belt and the camera catches the images and processes them, looking for any imperfections (dents, scratch or stains). This replaces manual inspection, reduces errors and shorten the time to sort through naormal and defected products.

Dataset Source: https://drive.google.com/drive/folders/1akV6po4Nrgkc3yQrJkzA6cJlV-wBvUYs?usp=sharing
