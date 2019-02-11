Welcome to the Workshop
===

---

## Points to cover
* Some vocabluary to begin with
* How OSD is built currently
* How we planned on changing this workflow
* How to work in the command line efficiently
* Git and especially git-flow
* How linux works (in general, just an overview)
* Why we do the changes we do

---

## Some vocabluary to begin with
![boring](https://media.giphy.com/media/MGmnFOZRFRo4w/giphy.gif)

~~~

git
> Git (/ɡɪt/) is a distributed version-control system for tracking changes in
> source code during software development. It is designed for coordinating
> work among programmers, but it can be used to track changes in any set of
> files. Its goals include speed, data integrity, and support for
> distributed, non-linear workflows.
*~wikipedia.org*

~~~

Jenkins
> Jenkins is an open source automation server written in Java. Jenkins helps to
> automate the non-human part of the software development process, with
> continuous integration and facilitating technical aspects of continuous
> delivery. It is a server-based system that runs in servlet containers such as
> Apache Tomcat.
*~wikipedia.org*

~~~

CI
> In software engineering, continuous integration (CI) is the practice of
> merging all developer working copies to a shared mainline several times a day.
*~wikipedia.org*

~~~

CDE
> Continuous delivery (CD or CDE) is a software engineering approach in which
> teams produce software in short cycles, ensuring that the software can be
> reliably released at any time and, when releasing the software, doing so
> manually. It aims at building, testing, and releasing software with
> greater speed and frequency.
*~wikipedia.org*

~~~

CD
> Continuous deployment (CD) is a software engineering approach in which
> software functionalities are delivered frequently through automated
> deployments.
*~wikipedia.org*

~~~

Agile software development
> Agile software development is an approach to software development under which
> requirements and solutions evolve through the collaborative effort of
> self-organizing and cross-functional teams and their customer(s)/end
> user(s).[1] It advocates adaptive planning, evolutionary development,
> empirical knowledge, and continual improvement, and it encourages rapid and
> flexible response to change.
*~wikipedia.org*

~~~

DevOps
> DevOps (a clipped compound of "development" and "operations") is a software
> development methodology that combines software development (Dev) with
> information technology operations (Ops) to shorten the systems development
> life cycle while delivering features, fixes, and updates frequently in close
> alignment with business objectives.
*~wikipedia.org*

~~~

Scrum
> Scrum is an agile framework for managing knowledge work, with an emphasis on
> software development. It is designed for teams of three to nine members, who
> break their work into actions that can be completed within timeboxed
> iterations, called "sprints", no longer than one month and most commonly two
> weeks, then track progress and re-plan in 15-minute time-boxed stand-up
> meetings, called daily scrums.
*~wikipedia.org*

~~~

Scalability
> Scalability is the capability of a system, network, or process to handle a
> growing amount of work, or its potential to be enlarged to accommodate that
> growth.
*~wikipedia.org*

~~~

DebianRepository
> A Debian repository is a set of Debian binary or source packages organized in
> a special directory tree and with various infrastructure files - checksums,
> indices, signatures, descriptions translations, ... - added. Client computers
> can connect to the repository to download and install the packages using an
> Apt-based package management tool.
*~debian.org*

~~~

APT
> Advanced Package Tool, or APT, is a free-software user interface that works
> with core libraries to handle the installation and removal of software on
> Debian, Ubuntu, and related Linux distributions.
*~wikipedia.org*

~~~

Filesystem Hierarchy Standard
> The Filesystem Hierarchy Standard (FHS) defines the directory structure and
> directory contents in Linux distributions. It is maintained by the Linux
> Foundation. The latest version is 3.0, released on 3 June 2015.
*~wikipedia.org*

~~~

Groovy
> Apache Groovy is a Java-syntax-compatible object-oriented programming language
> for the Java platform.
*~wikipedia.org*

~~~

*~wikipedia.org*

~~~


---

## How OSD is built currently

~~~

Currently built on Jenkins with a Jenkinsfile
![Image of jenkins](resources/images/Jenkins.png)

~~~

```Groovy
node() {
    try {
      stage('Checkout') { checkout scm }

      dir("development") {
        stage('Check prerequisites') {
          sh './check_prerequisites.sh'
          sh 'df -h'
        }
        stage('Download ISO') {
          sh './get_newest_mini_iso.sh'
        }
...
}
```

~~~

... or locally within docker
![Image of docker build](resources/images/Dockerbuild.png)

---

### Jenkins
* is used as our build server
* has a pipeline system which is programmable in groovy
* builds every time a 'git push' happens

---

## Changes we planned for this workflow
* Using docker on Jenkins
* Making the whole process more granular
* Therefore making more use of the pipeline
* Use ansible as configuration management tool
* Simplifying things in general

---

## How to work in the command line efficiently
* Zsh
* Vim vs vi
* Useful unix programs
* Handle command output and command chaining
* Some tricks
* Cheat sheets
* Dotfiles

---

## zsh
* customisation
* autocompletion

<!--
touch testfile{1..6}.txt, ls, echo "this is a test" > testfile{1,2}.txt
ll testfile<tab><tab>, rm testfile{2,4}.txt, ls. rm *
-->

---

## vim vs vi
* w? q? wq!
* plugins

---

## useful unix programs
* manpages '/' to search
* cat
* grep
* ssh

---

## handle command output and command chaining
* <( )
* $( )
* wget -O -
* echo "hi" |
* <<, <, >, >>, <<<
* $?
* &&, ||, ;

---

## some tricks
* '' vs ""
* set -e, set -x
* /usr/bin/env bash
* ctrl arrows
* ctrl shift arrows
* ctrl r
* alt .
* TERM=ansi

---

## cheat sheets
* vim
* git
* regex
* unix

---

## dotfiles
* vimrc
* zshrc
* use of alias
* gitconfig

---

* git and especially git-flow
    * working with branches
        * feature, hotfix, bugfix, release, dev
    * commits
        * write good commit messages
        * how often to commit
    * conflicts
        * why
        * how to resolve
    * configuration of git
        * gitconfig
        * gitignore
    * git diff
    * remotes / HEAD / revisions
    * rebase correctly
    * stash
* how linux works (in general, just an overview)
    * what is a kernel
        * managing hardware resources
        * managing software
        * abstracting hardware
    * what is a kernel module
        * providing functionality
        * simple interface
    * where (and where not) to put files
        * FHS
        * /tmp is mounted in ram
        * clean up after yourself
        *
* why we do the changes we do
    * compliance
    * security
    * ease of use
    * pre requisites for making linux work inside of bosch

generally make everyone more interested in the project and technology in general
