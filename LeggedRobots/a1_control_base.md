---
layout: default
title: Onboarding for A1 Control
parent: Legged Robots Index
nav_order: 1
---
**Last Updated:** 2023-10-17  

![overview](/assets/imgs/a1_repo/repo_overview.png?raw=true)

> ⚠️ In this article, note that `~/WORKING_DIR/` refers to any directory that will contain the cloned repo.

## 0. Install Isaac-gym and test venv

If you do not have Isaacgym installed please see the [Dev/Isaac](../Development/Isaac#isaac-gym) page.

## 1.  Clone this repo, create venv, and install dependencies


<details markdown="block">
<summary> 1.1 Clone the repo (expand) </summary>
```bash
cd ~/WORKING_DIR/
git clone https://github.com/UWRobotLearning/ground_control_base
```
</details>


<details markdown="block">
<summary> 1.2 Create virtual env and install dependencies (expand) </summary>
```bash
conda create -n a1 python==3.8
conda activate a1
conda install pytorch torchvision torchaudio pytorch-cuda=11.8 -c pytorch -c nvidia

cd ground_control_base
pip install -e .
```
</details>

> ⚠️️ Need to add these dependencies (or remove them totally)
- noise
- scikit-learn
- tqdm

> Briefly list why the dependencies exist


## 2. Run `train.py` script

This is the entry point to the base training loop with sane defaults. It utilizes [hydra](https://hydra.cc/docs/intro/) for:
1. More powerful config interpolation / composition
2. Parallelized experiment dispatch
3. Plug-in to hyperparam search like [Optuna](https://optuna.org/#key_features), [Ax](https://ax.dev/docs/why-ax.html), [Nevergrad](https://facebookresearch.github.io/nevergrad/)...

Note that this code can be run without hydra, and it is helpful to note that clean code creates a clear barrier between "config-logic" and envs / learning machinery. This maintains a clear decoupling which allows your contributions to be _evergreen_ rather than _ad-hoc_.

> See [Config Management](./config_management) for a more detailed discussion of this concept.

<details markdown="block">
<summary> 2.0 Examine the train_nohydra.py (expand) </summary>
```bash
vim train_nohydra.py
```
This will produce outputs in `experiment_logs` which contain:
> Insert image of 

</details>

<details markdown="block">
<summary> 2.1 Run train.py (expand) </summary>
```bash
cd ~/WORKING_DIR
python ground_control/leggedgym/scripts/train.py
```
This will produce outputs in `experiment_logs` which contain:
```bash
user@computer:~/WORKING_DIR/experiment_logs$ tree
.
├── 2023-10-13_14-35-39
│   ├── events.out.tfevents.1697232945.u114025.45506.0
│   ├── exported_policy.pt
│   ├── model_0.pt
│   ├── ⋮
│   ├── model_1000.pt
│   ├── ⋮
│   ├── model_5000.pt
│   ├── resolved_config.pkl
│   ├── resolved_config.yaml
│   └── train.log
```

</details>

## 3. Run `play.py` script

This is the entry point for replaying training runs. It defaults to replaying the most recent model trained in the most recent (chronogically) folder located in `experiment logs` by default. This script reproduces the exact conditions of the specified experiment by deserializing the `resolved_config` and loading it into the configs defined at the top of the script into the `MISSING` fields. Note that play is only meant to replay in Isaac. For deploying to real or sim-to-sim (e.g. pybullet or mujoco), use `deploy.py`.

<details markdown="block">
<summary> 2.1 Run play.py (expand) </summary>
```bash
cd ~/WORKING_DIR
python ground_control/leggedgym/scripts/play.py
```
</details>

## 4. Inspect `experiment_logs` outputs
- View Tensorboard rewards
- Make way to "remove the noise"

## 5. Make a change to the `Env` config

## 6. Train again (do step 2)

## 7. Deploy to hardware


## Related Repo Sources
- [https://github.com/leggedrobotics/legged_gym](https://github.com/leggedrobotics/legged_gym)
- [https://github.com/Alescontrela/AMP_for_hardware](https://github.com/Alescontrela/AMP_for_hardware)
- [https://github.com/yxyang/fast_and_efficient](https://github.com/yxyang/fast_and_efficient)


