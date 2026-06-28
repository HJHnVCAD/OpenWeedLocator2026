
## Data store in this folder Structure

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
│   ├── dist_coeffs.npy
│   └── README.md              # This file
|

```

L'autocalibration prend une photo automatiquement dès que le damier est present dans le champ de vision à un intervalle de 5 secondes
Paramètre ligne 575 dans owl.py