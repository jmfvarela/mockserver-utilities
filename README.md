# Requeriments
* JDK
* Node.js

# Installing
```
npm install mockserver-grunt --save-dev
npm install mockserver-client 
```

# Starting
```
node start_mockserver
```

# Collecting data
Set proxy in your browser to localhost:1090.

Navigate with your browser over the resources to collect. For example:
http://api.openweathermap.org/data/2.5/weather?q=Seville,Sp&appid=2de143494c0b295cca9337e1e96b00e0
https://en.wikipedia.org/w/api.php?format=json&action=query&titles=mock&prop=revisions&rvprop=content

If you are going to use HTTP, you can install the server certificate 'CertificateAuthorityCertificate.pem' into the "certification authorities" in the browser.

Capture logs executing:
```
node dumpToLogs
```

# Configuring mocks
* Create new mock extracting fields (httpRequest, httpResponse, times, timeToLive) from mockserver_request.log in the format:
```
mockServerClient("localhost", 1080).mockAnyResponse(
{
  "httpRequest" : {...}, // the http request that must be matched for this expectation to respond
  "httpResponse" : {...}, // object that can be used to specify the response
  "times" : {...}, // the number of times to respond when this http is matched
  "timeToLive" : {...} // timeToLive  the length of time from when the server receives the expectation that the expectation should be active
});
```
* Select only required properties in httpRequest and remove the others.
* Set times.unlimited to true.

Example: mockserverclient.js

# Using mocks
Import mocks executing:
```
node mockserverclient
```
Test the results. For example with your browser:
http://localhost:1080/data/2.5/weather?q=Seville,Sp&appid=2de143494c0b295cca9337e1e96b00e01
https://localhost:1080/w/api.php?format=json&action=query&titles=mock&prop=revisions&rvprop=content

# Todo
* Exception message with Certification Authorities during the server execution, but it seems that does not affect operation.

