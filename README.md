# Textmentations
Textmentations is a Python library for augmenting Korean text. 
Inspired by [albumentations](https://github.com/albumentations-team/albumentations). 
Textmentations uses the albumentations as a dependency.

## Installation

```
pip install textmentations
```

## A simple example

Textmentations provides text augmentation techniques implemented using the [TextTransform](https://github.com/Jaesu26/textmentations/blob/v0.0.2/textmentations/core/transforms_interface.py#L17), 
which inherits from the albumentations [BasicTransform](https://github.com/albumentations-team/albumentations/blob/1.2.1/albumentations/core/transforms_interface.py#L54). 

This allows textmentations to reuse the existing functionalities of albumentations.

```python
from albumentations import Compose
from textmentations import RandomDeletion, RandomInsertion, RandomSwap, SynonymReplacement

text = "어제 식당에 갔다. 목이 너무 말랐다. 먼저 물 한잔을 마셨다. 그리고 탕수육을 맛있게 먹었다."
rd = RandomDeletion(deletion_prob=0.3, min_words_each_sentence=1)
ri = RandomInsertion(insertion_prob=0.3, n_times=1)
rs = RandomSwap(n_times=3)
sr = SynonymReplacement(replacement_prob=0.3)
eda = Compose([rd, ri, rs, sr])

print(rd(text=text)["text"])
# 식당에 갔다. 목이 너무 말랐다. 먼저 물. 그리고 탕수육을 맛있게.

print(ri(text=text)["text"])
# 어제 최근 식당에 갔다. 목이 너무 말랐다. 먼저 물 한잔을 마셨다 음료수. 그리고 탕수육을 맛있게 먹었다.

print(rs(text=text)["text"])
# 어제 갔다 식당에. 목이 너무 말랐다. 물 먼저 한잔을 마셨다. 그리고 먹었다 맛있게 탕수육을.

print(sr(text=text)["text"])
# 과거 식당에 갔다. 목이 너무 말랐다. 먼저 소주 한잔을 마셨다. 그리고 탕수육을 맛있게 먹었다.

print(eda(text=text)["text"])
# 식당에 어제 과거. 너무 말랐다. 상수 한잔을 마셨다 맹물. 먹었다 그리고 맛있게.
```

## List of augmentations

- `RandomDeletion`
- `RandomDeletionSentence`
- `RandomInsertion`
- `RandomSwap`
- `RandomSwapSentence`
- `SynonymReplacement`

## References

- [albumentations](https://github.com/albumentations-team/albumentations)

- [EDA: Easy Data Augmentation Techniques for Boosting Performance on
Text Classification Tasks](https://arxiv.org/pdf/1901.11196.pdf)

- [Korean WordNet (KWN)](http://wordnet.kaist.ac.kr/)

- [Korean Stopwords](https://www.ranks.nl/stopwords/korean)