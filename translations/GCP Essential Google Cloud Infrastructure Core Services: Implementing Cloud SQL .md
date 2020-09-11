## Course: Essential Google Cloud Infrastructure: Core Services

# LAB:Implementing Cloud SQL

## Objectives:

In this lab, you learn how to perform the following tasks:

-   Create a Cloud SQL database

-   Configure a virtual machine to run a proxy

-   Create a connection between an application and Cloud SQL

-   Connect an application to Cloud SQL using Private IP address

## Steps:

1.  Create a Cloud SQL database
            gcloud beta sql instances create "wordpress-db" --password "root@" -- region "us-central1" --db-version "MySQL 5.7" 

            gcloud config set instance/zone "Any" -- select "db-n1-standard-1"



2.Configure a proxy on a virtual machine

## steps:
   - use the ssh command line to open command prompt on wordpress-europe-proxy

        ssh wordpress-europe-proxy

   -  Download the Cloud SQL Proxy and make it executable
        wget https://dl.google.com/cloudsql/cloud_sql_proxy.linux.amd64 -O cloud_sql_proxy && chmod +x cloud_sql_proxy

   - Replacing [SQL_CONNECTION_NAME] with the unique name
         gcloud create  "SQL_CONNECTION_wordpress" 

   -  export the connection  
          export SQL_CONNECTION=[SQL_CONNECTION_wordpress]

   - verify that the environment variable is set
           echo $SQL_CONNECTION

   - activate the proxy connection to your Cloud SQL database 
           ./cloud_sql_proxy -instances=$SQL_CONNECTION=tcp:3306 

           Result:

           127.0.0.1:3306 (localhost)  is the proxy that connects securely to your Cloud SQL over a secure tunnel using the external IP address of the machine

 3. Connect an application to the Cloud SQL instance

    -      curl -H 


   - To find the external IP address of your virtual machine

           http://169.254.169.254/computeMetadata/v1/instance/network-interfaces/0/access-configs/0/external-ip && echo
   -  Run the installation to instantiate Wordpress and its database in your Cloud SQL

   -  Past the  proxy IP address on your browse 127.0.0.1

    Result:

    Hello world!


    Welcome to WordPress. This is your post. Edit or delete it, then start writing!





