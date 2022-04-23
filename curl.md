# Curl

````
#GET Request
#-v for verbose output
Staphy$ curl http://staphysce.com/ -v 

# cURL - Basic AUTH Login
Staphy$  curl http://admin:password@staphysec.com/ -vvv

#Alternately, the "`-u`" flag can be used to specify credentials as well.
Staphy$  curl -u admin:password  http://staphysec.com/ -vvv

#cURL - Basic AUTH Login & Follow Redirections
Staphy$ curl -u admin:password -L http://staphysec.com/

#cURL - GET Request With Parameter
Staphy$ curl -u admin:password 'http://staphysec.com/search.php?port_code=us'

#POST Method
The "`-L`" flag instructs curl to follow redirections.
The default "`Content-Type`" used by `cURL` is "`application/x-www-form-urlencoded`


Staphy$ curl -d 'username=admin&password=password' -L http://staphysce.com/login.php

#### cURL - Debug

The "`-L`" flag instructs curl to follow redirections.
`cURL` automatically sends a POST request when the "`-d`" flag is used. It's found that we're still on the login page even after specifying valid credentials. Let's use the "`-v`" switch to debug this.

```shell-session
Staphy@htb[/htb]$ curl -d 'username=admin&password=password' -L  http://staphysec.com/login.php -v
```
The "`--cookie`" or "`--cookie-jar`" option can be used to specify cookie usage in `cURL`. This can point to `/dev/null` or a file on the disk, where the cookies will be saved.
#cURL - Cookie
Staphy$ curl -d 'username=admin&password=password' -L --cookie-jar /dev/null  http://staphysec.com/login.php -v

#cURL - Cookie File
Staphy$ curl -d 'username=admin&password=password' -L --cookie-jar cookies.txt  http://staphysec.com/login.php

Specifying a file name as the argument saves the cookies to a file, which can be used to access the page later directly.
Staphy$ curl --cookie cookies.txt http://staphysec.com/admin/dashboard.php -v


#Content-Type header
#It's also possible to send JSON data using `cURL`. This can be done by specifying the "`application/json`" header with the "`-H`" flag.
Staphy$ curl -H 'Content-Type: application/json' -d '{ "username" : "admin", "password" : "password" }' --cookie-jar /dev/null -L  http://staphysec.com/login.php

#PUT and DELETE Methods
#The "`-X`" option can be used to specify the request method to use.
Staphy$ curl -X OPTIONS http://staphysec.com/ -vv


#cuRL - File Upload
Staphy$ curl -X PUT -d @test.txt http://staphysec.com/test.txt -vv

#cURL - DELETE Method
Staphy$ curl -X DELETE http://staphysec.com/test.txt -vv
````
