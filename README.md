# Automatic Center of Rotation (COR) Finding Algorithm for CT Reconstruction

## Overview
This project focuses on developing a novel automatic Center of Rotation (COR) finding algorithm in Python, replacing traditional manual calculations. The algorithm enhances computed tomography (CT) data reconstruction, including 4D X-ray CT scans for Li-ion batteries. By implementing and analyzing new research findings, this project aims to improve accuracy and efficiency in CT reconstruction and modeling.

## Features
- Automatic COR detection, eliminating manual adjustments.
- CT data reconstruction with support for advanced methodologies.
- Integration with ASTRA and TomoPy for enhanced reconstruction.
- GPU acceleration for faster processing.
- Intensity clipping & filtering for improved data quality.
- HDF5 data format support.

## Dependencies
Install required libraries:
```bash
pip install numpy scipy matplotlib tomopy astra-toolbox torch h5py
```

## File Structure
- **BAM_CT_Reconstruct.py**: Core module for CT reconstruction and automatic COR detection.
- **Final_Automatic_COR_Findings.pptx**: Presentation detailing methodology and results.
- **Projection Import Modules**: Handles input from HDF5 and other CT scan formats.

## Usage (Unavailable Due to Data Confidentiality)
The usage examples below outline the intended process, but due to company confidentiality, the dataset required to execute these steps is not publicly available. As a result, direct implementation and testing cannot be performed outside the internal environment.
### Load and Process Data
```python
from BAM_CT_Reconstruct import Reconstruction
from projection_import import ProjectionFile

file_path = "path/to/data.h5"
ProjectionFile = ProjectionFile(file_path)
reconstructor = Reconstruction(ProjectionFile, gpu=True)
```

### Perform Automatic COR Finding & Reconstruction
```python
reco_settings = {
    "COR": 1300.5,
    "reco_algorithm": "gridrec",
    "filter_name": "shepp",
    "pixel_size": 0.72,
    "ring_radius": 50,
}
data_slice = reconstructor.on_the_fly_one_slice(reco_settings)
```

### Full Volume Reconstruction
```python
save_settings = {
    "dtype": "float32",
    "fileType": "tif",
    "save_folder": "output/",
}
reconstructor.on_the_fly_volume_reco(reco_settings, save_settings)
```

## Data Confidentiality
Due to company confidentiality, the dataset used in this project is not publicly available. However, the results and methodology are presented below.

## Experiment: Algorithm & Hypothesis Testing

### Hypothesis 
The goal of this experiment is to develop an algorithm that can automatically determine the true Center of Rotation (COR), denoted as C1. Our function should find C1 given an initial guess:

```
COR_finder(COR_first_guess, Slice) → C
```

### Testing Approach
The first hypothesis states that if we are near C1, the closer we get, the lower the standard deviation (std) of the reconstructed image. We test this hypothesis as follows:

1. **Reconstruction Range:** Reconstruct slices for COR values from C - ne to C + ne with n = 10, giving 21 slices in total.
2. **Step Size:** Set e = 1, 10, 20 to observe different levels of granularity.
3. **Plot Analysis:** Plot the standard deviation of the image vs. COR and observe trends.
4. **Cropping Adjustment:** If no meaningful trend is found, crop the reconstructed slice to the image center with a 200px radius and repeat the std vs. COR plot.
5. **Filtering Impact:** Apply mean and median filtering before calculating std to test their effect on the std vs. COR trend.

### Implementation
To find the actual COR, reconstruct images from previous reconstructions and write a loop that reconstructs and saves slices from C - ne to C + ne for e = 1, 10, 20 and n = 10.

## Results
The presentation of the results can be found in the file **Final_Automatic_COR_Findings.pptx**.
- Automatic COR detection improves accuracy over manual methods.
- Enhanced CT reconstruction for better visualization and analysis.
- GPU acceleration significantly reduces processing time.

## Future Work
- Improve robustness for different CT scan types.
- Implement deep learning-based COR estimation.
- Optimize performance for large datasets.

## Contributors
- **Garima Dhakal** – Developer
- **Dr. Henning Markötter** – Legacy Code and Data Import Contributions
- **Dr. Shahabeddin Dayani** – Legacy Code and Data Import Contributions


## License
This project is licensed under the MIT License. See `LICENSE` for details.

