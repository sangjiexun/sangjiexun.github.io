https://yunwu.zeabur.app
apikey=sk-jUtWyLerwlKHc6cXWOfO9OrNLL5vVRXZKrNHWZZGnV7jPqWX
参考代码：
var https = require('follow-redirects').https;
var fs = require('fs');

var options = {
   'method': 'POST',
   'hostname': 'yunwu.ai',
   'path': '/v1/chat/completions',
   'headers': {
      'Accept': 'application/json',
      'Authorization': 'Bearer <token>',
      'Content-Type': 'application/json'
   },
   'maxRedirects': 20
};

var req = https.request(options, function (res) {
   var chunks = [];

   res.on("data", function (chunk) {
      chunks.push(chunk);
   });

   res.on("end", function (chunk) {
      var body = Buffer.concat(chunks);
      console.log(body.toString());
   });

   res.on("error", function (error) {
      console.error(error);
   });
});

var postData = JSON.stringify({
   "model": "gpt-5-nano",
   "messages": [
      {
         "role": "user",
         "content": "nihao。"
      }
   ],
   "max_tokens": 1000
});

req.write(postData);

req.end();

响应结果
返回响应
🟢200
OK
application/json
id
string 
必需
object
string 
必需
created
integer 
必需
choices
array [object] 
必需
index
integer 
可选
message
object 
可选
finish_reason
string 
可选
usage
object 
必需
prompt_tokens
integer 
必需
completion_tokens
integer 
必需
total_tokens
integer 
必需
示例
{
    "id": "chatcmpl-123",
    "object": "chat.completion",
    "created": 1677652288,
    "choices": [
        {
            "index": 0,
            "message": {
                "role": "assistant",
                "content": "\n\nHello there, how may I assist you today?"
            },
            "finish_reason": "stop"
        }
    ],
    "usage": {
        "prompt_tokens": 9,
        "completion_tokens": 12,
        "total_tokens": 21
    }
}