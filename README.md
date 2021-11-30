# IoT-HW
 IoT Communication Design (Homework)

## How to run
- Install project dependencies
```bash
# Install protobuf compiler
$ sudo apt-get install protobuf-compiler

# Install buildtools
$ sudo apt-get install build-essential make

# Install packages
$ pip3 install -r requirements.txt
```
- Run the eclipse mosquitto docker container
```bash
$ sudo docker run -d -it -p 1883:1883 -v $(pwd)/mosquitto.conf:/mosquitto/config/mosquitto.conf eclipse-mosquitto
```
- Compile protobuf schema to python wrapper
```bash
$ make
```
- Start the gRPC service
```bash
$ python3 fibserver.py --ip 0.0.0.0 --port 8080
$ python3 logserver.py --ip 0.0.0.0 --port 8090
```
- Migrate database tables
```bash
$ python3 manage.py migrate
```
- Run the backend server
```bash
$ python3 manage.py runserver 0.0.0.0:8000
```

## Using `curl` to perform client request
Ask for the result of fibonacci at N order
```bash
$ curl -d '{"order":N}' -X POST http://localhost:8000/rest/fibonacci
```
- Or you can use `http` to send request
```bash
$ sudo apt-get install httpie
$ http POST http://localhost:8000/rest/fibonacci <<< '{"order":N}'
```

Get a list of history fibonacci requests sent before
```bash
$ curl http://localhost:8000/rest/logs
```
- Or you can use `http` to send request
```bash
$ sudo apt-get install httpie
$ http http://localhost:8000/rest/logs
```