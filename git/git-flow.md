git-flow 模式会预设两个主分支在仓库中：

* <strong>master </strong>只能用来包括产品代码。你不能直接工作在这个 master 分支上，而是在其他指定的，独立的特性分支中（这方面我们会马上谈到）。不直接提交改动到 master 分支上也是很多工作流程的一个共同的规则。
* <strong>develop </strong>是你进行任何新的开发的基础分支。当你开始一个新的功能分支时，它将是_开发_的基础。另外，该分支也汇集所有已经完成的功能，并等待被整合到 master 分支中。

* <strong>feature/rss-feed</strong> 开发一个新功能 “rss-feed”

* <strong>hotfix/missing-link</strong> 修复release（master）上问题