This repository contains code used in the paper [Embedding Arithmetic for Text-driven Image Transformation](https://arxiv.org/abs/2112.03162) (Guillaume Couairon, Holger Schwenk, Matthijs Douze,  Matthieu Cord)

We extend this idea to multimodal embedding spaces (like CLIP), which let us semantically edit images via "delta vectors". 

Transformed images can then be retrieved in a dataset of images.

<p align="center">
    <img src="assets/method.png">
</p>

## Examples

Below are a few examples that are in the dataset, and images that were retrieved for our best-performing algorithm.

<p align="center">
    <img src="assets/examples_pos.png" style='width:66%'>
</p>

## Download dataset

The SIMAT database is composed of images from Visual Genome.

1. First need to install the Visual Genome 

```python
pip install visual-genome
```

2. And install all the required dependencies listed below

python>=3.6
pandas:
```python
pip install pandas
```
tqdm:
```python
pip install tqdm
```
torch:
```python
pip install torch
```
torchvision:
```python
pip install torchvision
```
PIL:
```python
pip install Pillow
```
pytorch-lightning:
```python
pip install pytorch-lightning
```
pycocotools:
```python
pip install pycocotools
```
CLIP:
(git+https://github.com/openai/CLIP.git)

3. After downloading the required depencies Download the part 1, part 2 images set from the [Visual Genome](https://visualgenome.org/api/v0/api_home.html) Club both part1 and part2 images into single folder.

4. Excution will start from the prepare_dataset.py file use below command to execute and specify the path where Visual Genome Images are downloaded.

```python
python prepare_dataset.py --path=/Users/Downloads/images
```
If do you use python3 please specifiy python3 instead of python in the above command.

5. Install COCO 

```python
pip install coco
```
6. Install COCO [datasets](http://images.cocodataset.org/annotations/annotations_trainval2017.zip) from this [link](http://images.cocodataset.org/annotations/annotations_trainval2017.zip) and place respective file path in the adaption.py file.


## Compute SIMAT scores with CLIP

You can run the evaluation script with the following command:

```python
python eval.py --backbone clip --domain dev --tau 0.01 --lbd 1 2
```
It automatically load the adaptation layer relative to the value of *tau*.

## Train adaptation layers on COCO

In this part, you can train linear layers after the CLIP encoder on the COCO dataset, to get a better alignment. Here is an example :

```python
python adaptation.py --backbone ViT-B/32 --lr 0.001 --tau 0.1 --batch_size 512
```

