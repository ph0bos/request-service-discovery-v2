# Service Request Client

Utility module for making HTTP requests against discoverable HTTP services.

Supported service discovery technologies include:

* Container DNS
* ZooKeeper (to be added in the future)
* Consul (to be added in the future)
* Basic Host Port


[![NPM](https://nodei.co/npm/service-request-client.png?downloads=true&downloadRank=true&stars=true)](https://nodei.co/npm/service-request-client/)


## Basic Usage

The following is the most basic example of a Container DNS client:

```javascript
'use strict';

const Client = require('service-request-client').ContainerDNSClient;

// Instantiate a client
const client = new Client(
  'service-name', 
  8001, 
  'my/service/path/v1', 
  { 
    verbose: true, 
    retries: 2,
    timeoutMs: 3000, 
    correlationHeaderName: 'X-Unity-CorrelationID'
  }
);

const query = {
  "myParam": "myValue"  
};

const headers = {
  "Content-Type": "application/json"  
};

const body = {
 "prop1": "value1",
 "prop2": "value2"  
};

// Invoke a GET request against the service endpoint (promise style)
client.get('item/search', { query, headers })
  .then(res => console.log(res.body))
  .catch(err => console.log(err));

// Invoke a GET request against the service endpoint (async/await style)
let res;
  
try {
  res = await client.get('item/search', { query, headers });
  console.log(res.body);
} catch (err) {
  console.log(err);
}

// Invoke a PUT request against the service
client.put('item', { query, headers }, body)
  .then(res => console.log(res.body))
  .catch(err => console.log(err));

// Invoke a POST request against the service
client.post('item', { query, headers }, body)
  .then(res => console.log(res.body))
  .catch(err => console.log(err));  

// Invoke a DELETE request against the service
client.delete('item', { query, headers }, body)
  .then(res => console.log(res.body))
  .catch(err => console.log(err));

 // Invoke a GET request against the service
 client.method('GET', 'item/search', { query, headers }, body)
   .then(res => console.log(res.body))
   .catch(err => console.log(err));  
```


The following is the most basic example of a Host Port client:


```javascript
'use strict';

const Client = require('service-request-client').HostPortClient;

// Instantiate a client
const client = new Client(
  'api.test.io', 
  80, 
  'v1', 
  { 
    verbose: true, 
    retries: 2,
    timeoutMs: 3000
  }
);

const query = {
  "myParam": "myValue"  
};

const headers = {
  "Content-Type": "application/json"  
};

const body = {
 "prop1": "value1",
 "prop2": "value2"  
};

// Invoke a GET request against the service endpoint (promise style)
client.get('item/search', { query, headers })
  .then(res => console.log(res.body))
  .catch(err => console.log(err));

// Invoke a GET request against the service endpoint (async/await style)
let res;
  
try {
  res = await client.get('item/search', { query, headers });
  console.log(res.body);
} catch (err) {
  console.log(err);
}

// Invoke a PUT request against the service
client.put('item', { query, headers }, body)
  .then(res => console.log(res.body))
  .catch(err => console.log(err));

// Invoke a POST request against the service
client.post('item', { query, headers }, body)
  .then(res => console.log(res.body))
  .catch(err => console.log(err));  

// Invoke a DELETE request against the service
client.delete('item', { query, headers }, body)
  .then(res => console.log(res.body))
  .catch(err => console.log(err));

 // Invoke a GET request against the service
 client.method('GET', 'item/search', { query, headers }, body)
   .then(res => console.log(res.body))
   .catch(err => console.log(err));  
````
