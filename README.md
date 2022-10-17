# Getting-Started-Metro

Install Metro using npm:  npm install --save-dev metro metro-core
Or via yarn            :  yarn add --dev metro metro-core

 + Running metro #You can run Metro by either running the CLI or by calling it programmatically.

Method runMetro(config) #
-Given the config, a metro-server will be returned. You can then hook this into a proper HTTP(S) server by using its processRequest method:
  CODE:
    'use strict';

    const http = require('http');
    const Metro = require('metro');

    // We first load the config from the file system
    Metro.loadConfig().then(async (config) => {
      const metroBundlerServer = await Metro.runMetro(config);

      const httpServer = http.createServer(
        metroBundlerServer.processRequest.bind(metroBundlerServer),
      );

      httpServer.listen(8081);
    });
    
-In order to be also compatible with Express apps, processRequest will also call its third parameter when the request could not be handled by Metro. This allows you to integrate the server with your existing server, or to extend a new one:
  CODE:
    const httpServer = http.createServer((req, res) => {
      metroBundlerServer.processRequest(req, res, () => {
        // Metro does not know how to handle the request.
      });
    });


