XDomain
=====
v0.0.1

Summary
---
A JQuery plugin to do cross-domain AJAX requests via postMessage

Downloads
---

* [Development Version](http://xdomain.jpillora.com/dist/xdomain.js)
* [Production Version](http://xdomain.jpillora.com/dist/xdomain.min.js)

Usage
---

Say you wanted to communicate from:

`http://abc.example.com` to `http://xyz.example.com`

1. On your slave domain, create a `proxy.html` file which looks like:

  File: `http://xyz.example.com/proxy.html`
  
  ``` html
  <html>
  <body>
    <!-- jQuery -->
    <script src="//ajax.googleapis.com/ajax/libs/jquery/1.9.1/jquery.min.js"></script>
    <!-- XDomain -->
    <script src="http://xdomain.jpillora.com/dist/xdomain.js"></script>
    <!-- XDomain Whitelist -->
    <script type="text/javascript">
    $.xdomain({
      masters: {
        'http://abc.example.com': '*'
      }
    });
    </script>
  </body>
  </html>
  ```

2. On your master domain (`http://abc.example.com`), definte all slaves 

  File: `http://abc.example.com/index.html`
  ``` html
  <html>
  ...
  <body>
  
    ...
  
    <!-- jQuery -->
    <script src="//ajax.googleapis.com/ajax/libs/jquery/1.9.1/jquery.min.js"></script>
    <!-- XDomain -->
    <script src="http://xdomain.jpillora.com/dist/xdomain.js"></script>
    <!-- XDomain Whitelist -->
    <script type="text/javascript">
    $.xdomain({
      slaves: {
        'http://xyz.example.com': '/proxy.html'
      }
    });
    </script>
    <!-- Other scripts --->
    <script src="app.js"></script>
  </body>
  </html>
  ```

3. Requests from your master domain to your slave domain will work seemlessly

  File: `http://abc.example.com/app.js`
  
  ``` js
  $.get('http://xyz.example.com/secret/data.json').always(function() {
      console.log("got result: ", arguments);
  });
  
  ```

Limitations
---
* IE6/7 Not supported yet
* Functions are removed from the ajax response

Demos
---

http://xdomain.jpillora.com/

API
---

## `$.xdomain`(`object`)

Method to white list master and slave domains

Conceptual Overview
---
XDomain will create an iframe on the master of the slave's proxy.
Master will communicate to slave using postMessage.
Slave will call `$.ajax` on behalf of master.

Contributing
---
Issues and Pull-requests welcome.

Change Log
---

v0.0.1

* Alpha Version

License
---
MIT
