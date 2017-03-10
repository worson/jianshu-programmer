# gitbook的使用
[仓库](https://github.com/GitbookIO/gitbook "仓库")
## 建立项目
```
gitbook init
```
## 运行
```
gitbook serve .
```
## 生成html
```
gitbook build . ./output
```
## 生成pdf
```
gitbook pdf .  # 重新执行命令生成pdf，目标文件为book.pdf
```
---
# 自定义python工具
## 需求
### 引用其他地方的文件
- 抽离出图片列表
- 获取对应的图片对指定的文件目录
- 将当前的markdown文件图片的url进行替，并保存到对应目录