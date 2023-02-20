Version: 1.5

#How to calculate the Piercing Index?

Calculating the PI is simple! Only a few questions, labelled A1 to A8, need to be answered.

If the vulnerability is X-tenant, only 4 questions must be answered: A1, A2, A7, A8. 

Otherwise, 6 questions must be answered: A3, A4, A5, A6, A7, A8.

Then we just need to sum the decimal logarithm of all relevant answers and divide by the Max score:

<p align="center"><img width="15%" align="center" src="https://github.com/piercing-index/cloud-vulnerabilities/blob/main/pi_formula.PNG" class="center"></p>

Max=log(20x1.1x1.21x1.1x1.1x1.1) = 1.55 approximately



# X-tenant boundary violation (questions A1, A3, A7, A8)

Is another customer’s data plane accessible within the vulnerable service boundary?
```
Yes___________________A1 = 20
No____________________A1 = 1
```

Is another customer’s control plane accessible within the vulnerable service boundary?
```
Yes____________________A1 = A1  * 1.1
No_____________________A1 = A1 * 1
```

Is the data or control plane of another service accessible within the vulnerable service boundary?
```
Yes, either the data OR the control plane__A2 = 1.1
Yes, both data AND control planes__________A2 = 1.1 * 1.1 = 1.21 
No, the vulnerability is not X-service_____A2 = 1
```
