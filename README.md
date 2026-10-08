# Nuclei Segmentation (Data Science Bowl 2018)

U-Net (ResNet34 encoder) for nuclei segmentation on fluorescence and
histology images, with watershed post-processing to separate touching nuclei.

## Pipeline
1. Load 670 images + merged binary masks, resize to 256x256
2. 85/15 train/val split
3. U-Net (ImageNet-pretrained ResNet34), Dice + BCE loss
4. Adam (lr 3e-4) + ReduceLROnPlateau, early stopping, best-model checkpoint
5. Watershed on a smoothed distance transform for instance separation

## Results
- Validation IoU: **0.858**
- Semantic masks: `results/predictions.png`
- Instance separation: `results/watershed.png`

## Lessons learned
- lr 1e-3 caused training spikes; 3e-4 + scheduler was stable
- Watershed: smoothing the distance map and removing tiny objects
  reduced over-splitting
- Limitation: heavily merged blobs in the U-Net mask can't be split by
  watershed; boundary-aware training is the next step

## Dataset
Kaggle Data Science Bowl 2018 (stage1_train)
