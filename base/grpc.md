## grpc
### protoc
  安装protoc工具
  go get -d -u github.com/golang/protobuf/protoc-gen-go
  
### php
  安装手册 https://github.com/grpc/grpc/tree/master/src/php
  ```git
  sudo pecl install grpc
  git clone -b $(curl -L https://grpc.io/release) https://github.com/grpc/grpc
  cd grpc/src/php/ext/grpc
  phpize
  ./configure
  make
  sudo make install

  //You need to add this to your project's composer.json file.
   "require": {
    "grpc/grpc": "v1.12.0"
  }
  ```
### 使用
  protoc -I ./ --php_out=./client --grpc_out=./client --plugin=protoc-gen-grpc=/Users/zyp/grpc/bins/opt/grpc_php_plugin deposit.proto
