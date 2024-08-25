FROM node:14.16.0-alpine3.13

# Create a group and user for the app
RUN addgroup app && adduser -S -G app app
USER app

# Set the working directory
WORKDIR /app

# Copy package.json and install dependencies
COPY package*.json ./
RUN npm install

# Copy the rest of the application files
COPY . .

# Expose the application port
EXPOSE 3001

# Set the default command to run your entrypoint script
CMD ["/app/docker-entrypoint.sh"]
