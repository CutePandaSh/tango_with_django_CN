# 1. 概述

本书是基于Django和Python网站开发的实战型手册。本书主要是为初学者设计的，希望为初学者提供一个如何使用Django 2.0开发一个网站应用的含有详细步骤的攻略教程。

本书旨在对Django官方以及其他优秀的网上教程进行补充。通过将所有的内容整合在一起，实战开发的方法学习如何正确使用Django 2.0框架， 同时填补了不少官方文档中的坑。此外，本书还介绍了一些在网络应用开发中需要用到的其他的知识（例如，HTML、CSS、JavaScript 等等）。

## 1.1 为什么使用本书学习

**本书能节约你的时间**   我们经常能见到很多十分聪明的学生在学习Django和其他相关的网站应用开发工具时，耗费了大量的精力和时间，依然被卡在某个环节。其原因往往是因为某个关键知识点没有提供支持信息，或者说明的不够清晰。偶尔情况下，这样的问题会耽误你学习工作10-15分钟，更多时候解决这些问题需要耗费数个小时。我们试图尽可能的扫除这些障碍，帮助你尽快的投入到应用开发中，而不是泥足深陷在这些坑里。

**本书能降低你的学习曲线**  当然应用程序框架(Django)可以帮助你减少大量的麻烦和时间，前提是你必须准确知道如何使用他们！但是通常情况下，相关知识的学习曲线是非常陡峭。本书尝试着解释清楚如何将所有的知识整合在一起，从而帮助你能快速前进。

**本书能提升你的工作流程**  使用应用程序框架要求遵循特定的设计模式，所以这也要求需要将特定的代码块放入特定的位置。在和很多初学者一起工作以后，我们听到很多关于使用框架的抱怨，特别是如何摆脱框架的控制（即反转控制），我们创造了很多工作流来帮助你更好的聚焦在开发过程，这样你就能重新获得控制感，并更有规则的构建的网站应用。

**本书不是用来阅读的** 你可以按照你的设想做所有的事情，但是请不要仅仅阅读本书！这是一本教你如何动手用Django开发应用的指导书，阅读不是上手做。只有跟随本书真正动手完成开发了这个应用，你才能从练习中收获得更多。但是在你为这个应用实际编写代码的时候，请不要 *复制黏贴* 书中的代码。请手动输入每一行代码，思考每一行代码的作用，并阅读本书中所为你提供的相关解释，如果你依然无法理解，你可以尝试使用[Stack Overflow](https://stackoverflow.com/questions/tagged/django)或者其他有用的网站来帮助你解决问题，这样你才能弥补你知识中的不足。当然当你发现你无法跨过这道坎的时候，你也可以联系我们，这样我们可以更好的更新我们的资源，其实我们获得了许多其他读者的帮助和反馈。

## 1.2 你能从本书中学到什么

在本书中，我们将使用案例教学的方法，本书将会一步一步教你如何构建一个名叫 *Rango* （请查阅1.4 项目设计简述）的网站应用程序。在这个学习过程中，我们将向你展示如何完成以下关键性任务。

- **如何配置你的开发环境** ——包括如何使用 终端，虚拟环境，pip 安装程序，以及如何使用 Git 等等
- **安装Django项目** 以及如何创建一个基础的Django项目
- **配置Django项目** 来支持静态媒体及其他媒体文件
- **创建数据库模型** 使用Django所提供的对象关系映射（ORM）功能
- **创建表单** 这样你就能利用数据库模型来动态生成你的网站页面
- 使用Django提供的 **用户验证(user Authentication)** 功能模块
- 将 **外部服务(external services)** 整合进你的Django项目中去
- 在你的网站应用中使用 _层叠样式表（CSS）_ 和 _JavaScript_
- 让你应用中所使用的 **_CSS_** 显的更专业
- 在Django中使用 **Session** 和 **cookie**
- 在你的应用中使用更高级的内容，例如 **_AJAX_**
- 使用 _PythonAnyWhere_ 在网站服务器上 **部署你的应用**

在每一章的结尾处，我们提供了一些具有挑战性的练习，在让你更深入思考的同时，让你了解自己是否已经掌握了刚才所学的内容。本书的后面几章还提供了一些开放性的开发练习，同时包含了相应的解决方案和思路。

> ### 练习： _所有练习都会以这样的方式清晰展示_
>
> 在每一个单元我们都已经添加了一些练习来测试你是否已经掌握了知识点和相关技能。
> 你需要认真的完成这些练习，因为后续的章节能否很好的理解，依赖于这些知识和技能的掌握。
> 假如你在某个问题商卡住了，也请不要担心，你可以直接查询我们的 [Github 代码库](https://github.com/leifos/tango_with_django_19)，来寻找问题的答案。

## 1.3 相关技术和功能包

在本书的教程中，我们将会涉及以下的技术和外部功能服务包。

- Python 编程语言
- Pip 包管理
- Django
- Git 版本控制
- Github
- HTML
- CSS
- JavaScript
- JQuery 库
- Twitter Bootstrap 前端框架
- Webhose API 搜索接口
- PythonAnyWhere 主机部署服务

我们选择这些技术不仅仅是因为这些技术是网站应用开发的基础，而且为我们提供了很好的例子来向你展示，如何集成类似  _Bootstrap_ 的CSS工具组件，类似 _Webhose API_ 的第三方服务包，以及如何使用 _PythonAnyWhere_ 来快速部署你的网站应用。

## 1.4 Rango: 初始设计以及功能定义

在本书中，我们将会聚焦在如何开发一个应用，名叫 _Rango_ 。 我们在开发这个应用的过程中，将会学习到将来开发任何网站应用都会用到的核心组件。要想查看这个应用的完整功能，请访问 [How to Tango with Django 网站](http://www.tangowithdjango.com/)。

### 设计概述

现在你的客户向你提出了一个需求，需要创建一个名叫 _Rango_ 的网站。在这个网站上可以让用户通过用户定义的多个目录访问相对应的不同网站页面。在西班牙问中，_rango_ 的意思是“_质量排名协会_“或者“_社会阶层的位置_“

- 在 Rango 的主页 **main page** ，你的客户希望用户能看到：
    - 前 5 个浏览最多的页面
    - 前 5 个浏览最多（或者打分最多）的目录
    - 为访问者提供浏览和检索目录的功能
- 当用户浏览 目录页面 **category page** 的时候，你的客户希望 _Rango_可以显示：
    - 当前 _目录的名称_，_访问数量_, _喜欢数量_, 以及和当前目录相关的页面列表（显示页面名称，以及超链接到页面内的地址）
    - 以及提供*搜索功能*（通过搜索API）查询其他可以被加入当前目录的页面。
- 在特定的目录中，客户希望：*可以记录目录的名字*， *每个目录页面的被访问次数*，以及 *多少用户点击了喜欢* （即，页面被打分）。
- 每个目录需要可以通过具有*可读性*的地址进行访问，例如 `/rango/books-aboutdjango/`
- 只有 *注册用户才能在目录中添加和搜索页面*， 因此访客可以自己注册账户。

一眼看去，这个应用的开发似乎非常简单，本质上这就是一个网页链接分类目录的列表系统，但是，这个项目中还是有不少复杂的具有挑战的知识点需要我们关注的。首先让我们通过一些顶层设计，看看到底我们在项目中需要开发哪些细节。

> ### 练习：
>
> 在展开进一步工作之前，先让我们考虑一下以上对项目的需求定义，并做一些设计草案。
> - N层(N-Tier)和系统结构图(System Architecture diagram)
> - 首页和目录页的线框图(Wireframes)
> - 本应用的一系列地址映射(URL Mappings)
> - 用来描述我们需要实现的数据模型的实体关系(ER)图
>
> 在学习下面环节之前，请尝试着先完成这些练习，即使你并不了解系统结构图，线框图或者实体关系图，那就请考虑一下你该如何解释和描述哪些你准备开发的东西呢？

### N层结构 N-Tier Architecture

大多数网站应用的高层级结构使用的是3层结构。但是 _Rango_ 需要和第三方服务做接口，所以它的层次结构是一个非标准的变体。

![Rango应用程序3层结构概览图](https://s1.ax1x.com/2018/05/06/CU3j1K.png)

由于我们是使用Django来构建我们的网站应用，我们将会使用以下的技术来实现各个层次：

- **客户端（client）** 网页浏览器（例如 Chrome, Safari, Firefox），负责对 HTML／CSS 页面进行渲染
- **中间层（middleware）** 是 *Django* 应用，在我们开发的时候，将会使用Django网页服务器作为任务调拨
- **数据库（database）** 使用基于Python的 *SQLite3* 数据库引擎
- **搜索接口（Search API）** 就是搜索接口

在大部分的情况下，我们将会聚焦在如何开发中间层，但是很显然从系统结构图来看，我们要考虑所有的组件并与所有其他组件接口

### 线框图

向客户展现最终项目完成时的界面，线框图是一个很好的方法。它能节约大量的时间，并且你可以根据你所掌握的工具，选择向客户提供简单手绘草图，或是高精度仿制模型。对于我们的Rango应用来说，我们希望我们的首页和目录页能与下面的截图一致。
![首页，在左侧带有目录搜索条，并且显示前五的页面和目录](https://s1.ax1x.com/2018/05/06/CU0kZV.png)
![目录页显示了目录内的所有Page，以及查看数量。在下方进行了“python”的搜索，并显示了搜索结果](https://s1.ax1x.com/2018/05/06/CU03dK.png)

### 页面和地址映射 URL Mapping

根据需求定义，我们已经在我们的应用内确定了两个需要在不同的访问位置下向用户展现的页面。我们需要描述清楚 URL地址，用来让用户访问不同的页面。地址映射就是用户在浏览器地址栏中输入的地址文本，来浏览指定的页面。Rango的基础URL 地址映射如下。

- 用 `/` 或者 `/rango/` 来访问首页（入口页）

- `/rango/about/` 指向关于页

- `/rango/category/<category-name>/`,将会指向`<category-name>`所对应的目录页，它的值可能是会是：
    - games;
    - python-recipes;
    - code-and-compilers。

在构建我们的应用的时候，我们很可能需要创建其他的URL地址映射。但是上述所列的可以给我们一个起点，并且在我们创建其他页面的时候提供很好的思路。同时，随着本书逐步学习，我们将会使用Django框架和 模型-视图-视图模版 的设计思路来充实我们构建这些页面的方法。我们现在已经有了URL地址映射的关键点，以及页面未来的样子，现在我们要开始定义为我们的应用存储和提供数据的数据模型了。

### 实体关系图（ER图）

根据需求定义，很显然我们至少需要两个实体：_category_ 和 _page_ ， 并且一个 _category_ 可以容纳许多个 _page_。以此我们可以用以下的ER图来表示简单的数据模型。
![Rango应用两个主体的ER图](https://s1.ax1x.com/2018/05/06/CUBahF.png)
需要留意的是，这里有一些需求定义并不是很清晰，理论上来说一个 _page_ 应该可以属于1个或者多个 _category_ 。如果要满足这个需求，那么我们需要定义 _category_ 和 _page_ 为多对多的关系。然而这样的化，会让项目复杂很多，所以为了简化项目，我们在这里设定：一个 _category_ 可以包含多个 _page_，但是一个 _page_ 只能属于一个 _category_ 。其实这个并不影响一个页面需要存在于多个目录下这个功能，只是这个页面需要在数据库中建立多个记录，当然这个解决方案是有瑕疵的。

> ### 做好笔记
>
> 养成记录你曾做过的所有设定的习惯，就像我们现在设定的一对多的实体关系一样。你永远都不知道你做的设定会给你埋下多大的坑。记录下来，这让你可以通过于你开发团队成员之间的沟通来确保，你所做的设定是明智，所有人都可以在这个设定下进行工作。

依据这个设定，我们做了一些表格来描述各个实体的细节。这些表格说明了各个实体都拥有哪些字段。我们使用了Django的 `ModelField` 类型来定义各个字段的类型（即 `CharField`, `IntegerField`, `URLField` 以及 `ForeignKey`），请留意在Django中 *主键 primary keys* 是隐式的，以便 Django向每个模型添加了`id`，我们会在后面的 **数据库和模型** 章节深入讨论。

#### Category 模型

Field | Type
:-: | :-:
name| CharField
views| IntegerField
likes| IntegerField

#### Page 模型

Field | Type
:-: | :-:
category| ForeignKey
title| CharField
url| URLField
views| IntegerField

我们还需要有个 `User` 的模型，这样用户才能注册和登陆。我们现在不做讨论，但是会在用户验证部分进行介绍。在后续章节中，我们将会展示如何在 Django 中实例化这些模型，同时如何使用内建的 **ORM** 连结数据库。

## 1.5 总结

这些顶层设计和需求规范将会为我们的网站应用开发建立非常良好的参考点。虽然我们将主要关注如何使用特定的技术，但是这些方法在绝大部分数据库驱动的网站中都是非常常见的。所以熟悉如何阅读和制作这些需求规范和设计文档，能帮助你更好的和其他人沟通你的想法和设计，这是十分重要和有帮助的。在这里，我们将使用 Django 以及相关的技术来实现这些需求定义。

> ### 复制粘贴代码
> 随着本教程的进行，你很有肯能试图从书中直接复制代码，并粘贴到你自己的代码编辑器中去。**但是，请尽可能的自己手动输入所有的代码**。我们知道这个很无聊，但是这能帮助你更好的记住操作过程，以及那些你后面将会用到的命令。
>
> 此外，复制粘贴 Python 代码，你很可能在自找麻烦。书中的空白区域很可能被解释成 `space`，`tab` 或者 `space`和`tab`的混合体，这会导致大量奇奇怪怪的问题，而不一定仅仅是缩进错误。请特别留意，如果你正在使用Python 3，如果在缩进中混合使用 `space` 和 `tab` ，将会导致 `TabError`错误。
>
> 现在绝大部分的编辑器，都能够正确显示空白区域是使用的`tab`还是`space`，如果有这个功能，请打开它，这能帮你解决不少困惑。