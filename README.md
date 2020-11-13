# test_ci

## build 

``` bash
npm i 
npm run build
# JENKINS_HOME === /var/lib/jenkins
# 目标文件夹需要设置权限  chmod a+rw /www/ci.rbut.cc
cp -r ${JENKINS_HOME}/workspace/${JOB_NAME}/dist/* /www/ci.rbut.cc/
```

## jenkins 新建JOB之后的配置 （使用 github中的项目

> 【源码管理】 勾选 Git;
>> 在 Repositories URL 中填入 https://github.com/xxxx.git;
>> private私有项目 添加 Credentials (使用 secret_key 失败，使用github的账号密码就可以正常获取)

> 【构建触发器】 暂未设置 后期可以使用需要的方式 触发更新

> 【构建环境】
>> 勾选 Provide Node & npm bin/folder to PATH 选择高一点版本的nodejs

> 【构建】
>> 需要注意的是  在jenkins 中的操作 都在 jenkins内部  所有文件操作都是在 linux 用户名 jenkins中；所以无法使用到 当前 root用户中的 npm包 包括 pm2 这种 全局安装的包


> 对于 nodejs 项目
``` bash
# 目标目录 target_path
# 复制 项目所有文件到 指定目录
cp -r ./* /www/wwwroot/target_path/
# 复制完成后 切换到 目标目录
cd /www/wwwroot/target_path

# 检查 pm2 是否存在 pm2 -version 可替换成其他命令用于检查命令是否存在
if ! command -v pm2 -version &> /dev/null
then
        echo 'pm2 不存在'
        npm i -g pm2
fi
npm i
npm run start

```

> 对于 vue 项目 
``` bash
# 在工作区 进行 安装包 
npm i
# 之后 命令构建 将 dist 中的文件 复制到 指定目录
npm run build 
cp -r ./dist/* /www/wwwroot/wx.rbut.cc/
```