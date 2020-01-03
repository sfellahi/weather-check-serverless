# Wether check serverless (AWS Lex, Lambda and API Gateway)

The goal of this website is to support the learning of the Building Serverless Applications course.


### Application rendering
![Screenshot](images/mainapp.png)

### AWS Lex test code

![Screenshot](images/awslex.png)

![Screenshot](images/lexarchi.png)
````
 function handler(event, context, callback){      
      var 
          MESSAGE_STR = event.message_str,
          USER_ID_STR = event.user_id_str,
          AWS = require("aws-sdk"),
          LEXRUNTIME = {},
          BOT_NAME_STR = "WeatherCatBot",
          BOT_ALIAS_STR = "$LATEST",
          sessionAttributes = {
  
          },
          params = {};
      
      AWS.config.update({
          region: "us-east-1"
      });
      
      LEXRUNTIME = new AWS.LexRuntime();
  
      params = {
          botAlias: BOT_ALIAS_STR,
          botName: BOT_NAME_STR,
          inputText: MESSAGE_STR,
          userId: USER_ID_STR,
          sessionAttributes: sessionAttributes
      };
      LEXRUNTIME.postText(params, function(error, data){
          var response = {};
          if(error){
              console.log(error, error.stack);
              response = "problem with lex";
              callback(null, response);
          }else{
              console.log(data);
              response = data;
              callback(null, response);
          }
      });
  }
  exports.handler = handler;
```