## 配置密钥
公钥和私钥就像钥匙和锁，要想本地免密连接服务器，就得在服务器上锁，这个就是公钥；而本地需要一把钥匙，这个就是私钥。
* 在本地生成密钥对
```bash
ssh-keygen 
# 一直enter就行，不用输入其他。会在用户目录的`.ssh`文件夹下生成私钥`id_rsa`和公钥`id_rsa.pub`
```
* 上传公钥`id_rsa.pub`至服务器用户的`.ssh`文件夹下。

* 登录服务器，将公钥添加至 `authorized_keys` 文件中。

```
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
```

## 命令行ssh免密登录
```bash
ssh username@ip –i /your/path/to/rsa
# `-i`的参数可以不用加，默认是用户的`.ssh`文件夹下的`id_rsa`文件，但有时候有多台服务器要登录，免不了给不同的私钥命名。要指定的话就要按照这种方法指定。
```

## VScode 免密登录
* 下载微软官方的remote-ssh插件
* 在ssh的配置文件中添加登录信息

```bash
Host 任意命名的主机名
    HostName 填ip地址
    User 填用户名
    IdentityFile 填本地rsa私钥的地址，默认在.ssh文件夹下的id_rsa文件
# 可以添加任意多个host
```
