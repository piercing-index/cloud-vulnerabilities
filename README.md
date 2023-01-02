# The Piercing Index (PI)

When a Public Cloud vulnerability is disclosed, Cloud providers don't assess the CVE Base Score unless customer impact has been demonstrated.

The Cloud customers community need a way to perform such assessment for analyzing the potential impact the vulnerability may have had in their subscriptions and accounts.

PI is a simple methodology for rating the base score of a Public Cloud vulnerability independently from Clod providers.

Like CVE, PI ranges from 0.0 to 10.0:
- LOW vulnerabilities score less than 5.0
- MEDIUM vulnerabilities score between 5.0 and 7.5
- HIGH vulnerabilities score between 7.5 and 9.5
- CRITICAL vunerabilities score more than 9.5


## How to assess Cloud vulnerabilities?

[PiercingIndex.pdf](https://github.com/piercing-index/cloud-vulnerabilities/blob/main/PiercingIndex.pdf) explains how the PI is calculated. Only 8 questions, labelled A1 to A8, must be answered to get a rating.

The AWS and Azure folders contain the detailed individual scores of Cloud vulnerabilities rated so far: files are sorted according the following naming convention:

```
YYYY_MM_name.md
```

YYYY and MM are the year and month of the public diclosure.

In each file, the following components must be mentionned:
- the PI version (currently, it is version 1.5)
- the URL of the vulnerability report
- a Vector String summarizing answers to the 8 questions, it is an easy and portable way to reason about the severity of a vulnerability.
- the PI calculated from that vector.

## Vector String format

The Vector String is directly inspired from the CVSS format.

The exact answers to put into the vector depend whether the vulnerability is cross-tenant or not

### The vulnerability is cross-tenant

Only questions A1,A2,A7 and A8 matter for the PI rating.

The Vector must be formed as such:

```
PI:version.subversion/A1:val_A1/A2:val_A2/A7:val_A7/A8:val_A8
```

### THe vulnerability is not cross tenant


## Revision history

### 1.5 (29 December 22)
Modified PI range to align with CVE range: was 0.0 - 1.0
Now: 0.0 - 10.0

### 1.4 (03 November 22)
Modified A8 weight to account for Lightspin Azure Cloudshell and Orca CosMiss disclosures

### 1.3 (19 July 22)
Modified A3 weigth to account for Azure FabricScape and AWS EKS IAM authentication vulnerability disclosures

### 1.2 (30 May 22)
Modified global weigthing accounting for the data accumulated over the past semester.
