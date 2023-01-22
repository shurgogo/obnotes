# Git flow
Manage a project with git

## Acknowledgements

- [Learn Git](https://www.atlassian.com/git/workflows#!workflow-gitflow)

- [A successful Git branching model](https://nvie.com/posts/a-successful-git-branching-model)

## How gitflow works

![image](https://blog.didispace.com/content/images/posts/gitflow-info-5.png)

  

### Prepare Works

Clone a repo with "master" branch
```bash
git clone xxx.git
```

Create the "develop" branch from "master" branch
```bash
git checkout master
git branch develop
git push -u origin develop
```

### Feature Development

Checkout the "feature" branch from "develop", not "master"
```bash
git checkout -b feature develop
```

Develop and commit
```bash
git add <some-file>
git commit -m <msg>
```

Merge changes to develop branch
```bash
git pull origin develop
git checkout develop
git merge feature
git push
git branch -d feature
```

### Release
```bash
git checkout -b release-0.1 develop
```
Some release work: compliance, test, doc, etc.

Merge into the master and develop branches, then delete the release branch.
```bash
git checkout master
git merge release-0.1
git push
git checkout develop
git merge release-0.1
git push
git branch -d release-0.1
```
The release branch acts as a buffer between the develop branch and the master branch. Whenever you merge something into master, you should tag it appropriately.

```bash
git tag -a <tagName> -m <msg> master
git push --tags
```
- Some Hooks(CI/CD)

### Bug fix
```bash
git checkout -b bugfix#001 master
\# some fix work
git checkout master
git merge bugfix#001
git push
git checkout develop
git merge bugfix#001
git push
```

## Version Number
a.b.c.xxx
- a

非正式版本，a=0
第一个正式版本，a=1
正式版本，存在非兼容变更或者重大特性更新，a 迭代

- b
特性增加后，b 迭代；a 增加，b 清零

- c
补丁增加后，c 迭代；b 增加，c 清零

- xxx