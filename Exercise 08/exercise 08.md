![Altschool Africa Logo](./images/1633989073690.jpg)


# Exercise

## Task:
Create an Ansible Playbook to setup a server with Apache.

The server should be set to the Africa/Lagos Timezone.

Host an index.php file with the following content, as the main file on the server:

```sh
<?php
echo date("F d, Y h:i:s A e", time());
?>
```
## Instruction
Submit the Ansible playbook, the output of systemctl status apache2 after deploying the playbook and a screenshot of the rendered page

## Solution

![systemctl status apache2](./images/apache.png)

![screenshot of rendered page](./images/rendered.png)
