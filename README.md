# Simple API Router

A lightweight, flexible `API` routing library for `JavaScript` that provides a simple and extensible way to define and manage `API Endpoints`.

## Features

- Simple `API` and `Endpoint` class structure
- Easy route and method matching
- Flexible endpoint handler execution
- Supports dynamic API routing

## Usage Example

This example is taken from a [`Full Working Example`](https://github.com/FirstTimeEZ/server-ssl)

Defining an `API`

```javascript
import { Api, Endpoint } from 'simple-api-router';

const API = new Api("/api/");

API.addEndpoint(new Endpoint("time", "GET", (req, res) => {
    return STATE.respondWithContent(res, Date.now().toString(), STATE.TEXT_HTML);
}));

const HTTPS_SERVER = createServerHTTPS(STATE.loadDefaultSecureContext(), (req, res) => {
    if (API.checkFindExecute(req, res)) {
        return;
    }
    
    ...
})...
```

Calling an `API`

```javascript
fetch("/api/time").then((response) => response.json().then((time) => console.log(time)));
```

## API Classes

### `Api` Class

#### Constructor
- `new Api(apiRoute)`: Create a new API with a base route

#### Methods
- `addEndpoint(endpoint)`: Add an endpoint to the API
- `checkRoute(url)`: Check if a URL matches the API's base route
- `findEndpoint(endpointPath)`: Find an endpoint matching a given path
- `findEndpointCheckMethod(req)`: Find an endpoint and verify its HTTP method
- `checkFindExecute(req, res)`: Attempt to execute the handler for a matching endpoint

### `Endpoint` Class

#### Constructor
- `new Endpoint(path, method, handler)`: Create a new endpoint

#### Methods
- `checkMethod(method)`: Verify the HTTP method
- `executeHandler(req, res)`: Execute the endpoint's handler
- `executeHandlerArgs(req, res, ...args)`: Execute the handler with additional arguments

## Key Concepts

- The `Api` class manages a collection of endpoints for a specific route prefix
- `Endpoint` instances define specific path, HTTP method, and handler combinations
- `checkFindExecute` method provides a convenient way to route and handle requests