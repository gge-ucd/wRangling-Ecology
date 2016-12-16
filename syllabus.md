---
layout: page
title: Syllabus
catalog: ECL 290
credits: 2 (S/U Grading)
semester: Winter 2017
professor: Ryan Peek
office: 1117 Center for Watershed Sciences Building
email: rapeek@ucdavis.edu
phone: 530-754-5351
schedule: ['Mondays 1-3, 2124 Wickson Hall']
office_hours: Mondays 3-4 pm, or by appointment
TA: TBA
TA_email: TBA
---

## {{ site.title }}

{{ page.catalog }}, {{ page.credits }} Credits, {{ page.semester }}

### Instructor

{{ page.professor }}

Office: {{ page.office }}

Email (best way to contact me):
[{{ page.email }}](mailto:{{ page.email }})

Phone: {{ page.phone }}


### Times & Location

{% for class in page.schedule %}
  {{ class }}
{% endfor %}


### Office Hours

Times: {{ page.office_hours }}

Location: {{ page.office }}

*Note: Please try to set up a time to meet in advance if possible, there's far more of you than me.*


### Course TA

None currently

{{ page.TA }}

Email: {{ page.TA_email }}


### Website

The syllabus and other relevant class information and resources will be posted at [{{ site.url}}]({{ site.baseurl }}/).

Changes to the schedule will be posted to this site so please try to check it periodically for updates.


### Course Communications

Email: [{{ page.email }}](mailto:{{ page.email }})


### Course Description

Computers are increasingly essential to the study of all aspects of biology. Data management skills are needed for entering data without errors, storing it in a usable way, and extracting key aspects of the data for analysis. Basic programming is required for everything from accessing and managing data, to statistical analysis, to modeling. This course will provide an introduction to data management, manipulation, and analysis, with an emphasis on biological data problems. Class will typically consist of short introductions or question & answer sessions, followed by hands on computing exercises. The course will be taught using git/Github, R/RStudio, RMarkdown, and SQLite, but the concepts learned will easily apply to all programming languages and database management systems. No background in programming of databases or R/computational experience is required.


### Prerequisite Knowledge and Skills

A willingess to practice and a knowledge of basic biology.


### Purpose of Course

In this course you will learn all of the fundamental aspects of computer programming that are necessary for conducting biological research. By the end of the course you will be able to use these tools to import data into R, perform analysis on that data, write reports/CV's in RMarkdown, export results to graphs, text files, and databases, as well as collaborate on Github with version-controlled projects.

The focus of this course is to provide graduate students with training that develops and teaches the tools applicable to the entire process of reproducible data-driven research. By learning how to get the computer to do your work for you, you will be able to do more science faster, and your future self will thank you.


### Course Goals and Objectives

Students completing this course will be able to:

* Obtain, Read, Import/Export Data into R
* Tidy/summarize and analyze data
* Write simple computer programs in R
* Automate data analysis
* Apply these tools to address biological questions
* Apply general data management and analysis concepts to other programming languages and database management systems

### Teaching Philosophy

This class is taught using a flipped, learner-centered, approach, because learning to program and work with data requires actively working on computers. Flipped classes work well for all kinds of content, but I think they
work particularly well for computer oriented classes. If you're interested in knowing more take a look at this great [info-graphic](http://www.knewton.com/flipped-classroom-2/).


### Instructional Methods

As a flipped classroom, students are provided with either reading or video material that they are expected to view/read prior to class. Classes will involve brief refreshers on new concepts followed by working on exercises in class that cover that concept. While students are working on exercises the instructor will actively engage with students to help them understand material they find confusing, explain misunderstandings and help identify mistakes that are preventing students from completing the exercises, and discuss novel applications and alternative approaches to the data analysis challenges students are attempting to solve. For more challenging topics class may start with 20-30 minute demonstrations on the concepts followed by time to work on exercises.

### Assessments and Expectations

Given this approach, the onus of learning is on you as students. Each week will build on the previous week, and to learn these basic skills you must practice them. Therefore I expect the following:

- Read/watch the material prior to class
- Attend class
- Turn in your own scripts, even if you completed the problems as a group

As a graduate student myself, I understand that life is busy – mine is too. However, if you plan to join us you should expect to spend 1-2 hours to prepare for class, 2 hours in class, and possibly 1 hour to review or finish problem sets. If you cannot commit to 3–5 hours a week, please don’t sign up for this class. Having said that, I do realize that life happens in unexpected ways. Please contact me with genuine concerns about scheduling, time, or any other issues that arise.


### Grading Policies

Grading for this course will revolve around the weekly assignments, which will either be homeworks or presentations provided by students on a given lesson.

If fewer than 75% of weekly assignments are submitted on time, you will not receive a passing grade.


## Course Policies


### Attendance Policy

Attendance will not be taken or factor into the grades for this class. However, experience suggests that students who regularly miss class struggle to learn the material.


### Assignment policy

Assignments are due Monday night by 11:59 pm PST. Assignments should be submitted via Github.

### Course Technology

Students are required to provide their own laptops and to install free and open source software on those laptops (see [Setup]({{ site.baseurl }}/computer-setup) for installation instructions). Support will be provided by the instructor in the installation of required software.

### Netiquette and Communication Courtesy

All members of the class are expected to follow rules of common
courtesy in all email messages, threaded discussions and chats.


## Course Schedule

The details course schedule is available on the course website at:
[{{ site.url }}/schedule]({{ site.baseurl }}/schedule).


**Disclaimer:** This syllabus represents my current plans and objectives. As we go through the quarter, those plans may need to change to enhance the class learning opportunity. Such changes, communicated clearly, are not unusual and should be expected. Bear with me!
