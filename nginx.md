## Comparing Nginx vs Apache

- Similarities

  - Free and open-source software
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

The /etc/nginx directory holds the configuration for the entire nginx installation. Inside this directory, you’ll find the files that control the way the web server runs along with the files that define the web sites being served.

/etc/nginx/nginx.conf is the main configuration file for NGINX. It contains configuration for the main server program and can load other configurations as well.



Two useful way to store configuration

- use `/etc/nginx/conf.d` (more strightforword and easy to maintain)
- use `/etc/nginx/sites-enabled/`

在更改nginx config之前记得使用`nginx -t`测试一下

没有问题的话再执行 `systemctl nginx reload`



The server_name directive lets NGINX know which sites a server configuration applies to. Otherwise, if NGINX were serving multiple sites from the same IP address, the wrong content might be served.

### niginx logs

- `access_log /var/log/nginx/access.log`
- `error_log /var/log/nginx/error.log`

we can define our individual log file and monitor each site seperately.

Default logging is configured in the http context and can be overridden in the server and location contexts.

### common troubleshoot

1. use `nginx -t` to test before reload
2. Check typo
3. Check nginx status `systemctl status nginx`
4. verify the ports
   1. `sudo lsof -P -n -i :80 -i :443 | grep LISTEN `
   2. `sudo netstat -plan | grep nginx`

5. tail the logs `tail -f /var/logs/nginx/*.log`
6. 





### Nginx security

1. Keep your operatiing system and software patched and up-to-date
2. Restrict access where possible
3. use passwords to protect sensiteve information
4. use ssl to protect transmissions and identify your site.



configure allow and deny directives:

```
example:

location /appointments/ {
	allow 192.168.0.0/24;
	allow 10.0.0.0/8;
	deny all;
}
```



create a custom default 403, 404 page





### Reverse Proxies and Load Balancers

They are very similar to use, If there is only one server in an upstream, NGINX will operate as a reverse proxy. If more than one server is in an upstream, NGINX will operate as a load balancer.

Load Balancing directives:

- Round Robin: -
- Least Connections: least_conn
- IP Hash: ip_hash
- All: weight

NGINX is great at simplifying things that might be harder to implement in other technologies like SSL termination and logging. NGINX proxies are also good for accelerating the response from backend servers by caching content.



Upstreams are defined in the HTTP context. This is useful so that one upstream can be defined and then reused by multiple servers also defined in the HTTP context.



The weight directive is used to influence load balancing methods. Since each server is considered evenly in the round robin method and by connections in the least connections method, a weight can be applied to a server to give it a higher preference.