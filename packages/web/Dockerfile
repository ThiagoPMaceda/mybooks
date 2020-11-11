FROM node:latest As builder
ENV NODE_ENV=production
WORKDIR /usr/src/app
COPY ["package.json", "package-lock.json*", "npm-shrinkwrap.json*", "./"]
RUN npm install --production --silent && mv node_modules ../
COPY . .

FROM nginx:latest

COPY --from=builder /usr/src/app/dist/web/ /user/share/nginx/html

EXPOSE 4000
CMD ["npm", "start"]
