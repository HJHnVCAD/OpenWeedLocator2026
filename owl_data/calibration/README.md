
## Data store without USB Drive is this folder Structure

Before, in 'GENERAL_CONFIG.ini':
```
save_directory = /home/owl/owl/owl_data
```

All files are store in this directory:

```
owl_data/
├── calibration/    folder for image of calibration
│   ├── image1.jpg
│   ├── image2.jpg
│   ├── image3.jpg
│   ├── ...
│   ├── perspective_matrix.npy
│   ├── calibration_meta.json
│   ├── camera_matrix.npy
│   └── dist_coeffs.npy
├── sessioncapture001/    folder for image of session recording
│   ├── image1.jpg
│   ├── image2.jpg
│   ├── image3.jpg  
├── sessioncapture002/
│   ├── ...        
└── README.md              # This file

```
