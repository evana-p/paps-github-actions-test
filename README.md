# Github Actions Test
## Name of repo: paps-github-actions-test
Description: This is a repo for testing how Github actions works in an Android project and compare it to other services like Bitrise

## Step 1: Documentation
Go read the docs at: https://docs.github.com/en/actions

### Read the About Github actions
Docs at: [About GitHub Actions - GitHub Docs](https://docs.github.com/en/actions/getting-started-with-github-actions/about-github-actions)
*Key points*: 
1. GitHub Actions enables you to create custom software development life cycle (*SDLC*) workflows directly in your GitHub repository.
2. You can write individual tasks, called actions, and combine them to create a custom workflow.
3. Workflows are custom automated processes that you can set up in your repository to build, test, package, release, or deploy any code project on GitHub.
4. What’s the difference between release and deploy?
5. There are some limitations depending on the GitHub plan: [About GitHub Actions - GitHub Docs](https://docs.github.com/en/actions/getting-started-with-github-actions/about-github-actions#usage-limits)

### Read about the terminology of GitHub actions
Docs at: [Core concepts for GitHub Actions - GitHub Docs](https://docs.github.com/en/actions/getting-started-with-github-actions/core-concepts-for-github-actions)

No need to copy each concept, but they are good to reference often.

*Key points*:
1. A group of steps to perform a certain thing constitute an *action*.
2. *Artifacts* are not just apks, but also things that come out of testing like logs or screenshots, any by-product.
3. GitHub performs all upgrades and maintenance of GitHub-hosted runners (so if you want to run your tests in an older version of Android you may be tied up to the latest and greatest?)
4. Steps > Actions > Jobs > Workflow
5. *Runner* is the app that runs ‘GitHub Action Workflows’

### Read about security
Docs at: [Security hardening for GitHub Actions - GitHub Docs](https://docs.github.com/en/actions/getting-started-with-github-actions/security-hardening-for-github-actions)

This includes the basics of secrets, the use of third-party actions and cross-repository access.

### Pre-configured workflow templates
Docs at: [Starting with preconfigured workflow templates - GitHub Docs](https://docs.github.com/en/actions/getting-started-with-github-actions/starting-with-preconfigured-workflow-templates)

Here we find a *starter workflow for Android* [starter-workflows/android.yml at master · actions/starter-workflows · GitHub](https://github.com/actions/starter-workflows/blob/master/ci/android.yml) would be ideal to show it to the user and show how to expand on it.

This starter runs a Gradle build on a push to the repo or on pull requests.

``` javascript
name: Android CI

on:
  push:
    branches: [ $default-branch ]
  pull_request:
    branches: [ $default-branch ]

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2
    - name: set up JDK 1.8
      uses: actions/setup-java@v1
      with:
        java-version: 1.8
    - name: Build with Gradle
      run: ./gradlew build
```


Next the hands-on starts, there is an example on how to add a workflow to a repo! (link above)

1. I went to the top of the repo and clicked on ‘Actions’

![](https://github.com/evana-p/paps-github-actions-test/blob/master/images/10F22D4C-824F-4E55-ADC0-FB53F45459F4.png)

2. The one suggested by default was the *Simple workflow*, which is not the one I would have expected, I would have expected an Android suggestion.

![](https://github.com/evana-p/paps-github-actions-test/blob/master/images/FAF214A3-B07F-4E8E-AF70-3C5DDD5B197E.png)

3. So I clicked in *Set up a workflow yourself*

![](https://github.com/evana-p/paps-github-actions-test/blob/master/images/230EEBB5-FFA3-4988-A005-80F855E0EC0C.png)

4. And got a .yml to edit by myself.

![](https://github.com/evana-p/paps-github-actions-test/blob/master/images/18A0CADD-D40B-4813-83D1-5DA0362C129C.png)

Note: to the right you get easy to add actions, so in case you don’t know how to properly write the YML, you can still get ‘templates’ as a beginner (liked this a lot).

5. This was the default one. So I copied the Android starter I had in the code snippet above.

6. Saved the files as main.yml, as it had by default and I clicked on *Start commit* green button at the right.

7. I couldn’t merge it directly with my test branch, had only the option to merge directly to master or to create a branch specifically for this and start a PR.

![](https://github.com/evana-p/paps-github-actions-test/blob/master/images/49CF162C-E32E-4FCC-9B87-92EA8F0567DF.png)

8. I was taken directly to creating a PR

![](https://github.com/evana-p/paps-github-actions-test/blob/master/images/933664F3-6AD8-4918-83E5-675F9D7880D9.png)

9. Merged it and now I have the workflow.

11. You can find the file in project > .github > workflows > main.yml

![](https://github.com/evana-p/paps-github-actions-test/blob/master/images/DF472CCA-3A3E-45E8-95C5-7501490FAB8B.png)

### Actions from the Github Marketplace

Docs at: [Using actions from GitHub Marketplace - GitHub Docs](https://docs.github.com/en/actions/getting-started-with-github-actions/using-actions-from-github-marketplace)

If you go into the marketplace and search for Android, you see there is only one verified action (the one with a blue checkmark next to it)

![](https://github.com/evana-p/paps-github-actions-test/blob/master/images/DCCA4055-A961-43C0-8F94-9F2D6A8862F3.png)

### Tested Actions

I did a push directly in master and discovered the first file wasn’t working, so I created another workflow, this time called android.yml, removing the comments and weirdly that worked.

![](https://github.com/evana-p/paps-github-actions-test/blob/master/images/C692A53C-882E-422D-9990-38A031815879.png)

When I pushed it directly to master it did trigger the workflows in GitHub 


![](https://github.com/evana-p/paps-github-actions-test/blob/master/images/F298601B-FF36-4D1D-AE28-3FC8D674601C.png)

And you get pretty much what you would get in any other CI / CD tool
