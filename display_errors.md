# 显示错误

web应用几乎没有例外的会在某些点上生成一些验证错误信息，提示用户做错了什么，应该怎么样正确的去做。这些提示应该与你的应用UI策略一致，能明确的告诉用户如何去处理。下面介绍如何利用Stripes进行错误信息处理。

## 输出错误

Stripes提供若干输出验证错误信息的标签，这些标签是值得花时间通过阅读文档去了解的。主要的标签是[stripes:erros](http://stripes.sourceforge.net/docs/current/taglib/stripes/errors.html)。这个标签可以针对一个表单输出所有的验证错误信息或者仅仅输出一个单独域的错误信息。

这里就不重复标签文档内容了，但这里有几个例子：

> 示例一：使用默认的格式输出所有错误
>
    <stripes:errors/>

针对这个例子，假设其不是内嵌在｀<stripes:form>` 标签中的，它会将所有错误信息通过HTML的ul标签展示出来。假如在一个页面上有多个表单，可以为每一个表单在不同的位置显示错误信息：

> 示例二：多表输出错误信息在不同的位置

>      <stripes:form action="/foo/first.action">
          <stripes:errors/>
          ...
          </stripes:form>
> 
      ...
> 
      <stripes:errors action="/foo/second.action">
      <stripes:form action="/foo/second.action">
          ...
      </stripes:form>

