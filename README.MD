# Flask app with security and logger

## Workflow

### Launch flask sever

```
python3 -m venv env

source env/bin/activate

pip3 install -r requirements.txt

python app.py
```

### Test API

**All the following endpoint use http post request**

_/register and /login need one object containing the email and password_.

_protected route is used with the bearer access token send by the server when we login_.

_refresh_token route is used with the bearer refresh token send by the server when we login_

```
{
email: 'email',
password: 'password'
}
```

### EndPoints

1. http://localhost:4000/register

2. http://localhost:4000/login

3. http://localhost:4000/protected

4. http://localhost:4000/refresh_token

5. http://localhost:4000/protecteddata

6. http://localhost:4000/userdata

7. http://localhost:4000/limitedaccess

7. http://localhost:4000/openaccess

9. http://localhost:4000/logout


### Below are some sample api calles added for reference


## "register"

```
curl -i -u application_name:application_password --data '{"email": "nag@test.com", "password":"testpass"}' http://localhost:4000/register --header 'Content-Type: application/json' --header 'Accept: application/json'
```
## "login"
```
curl -i -u application_name:application_password --data '{"email": "nag@test.com", "password":"testpass"}' http://localhost:4000/login --header 'Content-Type: application/json' --header 'Accept: application/json'
```

## call protected api using 
## "protected"
```
curl -i -u application_name:application_password --data '{"email": "nag1@test.com", "password":"testpass"}' http://localhost:4000/protecteddata --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpYXQiOjE2MTMzODI1MzMsIm5iZiI6MTYxMzM4MjUzMywianRpIjoiOWVlOTJlNTAtMzZiNS00NzY5LTlmZGEtOTJlMmFmOWYxN2MyIiwiZXhwIjoxNjEzMzgzNDMzLCJpZGVudGl0eSI6MSwiZnJlc2giOmZhbHNlLCJ0eXBlIjoiYWNjZXNzIn0.SLRrd3go1c1xdti1dSdzxe1I9GAm4KVmyvd3esTV-'
```

# we can not access api without current users access token
```
curl -i -u application_name:application_password --data '{"email": "nag@test.com", "password":"testpass"}' http://localhost:4000/protected --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpYXQiOjE2MTMzODI1MzMsIm5iZiI6MTYxMzM4MjUzMywianRpIjoiOWVlOTJlNTAtMzZiNS00NzY5LTlmZGEtOTJlMmFmOWYxN2MyIiwiZXhwIjoxNjEzMzgzNDMzLCJpZGVudGl0eSI6MSwiZnJlc2giOmZhbHNlLCJ0eXBlIjoiYWNjZXNzIn0.SLRrd3go1c1xdti1dSdzxe1I9GAm4KVmyvd3esTV-'
```

## userdata  you can access using GET request without any token.
```
visit http://localhost:4000/userdata from bwowser
```

## added custom limit 6per day for ip to access api GET method
```
visit http://localhost:4000/limitedaccess from bwowser and refrest 6 times
```
TODO
## for whitelisting ip refer
https://flask-limiter.readthedocs.io/en/stable/#flask_limiter.Limiter.request_filter 

## this api can called without any limit

visit http://localhost:4000/openaccess from bwowser and refrest 

deploy on AWS refer [deploy_flask_om_aws.md]



