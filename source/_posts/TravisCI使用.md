---
title: TravisCI使用
categories: []
tags:
  - 项目管理
reward: true
originContent: >-
  ## 简介


  Travis CI是开源持续集成构建项目.可以直接使用github登陆.支持的语言nodejs,Go.


  [官网](https://travis-ci.org/)


  [阮一峰的Travis
  CI教程](http://www.ruanyifeng.com/blog/2017/12/travis_ci_tutorial.html)




  ## 配置文件


  ### 生命周期

  ![travis语法.png](/images/2019/02/04/7f2c6d60-2855-11e9-ab93-fd218122efe7.png)


  ### Go语言


  ```yaml

  language: go


  go:
    - "1.10.x"
    - "1.11.x"
  services:
    - redis-server
    - mysql
    - postgresql
    - memcached
  env:
    - ORM_DRIVER=sqlite3   ORM_SOURCE=$TRAVIS_BUILD_DIR/orm_test.db
    - ORM_DRIVER=postgres ORM_SOURCE="user=postgres dbname=orm_test sslmode=disable"
  before_install:
   - git clone git://github.com/ideawu/ssdb.git
   - cd ssdb
   - make
   - cd ..
  install:
    - go get github.com/lib/pq
    - go get github.com/go-sql-driver/mysql
    - go get github.com/mattn/go-sqlite3
    - go get github.com/bradfitz/gomemcache/memcache
    - go get github.com/gomodule/redigo/redis
    - go get github.com/beego/x2j
    - go get github.com/couchbase/go-couchbase
    - go get github.com/beego/goyaml2
    - go get gopkg.in/yaml.v2
    - go get github.com/belogik/goes
    - go get github.com/siddontang/ledisdb/config
    - go get github.com/siddontang/ledisdb/ledis
    - go get github.com/ssdb/gossdb/ssdb
    - go get github.com/cloudflare/golz4
    - go get github.com/gogo/protobuf/proto
    - go get github.com/Knetic/govaluate
    - go get github.com/casbin/casbin
    - go get github.com/elazarl/go-bindata-assetfs
    - go get -u honnef.co/go/tools/cmd/gosimple
    - go get -u github.com/mdempsky/unconvert
    - go get -u github.com/gordonklaus/ineffassign
    - go get -u github.com/golang/lint/golint
    - go get -u github.com/go-redis/redis
  before_script:
    - psql --version
    - sh -c "if [ '$ORM_DRIVER' = 'postgres' ]; then psql -c 'create database orm_test;' -U postgres; fi"
    - sh -c "if [ '$ORM_DRIVER' = 'mysql' ]; then mysql -u root -e 'create database orm_test;'; fi"
    - sh -c "if [ '$ORM_DRIVER' = 'sqlite' ]; then touch $TRAVIS_BUILD_DIR/orm_test.db; fi"
    - sh -c "go get github.com/golang/lint/golint; golint ./...;"
    - sh -c "go list ./... | grep -v vendor | xargs go vet -v"
    - mkdir -p res/var
    - ./ssdb/ssdb-server ./ssdb/ssdb.conf -d
  after_script:
    - killall -w ssdb-server
    - rm -rf ./res/var/*
  script:
    - go test -v ./...
    - gosimple -ignore "$(cat .gosimpleignore)" $(go list ./... | grep -v /vendor/)
    - unconvert $(go list ./... | grep -v /vendor/)
    - ineffassign .
    - find . ! \( -path './vendor' -prune \) -type f -name '*.go' -print0 | xargs -0 gofmt -l -s
    - golint ./...
  addons:
    postgresql: "9.6"
  ```
toc: false
date: 2018-12-24 11:37:33
description:
---

## 简介

Travis CI是开源持续集成构建项目.可以直接使用github登陆.支持的语言nodejs,Go.

[官网](https://travis-ci.org/)

[阮一峰的Travis CI教程](http://www.ruanyifeng.com/blog/2017/12/travis_ci_tutorial.html)



## 配置文件

### 生命周期
![travis语法.png](/images/2019/02/04/7f2c6d60-2855-11e9-ab93-fd218122efe7.png)

### Go语言

```yaml
language: go

go:
  - "1.10.x"
  - "1.11.x"
services:
  - redis-server
  - mysql
  - postgresql
  - memcached
env:
  - ORM_DRIVER=sqlite3   ORM_SOURCE=$TRAVIS_BUILD_DIR/orm_test.db
  - ORM_DRIVER=postgres ORM_SOURCE="user=postgres dbname=orm_test sslmode=disable"
before_install:
 - git clone git://github.com/ideawu/ssdb.git
 - cd ssdb
 - make
 - cd ..
install:
  - go get github.com/lib/pq
  - go get github.com/go-sql-driver/mysql
  - go get github.com/mattn/go-sqlite3
  - go get github.com/bradfitz/gomemcache/memcache
  - go get github.com/gomodule/redigo/redis
  - go get github.com/beego/x2j
  - go get github.com/couchbase/go-couchbase
  - go get github.com/beego/goyaml2
  - go get gopkg.in/yaml.v2
  - go get github.com/belogik/goes
  - go get github.com/siddontang/ledisdb/config
  - go get github.com/siddontang/ledisdb/ledis
  - go get github.com/ssdb/gossdb/ssdb
  - go get github.com/cloudflare/golz4
  - go get github.com/gogo/protobuf/proto
  - go get github.com/Knetic/govaluate
  - go get github.com/casbin/casbin
  - go get github.com/elazarl/go-bindata-assetfs
  - go get -u honnef.co/go/tools/cmd/gosimple
  - go get -u github.com/mdempsky/unconvert
  - go get -u github.com/gordonklaus/ineffassign
  - go get -u github.com/golang/lint/golint
  - go get -u github.com/go-redis/redis
before_script:
  - psql --version
  - sh -c "if [ '$ORM_DRIVER' = 'postgres' ]; then psql -c 'create database orm_test;' -U postgres; fi"
  - sh -c "if [ '$ORM_DRIVER' = 'mysql' ]; then mysql -u root -e 'create database orm_test;'; fi"
  - sh -c "if [ '$ORM_DRIVER' = 'sqlite' ]; then touch $TRAVIS_BUILD_DIR/orm_test.db; fi"
  - sh -c "go get github.com/golang/lint/golint; golint ./...;"
  - sh -c "go list ./... | grep -v vendor | xargs go vet -v"
  - mkdir -p res/var
  - ./ssdb/ssdb-server ./ssdb/ssdb.conf -d
after_script:
  - killall -w ssdb-server
  - rm -rf ./res/var/*
script:
  - go test -v ./...
  - gosimple -ignore "$(cat .gosimpleignore)" $(go list ./... | grep -v /vendor/)
  - unconvert $(go list ./... | grep -v /vendor/)
  - ineffassign .
  - find . ! \( -path './vendor' -prune \) -type f -name '*.go' -print0 | xargs -0 gofmt -l -s
  - golint ./...
addons:
  postgresql: "9.6"
```