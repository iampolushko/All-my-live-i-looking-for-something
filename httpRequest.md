## Http protocol

have:

- http request (from user to server)
- http response (from server to user)

http request structure:
<text style="color: rgba(0, 0, 0, 0.2);">you dont see this. It is browser work</text>

- method (get, post - is the most pupalt but put, patch and delete exists too)
- addres
- protocol

<text style="color: rgba(0, 0, 0, 0.2);">Headers. You work wiht that as usual</text>

- host (id or domian name)
- user agent (u can do not see this)
- accept (u dont see this too)
  <text style="color: rgba(0, 0, 0, 0.2);">Dont give a damn</text>
- empty line what division haders and body
  <text style="color: rgba(0, 0, 0, 0.2);">body</text>
  body looks linke: k1=1&k2=2&k3=3. Possible to be empty

### Requests

- #### GET

  - idempotent (don't change nothing on server). In the most cases work for follow to link, request in google
  - His body always empty but if we need to send it we just can add it directly in URL after "?" and devide by "&" like:
    https://vk.com/audios6666?first=1&second=2

  * Body ALWAYS empty. It is means what user always see the params in URL
  * We can send data only like "key=value"

* #### POST
  - Made for change something on server (like add the data)
  - Commonly use for send data from HTML form
  - All params containig in request body (User don't see this in URL)
  - We can send data in any object

#### Response

<text style="color: rgba(0, 0, 0, 0.2);">you don't see this. It is browser work</text>
Start line:

- protolol (like HTTP or HTTPS)
- answer code

<text style="color: rgba(0, 0, 0, 0.2);">Headers. You work wiht that as usual</text>
Headers:

- Date
- Server (Like Apache)
- Content-Type (text/html or text/css or text.xml or application/json)

  <text style="color: rgba(0, 0, 0, 0.2);">Dont give a damn</text>
  body:

```html
<h1>Some shit</h1>
```

### Statuses

- 200 - It is OK
- 3xx - redirect
- 4xx - client error
- 5xx - server error
