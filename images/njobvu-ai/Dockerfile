FROM node:18

# Install git (needed to clone the repo)
RUN apt-get update && apt-get install -y git && apt-get clean

# Set the working directory inside the container
WORKDIR /app

# Clone the repository
RUN git clone https://github.com/sullichrosu/Njobvu-AI.git .

# Remove unwanted files and directories 
RUN rm -rf /app/.git /app/node_modules /app/logs /app/__pycache__ \
    /app/db_data /app/build /app/*.md /app/*.zip /app/*.tar* \
    /app/docker-compose*.yml /app/.env /app/.vscode /app/.idea \
    /app/*.exe /app/*.bat /app/*.cmd /app/*.lnk /app/*.vbs /app/*.ps1

# Optimize dependencies: Copy package.json first, then install dependencies
COPY ./package*.json ./
RUN npm install

# Copy the rest of the app files (except those ignored by .dockerignore)
COPY . .

# Replace the training config file with the custom one
COPY ./config.json /app/controllers/training/config.json

# Create necessary directories if they don't exist
RUN mkdir -p tmp

# Expose the port for the application
EXPOSE 8080

# Start the application
CMD ["node", "server.js"]
