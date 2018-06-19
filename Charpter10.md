# 10 Cookies 和 Session

## 10.2 Sessions 和 无状态协议

网页浏览器（客户端）和服务器之间的通讯都是被封装在HTTP协议中的。就如同之前所提及的，HTTP是无状态协议，这个意味着每次运行网页浏览器的客户端电脑，向某个资源进行请求(HTTP _get_)或者提交(HTTP _post_)的时候，都必须与服务器建立一个新的连接(TCP 连接)。

由于在客户端和服务器之间没有持久性的连接，所以在两端的软件就不能简单的依靠这种连接来保持 _会话状态(session state)_。例如，客户端每次都需要告诉服务器端目前是哪个用户在当前的电脑上登陆的。这被认为是客户端和服务器之间的一种 _对话_ 模式，这也是 _会话 session_ 的基础 —— 一种半持久性的信息交换。作为一种无状态协议，HTTP要持有会话状态是具有挑战性的，但是幸运的是，目前已经有数种技术让我们可以绕过这个问题。

目前持有状态最常用的方法是将会话ID用cookie的形式存储在客户端的电脑上。会话ID可以被认为是一个在特定的web应用程序上能标示当前会话的唯一性的令牌(一个字符的序列，或者是一个 _字符串 string_)。这个解决方案，并不会将所有的信息(例如用户登陆名、姓名、密码等)都使用cookie存储在客户端上，只有会话ID才会被存储，并且这个ID对应着服务器上的一个数据结构。在这个数据结构中，你可以存放你所需要的所有信息。这是一个 **安全得多** 的方法来存储用户信息，因为这种情况下，即使是使用不安全的客户端或者连接被监听也不能破坏会话中的信息。

如果你正在使用一个正确配置的现代浏览器，那么它就应该是支持cookie的。目前绝大部分的网站都会在你访问的时候创建一个新的 _会话 session_。你现在就可以自己查看一下——请查看下方的截图。在谷歌Chrome浏览器中，你可以使用Chrome开发者工具来查看当前访问的网站所建立的cookie，你可以在 _Chrome_ 的菜单中的 _更多工具_ 下，找到 _开发者工具_ 的选项。在开发者工具面板打开情况下，请点击 _Application_ 页片，然后在左下方的 _Storage_ 菜单下找到 _Cookies_ 选项。如果你是在打开 Rango 页面的状态下，进行的操作，那么你就会发现一个名字为 `sessionid` 的cookie。这个`sessionid` cookie包含了一串的字母和数字，这个就是Django用来识别当前电脑会话的唯一性标志。使用这个会话ID，你的会话的所有细节信息就能被访问到了——但是这些信息仅仅是在 _服务器端_ 存储的。

> ### 如果没有cookie
>
> 另一个不使用cookie来持久化状态信息的方法，就是将会话ID编码后放入网络地址 URL 中。例如你可能曾经在PHP驱动的网站上看到过类似如下这样的地址：
> `http://www.site.com/index.php?sessid=someseeminglyrandomandlongstring1234`
>
> 这意味着你就不需要在客户端存储cookie了，但是访问地址将会变得非常丑陋。这种形式的访问地址违反了Django的原则——简单、人性化的访问地址。

## 10.3 在Django中配置Session

虽然在默认情况下，session的功能应该已经被正确设置，并且能够正常使用了，但是详细了解Django的哪些模块提供了哪些对应的功能，是学习Django很好的实践过程。对于session这个功能来说，是由Django的 _中间件middleware_ 来实现的。

让我们按照顺序来检查每一个功能吧，先打开你Django项目文件夹下的`setting.py` 文件。在这个文件中，你能找到一个名为`MIDDLEWARE`的列表，在这个列表中，可以找到一个用字符串`django.contrib.sessions.middleware.SessionMiddleware`表示的模块。如果你没有在列表中看到它，那么现在就马上把它加入这个列表。这个名为`SessionMiddleware`的中间件，就是负责建立唯一`sessionid` cookie的功能模块。在设计上，SessionMiddleware 中间件模块，是可以非常灵活的支持各种不同的方式来存储会话信息的。这里举例了几个不同的解决方案——你可以把所有的信息都存到一个文件里面，或者数据苦，甚至可以存储在内存缓存区中。最为直接的解决方案就是使用`django.contrib.session`应用来将会话信息，通过Django的模型/数据库机制存储起来(使用的是`django.contrib.sessions.models.Session`这个模型)。如果要使用这个解决方案，请确保在你的Django项目的`setting.py`里的INSTALLED_APPS这个元组里已经加入了`django.contrib.sessions`。请记住，如果你是现在才将这个应用添加到你的项目中去的话，请使用之前使用过的数据库迁移(migration)指令来更新你的数据库。

> ### 会话缓存
>
> 如果你希望实现更加好的性能表现，那么你可能会考虑使用缓存的方式来存储你的会话信息。你可以查看Django的官方文档来实现这个功能。

## 10.4 用 cookie 来尝试 session

虽然几乎所有的现代浏览器都已经支持了cookie，但是还是会有部分cookie会被你的浏览器所拦截，这是由于浏览器的安全等级设置所引起的。在我们继续之前，请务必检查一下你的浏览器，确保能够正确使用cookie功能。然后你就已经做好能够继续学习的准备工作了。

### Cookie的功能测试

我们可以使用一些由Django 的 `request` 对象所提供的便捷方法，来测试我们的cookie。有三个核心方法我们需要关注的，分别是`set_test_cookie()`, `test_cookie_worked()`, 以及 `delete_test_cookie()`。在一个视图中，可以设置测试cookie， 然后在另一个视图中测试这个cookie，确认它是正确存在的。之所以需要两个不同的视图才能进行这个测试，那是因为我们需要等一会儿才能看到客户端是不是从服务器端接受到的cookie。

我们将会使用两个已存在的视图来完成这个练习，`index()` 和 `about()`。 我们不会直接在页面上显示任何信息，而是会在Django的开发服务器上，通过终端来输出验证，cookie是不是已经正确工作了。

在Rango的 `views.py` 文件中，找到 `index()` 视图方法。然后请将以下语句添加到方法中去。为了确保这个语句被执行，你可以把它放到视图方法的第一句。

```python
request.session.set_test_cookie()
```

同样的，请在 `about()` 视图方法的第一句加入以下的语句。

```python
if request.session.test_cookie_worked():
    print(‘TEST COOKIE WORKED’)
    request.session.delete_test_cookie()
```

在保存了这个小小的变化以后，你就可以启动Django 开发服务器了，然后导航到Rango的主页 `http://127.0.0.1:8000/rango/` 。然后再访问 about 页面，你就可以在运行Djangp开发服务器的终端窗口里看到 `TEST COOKIE WORKED` 这个输出了，如以下截图 所示。

如果这个信息没有被显示，请检查你浏览器的安全设置，有可能是安全设置的问题，导致浏览器拒绝保存cookie。

## 10.5 在客户端的cookie： 站点计数器的例子

现在，我们已经基本知道了cookie是如何工作的，下面我们将会实现一个非常简单的站点计数器。要实现这个功能，我们需要建立2个cookie：一个用来跟踪当前用户访问了多少次我们的Rango应用；另一个用来追踪这个用户最后一次访问我们站点的情况。通过保存最后一次访问的日期和时间，我们就可以设定规则每个用户每天只计数一次，这样就能一定程度上来避免用户使用垃圾信息来增加访问次数了。

在这里我们认为设定用户在Rango站点的入口就是首页，这个是为了简化需求的设定。打开Rango的 `wiews.py`，让我们先建立一个处理函数来处理cookie(`visitor_cookie_handler()`)，这个函数需要同时处理 `request` 和 `response` 对象。然后我们就可以在Rango的 `index()` 中使用这个函数了。 请在 `views.py` 文件中增加下述的函数。请留意，从技术上来看，这个函数并不是视图函数，因为它没有返回一个 `response` 对象，它仅仅是一个帮助函数。

```python
def visitor_cookie_handler(request, response):
    # Get the number of visits to the site.
    # We use the COOKIES.get() function to obtain the visits cookie.
    # If the cookie exists, the value returned is casted to an integer.
    # If the cookie doesn’t exist, then the default value of 1 is used.
    visits = int(request.COOKIES.get(‘visits’, ‘1’))

    last_visit_cookie = request.COOKIES.get(‘last_visit’, str(datetime.now()))
    last_visit_time = datetime.strptime(last_visit_cookie[:-7], ‘%Y-%m-%d %H:%M:%S’)

    # If it’s been more than a day since the last visit...
    if (datetime.now() - last_visit_time).days > 0:
        visits = visit + 1
        #Update the last visit cookie now that we have updated the count
        response.set_cookie(‘last_visit’, str(datetime.now()))
    else:
        # Set the last visit cookie
        response.set_cookie(‘last_visit’, last_visit_cookie)

    # Update/set the visits cookie
    response.set_cookie(‘visits’, visits)
```

这个辅助函数同时使用了 `request` 和 `response` 对象来作为参数。这是因为我们需要从 `request` 中获取到传入的cookie，同时我们还需要在 `response` 中添加和更新cookie。在这个函数中，你可以看到我们调用了 `request.COOKIE.get()` 函数，这是由 Django 提供的一个进一步的辅助函数。如果对应的cookie存在，这个函数就会返回对应的值，如果不存在，我们可以提供一个默认值。我们获取到每个cookie所对应的值以后，就能计算现在和上次的最后一次访问之间差距的天数( `.days` )了。

如果你想测试这部分的代码，而又不想等待一整天的话，你可以把 `days` 改成 `seconds` ， 这样我们的计数器就能每秒就能更新一次了，而不是一整天。

**请注意，所以从cookie中取到的值，都是字符串 string 类型的** ，_千万不要认为存储了数字的cookie就会返回整数类型 integer_ 。你只能自己手动将取到的值转换成对应的正确类型，这是因为在cookie中已经没有多余的空间来存储对应值的类型了。

如果这个cookie不存在的话，你可以使用 `response` 对象的 `set_cookie()` 方法来进行创建。这个方法需要两个参数，第一个是你想创建的cookie的名称(字符串类型)，第二个是你想存入这个cookie的值。需要注意的是，这个情况下，无论你输入的值是什么类型的，都会被自动转换成字符串类型。

既然我们在代码中使用了 `datetime` ，那么我们需要在 `views.py` 的头部增加以下语句。

```python
from datetime import datetime
```

下一步，我们需要更新 `index()` 这个视图方法来应用 `cookie_handler_function()` 这个函数。要实现这个目的，我们要提前取得 `response` 对象。

```python
def index(request):
    category_list = Category.objects.order_by('-likes')[:5]
    page_list = Page.objects.order_by('-views')[:5]
    context_dict = {'categories': category_list, 'pages': page_list}

    # Obtain our response object early so we can add cookie information.
    response = render(request, 'rango/index.html', context_dict)

    # Call helper function to handle the cookies
    visitor_cookie_handler(request, response)

    # Return response to user, updating any cookies that need changed.
    return response
```

现在打开Rango的首页，并且打开你浏览器提供的cookie检查器(比如：谷歌浏览器的开发者工具)，你就可以看到 `visits` 和 `last_visit` 这两个cookie。上面的截图显示了操作中的cookie信息，如果你不想使用开发者工具，你可以直接在 `index.html` 模板中加入 `<p>visits: {{ visits }}</p>` 语句，就能在页面上显示访问数量了。

## 10.6 会话数据

上一个例子，我们显示了如何存储和操作客户端的cookie——或者说在客户端存储的cookie。但是存储Session信息更安全的做法是是将相关的数据存储在服务器端。我们可以在客户端匿名存储SessionID的cookie，然后用这个cookie作为主键来访问相关数据。

要使用基于会话的cookie，你需要先做完以下几个步骤：

- 确认在 `setting.py` 的 `MIDDLEWARE_CLASSES` 列表变量中，包含了 `django.contrib.sessions.middleware.SessionMiddleware` 。

- 配置你 `session` 的后端支持。请确认 `django.contrib.sessions` 已经在你的 `setting.py` 文件的 `INSTALLED_APPS` 的列表变量中了。如果没有，请现在把它加上，并且运行 `python manage.py migrate` 命令来更新数据库。

- 默认情况下，基于数据库的后端将会被建立，但是你可能会考虑使用其他的方案(比如基于缓存)来部署，这种情况下，请参考[Django 官方文档：使用其他配置的Session后端](https://docs.djangoproject.com/en/2.0/topics/http/sessions/)

