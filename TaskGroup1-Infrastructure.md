# Multi-tenant DB Data in rest:

<img width="788" alt="Screenshot 2022-06-28 at 21 18 56" src="https://user-images.githubusercontent.com/20538426/176267242-f5c6dc16-8320-4473-a8b6-3fcd36ce3336.png">

The above diagram shows the abstract understanding of the DB cluster which is shared between environments/teams/bussiness units. Modern day public cloud providers are providing managed services that stores the data with encryption at rest.

### Here we are assuming different scenarios to implement or propose the solution:

1. Data is stored in public cloud with storage services used (Encrypt at rest or serverside encyrption like S3, EBS encryption, KMS etc)
2. we are using the additional method to retrieve data with key value store database like dynamoDB or KMS to store and shared between users.
3. Any Secret management tool to provide access to the Databse like hashicorp vault which is spreaded in namespaces, policies, paths, ,Auth Methods
Secrets Engines, Tokens, Identity entities and groups.


A brief prototyped implementation and encyrption engineering:

1. Here’s what we do.  When the software runs for the first time, it checks to see if the encryption keys are the ones it was born with. If that’s the case, it insists that you restart it as “root” and quits. 
2.  When you do as you’re told, it does this:    Verifies that it is either locked to this hardware, or that this is a first-time run.   If neither is true, it quits, otherwise, you are invited to enter the metadata associated with the admin password.
3.  The hash of the password, encrypted with the keys scattered throughout this executable, is stored in the database.  
4.  If you fail to enter the correct metadata which, as a hacker you will, it quits. After three such failures, it trashes as much of the database as it can, before the hacker notices.   Otherwise, it locks the executable to the machine on which it’s running.
5.  This means that the executable won’t run on any other hardware and, once set, this lock cannot be reset.   Next, it backs up the current values of the arrays holding the encryption key fragments, in memory. 
6.  Then, it generates a new set of random numbers, to fill the arrays.   Next, it changes the concatenation order to a new random order   Finally, it creates a new encryption key, and initialisation vector, using the elements of the new arrays, concatenated in the new random order.



