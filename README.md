# Fashion Product Image-to-Text Prediction

This project aims to predict the display names of fashion products from images using two distinct approaches. The dataset comprises fashion product images and their attributes, such as category, color, brand, and season. The goal is to convert these images into descriptive display names.

## Dataset

The dataset used for this project is the [Fashion Product Images Dataset](https://www.kaggle.com/datasets/paramaggarwal/fashion-product-images-dataset) from Kaggle. It includes:
- **Images** of fashion products.
- **Attributes** for each image, including category, color, brand, and season ([Classification of These Attributes](https://github.com/i4mShayan/Fashion-Product-Multilabel-Classification)).
- **Display Names** which are the target labels we aim to predict.

## Pre-Trained Classification Model

<a href="https://www.kaggle.com/code/shayankebriti/fashion-product-multilable-classification" target="_blank">
  <img src="https://kaggle.com/static/images/open-in-kaggle.svg" alt="Open in Kaggle">
</a>

For the approaches below, I utilize a pre-trained model developed for multi-label classification of fashion products.

You can find the details and code for this model in the [Fashion Product Multilabel Classification repository](https://github.com/i4mShayan/Fashion-Product-Multilabel-Classification).

## Approaches

Implemented two approaches to tackle the image-to-text prediction problem:

### Approach One: End-to-End Transfer Learning with RNN

<a href="https://www.kaggle.com/code/shayankebriti/fashion-product-descriptiongeneration" target="_blank">
  <img src="https://kaggle.com/static/images/open-in-kaggle.svg" alt="Open in Kaggle">
</a>

- **Model**: Utilizes the pre-trained classification model from the [Fashion Product Multilabel Classification repository](https://github.com/i4mShayan/Fashion-Product-Multilabel-Classification) as a feature extractor. An additional RNN (LSTM) head is added to directly predict the display name from the image features.
- **Implementation**: [Kaggle Notebook - Approach One](https://www.kaggle.com/code/shayankebriti/fashion-product-descriptiongeneration)
- **Performance**:
  - **Average BLEU Score**: 0.8994
  - **Average ROUGE-1 F1 Score**: 0.9532
  - **Average ROUGE-2 F1 Score**: 0.9394
  - **Average ROUGE-L F1 Score**: 0.9532
- **Example**:
![image](https://github.com/user-attachments/assets/b973d0b4-5eb2-499c-9713-8772ef2d9cec)

  

### Approach Two: Multi-Stage Model

<a href="https://www.kaggle.com/code/shayankebriti/fashion-product-descriptiongeneration-approach-2" target="_blank">
  <img src="https://kaggle.com/static/images/open-in-kaggle.svg" alt="Open in Kaggle">
</a>

1. **Segment One: Attribute Classification**
   - **Model**: Fine-tuned ResNet-50 model for classifying various attributes of fashion images such as category, base color, brand, and season.
   - **Output**: The predicted classes for each attribute.

2. **Segment Two: Display Name Prediction**
   - **Inputs**: 
     - The class predictions from Segment One.
     - The encoded image features from the ResNet-50 model.
   - **Model**: An RNN (LSTM) model that takes these inputs and predicts the display name of the product.
   - **Implementation**: [Kaggle Notebook - Approach Two](https://www.kaggle.com/code/shayankebriti/fashion-product-descriptiongeneration-approach-2)
   - **Example**:
![image](https://github.com/user-attachments/assets/a8b23f13-1a2c-4ae4-a634-9cada85624a2)

**Note**: The first approach achieved better accuracy in fewer epochs than the second approach.
