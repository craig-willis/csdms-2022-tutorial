# Introduction

*Questions:*
* What is Whole Tale?
* What is a tale?
* What is a recorded run?
* What are Docker and `repo2docker` and why are they used in Whole Tale?

*Objectives:*
* Learn about the Whole Tale project and platform
* Learn what a "tale" is and how it relates to similar research objects
* Learn what Docker and repo2docker are and how they relate to Whole Tale
* Learn about the key features of Whole Tale

### What is Whole Tale?

Whole Tale is an open-source platform for creating and publishing transparent and reproducible computational research artifacts.

Researchers create _tales_ that can be published to research data repositories.

#### What is a "tale"?

A tale is a standards-based research object that combines:
* Data
* Code
* Workflow
* Documentation
* Results
* Information about the computational environment

Tales are intended to be transparent, executable, and verifiable.

Tales are published to external research repositories to obtain a digital object identifier (DOI).

#### What is a digital object identifier or DOI?

A persistent link and globally unique identifier commonly used by research repositories to provide access to published materials (e.g., papers, data, code, etc). They require a commitment from an institution or provider to maintain access to the URL. DOIs are commonly issued by publishers and research repositories. 

Whole Tale enables researchers to publish (or deposit) tales to DOI-issuing research repositories.

#### What is a research (data) repository?

Institutional and data repositories provide a way to preserve and provide access to research materials and artifacts. It is common today for peer-reviewed journals to require authors to deposit data and other computational artifacts in a suitable repository.

Whole Tale integrates with repository platforms including Zenodo, Dataverse, DataONE, and Globus.

### Reproducible computational research 

Communities use different terms to describe conventions and practices for sharing reproducible computational research artifacts. Below are two historical definitions. 

The concept of a _replication data set_ (King, 1995) is widely adopted in the social sciences:

> Replication data sets include all information necessary to replicate 
> empirical results. For quantitative researchers, these might include original data, 
> specialized computer programs, sets of computer program recodes, extracts of existing
> publically available data (or very clear directions for how to obtain exactly the 
> same ones you used), and an explanatory note (usually in the form of a "read-me" file)
> that describes what is included and explains how to reproduce the numerical results 
> in the article.

The concept of a _research compendium_ (Gentleman and Lang, 2004) originated in the statistics community and has been adopted by others:

> "...as both a container for the different elements that make up the
document and its computations (i.e. text, code, data, ...), and as a means
for distributing, managing and updating the collection" for reproducible
research.

Reproducible computational research artifacts are increasingly being deposited or published in research repositories.


#### Activity 1: Exploring a "research compendium"

_Research compendium package for d'Alpoim Guedes and Bocinsky 2018_
* Published research compendium: https://zenodo.org/record/1405073
* Associated Github repository: https://github.com/bocinsky/guedesbocinsky2018


Consider the following:
* The Github repository contains materials to reproduce results reported in a peer-reviewed paper (http://doi.org/10.1126/sciadv.aar4491).
* A specific version of the repository has been archived to Zenodo to obtain a DOI.
* The repository contains a Dockerfile (https://github.com/bocinsky/guedesbocinsky2018/blob/master/Dockerfile) and has an associated Docker image  on DockerHub (https://hub.docker.com/r/bocinsky/guedesbocinsky2018/)

#### What is Docker?

Docker is a popular virtualization ("container") platform that has been widely adopted for the packaging, distribution, and deployment of software -- including scientific software. 

From https://www.docker.com/resources/what-container:

> A container is a standard unit of software that packages up code and all its dependencies so the application runs quickly and reliably from one computing environment to another. A Docker container image is a lightweight, standalone, executable package of software that includes everything needed to run an application: code, runtime, system tools, system libraries and settings... Containers isolate software from its environment and ensure that it works uniformly despite differences for instance between development and staging.

A `Dockerfile` is a simple text file that contains instructions used to build a Docker image.

A Docker registry is a library of pre-built images. Users can `push` or `pull` images from the registry.  For example, https://hub.docker.com.


### Activity 2: Exploring Dockerfiles

Because Whole Tale relies on Docker, we will consider a very brief example.

The following `Dockerfile` can be used to build an image:

```
FROM ubuntu:20.04
RUN apt-get update -y && \
    apt-get install -y python-minimal=3.8.2-0ubuntu2
```

Questions:
* What does this Dockerfile do?
* What is `ubuntu` and what does `20.04` mean?
* Why do you think Whole Tale uses Docker images?

Note:
* The `FROM` instruction specifies the base image, in this case `ubuntu:20.04`
* This is a Long Term Support (LTS) version of the Ubuntu (Linux) operating system
* The `RUN` instruction uses the `apt` package manager to install a specific version of Python
* An image built from these instructions can be run on a variety of operating systems.
* Using Docker, research results can be packaged and archived along with the exact versions of software used in their creation

### What is repo2docker ?

`repo2docker` is part of the Binder platform developed by the  Jupyter community. As suggested by the name, `repo2docker` provides a way to convert a repository (e.g., Github) into a Docker image. If your repository (or local directory) contains some [well-defined and commonly used configuration files](https://repo2docker.readthedocs.io/en/latest/config_files.html), `repo2docker` can be used to build and run a Docker container with the specified software packages installed.  

Takeaway: Users do not need to know how to write Dockerfiles.

### Activity 3: Exploring repo2docker

Look at the list of supported [configuration files](https://repo2docker.readthedocs.io/en/latest/config_files.html)

Question:
* Do you recognize or use any of the configuration files?
* What is the base operating system used on repo2docker generated images?
* What configuration file would you use to create the previous example?

Note:
* `repo2docker` images are based on Ubuntu LTS. Windows is not currently supported by Whole Tale.
* The `apt.txt` file can be used to specify OS-level packages.


## Activity 4: Exploring a replication package

_Replication Data for: Parliamentary Constraints and Long-term Development: Evidence from the Duchy of Württemberg_
* Published replication package: https://doi.org/10.7910/DVN/CZDGR2

Consider the following:
* This "replication package" has been published in conformance with journal policy (see also [AJPS Verification Policy](https://ajps.org/ajps-verification-policy/))
* It contains code, data, and instructions required to reproduce results
* It has been independently verified
* It uses STATA, a commercial software package 

Note:
* Whole Tale extends repo2docker to add support for commercial packages including STATA and MATLAB


## Activity 5: Exploring a tale

Here is an example tale based on the above replication package: https://doi.org/10.5072/zenodo.1059962

Consider the following:
* It contains the same code, data, and instructions as Activity 4
* It has a "recorded run" with associated outputs (figures)
* It can be imported and re-executed in Whole Tale

### What is a "recorded run"?

How do you know that the provided code, data, workflow, and environment were used to obtain a particular result?

A "recorded run" executes a tale workflow in an isolated container, capturing:
* An immutable version of the tale including all output files as well as standard out/error.
* Usage information (memory, CPU, I/O)


## Key points

* Whole Tale is an open-source platform for transparent and reproducible computational research
* Tales are a way to package and publish your research artifacts
* Whole Tale uses Docker to build and distribute container images
* Whole Tale uses repo2docker to simplify the process of creating Docker images
* Whole Tale includes support for commercial software including STATA and MATLAB
* Recorded runs can be used to demonstrate that specific code/data/workflow were used to obtain results


## Next

[Signing in](2-access.md)
