# git flow 基于git的版本控制
## 安装
1.gitflow: 基于 git 的工作流程工具, 使用多分支完成版本的开发/合并(develop), 以及 hotfix 的发布
  - gitflow 是 git 命令的一系列组合

2.git flow init: 初始化项目, 其实还是 git 项目, 不过在分支上配置了 gitflow 的流程
  - master: 主线分支/正式环境/线上环境分支
  - develop: 测试分支/测试环境/本地环境
  - hotfix: 对线上环境的 bug 修复
  - feature: 功能分支, 在向线上添加一个功能时, 在 feature fun-name 完成功能的开发, 然后合并到 develop, 测试通过后发布到 master

3.git flow feature start fun-name: 开始一个功能 fun-name 的开发, 自动创建一个
  - git flow feature finish fun-name: 结束 fun-name 功能的开发, 合并到 develop 分支
  
4.git flow release start 1.1.5: 生成一个新的 release
  - 一般此时, 代码已经经过完整的测试, 包含版本更新和修复
  - git flow release finish 1.1.5: 发布 release
  - git pull 获取最新更新
  - release 合并到 develop/master
  - 添加更新标记等, 更新到 master
  
5. hotfix
 - git flow hotfix start missing-link: 修复正式版本中的问题(基于 master 分支)
 - git flow hotfix finish missing-link: 完成修复, 提交到master