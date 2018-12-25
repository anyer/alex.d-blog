# Alex.D-Blog

![node-v8.11.2][1]
![npm-v5.6.0][2]
![NexT-v6.4.2][5]
![Hexo-v3.7.1][3]
![gulp-v3.9.1][4]

个人Hexo博客资源文件，博客地址: https://anyer.github.io/alex.d-blog/



------

### **使用说明**

```bash
# 拉取项目到本地 在目录 `.\source\_posts` 下放置需要发布的博文md文件

# 安装需要的模块（国内推荐使用cnpm install，需要提前安装cnpm)
npm install

# 生成静态文件（可缩写  hexo g）
hexo generate

# 静态资源打包
gulp

# 本地运行 （可缩写 hexo s）
hexo server

# 远程部署 （可缩写 hexo d）
hexo deploy

# 2018-12-25 更新部署命令(package.json中新增scripts)
npm run push  # 等价于命令 hexo cl && hexo g && hexo d

```



[1]: https://img.shields.io/badge/node-v8.11.2-green.svg
[2]: https://img.shields.io/badge/npm-v5.6.0-brightgreen.svg
[3]: https://img.shields.io/badge/hexo-v3.7.1-blue.svg
[4]: https://img.shields.io/badge/gulp-v3.9.1-orange.svg
[5]:https://img.shields.io/badge/NexT-v6.4.2-red.svg