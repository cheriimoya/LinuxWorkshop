Welcome to the Workshop
===

---

## Points to cover
<ul>
<li class="fragment">Some vocabluary to begin with</li>
<li class="fragment">How OSD is built currently</li>
<li class="fragment">How we planned on changing this workflow</li>
<li class="fragment">How to work in the command line efficiently</li>
<li class="fragment">Git and especially git-flow</li>
<li class="fragment">How linux works (in general, just an overview)</li>
<li class="fragment">Why we do the changes we do</li>
</ul>

---

## Some vocabluary to begin with
<div class="fragment">
![boring](https://media.giphy.com/media/MGmnFOZRFRo4w/giphy.gif)
</div>

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

docker
> Docker is a computer program that performs operating-system-level
> virtualization, also known as "containerization". It was first released
> in 2013 and is developed by Docker, Inc. Docker is used to run software
> packages called "containers". Containers are isolated from each other and
> bundle their own application, tools, libraries and configuration files;
> they can communicate with each other through well-defined channels
*~wikipedia.org*

~~~

qemu
> QEMU (short for Quick Emulator) is a free and open-source emulator that
> performs hardware virtualization. QEMU is a hosted virtual machine monitor:
> it emulates the machine's processor through dynamic binary translation and
> provides a set of different hardware and device models for the machine,
> enabling it to run a variety of guest operating systems.
*~wikipedia.org*

---

## How OSD is built currently

~~~

Currently built on Jenkins with a Jenkinsfile
<div class="fragment">
![Image of jenkins](resources/images/Jenkins.png)
</div>

~~~

... or locally within docker
![Image of docker build](resources/images/Dockerbuild.png)

---

### Jenkins
<ul>
<li class="fragment">is used as our build server</li>
<li class="fragment">has a pipeline system, programmable in groovy</li>
<li class="fragment">builds every time a 'git push' happens</li>
<li class="fragment">will notify bitbucket about build status</li>
</ul>
<div class="fragment">![jenkins logo](https://jenkins.io/images/logos/jenkins/jenkins.svg)</div>

~~~

#### Scripted Pipeline syntax
* node() { ... }
<div class="fragment">~ computer to build on</div>
* stage( '...' ) { ... }
<div class="fragment">~ block of code that executes defined task</div>
* step
<div class="fragment">~ actual task being run</div>

~~~

#### Example
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

#### Iso build process
![build diagram](https://inside-docupedia.bosch.com/confluence/rest/gliffy/1.0/embeddedDiagrams/1114b640-dcaf-4dc4-b836-e30f6a1d1ddd.png)
[Build process](https://inside-docupedia.bosch.com/confluence/display/BSC2OSD/ISO+Build+Process)

---

### docker
<ul>
<li class="fragment">Can be used to build osd in a container without touching any files on the host</li>
<li class="fragment">Always produces the same output given the same input</li>
</ul>
<div class="fragment">![docker logo](https://upload.wikimedia.org/wikipedia/commons/4/4e/Docker_%28container_engine%29_logo.svg)</div>

~~~

Dockerfile is used for config
```dockerfile
FROM ubuntu:xenial
ADD res/sources.list /etc/apt/sources.list
RUN apt-get update
RUN apt-get install --no-install-recommends -y sudo
ADD development.tar.gz /workspace-osd
WORKDIR "/workspace-osd/development"
ENTRYPOINT [ "bash", "run_inside_docker.sh" ]
```

---

### Testing
<ul>
<li class="fragment">still done by qemu</li>
<li class="fragment">docker has some limitations</li>
</ul>

---

### ansible

---

## Changes we planned for this workflow
<ul>
<li class="fragment">Using docker on Jenkins</li>
<li class="fragment">Making the whole process more granular</li>
<li class="fragment">Therefore making more use of the pipeline</li>
<li class="fragment">Use ansible as configuration management tool</li>
<li class="fragment">Simplifying things in general</li>
</ul>

---

## How to work in the command line efficiently
<ul>
<li class="fragment">Zsh</li>
<li class="fragment">Vim vs vi</li>
<li class="fragment">Useful unix programs</li>
<li class="fragment">Handle command output and command chaining</li>
<li class="fragment">Some tricks</li>
<li class="fragment">Cheat sheets</li>
<li class="fragment">Dotfiles</li>
</ul>

---

## Zsh
<ul>
<li class="fragment">customisation</li>
<li class="fragment">autocompletion</li>
</ul>

<!--
touch testfile{1..6}.txt, ls, echo "this is a test" > testfile{1,2}.txt
ll testfile<tab><tab>, rm testfile{2,4}.txt, ls. rm *
-->

---

## vim vs vi
<ul>
<li class="fragment">w? q? wq!</li>
<li class="fragment">plugins</li>
</ul>

---

## Useful unix programs
<ul>
<li class="fragment">manpages '/' to search</li>
<li class="fragment">cat</li>
<li class="fragment">grep</li>
<li class="fragment">ssh</li>
</ul>

---

## Handle command output and command chaining
<ul>
<li class="fragment"><( )</li>
<li class="fragment">$( )</li>
<li class="fragment">wget -O -</li>
<li class="fragment">echo "hi" |</li>
<li class="fragment"><<, <, >, >>, <<<</li>
<li class="fragment">$?</li>
<li class="fragment">&&, ||, ;</li>
</ul>

---

## Some tricks
<ul>
<li class="fragment">'' vs ""</li>
<li class="fragment">set -e, set -x</li>
<li class="fragment">/usr/bin/env bash</li>
<li class="fragment">ctrl arrows</li>
<li class="fragment">ctrl shift arrows</li>
<li class="fragment">ctrl r</li>
<li class="fragment">alt .</li>
<li class="fragment">TERM=ansi</li>
</ul>

---

## Cheat sheets
<ul>
<li class="fragment">vim</li>
<li class="fragment">git</li>
<li class="fragment">regex</li>
<li class="fragment">unix</li>
</ul>

---

## Dotfiles
<ul>
<li class="fragment">vimrc</li>
<li class="fragment">zshrc</li>
<li class="fragment">use of alias</li>
<li class="fragment">gitconfig</li>
</ul>

---

## Git and especially git-flow
* working with branches
    * feature, hotfix, bugfix, release, dev

~~~

* commits
    * write good commit messages
    * how often to commit

~~~

* conflicts
    * why
    * how to resolve

~~~

* configuration of git
    * gitconfig
    * gitignore

~~~

* git diff

~~~

* remotes / HEAD / revisions

~~~

* rebase correctly
* stash

---

## How linux works (in general, just an overview)

~~~

### What does the linux kernel do?
* managing hardware resources
* managing software
* abstracting hardware

~~~

### What do we need kernel modules for?
* providing functionality
* simple interface

~~~

## Where (and where not) to put files
* FHS
* /tmp is mounted in ram
* clean up after yourself

---

## why we do the changes we do
* compliance
* security
* ease of use
* pre requisites for making linux work inside of bosch

generally make everyone more interested in the project and technology in general
