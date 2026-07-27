#Model Card: HAM10000 EfficientNetB0 Classifier

#Model Description

This project uses EfficientNetB0 transfer learning to classify dermoscopic images into seven categories from the HAM10000 dataset.

#Intended Use

This model was created for:

- Educational machine-learning practice
- Computer-vision research
- Transfer-learning experimentation
- Model evaluation and error analysis

#Out-of-Scope Uses

This model must not be used for:

- Medical diagnosis
- Patient screening
- Treatment decisions
- Emergency decisions
- Replacing a dermatologist or medical professional

#Dataset

The model was trained and evaluated using the HAM10000 dataset.

#Architecture

- EfficientNetB0
- Transfer learning
- Seven output categories
- TensorFlow and Keras

#Evaluation Results

- Test accuracy: 41.70%
- Balanced accuracy: 59.20%
- Macro F1 score: 33.52%
- Macro recall: 59.20%

#Limitations

- Strong class imbalance
- Uneven performance among categories
- High-confidence incorrect predictions
- Limited generalization beyond HAM10000
- No patient history or clinical context
- No clinical validation

#Ethical Considerations

Incorrect predictions could be harmful if treated as medical information. This model is an educational experiment and must not be used to make healthcare decisions.

#Disclaimer

This project is for educational machine-learning research only. It is not a medical diagnostic system.