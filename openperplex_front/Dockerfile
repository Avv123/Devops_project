FROM node:18

WORKDIR /app

# Copy the frontend code
COPY . .

# Install dependencies
RUN npm install

# Expose the frontend port
EXPOSE 3000

# Start the frontend in development mode
CMD ["npm", "run", "dev"]
