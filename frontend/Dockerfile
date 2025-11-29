####### BUILD STAGE #######
FROM node:lts-alpine AS build

WORKDIR /app

COPY package*.json ./
COPY frontend/package*.json ./frontend/

RUN npm ci --workspace=frontend

COPY . .

ARG VITE_API_URL
RUN VITE_API_URL=$VITE_API_URL npm run build:frontend

# ####### DEVELOPMENT STAGE #######
# FROM build AS development

# CMD ["npm", "run", "dev:frontend"]

####### PRODUCTION STAGE #######
FROM node:lts-alpine AS production

RUN npm install -g serve

WORKDIR /app

COPY --from=build /app/frontend/dist ./

EXPOSE 5000

CMD ["serve", "-s", "."]