# Step 1: Build the app in image 'builder' (multi-stage builds)
FROM node:20 as builder

# Define working directory
WORKDIR /app

# Copy package.json and package-lock.json before other files
# Utilise Docker cache to save re-installing dependencies if unchanged
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy all files
COPY . .

# Build app
RUN npm run build --prod

# Step 2: Serve app with nginx server
FROM nginx:alpine

# Copy over the artifacts from the build step
COPY --from=builder /app/dist/my-angular-app/ /usr/share/nginx/html

# Copy the default nginx.conf provided by tiangolo/node-frontend
COPY ./nginx.conf /etc/nginx/conf.d/default.conf
