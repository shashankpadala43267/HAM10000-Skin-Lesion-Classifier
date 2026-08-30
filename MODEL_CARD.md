#Model Card: HAM10000 EfficientNetB0 Classifier

#Model Details
Developed by: Shashank Padala (independent, educational project)
Model type: Convolutional neural network (transfer learning)
Architecture: EfficientNetB0, fine-tuned
Framework: TensorFlow / Keras
Training approach: Frozen-base training followed by fine-tuning of the final EfficientNetB0 layers
Input: Dermoscopic skin lesion images
Output: One of 7 lesion class labels, with per-class confidence scores
#Intended Use

This model was built as an educational project to practice the full applied deep learning workflow: data handling, leakage prevention, imbalanced classification, transfer learning, fine-tuning, and rigorous evaluation.

#Intended uses:

Learning and demonstrating deep learning / computer vision techniques
Portfolio and coursework purposes
A basis for further experimentation (e.g., Grad-CAM, architecture comparisons)

#Out-of-scope uses:

Medical diagnosis or screening of any kind
Any clinical decision-making
Any use that replaces a licensed healthcare professional
Training Data
Dataset: HAM10000 ("Human Against Machine with 10000 training images")
Classes (7): akiec (actinic keratoses), bcc (basal cell carcinoma), bkl (benign keratosis-like lesions), df (dermatofibroma), mel (melanoma), nv (melanocytic nevi), vasc (vascular lesions)
Split strategy: Images were split by lesion ID, not image ID, so that images of the same physical lesion cannot appear across the training, validation, and test sets. This reduces (though does not fully eliminate) the risk of data leakage inflating performance.
Split sizes: 7,002 training / 1,519 validation / 1,494 test images
Class balance: The dataset is significantly imbalanced — nv (melanocytic nevi) makes up the large majority of images, while classes like df and vasc have far fewer examples.
Training Procedure
Metadata validation and image-path mapping
Data augmentation (applied to the training set)
Class weighting to reduce (not eliminate) the impact of class imbalance
Initial training with the EfficientNetB0 base frozen
Fine-tuning: unfreezing the final EfficientNetB0 layers and continuing training at a lower learning rate
Evaluation Results

Final results on the held-out test set (1,494 images), after fine-tuning:

#Metric	Value
Test Accuracy	72.49%
Balanced Accuracy	66.76%
Macro F1 Score	53.52%
Macro ROC-AUC	92.39%

How to read these numbers:

#Test accuracy (72.49%) is the raw fraction of correct predictions. Because the dataset is imbalanced, this metric alone can overstate real performance — a model that mostly predicts the majority class (nv) would already score fairly well on raw accuracy overall.
Balanced accuracy (66.76%) averages recall across all 7 classes equally, regardless of how many images each class has. This is a fairer read of performance across rare and common classes alike.
Macro F1 (53.52%) is lower than balanced accuracy, which indicates that while the model finds a reasonable share of true cases in each class (recall), its precision is uneven — it produces more false positives for some classes than others.
Macro ROC-AUC (92.39%) measures how well the model ranks/separates classes by confidence score, independent of the specific decision threshold. This being notably higher than the other metrics suggests the model has learned meaningful class-discriminative features, even where the final categorical decision is sometimes wrong.

See the confusion matrix and per-class recall chart in the README for the full breakdown by lesion type.

#Limitations
The dataset is highly imbalanced, and performance is not uniform across classes — rarer classes (e.g., df, vasc) are harder for the model to learn reliably.
The model produces some high-confidence incorrect predictions (see error analysis in the README).
Results are specific to HAM10000 and may not generalize to other imaging equipment, patient populations, or skin tones not well represented in the dataset.
The model uses image data only — no patient history, symptoms, or other clinical context is incorporated.
This model has not undergone any clinical validation and is not a substitute for professional medical evaluation.

#Ethical Considerations
Medical imaging datasets, including HAM10000, are not necessarily representative of all patient populations (e.g., skin tone diversity). Any real-world deployment of a model like this — which this project explicitly does not attempt — would require rigorous clinical validation, regulatory review, and fairness auditing across demographic groups before any clinical use could be considered responsible.

#Future Work
Grad-CAM or similar visual explanations to show which image regions drive predictions
Additional imbalance-handling techniques (e.g., focal loss)
Comparison against other architectures (ResNet50, MobileNetV2)
Precision-recall curves per class
Broader external validation on other dermoscopic datasets
