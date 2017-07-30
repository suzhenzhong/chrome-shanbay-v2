# chrome-shanbay-v2

> shanbay chrome 网页查单词插件

是[jinntrance/shanbay-crx](https://github.com/jinntrance/shanbay-crx)的重构版


和原版的区别：
- 没有Webster了
- 没有快捷键
- 没有弹出框延时关闭
- 弹出框界面跟shanbay的一模一样了（抄的，能不一样么～～）
- 弹出框出现的位置友好了一点
- 代码上简洁了一点点，然后没有用外部库，全手撸（其实代码量很少）
- console里面打印的日志少了一点（逃～～


已知的问题

- 有些词语的释义渲染的很差。这个锅主要由扇贝的API来背……
- 网页中嵌套iframe的时候，不能正确触发事件。这个不打算处理。因为默认的获取选区方法是获取当前顶级文档下的选区。想要获取frame的选区必须得到frame的文档，但是页面不知道会嵌入多少个文档，所以这个很难处理。现在还在广泛使用嵌入frame的网页有网页播放器，网页邮箱，在一个网站获取一个社交的网站动态（比如微博）等。一个嵌套了frame的网页，对于用户来说，一眼是看不出来的。这个也不想弹出一个警告什么的，太丑了。所以，let it go吧。

吐槽：

主要目标是Shanbay API。

1，他们自己弹出框用的数据跟API返回的数据居然不一样，而且质量没有自己用的好。不知道这样设置的原因是什么
2，返回单词语音的连接是HTTP的，而自己使用的单词语音资源是HTTPS的。这个问题是写第一版的时候，直接使用audio标签进行语音的处理的时候，在HTTPS的网站上发现的（后来因为GitHub的CSP导致这个方案死掉了）。这个是为了省钱？但是HTTPS的认证好像也不是很贵啊，免费的也行啊。
3，返回数据格式不统一。中文释义跟英文释义的格式不一样。中文的词性一项经常是空的，就返回一个特长的一个字符串，里面包含了N多条目。用换行符分割的，开发者自己去解析。我想弄的好看点，词性加粗，然后跟后面的解释分开。但是因为返回内容没有一点规律，不得不放弃掉。
4，实际上呢，因为是chrome的插件，chrome当然可以获得自己所有的cookies，直接使用Shanbay内部的API更简单粗暴，也不需要认证。我甚至给开发者发邮件说，你们这API使用体验不好的话，是变相让用户使用你们内部API，这样给你们的服务器带来的压力就没办法分类了，而且鉴于没有那么多限制，也不好控制开发者行为了。然后也没见人回复。就这吧，毕竟沪江还没API呢。

