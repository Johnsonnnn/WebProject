---
tags: JavaScript
---

# JavaSctipt Basic

### Download
```bash
npm install request
```


```javascript=
require("webduino-js");

var request = require("request");

var jp = function(){
  request(
    url:"http:...",
    method:"GET"
  ), function(error, response, body){
      if(error || !body){
        return;
      }else{
        console.log(body);
      }
  }
}
```