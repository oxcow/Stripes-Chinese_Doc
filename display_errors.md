# 展示错误

web应用几乎没有例外的会在某些点上生成一些验证错误信息，提示用户做错了什么，应该怎么样正确的去做。这些提示应该与你的应用UI策略一致，能明确的告诉用户如何去处理。下面介绍如何利用Stripes进行错误信息展示。

## 输出错误

Stripes提供若干输出验证错误信息的标签，这些标签是值得花时间通过阅读文档去了解的。主要的标签是[stripes:erros](http://stripes.sourceforge.net/docs/current/taglib/stripes/errors.html)。这个标签可以针对一个表单输出所有的验证错误信息或者仅仅输出一个表单指定域的错误信息。

这里就不重复标签文档内容了，直接看下几个示例：

> 示例1：使用默认的格式输出所有错误
>
    <stripes:errors/>

针对这个例子，假设其不是内嵌在｀<stripes:form>` 标签中的，它会将所有错误信息通过HTML的ul标签展示出来。如果在一个页面上有多个表单，可以为每一个表单在不同的位置显示错误信息：

> 示例2：多表输出错误信息在不同的位置

>     <stripes:form action="/foo/first.action">
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

第一个`<stripes:errors/>`标签是内嵌在｀<stripes:form>` 标签中的.这种情况下，`<stripes:errors/>` 仅输出表单提交后针对该表单的错误信息。第二个`<stripes:errors/>`不是内嵌在表单元素内的，但是由于其支持 **action** 属性，因此它将也只显示与 **action** 属性值匹配的表单错误信息。

下面的示例展示如何输出指定域的错误信息，以及如何输出全局错误（不关联任何指定的的域）

> 示例3：输出指定域的错误信息
>
	<stripes:form action="/foo/fist.action">
       <stripes:errors globalErrorsOnly="true"/>
       <table>
			<tr>
			    <td>Username:</td>
			    <td>
				<stripes:text name="username"/>
				<stripes:errors field="username"/>
			    </td>
			</tr>
			<tr>
			    <td>Password:</td>
			    <td>
				<stripes:text name="password"/>
				<stripes:errors field="password"/>
			    </td>
			</tr>
    	</table>
	</stripes:form>


默认的错误输出格式是通过错误消息包下的一组四个资源控制的（通常是StripesResources）。A different set of resources is used when outputting field specific errors to allow distinct presentation.关于错误输出的更多细节可以在标签文档[errors tag](http://stripes.sourceforge.net/docs/current/taglib/stripes/errors.html)中找到。同时，错误格式也可通过每次使用错误标签时，内嵌[individual错误标签](http://stripes.sourceforge.net/docs/current/taglib/stripes/individual-error.html)进行修改。 



## 域错误高亮显示

Stripes具有当错误发生时改变字段域展示的能力。为此，该类通过实现 [TagErrorRenderer]接口，并通过一个实现了[TagErrorRendererFactory]接口的工厂类来提供实例。接下来的几分钟内，我们将介绍实现了这些接口的自定义类能做些什么，但在这之前，让我们先看下默认的类都多了些什么。

### 使用默认的TagErrorRenderer改变样式


首先，有一个非常简单的默认工厂类[DefaultTagErrorRendererFactory]，通过它可以返回[DefaultTagErrorRenderer]的初始化实例。它也可以被配置成返回你自己的实现了TageErrorRender对象的实例。

[DefaultTagErrorRenderer]的实现是非常简单的。针对错误中的任何一个域它只做了一个改变标签的CSS样式的操作。如果标签没有一个*class="something"*的属性（也就是没有**class**属性），默认的将会为其添加*class="error"*。如果标签包含**class**属性，比如*class="foo"*那么渲染器将重写**class**属性为*class="error foo"*



[TagErrorRenderer]: (http://stripes.sourceforge.net/docs/current/javadoc/net/sourceforge/stripes/tag/TagErrorRendererFactory.html)
[TagErrorRendererFactory]: (http://stripes.sourceforge.net/docs/current/javadoc/net/sourceforge/stripes/tag/TagErrorRendererFactory.html)
[DefaultTagErrorRenderer]: (http://stripes.sourceforge.net/docs/current/javadoc/net/sourceforge/stripes/tag/DefaultTagErrorRenderer.html)
[DefaultTagErrorRendererFactory]: (http://stripes.sourceforge.net/docs/current/javadoc/net/sourceforge/stripes/tag/DefaultTagErrorRendererFactory.html)



