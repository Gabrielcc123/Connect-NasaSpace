FROM node:18-alpine

# Create app directory
WORKDIR /app

ENV NODE_ENV=production

# Install dependencies only for backend
COPY CONTROLLERFINALFINAL/backend/package*.json ./backend/
RUN cd ./backend \
  && npm ci --omit=dev

# Bundle app source
COPY CONTROLLERFINALFINAL/backend ./backend
COPY CONTROLLERFINALFINAL/frontend ./frontend

# Expose and run
WORKDIR /app/backend
ENV PORT=4000
EXPOSE 4000

CMD ["node", "server.js"]


