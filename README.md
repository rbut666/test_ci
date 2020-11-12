# test_ci

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).

## build 

``` bash
npm i 
npm run build
cp -r ${JENKINS_HOME}/workspace/${JOB_NAME}/dist/* /www/ci.rbut.cc/
```
