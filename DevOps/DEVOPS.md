What is DEVOPS ? 

What is the Problem ? / why it is born ? 
--------------------------------------------
DEVOPS born after AGILE. usually there are two departement in IT, it is Operation that have mindset to keep production stable and reliable and usually it means slowing down the new deployment, and Developoment that have mindset to fulfilling business request by pushing new deployment to production. this two opposite mindset slowing down business changes. Business need fast changes to adapt to market condition. That is why DEVOPS born with mindset enabling the business by continously delivering value to customer. 

Old Organization Stucture of dev and ops:
-----------------------------
            |               |
DEV TEAM    |   OPS TEAM    |
            |               |
-----------------------------

What is the solution ? 
--------------------------------------------
The solution is by removing/reducing the wall that separate DEV and OPS Team. but we should understand first, why OPS Team and its mindset able to slowing down the business ?. Because deploy to production will able to disturb stability or reliability or we can say it bring problem to OPS Team. then, how to do deployment but not bring/minimizing the impact ?. by reducing human touch/human error, during development the tasks will be : Req Gathering, Development, Testing, and Deploy. 

We need to reduce the problem during development by 
    1. force the developer to do Unit test, 
    2. and during testing need to have robust testing by do automatic testing for all possibility (automation will consume less time than human for test all possibility), then conduct manual exploratory testing. 
    3. and duing deployment need to have automatic deployment to all environment, automatization of deployment will also make sure to execute the same deployment procedure in all environment, and if there is wrong procedure we will know it in development environment first.

Automate since development, bulld, test, release. it is called as CI (continous integration), and CD (continous Delivery), and if reach deployment it is called CD (Continous Deployment). somehow this DEVOPS aligning with AGILE. 

Implementing devops will also have impact on organization structure ?, and there are around 9 different types of new structure. could be find here : https://web.devopstopologies.com/. one of it is google SRE structure : 

---------------------------------
                |               |
DEV TEAM        |   OPS TEAM    |
        ---------------         |
        |DEVOPS :  SRE|         |
---------------------------------