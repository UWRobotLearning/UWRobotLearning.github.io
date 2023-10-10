---
layout: default
title: Virtual Environments
parent: Development Tips
nav_order: 2
---
**Last Updated:** 2023-10-10

 **Need something quick for Ubuntu?**: 
```bash
mkdir -p ~/miniconda3
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda3/miniconda.sh
bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
rm -rf ~/miniconda3/miniconda.sh
~/miniconda3/bin/conda init bash
`````

See the [miniconda documenation](https://docs.conda.io/projects/miniconda/en/latest/)for the most up-to-date instructions and distributions for other platforms.

## Conda vs.  VirtualEnv vs. ?

Discussion to come...