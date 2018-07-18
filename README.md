# Windows 下 nginx 自启动
如果 Nginx 每次使用都需要手动启动确实很麻烦，所以最好将其设置为 Windows 系统服务，开机自启动就行了。

## 下载运行环境支持程序
下载最新的 [Windows Service Wrapper](https://www.nuget.org/packages/WinSW/) ，下载的文件是 .nupkg 格式，可通过 [NuGet 的 Explorer](http://nuget.codeplex.com/releases) 导出，得到的文件有 .NET2.0 和 .NET4.0 两个版本，按电脑所装的 .net framework 版本选择，我们可以重命名文件，比如：nginxservice.exe，但 exe 文件和 xml 文件必须同名，将这两个文件放在 nginx.exe 所在目录下;

## 修改xml文件中的配置项
仅修改路径为 nginx 的路径，如我的 nginx 路径为 D:\tools\nginx-1.13.2，那么配置文件如下

```html
<service>
    <id>nginx</id>
    <name>nginx</name>
    <description>nginx</description>
    <executable>D:\tools\nginx-1.13.2\nginx.exe</executable>
    <logpath>D:\tools\nginx-1.13.2\logs</logpath>
    <logmode>roll</logmode>
    <depend></depend>
    <startargument>-p</startargument>
    <startargument>D:\tools\nginx-1.13.2</startargument>
    <stopexecutable>D:\tools\nginx-1.13.2\nginx.exe</stopexecutable>
    <stopargument>-p</stopargument>
    <stopargument>D:\tools\nginx-1.13.2</stopargument>
    <stopargument>-s</stopargument>
    <stopargument>stop</stopargument>
</service>
```

## 安装程序设置为Windows服务操作
通过 cmd 安装，进入 nginx.exe 所在目录，执行以下命令

```
nginxservice.exe install
```

安装完成后，通过“计算机”->"管理"->"服务"可以找到 nginx 服务

**本文翻译自：** [https://stackoverflow.com/questions/10061191/add-nginx-exe-as-windows-system-service-like-apache/13875396#13875396](https://stackoverflow.com/questions/10061191/add-nginx-exe-as-windows-system-service-like-apache/13875396#13875396)