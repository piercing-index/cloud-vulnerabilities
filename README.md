# The Piercing Index (PI)

![Alt text](https://github.com/piercing-index/cloud-vulnerabilities/blob/main/PiercingIndex.png)

When a Public Cloud vulnerability is disclosed, Cloud providers don't assess the CVE Base Score unless customer impact has been demonstrated.

The Cloud customers community need a way to perform such assessment for analyzing the potential impact the vulnerability may have had in their subscriptions and accounts.

PI is a simple methodology for rating the base (i.e. unmitigated) score of a Public Cloud vulnerability independently from Clod providers.

## What is the meaning of a PI rating?

Like CVE, PI ranges from 0.0 to 10.0:
- LOW vulnerabilities score less than 5.0
- MEDIUM vulnerabilities score between 5.0 and 7.5
- HIGH vulnerabilities score between 7.5 and 9.5
- CRITICAL vunerabilities score more than 9.5

### On the exponential scale

From long standing experience in risks assessments, I have noticed that the key questions to ask when conducting an assessment depend on the **order of magnitude** of the risk. Each order of magnitude must address a limited set of concerns, and all that is below that order is meaningless.

For Cloud vulnerabilities, I have defined several orders of magnitude, the two major ones being cross-tenant and same-tenant.

So in the end we have only very few questions to answer, this makes the assessment pretty simple and straightforward: the orders of magnitude behave like filters hat show you only relevant questions.

To keep the PI rating within the 0.0 -> 10.0 range, a logarithm is being used.

## Where may I find the rating of a given vulnerability?

The AWS and Azure folders contain the detailed individual scores of Cloud vulnerabilities rated so far: files are sorted according the following naming convention:

```
YYYY_MM_name.md
```

YYYY and MM are the year and month of the public diclosure.

## How to contribute?

### I want to add a new assessment, or to edit an existing assessment

Open a pull request and I will review it for merge into this repository. 
Please note that, for now, only Azure and AWS providers are supported. We plan to add more in the future.

### I want to request for a change in the calculation method

Calculations are versioned. The current version is 1.5

To propose any change, make a pull request to the markdown file called [Specifications](https://github.com/piercing-index/cloud-vulnerabilities/blob/main/Specifications.md). Don't forget to add detailed explanations in comments.

## How to assess Cloud vulnerabilities?

[PiercingIndex.pdf](https://github.com/piercing-index/cloud-vulnerabilities/blob/main/PiercingIndex.pdf) explains how the PI is calculated. Only 8 questions, labelled A1 to A8, must be answered to get a rating.

In each indivudual vulnerability file, the following components must be mentionned:
- the PI version (currently, it is version 1.5)
- the URL of the vulnerability report
- a traceback to cloudvulndb.org assessment (a YAML file)
- a vector string summarizing answers to the 8 questions, it is an easy and portable way to reason about the severity of a vulnerability.
- the PI calculated from that vector.

## Quick guide to Understand the Vector String format

The Vector String is directly inspired from the CVSS format.

As explained in the PDF documentation, the exact answers to put into the vector depend whether the vulnerability is cross-tenant or not

### The vulnerability is cross-tenant

Only questions A1,A2,A7 and A8 matter for the PI rating: questions A1 and A2 are purpose-built for cross-tenant vulnerabilities, while questions A7 and A8 are miscellaneous questions applicable to all vulnerabilities.

For a cross-tenant vulnerability, the vector must be formed as such:

```
PI:version.subversion/A1:val_A1/A2:val_A2/A7:val_A7/A8:val_A8
```

The AWS ECR cross-tenant vulnerability, for example, is attributed the following vector in PI version 1.5:

```
PI:1.5/A1:20/A2:1/A7:1.1/A8:1.1
```

### The vulnerability is not cross tenant


In this case, only questions A3 to A8 matter: questions A3 through A6 pertain to same-tenant vulnerabilities, while A7 and A8 apply to all vulnerabilities.


For same cross-tenant vulnerability, the vector must be formed as such:

```
PI:version.subversion/A3:val_A3/A4:val_A4/A5:val_A5/A6:val_A6/A7:val_A7/A8:val_A8
```

For example, here is the vector of the Azure logic App same-tenant vulnerability in PI version 1.4:

```
PI:1.4/A3:1.05/A4:1.05/A5:1.05/A6:8/A7:1.1/A8:0.9
```

## Revision history
### 1.6 (24 February 25)
Modify A1 to distinguish between non-production and production services in the data plane. Non-production services have a coefficient of 10, whereas production have 20.
(Before, we used to have one single value when A1 was ticked, it was 20).

### 1.5 (29 December 22)
Modified PI range to align with CVE range: was 0.0 - 1.0
Now: 0.0 - 10.0

### 1.4 (03 November 22)
Modified A8 weight to account for Lightspin Azure Cloudshell and Orca CosMiss disclosures

### 1.3 (19 July 22)
Modified A3 weigth to account for Azure FabricScape and AWS EKS IAM authentication vulnerability disclosures

### 1.2 (30 May 22)
Modified global weigthing accounting for the data accumulated over the past semester.

## License information

[![License: CC BY-NC-SA 4.0](https://img.shields.io/badge/License-CC%20BY--NC--SA%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc-sa/4.0/)
