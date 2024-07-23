# Road Network Extraction from Satellite Images Using U-Net

This project focuses on extracting road networks from satellite images using a U-Net architecture. The U-Net model, originally developed for biomedical image segmentation, is highly effective for semantic segmentation tasks like ours. Below, we detail the approach, the model architecture, and the results achieved.

## Approach

1. **Data Preparation**
   - **Mounting Google Drive**: Data is stored in Google Drive, and we mount it to access the ZIP files.
   - **Extracting ZIP Files**: Satellite and mask images are extracted from ZIP files to the local directory.
   - **Image Pairing**: Satellite images and their corresponding masks are paired for training and validation.

2. **Data Generator**
   - A custom `DataGenerator` class is implemented using `tf.keras.utils.Sequence` to efficiently load and preprocess image batches.
   - The generator loads images and masks, resizes them, and normalizes the mask values to binary.

3. **Model Architecture**
   - The U-Net model is defined with a series of convolutional and max-pooling layers in the encoder path, and convolutional transpose and concatenate layers in the decoder path.
   - The model outputs a binary mask indicating the presence of road networks.

4. **Training**
   - The model is compiled with the Adam optimizer, binary cross-entropy loss, and accuracy metrics.
   - The training is performed with early stopping and model checkpoint callbacks to monitor validation performance.

5. **Evaluation**
   - Model performance is evaluated using Mean Intersection over Union (IoU) and Dice Coefficient metrics.
   - Predictions are visualized to qualitatively assess the segmentation results.

## Model Architecture

The U-Net architecture consists of the following components:

1. **Input Layer**
   - Input size: `(256, 256, 3)` for RGB satellite images.

2. **Encoder Path**
   - Four blocks of two convolutional layers followed by a max-pooling layer.
   - Filter sizes: 64, 128, 256, 512.

3. **Bottleneck**
   - Two convolutional layers with 1024 filters.

4. **Decoder Path**
   - Four blocks of a convolutional transpose layer followed by two convolutional layers.
   - Filter sizes: 512, 256, 128, 64.

5. **Output Layer**
   - A convolutional layer with a single filter and sigmoid activation to produce the binary mask.

## Results

 **Training and Validation Performance**:
 
    - After 25 epochs
        - loss: 0.0667 
        - accuracy: 0.9749 
        - val_loss: 0.0735 
        - val_accuracy: 0.9729
    - Mean IoU: 0.383
    - Dice Coefficient: 0.0345
    


















![image](https://github.com/user-attachments/assets/298de912-c04b-436e-ab86-8b3e1c87eb21)
