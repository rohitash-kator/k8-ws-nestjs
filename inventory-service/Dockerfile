# Use official Node.js image as the base
FROM node:18-slim AS build

# Set the working directory in the container
WORKDIR /app

# Copy package.json and package-lock.json to install dependencies
COPY package.json package-lock.json ./

# Install dependencies
RUN npm install
RUN npm install g nest

# Copy the rest of the application files (including the TypeScript code)
COPY . ./

# Build the TypeScript code
RUN npm run build

# Production Stage
FROM node:18-slim AS production

# Set the working directory for production
WORKDIR /app

# # Copy the build files from the build stage
# COPY --from=build /app/dist /app/dist

# # Copy node_modules from the build stage
# COPY --from=build /app/node_modules /app/node_modules

# Copy package.json and .env file from the build stage
COPY --from=build /app/package.json /app/package.json
COPY --from=build /app/.env /app/.env

# Expose the service port
EXPOSE 3000

# Command to run the service
CMD ["npm", "run", "start"]
