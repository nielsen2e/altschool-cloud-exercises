![AltSchool Africa Logo](./images/1633989073690.jpg)


# Exercise:

Create 3 groups – admin, support & engineering and add the admin group to sudoers. 
Create a user in each of the groups. 
Generate SSH keys for the user in the admin group

## Instruction:

Submit the contents of /etc/passwd, /etc/group, /etc/sudoers.

## Solution
<ol>
   <li>

   ```sh
  sudo tail /etc/passwd
  ``` 

  ![users](./images/users.png)
   </li>

   <li>
   
   ```sh
  sudo tail /etc/group
  ``` 

  ![groups](./images/groups.png)
   </li>

   <li>
   
   ```sh
  sudo cat /etc/sudoers
  ``` 

  ![sudoers](./images/sudoers.png)
   </li>


</ol>