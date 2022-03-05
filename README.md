# docker-library
china mirror

#### Rust Workground
```shell
git clone https://github.com/RedisJSON/RedisJSON.git --branch v2.0.7 --single-branch

podman run --rm --tz=Asia/Shanghai --network=host -it -v "${pwd}/RedisJSON":/data/work --name work --hostname work redsos/rust:1.58-tencentyun cargo build --release
```


#### Python Workground
```shell
docker run --rm --tz=Asia/Shanghai --network=host -it redsos/python:3.9-tencentyun python --version
```
