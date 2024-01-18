# System engeneering

## Types of architecture

[Vide about architecture](https://www.youtube.com/watch?v=PmIrrFqOfn8)
[Very short about it](https://www.youtube.com/watch?v=mTLY4Iw7j2U)

### 1 - Monolit

- All functional in one app
- If we need add some. fonctional we need to uptade all app.
- Stupid but easey to make in solo.
- it is very fast.

### 2 - Service orient architecture

![Architecture description photo](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRU1oYYgbvrqB1xJfFEjpm-lvpUh-5cM01ANmoXtm0-fI2T0zKkhp9iXEKP3ISyR0YAmxs&usqp=CAU)

- Frontend services and backend services is different services
- Have a special app to controll all of the services (шина). Fully centralised logic.
- Every service is idipendent(Have them own user interface, buisnes logic and DB)

For communication them use the [SOAP]() protocol

### 3 - Microservices

Is a very small services what can make only one simple work but it working together in one system

## Hosting

Nginx

Apache

MS-2S
