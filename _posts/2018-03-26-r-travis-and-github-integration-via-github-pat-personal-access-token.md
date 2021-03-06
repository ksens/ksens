---
layout: post
published: true
title: 'R, Travis and Github integration via GITHUB_PAT (personal access token)'
subtitle: Automating book publishing and collaboration
---
I started using RStudio BookDown to develop documentation for SciDB insight API.

The template has a `_deploy.sh` script that depends on setting of a Github PAT (personal access token). The script also uses the token to push to `gh_pages` branch of the repo (so that documentation built by travis is uploaded automatically). See code snippet below:

From [here](https://github.com/Paradigm4/insight-docs/blob/master/_deploy.sh)
```sh
git clone -b gh-pages https://${GITHUB_PAT}@github.com/${TRAVIS_REPO_SLUG}.git book-output
```

# How do you set GITHUB_PAT?

1. First create a personal access token at [Github developer settings](https://github.com/settings/tokens)

2. When you generate the token, make sure to add `repo` or `repo/public_repo` privilege (based on whether your repo is private or public). See more scope rules [here](https://developer.github.com/apps/building-oauth-apps/scopes-for-oauth-apps/)

3. Next, the token must be set as an environment variable named `GITHUB_PAT` in Travis CI settings for your repo 

- https://travis-ci.org/<organization-or-username>/<repo-name>/settings
- or in my case, https://travis-ci.org/Paradigm4/insight-docs/settings

# Advantages

My main motivation for setting this up is that anyone can now head over to the blog website, and start editing via the **Edit** button.

![Edit button](https://user-images.githubusercontent.com/13973052/37941162-c6c9e480-313a-11e8-9fb1-e5ef2e2ba5f7.png)

with which anyone in the world can edit via Github, start pull requests, and all that good stuff. 

![start editing](https://user-images.githubusercontent.com/13973052/37941182-e1711524-313a-11e8-99f9-1ad08b8c6b90.png)