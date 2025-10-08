Version: 1.6.1

Note that all versions are backward compatible.

# How to calculate the Piercing Index?

Calculating the PI is simple! Only a few questions, labelled A1 to A8, need to be answered.

If the vulnerability is X-tenant, only 4 questions must be answered: A1, A2, A7, A8. 

Otherwise, 6 questions must be answered: A3, A4, A5, A6, A7, A8.

Then we just need to sum the decimal logarithm of all relevant answers and divide by the Max score:

<p align="center"><img width="15%" align="center" src="https://github.com/piercing-index/cloud-vulnerabilities/blob/main/pi_formula.PNG" class="center"></p>

Max=10*log(20x1.1x1.21x1.1x1.1x1.1x1.1) = 1.55 approximately


# X-tenant boundary violation (questions A1, A2)

Is another customer’s data plane accessible within the vulnerable service boundary?
```
Yes, production____________________________________________________________A1 = 20
Yes, non production________________________________________________________A1 = 10
No_________________________________________________________________________A1 = 1
```

Is another customer’s control plane accessible within the vulnerable service boundary?
```
Yes________________________________________________________________________A1 = A1  * 1.1
No_________________________________________________________________________A1 = A1 * 1
```

Is the data or control plane of another service accessible within the vulnerable service boundary?
```
Yes, either the data OR the control plane__________________________________A2 = 1.1
Yes, both data AND control planes__________________________________________A2 = 1.1 * 1.1 = 1.21 
No, the vulnerability is not X-service_____________________________________A2 = 1
```

# Same-tenant vulnerability (questions A3, A4, A5, A6)
Is this same-tenant vulnerability a X-service boundary violation?
```
No, but it permits X-plane boundary violation (data / control planes)______A3 = 1.05
No, and it does not permit a X-plane boundary violation____________________A3 = 1
Yes , it is X-service boundary violation___________________________________A3 = 1.1
```

Does the vulnerability allow illegitimate read access?
```
Yes, to the control or data plane of another service_______________________A4 = 1.05
Yes, to the control or data plane of this service only_____________________A4 = 1.05
No_________________________________________________________________________A4 = 1
```

Does the vulnerability allow illegitimate write access?
```
Yes, to the control or data plane of another service_______________________A5 = 1.05
Yes, to the control or data plane of this service only_____________________A5 = 1.05
No_________________________________________________________________________A5 = 1
```

What is the maximum scope elevation granted by this vulnerability?
```
Whole tenant/organization__________________________________________________A6 = 8
Subscription/account_______________________________________________________A6 = 6
Resource group_____________________________________________________________A6 = 3
Resource __________________________________________________________________A6 = 2.3
```

# Common questions (A7, A9)
What is the complexity of exploitation?
```
Fully disclosed____________________________________________________________A7 = 1.1
Partially disclosed – key elements removed_________________________________A7 = 1
Undisclosed________________________________________________________________A7 = 0.9
```
Does it require some insider help to trigger?
```
Yes, data exfiltration (e.g.: a random ID)_________________________________A8 = 0.7
Yes, user intervention (e.g.: phishing)____________________________________A8 = 0.9
No, but bruteforceable (e.g.: a repo name)_________________________________A8 = 1.0
No_________________________________________________________________________A8 = 1.1
```
The last question is reserved for future use, it should be set to 1 by default:
```
___________________________________________________________________________A9 = 1.1
Default value______________________________________________________________A9 = 1
```

# Examples

## X-Tenant vulnerability
Let’s suppose an AWS X-tenant vulnerability impacts read access to the data plane of one Cloud service. (A1=20 ,A2  = 1.1). 
The exploit has not been disclosed (A7=0.9).
User intervention is not required and no extra secret is necessary (A8=1.1). 

PI =10 * log⁡(20 * 1.1 * 0.9 * 1.1)/MAX  = 8.6

In this example, the piercing index is 8.6. It falls into the red category (ranging between 7.5 and 9.5).

## Minimum score of the PI

What is the minimum score a vulnerability can get? This happens in a same-tenant vulnerability (A3=1) without ilegitimate access (A4=1 and A5=1) with a max elevation scope at the resource level (A6=2.3), undisclosed (A7=0.9), requires data exfiltration (A8=0.7)  

PI =10* log(0.9 * 0.7 * 2.3)/MAX = 1.03



