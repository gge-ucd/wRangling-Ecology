---
layout: page
element: notes
title: Gitting Started
---


## Why Git?

Please read through this [**slide deck**](https://speakerdeck.com/alicebartlett/git-for-humans), and an overview of the [Big Picture](http://happygitwithr.com/big-picture.html)

<sub>(The following lesson is adapted from Jenny Bryan's [course](http://stat545.com/git08_claim-stat545-repo.html))
</sub>

### Prerequisites

**We assume the following:**

 - You’ve already installed Git and (possibly) a Git client.
 - You’ve already registered a free GitHub account.
 - You’ve already introduced yourself to Git.
 - You’ve confirmed that you can push to / pull from GitHub from the command line.
 - You’ve already installed R and RStudio.
 - You’ve proven that you can push to / pull from GitHub from RStudio.
 - You are no longer being challenged for your GitHub username and password because your credentials have been cached or you’ve set up SSH keys.

 *Instructions for all of this are here:*

 > **http://happygitwithr.com**

## Setting up your Repository
You should all have gotten an invitation to join the **_gge-ucd_** Organization. Check your email.

I've added you to a private repository that belongs *only* to you. Other students can see this repo, but they cannot edit it. The rest of the world cannot even see it. I can see and can write to it, but I probably won’t.

### Steps to *Git*ting It:

 1. Go to that repository in the browser.
 2. Copy the HTTPS URL. It will be something like this: **https://github.com/gge-ucd/indiana_jones
 3. In RStudio, start a new Project:
    - **File** > **New Project** > **Version Control** > **Git**. In the “*repository URL*” paste the URL of your new GitHub repository.
    - **Take charge of – or at least notice! – the local directory for the Project.** This will be the main folder for your coursework, and will include all of these things:
      - a directory on your computer
      - a Git repository, linked to a remote GitHub repository
      - an RStudio Project (.RProj)
  4. Create the Project … you should get a pre-existing skeleton README.md that's been pre-created for you.

### Now You Can Do Stuff!

 - Make some local changes, e.g. edit or add files.
 - Commit these changes to your local repo.
 - Pull from GitHub (I’m just trying to help you establish this habit...remind me to explain why).
 - Push to GitHub.
 - Repeat ad nauseum as you do your coursework.

### See your Commit Messages

 - See your commit messages Star Wars style:
   - http://starlogs.net/
