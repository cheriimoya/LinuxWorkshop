Day 2
===

---

## Agenda

~~~

### Day 2

<ul>
<li class="fragment">Your expectations</li>
<li class="fragment">Self reflection</li>
<li class="fragment">Defining learning goals</li>
<li class="fragment">Tree of good harvest</li>
<li class="fragment">What can we improve?</li>
<li class="fragment">Definitions of the day</li>
<li class="fragment">Breaking down the installation process</li>
<li class="fragment">Analysing it</li>
<li class="fragment">Questions for me... and you;)</li>
<li class="fragment">Feedback round & closing</li>
</ul>

---

### Recap (what did we learn yesterday?)

<ul>
<li class="fragment">Why OSD is a cool project</li>
<li class="fragment">What we can (and must) improve</li>
<li class="fragment">Meaning behind CI, CDE and CD</li>
<li class="fragment">How the build process works</li>
</ul>

---

### Definitions of the day

~~~

Jenkins
> Jenkins is an open source automation server written in Java. Jenkins helps to
> automate the non-human part of the software development process, with
> continuous integration and facilitating technical aspects of continuous
> delivery. It is a server-based system that runs in servlet containers such as
> Apache Tomcat.
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

### How OSD is built currently

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

### Playing around with "local" Jenkins (maybe)

---

### docker
<ul>
<li class="fragment">Can be used to build osd in a container without touching any files on the host</li>
<li class="fragment">Always produces the same output given the same input</li>
</ul>
<div class="fragment">![docker logo](https://upload.wikimedia.org/wikipedia/commons/4/4e/Docker_%28container_engine%29_logo.svg)</div>

~~~

Dockerfile is used for preparing docker
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

### Visualizing the build process

---

### Create litte docker container

~~~

### Build iso in docker (old way)

~~~

### Build iso in docker (new way)

---

### Testing

<ul>
<li class="fragment">Why do we still use QEMU?</li>
<li class="fragment">docker and its limitations</li>
<li class="fragment">Boot up OSD image in qemu</li>
</ul>

---

### Changes we planned for this workflow

<ul>
<li class="fragment">Using docker on Jenkins</li>
<li class="fragment">Making the whole process more granular</li>
<li class="fragment">Therefore making more use of the pipeline</li>
<li class="fragment">Use ansible as configuration management tool</li>
<li class="fragment">Simplifying things in general</li>
</ul>

---

### Feedback

---

### Thanks:)
