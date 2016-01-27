//xxxxx
var url = require("url");
 var http = require('http');
 var fs=require("fs");  
 var time1=function(xx){
 	return {
		"hour": xx.getHours(),  
       "minute": xx.getMinutes(),  
       "second": xx.getSeconds() 

 	}
 }
 var time2=function(xx){
 	return {
		"unixtime": xx.getTime()
 	}
 }
     var server = http.createServer(function (req, res) {  
       res.writeHead(200, {'Content-Type': 'application/json' })
  		var urlpaser=url.parse(req.url, true);
  		var time=new Date(urlpaser.query.iso);
  		var results=null;
  		if (urlpaser.pathname=="/api/parsetime"){
  			results=time1(time);
  		}
  		if (urlpaser.pathname=="/api/unixtime"){
  			results=time2(time);
  		}
  		res.end(JSON.stringify(results));
     })  
     server.listen(process.argv[2]); 
