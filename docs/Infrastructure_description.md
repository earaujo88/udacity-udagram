Overview

This proects uses AWS services to host the application and it dependets infrasctructure.

Database

A RDS public available will be used fro transactional data. The dabatase must be Postgre 17+

API Hosting

Elasticbeanstalk will used to host the api. Create a environment using nodejs 14+ as a runtime. Make sure the create the proper env variables. Check udagram/set_env.sh for the detailed env variables needed.

Frontend hosting

A public S3 must be configured in order to host the application. Enable S3 to be a static website hosting.