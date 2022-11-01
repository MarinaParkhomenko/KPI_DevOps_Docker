# KPI DevOps Docker Project. Dockerizing a Node.js web app

Creating `package.json` file that describes the app and its dependencies
```json
{
  "name": "docker_web_app",
  "version": "1.0.0",
  "description": "Node.js on Docker",
  "author": "Maryna Parkhomenko",
  "main": "server.js",
  "scripts": {
    "start": "node server.js"
  },
  "dependencies": {
    "express": "^4.16.1"
  }
}
```

Running `npm install`

Creating `server.js` file that defines a web app
```js
'use strict';

const express = require('express');

// Constants
const PORT = 80;
const HOST = '0.0.0.0';

// App
const app = express();
app.get('/', (req, res) => {
  res.send('Hello World');
});

app.listen(PORT, HOST, () => {
  console.log(`Running on http://${HOST}:${PORT}`);
});
```

Creating `Dockerfile`
```Dockerfile
FROM node:16

# Create app directory
WORKDIR /usr/src/app

# Install app dependencies
# A wildcard is used to ensure both package.json AND package-lock.json are copied
# where available (npm@5+)
COPY package*.json ./

RUN npm install
# If you are building your code for production
# RUN npm ci --only=production

# Bundle app source
COPY . .

EXPOSE 80
CMD [ "node", "server.js" ]
```

Building the image <br>
`docker build . -t dockermarina02/node-web-app`

Running the image <br>
`docker run -p 80:80 -d --memory="20m" --cpus=1.5 dockermarina02/node-web-app`

Checking http://localhost/
<br>
## Voila 
![devops_docker](https://user-images.githubusercontent.com/84531890/199003045-dc7fbdab-9fe6-4174-8ead-fcf73777c040.jpg)
