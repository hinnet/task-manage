####### BUILD STAGE #######
FROM node:lts-alpine AS build

WORKDIR /app

COPY package*.json ./
COPY backend/package.json ./backend/

RUN npm ci --workspace=backend

COPY . .

RUN npm run build:backend

# ####### DEVELOPMENT STAGE #######
# FROM build AS development

# CMD ["npm", "run", "dev:backend"]

####### PRODUCTION STAGE #######
FROM node:lts-alpine AS production

WORKDIR /app

COPY package*.json ./
COPY backend/package.json ./backend/

RUN npm ci --workspace=backend --omit=dev

COPY --from=build /app/backend/dist ./backend/dist

CMD ["npm", "--workspace=backend", "start"]