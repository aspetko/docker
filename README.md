# docker-glassfish-4.1.1 image
GlassFish is an open-source application server project started by Sun Microsystems for the Java EE platform. After Oracle Corporation bought Sun Microsystems, Oracle continued the work on Glassfish.

Thank you Oracle for keeping a great product alive. I have seen to many times a great product beeing discontinued for various reasons. But this is here not the case.

GlassFish is and was the reference implementation of Java EE.

By executing the docker image you agree to the "Oracle Binary Code License Agreement for Java", because the image overwrite the header information to download the required software. If you do not agree, do not use this image!

In this image is the latest (as of today) version of:
* Java 1.8 update 92 (Update from 30th of April 2016) 
* Glassfish 4.1.1
included.

Under the subdirectory 
* web is the web profile and 
* full you find the full Java EE profile.

## Building the container
1. Clone the GitHub repository: 

      
      $ git clone https://github.com/aspetko/docker-glassfish-4.1.1.git
      
2. Change into the correct directory


    $ cd docker-glassfish-4.1.1/full for the full profile 

or
   
 
    $ cd docker-glassfish-4.1.1/web for the web profile
3. Execute a Docker build command 


      $ sudo docker build -t glassfish_full_profile:4.1.1 . 

or
    
     $ sudo docker build -t glassfish_web_profile:4.1.1 . 
or tag it with whatever you prefer.
## Domain, Username and Password
The image is setting up the 
* Default Domain: domain1
* Username: admin
* Password: glassfish

# Starting GlassFish on Docker
To run the image simply type:

    $ sudo docker run -d -p 4848:4848 -p 8080:8080 -p 8181:8181 glassfish_full_ofile:4.1.1
         5059e9a6b95ad47b5ed92a07bfc73e7857d8d1989b1641363578cc59e1f69f63

    $ sudo docker ps | grep glassfish

         5059e9a6b95a        glassfish_full_profile:4.1.1 ...
    $ sudo docker logs -f 5059e9a6b95a

The last command will output the stdout to the console. Because of the -f flag it wont stop.  

All default ports are exposed, by the image:

* the admin console: 4848 
* the HTTP access: 8080
* the HTTPS access: 8181

Open 

    http(s)://\[ip of the docker machine\]:4848

to open the administrative console.
 
## Deploying Java EE Applications
You can use either:

* the administrative console on port 4848 or
* the GlassFish Maven Plugin. 

## Other material
[Soon]: You can find on my business related channel on youtube a video about this container was build and an running example. 

