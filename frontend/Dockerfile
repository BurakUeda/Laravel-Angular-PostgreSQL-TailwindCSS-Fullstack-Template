FROM node:22

# Set working directory inside the container
WORKDIR /app

# Install Angular CLI globally
RUN npm install -g @angular/cli

# Copy only package.json and package-lock.json first (for layer caching)
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the app
COPY . .

# Expose Angular dev port
EXPOSE 4200

# Start the dev server
CMD ["npm", "start"]
