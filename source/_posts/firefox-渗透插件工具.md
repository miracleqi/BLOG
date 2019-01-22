title: firefox 渗透插件工具
author: MiracleQi-温柔魔君
tags:
  - firefox
categories:
  - browser
date: 2016-07-11 17:01:00
cover: /img/post-cover/26.jpg
---
列举 19 个 firefox 插件工具

# 背景

Firefox 是一个出自 Mozilla 组织的流行的 web 浏览器。Firefox 的流行并不仅仅是因为它是一个好的浏览器，而是因为它能够支持插件进而加强它自身的功能。   
Mozilla 有一个插件站点，在那里面有成千上万的，非常有用的，不同种类的插件。一些插件对于渗透测试人员和安全分析人员来说是相当有用的。这些渗透测试插件帮助我们执行不同类型的攻击，并能直接从浏览器中更改请求头部。对于渗透测试中涉及到的相关工作，使用插件方式可以减少我们对独立工具的使用。  

在这篇简明的文章中，我们列举了一些流行的和有趣的 Firefox 插件，这些插件对渗透测试 人员来说是非常有用的。这些插件是多样的，有信息收集工具，也有攻击攻击。使用那些你认为有用的插件就可以了。这里面也有一些需要额外付费的插件，比如 Dominatorpro,它就需要从官方购买。请看下面的列表。

对安全研究人员和渗透测试人员有用的 Firefox 插件

# 插件列表

## 1.FoxyProxy Standard

 FoxyProxy 是一个高级的代理管理插件。它能够提高firefox的内置代理的兼容性。这儿也有一些其它的相似类型的代理管理插件。但是它可以提供更多的功能。基于 URL的参数，它可以从一个或多个代理之间转换。当代理在使用时，它还可以显示一个动画的图标。假如你要想看这个工具使用过的代理，你就可以查看它的日 志。 
 
 链接地址：https://addons.mozilla.org/en-US/firefox/addon/foxyproxy-standard/

## 2.Firebug

 Firebug是一个好的插件，它集成了 web 开发工具。使用这个工具，你可以编辑和调试页面上的 HTML,CSS 和 javascript，然后查看任何的更改所带来的影响。它能够帮助我们分析 JS 文件来发现 XSS 缺陷。用来发现基于 DOM 的 XSS 缺陷，Firebug 是相当有用的。
 
 链接地址：https://addons.mozilla.org/en-US/firefox/addon/firebug/

## 3.Web Developer

 Web Developer 是另外一个好的插件，能为浏览器添加很多 web 开发工具。当然在渗透渗透测试中也能帮上忙。
 
 链接地址：https://addons.mozilla.org/de/firefox/addon/web-developer/

## 4.User Agent Switcher

 该插件是在浏览器上增加一个菜单和一个工具条按钮。如果你想改变 useragent, 使用这个工具条和按钮就可以了。该插件可以帮助我们在执行一些攻击时做到欺骗的目的。  
 
 链接地址：https://addons.mozilla.org/en-US/firefox/addon/user-agent-switcher/

## 5.Live HTTP Headers

 该插件是相当有用的渗透测试插件。它实时的现实每一个 http 请求和 http 响应的 headers.当然你也可以通过点击位于左侧角落的按钮来保存 header 信息。多余的话就不多说了。重要性大家都知道。
 
 链接地址：https://addons.mozilla.org/en-US/firefox/addon/live-http-headers/

## 6.Tamper Data

 Tamper Data 和上面的 LiveHTTP Header 类似。但 Temper Data 有 header 编辑的功能。使用该插件，你可以查看，编辑 HTTP/HTTPSHeader 和 post 参数。它还可以通过更改 headerdata 被用于执行 XSS 和 SQL 注入攻击。
 
 链接地址：https://addons.mozilla.org/en-US/firefox/addon/tamper-data/

## 7.Hackbar

 Hackbar 是一个简单的渗透测试工具。它能帮助我们测试简单的 SQL 注入和 XSS 漏洞。你不能使用它来执行标准的 exploits，但是你可以使用它来测试缺陷存在与否。你可以手动的提交带有 GET 和 POST 的表单数据。它还有加密和编码的功能。大部分情况下，这个工具可以帮助我们使用编码的 payload 测试 XSS 缺陷。它还支持键盘快捷键方式来执行多种任务。我很确定，大多数安全领域的伙计们都知道这个工具。这个工具能用来发现 POSTXSS 缺陷。因为它可以手动发送 POSTData 到任何你喜欢的页面。这样的话，你就可以绕过客户端页面的验证。如果你的 payload 将在客户端编码，你可以使用编码工具来编码你的 payload,然后执行攻击。如果应用易受到 XSS 攻击，我非常确信你将在 Hackbar 的帮助下找到这个缺陷点。
 
 链接地址：https://addons.mozilla.org/en-US/firefox/addon/hackbar/

## 8.WebSecurity

 WebSecurity 是一个不错的渗透测试工具。我们已经在前面的文章中介绍过这个工具栏。WebSecurity 可以检测大多数常见的web应用缺陷。这个工具可以容易的检测 XSS，SQL 注入和其它 web 应用缺陷。不像其它所列举的工具，websecurity 完完全全是一个渗透测试工具。
 
 链接地址：https://addons.mozilla.org/en-us/firefox/addon/websecurify/

## 9.Add N Edit Cookies

 Add N Edit Cookies 是一个 cookie 编辑插件，它允许你在浏览器中添加和编辑 cookie 数据。使用这个插件，你可以轻松的手动添加 session 数据。这个工具可以在当你拥有活动的用户的 session 数据时执行 session 劫持攻击。编辑你的 cookie 添加数据并劫持该帐户。
 
 链接地址：https://addons.mozilla.org/en-US/firefox/addon/add-n-edit-cookies-13793/

## 10.XSS Me

 跨站点脚本攻击是最常见的 web 应用缺陷。在一个 web 应用中检测 XSS 缺陷，这个插件应该是一个有用的工具。XSSMe 常常用于发现反射型的 XSS 缺陷。它扫描页面中所有的表单，然后在所选择的页面上使用预定义的 XSSPayloads 执行攻击。在扫描完成以后，它会列出所有的页面，这些页面会显示 payload.这些页面可能易受到 XSS 攻击。现在你可以手动测试 web 页面去发现 XSS 缺陷存在与否。
 
 链接地址：https://addons.mozilla.org/en-us/firefox/addon/xss-me/

## 11.SQL Inject Me

 SQL Inject Me 也是一个不错的 Firefox 插件，常常被用于查找 Web 应用的 SQL 注入缺陷。这个工具不能利用缺陷，但是能够显示它是存在的。SQL 注入是最具伤害的 web 应用缺陷之一，它孕育攻击者查看，更改，编辑，添加或删除数据库中的记录。这个工具向表单中发送一些未被过滤的字符串，然后尝试搜索数据库的错误信 息。如果它发现数据库的错误信息，它就会标记该页面是易受攻击的页面。QA 测试人员可以使用这个工具作为 SQL 注入的测试。
 
 链接地址：https://addons.mozilla.org/en-us/firefox/addon/sql-inject-me/

## 12.FlagFox

 FlagFox 是另外一个有趣的插件。一旦安装到浏览器，它就会显示一个国旗用来告知 web 服务器的位置。它同时也包含其它功能， 如：whois, WOTscorecard 和 ping. 
 
 链接地址：https://addons.mozilla.org/en-us/firefox/addon/flagfox/

## 13.CrytoFox

 CrytoFox 是一个加密和解密的工具。它支持绝大多数的加密算法。因此你可以轻易的使用支持的加密算法加密和解密数据。这个插件有字典攻击的支持，可以破解 MD5的密码。虽然对它的评论不太好，但它的作用还是令人满意的。
 
 链接地址：https://addons.mozilla.org/en-US/firefox/addon/cryptofox/

## 14.Access Me

 Access Me 是另外一个专业的安全测试插件。这个插件是由 XSS Me 和 SQLInject Me 同一家公司开发的。该插件是用来测试web应用的访问缺陷的。这个工具是通过发送一些不同版本的页面请求来工作的。带有 HTTPHEAD 的请求和由 SECCOM 组成的请求将会被发送。一个有 session 和 HEAD/SECCOM 的集合同样也会被发送。
 
 链接地址：https://addons.mozilla.org/en-US/firefox/addon/access-me/

## 15.SecurityFocus Vulnerabilities search plugin

 该插件不是一个安全工具，而是一个搜索插件，让用户从 SecurityFocus 的数据库来搜索相关的缺陷点。
 
 链接地址：https://addons.mozilla.org/en-us/firefox/addon/securityfocus- vulnerabilities-/

## 16.Packet Storm search plugin

 这是另外一个搜索插件，让用户从 packetstormsecurity.org 站点搜索工具和相关利用。这个站点提供最新的免费的安全工具，利用和公告。
 
 链接地址：https://addons.mozilla.org/en-us/firefox/addon/packet-storm-search-plugin/

## 17.Offset Exploit-db Search

 这个插件和上面两个类似。它也是让用户从 exploit-db.com 站点搜索缺陷和列举的利用。当然这个站点提供的东东也是最新。
 
 链接地址：https://addons.mozilla.org/en-us/firefox/addon/offsec-exploit-db-search/

## 18.Snort IDS Rule Search

 这个插件也是一个搜索插件。用户可以利用这个插件从 snort.org 站点搜索 SnortIDS rules. Snort 是世界范围内部署最广泛的 IDS/IPS 技术。它是开源的网络入侵预防和检测系统，超过 400000 用户在使用该技术。
 
 链接地址：https://addons.mozilla.org/en-US/firefox/addon/snort-ids-rule-search/

## 19.Poster  

 用来 Post 和 Get 数据。

 链接地址：https://addons.mozilla.org/fr/firefox/addon/2691