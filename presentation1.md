class: center, middle


# Code Quality

???

The idea is that every week (or every other week, or as needed) after the meeting I'll talk about some code quality issues, probably something that came up during the week. Not sure if this is going to be the right venue or format, but we'll see and figure it out!


---

class: middle


### The point

Improve your code to professional standards:

- always have up-to-date, legible, and professional code you can share with colleagues or at conferences
- always know which version of the code created what dataset
- easily collaborate with each other and with other colleagues
- learn coding patterns that will help you write code more quickly and make it simpler and clearer.
- this will save you time and make you look good.

???

[publish the exact code used to generate the data for every paper published.]

---

class: middle

This is not hard! It's mostly just being organized and learning a couple tools. 

But it can still take the rest of your life because it is about common-sense, discipline, and avoiding miscommunication.

You can always get better at it.

---

class: middle

"Anybody can write code that a computer can understand. Good programmers write code that humans can understand."

- Martin Fowler

"You spend more time reading code than writing it."

???

(So it should be optimized for clarity of understanding when reading)


---

class: middle

1. Basics of project organization
2. Get your project in github
3. Bare minimum code quality: follow a style guide

???

Following a styleguide doesn't require much experience or discernment, but it makes things way easier. We'll be talking about code quality practices that requirem more judgement soon.

---

class: center, middle

### Project Organization

---

class: middle

Your project should be organized according to language-specific best practices.

Usually, that means these types of things are kept separate:

- scripts / executables
- code libraries / modules / objects
- artifacts / output
- documentation (except when documentation is inline to the code)

Always include a README and enough information for somebody (this includes "future you") get started!

???

you are going to get a paper accepted, it gets published in 2017 and you start getting questions and you will have moved on to cooler things, and you won't remember how to run the code you wrote two years ago. And you will have to spend a day trying to figure out how to run the code, and what other files you used, etc. Don't do that, write the README and keep it up-to-date. ]

---

class: middle

Sample python project directory structure:

```
README
LICENSE
setup.py
requirements.txt
sample/__init__.py
sample/core.py
sample/helpers.py
docs/conf.py
docs/index.rst
tests/test_basic.py
tests/test_advanced.py
```

Read this: http://docs.python-guide.org/en/latest/writing/structure/


---

class: middle

Sample node.js project directory structure

??

```
README
LICENSE
/lib/
package.json
```

??

---

class: center, middle

### Github

---

class: middle

git is a code quality tool for version control. github is a host for git projects that is free for public projects, and includes great collaboration and workflow tools.

it facilitates:

- backup
- recordkeeping
- collaboration and review

Getting started: http://rogerdudler.github.io/git-guide/
If you want to nerd out: http://git-scm.com/book/en/v2

???

- backup [you should never, ever lose more than a few hours of work, even if your laptop explodes]
- recordkeeping [you should always know which code revision produced which dataset]
- collaboration and review [ code reviews, comments, pull requests, issue tracker ]


everybody used git?

- branches?
- tags?
- merges?
- forks?
]

---

class: middle, center

All code that is longer than a 2-hour project should be in github!

---

class: middle

I created two github projects last week.

https://github.com/paulboone/sam-modules
https://github.com/paulboone/sam-bin

If you are not online, you can just make a new dir and `git init` so you are ready to push it later.

???

why:

- there is no way I will remember how to compile node.js so I scripted it and made it repeatable.
- other people might want to compile node.js for sam, so I can share it with them.
- sam-bin: if it is not in a repo, what happens if there is data-loss on ihome? will I remember the script? how will I tell if I've made changes to the scripts?


---

class: middle

First, organize your project according to language-specific best practices. Then:

- create your own github account.
- push your project to your github account. 
- send me the link! I am your first collaborator.

???

what should be on wilmerlab vs your site?
this will be primarily where we interact

---

class: middle

Ultimately, you are responsible for and in charge of how you code, and what it looks like. That means choosing your:

- development OS
- IDE or text editor
- language
- style guide
- version control system

???

But some choices are bad!

But there are lots of tradeoffs to make and you can make good or bad decisions with any of this. I'm going to make suggestions (and some of this is really just not worth thinking about) but you can make different decisions than I would make as long as you're willing to do the homework.

---

class: middle

### Recommendation: use linux.

If you are writing code for the supercomputer cluster, consider doing the development on a linux machine or vm (i.e. MacOSX, Ubuntu, Fedora, etc). This is so your tools match up. You can write build scripts, bash scripts, etc on your development machine and (mostly) expect them to run on the supercomputer cluster. If you do all your development on a windows machine, you will have to deal with more platform issues and will have to learn two sets of tools.

---

class: middle

Basic Coding Style Guides

- CHOOSE ONE
- Make well-researched and justifiable changes to it if you must
- but BE CONSISTENT

and, if you are using a higher-level language like python or javascript, use a linter.

---

class: middle

### Recommendations

Python: PEP8

javascript:
https://github.com/felixge/node-style-guide
but:

- do not “Use Semicolons"
- do not "Use multi-line ternary operator"
- "80 characters per line" => 100 is ok.

and always `use strict`: https://www.npmjs.com/package/use-strict

others: ?

---

class: middle

Be consistent!

If you differ from best practices, do it intentionally–don't be sloppy!

---

class: middle

Future things to talk about:

- git techniques
  - git workflows
  - merges / conflicts
  - pull requests
  - good / bad branching practices
  - atomic commits and good commit messages
  
- good commenting practices
- simple code refactors for better communication
- testing
- profiling and optimization




---

The end.

---

class: middle, center

# Code Quality 2016-03-10

---

class: middle, center

## Shared Stack

https://github.com/WilmerLab/stackdocs


---

class: middle, center

## Random lessons from the week


---

class: middle

### Copying functions, files, configs to multiple places will ruin your life.

Generally:

- if you are copying functions into multiple files => put them in a library and include them.
- if you are copying code files to multiple places => there's a better way to structure your project.
- if there is no way around it, automate it. Don't do ANYTHING BY HAND because you will make a mistake and screw it up. The files should be recreated every time the code changes.

Don't copy code, don't copy configs, don't copy jobs files. If you find yourself doing this and can't think of a better way to do it, talk to me and we'll find a better solution.

---

### Use descriptive variable names

- except maybe for dimensions (like x,y,z) and certain mathematical quantities, single-letter variables names should be avoided.
- don't make people guess what something is, actually describe it.
- if somebody else were reading your code, would they immediately understand what your variable means? If not, they would immediately ask "what is this variable?" The answer to that question is what you name that variable. Then, when this happens in real life, you can skip both the question and the answer, and when you forget how everything works in six months, you can answer yourself.

---

class: middle

### Git Basics

Concepts:

- remote repository / local working copy
  - git push / git pull
- making changes to your local working copy:
  - git add / git commit


Getting started: http://rogerdudler.github.io/git-guide/  
If you want to nerd out: http://git-scm.com/book/en/v2  
Git command cheat sheet: https://www.git-tower.com/blog/git-cheat-sheet/  

---

### Basic Demo

- creating a repository
- git pull
- committing
- git push

???

Now do it with git kraken?


---
class: middle

### Commits

1. **master should ALWAYS work.**

2. commits should be atomic, meaning they should do ONE thing and the code should work both before and after. Don't mix multiple features, bug fixes, etc into one commit.

3. all experimental work, all incomplete work, all NON-WORKING work should be in branches.

4. commits should leave the code in a working state. 
  - exceptions are allowed when you are working on a branch and you clean up the commits before merging back to master.
  
5. **master should ALWAYS work.**

???

You should always be ready to share master with someone important you just met at a conference, without any shred of doubt or concern.


---
class: middle
### Commit messages

- should state what you did, but more importantly WHY you did it, and what the purpose was.

- remember that it should only be one thing. If you are using the word "and" in describing what you did, you likely need another commit.

---
class: middle

### Commit message examples

https://github.com/numat/RASPA2/commits/master


---

class: middle

I helped with this so I know what it means, but a reasonable person could ask "why was the timeout removed?"

A better message would have been: "removed unnecessary 1s timeout which was causing MacOSX runs to fail after 1s. Other platforms seem to have been ignoring the timeout and would wait indefinitely for the RASPA process to complete (which is the desired behavior)."

???

You'll get lots of feedback on these, going forward.



---

A basic workflow for something simple:

```
git checkout master
git pull
### make changes
git add ...
git commit -m "this is what I did and why I did it"
git push
```


---

A workflow for something more complex, or that will take longer:

```
git checkout master
git pull
git branch my_new_feature
git checkout my_new_feature
### make changes
git add ...
git commit -m "this is what I did and why I did it"
git checkout master
git merge my_new_feature
git push
```

---

### Branching guidelines

- if you are working on something small, making changes and committing to master is fine.

- if you are working on something large or experimental, make a branch

- if you are working on something large or experimental, and you start making changes that are generally useful and would immediately work on master, you may want to put those directly on master. (otherwise, you'll start expecting to be able to use that code, but when you branch for a new feature, it won't be there).



---


Getting started: http://rogerdudler.github.io/git-guide/  

If you want to nerd out: http://git-scm.com/book/en/v2  

Git command cheat sheet: https://www.git-tower.com/blog/git-cheat-sheet/  


---

The end.




---

commenting:
     explain what it SHOULD do, not what it is doing
     explain the why, not the what
     but also for you to remember what you did, when it isn’t obvious
     when you do something that could look like a mistake to somebody else
     to explain something that wouldn’t immediately make sense to a “reasonable” programmer


---

Using git (and github) with a proper process means:

PUSHING
- your code is always backed up remotely

BRANCHING
- you always have a working version of your code, even when you are experimenting on multiple things.
     - in industry, this means the code that is deployed to your users and is currently in use

TAGGING
- you have a record of the exact code you used to generate a dataset
     - in industry, this means everytime code is released to users, you have a record of the exact version of the code released.
     - in education, this likely means you record the release

PULLING / MERGING
- multiple people can work on a codebase without clobbering each other

FORKING:
 - forking other people’s projects, making pull requests

GITHUB
- easily comment on other people’s commits (code reviews)
