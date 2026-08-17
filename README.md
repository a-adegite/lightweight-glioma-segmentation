# Lightweight Glioma Segmentation on Low-Resource Systems

A lightweight 3D U-Net-based brain tumor segmentation pipeline designed for multi-modal MRI segmentation, with an emphasis on reproducibility and deployment on CPU-constrained systems.

This project follows the Lightweight Brain Tumor Segmentation on Low-Resource Systems: A Step-by-Step Guide with 3D U-Net tutorial developed by the Medical Artificial Intelligence (MAI) Lab and extends the workflow through model inference and practical deployment using Streamlit.


## Live Demo

The trained segmentation model is integrated into an interactive Streamlit application.

**Try the deployed application:**

https://lightweight-glioma-segmentation-jrr3vk4aqgmjzj5ygytfd7.streamlit.app/

The application allows users to:

- Upload four MRI modalities in NIfTI format
- Preprocess the MRI volumes
- Construct a multi-modal 3D input
- Run 3D U-Net inference
- Visualize segmentation results
- Download the predicted segmentation mask as a NIfTI file

> **Note:** This application is intended for research and educational purposes only. It is not a clinically validated diagnostic tool and should not be used for clinical decision-making.


## Project Overview

Brain tumor segmentation is an important task in medical image analysis because it enables the identification and delineation of tumor regions from magnetic resonance imaging (MRI) scans.

This project implements an end-to-end lightweight 3D segmentation workflow covering:

1. MRI data preparation and preprocessing
2. Multi-modal MRI input construction
3. 3D U-Net model development
4. Model training and evaluation
5. Training history tracking
6. CPU-oriented inference
7. Interactive model deployment using Streamlit

The project is designed around the principle of making deep learning-based medical image segmentation more accessible in environments where high-performance GPUs may not be available.


## Model

The segmentation model is based on a **3D U-Net architecture**.

The model receives four MRI modalities as input channels:

| Modality | Description |
|----------|-------------|
| **T1n** | Native T1-weighted MRI |
| **T1c** | Contrast-enhanced T1-weighted MRI |
| **T2w** | T2-weighted MRI |
| **T2f** | T2-FLAIR MRI |

These four modalities are combined into a multi-channel 3D volume and passed to the 3D U-Net for voxel-wise tumor segmentation.

The trained model is used for inference in the Streamlit application.


##  Dataset

The project follows the workflow described in the MAI Lab tutorial using the **BraTS-Africa 2024** dataset.

The dataset provides multi-modal MRI volumes that are processed and combined into a four-channel input representation.

### MRI Modalities

| Modality | Role |
|----------|------|
| T1n | Native anatomical information |
| T1c | Contrast-enhanced tumor information |
| T2w | T2-weighted anatomical information |
| T2f | Fluid-attenuated inversion recovery information |

Each modality is independently loaded and preprocessed before being combined for model inference.


## Preprocessing Pipeline

The inference pipeline performs the following operations:

1. Load the uploaded NIfTI MRI volumes.
2. Identify each MRI modality from its filename.
3. Normalize the image intensities.
4. Combine T1n, T1c, T2w, and T2f into a four-channel volume.
5. Crop the volume to the region used by the model.
6. Resize the volume to the model's expected input dimensions.
7. Add the batch dimension.
8. Run inference using the trained 3D U-Net.
9. Convert the model output into a voxel-wise segmentation using `argmax`.
10. Upsample the predicted segmentation to the processed volume size.
11. Save the prediction as a NIfTI file.

## Deployment

The model is deployed using Streamlit, allowing inference through a web-based interface.

The application is designed to support CPU-based inference and does not require the user to have a local GPU.

## Repository Structure

The repository separates the model development workflow from the deployment application.

```text
lightweight-glioma-segmentation/
│
├── notebooks/
│   ├── bt_processing.ipynb
│   └── bt_segmentation.ipynb
│
├── model_history/
│   └── training_history.csv
│
├── app.py
├── requirements.txt
└── README.md
```

## Project Dependecies

The application uses the following major Python packages:

- Python 3.12
- TensorFlow / Keras
- NumPy
- NiBabel
- scikit-learn
- SciPy
- Matplotlib
- Streamlit
- gdown

The complete dependency list is available in the [`requirements.txt`](https://github.com/a-adegite/lightweight-glioma-segmentation/blob/main/requirements.txt) file.

## Limitations

The current implementation has several limitations:

- Inference is CPU-oriented and may take several minutes depending on the available hardware.
- The application expects all four MRI modalities.
- Input files must follow the expected modality naming convention.
- The deployed model has not undergone clinical validation.
- The predicted segmentation should not be interpreted as a clinical diagnosis.
- Model performance may vary depending on differences between training data and user-provided MRI scans.

## Limitations

The current implementation has several limitations:

- Inference is CPU-oriented and may take several minutes depending on the available hardware.
- The application expects all four MRI modalities.
- Input files must follow the expected modality naming convention.
- The preprocessing pipeline assumes MRI volumes are compatible with the spatial assumptions used during model development.
- The deployed model has not undergone clinical validation.
- The predicted segmentation should not be interpreted as a clinical diagnosis.
- Model performance may vary depending on differences between training data and user-provided MRI scans.

## Disclaimer

This project is intended for **research, educational, and demonstration purposes only**.

The model and Streamlit application have not been clinically validated and should not be used as a substitute for professional medical diagnosis, treatment planning, or clinical decision-making.

Predictions should be interpreted by appropriately qualified professionals within the appropriate clinical or research context.

## References

[1] Oladele, A., Confidence, R., Zhang, D., Umoren, C., Iorumbur, A. M.,
Gbadamosi, A., Dako, F., Adewole, M., & Anazodo, U. (2025).
*Lightweight Brain Tumor Segmentation on Low-Resource Systems:
A Step-by-Step Guide with 3D U-Net*. protocols.io, Version 5.
https://dx.doi.org/10.17504/protocols.io.dm6gpdwmdgzp/v5

[2] Ronneberger, O., Fischer, P., & Brox, T. (2015).
U-Net: Convolutional Networks for Biomedical Image Segmentation.
In *MICCAI 2015*, pp. 234–241.
https://doi.org/10.1007/978-3-319-24574-4_28

## Acknowledgements

This project was developed as an implementation and deployment exercise based on the Medical Artificial Intelligence (MAI) Lab tutorial on lightweight brain tumor segmentation.

The original protocol was collaboratively developed by researchers at the MAI Lab, Lagos, Nigeria, and participants of the **SPARK AI Training for African Medical Imaging Knowledge Translation** programme.

Special acknowledgement is given to the authors of the original protocol and the contributors to the BraTS-Africa dataset.


## License

This repository is intended for educational and research use.

Please refer to the licensing terms of the original dataset, protocol, model, and third-party resources before redistributing or using this project for other purposes.
