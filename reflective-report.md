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

Software vulnerabilities are a major concern in the world today. It is therefore the programmer's responsibility to consider the cybersecurity implications when writing code.

The report has three sections. First, a brief overview of my programming journey and the path it took to develop those initial skills before starting my degree, during the duration of the degree, and any new insights that I have learned recently – but with a security context in mind where applicable.

Secondly, examples of specific Java code or functionality and the relevant choices made to address any security vulnerabilities. This section will present a much more in-depth understanding of any development decisions that can lead to said vulnerabilities.

Finally, considering what I have learned now within my degree and in my own time, incorporate a security mindset in my programming going forward based on my reflections.

# 2 My programming journey

## 2.1 Skills before starting the degree

Before beginning my university studies, I had a lot of exposure to computer programming. I experimented with basic HTML and CSS, with the task of creating a simple web dashboard that supported weather, calendar, and news APIs (see [Appendix 5.1.1](#511-html-home-dashboard)). This was also the first project in which I became introduced to version control concepts, i.e. GitHub, and the idea of commits, cloning repositories, etc.

I also attended coding boot camps that taught many programming languages, starting with Python. We learned about advanced concepts like OOP (Object-Oriented Programming) and used it to develop a space invaders-style game. OOP in this instance was highly beneficial, as modules like Tkinter and Pygame operated in such a way. It helped me to build upon my Python programming fundamentals, (variables, functions, loops, and so on) that I learned in school. In addition, we learned the secure concepts of OOP – how objects are encapsulated, the polymorphism of objects, and the explicit use of getter and setter methods.

Java boot camps I have attended, helped me have more of an appreciation for the consistency in coding concepts – the only difference being in the syntax structure. In these boot camps, we learned about the differences between Java and Python in terms of interaction with compilers, portability, and more. Each programming language has its respective strengths and weaknesses depending on the given scenario.

Before university (see [Appendix 5.1.2](#512-a-level-projects)), we learned about higher-level programming concepts, such as data structures, and their search algorithms, as well as an understanding of the different software development methodologies. Using this, for the coding project component of my A-Level, I developed an Android application allowing users to listen to music collaboratively. Kotlin was used for the backend but XML for UI. This project taught me many skills, furthering my knowledge in Git version control (shelving and reverting changes/commits), integrating APIs, collecting stakeholder feedback, and using an Agile development methodology (i.e. sprints and tickets).

## 2.2 Skills learned during the degree

The skills learned beforehand, although I knew that security concepts existed and perhaps could have been implemented within the previous project, I now had to implement them. This was quickly addressed when a pair programming task was assigned, in which we had to secure a JavaScript React application from SQL injection attacks. The project's security implications came into play further when we were tasked with uploading it to the cloud, so containerisation (via Docker) and applying the appropriate encryption parameters had to be taken into account. It then had to be uploaded to a cloud on an Amazon EC2 instance using AWS CloudFormation. All of this was automated, and this was a great introduction to DevOps (Development Operations) i.e. CI/CD (Continuous Integration/Continuous Delivery) pipelines.

Another big software project completed recently was a C# web application (see [Appendix 5.1.3](#513-c-web-application)) to develop a hotel and tour reservation system for a given scenario. Since the scope of the project was intricate, organisational skills were required to balance out the implementation of features with the given time constraints. This project, in conjunction with the previous ones, helped us gain further acknowledgment of software development methodologies, again this time, using Agile sprints. The project required various languages, such as JavaScript, C# of course (since it is ASP.NET), and SQL database commands. Here, a lot of security aspects had to be implemented, but many of them were quickly addressed by the default dependencies that Microsoft provides (Entity Framework Core). In essence, this just needed minimal configuration and enabling, rather than manual development.

Using Python I have also developed recreations of existing cybersecurity tools, such as a key logger, packet capturer, and password manager (see [Appendix 5.1.4](#514-python-cybersecurity-tools)). Using existing Python libraries for these projects explores the concept of libraries and how they modularise code reusability to build applications that are complex in functionality.

Finally, the last major project that helped me learn more development skills and technologies was the creation of a backend database in PostgreSQL (see [Appendix 5.1.5](#515-sql-backend-database)). Databases are a huge component of application storage, so I learned more about database theory such as entities and the types of relationships between them. Securing the application was also crucial, so database roles were created along with the necessary permissions for them.

## 2.3 Skills learned in this module

This module has improved my programming abilities, by mainly focusing on the Java language and common security. Moreover, getting used to Java in a security context was highly beneficial and serves as a transferrable skill that can be applied when writing code in other programming languages. A newfound understanding of CWEs (Common Weakness Enumeration) such as code injections, buffer overflows, and lack of error console logging helped me identify threat patterns of which I was previously unaware. This security mindset has led me to take caution in handling user inputs, third-party library functions, and robust code measures to allow for more code resilience.

# 3 Applying cyber security in my programming

## 3.1 Example 1 – input validation

This code snippet is from my Android application's login page. It checks the value before passing it to the subsequent authentication method.

```java
String username = request.getParameter("username");
String password = request.getParameter("password");

if(username == null || username.isEmpty()){
  throw new ValidationException("Username cannot be empty");
}

if(password == null || password.length() < 8){
  throw new ValidationException("Invalid password");
}

authSystem.login(username, password);
```

It first makes sure the `password` parameter is of the required length requirement, meaning that any malicious data does not get sent to authentication. It then checks for `null` or empty to prevent any null exception errors with the backend authentication system. Furthermore, it enforces client-side password checks before reaching the necessary authentication logic. This programming practice always has the underlying assumption that user inputs are always out to break the system.

## 3.2 Example 2 – parameterised SQL statements

The Android application I developed required a backend connection to the database. The database I was using was SQL, meaning that it always carries a risk of SQL injection attacks.

```java
String name = request.getParameter("username");
int age = Integer.parseInt(request.getParameter("age"));

PreparedStatement stmt = con.prepareStatement("INSERT INTO users VALUES(?, ?)");
stmt.setString(1, name);
stmt.setInt(2, age);
stmt.executeUpdate();
```

Initially, it requests the user's `name` and `age` parameters, parsing them to the appropriate data types. It then executes a database query via a `PreparedStatement` to add the user's supplied data securely. This means that the string cannot be manipulated or exploited by ensuring the exact string structure. Using this over normal string concatenation allows user inputs to be treated as separate parameters instead of singular inline SQL statements. It helps to maintain control and prevents the insertion of unintended SQL data.

## 3.3 Example 3 – encrypting sensitive data

When storing sensitive data, such as the user's password, robust encryption is required. Here is a short code snippet from my POC project.

```java
Key encryptionKey = KeyGenerator.getInstance("AES").generateKey();
Cipher c = Cipher.getInstance("AES/CBC/PKCS5Padding");
c.init(Cipher.ENCRYPT_MODE, encryptionKey);

String password = "1234myP@sswd";
byte[] encrypted = c.doFinal(password.getBytes());

FileWriter fw = new FileWriter("password.txt");
fw.write(Base64.getEncoder().encodeToString(encrypted));
fw.close();
```

In this case, AES encryption and base64 encoding are used to securely save the password string. AES also applies symmetric key encryption, where the keys are dynamically generated each time rather than hard-coded values. It also encrypts at the last possible moment just before the password is stored in the `.txt` file.

## 3.4 Example 4 – using trusted Java libraries

Here is some logic from a small POC that I developed, it relies on a standard security framework.

```java
import org.owasp.encoder.Encode;

String input = request.getParameter("query");
String query = Encode.forJava(input);
stmt.setString(1, query);
```

In this code snippet, the OWASP Encoder is used to filter application inputs and allows SQL injection attacks to be prevented. Rather than using custom logic that is prone to failure, leveraging existing frameworks is more reliable. In this way, developers can focus more on the application's business logic, rather than having to spend time recreating security – reducing mistakes and improving development efficiency.

# 4 Incorporating cyber security in future programming

## 4.1 As a programmer

In the future, in a career in software engineering, the knowledge and skills gained from this module are transferrable and therefore applicable to the approach I will take in developing applications and systems.

Therefore, here are some considerations I will be taking into future development:

- Any UI features will consider user psychology and adversarial threats.
- Written code will take into account input validations, encryption algorithms, and SQL parameterised queries.
- Developers or specialists with specific security mindsets will be integrated early so that vulnerabilities can be patched.
- Only trusted code libraries and official frameworks that prioritise safety implementations will be incorporated.

The priority would be to adopt a strict security mindset at all times.

## 4.2 As a programming auditor/tester

In the context of evaluating applications, considering the previous sections, security should be the main focus of development.

Therefore, here are some considerations that will apply to such a role:

- Rather than just pointing out security weaknesses, I will also come up with an actionable improvement plan at a high-level abstraction level to then implement it exactly via code.
- The security recommendations that I come up with that arise from testing will only minimally disrupt developers, seeking not to disturb their productivity.
- I also plan to facilitate a good relationship with developers by giving constructive criticism about their code quality and practices.
- The aim that I have is to promote a resilient code practice mindset that will propagate across all the different software development teams.

Taking a more holistic but supportive view will produce a better risk remediation plan for any future threats.

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
