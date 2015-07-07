Docker + Wordpress
==================

1. Intro to Docker
------------------

### Why use Docker for WordPress development?

 - Mount a local folder inside the container - no messing around with network shares.

| Local filesystem  | Container filesystem |
| ----------------  | -------------------- |
| `~/wordpress_development/plugins` | `/var/www/wp-content/plugins` |

 - Like a VM, but faster, easier and smaller to set up new containers compared to new VMs

 - Consistent development environments across developers (ever had problems where one developer's PHP installation was missing some library? `php_gd` is a common one.)

### VMs vs Docker under the bonnet

A container is similar to a VM in a few ways:
 - The filesystem is isolated
 - Startup and shutdown 'machines' quickly and easily

Containers are more lightweight than VMs:
 - Containers use **much** less disk space
 - Containers start up and shut down extremely quickly
 - Containers are generally more reusable
 - You can include a docker image in your source repository


Compare a VM setup with Docker:
<table>
<tr>
  <td>Virtual Machines</td>
  <td>Docker Containers</td>
</tr>
<tr>
  <td>
    ![VM Diagram](https://www.docker.com/sites/default/files/what-is-docker-diagram.png)
  </td>
  <td>
     ![Container](https://www.docker.com/sites/default/files/what-is-vm-diagram.png)
  </td>
</tr>
</table>


#### VM

#### Container


2. Install Boot2Docker
----------------------
**Linux users can skip this section**

Docker only works inside a Linux environment. Mac and Windows users need to install Boot2Docker. But don't worry, once this is set up, using docker feels the same as using it locally.

3. Install `docker-compose`
---------------------------

4. Create a WordPress Container
-------------------------------

5. Install WP-CLI
-----------------
