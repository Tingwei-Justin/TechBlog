## Comparing Nginx vs Apache

- Similarities

  - Fre and open-source software
  - comminity of users reviewing the code
  - added functionality through dynamic modules
  - proxy servers
  - Event-based processing for large numbers of connections (both efficiently handle a large number of simultaneous connections)
    - in the past version of apache, each connection is handled by a process worker (require additional resources for each connection => consume all server resources with heavy load)
    - New apache is event-based processing

- Differences

  | Apache                                               | NGINIX                                         |
  | ---------------------------------------------------- | ---------------------------------------------- |
  | Configuration: XML syntax                            | Configuration: C-like syntax                   |
  | Distributed .htaccess files                          | centralized location blocks                    |
  | Dynamic content is natively processed with modules   | Dynamic content requires external processing   |
  | static content is less efficient                     | static content is more efficient               |
  | caching and load balancing capabilities with modules | native caching and load balancing capabilities |

  

- why choose Ngnix?

  - Its popularity growing and very active community. (lots of developers swith to nginx from apache)
  - Efficient and consistent performance under heavy load (e.g. limited cpu, limited RAM)
  - It's easier to configure

  

- create a vm with vagrant

  - Vagrant up
  - vagrant ssh
  - Vagrant halt : stop the VM
  - Vagrant destory



### Configure NGNIX

`sudo apt update`

`sudp apt upgrade`

`sudo apt install nginx`

Confirm with ngnix install successfully`nginx -v`

`systemctl status nginx`

`systemctl start nginx`

`systemctl stop nginx`

`systemctl reload nginx`



The main configuration file is `/etc/nginx/nginx.conf`

These store server configuration file

`conf.d`

`sites-available`

`sites-enabled`



`nginx -h`: help command of nginx

`nginx -t`: we can test before reload the config.  



### nginx.conf

Two useful way to store configuration

- use `/etc/nginx/conf.d` (more strightforword and easy to maintain)
- use `/etc/nginx/sites-enabled/`

在更改nginx config之前记得使用`nginx -t`测试一下

没有问题的话再执行 `systemctl nginx reload`