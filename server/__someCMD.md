
```curl -X GET http://localhost:3000 -v```


```curl -X GET http://localhost:3000 -c cookie-file.txt```
This creates a text file in our /client folder called ‘cookie-file.txt’

Now we can call curl again, but this time calling cookie-file.txt with the ‘-b’ flag which tells cURL to send our session id in our header data.

```curl -X GET http://localhost:3000 -b cookie-file.txt -v```


1. khi server restarted thì session merrory sẽ mất
2. lúc gửi request lên sẽ đi cùng sessionID (along with - cùng với)
3. The server receives the requests, and the session middleware can’t find the session id in memory, so it call the genid function

4. The genid function logs that we are inside the session middleware and it logs the request object’s session id. Since we sent the session id in our cURL request, the request object was actually instantiated with that session id. However, this session id is overwritten by the return value of the genid function.

5. When the session middleware is done overwriting the session id we sent, control is handed over to the callback function within app.get(), where we log that we are inside the hompage callback function and log the new id.

Nếu đúng như ta nghĩ, lúc ở Server overwritten, thì session id trong cookie file phải dc overwriten.
chúng ta sẽ run lệnh ```... -b``` and sessionID ko có dc overwritten ở phía Client.

ta sẽ run lệnh ``` -c```
The req.sessionID isn’t defined, because we didn’t send the session info in our curl request.
-> điều này có nghĩa với lệnh -c ta ko có send sessionID lên. Và lúc này
ta overwritten ở phía Client.

VẤn đề chẳng dc giải quyết

```curl -X POST http://localhost:3000/login -b cookie-file.txt -H 'Content-Type: application/json' -d '{"email":"test@test.com", "password":"password"}'```


