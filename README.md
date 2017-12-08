# windows 下 nginx 自启动
如果Nginx每次使用都需要手动启动确实很麻烦，所以最好将其设置为Windows系统服务，开机自启动就行了。

## 下载运行环境支持程序
下载最新的 [Windows Service Wrapper](https://www.nuget.org/packages/WinSW/) ，下载的文件是.nupkg格式，可通过 [NuGet的Explorer](http://nuget.codeplex.com/releases) 导出，得到的文件有 .NET2.0 和 .NET4.0 两个版本，按电脑所装的 .net framework 版本选择，我们可已重命名文件，比如：nginxservice.exe，但exe文件和xml文件必须同名，将这两个文件放在nginx.exe所在目录下;

## 修改xml文件中的配置项
仅修改路径为nginx的路径，如我的nginx路径为D:\tools\nginx-1.13.2，那么配置文件如下

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
通过cmd安装，进入nginx.exe所在目录，执行以下命令

```
nginxservice.exe install
```

安装完成后，通过“计算机”->"管理"->"服务"可以找到nginx服务