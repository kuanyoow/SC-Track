

### What's SC-Track?

SC-Track is an efficient multi-object cell tracking algorithm that can generate accurate single cell linages from the segmented nucleus of timelapse microscopy images. It employs a probabilistic cache-cascade matching model that can tolerate noisy segmentation and classification outputs, such as randomly missing segmentations and false detections/classifications from deep learning models. It also has a built-in cell division detection module that can assign mother-daughter relationships using the outline information of cells.

SC-Track allows users to use two different segmentation results as input. It can either take:
1) A greyscale Multi-TIFF image, where every segmented instance of cells is given a unique pixel value and the background set as 0.
2) A VGG image annotator (VIA2) compatible JSON file, containing a the segmented instances of every cell. 

SC-Track will output the tracking results in a track table for downstream analysis. It can optionally produce a png image folder containing the labelled cell linages, VIA2 combatible JSON file containing the tracking information and a collection of TrackingTree files to aid visualisation and analysis of the generated single cell tracks. 

### Why using SC-Track?

- The current mainstream methods for image segmentation all use deep learning, and the output results contain noises of varying intensities. SC-Track is currently the only algorithm that can use these noise data for accurate single-cell tracking and lineage reconstruction.
- SC-Track is compatible with the output results of most of the existing mainstream segmentation models, as well as manual segmentation results, including Cellpose, DeepCell, Stardist, etc. Users can choose a more advanced and suitable segmentation model according to the cell type to split.
- SC-Track can efficiently track multiple targets between frames without relying on global information, and can be used for real-time tracking.
- SC-Track is implemented in Python, which has strong scalability, convenient and quick installation, and low dependency.



### How to use SC-Track?

```
To use SC-Track, please follow the Installation steps first. It does not require too many settings during its use. When you only have a single-channel segmentation result, we require that your segmentation result must be a mask grayscale file in the form of 2D+t in tiff format. The cells in each mask need to guarantee their pixel values. is unique; or a JSON comment file. The specific format can refer to our example.

When the segmentation result is a mask, just run: sctrack -p image.tif -a mask.tif.
When the segmentation result is an annotation json file, just run: sctrack -p image.tif -a annotation.json.
Where image.tif is the original image, mask.tif, and annotation.json are annotation files. The original image may not be provided, but if the original image is not provided, the visualization result cannot be output.
```



### Installation

```
Requirement: Python >= 3.7

Windows: pip install SC-Track
Linux/Macos: pip3 install SC-Track
```







### Usage

```python
# We provide a command line tool, you only need to run the sctrack tool on the command line. To automate batch processing of a large number of files, please refer to our source code documentation.
# Its basic usage is:
    
from SCTrack import strat_track

image = 'path/to/image.tif'

# using mask annotation
annotation_mask = '/path/to/annotation.tif'
start_track(fannotation=annotation_mask, fimage=image)

# using json file annotation
annotation_json = '/path/to/annotation.json'
start_track(fannotation=annotation_json, fimage=image)
```

