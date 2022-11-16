# ACE

Here is the Pytorch implementations of the paper [Towards Automatic Concept-based Explanations](https://arxiv.org/abs/1902.03129) presented at NeurIPS 2019.

**Please cite the following work if you use this benchmark or the provided tools or implementations:**
```
@inproceedings{ghorbani2019towards,
  title={Towards automatic concept-based explanations},
  author={Ghorbani, Amirata and Wexler, James and Zou, James Y and Kim, Been},
  booktitle={Advances in Neural Information Processing Systems},
  pages={9273--9282},
  year={2019}
}
```

```
Ghorbani, Amirata, James Wexler, James Y. Zou, and Been Kim. 
"Towards Automatic Concept-based Explanations." 
Advances in Neural Information Processing Systems. 2019.
````

## Getting Started
### Prerequisites

Required python libraries:

```
  Pytorch, Torchvision, Scikit-image, Matplotlib
```

### Installing

An example run command:

```
python ace_run.py --num_parallel_runs 0 --target_class zebra --source_dir SOURCE_DIR --working_dir SAVE_DIR --model_to_run resnet18 --labels_path imagenet_class_index.json --feature_names layer3 --num_random_exp 20 --max_imgs 50 --min_imgs 30
```

where:
```
num_random_exp: number of random concepts with respect to which concept-activaion-vectors are computed for calculating the TCAV score of a discovered concept (recommended >20).
```
For example if you set num_random_exp=20, you need to create folders random500_0, rando500_1, ..., random_500_19 and put them in the SOURCE_DIR where each folder contains a set of 50-500 randomly selected images of the dataset (ImageNet in our case). 

```
target_class: Name of the class which prediction is to be explained.
```

```
SOURCE_DIR: Directory where the discovery images (refer to the paper) are saved. 
It should contain (at least) num_random_exp + 2 folders: 
1-"target_class" which contains images of the class to be explained (in this example the shoulder should be names as zebra). 
2-"random_discovery" which contains randomly selected images of the same dataset (at lease $max_imgs number of images).
3-"random500_0, ..., random_500_${num_random_exp} where each one contains 500 randomly selected images from the data set"
```

```
num_parallel_runs: Number of parallel jobs (loading images, etc). If 0, parallel processing is deactivated.
```


```
SAVE_DIR: Where the experiment results (both text report and the discovered concept examples) are saved.
```

```
model_to_run: Any torch.hub model. Note that you may need to edit the _get_gradients function in ace.py, this code is tested with googlenet and resnets
```

## Authors of Original Paper

* **Amirata Ghorbani** - [Website](http://web.stanford.edu/~amiratag)
* **James Wexler** - [Website](https://ai.google/research/people/105507/)
* **James Zou** - [Website](https://www.james-zou.com/)
* **Been Kim** - [Website](https://beenkim.github.io/)


## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

Work was done as part of Google Brain internship.

