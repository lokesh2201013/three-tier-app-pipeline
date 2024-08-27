# Stage 1: Build stage
FROM node:lts-alpine AS build

# Set environment variable for production
ENV NODE_ENV=production

# Set working directory
WORKDIR /usr/src/app

# Copy package files and install dependencies
COPY ["package.json", "package-lock.json*", "npm-shrinkwrap.json*", "./"]
RUN npm install --production --silent

# Stage 2: Production stage
FROM node:lts-alpine

# Set environment variable for production
ENV NODE_ENV=production

# Set working directory
WORKDIR /usr/src/app

# Copy only the node_modules from the build stage
COPY --from=build /usr/src/app/node_modules ./node_modules

# Copy the rest of the application code
COPY . .

# Change ownership to the node user
RUN chown -R node /usr/src/app

# Switch to the non-root user
USER node

# Start the application using npm start
CMD ["npm", "start"]
