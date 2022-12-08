---
title: 'BioHackEU22 Report for Project 16: Make your own or favourite software available on your cluster with EasyBuild/EESSI'
title_short: 'BioHackEU22 #16: easybuild-eessi'
tags:
  - Software installation framework
  - Workflows
  - Scientific software
authors:
  - name: Sébastien Moretti
    orcid: 0000-0003-3947-488X
    affiliation: 1
  - name: Kenneth Hoste
    orcid: 0000-0001-8034-648X
    affiliation: 2
  - name: Alan O’Cais
    orcid: 0000-0002-8254-8752
    affiliation: 3
  - name: Jurij Pečar
    orcid: 0000-0002-6096-3808
    affiliation: 4
  - name: Elisabeth Ortega
    orcid: 0000-0001-5410-5375
    affiliation: 5
  - name: Anthony Fullam
    orcid: 0000-0002-0884-8124
    affiliation: 4
affiliations:
  - name: Vital-IT group, SIB Swiss Institute of Bioinformatics, Lausanne, CH
    index: 1
  - name: Dept of Information and Communication Technology, Ghent University, Ghent, BE
    index: 2
  - name: Centre Européen de Calcul Atomique et Moléculaire (CECAM), EPFL, Lausanne, CH
    index: 3
  - name: EMBL, Heidelberg, DE
    index: 4
  - name: HPCNow! Barcelona, Barcelona, ES
    index: 5
date: 8 November 2022
cito-bibliography: paper.bib
event: BH22EU
biohackathon_name: "BioHackathon Europe 2022"
biohackathon_url:   "https://biohackathon-europe.org"
biohackathon_location: "Paris, France, 2022"
group: Project 16
# URL to project git repo --- should contain the actual paper.md:
git_url: https://github.com/elixir-europe/biohackathon-projects-2022/tree/main/16
# This is the short authors description that is used at the
# bottom of the generated paper (typically the first two authors):
authors_short: Sébastien Moretti & Kenneth Hoste \emph{et al.}
---


# Introduction

As part of the BioHackathon Europe 2022, we here report the outcomes of the Project #16: **Make your own or favourite software available on your cluster with EasyBuild/EESSI**.

![EasyBuild logo](./easybuild_logo400.png)  ![EESSI logo](./EESSI_logo400.png)

The main goals of the project were to introduce users to [EasyBuild](https://easybuild.io/) and [EESSI](https://www.eessi-hpc.org/), to port new software to EasyBuild/EESSI (e.g., the participant’s own or favourite software) - thereby making it available and discoverable to the entire EasyBuild community -, and to convert a Nextflow pipeline into an EESSI pipeline. In parallel we started to build bridges between EESSI and Galaxy to make the scientific software more accessible to researchers in the domain.


## What are EasyBuild and EESI?

EasyBuild is a community effort to develop a software build and installation framework that allows you to manage (scientific) software on High Performance Computing (HPC) systems in an efficient way. As its name suggests, EasyBuild makes software installation easy by automating builds, making previous builds reproducible, resolving dependencies, and retaining logs for traceability. It is also one of the components of the **European Environment for Scientific Software Installations** (EESSI), a collaboration between different European HPC sites and industry partners, with the common goal to set up a shared repository of scientific software installations that can be used on a variety of operating systems and computer architectures. It can be applied in a full size HPC cluster, a cloud environment, a container or a personal workstation.

EasyBuild is the software layer component of EESSI.


## EasyBuild and EESSI in life sciences

With the deluge of data in the genomics field (e.g., clinical data) and the concomitant development of new technologies, the number of data analysis software has exploded in recent years. The fields of bioinformatics and cheminformatics follow this same trend with ever more developments to optimize and parallelize analyses. The bioinformatics field is now the main provider of new software in EasyBuild. Developers of those tools are not always professional developers, and they do therefore not always follow best practices when releasing their software. As a result, many tools are complicated to install, making them ideal candidates for porting their installation to EasyBuild so that they become more easily accessible to end users.


# Materials

## New software to port to EasyBuild
Based on feedbacks from BioHackathon users, as well as on BioHackathon project topics, some software of the following categories will be added or updated in EasyBuild:
- Galaxy/Workflow
- Systems Biology
- Cheminformatics
- Phylogeny/Orthology

## The Nextflow pipeline to convert to an EESSI pipeline
One of our users works in metagenomics and is interested by the [nf-core/mag](https://nf-co.re/mag) pipeline: **Assembly and binning of metagenomes**.

**nf-core/mag** is a "bioinformatics best-practise analysis pipeline for assembly, binning and annotation of metagenomes". It is composed of about 28 different tools. This complicated pipeline was chosen to illustrate how easy pipelines can be deployed in an optimised version with EESSI.

Missing tools have to be added in EasyBuild, and some tools already in EasyBuild may have to be updated.


# Results

## Introduce EasyBuild and EESSI
During the BioHackathon, EasyBuild and EESSI were presented to different users, with different backgrounds.

## Port new software to EasyBuild
During the BioHackathon the following new tools were added in EasyBuild:
- Galaxy/Workflow tools: [cwltool](https://github.com/common-workflow-language/cwltool)
- Systems Biology tools: [python-libsbml](https://pypi.org/project/python-libsbml/) and [COBRApy](https://opencobra.github.io/cobrapy/)
- Cheminformatics tools: [Chemaxon_marvin](https://chemaxon.com/)
- Phylogeny/Orthology tools: [Godon](https://bitbucket.org/Davydov/godon) and [InParanoid](https://bitbucket.org/sonnhammergroup/inparanoid/)

[Nextflow](https://www.nextflow.io/)(Galaxy/Workflow) required for the pipeline conversion to EESSI was updated to the last version.

So, **7** pull requests!

[toil](https://github.com/DataBiosphere/toil)(Galaxy/Workflow) deployment in EasyBuild is almost complete, waiting for a fix from the toil main developer.

Those tool categories will continue to have particular attentions and be extended in EasyBuild.


## Convert a Nextflow pipeline to EESSI

### Software side
As mentioned previously [Nextflow](https://www.nextflow.io/)(Galaxy/Workflow) was first updated in EasyBuild, and added in the base configuration of EESSI.

Tools from the **nf-core/mag** pipeline not available in EasyBuild were added:
- [NanoLyse](https://github.com/wdecoster/nanolyse)
- [PyDamage](https://github.com/maxibor/pydamage)
- [CAT-BAT](https://github.com/dutilh/CAT)

Some other tools of the pipeline were version- and/or toolchain-updated.

With their requirements, overall, it corresponds to about **20** pull requests, i.e., about **27** software.

An extra pull request was done to bundle the whole pipeline tool list into a single entry point for EESSI.

See pull request details [here](https://github.com/easybuilders/easybuild-easyconfigs/issues?q=label%3ABioHack2022)

### EESSI deployment side
On the EESSI deployment side, a pull request was done to add the pipeline in the EESSI pilot script.

Nevertheless, several issues came out:

- The pipeline was tested in a cloud environment with different architectures. Some of the pipeline tools do not compile easily on some of these architectures.
- Some tools try to force some library usage. This has to be fixed upstream.
- Due to the large number of tools in the pipeline, the build in EESSI for the future deployments takes a lot of time and space.
- It looks the original pipeline - running with containers - has also issues and cannot be run as is.

See pull requests details [here](https://github.com/EESSI/software-layer/issues?q=label%3ABioHack2022)

We will continue to work on the issues, and try to complete the EESSI deployment of the **nf-core/mag** pipeline in the coming weeks.


# Discussion

...

## Acknowledgements
We would like to acknowledge all users of the BioHackathon for fruitful interactions and advices, as well as the ELIXIR BioHackathon organization team for this great event.

## Useful links

### Getting started and Slack links

- Getting started with EasyBuild: https://docs.easybuild.io/
- Getting started with EESSI: https://eessi.github.io/docs/
- EasyBuild Slack channel: https://easybuild.io/join-slack
- EESSI Slack channel: https://www.eessi-hpc.org/slack-channel/

### Other links

- EasyBuild homepage: https://easybuild.io/
- EasyBuild community: https://github.com/easybuilders
- EasyBuild last presentations: https://www.youtube.com/c/easybuilders
- EESSI homepage: https://www.eessi-hpc.org/
- EESSI at GitHub: https://github.com/EESSI
- Introductory talk on EESSI:
  - https://archive.fosdem.org/2021/schedule/event/eessi
  - https://eessi.github.io/docs/meetings/2022-09-amsterdam/EESSI-community-meeting-2022.09-001-introduction-to-EESSI.pdf

## References

1. EESSI [@citesAsAuthority:EESSI2022]
