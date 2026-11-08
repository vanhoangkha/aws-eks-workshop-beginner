# Getting started with Amazon Elastic Kubernetes Service

> Amazon EKS Workshop for Beginners — Step-by-step Kubernetes on AWS tutorial.

A hands-on workshop from the [AWS First Cloud Journey](https://github.com/vanhoangkha/aws-first-cloud-journey) series, available in English and Vietnamese.

**Read the workshop online:** https://vanhoangkha.github.io/aws-eks-workshop-beginner/

## Overview

This workshop is part of a series of EKS workshops. Here, we provide an overview and help you to get familiar with deploying, configuring, and operating your applications on Kubernetes. With this particular workshop, we aim to provide a better understanding of how to create an EKS cluster, to execute commands, and to deploy some simple workloads on the cluster.

## Workshop contents

1. Introduction
   - Cluster Architecture
   - Pods and Deployments
2. Prerequisites
   - Environment Preparation
   - Creating your Kubernetes Cluster
   - Workshop Structure
3. Getting Started
   - Sample Application
   - Lab Components
   - Microservices on Kubernetes
   - Deploy our first component
   - Other Components
4. Kustomize
5. Helm
6. Clean up

## Prerequisites

- An AWS account with permissions to create the resources used in the labs
- Basic familiarity with the AWS Management Console
- [Hugo](https://gohugo.io/installation/) (extended edition) if you want to run the site locally

## Run locally

```bash
git clone https://github.com/vanhoangkha/aws-eks-workshop-beginner.git
cd aws-eks-workshop-beginner
hugo server -b localhost/EKS-Workshop-1
```

The `-b` (base URL) flag is required for images to load. Then open http://localhost:1313/EKS-Workshop-1/ in your browser.

## Repository structure

| Path | Purpose |
| --- | --- |
| `content/` | Workshop pages (`*.md` English, `*.vi.md` Vietnamese) |
| `static/` | Images and other static assets |
| `layouts/` | Hugo layout overrides |
| `themes/` | Hugo theme |
| `config.toml` | Site configuration |

## Cost and cleanup

The labs create AWS resources that may incur charges. Complete the **Clean up** chapter when you finish to remove them.

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE).
