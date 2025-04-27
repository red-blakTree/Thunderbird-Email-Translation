<p align="center">
  <img align="center" width="100" src="https://i.ibb.co/wzBTHGm/immersive-translate-Thunderbird-logo.png" />

  <h1 align="center">Thunderbird邮件翻译插件</h1>
  <h3 align="center">【沉浸式翻译】</h3>
</p>

<p align="center">❤❤❤❤❤❤❤❤❤❤❤❤❤❤❤❤</p>

Thunderbird 是免费的邮件客户端，注重隐私、界面清爽、支持中文、操作灵活便捷，但没有邮件内容翻译功能。扩展市场中的翻译插件也不尽人意，这里推荐太过好用的沉浸式翻译。Thunderbird 插件市场里没有这款插件，如果直接上传沉浸式翻译的插件包无法正常实现翻译功能，这时我们需要修改一下沉浸式翻译的插件代码得以实现在 Thunderbird 客户端内翻译邮件内容。

## 项目说明

本项目基于 [YGGYDW/Thunderbird-Email-Translation](https://github.com/YGGYDW/Thunderbird-Email-Translation) 进行了修改，以适配 Thunderbird 邮件客户端。以下是具体的修改步骤和方法：

## 方法：

<!-- toc -->

- [直接安装插件](#直接安装插件)
- [手动修改文件代码](#手动修改文件代码)
  - [下载插件](#沉浸式翻译官方下载Firefox插件)
  - [更改扩展名](#将下载后的文件扩展名xpi更改为zip后解压缩)
  - [要修改的文件](#找到压缩包内以下三个文件)
  - [修改background.js](#修改background文件)
  - [修改manifest.json](#修改manifest文件)
  - [修改options.js](#修改options文件)
  - [参考原代码修改差异](#参考原代码修改差异)
  - [重新打包](#根目录从新打成压缩包)
- [安装步骤](#安装步骤)

<!-- tocstop -->

## 直接安装插件

- 在右侧 Releases 中下载插件，或点击链接进入下载页面:<a href="https://github.com/YGGYDW/Thunderbird-Email-Translation/releases/tag/immersive-translate-ThunDerbird" target="_blank">Releases</a>

- 下载完后跳过第二步，[直接看第三步](#安装步骤)。

- 注意事项：Thunderbird 邮件客户端要求为最新版本<a href="https://www.thunderbird.net/zh-CN/thunderbird/all/" target="_blank">Thunderbird128.6.0esr</a>，请检查是否为最新版本。

## 手动修改文件代码

### 沉浸式翻译官方下载Firefox插件

<a href="https://immersivetranslate.com/zh-Hans/" target="_blank">下载</a>


<details>
  <summary><h4>✨点击查看图示✨</h4></summary>


![点击Firefox扩展](https://i.ibb.co/hMfcQ1z/Immersive-Translate1.png)

![点击“下载文件”](https://i.ibb.co/zHkf2kG/Immersive-Translate2.png)

</details>

> 如果下载的文件为.xpi文件,需要改成.zip后解压缩

### 找到压缩包内以下三个文件

- background.js

- manifest.json

- options.js

<details>
  <summary><h4>✨点击查看图示✨</h4></summary>

![解压缩后的文件内容](https://i.ibb.co/PY58Zd6/Immersive-Translate3.png)

</details>

### 修改background.js文件

- 搜索`browser_action`

- `找到[“browser_action”, “page_action”]这一项`

- 删掉`, “page_action”`

- 更改为`[“browser_action”]`

- （此处共 1 处需要修改）

- 搜索所有`.contextMenus`  

- 删除`context`
- 更改为`.Menus`
- (此处共 6 处需要修改)

- 添加以下代码在【主体】结尾处：

  bh().catch((e) => {});
  })();之下添加以下代码

```js
async function registerMsgDisplayScript() {
		await messenger.messageDisplayScripts.register({
			js: [{file: "/content_script.js"}, {file: "/content_start.js"}]
		});
	}
	registerMsgDisplayScript();
```

/\*! Bundled license information:之上添加以上代码

- （此处共 1 处需要修改）

### 修改manifest.json文件

- 搜索到`contextMenus`

- 将`"contextMenus",`

- 删掉其中的`context`

- 更改为`"Menus",`  

- `"Menus",` 下面一行添加新的代码

- `"messagesModify",`

- (此处共 1 处需要修改)

- 搜索到`"strict_min_version": "63.0"`

- `63.0`

- 更改为

- `128.0 `

- (此处共 1 处需要修改)

- （这个数字代表 Thunderbird 客户端的版本号，截至 2025 年 4 月 21 日 Thunderbird 的最新版本是 128.9.1esr，所以我这里更改为 128.0 是兜的住 128.9.1esr 这个版本的。Thunderbird 客户端版本不能低于 78.0。）

### 修改options.js文件

- 搜索到所有的`.contextMenus`  

- 删除`context`  

- 更改为`.Menus`  

- （此处共 3 处需要修改）

<!-- ### 参考原代码修改差异

- <a href="https://github.com/YGGYDW/Thunderbird-Email-Translation/commit/7716ddb51446450ea7f48c58dde88ec5a79f809d" target="_blank">源代码差异</a> -->

### 根目录从新打成压缩包

- 在修改文件的这个目录下，Ctrl+A 全选所有文件

- 右键选择压缩文件（文件名随意）

- 压缩成 zip 文件后，看第三步，安装步骤。

## 安装步骤

- 点击右上角`三横杠`的图标

- 选择`扩展和主题`

- 点击`小齿轮`的图标

- 选择`从文件安装附加组件`

- 将压缩包上传，根据提示完成操作。

<details>
  <summary><h4>✨点击查看图示✨</h4></summary>

![打开Thunderbird1界面](https://i.ibb.co/5rLyXVc/Thunderbird1.png)

![上传压缩包插件](https://i.ibb.co/vz6z85W/Thunderbird2.png)

![点击添加](https://i.ibb.co/61w94zK/Thunderbird3.png)

![点击知道了](https://i.ibb.co/Gv8cZ5d/Thunderbird4.png)

![点击继续](https://i.ibb.co/nmQDCR9/Thunderbird5.png)

![点击右侧浮窗或Alt+A完成首次翻译测试](https://i.ibb.co/cNZhDDW/Thunderbird6.png)

![点击继续大功告成](https://i.ibb.co/NK4s2F8/Thunderbird7.png)

 </details>
