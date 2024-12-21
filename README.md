# GazeT dataset
Dataset for 2D gaze direction estimation

![image](https://github.com/user-attachments/assets/b48bb6aa-bc8e-4ec4-8a90-5cfb24cde36e)

## Overview
GazeT dataset consists of 6744 sessions obtained through crowdsourcing and contains 144k annotated photos of operators in front of screen for the task of determining 2D gaze direction. The sample for training and testing was collected using toloka. The markers were asked to click on points on the screen and at the moment of clicking, the relative coordinate of the screen and the photo of the person at that moment were fixed. The marker also had to enter the diagonal of his screen and the type of his device (PC or laptop). See paper for details.

For more information, please address our [paper](http://www.jip.ru/2024/421-429-2024.pdf).

## Comparison to other datasets

| Dataset | Number of unique persons | Number of photos |
| ------ | ----------- | ---- |
| MPIIGaze | 15 | ∼213k |
| Gaze360 | 238 | ∼100k | 
| ETH-XGaze | 110 | ∼1kk |
| EYEDIAP | 16 | ∼85k |
| GazeCapture | ~1,5k | ∼2,5kk |
| GazeT | ~6,7k | ∼144k |

## Download
If you would like to access the GazeT dataset, please fill out this [google form](https://docs.google.com/forms/d/e/1FAIpQLSciF9ur9a6BZbK7l66msrRwXeKFsaW2kki9HBj2sk0JTm7Mtw/viewform?usp=sf_link). The download link will be sent to you once the form is accepted.

Please cite our paper in your publications if the GazeT dataset is used in your research:
```
@article{красильников2024gazet,
  title={GazeT: улучшение определения трехмерного вектора направления взгляда оператора},
  author={Красильников, МД and Никитин, МЮ},
  journal={Информационные процессы},
  volume={24},
  number={4},
  pages={421--429},
  year={2024}
}
```

## Data reading and data structure
Load dataset and put it under `./dataset`. Dataset contains images and metadata. Data loading process and visualizations can be found in `load_dataset.ipynb`.

### Crop design
The bbox for the crop is determined by four points of eyes using the following algorithm:
- the centers and sizes of the eyes are calculated.
- the size of the indentation from the centers of the eyes is considered to be the average between the size of the right and left eyes (mean_dist)s.
- The crop box is designed so that the distance from its borders to the corresponding nearest center of the eye is equal to mean_dist.

### Metadata description

```
`task_id`: str - each collected session has a unique task number
`step`: str - the name of a specific frame within the session
`relative_x`: float - the relative coordinate of the horizontal direction of view (0 is the left edge of the screen, 1 is the right)
`relative_y`: float - the relative coordinate of the vertical direction of view (0 is the top of the screen, 1 is the bottom)
`screen_size_x`: int - width in pixels (screen resolution)
`screen_size_y`: int - height in pixels (screen resolution)
`screen_size_cm_x`: float - screen width in centimeters
`screen_size_cm_y`: float - screen height in centimeters
`diagonal_cm`: float - the diagonal of the screen in centimeters
`type`: str - point type. gaze_on_fixed_point - a pre-specified point (most often the corners and center of the screen), gaze_on_random_point - random point
`is_notebook`: bool - true if the performer indicated that he has a laptop
`eyes_left_left`: Tuple[float, float] - coordinates of the left corner of the left eye
`eyes_left_right`: Tuple[float, float] - coordinates of the right corner of the left eye
`eyes_right_left`: Tuple[float, float] - coordinates of the left corner of the right eye
`eyes_right_right`: Tuple[float, float] - coordinates of the right corner of the right eye
```

## Privacy Statement

This dataset is released under the [Terms to Use GazeT](https://docs.google.com/forms/d/e/1FAIpQLSciF9ur9a6BZbK7l66msrRwXeKFsaW2kki9HBj2sk0JTm7Mtw/viewform?usp=sf_link), which is provided "as it is" and we are not responsible for any subsequence from using this dataset. If you feel uncomfortable about your identity shown in this dataset, please contact us and we will remove corresponding information from the dataset.

