# SpecTruMetRx Contribution Guidelines

Thank you for committing to working on the development of the **SpecTruMetRx Payments & Healthcare Analytics** solution with [us](https://www.DavidPLopez.com). We use our [Discord Chat Room](https://discord.gg/yw3BnBk) for our team and its contributors, please join us and use the `#engineering` channel in our [Discord Chat Room](https://discord.gg/yw3BnBk) to discuss any development related topics.

## Summary

The short version:

1. Write your Contribution
2. Make sure your contributin meets code, test, and commit message standards as described below.
3. Submit a Pull Request from a topic branch back to `master`. Include a checklist, as described below. (Optionally, assign this to a specific member for review).
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

### Branching

Four basic types of branches may be included in the repositories above:

1. Master branch
2. Dev branch
2. Topic branches
3. Developer branches

Branches which do not fit into the above categories may be created and used during the course of development for various reasons, such as large-scale refactoring of code or implementation of complex features which may cause instability. In these exceptional cases it is the responsibility of the developer who initiates the task which motivated this branching to communicate to the team the role of these branches and any associated procedures for the duration of their use.

**Master Branch**

The `master` branch is the `PROD` ready version of the application which should be a **stable** version of our software. Development branches will be merged into the `master` branch only by the **Product Owner** after having reviewed all Source Code, Code Reviews, and Pull Requests.

**Dev Branch**

The role of the `dev` branch is to represent the latest "ready for unit testing" version of the software. Source code on the `dev` branch has undergone peer review, and will undergo regular automated testing with notification on failure. Development branches may be unstable (particularly for recent features), but the intent is for the stability of any features on `dev` branches to be non-decreasing. It is the shared responsibilityt of authors, reviewers, and integrators to ensure this. Create all Pull Requests to merge *Topic* branches into the *Dev* branch of the application.

**Topic Branches**

Topic branches are used by developers to perform and record work on issues.

Topic branches do not need to be stable, even when pushed to the central repository; in fact, the practice of making incremental commits while working on an issue and pushing these to the central repository is encouraged, to avoid lost work and to share work-in-progress. (Small commits also help isolate changes, which can help in identifying which change introduced a defect, particularly when that defect went unnoticed for some time, ed using `git bisect`).

Topic branches should be named according to their corresponding issue identifiers, all lower case, with hyphens. (e.g. branch spectrum-9 would refer to issue #9). Currently topic branches have been named according to the issue subject line e.g. clinic-registration. Please adjust as needed.

**Developer Branches**

Developer branches are any branches used for purposes outside of the scope stated above; e.g. to "try things out", or to maintain a "my latest stuff" branch that is not delayed by the review and integration process. These may be pushed to the central repository, and may follow any naming convention desired so long as the owner of the branch is identifiable, and so long as the name chosen could not be mistaken for a `topic` or `master` branch. e.g.:

`$ git checkout -b lopez-my-stuff-branch`

### Merging

When development is complete on an issue the first step toward merging it back into the `master` branch is to file a **Pull Request** to first merge the work to review into the `dev` branch. The contributions should meet code, test, and commit message standards as described below, and the pull request should include a complete author checklist, also as described below. Pull Requests may be assigned to specific team members when appropriate and should **ONLY be requested for merging into** the `dev` branch (e.g. to draw the person's attention).

Code review should take place using discussion features within the Pull Request. When the reviewer is satisfied, they should add a comment to the pull request containing the reviewer checklist (from below) and complete the merge back into the `dev` branch.

#### Merge into PROD (`master` branch) by Product Owner ONLY!!!

Upon the successful completion of the merge into `dev` the reviewer/integrator **SHALL** create a second Pull Request to merge the `dev` branch into the `master` branch.

The **SpecTruMetRx** Product Owner is the only person authorized to merge the `dev` branch into `master` for automated deployment into `Production`.

## Standards

Contributing to **SpecTruMetRx** must satisfy **ESLint** under the default settings for `create-react-app` on the frontend or the settings documented in the SpectrumStack repository for the backend.

### Code Standards

JavaScript sources in **SpecTruMetRx** should:

* Use Tabs. Spaces should not be used (ESLint & JSFormatter will resolve automatically).
* Include JSDoc for any exposed API (e.g. public methods, constructors).
* Include non-JSDoc comments as-needed for explaining private variables, methods, or algorithms when they are non-obvious.
* Define one public class per script, expressed as a constructor function returned from an AMD-style module.
* Follow “Java-like” naming conventions. These includes:
  * Classes should use camel case, first letter capitalized (e.g. SomeClassName).
  * Methods, variables, fields, and function names should use camel case, first letter lower-case (e.g. someVariableName).
  * Constants (variables or fields which are meant to be declared and initialized statically, and never changed) should use only capital letters, with underscores between words (e.g. SOME_CONSTANT).
  * File names should be the name of the exported class, plus a .js extension (e.g. SomeClassName.js).
* Avoid anonymous functions, except when functions are short (a few lines) and/or their inclusion makes sense within the flow of the code (e.g. as arguments to a forEach call).
* Avoid deep nesting (especially of functions), except where necessary (e.g. due to closure scope).
* End with a single new-line character.
* Expose public methods by declaring them on the class's prototype.
* Within a given function's scope, do not mix declarations and imperative code, and  present these in the following order:
  * First, variable declarations and initialization.
  * Second, function declarations.
  * Third, imperative statements.
  * Finally, the returned value.

Deviations from **SpecTruMetRx** code style guidelines require two-party agreement, typically from the author of the change and its reviewer.

#### Code Example

```js
/*global define*/

/**
 * Title: someClass.js WebService API
 * SpecTruMetRx - MediPayCore
 * Author: Engineer's Name
 * [Month] [Day], [Year]
 *
 * Bundles should declare themselves as namespaces in whichever source
 * file is most like the "main point of entry" to the bundle.
 * @namespace some/bundle
 */
define(
    ['./OtherClass'],
    function (OtherClass) {
        "use strict";

        /**
         * A summary of how to use this class goes here.
         *
         * @constructor
         * @memberof some/bundle
         */
        function ExampleClass() {
        }

        // Methods which are not intended for external use should
        // not have JSDoc (or should be marked @private)
        ExampleClass.prototype.privateMethod = function () {
        };

        /**
         * A summary of this method goes here.
         * @param {number} n a parameter
         * @returns {number} a return value
         */
        ExampleClass.prototype.publicMethod = function (n) {
            return n * 2;
        }

        return ExampleClass;
    }
);
```

### Test Standards

Automated testing shall occur whenever changes are merged into the main development branch and must be confirmed alongside any pull request.

Automated tests are typically unit tests which exercise individual software components. Tests are subject to code review along with the actual implementation, to ensure that tests are applicable and useful.

Examples of useful tests:
* Tests which replicate bugs (or their root causes) to verify their resolution.
* Tests which reflect details from software specifications.
* Tests which exercise edge or corner cases among inputs.
* Tests which verify expected interactions with other components in the system.

During automated testing, code coverage metrics will be reported. Line coverage must remain at or above 80%.

## SpecTruMetRx Git Commit Message Style Guide

#### Introduction

This style guide acts as the official guide to follow in your projects and commits. SpecTruMetRx evaluators will use this guide to complete *code reviews* of any work pushed to our repositories. There are many opinions on the "ideal" style in the world of development. Therefore, in order to reduce the confusion on what style engineers should follow during the course of their work, we urge all contibutors to refer to this style guide before committing their code.

Commit messages should:

* Contain a one-line subject, followed by one line of white space, followed by one or more descriptive paragraphs, each separated by one line of white space.
* Contain a short (usually one word) reference to the feature or subsystem the commit effects, followed by a colon, at the start of the subject line (e.g. `feat: Draft of check-in process`).
* Contain a reference to a relevant issue number in the body of the commit.
  * This is important for traceability; while branch names also provide this, you cannot tell from looking at a commit what branch it was authored on.
  * This may be omitted if the relevant issue is otherwise obvious from the commit history (that is, if using `git log` from the relevant commit directly leads to a similar issue reference) to minimize clutter.
* Describe the change that was made, and any useful rationale therefore.
  * Comments in code should explain what things do, commit messages describe how they came to be done that way.
* Provide sufficient information for a reviewer to understand the changes made and their relationship to previous code.

Commit messages should not:

* Exceed 54 characters in length on the subject line.
* Exceed 72 characters in length in the body of the commit,
  * Except where necessary to maintain the structure of machine-readable or machine-generated text (e.g. error messages).

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

Subjects should be no greater than 54 characters, should begin with a capital letter and do not end with a period.

Use an imperative tone to describe what a commit does, rather than what it did. For example, use change; not changed or changes.

**The Body**

Not all commits are complex enough to warrant a body, therefore it is optional and only used when a commit requires a bit of explanation and context. Use the body to explain the what and why of a commit, not the how.

When writing a body, the blank line between the title and the body is required and you should limit the length of each line to no more than 72 characters.

**The Footer**

The footer is optional and is used to reference issue tracker IDs.

**Example Commit Message**
```
feat: Summarize changes in around 54 characters or less

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

## Issue Reporting

Issues are tracked at https://github.com/SpecTruMetRx/Documentation/issues.

Issues should include:

* A short description of the issue encountered.
* A longer-form description of the issue encountered. When possible, steps to reproduce the issue.
* When possible, a description of the impact of the issue. What use case does it impede?
* An assessment of the severity of the issue.

Issue severity is categorized as follows (in ascending order):

* _Trivial_: Minimal impact on the usefulness and functionality of the software; a "nice-to-have."
* _(Unspecified)_: Major loss of functionality or impairment of use.
* _Critical_: Large-scale loss of functionality or impairment of use, such that remaining utility becomes marginal.
* _Blocker_: Harmful or otherwise unacceptable behavior. Must fix.

