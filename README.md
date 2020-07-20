# hippodeep
Brain Hippocampus Segmentation

This program can quickly segment (<1min) the Hippocampus of raw brain T1 images.

![blink_rotated](https://user-images.githubusercontent.com/590921/75311442-1a705a00-589a-11ea-9cb6-d889fb226516.gif)

It relies on a Convolutional Neural Network pre-trained on thousands of images from multiple large cohorts, and is therefore quite robust to subject- and MR-contrast variation.
For more details on its creation, refer the corresponding manuscript at http://dx.doi.org/10.1016/j.media.2017.11.004

This version is a PyTorch port of the original Theano model. This version has less dependencies and is notably faster thanks to pytorch multithreading. While the hippocampal segmentation model is exactly the same as described in the paper, the pre- and post-processing steps had been improved, and thus, results may slightly differ. The original repo is still available at https://github.com/bthyreau/hippodeep


## Requirement

This program requires Python 3, with the PyTorch library, version > 1.0.0.

No GPU is required

Tested on Linux CentOS 6.x/7.x, Ubuntu 18.04 and MacOS X 10.13, using PyTorch versions 1.0.0 to 1.4.0

## Installation

Just clone or download this repository.

In addition to PyTorch, the code requires scipy and nibabel.

The simplest way to install from scratch is maybe to use a Anaconda environment, then
* install scipy (`conda install scipy` or `pip install scipy`) and  nibabel (`pip install nibabel`)
* get pytorch for python from `https://pytorch.org/get-started/locally/`. CUDA is not necessary.

## Windows Installation

* pip install numpy scipy nibabel
* pip install torch==1.3.0+cpu -f https:&#8203;//download.pytorch.org/whl/torch_stable.html
* pip install psutil pywin32 pillow fpdf2

to compile an executable:

* pip install pyinstaller
* pyinstaller HippoDeep.spec
* your compiled executable should be under .\dist\HippoDeep.exe

A precompiled Windows executable can be found under the Release section 
<a href="https://github.com/bfoe/hippodeep_pytorch/releases/download/v0.3/HippoDeep_Windows_v0.3.zip">here</a>

## Usage:
To use the program, simply call:

`deepseg1.sh example_brain_t1.nii.gz`.

if called without argument a file dialougue should appear
<br/>
(this is, if you have tkinter installed with: "yum install tkinter" or "apt-get install python3-tk")

To process multiple subjects, pass them as multiple arguments.
`deepseg1.sh subject_*.nii.gz`.

The resulting segmentations should be stored as `example_brain_t1_mask_L.nii.gz` (or R for right) and `example_brain_t1_brain_mask.nii.gz`.  The mask volumes (in mm^3) are stored in a csv file named `example_brain_t1_hippoLR_volumes.csv`.  If more than one input was specified, a summary table named `all_subjects_hippo_report.csv` is created.

also eports to PDF file(s):<br/>
![ReportExample](https://github.com/bfoe/hippodeep_pytorch/blob/master/ReportExample.jpg)
