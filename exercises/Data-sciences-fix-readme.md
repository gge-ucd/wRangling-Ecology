---
layout: exercise
topic: Data Science
title: Fix Readme
language: R
---

### Overview

We assume you've been keeping up with our live class activities, which have included

  * verifying your R/RStudio/Git/GitHub setup
  * joining the gge-ecl Organization and claiming your private repo
  * successfully rendering R Markdown

### Edit `README.md`

We created this repository for you but it is empty. When you first visit, you should see a screen like with nothing but a README.md file ([here's an example](https://github.com/STAT545-UBC/STAT545-UBC.github.io/blob/82b6365c5d28d7cd677dde9320bd4c0fb8d0d034/img/screenshot-new-repo-with-readme.png)). You need to edit your `README.md` file to welcome your visitors (you, instructors/ peers, whomever).

If you are already familiar with GitHub, edit the `README.md` any way you wish.

If you are new to Git and GitHub, click on the `README` link in the area that looks like a file browser. Click on the pencil and make an edit. Then head down to "Commit changes". Enter a short *commit message*. Then click "Commit changes". This is how you can edit files in GitHub repository through the browser. If you are still mystified by Git(Hub), you can use this browser-based method to edit `README.md` until you get more comfortable with using Git locally and pushing to GitHub. __However, if at all possible__, we want you to pilot a more powerful workflow:

  - Pull from GitHub (just an empty precaution now, but will matter when you collaborate with others).
  - Make changes locally to local files -- RStudio is a great Markdown editor! Click Preview to see how it's going to look!
  - Save your changes.
  - Commit your changes to your repo.
  - Push the commit to GitHub.

Go take possession of your **gge-ecl** private repository and have at it.

__At the very least__, change `README.md` to something like "This is the repository of Jenny Bryan," just to prove you have been there. Practice making a link, for example, to the [Aggie Brickyard](http://aggiebrickyard.github.io).

Much better is to introduce yourself to the class; this page is private to our class only. Feel free to read up on Markdown and practice with some of the syntax. Put in a photo or a GIF!

Here's a [sample readme file](https://github.com/STAT545-UBC/STAT545-UBC.github.io/blob/master/hw01_sample_readme.md) that you can use as reference and/or inspiration, and here is the [raw source](https://raw.githubusercontent.com/STAT545-UBC/STAT545-UBC.github.io/master/hw01_sample_readme.md). The *Help* menu in RStudio will bring up a Markdown Quick Reference at any time.


### Add R Markdown / Markdown

This is optional. If you are really struggling, skip it for now. But try!

Polish and extend the R Markdown document started in class, render it to the `github_document` output format. Commit both the `.Rmd` and `.md` files and push them to GitHub.

Give this a decent name, such as `hw01_gapminder.Rmd` (which will produce a companion file, `hw01_gapminder.md`).

### Report your process

**WE REALLY CARE ABOUT THIS! DON'T SKIP IT.**

Include a description of how you got the changes into `README.md` on GitHub.

  * Did you edit in the browser at github.com?
  * Did you pull, edit locally, save, commit, push to github.com?

How did it all work for the R Markdown document?

You're encouraged to reflect on what was hard/easy, problems you solved, helpful tutorials you read, etc. Put this in your README. In a week or two, you can delete this bit.

### Submit the assignment

Make sure you have:

 1. Pulled from your github repo already (Just good habit!)
 2. Saved all the files associated with your solution locally. Committed all those files to your local Git repository.
 3. Pushed the current state of your local repo to GitHub.
 4. Open an issue, link to the latest commit, and tag an instructor:
   - Visit your GitHub repo in a web browser. Just above the file list, look for "latest commit" followed by ten numbers and letters (called the revision SHA) and a clipboard icon.
   - Click the clipboard icon to copy the revision SHA to your clipboard.
   - Click on "Issues", then on "New Issue". Name the issue "Mark homework x of firstname-lastname", where x is the week of the quarter
   - In the issue description, tag Ryan by including the text @ryanpeek, and paste the revision SHA. Include a link to exactly where you want a reviewer to go.
 5. Click "Submit new issue". You're done! *Congratulations!*
