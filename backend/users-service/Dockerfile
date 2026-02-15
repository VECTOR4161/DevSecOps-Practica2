FROM node:20-alpine AS deps

WORKDIR /app

COPY package*.json ./
RUN npm ci --omit=dev

FROM node:20-alpine AS runtime

WORKDIR /app

RUN rm -rf /usr/local/lib/node_modules/npm \
	&& rm -f /usr/local/bin/npm /usr/local/bin/npx

COPY --from=deps /app/node_modules ./node_modules
COPY src ./src

EXPOSE 3001
CMD ["node", "src/server.js"]