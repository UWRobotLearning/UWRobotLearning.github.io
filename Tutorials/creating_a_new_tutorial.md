---
layout: default
title: Creating a New Tutorial
parent: Tutorials
nav_order: 1
---
🚧 Work In Progress
{: .label .label-yellow}

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

You can also add a different label here like:
```
🔥 Fire Tutorial
{: .label .label-blue}
```
![07](/assets/imgs/meta_tut/07.png)


## [08] Commit Changes
1. Scroll down to the bottom of the page.
2. Add a quick comment about your changes.
3. Click the green `Commit changes` button.

![08](/assets/imgs/meta_tut/08.png)


## [09] Navigate to Pull Requests
Click the `Pull requests` Tab.

![09](/assets/imgs/meta_tut/09.png)


## [10] Create Pull Request
You will now create a pull request to merge from the `tutorials/safe_reinforcement_learning` branch to the `master` branch.

![10](/assets/imgs/meta_tut/10.png)


## [11] Draft PR or Ready To Go PR
Here, you have two options. File a "Draft PR" or a PR that is ready to merge right away. The purpose of a draft PR is to remain in the PR inbox with the option for other lab members to review without explicitly requesting reviews yet. Typically a Draft PR has the prefix `[WIP]` which stands for `Work in Progress`.

### Draft:
1. Give a title prefixed with `[WIP]`.
2. Click either the drop down to select `Create draft pull request`.
3. Click the green button to submit the draft pull request.

### Ready PR:
1. Give a title
2. Click the `Create pull request` button to submit it for review.

![11](/assets/imgs/meta_tut/11.png)


## [12] Request a Reviewer
1. Click the gear icon.
2. Type a lab member's name to explictly request their review.

![12](/assets/imgs/meta_tut/12.png)


## [13] Patiently Await Review
You will now see your PR waiting in the Open List under the `Pull requests` tab.

![13](/assets/imgs/meta_tut/13.png)


## [14] Get Your Review and Reply
You'll receive some feedback on your content so far and you will receive one of these:
1. Requested changes before approval
2. Comments with no explicit approval
3. Explicit approval

Feel free to ask questions or ask for clarifications. These PRs are meant to be like fast conversations.

![14](/assets/imgs/meta_tut/14.png)


## [15] [If Draft] Mark Ready for Full Review
This only applied if the PR was still in draft mode. Click the `Read for review` button to convert the draft to a full PR.

![15](/assets/imgs/meta_tut/15.png)


## [16] [If Draft] Edit the PR Title
If the PR is changing from Draft to Full, remove the `[WIP]` prefix from the title by clicking the `Edit` button.

![16](/assets/imgs/meta_tut/16.png)


## [17] Await Merge
Finally, ensure this title is something descriptive before it gets merged into `master` as this will remain in the record of `Merged` PRs after the merge process is complete. Typically a non-author lab member will approve the final merge.

If the PR-Merge workflow still seems shrouded in mystery, see the [Github Workflow Tutorial](https://guides.github.com/introduction/flow/) for more detail.

![17](/assets/imgs/meta_tut/17.png)


## References
- [10 min Markdown Tutorial](https://commonmark.org/help/tutorial/index.html)
- [Github Markdown Tutorial](https://guides.github.com/features/mastering-markdown/)
- [Gitub Workflow Tutorial](https://guides.github.com/introduction/flow/)

