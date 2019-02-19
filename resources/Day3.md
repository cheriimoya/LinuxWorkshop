Day 3
===

---

## Agenda

~~~

### Day 3

<ul>
<li class="fragment">Recap</li>
<li class="fragment">Definitions of the day</li>
<li class="fragment">Understanding the installation process</li>
<li class="fragment">Why do we do the changes we do?</li>
<li class="fragment">What is going to change?</li>
</ul>

---

### Recap (what did we learn yesterday?)

<ul>
<li class="fragment">What Jenkins, docker and QEMU are</li>
<li class="fragment">How we use them in the project currently</li>
<li class="fragment">How we want to use them in the future</li>
<li class="fragment">Correlation and order of scripts used</li>
</ul>

---

### Definitions of the day

~~~

Jinja
> Jinja is a web template engine for the Python programming language and is
> licensed under a BSD License created by Armin Ronacher. It is similar to the
> Django template engine but provides Python-like expressions while ensuring
> that the templates are evaluated in a sandbox. It is a text-based template
> language and thus can be used to generate any markup as well as sourcecode.
*~wikipedia.org*

~~~

Grub
> GNU GRUB (short for GNU GRand Unified Bootloader, commonly referred to as GRUB)
> is a boot loader package from the GNU Project. GRUB is the reference
> implementation of the Free Software Foundation's Multiboot Specification, which
> provides a user the choice to boot one of multiple operating systems installed
> on a computer or select a specific kernel configuration available on a
> particular operating system's partitions.
*~wikipedia.org*

~~~

Debian installer / Preseed
> Debian-Installer is an installation program designed for the Debian Linux
> distribution. It originally appeared in Debian release 3.1 (Sarge),[2] released
> on June 6, 2005,[3] although the first release of a Linux distribution it was
> used with was Skolelinux Venus (1.0).[4] It is also one of two official
> installers available for Ubuntu; the other being called Ubiquity (itself based
> on parts of debian-installer) which was introduced in Ubuntu 6.06 (Dapper
> Drake).
*~wikipedia.org*

~~~

UUID
> A universally unique identifier (UUID) is a 128-bit number used to identify
> information in computer systems. The term globally unique identifier (GUID) is
> also used.
> When generated according to the standard methods, UUIDs are for practical
> purposes unique, without depending for their uniqueness on a central
> registration authority or coordination between the parties generating them,
> unlike most other numbering schemes. While the probability that a UUID will be
> duplicated is not zero, it is close enough to zero to be negligible.
*~wikipedia.org*

~~~

systemd
> Systemd (stylized as systemd) is a software suite that provides fundamental
> building blocks for a Linux operating system. It includes the systemd
> "System and Service Manager", an init system used to bootstrap user space
> and manage user processes.
> systemd aims to unify service configuration and behavior across Linux
> distributions. It replaces the UNIX System V and BSD init systems.
> Since 2015, the majority of Linux distributions have adopted systemd,
> and it is considered a de facto standard.
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

Ansible
> In computing, Ansible is an open-source software provisioning, configuration
> management, and application deployment tool. It runs on many Unix-like
> systems, and can configure both Unix-like systems as well as Microsoft Windows.
> It includes its own declarative language to describe system configuration.
> It was written by Michael DeHaan and acquired by Red Hat in 2015. Unlike
> competing products, Ansible is agentless - temporarily connecting remotely via
> SSH or remote PowerShell to do its tasks.
*~wikipedia.org*

---

### The installation process

<ul>
<li class="fragment">Breaking it down</li>
<li class="fragment">Analysing it</li>
<li class="fragment">Presenting the analysis</li>
<li class="fragment">Q&A</li>
<li class="fragment">Summary of the process</li>
</ul>

---

### why we do the changes we do

<ul>
<li class="fragment">Compliance</li>
<li class="fragment">Security</li>
<li class="fragment">Ease of use</li>
<li class="fragment">Make Linux work inside of Bosch</li>
<li class="fragment"></li>
</ul>

---

### What is going to change?

~~~

### Ansible

<ul>
<li class="fragment">Configuration and management tool</li>
<li class="fragment">Descriptive language</li>
<li class="fragment">Agentless (uses ssh)</li>
<li class="fragment">We will use it locally</li>
<li class="fragment">Will be the only tool to configure osd5</li>
</ul>

~~~

### Unni presenting his work

<ul>
<li class="fragment">Configuration and management tool</li>
<li class="fragment">Descriptive language</li>
<li class="fragment">Agentless (uses ssh)</li>
<li class="fragment">We will use it locally</li>
<li class="fragment">Will be the only tool to configure osd5</li>
</ul>

---

### Feedback

---

### Thanks:)
