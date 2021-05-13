# build docker image

docker build -t node-server .

# tag docker name

docker tag node-server fabxc/nodejs_app

# push image to your docker repository

docker push fabxc/nodejs_app

# 1. Deploy the application
# 2. Deploy the prometheus operator
# 3. Deploy the prometheus
