# Step one
Read through the README.md file in the YOLO directory & install all dependencies, npm install in both client & backend directories. Run 'npm start' to  test the app on http://localhost:3000/ & start the mongodb service, confirmed this by running the command 'sudo systemctl status mongod', Server listening on port 5000 & Database connected successfully.

 {First error was encountered,'Failed to start mongodb.service: Unit mongodb.service not found.', I had to unintsall current installation completely. I then encountered my second error 'E: Unable to locate package mongodb-org' when I tried to re-install mongodb  which was troubleshooted and resolved, successfully installing mondodb}

# Step Two
Create a Dockerfile for the client dir > create a docker container

# Step Three
Create a Dockerfile for the backend dir > create a docker container

# Step Four
Create docker-compose.yml file

# Step Five
Add product
if the data is persistent

 