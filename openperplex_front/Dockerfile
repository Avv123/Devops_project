FROM node:18

# Set the working directory in the container
WORKDIR /app

# Copy package.json and package-lock.json (if available) to the working directory
COPY package*.json ./

# Install dependencies, including Vite
RUN npm install

# Install Vite globally
RUN npm install -g vite

# Copy the rest of your application files to the container
COPY . .

# Expose the port that Vite will run on
EXPOSE 3000

# Start the development server using the globally installed Vite
CMD ["vite"]
