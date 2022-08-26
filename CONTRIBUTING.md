# [Please contribute](#please-contribute)

You can really make a difference by:

- [Always Start with an Issue](https://about.gitlab.com/blog/2016/03/03/start-with-an-issue)
- [Making an issue](https://docs.gitlab.com/ee/user/project/issues/managing_issues.html#from-a-project/). A well described issue helps a lot. (Have a look at the [known issues](https://gitlab.com/groups/aussielunix/ansible/-/issues/?sort=created_date&state=opened).)
- [Making a merge request](https://docs.gitlab.com/ee/user/project/merge_requests/creating_merge_requests.html#when-you-work-in-a-fork) when you see an error or want to add a new feature.

We'll try to help and take every contribution seriously.  
It's a great opportunity for us to learn how you use the role and also an opportunity to get into the habit of contributing to open source software.

## [Step by step](#step-by-step)

Here is how you can help, a lot of steps are related to GitLab, not specifically our roles.

### [1. Make an issue.](#1-make-an-issue)

When you spot an issue, [create an issue](https://gitlab.com/aussielunix/ansible/ansible-role-netbox/~/issues).  
Creating an issue helps us and others to find similar problems in the future.

### [2. Fork the project.](#2-fork-the-project)

[Fork this](https://gitlab.com/aussielunix/ansible/ansible-role-netbox/-/forks/new) or
On the top right side of [the repository on GitLab](https://gitlab.com/aussielunix/ansible/ansible-role-netbox), click `fork`. This copies everything to your own GitLab namespace.  

### [3. Make the changes](#3-make-the-changes)

In you own GitLab namespace, make the required changes in a branch.  
I typically do that by cloning the forked repository (in your namespace) locally to my workstation:

```bash
git clone git@gitlab.com:<YOURNAMSPACE>ansible-role-netbox.git
cd ansible-role-netbox
git checkout -b Feature-add-something
```

Now you can start to edit on your workstation.

### [4. Make a merge request](#4-make-a-merge-request)

[Making a merge request from a fork](https://docs.gitlab.com/ee/user/project/merge_requests/creating_merge_requests.html#when-you-work-in-a-fork).
In the comment-box, you can [refer to the issue number](https://docs.gitlab.com/ee/user/project/issues/managing_issues.html#closing-issues-automatically) to automatically close any issues related to the merge request.

### [5. Wait](#5-wait)

Now we'll get a message that you've added some code. Thank you, really.  
CI starts to test your changes. You can follow the progress on [GitLab Pipelines](https://gitlab.com/aussielunix/ansible/ansible-role-netbox/-/pipelines).  

