# README

> 感觉upstream的合并可以用GitHub页面去管理

## 编译流程

```log
# 5800H 2021.05.18 20min
```

```bash
# 前期准备
# 安装 homebrew，参考官网一键[脚本](https://brew.sh/)
# 可以用raw.hee.ink替换raw.githubusercontent.com
brew install clojure/tools/clojure
brew install leiningen
# 假设你已经装好了 nodejs，配好了npm和yarn
# 假设你已经装好了 openjdk-8-jdk 或 openjdk-11-jdk （推荐前者）
```

然后就可以执行以下的命令

```bash
yarn # 前端
lein deps # 后端
lein run # 后端运行
./bin/build # 前后端一起编译
```


## Zen

> 待翻译

**The Zen of Metabase**


- Give the user value as soon as possible

- Structure things so that we can automagically infer things for the user

- Don’t ask the user for information the system should already know

- Make it easy for the user to do the right thing

- Don’t leave the user booby traps

- Go the extra mile to make the user experience pleasant 


## 编译踩坑

### 前端

```shell
yarn config set registry https://registry.npm.taobao.org
npm config set registry https://registry.npm.taobao.org
```

### 后端

[Clojars清华源加速](https://blog.csdn.net/chybr80884/article/details/100685816)

```clojure
"cat ~/.lein/profiles.clj"

{
    :user {
        :mirrors {
            "central" {
                :name "aliyun"
                :url "https://maven.aliyun.com/repository/central"
            }
            "clojars" {
                :name "tsinghua"
                :url "https://mirrors.tuna.tsinghua.edu.cn/clojars/"
            }
        }
    }
}

```

## 源码学习

### 登录改造 

- JWT方式`jwt.clj`
- 一般的 `session.clj`
- 单点登录 `enterprise/backend/sso` 

对比：一般的登录会尝试`ldap-login`和`email-login`，没数据就不给登录了。JWT登录方式要提供更多的信息，它需要初始化一个用户（如果没登陆过，就创建新用户，如果有记录，就更新记录）

思路：手动加一个接口，模仿企业版的写法，`api/myjwt`，接收到之后做类似的操作（如果没登陆就创建新用户，如果有记录，就更新记录）


### 语言包 `locales.clj`

~~I am Chinese!(大雾)~~

所以语言包(`locales.clj`)只需要编译简体中文就行了。

有一个错误

```bash
Step "Build translation resources" failed with error "Compiling locales/nl.po for frontend...\n+ Warning: removed 8 fuzzy translations\n./bin/i18n/build-translation-resources: 43: msgfmt: not found"
# Ubuntu 20.04 WSL2 
# 看起来 msgfmt是个命令 但是找不到
sudo apt install gettext
# which msgfmt
# 问题解决
```
