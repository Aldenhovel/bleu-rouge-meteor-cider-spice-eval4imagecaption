# About Image Captioning Metrics 

1. **BLEU**

   > Papineni, K., Roukos, S., Ward, T., & Zhu, W.-J. (2002). Bleu: a method for automatic evaluation of machine translation. In *Proceedings of meeting of the association for computational linguistics* (pp. 311–318). 

   BLEU has frequently been reported as correlating well with human judgement, and remains a benchmark for the assessment of any new evaluation metric. There are however a number of criticisms that have been voiced. It has been noted that, although in principle capable of evaluating translations of any language, BLEU cannot, in its present form, deal with languages lacking word boundaries. It has been argued that although BLEU has significant advantages, there is no guarantee that an increase in BLEU score is an indicator of improved translation quality.

2. **ROUGE-L**

   > Lin, C.-Y. (2004). ROUGE: A package for automatic evaluation of summaries. In *Proceedings of meeting of the association for computational linguistics* (pp. 74–81). 

   ROUGE-L: Longest Common Subsequence (LCS) based statistics. [Longest common subsequence problem](https://en.wikipedia.org/wiki/Longest_common_subsequence_problem) takes into account sentence level structure similarity naturally and identifies longest co-occurring in sequence n-grams automatically.

3. **METEOR**

   > Banerjee, S., & Lavie, A. (2005). METEOR: An automatic metric for MT evaluation with improved correlation with human judgments. In *Proceedings of meeting of the association for computational linguistics* (pp. 65–72). 

   The metric is based on the harmonic mean of unigram precision and recall, with recall weighted higher than precision. It also has several features that are not found in other metrics, such as stemming and synonymy matching, along with the standard exact word matching. The metric was designed to fix some of the problems found in the more popular BLEU metric, and also produce good correlation with human judgement at the sentence or segment level. This differs from the BLEU metric in that BLEU seeks correlation at the corpus level.

4. **CIDEr**

   > Vedantam, R., Zitnick, C. L., & Parikh, D. (2015). CIDEr: Consensus-based image description evaluation. In *Proceedings of IEEE conference on computer vision and pattern recognition* (pp. 4566–4575). 

5. **SPICE**

   > Anderson, P., Fernando, B., Johnson, M., & Gould, S. (2016). SPICE: Semantic propositional image caption evaluation. In *Proceedings European conference on computer vision* (pp. 382–398). 

# How To Use

This repo is mainly based on the code from `pycocotools` and `pycocoevalcap` , which is designed for evaluation of MS COCO caption generation. Here the API was simplified, we can transfer the use of this evaluation tool to other caption datasets, such as Flickr8k, Flickr30k or any other else.  

There are 2 `json` file saving the references and candidate captions were required.  `main.py`  we read these `json` files and evaluate the scores automatically, then print them.

the `references.json` and `captions.json` (candidate captions) were shown in `examples/` . In order to generate these files, please check the demo below:

```python
# Collect all captions generated and references with dict
references = {
    "1": ["this is a tree", "this is an apple"],
    "2": ["a man is sitting", "a man in the street"],
    ......
}

captions = {
    "1": ["this is a big tree"],
    "2": ["a man is sitting"],
    ......
}
```

```python
# Save them as correct json files
import json

new_cap = []
for k, v in captions.items():
    new_cap.append({'image_id': k, 'caption': v[0]})

new_ref = {'images': [], 'annotations': []}
for k, refs in references.items():
    new_ref['images'].append({'id': k})
    for ref in refs:
        new_ref['annotations'].append({'image_id': k, 'id': k, 'caption': ref})

with open('references.json', 'w') as fgts:
    json.dump(new_gts, fgts)
with open('captions.json', 'w') as fres:
    json.dump(new_res, fres)
```

Then we can check the new saved `references.json` and `captions.json` if it is the same format as demo `references_example.json` and `captions_example.json` .

Then use command in terminal to run `main.py` :

```bash
python main.py
```

# Notice 

Please 