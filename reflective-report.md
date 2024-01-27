---
title: "PLCS-CW1 Reflective Report"
author: "2242090"
bibliography: references.bib
toc: true
toc-title: Table of Contents
toc-depth: 3
geometry: "left=1.25cm, right=1.25cm, top=1.25cm, bottom=1.25cm"
csl: harvard-imperial-college-london.csl
---

# 1 Introduction

Software vulnerabilities are a major concern in the world today. It is therefore the programmer's responsibility to consider the cybersecurity implications in the initial stages of writing source code. For this report, however, I will reflect upon my programming learning progression path and provide examples of where cybersecurity practices have been integrated. Furthermore, I will also be discussing how I can incorporate potential cybersecurity practices into my future programming implementations.

The report is composed of three sections. First, a brief overview of my programming journey and the path it took to develop those initial skills before starting my degree, during the duration of the degree, and any new insights that I have learned recently – but with a security context in mind where applicable.

Secondly, two examples of specific Java code or functionality and the relevant choices made to address any security vulnerabilities. This section will present a much more in-depth understanding of any development decisions that can lead to said vulnerabilities.

Finally, considering what I have learned now within my degree and in my own time, incorporate a security mindset in my programming whilst going forward in the future based upon the reflections I have undertaken.

# 2 My programming journey

## 2.1 Skills before starting the degree

Before beginning my university studies, I had a lot of exposure to computer programming. At a very young age, I would experiment with basic HTML and CSS, with the task of creating a simple web dashboard that supported weather, calendar, and news APIs (see [Appendix 5.1.1](#511-html-home-dashboard)). The aim was to come up with a dashboard that can serve as a home daily dashboard to learn basic HTML tags and CSS styles whilst also implementing third-party APIs. This was also the first project in which I became introduced to version control concepts, i.e. GitHub, and the idea of commits, cloning repositories, etc.

I also have attended numerous coding boot camps that taught many programming languages. Starting with the Python one, we learned about more advanced concepts like OOP (Object-Oriented Programming) and used it to develop a space invaders-style game. OOP this instance was highly beneficial as modules like Tkinter and Pygame operated in such a way. It helped me to build upon my Python programming fundamentals, (variables, functions, loops, and so on) that I learned in school. In addition, we learned the secure concepts of OOP and how it contrasts from just typical programming – how objects are encapsulated, polymorphism of objects, and explicit use of getter and setter methods.

Java boot camps I have attended, one teaching Java concepts and the other, similar to Python in a game development environment, helped me have more of an appreciation for the consistency in coding concepts learned in other languages – the only difference in syntax structure. In these boot camps, we learned about the differences between Java and Python in terms of interaction with compilers, portability, and more. Each programming language has its respective strengths and weaknesses depending on the given scenario.

More recently before university, specifically in sixth form (see [Appendix 5.1.2](#512-a-level-projects)), we learned about higher-level concepts of computer science, such as data structures and their search algorithms, as well as an understanding of the different software development methodologies. Using this, for the coding project component of my A-Level, I developed an Android application that allows users to listen to music collaboratively. This was mainly in the Kotlin programming language for the backend but XML for the frontend. This project taught me many skills, furthering my knowledge in Git version control (shelving and reverting changes/commits), integrating more official enhanced APIs, collecting stakeholder feedback, using an Agile development methodology (i.e. sprints and tickets), and database concepts. Of course, however, due to the implementation complexity, this opened many security issues. As the scope of the project was massive, this could not be considered in the time remaining however I took the time to research appropriately about the Android security model and comment about how the application could be secured if time constraints weren't there.

## 2.2 Skills learned during the degree

The skills learned beforehand, although I knew that security concepts existed and perhaps could have been implemented within the programs I have completed before, I did now know the knowledge of how to implement them. This was quickly addressed prominently when a pair programming task was assigned, in which we had to secure a JavaScript React application from SQL injection attacks. The project's security implications came into play further when we were tasked with uploading it to the cloud, so containerisation (via Docker) and applying the appropriate encryption parameters had to be taken into account. Once packaged into a Docker virtual machine with all the required project dependencies, it had to be uploaded to a cloud on an Amazon EC2 instance using AWS CloudFormation – making it publicly accessible. All of this was automated, and this was a great introduction to DevOps (Development Operations) i.e. CI/CD (Continuous Integration/Continuous Delivery) pipelines.

Another big software project completed recently was a C# web application (see [Appendix 5.1.3](#513-c-web-application)) to develop a hotel and tour reservation system for a given scenario. Since the scope of the project was intricate, organisational skills were required to balance out the implementation of features with the given time constraints. This project, in conjunction with the previous ones, helped us gain further acknowledgment into software development methodologies, again this time, using Agile sprints. The project required various languages, such as JavaScript, C# of course (since it is ASP.NET), and SQL database commands. Here, a lot of security aspects had to be implemented, but many of them were quickly addressed by the default dependencies that Microsoft provides (Entity Framework Core). In essence, this just needed minimal configuration and enabling, rather than manual development to patch vulnerabilities.

Using the knowledge from Python, and since Python is a pivotal language in many cybersecurity tools, I have also taken personal time to develop small recreations of existing cybersecurity tools (see [Appendix 5.1.4](#514-python-cybersecurity-tools)), such as a key logger, packet capturer, and password manager. Using existing Python libraries for these projects, not only reinforces basic coding concepts learned in the past but explores the concept of libraries and how they modularise code reusability to build applications that are much more complex in functionality.

Finally, the last major project that helped me learn more development skills and technologies was the creation of a backend database in PostgreSQL (see [Appendix 5.1.5](#515-sql-backend-database)). Databases are a huge component of application storage, so this assignment helped me to learn more about database theory in general, entities, the types of relationships between them, and their relevant translation into SQL commands. Securing the application was the main part of this assignment, and for this, database roles were created along with the necessary permissions assigned to them. A configuration file was supplied with all security hardening options enabled, such as password encryption and SSL keys.

## 2.3 Skills learned in this module

# 3 Applying cyber security in my programming

# 4 Incorporating cyber security in future programming

# 5 Appendices

## 5.1 GitHub repositories

### 5.1.1 HTML home dashboard

- [home-automation](https://github.com/iArcanic/home-automation)

### 5.1.2 A-level projects

- [ocr-tunes](https://github.com/iArcanic/OCR-Tunes)
- [random-question-generator](https://github.com/iArcanic/random-question-generator)

### 5.1.3 C# web application

- [pacific-tours-ccse-cw1](https://github.com/iArcanic/pacific-tours-ccse-cw1)

### 5.1.4 Python cybersecurity tools

- [py-keylogger](https://github.com/iArcanic/py-keylogger)
- [py-password-manager](https://github.com/iArcanic/py-password-manager)
- [py-packet-capturer](https://github.com/iArcanic/py-packet-capturer)

### 5.1.5 SQL backend database

- [im-cw1](https://github.com/iArcanic/im-cw1)

# 6 References
