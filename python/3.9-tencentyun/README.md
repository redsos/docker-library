# env
`django v4` + `mysql` + `redis` + `celery` + `gunicorn` + `uvicorn[standard]` and  Tencentyun mirror。


#### example
```shell
docker build -t redsos/python:3.9 . -f Dockerfile
docker run --rm -it -v /etc/localtime:/etc/localtime:ro --name work --hostname work redsos/python:3.9 
```
