# Deep-Learning-on-Facial-Depth-Maps-for-Predicting-Obstructive-Sleep-Apnea-OSA-
osa is is a common yet underdiagnosed condition that causes repeated airway blockages during sleep. Traditional diagnosis using Polysomnography (PSG) is accurate but costly and not easily accessible.This project  uses of deep learning to predict OSA risk from lateral cephalometric X-ray images, offering a low-cost, non-invasive screening This project explores the use of deep learning to predict OSA risk from lateral cephalometric X-ray images, offering a low-cost, non-invasive screening alternative.We implemented a convolutional neural network (CNN) based on ResNet-18, trained on the Aariz Cephalometric Dataset, which consists of grayscale craniofacial radiographs. Due to the lack of actual OSA diagnostic labels in the dataset, we used simulated binary labels to validate the pipeline structure. The images were resized to 224×224 pixels, normalized, and augmented for training.To make the model explainable, we integrated Grad-CAM, which highlighted facial regions that influenced predictions. The model consistently focused on clinically relevant zones like the jawline and upper airway. On the validation set of 147 images, the model achieved an accuracy of 48.98%, recall of 87.84%, and an F1-score of 63.41%.
Although trained with synthetic labels, the system demonstrates technical feasibility and lays the foundation for future integration with real OSA clinical data. This project provides a reproducible, scalable framework for AI-assisted OSA risk screening, with potential applications in mobile health and telemedicine.
## 📂 Dataset
This project uses the **Aariz Cephalometric Dataset**, which contains:
- 2D lateral cephalometric X-ray images (PNG)
- 29 anatomical landmark annotations (JSON)
- CVM (Cervical Vertebrae Maturation) labels
- Pixel-to-mm metadata (CSV)

➡️ Note: The dataset does **not** include real OSA labels.  
Simulated binary labels (0 = Non-OSA, 1 = OSA) were used to validate the pipeline.

## 🧠 Methodology
1. Load and preprocess lateral X-ray images  
2. Resize to 224×224, convert to RGB, normalize  
3. Apply data augmentation (rotation, flip)  
4. Fine-tune pretrained **ResNet-18**  
5. Modify final FC layer → 2 classes (OSA/Non-OSA)  
6. Train using CrossEntropyLoss + Adam optimizer  
7. Generate explainability maps using **Grad-CAM**  
8. Evaluate using Accuracy, Precision, Recall, F1-score

   
## 🏗️ Model Architecture (ResNet-18)
- Input: 224×224×3  
- 7×7 Conv + MaxPooling  
- Residual Blocks: 64 → 128 → 256 → 512  
- Global Average Pooling  
- Fully Connected (2 neurons)  
- Softmax output (OSA / Non-OSA)

<img width="171" height="768" alt="cnn flow" src="https://github.com/user-attachments/assets/bb613fef-f700-4a51-934a-f5bd06aa7420" />
<img width="348" height="930" alt="flow chart" src="https://github.com/user-attachments/assets/3941fd52-a9f6-47c4-924d-ca75a0c2ea04" />

## 🔍 Grad-CAM Explainability
Grad-CAM was used to highlight which craniofacial regions influenced the model's decision.

The heatmaps focused on:
- Posterior airway space  
- Mandibular plane  
- Tongue base  
- Jaw structure  

These regions align with known anatomical indicators of OSA.

## 📈 Results
The model predicted OSA vs Non-OSA with probability scores.

### Sample OSA Risk Levels:
| Image | Probability |
|-------|-------------|
| 1     | 76%         |
| 2     | 91%         |
| 3     | 86%         |
| ...   | ...         |

### Grad-CAM Outputs
Below are visualization examples showing model focus regions.
## 📊 Performance Metrics

| Metric      | Score    |
|-------------|----------|
| Accuracy    | 48.98%   |
| Precision   | 49.62%   |
| Recall      | 87.84%   |
| F1-Score    | 63.41%   |

⚠️ *Note:* Performance is limited by simulated labels.  
The pipeline is technically validated, but clinical accuracy requires real OSA labels.





