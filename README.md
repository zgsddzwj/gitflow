# Git 规范

所有使用了本规范的项目，必须严格规范操作，否则不予以合并代码、提测、打包上线等后续操作。

### 基本要求
* 所有commit必须有注释，**内容必须按照注释格式严格执行！**
* 合理控制提交内容的颗粒度，一次commit含一个独立功能点。严禁一次提交涵盖多个功能项。
* 正确为每个项目设置Git提交用到的user.name和user.email信息，以公司邮箱为准，不可随意设置以影响无法正确识别。 查看当前项目配置信息的命令：`git config -l`

### 版本号(tag)
* 版本号(tag)命名规则：`主版本号.次版本号.修订号`，如`2.1.13`。(遵循GitHub[语义化版本](https://semver.org/lang/zh-CN/)命名规范)
* 版本号仅标记于master分支，用于标识某个可发布/回滚的版本代码
* 对master标记tag意味着该tag能发布到生产环境
* 对master分支代码的每一次更新(合并)必须标记版本号
* 仅项目管理员有权限对master进行合并和标记版本号

### 项目权限
Git权限分管理员、开发者、浏览者三种类型，可以在Gitlab上设置每个项目的项目权限


![gitlab_role.png](https://upload-images.jianshu.io/upload_images/4822184-b4397df1b304add5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


* 浏览者(Guest)只能浏览代码，无push、pull request等所有写权限
* 开发者(Developer)拥有浏览、push非主分支、提交pull request工单权限
* 管理员(Master)拥有建立和管理Git项目、合并分支和代码、给master打tag版本号等权限

### 分支使用
* 每个Git项目固定含有上述所有分支类型。主分支master和develop是保护分支，只能进行合并请求，均不可直接提交代码。
* 功能需求或常规Bug修复，请从develop拉取feature分支；线上紧急问题修复，请从master拉取hotfix分支。

### 代码提交
* 一个提交就代表解决一个问题
* 大问题适当地分解为多个小问题，以便每次小型提交都更易于理解

### 代码合并

将开发完毕的分支，拉取develop最新代码，merge并解决冲突后，之后在对应的feature分支创建并提交到develop分支，并自动触发merge request请求，然后进行code review，确认无误后再合并。    

**注意：**

* 每个merge request不要包含不相关的功能
* merge request提交后需要及时跟踪动态，包括通过、打回等
* 该功能进入提测流程后，需删除之前的功能分支

### 注释格式

每次提交，Commit message 都包括三个部分：Header，Body 和 Footer。

![code_comment.png](https://upload-images.jianshu.io/upload_images/4822184-89a8f14821ef45a5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


其中，`Header` 是必需的，`Body` 和 `Footer` 可以省略。不管是哪一个部分，任何一行都不得超过72个字符。这是为了避免自动换行影响美观。
#### Header
Header部分只有一行，包括三个字段：`type`（必需）、`scope`（可选）和`subject`（必需）。

* `type`用于说明 commit 的类别，只允许使用下面7个标识。

>* feat：新功能（feature）
* fix：修补bug
* docs：文档（documentation）
* style： 格式（不影响代码运行的变动）
* refactor：重构（即不是新增功能，也不是修改bug的代码变动）
* test：增加测试
* chore：构建过程或辅助工具的变动

* `scope`用于说明 commit 影响的范围，比如数据层、控制层、视图层等等，视项目不同而不同。

* `subject`是 commit 目的的简短描述，不超过50个字符。

以动词开头，使用第一人称现在时，比如change，而不是changed或changes
第一个字母小写
结尾不加句号（.）
#### Body
Body 部分是对本次 commit 的详细描述，可以分成多行, 有两个注意点:

* 使用第一人称现在时，比如使用change而不是changed或changes;

* 应该说明代码变动的动机，以及与以前行为的对比;

#### Footer
Footer 部分只用于两种情况:

* 如果当前代码与上一个版本不兼容，则 Footer 部分以BREAKING CHANGE开头，后面是对变动的描述、以及变动理由和迁移方法;

* 如果当前 commit 针对某个issue，那么可以在 Footer 部分关闭这个 issue (Closes #123, #245, #992), GitHub这个功能很好用；

Revert

还有一种特殊情况，如果当前 commit 用于撤销以前的 commit，则必须以revert:开头，后面跟着被撤销 Commit 的 Header。

> 为什么要约定注释格式？ 1. 加快 Reviewing Code 的过程 2. 帮助我们写好 release note 3. 5年后帮你快速想起来某个分支，tag 或者 commit 增加了什么功能，改变了哪些代码 4. 让其他的开发者在运行 git blame 的时候想跪谢 5. 其他小伙伴不会出现想抽你的冲动 6. 总之，一个好的提交信息，会帮助你提高项目的整体质量


## Git Flow

### 简介
　　`Git Flow`是构建在Git之上的一个组织软件开发活动的模型，是在Git之上构建的一项软件开发最佳实践。Git Flow是一套使用Git进行源代码管理时的一套行为规范和简化部分Git操作的工具。

![gitflow_main.png](https://upload-images.jianshu.io/upload_images/4822184-1b70ca8c0a9069d2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


工作流中涉及到的角色介绍：

+ 功能开发者：模块中功能的开发人员；
+ 开发管理员：由项目模块开发的小组长（team leader）担当；
+ 测试管理员：由测试团队指定人员担当；
+ 发布管理员：由生产环境发布团队指定人员担当；

### 分支说明

| 名称 | 说明 | 命名规范 |命名示例 |合并目标 |合并操作 |
| ------ | ------ | ------ | ------ | ------ | ------ |
| master | 线上稳定版本 | master | master | -- | -- |
| release | 待发布分支，下个版本需上线的版本 | release/xxx | release/v1.0.0 | master | merge request |
| develop | 当前正在开发的分支 | develop | develop | master | merge request |
| feature | 功能分支，每个功能需分别建立自己的子分支 | feature/版本号-功能名 | feature/v1.0.0-Login | develop | merge request |
| hotfix | 紧急修复分支 | hotfix/xxx | hotfix/v1.0.1 | master/develop | merge request |

### 分支约定
　　Git Flow有主分支和辅助分支两类分支。其中主分支用于组织与软件开发、部署相关的活动；辅助分支组织为了解决特定的问题而进行的各种开发活动。

#### 主分支
![git_master.png](https://upload-images.jianshu.io/upload_images/4822184-056668f897b82511.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



　　主分支是所有开发活动的核心分支。所有的开发活动产生的输出物最终都会反映到主分支的代码中。主分支分为master分支和develop分支。

##### master 分支
* master分支存放的是随时可供在生产环境中部署的稳定版本代码
* master分支保存官方发布版本历史，release tag标识不同的发布版本
* 一个项目只能有一个master分支
* **仅在发布新的可供部署的代码时才更新master分支上的代码**
* 每次更新master，都需对master添加指定格式的tag，用于发布或回滚
* master分支是保护分支，不可直接push到远程仓master分支
* master分支代码只能被release分支或hotfix分支合并

##### develop 分支
* develop分支是保存当前最新开发成果的分支
* 一个项目只能有一个develop分支
* develop分支衍生出各个feature分支
* develop分支是保护分支，不可直接push到远程仓库develop分支
* develop分支不能与master分支直接交互

每次将develop分支上的代码合并回master分支时，我们都可以认为一个新的可供在生产环境中部署的版本就产生了。基于此，理论上说，每当有代码提交到master分支时，我们可以使用Git Hook触发软件自动测试以及生产环境代码的自动更新工作。这些自动化操作将有利于减少新代码发布之后的一些事务性工作。



只有`开发管理员`有合并的权限

### 辅助分支
![git_assist.png](https://upload-images.jianshu.io/upload_images/4822184-024429e135c8d8d5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



　　辅助分支是用于组织解决特定问题的各种软件开发活动的分支。辅助分支主要用于组织软件新功能的并行开发、简化新功能开发代码的跟踪、辅助完成版本发布工作以及对生产代码的缺陷进行紧急修复工作。这些分支与主分支不同，通常只会在有限的时间范围内存在。跟“历史性”分支相反，这三类分支都是短期分支，针对他们的工作内容完成后，一般都要进行删除。

**工作内容完成的标识有两个：开发完成、合并完成，缺一不可。**

辅助分支包括：

* 用于开发新功能时所使用的`feature`分支
* 用于辅助版本发布的`release`分支
* 用于修正生产代码中的缺陷的`hotfix`分支

　　以上这些分支都有固定的使用目的和分支操作限制。从单纯技术的角度说，这些分支与Git其他分支并没有什么区别，但通过命名，我们定义了使用这些分支的方法。

##### feature 分支
使用规范：

* 分支的命名格式必须是版本号-功能名，例如`v1.0.0-login`
* develop分支的功能分支
* feature分支使用develop分支作为它们的父类分支
* 以功能为单位从develop拉一个feature分支
* 每个feature分支颗粒要尽量小，以利于快速迭代和避免冲突
* 当其中一个feature分支完成后，它会合并回develop分支
* 当一个功能因为各种原因不开发了或者放弃了，这个分支直接废弃，不影响develop分支
* feature分支代码可以保存在开发者自己的代码库中而不强制提交到主代码库里
* 由每组开发管理员负责把所有feature分支开发完成的代码合并到develop分支
* feature分支只与develop分支交互，不能与master分支直接交互

　　如有几个同事同时开发，需要分割成几个小功能，每个人都需要从develop中拉出一个feature分支，但是**每个feature颗粒要尽量小**，因为它需要我们能尽早merge回develop分支，否则冲突解决起来就没完没了。同时，当一个功能因为各种原因不开发了或者放弃了，这个分支直接废弃，不影响develop分支。

##### release 分支
使用规范：

* 命名规则：`release/*`，“*”以本次发布的版本号为标识
* release分支主要用来为发布新版的测试、修复做准备
* 当需要为发布新版做准备时，从develop衍生出一个release分支
* release分支可以从develop分支上指定commit派生出
* release分支测试通过后，合并到master分支并且给master标记一个版本号
* **release分支一旦建立就将独立，不可再从其他分支pull代码**
* 必须合并回develop分支和master分支

　　release分支是为发布新的产品版本而设计的。在这个分支上的代码允许做小的缺陷修正、准备发布版本所需的各项说明信息（版本号、发布时间、编译时间等）。通过在release分支上进行这些工作可以让develop分支空闲出来以接受新的feature分支上的代码提交，进入新的软件开发迭代周期。

　　当develop分支上的代码已经包含了所有即将发布的版本中所计划包含的软件功能，并且已通过所有测试时，我们就可以考虑准备创建release分支了。而所有在当前即将发布的版本之外的业务需求一定要确保不能混到release分支之内（避免由此引入一些不可控的系统缺陷）。

　　成功的派生了release分支，并被赋予版本号之后，develop分支就可以为“下一个版本”服务了。所谓的“下一个版本”是在当前即将发布的版本之后发布的版本。版本号的命名可以依据项目定义的版本号命名规则进行。

##### hotfix 分支
使用规范：

* 命名规则：`hotfix/*`，“*”以本次发布的版本号为标识
* hotfix分支用来快速给已发布产品修复bug或微调功能
* 只能从master分支指定tag版本衍生出来
* 一旦完成修复bug，必须合并回master分支和develop分支
* master被合并后，应该被标记一个新的版本号
* hotfix分支一旦建立就将独立，不可再从其他分支pull代码

　　除了是计划外创建的以外，hotfix分支与release分支十分相似：都可以产生一个新的可供在生产环境部署的软件版本。

　　当生产环境中的软件遇到了异常情况或者发现了严重到必须立即修复的软件缺陷的时候，就需要从master分支上指定的TAG版本派生hotfix分支来组织代码的紧急修复工作。

　　这样做的显而易见的好处是不会打断正在进行的develop分支的开发工作，能够让团队中负责新功能开发的人与负责代码紧急修复的人并行的开展工作。
　　
## 版本管理

我们使用 `Git Flow` 来进行版本管理控制，它相对于 `GitHub Flow` 更适合在产品开发中快速迭代，这种代码管理模式应该已经广泛使用了。

另外，我们鼓励使用 Git 客户端 `SourceTree`，它集成了 Git Flow 的一些基本操作。如果严格遵循 Git Flow 的流程进行版本管理控制，那么我们只用管开始和结束一个 `Feature/Release/Hotfix`，基本上是不用手动 merge 分支的。

![gitflow_branch.jpg](https://upload-images.jianshu.io/upload_images/4822184-92091dee2e1f3df7.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


### 新功能开发流程
1. 从 develop 分支创建 feature 分支；
1. 开发调试完将 feature 分支提交到远程版本库；
1. 提交 pull request 请求合并到 develop 分支；
1. 相关负责人 code review 后如果同意合并后，删除远程 feature 分支，如果不同意，重新修改后再上传 feature 分支请求 pull request。

## Pull Request

Pull Request是当`功能开发者`完成一个新功能后向`项目维护者`发送合并请求通知的机制。它的使用过程如下：

![pull_request.png](https://upload-images.jianshu.io/upload_images/4822184-3e5ff2b5538426e5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


1. `功能开发者`可以通过[Gitlab页面](https://gitlab.enncloud.cn)发送pull request
2. `开发管理员`自己或组织其他的团队成员审查、讨论和修改代码
3. `开发管理员`合并新增功能分支到develop分支，然后关闭pull request，并且可以选择删除新增分支

## 工作流程

1⃣️ 由`开发管理员`负责在Gitlab上创建空白的仓库，并clone到本地，在sourcetree的git flow菜单中选择初始化仓库，并push到远端。

![init_repo.png](https://upload-images.jianshu.io/upload_images/4822184-d3481bd149c67dd5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


2⃣️ 在Gitlab上设置保护分支，把master、develop分支保护起来，只有指定人可push。

3⃣️ `功能开发者`clone代码到本地，先在sourcetree的git flow菜单中选择初始化仓库。

![init_repo.png](https://upload-images.jianshu.io/upload_images/4822184-d3481bd149c67dd5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

4⃣️ 然后再开始新建功能分支，进行开发工作。

![new_feature.png](https://upload-images.jianshu.io/upload_images/4822184-5b950798a9fd2b9d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


5⃣️ 新功能开发全部完成或部分完成后，`功能开发者`把最新代码push到远端同样的新功能分支里，并在Gitflow发起pull request给`开发管理员`

6⃣️ `开发管理员`review代码，选择合并代码到develop，并可选择删除已经合并的新功能分支

7⃣️ 当`开发管理员`处理完合并请求后，开发者,切换到develop分支，直接删除自己的本地分支及远程分支，不要点击完成(Finish Feature)，此时开发者pull远端develop分支最新代码即可，可忽视本地的push提醒。
![delete_feature1.png](https://upload-images.jianshu.io/upload_images/4822184-a08a2e2c8b25c9cb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![delete_feature2.png](https://upload-images.jianshu.io/upload_images/4822184-75cb6fb1ab52dcc3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


8⃣️ release、hotfix分支和feature分支操作类似。

9⃣️ 不可点击完成新功能、完成发布版本、完成修复补丁，因为这样会导致自动合并代码到master或develop分支

![finish_feature_no.png](https://upload-images.jianshu.io/upload_images/4822184-6e3612bc757aeebc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



## SourceTree mac版本下载地址

SourceTree_2.3.1.zip

链接:[https://pan.baidu.com/s/1XHFvLh5MueebYjjGrEVcdQ](https://pan.baidu.com/s/1XHFvLh5MueebYjjGrEVcdQ)  密码:opjd

## SourceTree win版本下载地址

SourceTree2480.zip

链接:[https://pan.baidu.com/s/1z6UC7LrzJLNn9yeQnxoWyg](https://pan.baidu.com/s/1z6UC7LrzJLNn9yeQnxoWyg)  密码:7uac

windows下使用sourcetree需要安装一下软件，请在安装sourcetree前安装好：

Git-2.17.0-64-bit.exe

链接:[https://pan.baidu.com/s/1q0WQw03U9oCmhN5Fii7PNQ](https://pan.baidu.com/s/1q0WQw03U9oCmhN5Fii7PNQ)  密码:ab2n

mercurial-4.4.1-x64.msi

链接:[https://pan.baidu.com/s/1PBIRFFMPsIe3MoV_42dDzg](https://pan.baidu.com/s/1PBIRFFMPsIe3MoV_42dDzg)  密码:nvkx

安装SourceTree打开后会提示你Atlassian需要注册，这家软件公司在澳大利亚，所以注册时需要翻墙，才能注册成功，这里提供一个跳过注册的方法

1. 找到目录：C:\Users\用户\AppData\Local\Atlassian\SourceTree
2. 新建accounts.json文件里面输入下面代码块内容后，重新打开，就不会提示注册了！

```
[  
  {  
    "$id": "1",  
    "$type": "SourceTree.Api.Host.Identity.Model.IdentityAccount, SourceTree.Api.Host.Identity",  
    "Authenticate": true,  
    "HostInstance": {  
      "$id": "2",  
      "$type": "SourceTree.Host.Atlassianaccount.AtlassianAccountInstance, SourceTree.Host.AtlassianAccount",  
      "Host": {  
        "$id": "3",  
        "$type": "SourceTree.Host.Atlassianaccount.AtlassianAccountHost, SourceTree.Host.AtlassianAccount",  
        "Id": "atlassian account"  
      },  
      "BaseUrl": "https://id.atlassian.com/"  
    },  
    "Credentials": {  
      "$id": "4",  
      "$type": "SourceTree.Model.BasicAuthCredentials, SourceTree.Api.Account",  
      "Username": "",  
      "Email": null  
    },  
    "IsDefault": false  
  }  
]
```

## 推荐工具

* **Git Flow 扩展** Git Flow模型提出者nvie写的Git命令集扩展，提供了极出色的命令帮助以及输出提示。支持OSX，Linux和Windows平台。参考：[git-flow 备忘清单](http://danielkummer.github.io/git-flow-cheatsheet/index.zh_CN.html)

---
#### 参考资料
[Git 工作流与规范]([https://shockerli.net/post/git-flow-guide/](https://shockerli.net/post/git-flow-guide/)
)
[Commit message 和 Change log 编写指南]([http://www.ruanyifeng.com/blog/2016/01/commit_message_change_log.html](http://www.ruanyifeng.com/blog/2016/01/commit_message_change_log.html)
)
