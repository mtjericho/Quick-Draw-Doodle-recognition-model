# Quick, Draw! Doodle Recognition Challenge
Predict accurately the label of the drawings with a maximum of 3 guesses.
[based on this competition](https://www.kaggle.com/c/quickdraw-doodle-recognition).

---

## Problem Statement

With a dataset of over 50million hand drawn drawings and 340 labels, we are tasked by Google to build a better classifier for the existing Quick, Draw! dataset. This will have an immediate impact on handwriting recognition and its robust applications in areas including OCR (Optical Character Recognition), ASR (Automatic Speech Recognition) & NLP (Natural Language Processing).

As data scientists, we would like to build a predictive model that can predict accurately the label of the drawings with a maximum of 3 guesses. Hence our target metric is accuracy or more specifically the top 3 accuracy. With a better predictive model, Google will be able to immediately improve their handwritten recognition models and/or develop a way to capitalise on the model.

---

## Dataset

|     Key     |           Type          |                                   Description                                   |
|:-----------:|:-----------------------:|:-------------------------------------------------------------------------------:|
| key_id      | 64-bit unsigned integer | A unique identifier across all drawings.                                        |
| word        | string                  | Category the player was prompted to draw.                                       |
| recognized  | boolean                 | Whether the word was recognized by the game.                                    |
| timestamp   | datetime                | When the drawing was created.                                                   |
| countrycode | string                  | A two letter country code (ISO 3166-1 alpha-2) of where the player was located. |
| drawing     | string                  | A JSON array representing the vector drawing                                    |

---

## CNN Models

| Models          | Train top 3 accuracy | Test top 3 accuracy | Kaggle Score |
|-----------------|----------------------|---------------------|--------------|
| Custom CNN      | 0.74                 | 0.76                | 0.61         |
| VGG16 (32x32)   | 0.55                 | 0.57                | Did not try  |
| VGG16 (128x128) | 0.76                 | ***0.78***                |0.62              |

Our best model is the VGG16 with 128x128 images. It is evident that a higher dimension image is better for a pre-trained model. However the tradeoff is that we are not able to read in a lot of images due to RAM limitations. The train score and test score do not show signs of overfitting as the scores are pretty close 0.76 and 0.78 respectively. However we only got 0.62 for the kaggle score. One likely reason is our model has not trained on enough images from the train set and it is not able to generalize well to new images outside our test set. There are over 50million images and we only trained on less than a million images.

Limitations: Our model is only able to predict images from the 340 classes. It will not be able to predict drawings out of the 340 classes. It will instead predict the class that is closest to the 'never-before-seen' image.

Further improvements: However our model is still able to predict drawings quite well with 3 guesses. Given more time and with a more powerful cloud computer, we can improve our model by reading in 224x224 images instead and training on the entire train dataset.

---

## Conclusion and Recommendations

Google will be able to build upon our model and further improve it with their expertise and computing power. One way they can capitalize on an improved model will be to create a toddler programme/application that is able to guide the toddler if he/she is drawing the right image. This will help toddlers learn how to draw and develop artistic talent at an early age.

---
