####### BUILD STAGE #######
FROM node:lts-alpine AS build

WORKDIR /app

COPY package*.json ./
COPY backend/package.json ./backend/

RUN npm ci --workspace=backend

COPY . .

RUN npm run build:backend

# ####### DEVELOPMENT STAGE #######
# FROM node:lts-alpine AS development

# WORKDIR /app

# COPY package*.json ./
# COPY backend/package*.json ./backend/

# RUN npm ci --workspace=backend

# COPY . .

# EXPOSE 5000

# CMD ["npm", "run", "dev:backend"]
# CMD ["npm", "run", "dev", "--workspace=backend"]

####### PRODUCTION STAGE #######
FROM node:lts-alpine AS production

WORKDIR /app

COPY package*.json ./
COPY backend/package.json ./backend/

RUN npm ci --workspace=backend --omit=dev

COPY --from=build /app/backend/dist ./backend/dist

WORKDIR /app/backend

CMD ["node", "dist/server.js"]