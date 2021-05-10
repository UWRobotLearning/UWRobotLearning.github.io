---
layout: default
title: Creating a New Tutorial
parent: Tutorials
nav_order: 1
---
🚧 Work In Progress
{: .label .label-yellow}
🔥 Work In Progress
{: .label .label-orange}

# Creating a New Tutorial
This is a meta-tutorial on how to create a tutorial.

It is aimed at showing a lab member how they can create new tutorials without worrying about cloning this repository or using the command line. There are alternative ways to accomplish this, but this method can be done entirely within the github.com interface.

In most images, red dots signify where you should focus your attention/click.


## [00] Copying the Template
1. Navigate to `UWRobotLearning/UWRobotLearning.github.io/Tutorials/`
2. Click `_tutorial_template.md`

![00](/assets/imgs/meta_tut/00.png)


## [01] Create New Branch

1. Select switch branch by clicking on the current branch, `master`.
2. Type a new branch name. Here we prefix the branch name with `tutorials/`.
3. Click "Create branch`.

![01](/assets/imgs/meta_tut/01.png)


## [02] Branch Created

Notice, the branch selection now says `tutorials/safe..`.

![02](/assets/imgs/meta_tut/02.png)


## [03] Edit the Filename

Here we change the name from `_tutorial_template.md` to `safe_reinforcementlearning.md`.

![03](/assets/imgs/meta_tut/03.png)


## [04] Edit the Frontmatter
Change two fields in the `just_the_docs` [Frontmatter](https://jekyllrb.com/docs/front-matter/).
- Here we change the `title` from `Template for Tutorin'` to `Safe Reinforcement Learning`.
- We also change the `nav_order` from `99` to `10`. This affects the ranking in the nav bar. Lower is higher on the list.

![04](/assets/imgs/meta_tut/04.png)


## [05] Edit the Content
- Edit the template directly to contain the actual content you'd like to teach to others.
- For tips on markdown, see [References](#references).

![05](/assets/imgs/meta_tut/05.png)

## [06] Preview the Content
Click the preview tab to see the content you've entered. You can go back and forth between 'Edit file' and 'Preview' to check your formatting.

![06](/assets/imgs/meta_tut/06.png)

## [07] [Optional] Remove or Change the Label
If you plan to continue adding to this tutorial at a later date, but would like to share the content added so far, leavel the WIP label and skip this step.

You can also add a different label here like 
```
🔥 Fire Tutorial
{: .label .label-orange}
```
![07](/assets/imgs/meta_tut/07.png)


## References
- [10 min Markdown Tutorial](https://commonmark.org/help/tutorial/index.html)
- [Github Markdown Tutorial](https://guides.github.com/features/mastering-markdown/)

