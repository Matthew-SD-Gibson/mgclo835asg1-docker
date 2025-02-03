# Use localhost to connect to EC2 instance via SSH
ssh -i mgibson13-asgn1 <instance public ip>

# Export ECR repository into EC2 instance
export ECR=<ECR repsorirtory URL>

# Create local database docker
docker run -d --name my_db --network my_network -e MYSQL_ROOT_PASSWORD=password $ECR:my_db

# Create application docker with each respective color and port
docker run -dt --name my_app-blue --network my_network -p 8081:8080  -e DBHOST=172.18.0.2 -e DBPORT=3306 -e  DBUSER=root -e DBPWD=password  -e APP_COLOR="blue" $ECR:my_app

docker run -dt --name my_app-pink --network my_network -p 8082:8080  -e DBHOST=172.18.0.2 -e DBPORT=3306 -e  DBUSER=root -e DBPWD=password  -e APP_COLOR="pink" $ECR:my_app

docker run -dt --name my_app-green --network my_network -p 8083:8080  -e DBHOST=172.18.0.2 -e DBPORT=3306 -e  DBUSER=root -e DBPWD=password  -e APP_COLOR="green" $ECR:my_app
