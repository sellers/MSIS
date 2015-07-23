# DevOps example with cloud-init
### This is a basic example of the kind of work I have done

* `deploy.py`:  this is the management tool to launch and instance in EC2 

* `*.yaml` :  these are jinja2 templated files that send userdata to EC2 (cloud-init)
   *  flask-nginx-redis.yaml is a three-tier architecture of flask+nginx+redis

* `setup_virtual.sh` : this is a script that sets up the virtualenv for flask/python for 
the app - it's invocated by cloud-init

* `pt.py`: this is the web app (flask), shows visitors

#### Requirements:
1. you need to have an AWS account to use
2. you need to have python with boto support enabled
3. you need to have /etc/boto.cfg or similar setup with key/secret for AWS acct.
4. you need to have an AWS keypair setup and know the name of it

#### Purpose:
To complete the following:

1. start an ec2 instnace that deploys a flask+nginx+redis solution
2. deploy a flask app that will test nginx+flask+redis
3. setup ssh login using defined keys

#### Usage:
(--help will show command usage for deploy.py)
1. make sure you have a ec2 account to use (and a .boto or /etc/boto.cfg file setup with the info)
2. start the 3-tier app: `./deploy.py -t flask-nginx-redis.yaml -n my-three-tier 
3. visit http://\<ip.of.step2.host\> and see the flask app respond, click link and see redis data of visitor info
4. when done - you can use `./deploy.py --halt <instance id> ...` to halt instance(s)
