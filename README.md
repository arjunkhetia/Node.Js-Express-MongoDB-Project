# Node-Express-MongoDB Project   ![Version][version-image]

![Linux Build][linuxbuild-image]
![Windows Build][windowsbuild-image]
![NSP Status][nspstatus-image]
![Test Coverage][coverage-image]
![Dependency Status][dependency-image]
![devDependencies Status][devdependency-image]

The quickest way to get start with Node.Js, Express & MongoDB, just clone the project:

```bash
$ git clone https://github.com/arjunkhetia/Node.Js-Express-Project.git
```

Install dependencies:

```bash
$ npm install
```

Start Express.js app at `http://localhost:3000/`:

```bash
$ npm start
```

# Nodemon

Nodemon will watch the files in the directory in which nodemon was started, and if any files change, nodemon will automatically restart your node application.

Start Express.js app with nodemon at `http://localhost:3000/`:

```bash
$ nodemon bin/www
```

# Logger - Morgan & Winston

Morgan - HTTP request logger middleware for node.js:

```js
var logger = require('morgan');
app.use(logger('dev'));
app.use(logger(':remote-addr :remote-user :datetime :req[header] :method :url HTTP/:http-version :status :res[content-length] :res[header] :response-time[digits] :referrer :user-agent', {
    stream: accessLogStream
}));
```

Winston - is designed to be a simple and universal logging library with support for multiple transports:

```js
var winston = require('winston');
var logger = winston.createLogger({
  format: winston.format.combine(
    winston.format.colorize({
        all: true
    }),
    winston.format.printf(
        data => `${data.level} : ${data.message}`
    )
  ),
  transports: [
    new winston.transports.Console({
      level: 'silly'
    }),
    new winston.transports.File({
      level: 'silly',
      filename: './log/ServerData.log'
    })
  ]
});
```

# Rotating File Stream

To provide an automated rotation of Express/Connect logs or anything else that writes to a log on a regular basis that needs to be rotated based on date.

```js
var rfs    = require('rotating-file-stream');
var accessLogStream = rfs('file.log', {
    size:     '10M', // rotate every 10 MegaBytes written
    interval: '1d', // rotate daily
    compress: 'gzip' // compress rotated files
    path: 'log' // folder path for log files
});
```

# Mongo Database Connectivity (with connection pool)

MongoDB driver for Node.js. A Connection Pool is a cache of database connections maintained by your driver so that connections can be re-used when new connections to the database are required.

```js
var MongoClient = require('mongodb').MongoClient;
var option = {
  reconnectTries : 5, // Server attempt to reconnect.
  reconnectInterval: 1000, // Server will wait between retries.
  keepAlive: true, // Keep connection alive.
  poolSize : 10, // The maximum number of connections to create at once.
  connectTimeoutMS: 5000 // TCP Connection timeout setting.
};
```

[version-image]: https://img.shields.io/badge/Version-1.0.0-orange.svg
[linuxbuild-image]: https://img.shields.io/badge/Linux-passing-brightgreen.svg
[windowsbuild-image]: https://img.shields.io/badge/Windows-passing-brightgreen.svg
[nspstatus-image]: https://img.shields.io/badge/nsp-no_known_vulns-blue.svg
[coverage-image]: https://img.shields.io/coveralls/expressjs/express/master.svg
[dependency-image]: https://img.shields.io/badge/dependencies-up_to_date-brightgreen.svg
[devdependency-image]: https://img.shields.io/badge/devdependencies-up_to_date-yellow.svg
