# Python-notes

针对你的法学需求开始写的一份笔记。

最近，国内访问 GitHub 会因为 DNS（域名解析服务）的问题出现**图片无法显示**的情况，如果你也遇到了这样的问题，可以通过**修改本机的 hosts 文件**直接对 GitHub 的资源链接进行域名解析来加以解决。使用 macOS 系统的读者可以参考[《macOS 下三种修改 hosts 文件的方法》](<https://www.jianshu.com/p/752211238c1b>)一文来修改 hosts 文件；使用 Windows 系统的读者可以参考[《在 Windows 上如何管理 hosts 文件》](<https://sspai.com/post/43248>)一文来进行操作。我们可以把下面的内容添加到 hosts 文件的末尾，这样就可以解决 GitHub 上图片无法显示的问题。

```INI
151.101.184.133    assets-cdn.github.com
151.101.184.133    raw.githubusercontent.com
151.101.184.133    gist.githubusercontent.com
151.101.184.133    cloud.githubusercontent.com
151.101.184.133    camo.githubusercontent.com
```

也可以使用Github镜像源来代替，例如：**`github.com.cnpmjs.org`**
我在Gitee上添加了新的仓库，国内应该可以访问：https://gitee.com/tflsxyy/python-notes

## References

[1]. https://github.com/jackfrued/Python-Core-50-Courses

[2]. https://github.com/jackfrued/Python-100-Days

[3]. https://github.com/walter201230/Python
