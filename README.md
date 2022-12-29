# The Piercing Index (PI)

When a Public Cloud vulnerability is disclosed, Cloud providers don't assess the CVE Base Score unless customer impact has been demonstrated.

The Cloud customers community need a way to perform such assessment for analyzing the potential impact the vulnerability may have had in their subscriptions and accounts.

PI is a simple methodology for rating the base score of a Public Cloud vulnerability independently from Clod providers.

## Resources

The PDF document explains how the PI is calculated. Only 8 questions, labelled A1 to A8, must be answered to get a rating.

The ratings folder contains the detailed individual scores of AWS and Azure vulnerabilities.


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
