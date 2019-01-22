title: 对于 hexo Annie 主题部分修改
author: MiracleQi-温柔魔君
tags:
  - hexo-Annie
categories:
  - BLOG
cover: /img/post-cover/10.jpg
date: 2019-01-03 16:03:00
---
修改部分 Annie 主题的设置

## 字体
### 默认字体
Annie 默认是繁体字，改为默认是简体字
```
修改 Annie\source\js\chinese.js 文件的第五行
原文：
var zh_choose = 't';
改为：
var zh_choose = 's';
```
### 字体切换
在页面控制字体切换
```
修改 Annie\layout\_partial\footer.ejs 第 17 行

原文：
		<p>
			<%- link_to("http://hexo.io/", "Hexo", {external: true})%> Theme <%- link_to("https://github.com/Sariay/hexo-theme-Annie", "Annie", {external: true})%> by Sariay. 				
		</p>
改为：
		<p>
			<%- link_to("http://hexo.io/", "Hexo", {external: true})%> Theme <%- link_to("https://github.com/Sariay/hexo-theme-Annie", "Annie", {external: true})%> by Sariay. 		
			<a href="javascript:zh_tran('s');" class="zh_click" id="zh_click_s">简体</a> 
			<a href="javascript:zh_tran('t');" class="zh_click" id="zh_click_t">繁體</a>		
		</p>
```
### 添加备案号
在上面字体切换处，添加如下备案信息
```
<a href="http://shcainfo.miitbeian.gov.cn/publish/query/indexFirst.action" target="_blank">沪ICP备16011274号</a>
```