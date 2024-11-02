# Ansible Tower

![](https://i.imgur.com/waxVImv.png)
### [View all Roadmaps](https://github.com/nholuongut/all-roadmaps) &nbsp;&middot;&nbsp; [Best Practices](https://github.com/nholuongut/all-roadmaps/blob/main/public/best-practices/) &nbsp;&middot;&nbsp; [Questions](https://www.linkedin.com/in/nholuong/)
<br/>

Dockerfile for standalone [Ansible Tower](https://www.ansible.com/tower) 3.x+

# Build
```
docker build --no-cache --squash -t ansible-tower:${TOWER_VERSION} .
```

# Run

Run Ansible Tower with a random port:
```
docker run -d -P --name tower nholuongut/ansible-tower
```

or map to exposed port 443:
```
docker run -d -p 443:443 --name tower nholuongut/ansible-tower
```

To include certificate and license on container creation:
```
docker run -t -d -v ~/certs:/certs -p 443:443 -e SERVER_NAME=localhost  ansible-tower
```

To persist Ansible Tower database, create a data container:
```
docker create -v /var/lib/postgresql/9.4/main --name tower-data nholuongut/ansible-tower /bin/true
docker run -d -p 443:443 --name tower --volumes-from tower-data nholuongut/ansible-tower
```
or use create a Docker Volume on the host:
```
docker run -d -p 443:443 -v pgdata:/var/lib/postgresql/9.4/main --name ansible-tower nholuongut/ansible-tower
```

# Certificates and License

The ansible-tower Docker image uses a generic certificate generated for www.ansible.com by the Ansible Tower setup
program. If you generate your own certificate, it will be copied into /etc/tower by the entrypoint script if a volume
is mapped to /certs in the container, e.g:

* /certs/tower.cert -> /etc/tower/tower.cert
* /certs/tower.key  -> /etc/tower/tower.key

The environment variable SERVER_NAME should match the common name of the generated certificate and will be used to update
the nginx configuration file.

A license file can also be included similar to the certificates by renaming your Ansible Tower license file to **license** and
placing it in your local, mapped volume. The entrypoint script checks for the license file seperately and does not depend
on the certificates.

* /certs/license -> /etc/tower/license

The license file can also be uploaded on first login to the Ansible Tower web interface.

# Login

* URL: **https://localhost**
* Username: **admin**
* Password: **password**

# 🚀 I'm are always open to your feedback.  Please contact as bellow information:
### [Contact ]
* [Name: Nho Luong]
* [Skype](luongutnho_skype)
* [Github](https://github.com/nholuongut/)
* [Linkedin](https://www.linkedin.com/in/nholuong/)
* [Email Address](luongutnho@hotmail.com)
* [PayPal.me](https://www.paypal.com/paypalme/nholuongut)

![](https://i.imgur.com/waxVImv.png)
![](Donate.png)
[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/nholuong)

# License
* Nho Luong (c). All Rights Reserved.🌟