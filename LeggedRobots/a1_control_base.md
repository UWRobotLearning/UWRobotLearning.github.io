---
layout: default
title: Getting Started with A1 Control
parent: Legged Robots Index
nav_order: 1
---
**Last Updated:** 2023-10-09  

In this article, note that `~/WORKING_DIR/` refers to any directory that will contain the cloned repo.

![prof_spot](/assets/imgs/a1_repo/repo_overview.png?raw=true)
## 0. Install Isaac-gym and test venv

See Isaac Dev page
## 1.  Clone this repo, create venv, and install dependencies

<details markdown="block">
<summary> Clone the repo (expand) </summary>
```bash
cd ~/WORKING_DIR/
git clone https://github.com/UWRobotLearning/a1_control_simple
```
</details>

<details markdown="block">
<summary> Install dependencies (expand) </summary>
```bash

conda create -n a1 python==3.8
conda activate a1
conda install pytorch torchvision torchaudio pytorch-cuda=11.8 -c pytorch -c nvidia

cd a1_control_simple
pip install -e .
```
</details>

> ⚠️️ Need to add these dependencies (or remove them totally)
noise
scikit-learn
tqdm

## 2. Run `train.py` script

<details markdown="block">
<summary> Code (expand) </summary>
```bash
cd ~/WORKING_DIR/
python a1_control_simple/leggedgym/scripts/train.py
```
This will produce outputs in `experiment_logs` which contain:

```

</details>

## 3. Run `play.py` script

## 4. Inspect `experiment_logs` outputs

## 5. Make a change to the `Env` config

## 6. Train again (do step 2)

## 7. Deploy to hardware




## Related Repo Sources
[https://github.com/leggedrobotics/legged_gym](https://github.com/leggedrobotics/legged_gym)
[https://github.com/Alescontrela/AMP_for_hardware](https://github.com/Alescontrela/AMP_for_hardware)
[https://github.com/yxyang/fast_and_efficient](https://github.com/yxyang/fast_and_efficient)


