# SpecTruMetRx Contribution Guidelines

Thank you for committing to working on the development of the **SpecTruMetRx Payments & Healthcare Analytics** solution with [us](https://www.DavidPLopez.com). We use our [Discord Chat Room](https://discord.gg/yw3BnBk) for our team and its contributors, please join us and use the `#engineering` channel in our [Discord Chat Room](https://discord.gg/yw3BnBk) to discuss any development related topics.

## Summary

The short version:

1. Write your Contribution
2. Make sure your contributin meets code, test, and commit message standards as described below.
3. Submit a Pull Request from a topic branch back to `master`. Include a checklist, as described below. (Optionally, assign this to a specific member for review.)
4. Respond to any discussion. When the reviewer decides it's ready, they will merge back `master` and fill out their own checklist.

## Project Goals

We are building a *Healthcare Payments & Analytics* software suite on the blockchain to **help hospitals improve patient outcomes, and to help insurers eliminate fraud with our Ai Workbench, while helping banks to quickly and easily search for a healthcare practice that they will want to loan money to by accessing our underwriting data**. Our application includes a backend API service to handle basic CRUD operations and is built on a **DARN** technology stack that includes the following tools:

* DynamoDB
* AWS Serverless Lambda
* React.js
* Node.js (Python for Utilities & Analytics)

Our goal is to make **SpecTruMetRx** a trusted healthcare software service partner for Healthcare practices around the world by building a secure and HIPAA compliant *Progressive Web Application* (PWA) to target every device on the market. We want to be the most accessible and practical healthcare payments network on the market. We will deploy our services to fulfill the needs of the following healthcare practice types:

* Behavior Analyst Practices
* Dental Clinics
* Physical & Occupational Therapy Clinics
* Urgent Care Centers & Hospitals

## SpecTruMetRx Project Structure

There are a few repositories to be aware of to be able to successfully contribute to the development of this application. Below are the list of repositories in question:

1. [BusinessAdmin](https://github.com/SpecTruMetRx/BusinessAdmin)
  * This repository contains all of the Business/Marketing Plans & Financial Models that identify the mission we are trying to achieve. **Please make sure you read these documents to understand our business before writing any code**.

2. [Documentation](https://github.com/SpecTruMetRx/Documentation)
  * This is the project documentation repository, where we will document every feature that we implement.

3. [SpectrumStack](https://github.com/SpecTruMetRx/SpectrumStack)
  * This is our serverless + microservice backend repository. Navigate to the `/services` sub-directory within the record to create new services for each feature that we need to implement. Each individual serverless + microservice will have its own `serverless.yml` file which will serve as the AWS CloudFormation template used to deploy AWS resources with an *Infrastructure As Code* paradigm.

4. [SpectrumClient](https://github.com/SpecTruMetRx/SpectrumClient)
  * This is our React.js frontend repository.

## Contribution Process

**SpecTruMetRx** uses Git for Software Version Control, and for branching and merging. Please review the repositories above to understand which repository you will need to working within.

### Roles

References to roles are made throughout this document. These are not intended to reflect titles or long-term job assignments; rather, these are used as descriptors to refer to members of the development team performing tasks in the check-in process. These roles are:

* *Author*: The individual who has made changes to files in the software repository, and wishes to check these in.
* *Reviewer*: The individual who reviews changes to files before they are checked in.
* *Integrator*: The individual who performs the task of merging these files. Usually the reviewer.

## SpecTruMetRx Git Commit Message Style Guide

#### Introduction

This style guide acts as the official guide to follow in your projects and commits. SpecTruMetRx evaluators will use this guide to complete *code reviews* of any work pushed to our repositories. There are many opinions on the "ideal" style in the world of development. Therefore, in order to reduce the confusion on what style engineers should follow during the course of their work, we urge all contibutors to refer to this style guide before committing their code.

#### Commit Messages

**Message Structure**

A commit messages consists of three distinct parts separated by a blank line: the title, an optional body and an optional footer. The layout looks like this:
```
type: subject

body

footer
```
The title consists of the type of the message and subject.

**The Type**

The type is contained within the title and can be one of these types:

* **feat**: a new feature
* **fix**: a bug fix
* **docs**: changes to documentation
* **style**: formatting, missing semi colons, etc; no code change
* **refactor**: refactoring production code
* **test**: adding tests, refactoring test; no production code change
* **chore**: updating build tasks, package manager configs, etc; no production code change

**The Subject**

Subjects should be no greater than 50 characters, should begin with a capital letter and do not end with a period.

Use an imperative tone to describe what a commit does, rather than what it did. For example, use change; not changed or changes.

**The Body**

Not all commits are complex enough to warrant a body, therefore it is optional and only used when a commit requires a bit of explanation and context. Use the body to explain the what and why of a commit, not the how.

When writing a body, the blank line between the title and the body is required and you should limit the length of each line to no more than 72 characters.

**The Footer**

The footer is optional and is used to reference issue tracker IDs.

**Example Commit Message**
```
feat: Summarize changes in around 50 characters or less

More detailed explanatory text, if necessary. Wrap it to about 72
characters or so. In some contexts, the first line is treated as the
subject of the commit and the rest of the text as the body. The
blank line separating the summary from the body is critical (unless
you omit the body entirely); various tools like `log`, `shortlog`
and `rebase` can get confused if you run the two together.

Explain the problem that this commit is solving. Focus on why you
are making this change as opposed to how (the code explains that).
Are there side effects or other unintuitive consequenses of this
change? Here's the place to explain them.

Further paragraphs come after blank lines.

 - Bullet points are okay, too

 - Typically a hyphen or asterisk is used for the bullet, preceded
   by a single space, with blank lines in between, but conventions
   vary here

If you use an issue tracker, put references to them at the bottom,
like this:

Resolves: #123
See also: #456, #789
```

**You can also just keep it simple and just use one-line commit messages as so:**

`$ git commit -m "feat: Adding new feature."`

