**目录 (Table of Contents)**

[TOCM]

[TOC]

## 激活进程主窗口

### 功能描述
找到指定进程的主窗口并使其显示在前台。

### 官方文档
https://getquicker.net/KC/Help/Doc/activateprocessmainwindow

### 内部名称
sys:activateProcessMainWindow

### 传入参数


**process**

名称: 进程名称/pid

说明: 请输入要验证的进程名称或pid。进程名通常是exe的文件名去掉后缀，比如记事本程序的进程名称为notepad。

类型: 字符串-Text

必填: True



**className**

名称: 窗口类名

说明: 选填。未能获取主窗口时（如窗口隐藏），可以尝试根据类名查找窗口，支持正则。

类型: 字符串-Text



**windowTitle**

名称: 窗口标题

说明: 选填。未能获取主窗口时，根据窗口标题查找，支持正则。

类型: 字符串-Text



**hotkey**

名称: 热键

说明: 选填。软件最小化到托盘时，使用指定的全局热键激活窗口。

类型: 字符串-Text



**path**

名称: 程序路径

说明: 选填。如果进程不存在，可以根据此路径启动程序。

类型: 字符串-Text

必填: True



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 是否成功激活了进程主窗口

类型: 布尔值-Boolean



**pid**

名称: PID

说明: 进程ID

类型: 数字(整数)-Integer



**mainWinHandle**

名称: 主窗口句柄

说明: 进程的主窗口句柄

类型: 数字(整数)-Integer



**mainWinTitle**

名称: 主窗口标题

类型: 字符串-Text



### 范例


**范例1**
```json

```

***

## 跳出循环(break)

### 功能描述
跳出循环（“每个” 或 “重复” 模块）

### 官方文档
https://getquicker.net/KC/Help/Doc/break

### 内部名称
sys:break

### 传入参数
无

### 传出参数
无

### 范例


**范例1**
```json

```

***

## 检查路径/获取文件信息

### 功能描述
检查指定的文件或文件夹是否存在。

### 官方文档
https://getquicker.net/KC/Help/Doc/checkPathExists

### 内部名称
sys:checkPathExists

### 传入参数


**path**

名称: 路径

说明: 文件或文件夹的完整路径。

类型: 字符串-Text

必填: True



### 传出参数


**isExists**

名称: 路径是否存在

类型: 布尔值-Boolean



**isFile**

名称: 是否为文件

类型: 布尔值-Boolean



**fileLength**

名称: 文件长度

类型: 数字(整数)-Integer



**isFolder**

名称: 是否为文件夹

类型: 布尔值-Boolean



**isReadonly**

名称: 是否只读

类型: 布尔值-Boolean



**isHidden**

名称: 是否隐藏

类型: 布尔值-Boolean



**isSystem**

名称: 是否为系统文件

类型: 布尔值-Boolean



**fileCount**

名称: 文件夹内文件个数

说明: 仅对文件夹路径有效，输出时需要耗费一定时间扫描文件夹

类型: 数字(整数)-Integer



**totalLength**

名称: 文件夹大小

说明: 仅对文件夹路径有效，输出时需要耗费一定时间扫描文件夹

类型: 数字(整数)-Integer



**createTime**

名称: 创建时间

类型: 时间日期-DateTime



**editTime**

名称: 更新时间

类型: 时间日期-DateTime



**metaData**

名称: 文件扩展信息

说明: 获取文件的扩展信息，值为词典类型。

类型: 词典-Dict



**lnkTarget**

名称: lnk目标路径

说明: 快捷方式文件的目标文件

类型: 字符串-Text



**lnkArguments**

名称: lnk命令行参数

说明: 快捷方式中的命令行参数

类型: 字符串-Text



**md5hash**

名称: MD5 哈希值

说明: 获取文件的MD5哈希值。仅对文件有效，大文件需要一些时间扫描。

类型: 字符串-Text



**sha1hash**

名称: SHA1 哈希值

说明: 获取文件的SHA1哈希值。仅对文件有效，大文件需要一些时间扫描。

类型: 字符串-Text



**sha256hash**

名称: SHA256 哈希值

说明: 获取文件的SHA256哈希值。仅对文件有效，大文件需要一些时间扫描。

类型: 字符串-Text



**crc32hash**

名称: CRC32 哈希值

说明: 获取文件的CRC32哈希值。仅对文件有效，大文件需要一些时间扫描。

类型: 字符串-Text



### 范例


**范例1**
```json

```

***

## 检查程序已启动/获取进程信息

### 功能描述
检查指定的应用程序是否已经启动。

### 官方文档
https://getquicker.net/KC/Help/Doc/checkprocessexists

### 内部名称
sys:checkProcessExists

### 传入参数


**process**

名称: 进程名称/pid

说明: 请输入要验证的进程名称或id。通常是exe的文件名去掉后缀，比如记事本程序的进程名称为notepad。

类型: 字符串-Text

必填: True



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 操作是否成功

说明: 可能会因为无法访问高权限进程等原因而失败。进程未启动不会导致操作失败。

类型: 布尔值-Boolean



**isExists**

名称: 是否运行

说明: 指定的进程是否运行。如果已运行，返回True，否则返回False

类型: 布尔值-Boolean



**pid**

名称: 进程ID

说明: 找到的第一个匹配进程的ID

类型: 数字(整数)-Integer



**pidList**

名称: 所有进程ID列表

说明: 具有相同进程名的所有进程的ID列表

类型: 文本列表-List



**path**

名称: 程序路径

说明: 进程的应用程序路径

类型: 字符串-Text



**mainWinHandle**

名称: 主窗口句柄

类型: 数字(整数)-Integer



**mainwinTitle**

名称: 主窗口标题

类型: 字符串-Text



**startTime**

名称: 启动时间

类型: 时间日期-DateTime



### 范例


**范例1**
```json

```

***

## 云状态存取

### 功能描述
根据键值读取或写入网络数据。

### 官方文档
https://getquicker.net/KC/Help/Doc/clouddata

### 内部名称
sys:clouddata

### 传入参数


**type**

名称: 操作类型

类型: 选项-Enum

默认值: readGlobalState

必填: True



**key**

名称: 状态名称

说明: 存储或读取的数据条目名称(键)。

类型: 字符串-Text



**value**

名称: 内容

说明: 要保存的数据值。使用*NULL*删除此状态的存储。

类型: 字符串-Text



**expireSeconds**

名称: 超时时间

说明: 请求超时时间（秒数）

类型: 数字(小数)-Number

默认值: 2.5



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



**value**

名称: 内容

说明: 读取到的状态内容

类型: 任意类型-Any



**err**

名称: 错误信息

说明: 出错时输出的错误信息。

类型: 字符串-Text



**errCode**

名称: 错误代码

说明: 从云服务商返回的错误代码。NoSuchKey=不存在此状态。

类型: 字符串-Text



### 范例


**范例1**
```json

```

***

## 第三方云对象存储服务

### 功能描述
操作第三方云服务商的对象存储上传和下载文件。

### 官方文档
https://getquicker.net/KC/Help/Doc/cloudObjectOperation

### 内部名称
sys:cloudObjectOperation

### 传入参数


**type**

名称: 操作类型

类型: 选项-Enum

默认值: upload_file

必填: True



**vendor**

名称: 服务商

类型: 选项-Enum

默认值: aliyun

必填: True



**endpoint**

名称: Endpoint

说明: 存储目标区域网址

类型: 字符串-Text



**objectKey**

名称: Key

说明: 存储对象的Key。可以不填写（自动生成key），或填写以/结尾的前缀。

类型: 字符串-Text



**content**

名称: 上传内容

说明: 要上传到对象存储的内容。如果为路径则上传文件。

类型: 任意类型-Any



**extraHeaders**

名称: 附加的Http头

类型: 字符串-Text



**expireSeconds**

名称: 超时时间

说明: 请求超时时间（秒数）

类型: 数字(小数)-Number

默认值: 100



### 传出参数


**objectUrl**

名称: 对象网址

说明: 对象存储后生成的网址

类型: 字符串-Text



**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



### 范例


**范例1**
```json

```

***

## 跳过后续步骤(continue)

### 功能描述
跳过后续步骤（循环内部），开始下一次循环。在循环内部使用。

### 官方文档
https://getquicker.net/KC/Help/Doc/continue

### 内部名称
sys:continue

### 传入参数
无

### 传出参数
无

### 范例


**范例1**
```json

```

***

## 每个

### 功能描述
对列表的每项执行处理

### 官方文档
https://getquicker.net/KC/Help/Doc/each

### 内部名称
sys:each

### 传入参数


**input**

名称: 列表

说明: 要处理的列表

类型: 文本列表-List

必填: True



**useMultiThread**

名称: 线程模式

说明: ⚠通常不要选择! 请阅读文档详细了解后再使用。

类型: 选项-Enum

默认值: 0



**threadDelay**

名称: 线程启动间隔

说明: 多线程运行时，每个线程之间的启动时间间隔毫秒数。

类型: 数字(整数)-Integer

默认值: 5



**concurrentThreadNum**

名称: 同时线程数

说明: 最多同时启动的线程数，请根据电脑配置和任务内容设置。

类型: 数字(整数)-Integer

默认值: 4



**timeoutMs**

名称: 超时毫秒数

说明: 所有线程开启后，等待的超时时间，单位：毫秒。-1:不设置超时时间

类型: 数字(整数)-Integer

默认值: -1



**useLocalContext**

名称: 为线程创建独立上下文

说明: 此时只能读取变量，不能更新变量（词典、列表等引用传递的除外）

类型: 布尔值-Boolean

默认值: False



**waitAny**

名称: WaitAny模式

说明: 任意一个线程结束即可。

类型: 布尔值-Boolean

默认值: False



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**item**

名称: 项

说明: 列表中的每项，每次循环赋予当前项的值。在子步骤中应该对本输出进行处理。

类型: 任意类型-Any



**count**

名称: 计数

说明: 本次循环，处理到了第几项。

类型: 数字(整数)-Integer



**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



### 范例


**范例1**
```json

```

***

## 获取前台进程信息

### 功能描述
获取当前活动窗口进程的信息。

### 官方文档
https://getquicker.net/KC/Help/Doc/getactiveprocessinfo

### 内部名称
sys:getActiveProcessInfo

### 传入参数


**stopIfFail**

名称: 失败后中止动作

说明: 获取进程信息失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**path**

名称: 程序路径

说明: 获得的进程路径

类型: 字符串-Text



**procName**

名称: 进程名

说明: 进程名称

类型: 字符串-Text



**pid**

名称: PID

说明: 进程ID

类型: 数字(整数)-Integer



**isSuccess**

名称: 是否成功

说明: 是否成功获得进程信息

类型: 布尔值-Boolean



### 范例


**范例1**
```json

```

***

## 获取浏览器网址

### 功能描述
获取当前浏览器网址。

### 官方文档
https://getquicker.net/KC/Help/Doc/getchromeurl

### 内部名称
sys:getChromeUrl

### 传入参数


**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**output**

名称: 网址

说明: 当前标签网址URL

类型: 字符串-Text



**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



### 范例


**范例1**
```json

```

***

## 获取剪贴板文件列表

### 功能描述
获取剪贴板中复制的文件(或文件夹)的路径列表

### 官方文档
https://getquicker.net/KC/Help/Doc/getclipboardfiles

### 内部名称
sys:getClipboardFiles

### 传入参数


**stopIfFail**

名称: 失败后中止动作

说明: 获取选中的文本失败后，是否停止后续动作的执行。

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 是否成功获得文件列表

类型: 布尔值-Boolean



**output**

名称: 文件列表

说明: 从剪贴板获取的文件路径列表

类型: 文本列表-List



**elapsedMs**

名称: 已更新时间

说明: 剪贴板最后更新是在多少毫秒以前

类型: 数字(整数)-Integer



### 范例


**范例1**
```json

```

***

## 获取剪贴板图片

### 功能描述
读取剪贴板中的图片内容输出到图片变量中。

### 官方文档
https://getquicker.net/KC/Help/Doc/getclipboardimage

### 内部名称
sys:getClipboardImage

### 传入参数


**stopIfFail**

名称: 失败后中止动作

说明: 获取失败后，是否停止后续动作的执行。

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 是否成功获得剪贴板图片

类型: 布尔值-Boolean



**output**

名称: 结果图片

说明: 将获得的图片写入到变量

类型: 图片-Image



**elapsedMs**

名称: 已更新时间

说明: 剪贴板最后更新是在多少毫秒以前

类型: 数字(整数)-Integer



### 范例


**范例1**
```json

```

***

## 获取剪贴板文本

### 功能描述
读取剪贴板中的文本内容

### 官方文档
https://getquicker.net/KC/Help/Doc/getClipboardText

### 内部名称
sys:getClipboardText

### 传入参数


**format**

名称: 文本数据格式

说明: 需要读取的剪贴板文本内容格式。通常请使用Unicode纯文本格式。

类型: 选项-Enum

默认值: UnicodeText



**customFormat**

名称: 格式名称

说明: 自定义的剪贴板格式名，请和实际剪贴板格式名一致。只支持实际为文本类型的内容。

类型: 字符串-Text



**encoding**

名称: 文本编码

说明: 读取自定义格式时候使用的编码类型

类型: 选项-Enum

默认值: utf-8

必填: True



**waitMs**

名称: 重试时间

说明: 每10ms重试一次，直到获取到文本。为0时不重试。

类型: 数字(整数)-Integer

默认值: 400



**stopIfFail**

名称: 失败后中止动作

说明: 获取选中的文本失败后，是否停止后续动作的执行。

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 是否成功获得文本

类型: 布尔值-Boolean



**output**

名称: 完整结果内容

说明: 将获得的文本内容写入到变量

类型: 字符串-Text



**cleanHtml**

名称: 主要HTML片段

说明: HTML的主要内容。<!--StartFragment-->和<!--EndFragment-->之间的部分

类型: 字符串-Text



**htmlDoc**

名称: 完整的HTML文档

说明: 仅去除剪贴板头部信息的完整HTML文档内容。包含<html>等标签，可直接保存为.html文件。

类型: 字符串-Text



**url**

名称: 来源网址

说明: 从网页中复制内容时，可能会携带网址信息。

类型: 字符串-Text



**elapsedMs**

名称: 已更新时间

说明: 剪贴板最后更新是在多少毫秒以前

类型: 数字(整数)-Integer



### 范例


**范例1**
```json

```

***

## 获取日期时间

### 功能描述
获取当前或从文本、unix时间戳转换日期时间

### 官方文档
https://getquicker.net/KC/Help/Doc/gettime

### 内部名称
sys:getCurrentTime

### 传入参数


**source**

名称: 时间来源

说明: 时间数据来源

类型: 选项-Enum

默认值: currTime



**useUtc**

名称: 使用UTC时间

说明: 是表示使用UTC时间，否表示使用本地时间（电脑的当前时间）。

类型: 布尔值-Boolean

默认值: False



**timeStr**

名称: 待解析文本

说明: 待转换为时间值的文本

类型: 字符串-Text



**inputCulture**

名称: 语言文化

说明: 可选，待解析文本的语言文化。如zh-CN表示中文简体，en-US表示英文美国等。详情请参考文档。

类型: 字符串-Text

默认值: CURRENT



**inputFormat**

名称: 数据格式

说明: 可选，待解析文本的数据格式，如yyyy表示4位数年份，MM表示2位数月份等。详情请参考文档。

类型: 字符串-Text



**timeVar**

名称: 时间变量

说明: 时间变量

类型: 时间日期-DateTime



**timeStampStr**

名称: Unix时间戳值

说明: 从1970年1月1日开始所经过的秒数或毫秒数。根据需要开启或关闭使用UTC时间选项。

类型: 字符串-Text



**addDays**

名称: 添加天数

说明: 添加指定的天数（可以为小数/负数）

类型: 数字(小数)-Number

默认值: 0



**addHours**

名称: 添加小时数

说明: 添加指定的小时数（可以为小数/负数）

类型: 数字(小数)-Number

默认值: 0



**addMinutes**

名称: 添加分钟数

说明: 添加指定的分钟数（可以为小数/负数）

类型: 数字(小数)-Number

默认值: 0



**addSeconds**

名称: 添加秒数

说明: 添加指定的秒数（可以为小数/负数）

类型: 数字(小数)-Number

默认值: 0



**addMonths**

名称: 添加月数

说明: 添加指定的月数（整数）结果不跨月，如1月31日增加1个月等于2月28日。

类型: 数字(小数)-Number

默认值: 0



**format**

名称: 输出文本值格式

说明: 文本值的输出格式，请参考c#语言DateTime.ToString()的参数文档。

类型: 字符串-Text

默认值: yyyy-MM-dd HH:mm:ss



**outputCulture**

名称: 输出语言文化

说明: 可选。指定将时间值格式化为文本时所使用的语言文化。如zh-CN表示中文简体，en-US表示美国英文等。

类型: 字符串-Text

默认值: CURRENT



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



**output**

名称: 时间值

说明: 日期时间类型的结果时间

类型: 时间日期-DateTime



**strValue**

名称: 文本值

说明: 按‘文本值格式’参数转换后的文本格式值

类型: 字符串-Text



**timeStamp**

名称: UNIX时间戳(s)

说明: 获取Unix时间戳（1970年1月1日0时到指定时间的秒数）

类型: 数字(整数)-Integer



**timeStampMs**

名称: UNIX时间戳(ms)

说明: 获取Unix时间戳（1970年1月1日0时到指定时间的毫秒数）

类型: 数字(整数)-Integer



**year**

名称: 年

说明: 年份值

类型: 数字(整数)-Integer



**month**

名称: 月

说明: 月份值

类型: 数字(整数)-Integer



**day**

名称: 日

说明: 日期值

类型: 数字(整数)-Integer



**hour**

名称: 时

说明: 当前小时数，24小时制。

类型: 数字(整数)-Integer



**minute**

名称: 分

说明: 当前分钟数。

类型: 数字(整数)-Integer



**second**

名称: 秒

说明: 当前秒数。

类型: 数字(整数)-Integer



**dayOfWeek**

名称: 周第几天

说明: 本周的第几天，周日为0，周一为1，以此类推。

类型: 数字(整数)-Integer



**dayOfYear**

名称: 年第几天

说明: 本年的第几天。

类型: 数字(整数)-Integer



### 范例


**范例1**
```json

```

***

## 获取资源管理器路径/跳转路径

### 功能描述
获取资源管理器的当前文件夹路径。

### 官方文档
https://getquicker.net/KC/Help/Doc/getexplorerpath

### 内部名称
sys:getExplorerPath

### 传入参数


**operation**

名称: 操作类型

类型: 选项-Enum

默认值: getPath



**path**

名称: 路径

类型: 字符串-Text



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**output**

名称: 当前窗口路径

说明: 当前资源管理器窗口的路径

类型: 字符串-Text



**allPathList**

名称: 所有打开的路径

说明: 所有资源管理器窗口中打开的路径列表

类型: 文本列表-List



**lastPath**

名称: 最近访问的路径

说明: 最近访问的资源管理器窗口的路径

类型: 字符串-Text



**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



### 范例


**范例1**
```json

```

***

## 获取系统路径

### 功能描述
返回指定的特殊目录路径。

### 官方文档
https://getquicker.net/KC/Help/Doc/getfolderpath

### 内部名称
sys:getFolderPath

### 传入参数


**folder**

名称: 目录类型

说明: Windows的特殊目录类型，详情请搜索“Environment.SpecialFolder”。

类型: 选项-Enum

必填: True



### 传出参数


**path**

名称: 路径

说明: 返回的完整路径

类型: 字符串-Text



### 范例


**范例1**
```json

```

***

## 获取选中的文本

### 功能描述
获取选中的文字

### 官方文档
https://getquicker.net/KC/Help/Doc/get_selected_text

### 内部名称
sys:getSelectedText

### 传入参数


**format**

名称: 文本数据格式

说明: 需要读取的剪贴板文本内容格式。通常请使用Unicode纯文本格式。

类型: 选项-Enum

默认值: UnicodeText



**waitMs**

名称: 等待剪贴板时间

说明: 模拟复制键后，等待剪贴板变化的最长时间毫秒数。

类型: 数字(整数)-Integer

默认值: 250



**repeat**

名称: 重试次数

说明: 【已过时，仅为兼容性保留】失败后重试的次数。

类型: 数字(整数)-Integer

默认值: 0



**trim**

名称: 去除前后的空白

说明: 去除内容前后的空白（包括空行）。

类型: 布尔值-Boolean

默认值: False



**tryNoClipboard**

名称: 尝试不通过剪贴板的方式获取

说明: 通过UIAutomation方式获取（某些情况可能出现无法完整获取文字、失去换行信息等问题）

类型: 布尔值-Boolean

默认值: False



**useActionParam**

名称: 如果为动作传递了参数，使用参数值作为获取的结果

说明: 没有传递参数时仍尝试获取选中的文本。

类型: 布尔值-Boolean

默认值: False



**stopIfFail**

名称: 失败后中止动作

说明: 获取选中的文本失败后，是否停止后续动作的执行。

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 是否成功获取了文本

类型: 布尔值-Boolean



**output**

名称: 内容

说明: 将获得的文本写入到变量

类型: 字符串-Text



**cleanHtml**

名称: 去除封装的HTML

说明: 剪贴板HTML的主要内容<!--StartFragment-->和<!--EndFragment-->之间的部分

类型: 字符串-Text



**outputEncoded**

名称: URL编码的内容

说明: 对选中的内容进行URL编码处理后的结果，通常用于拼接网址。

类型: 字符串-Text



**url**

名称: 来源网址

说明: 从网页中复制内容时，可能会携带网址信息。

类型: 字符串-Text



### 范例


**范例1**
```json

```

***

## 获取系统或动作信息

### 功能描述
返回Windows系统信息。

### 官方文档
https://getquicker.net/KC/Help/Doc/getsysinfo

### 内部名称
sys:getSysInfo

### 传入参数
无

### 传出参数


**MachineName**

名称: 机器名

类型: 字符串-Text



**userName**

名称: 用户名

说明: 当前登录到电脑的用户名

类型: 字符串-Text



**userDomainName**

名称: 用户域名

说明: 当前用户的网络域名（DomainName）

类型: 字符串-Text



**OsVersion**

名称: 系统版本号

类型: 字符串-Text



**isWin10**

名称: 是否为Win10或以上

类型: 布尔值-Boolean



**isWin11**

名称: 是否为Win11

类型: 布尔值-Boolean



**isAutoRun**

名称: 是否自动启动

说明: 是否开机自动启动Quicker

类型: 布尔值-Boolean



**startupSeconds**

名称: 系统正常运行秒数

说明: 可参考任务管理器中显示的正常运行时间。

类型: 数字(小数)-Number



**isLocked**

名称: Windows是否锁定

类型: 布尔值-Boolean



**sysEnv**

名称: 环境变量

类型: 词典-Dict



**primaryScreenRes**

名称: 主屏分辨率

类型: 字符串-Text



**isFullscreen**

名称: 前台窗口是否为全屏状态

类型: 布尔值-Boolean



**isNetworkConnected**

名称: 是否联网

类型: 布尔值-Boolean



**lanIp**

名称: 本机局域网IP

类型: 字符串-Text



**quickerVersion**

名称: Quicker版本

类型: 数字(整数)-Integer



**isPro**

名称: 是否为专业版

说明: 当前用户是否使用专业版软件。

类型: 布尔值-Boolean



**unionId**

名称: UnionId

说明: 一个标识用户身份的字符串

类型: 字符串-Text



**hasBaiduAccount**

名称: 已设置自有百度OCR帐号

说明: 已经在设置中添加了自有百度OCR帐号。

类型: 布尔值-Boolean



**runnedSeconds**

名称: Quicker启动秒数

说明: Quicker启动后运行的秒数

类型: 数字(小数)-Number



**actionId**

名称: 动作ID

说明: 当前运行的动作ID

类型: 字符串-Text



**actionName**

名称: 动作名称

说明: 当前运行的动作名称

类型: 字符串-Text



**sharedActionId**

名称: 动作库ID

说明: 当前动作的动作库ID

类型: 字符串-Text



**sharedActionRevision**

名称: 动作版本号

说明: 当前安装的动作版本

类型: 数字(整数)-Integer



**actionCount**

名称: 运行个数

说明: 当前动作运行中的实例个数(包含此实例)

类型: 数字(整数)-Integer



**isDebugging**

名称: 是否调试运行

说明: 是否正在调试运行动作

类型: 布尔值-Boolean



**trigger**

名称: 触发方式

说明: 动作的触发方式

类型: 字符串-Text



**textParam**

名称: 文本上下文参数

说明: 传入动作的文本上下文参数

类型: 字符串-Text



**imageParam**

名称: 图片上下文参数

说明: 传入动作的图片上下文参数

类型: 图片-Image



**isWinInDarkMode**

名称: Windows是否为深色模式

说明: true表示深色模式，false表示浅色模式。

类型: 布尔值-Boolean



**quickerThemeMode**

名称: Quicker主题模式

说明: 可能为：light/dark/auto_light/auto_dark。auto_light/auto_dark表示为跟随windows，当前为浅色或深色模式。

类型: 字符串-Text



### 范例


**范例1**
```json

```

***

## 获取窗口信息/查找窗口

### 功能描述
获取指定窗口的标题等信息。

### 官方文档
https://getquicker.net/KC/Help/Doc/getwindowtitle

### 内部名称
sys:getWindowTitle

### 传入参数


**which**

名称: 目标窗口

说明: 判断哪个窗口的信息

类型: 选项-Enum

默认值: foreground

必填: True



**hWnd**

名称: 窗口句柄hWnd

说明: 未指定时使用前台窗口句柄

类型: 数字(整数)-Integer



**className**

名称: 窗口类名

说明: 要查找窗口的类名（ClassName），为空时不检查此项。

类型: 字符串-Text



**windowName**

名称: 窗口名称

说明: 要查找窗口的标题，为空时不检查此项。

类型: 字符串-Text



**procIdOrName**

名称: 进程名/pid

说明: 要查找窗口所属的进程名或pid，为空时不检查此项。

类型: 字符串-Text



**onlyVisible**

名称: 仅可见窗口

类型: 选项-Enum

默认值: default



**requireTitle**

名称: 仅名称(标题)不为空的窗口

类型: 布尔值-Boolean

默认值: True



**useRegex**

名称: 使用正则匹配窗口类名和标题

类型: 布尔值-Boolean

默认值: False



**winRectIncludeInvisibleBorder**

名称: 窗口位置包含不可见边框（阴影区域）

类型: 布尔值-Boolean

默认值: False



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



**output**

名称: 窗口标题

说明: 窗口的标题文字

类型: 字符串-Text



**className**

名称: 类名

说明: 窗口的 Class Name

类型: 字符串-Text



**handle**

名称: 句柄

说明: 窗口的句柄

类型: 数字(整数)-Integer



**pid**

名称: 进程ID

说明: 窗口所属进程的ID

类型: 数字(整数)-Integer



**procName**

名称: 进程名

说明: 进程名称

类型: 字符串-Text



**path**

名称: 程序路径

说明: 获得的进程路径

类型: 字符串-Text



**parent**

名称: 父窗口句柄

类型: 数字(整数)-Integer



**root**

名称: 根窗口句柄

类型: 数字(整数)-Integer



**rootOwner**

名称: 根所有者窗口句柄

类型: 数字(整数)-Integer



**rect**

名称: 窗口位置

说明: 文本值，格式为:Left,Top,Right,Bottom,Width,Height。

类型: 字符串-Text



**rectNoSize**

名称: 窗口位置(不含尺寸)

说明: 文本值，格式为:Left,Top,Right,Bottom。如:0,0,100,100

类型: 字符串-Text



**rectDict**

名称: 窗口位置(词典值)

说明: 词典值，属性为:Left,Top,Right,Bottom,Width,Height

类型: 词典-Dict



**isTopmost**

名称: 是否置顶

类型: 布尔值-Boolean



**isVisible**

名称: 是否可见

类型: 布尔值-Boolean



**showState**

名称: 显示状态

说明: 1:普通，2:最小化，3:最大化。

类型: 数字(整数)-Integer



**alpha**

名称: 不透明度

说明: 窗口的透明度，范围为0-255。0表示全透明

类型: 数字(整数)-Integer



**allChildWindows**

名称: 所有子窗口

说明: 词典值，Key为窗口句柄，Value为窗口标题

类型: 词典-Dict



**topLevelWindows**

名称: 所有顶层窗口

说明: 词典值，Key为窗口句柄，Value为窗口标题

类型: 词典-Dict



### 范例


**范例1**
```json

```

***

## 步骤组

### 功能描述
一组有关的模块（方便整体禁用、删除等）

### 官方文档
https://getquicker.net/KC/Help/Doc/group

### 内部名称
sys:group

### 传入参数


**skipErr**

名称: 忽略错误

说明: 忽略内部步骤的错误，继续允许后续代码

类型: 布尔值-Boolean

默认值: False



**skipWhenDebugging**

名称: 调试运行时不输出调试内容

说明: 用以减少不必要的调试输出

类型: 布尔值-Boolean

默认值: False



**useMultiThread**

名称: 使用多线程

说明: ⚠通常不要选择! 请阅读文档详细了解后再使用。

类型: 布尔值-Boolean

默认值: False



**waitAny**

名称: 多线程使用WaitAny模式

说明: 任意一个线程结束即可。

类型: 布尔值-Boolean

默认值: False



### 传出参数


**isSuccess**

名称: 是否成功

说明: 内部步骤是否运行成功

类型: 布尔值-Boolean



**errorMessage**

名称: 错误消息

类型: 字符串-Text



### 范例


**范例1**
```json

```

***

## HTTP请求

### 功能描述
发送HTTP请求，并获取返回结果

### 官方文档
https://getquicker.net/KC/Help/Doc/http

### 内部名称
sys:http

### 传入参数


**url**

名称: 网址

说明: 要打开的网页地址

类型: 字符串-Text

默认值: https://

必填: True



**method**

名称: 方法

说明: Http请求的类型

类型: 选项-Enum

默认值: GET

必填: True



**header**

名称: 请求头

说明: 发送的HttpHeader。每行一个header，格式为Name:Value

类型: 字符串-Text



**cookie**

名称: Cookie

说明: 请求的cookie内容

类型: 字符串-Text



**bodyType**

名称: 请求体类型

说明: Http 请求体的内容

类型: 选项-Enum

默认值: JSON

必填: True



**body**

名称: 请求体

说明: Http 请求 BODY。格式要求详见模块帮助。

类型: 字符串-Text



**contentType**

名称: 内容类型

说明: 选填。上传内容的ContentType，适用于“单个文件或图片变量（二进制）”或“纯文本” 请求体类型。

类型: 字符串-Text



**resultType**

名称: 结果类型

说明: Http请求的结果类型

类型: 选项-Enum

默认值: Text

必填: True



**ua**

名称: UserAgent

类型: 字符串-Text

默认值: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/112.0.0.0 Safari/537.36



**expireSeconds**

名称: 超时时间

说明: 请求超时时间（秒数）

类型: 数字(小数)-Number

默认值: 100



**noAutoRedirect**

名称: 禁止重定向

说明: 是否禁止自动跳转

类型: 布尔值-Boolean

默认值: False



**showProgress**

名称: 显示进度条

说明: 是否显示上传下载进度条

类型: 布尔值-Boolean

默认值: False



**skipCertVerify**

名称: 忽略HTTPS证书验证

类型: 布尔值-Boolean

默认值: False



**forceProxy**

名称: 强制使用代理

说明: 即使系统设置中未启用代理，本步骤仍然使用代理访问。

类型: 布尔值-Boolean

默认值: False



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



**useSSE**

名称: 启用SSE流式响应

说明: 调用AI接口时使用，通过子程序处理接收到的流式响应内容

类型: 布尔值-Boolean

默认值: False



**sseSpName**

名称: SSE流式响应处理子程序

说明: 用于处理接收到的流式响应消息，每次收到调用一次，通过data输入变量接收内容。

类型: 字符串-Text



### 传出参数


**isSuccess**

名称: 是否成功

说明: 是否操作成功

类型: 布尔值-Boolean



**statusCode**

名称: 状态码

说明: 返回的http请求状态码

类型: 数字(整数)-Integer



**respHeaders**

名称: 响应头

说明: 返回的HTTP响应Headers

类型: 词典-Dict



**respCookies**

名称: 响应Cookies

说明: 返回的Cookies

类型: 词典-Dict



**content**

名称: 文本结果

说明: 返回的文本内容

类型: 字符串-Text



**imgResult**

名称: 图片结果

说明: 返回的图片内容

类型: 图片-Image



### 范例


**范例1**
```json

```

***

## 如果/否则

### 功能描述
依据条件执行操作

### 官方文档
https://getquicker.net/KC/Help/Doc/if

### 内部名称
sys:if

### 传入参数


**condition**

名称: 如果

说明: 是否符合指定的条件

类型: 布尔值-Boolean



### 传出参数
无

### 范例


**范例1**
```json

```

***

## 模拟按键A（录入）

### 功能描述
模拟键盘输入

### 官方文档
https://getquicker.net/KC/Help/Doc/keyinput

### 内部名称
sys:keyInput

### 传入参数


**keys**

名称: 按键

说明: 模拟的按键内容

类型: 按键码

必填: True



**repeat**

名称: 重复次数

类型: 数字(整数)-Integer

默认值: 1



**interval**

名称: 重复间隔(毫秒)

说明: 每次重复之间的间隔毫秒数

类型: 数字(整数)-Integer

默认值: 1



**holdMs**

名称: 保持毫秒数

说明: 普通键（非Ctrl/Alt/Shift/Win）在抬起前保持的时间。-1表示使用默认设置。
某些直接模拟按键无法生效的软件中可以尝试增加此值。

类型: 数字(整数)-Integer

默认值: -1



### 传出参数
无

### 范例


**范例1**
```json

```

***

## 鼠标输入

### 功能描述
模拟鼠标输入

### 官方文档
https://getquicker.net/KC/Help/Doc/mouse

### 内部名称
sys:mouse

### 传入参数


**type**

名称: 类型

说明: 操作类型

类型: 选项-Enum

默认值: restore

必填: True



**hWnd**

名称: 窗口句柄

说明: 目标窗口的句柄。留空或 0 表示操作前台窗口。

类型: 数字(整数)-Integer



**btn**

名称: 按钮

说明: 操作哪个按钮

类型: 选项-Enum

默认值: left

必填: True



**bmp**

名称: 位图路径

说明: 需要在屏幕中查找的位图路径。位图必须和屏幕图像完全匹配，不能压缩。此时X、Y的值为相对于搜索位图的左上角的偏移。

类型: 字符串-Text

必填: True



**bmpVar**

名称: 位图变量

说明: 需要在屏幕中查找的位图。位图必须和屏幕图像完全匹配，不能压缩。此时X、Y的值为相对于搜索位图的左上角的偏移。

类型: 图片-Image

必填: True



**bmpTargetType**

名称: 查找范围

说明: 位图查找范围

类型: 选项-Enum

默认值: MainScreen



**searchRect**

名称: 查找坐标范围

说明: 当“查找范围”为“坐标范围”时有效，格式为：left,top,right,bottom

类型: 字符串-Text



**bmpPosition**

名称: 定位位置

说明: 查找到图片后，鼠标指针移动到的位置

类型: 选项-Enum

默认值: Center



**bmpColorError**

名称: 颜色容差

说明: 匹配像素时允许每个颜色通道的偏差值0-100，0表示精确匹配，速度最快。

类型: 数字(整数)-Integer

默认值: 10



**maxFindCount**

名称: 最大匹配数量

说明: 找图的最大匹配数量。将对每个查找到的目标执行附加动作。

类型: 数字(整数)-Integer

默认值: 1



**retryCount**

名称: 重试次数

说明: 未找到位图时的重试次数。每次重试间隔300ms。

类型: 数字(整数)-Integer

默认值: 1



**x**

名称: X

说明: 水平方向的坐标/坐标偏移/移动距离(像素) 或 滚动数量（clicks。正值向右，负值向左）

类型: 数字(整数)-Integer

默认值: 0

必填: True



**y**

名称: Y

说明: 垂直方向的坐标/坐标偏移/移动距离 或 滚动数量（clicks。正值向前，负值向后）

类型: 数字(整数)-Integer

默认值: 0

必填: True



**xy**

名称: 坐标

说明: 格式为：x,y，如：100,200。也可以使用百分比表示，如：50%,50% 表示屏幕中心。

类型: 字符串-Text

必填: True



**xyForWin**

名称: 相对坐标

说明: 格式为：x,y，如：100,200（相对于窗口左上角向右100，向下200）。也可以使用百分比表示，如：50%,50% 表示窗口中心。

类型: 字符串-Text

必填: True



**slowMove**

名称: 逐渐移动到目标

说明: 逐渐移动而不是直接移动到目标位置。

类型: 布尔值-Boolean

默认值: False



**extAction**

名称: 移动后操作

说明: 移动位置后，需要执行的动作

类型: 选项-Enum

默认值: none

必填: True



**restoreMousePos**

名称: 操作完成后恢复鼠标位置

类型: 布尔值-Boolean

默认值: False



**stopIfFail**

名称: 失败后中止动作

说明: 获取位置失败后，是否停止后续动作的执行。

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 找图定位是否成功

类型: 布尔值-Boolean



**mouseLocation**

名称: 鼠标位置

说明: 格式为X,Y的文本

类型: 字符串-Text



**mouseX**

名称: 鼠标位置X

说明: 鼠标位置X坐标

类型: 数字(整数)-Integer



**mouseY**

名称: 鼠标位置Y

说明: 鼠标位置Y坐标

类型: 数字(整数)-Integer



**cursorType**

名称: 光标类型

说明: 当前的鼠标指针形状类型

类型: 字符串-Text



### 范例


**范例1**
```json

```

***

## 提示消息

### 功能描述
显示可以自动消失的消息提示。

### 官方文档
https://getquicker.net/KC/Help/Doc/notify

### 内部名称
sys:notify

### 传入参数


**type**

名称: 类型

说明: 消息的类型

类型: 选项-Enum

默认值: Info

必填: True



**msg**

名称: 消息内容

说明: 显示的消息内容

类型: 字符串-Text

必填: True



**maxLines**

名称: 最大行数

说明: 显示内容的最大行数，0表示不限

类型: 数字(整数)-Integer

默认值: 0

必填: True



**style**

名称: 风格

类型: 选项-Enum

默认值: Default

必填: True



**clickAction**

名称: 点击命令

说明: 点击时运行命令（如网址等可以在Win+R中执行的文本，仅支持默认风格提示）。默认为复制提示文字。

类型: 字符串-Text



### 传出参数
无

### 范例


**范例1**
```json

```

***

## 比较数字

### 功能描述
比较数字大小。

### 官方文档
https://getquicker.net/KC/Help/Doc/numcompare

### 内部名称
sys:numCompare

### 传入参数


**param1**

名称: 数字1

说明: 左侧的数字

类型: 数字(小数)-Number

默认值: 0

必填: True



**type**

名称: 类型

说明: 比较方式

类型: 选项-Enum

默认值: >

必填: True



**param2**

名称: 数字2

说明: 右侧的数字

类型: 数字(小数)-Number

默认值: 0

必填: True



### 传出参数


**value**

名称: 值

说明: 比较结果是否为真

类型: 布尔值-Boolean



### 范例


**范例1**
```json

```

***

## 打开网址

### 功能描述
打开指定的网址

### 官方文档
https://getquicker.net/KC/Help/Doc/openurl

### 内部名称
sys:openUrl

### 传入参数


**url**

名称: 网址

说明: 要打开的网页地址

类型: 字符串-Text

默认值: https://

必填: True



**browser**

名称: 浏览器

说明: 使用什么浏览器打开网址

类型: 选项-Enum

默认值: default

必填: True



**exePath**

名称: 浏览器程序路径

说明: 浏览器exe程序路径

类型: 字符串-Text

必填: True



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



### 范例


**范例1**
```json

```

***

## 发送文本到窗口

### 功能描述
将文本输出到活动窗口中

### 官方文档
https://getquicker.net/KC/Help/Doc/outputtext

### 内部名称
sys:outputText

### 传入参数


**content**

名称: 内容

说明: 要输出的内容

类型: 字符串-Text

必填: True



**method**

名称: 方法

说明: 发送内容使用的方法

类型: 选项-Enum

默认值: paste

必填: True



**delayBeforePaste**

名称: 粘贴前延时

说明: 毫秒数。写入剪贴板以后，等待指定的时间后再发送粘贴按键(Ctrl+V)

类型: 数字(整数)-Integer

默认值: 50



**delayAfterPaste**

名称: 粘贴后延时

说明: 毫秒数。发送粘贴按键(Ctrl+V)之后等待的毫秒数

类型: 数字(整数)-Integer

默认值: 10



**delayBetweenChar**

名称: 字符间延迟

说明: 模拟输入下一个字符之前等待的毫秒数。

类型: 数字(整数)-Integer

默认值: 0



**appendReturn**

名称: 在末尾添加回车

说明: 发送内容后，在末尾输入回车

类型: 布尔值-Boolean

默认值: False



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 步骤是否成功

说明: 步骤是否成功完成

类型: 布尔值-Boolean



### 范例


**范例1**
```json

```

***

## 播放声音

### 功能描述
播放声音提示或声音文件。

### 官方文档
https://getquicker.net/KC/Help/Doc/playsound

### 内部名称
sys:playSound

### 传入参数


**type**

名称: 类型

类型: 选项-Enum

默认值: LOCAL



**localSound**

名称: 提示音类型

类型: 选项-Enum

默认值: info



**uri**

名称: 路径或URL

说明: 音乐文件的本地路径或网址。

类型: 字符串-Text



**text**

名称: 文本内容

说明: 需要朗读的文本。

类型: 字符串-Text



**wait**

名称: 等待播放完成

类型: 布尔值-Boolean



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



### 范例


**范例1**
```json

```

***

## Quicker操作

### 功能描述
调用Quicker的某个功能

### 官方文档
https://getquicker.net/KC/Help/Doc/quickeroperations

### 内部名称
sys:quickeroperations

### 传入参数


**type**

名称: 类型

说明: 操作类型

类型: 选项-Enum

默认值: showPanel

必填: True



**profileId**

名称: 动作页ID

说明: 请在场景与动作管理中，查看动作页信息获取ID。

类型: 字符串-Text

必填: True



**actionId**

名称: 动作ID或名称

说明: 在动作上点右键->信息可以查看动作信息。使用名称时不能有重名动作。获取动作信息时仅可填写动作Id。编辑动作时，使用%%id或%%name格式，可用于编辑公共子程序。

类型: 字符串-Text

必填: True



**position**

名称: 位置

说明: 坐标，格式为：left,top

类型: 字符串-Text

默认值: 200,200

必填: True



**exe**

名称: 场景标识

说明: 场景关联的exe文件名。请参考场景与动作管理窗口左侧应用列表。

类型: 字符串-Text

必填: True



**activatePointWindow**

名称: 自动激活鼠标位置窗口

类型: 布尔值-Boolean

默认值: 0



**followMousePosition**

名称: 跟随鼠标位置

类型: 布尔值-Boolean

默认值: True



**searchText**

名称: 预置的搜索内容

说明: 预先放入搜索框的内容

类型: 字符串-Text



**skinId**

名称: 外观ID

说明: 请在外观网页中复制外观ID

类型: 字符串-Text

必填: True



**theme**

名称: 主题模式

说明: 可选切换为浅色或暗色模式

类型: 选项-Enum



**viewMode**

名称: 显示状态

类型: 选项-Enum

默认值: ByProcess



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 步骤是否成功

说明: 步骤是否成功完成

类型: 布尔值-Boolean



**actionList**

名称: 动作列表

类型: 文本列表-List



**actionTitle**

名称: 动作标题

类型: 字符串-Text



**actionIcon**

名称: 动作图标

类型: 字符串-Text



### 范例


**范例1**
```json

```

***

## 重复

### 功能描述
循环指定的次数，或符合某个条件时中止

### 官方文档
https://getquicker.net/KC/Help/Doc/repeat

### 内部名称
sys:repeat

### 传入参数


**count**

名称: 次数

说明: 重复次数，除非符合条件提前中止。-1表示无限循环。

类型: 数字(整数)-Integer

默认值: 1



**stopCondition**

名称: 中止条件

说明: 选填。条件满足时停止循环（每次循环开始时检查）。

类型: 布尔值-Boolean



**startIndex**

名称: 计数开始值

说明: 计数序号的开始值，通常应该为0。

类型: 数字(整数)-Integer

默认值: 0



**repeatDelayMs**

名称: 循环间隔时间

说明: 每次循环之间的间隔毫秒数。如果为0，请确保循环内部有其他等待步骤，避免连续循环占用较多资源。

类型: 数字(整数)-Integer

默认值: 1



**progressBarTitle**

名称: 进度条标题

说明: 如果设置了此参数，则在循环过程中会显示一个进度条，标题为此参数的值。

类型: 字符串-Text



### 传出参数


**count**

名称: 计数

说明: 计数序号，表示第几次循环。

类型: 数字(整数)-Integer



### 范例


**范例1**
```json

```

***

## 显示进度条

### 功能描述
显示/更新进度条

### 官方文档
https://getquicker.net/KC/Help/Doc/reportProgress

### 内部名称
sys:reportProgress

### 传入参数


**type**

名称: 类型

说明: 操作类型

类型: 选项-Enum

默认值: REQUEST_ID

必填: True



**progressId**

名称: 进度条ID

说明: 进度条的序号，用于后续更新或删除进度条

类型: 数字(整数)-Integer

默认值: 0



**title**

名称: 进度条标题

说明: 进度条的标题(显示在进度条上方)

类型: 字符串-Text



**percentage**

名称: 进度百分比

说明: 0到100之间的数字

类型: 数字(小数)-Number

默认值: 0



**text**

名称: 说明文字

说明: 显示在进度条下方

类型: 字符串-Text



### 传出参数


**progressId**

名称: 进度条ID

说明: 进度条的序号，用于后续更新或删除进度条

类型: 数字(整数)-Integer



### 范例


**范例1**
```json

```

***

## 恢复活动窗口

### 功能描述
如果活动窗口改变了（比如使用了参数输入步骤）,使用此动作恢复窗口焦点。

### 官方文档
https://getquicker.net/KC/Help/Doc/restoreactivewindow

### 内部名称
sys:restoreActiveWindow

### 传入参数
无

### 传出参数
无

### 范例


**范例1**
```json

```

***

## 运行或停止动作

### 功能描述
执行指定的其他动作

### 官方文档
https://getquicker.net/KC/Help/Doc/runaction

### 内部名称
sys:runAction

### 传入参数


**type**

名称: 类型

说明: 操作类型

类型: 选项-Enum

默认值: StartAction

必填: True



**actionId**

名称: 目标动作

说明: 要运行的其他动作的ID或名称(使用名称时需要完全匹配且不能有重名动作)

类型: 字符串-Text

必填: True



**onlyCustomMenu**

名称: 仅显示动作的自定义菜单

说明: 不显示编辑、复制等菜单

类型: 布尔值-Boolean

默认值: False



**inputParam**

名称: 命令参数

说明: 传递给目标动作的参数。存储在该动作的quicker_in_param变量中。

类型: 字符串-Text

必填: True



**wait**

名称: 等待运行结束

说明: 是否等待此动作运行结束再执行后续动作（如需获取目标动作的输出，需选中此项）

类型: 布尔值-Boolean

默认值: True



**debug**

名称: 调试模式运行

说明: 是否以调试模式运行动作

类型: 布尔值-Boolean

默认值: False



**hideMessage**

名称: 不显示提示消息

说明: 仅对非动作库安装的动作有效

类型: 布尔值-Boolean

默认值: False



**stopIfFail**

名称: 失败后停止

说明: 如果未找到目标动作，是否停止当前动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



**actionTitle**

名称: 动作名称

说明: 运行的动作名称。

类型: 字符串-Text



**count**

名称: 运行个数

说明: 动作正在运行的个数

类型: 数字(小数)-Number



**output**

名称: 动作输出

说明: 被调用动作的输出。

类型: 字符串-Text



### 范例


**范例1**
```json

```

***

## 运行或打开

### 功能描述
运行软件或命令，打开文件、文件夹或网址。效果类似于在Windows“运行”对话框中执行命令。

### 官方文档
https://getquicker.net/KC/Help/Doc/run

### 内部名称
sys:run

### 传入参数


**path**

名称: 路径或命令

说明: 要运行的命令或打开的文件路径、网址、URI等。

类型: 字符串-Text

必填: True



**arg**

名称: 参数(可选)

说明: 程序参数

类型: 字符串-Text



**setWorkingDir**

名称: 工作目录

说明: 可输入 0或留空(不设置,由windows默认)、1(软件所在目录)、具体的工作目录路径。

类型: 字符串-Text

默认值: 1



**windowStyle**

名称: 窗口风格

说明: 设置期望的窗口风格，是否有效依赖于具体的软件。

类型: 选项-Enum

默认值: 0



**runas**

名称: 以管理员身份运行

说明: 以管理员身份运行软件或命令。

类型: 布尔值-Boolean

默认值: False



**waitInputIdle**

名称: 等待启动完成

说明: 等待进程完成后了初始化，可以接受用户输入。

类型: 布尔值-Boolean

默认值: False



**waitExit**

名称: 等待进程结束

说明: 等待进程结束后再执行后续操作步骤。

类型: 布尔值-Boolean

默认值: False



**activateWindowIfRunning**

名称: 如果程序已运行则尝试激活窗口

说明: 如果程序已经在运行，则尝试激活其窗口。

类型: 布尔值-Boolean

默认值: False



**activateWindowHotkey**

名称: 激活窗口快捷键

说明: 对于支持快捷键激活窗口的软件，设置该快捷键。支持“模拟按键B”语法。

类型: 字符串-Text



**alternativePath**

名称: 备用路径

说明: 文件在多个电脑上路径不同时，使用备用路径填写其他电脑上的文件路径。

类型: 字符串-Text



**username**

名称: 用户名

说明: 使用指定的用户运行

类型: 字符串-Text



**password**

名称: 密码

说明: 用户名对应的密码

类型: 字符串-Text



**outputEncoding**

名称: 控制台输出编码

说明: 控制台输出编码。如果输出遇到乱码，尝试修改此选项。

类型: 选项-Enum

默认值: oem

必填: True



**envVariables**

名称: 环境变量

说明: 为应用程序设置特定的环境变量值。每行一个，格式“变量名=值”，如“CONFIG_FILE=d:\config.json”

类型: 字符串-Text



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



**pid**

名称: PID

说明: 进程ID

类型: 数字(整数)-Integer



**mainWinHandle**

名称: 主窗口句柄

说明: 进程的主窗口句柄

类型: 数字(整数)-Integer



**mainWinTitle**

名称: 主窗口标题

类型: 字符串-Text



**stdout**

名称: 控制台输出

说明: 慎用！仅用于控制台程序，会自动等待进程结束。输出stdout，为空时输出stderr。

类型: 字符串-Text



**stdoutOnly**

名称: stdout输出

说明: 慎用！捕获控制台程序的stdout输出，会自动等待进程结束

类型: 字符串-Text



**stderr**

名称: stderr输出

说明: 慎用！捕获控制台程序的stderr输出，会自动等待进程结束

类型: 字符串-Text



**exitCode**

名称: 退出代码

说明: 进程的ExitCode，会自动等待进程结束。

类型: 数字(整数)-Integer



### 范例


**范例1**
```json

```

***

## 屏幕找图/找色/找字

### 功能描述
在屏幕上查找图片里的内容出现的位置

### 官方文档
https://getquicker.net/KC/Help/Doc/searchBmp

### 内部名称
sys:searchBmp

### 传入参数


**type**

名称: 类型

说明: 操作类型

类型: 选项-Enum

默认值: locateByBitmapFile

必填: True



**bmp**

名称: 位图路径

说明: 需要在屏幕中查找的位图路径。位图必须和屏幕图像完全匹配，不能压缩。此时X、Y的值为相对于搜索位图的左上角的偏移。

类型: 字符串-Text

必填: True



**bmpVar**

名称: 位图变量

说明: 需要在屏幕中查找的位图。位图必须和屏幕图像完全匹配，不能压缩。此时X、Y的值为相对于搜索位图的左上角的偏移。

类型: 图片-Image

必填: True



**searchText**

名称: 文字

说明: 要查找的文字。可使用多行指定多组可选文字，找到任意一组即可。

类型: 字符串-Text



**color**

名称: 颜色

说明: 要查找的颜色，如#FF0000

类型: 字符串-Text

默认值: #FF0000

必填: True



**bmpTargetType**

名称: 查找范围

说明: 位图查找范围

类型: 选项-Enum

默认值: MainScreen



**searchRect**

名称: 查找坐标范围

说明: 可选。当“查找范围”为“坐标范围”时有效，格式为：left,top,right,bottom

类型: 字符串-Text



**bmpPosition**

名称: 定位位置

说明: 定位点相对位图的位置

类型: 选项-Enum

默认值: Center



**x**

名称: X偏移

说明: 定位点水平坐标偏移量（正值向右）

类型: 数字(整数)-Integer

默认值: 0

必填: True



**y**

名称: Y偏移

说明: 定位点垂直坐标偏移量（正值向下）

类型: 数字(整数)-Integer

默认值: 0

必填: True



**bmpColorError**

名称: 颜色容差

说明: 匹配像素时允许每个颜色通道的偏差值0-100，0表示精确匹配，速度最快。

类型: 数字(整数)-Integer

默认值: 10



**maxFindCount**

名称: 最大匹配

说明: 找图的最大匹配数量。将对每个查找到的目标执行附加动作。

类型: 数字(整数)-Integer

默认值: 1



**retryCount**

名称: 重试次数

说明: 未找到位图时的重试次数。每次重试间隔300ms。

类型: 数字(整数)-Integer

默认值: 0



**ignoreWindowsOcr**

名称: 跳过WindowsOCR引擎

类型: 布尔值-Boolean

默认值: False



**ignoreBgColor**

名称: 忽略背景色

说明: 如果查找图片的4个顶点颜色一致，则认为是背景色，找图时忽略此颜色。

类型: 布尔值-Boolean

默认值: True



**stopIfFail**

名称: 失败后中止动作

说明: 获取位置失败后，是否停止后续动作的执行。

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

类型: 布尔值-Boolean



**firstPoint**

名称: 第一个匹配点

说明: 第一个匹配点坐标，格式为：x坐标,y坐标

类型: 字符串-Text



**allPoints**

名称: 所有匹配点

说明: 所有的匹配点列表

类型: 文本列表-List



**imgIndex**

名称: 匹配序号

说明: 从多个图片或多组文字中查找时，返回匹配到的图片或文字组序号，从0开始。

类型: 数字(整数)-Integer



### 范例


**范例1**
```json

```

***

## 在资源管理器中定位文件

### 功能描述
在资源管理器中选中文件

### 官方文档
https://getquicker.net/KC/Help/Doc/selectfileinexplorer

### 内部名称
sys:SelectFileInExplorer

### 传入参数


**path**

名称: 路径

说明: 要定位的文件完整路径。

类型: 字符串-Text

必填: True



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



### 范例


**范例1**
```json

```

***

## 用户选择

### 功能描述
请用户选择一个选项。

### 官方文档
https://getquicker.net/KC/Help/Doc/userselect

### 内部名称
sys:select

### 传入参数


**type**

名称: 类型

类型: 选项-Enum

默认值: single

必填: True



**prompt**

名称: 窗口标题

类型: 字符串-Text

默认值: 请选择

必填: True



**note**

名称: 提示信息

类型: 字符串-Text



**items**

名称: 选项

说明: 每行一个选项，格式为 “文本” 或 “显示文本|值”。如需显示图标，格式请参考文档。

类型: 字符串-Text

必填: True



**defaultValue**

名称: 默认值

说明: 预先选择的项

类型: 字符串-Text



**defaultValueMulti**

名称: 默认值

说明: 多选时默认选项，每行一个

类型: 字符串-Text



**showFilter**

名称: 启用筛选

说明: 是否显示筛选框。仅在且使用焦点时有效。

类型: 选项-Enum

默认值: auto



**filterContent**

名称: 筛选内容

说明: 预先显示的筛选内容

类型: 字符串-Text



**imeState**

名称: 输入法状态

说明: 筛选框输入法状态

类型: 选项-Enum

默认值: NO_CONTROL



**operations**

名称: 右键/全局菜单

说明: 每行定义一个操作，具体格式请参考文档。

类型: 字符串-Text



**fontsize**

名称: 字体大小

类型: 数字(小数)-Number

默认值: 12

必填: True



**fontfamily**

名称: 字体名称

说明: 可选。设置字体名称。如有多个字体，使用逗号分隔。

类型: 字符串-Text



**iconsize**

名称: 图标大小

类型: 数字(小数)-Number

默认值: 16

必填: True



**autoCloseSeconds**

名称: 自动关闭

说明: 几秒后自动关闭选择窗口。0表示不自动关闭。

类型: 数字(小数)-Number

默认值: 0



**winLocation**

名称: 窗口位置

说明: 在哪里显示选择窗口

类型: 选项-Enum

默认值: WithMouse1



**maxWinSize**

名称: 最大尺寸/位置坐标

说明: 可选。设置选择窗口的最大尺寸，格式为：宽度,高度。支持像素数值或屏幕宽高百分比，详情请参考模块文档。
“窗口位置” 类型为 “自定义位置” 时用于指定显示位置，格式为：left,top,right,bottom

类型: 字符串-Text



**keepLastPos**

名称: 使用上次位置

说明: 重复显示选择窗口时，保持上次的显示位置。

类型: 选项-Enum

默认值: 1



**noKeyboard**

名称: 不使用焦点

说明: 不抢占其他应用的焦点。此时无法使用键盘选择选项，只能用鼠标操作。

类型: 布尔值-Boolean

默认值: False



**closeOnDeactivated**

名称: 失去焦点后关闭窗口（仅在使用焦点时有效）

类型: 布尔值-Boolean

默认值: False



**restoreForeground**

名称: 恢复活动窗口到弹出前

说明: 将前台窗口还原为弹窗前的活动窗口。否则将会还原到最后一个活动窗口上。

类型: 布尔值-Boolean

默认值: True



**allowOkWhenEmpty**

名称: 允许不选择任何选项时点击确定

类型: 布尔值-Boolean

默认值: False



**enableQuickConfirm**

名称: 启用快速确认（点击选项后立即确认选择并关闭窗口）

类型: 布尔值-Boolean

默认值: True



**topMost**

名称: 置顶显示

类型: 布尔值-Boolean

默认值: True



**windowKey**

名称: 窗口标识

说明: 再次运行动作时，可根据标识自动关闭前一个窗口并在该位置显示新窗口。

类型: 字符串-Text



**help**

名称: 帮助按钮内容

说明: 点击弹出显示帮助内容，MarkDown格式

类型: 字符串-Text



**stopIfCancel**

名称: 取消后停止

说明: 取消选择后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否确认

说明: 是否成功选择了选项/点击了保存按钮

类型: 布尔值-Boolean



**textValue**

名称: 选择的项(值)

说明: 选中选项的值

类型: 字符串-Text



**selectedIndex**

名称: 索引号

说明: 选择的项在列表里的序号数字，从0开始。

类型: 数字(整数)-Integer



**selectedIndexList**

名称: 索引号列表

说明: 所有选择的项的序号列表

类型: 文本列表-List



**multiSelected**

名称: 选择的项值列表

说明: 所有选择的项的值的列表

类型: 文本列表-List



**extraOperation**

名称: 选择的菜单

说明: 选择的右键菜单或全局菜单项的值

类型: 字符串-Text



**selectedFullItems**

名称: 选择的完整选项

说明: 选择选项的完整定义内容（不仅仅返回选项值）

类型: 任意类型-Any



**selectedItemTitle**

名称: 选择的选项标题

说明: 所选中选项的标题

类型: 字符串-Text



**filterContent**

名称: 筛选内容

说明: 最后使用的筛选词

类型: 字符串-Text



### 范例


**范例1**
```json

```

***

## 模拟按键B（参数）

### 功能描述
发送按键和文本

### 官方文档
https://getquicker.net/KC/Help/Doc/sendKeys

### 内部名称
sys:sendKeys

### 传入参数


**keys**

名称: 按键序列

说明: 要发送的按键序列，使用C#语言SendKeys.Send()语法，具体请参考教程文档。

类型: 字符串-Text



### 传出参数
无

### 范例


**范例1**
```json

```

***

## 向窗口发送消息

### 功能描述
使用SendMessage Win32Api向窗口发送消息。使用方法请搜索SendMessage Win32 API接口。

### 官方文档
https://getquicker.net/KC/Help/Doc/sendMessage

### 内部名称
sys:sendMessage

### 传入参数


**operation**

名称: 操作类型

类型: 选项-Enum

默认值: SendMessage



**hWnd**

名称: 窗口句柄hWnd

说明: 留空或0表示前台窗口

类型: 数字(整数)-Integer



**wMsg**

名称: 消息

说明: 要发送的消息。

类型: 字符串-Text



**wParam**

名称: wParam参数

类型: 字符串-Text



**lParam**

名称: lParam参数

类型: 字符串-Text

默认值: 0



**textLParam**

名称: lParam参数(文本)

说明: 文本内容

类型: 字符串-Text



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



**rtn**

名称: 返回值

说明: 返回值，依据消息的不同具有不同的含义，请查询对应API的文档。

类型: 数字(整数)-Integer



### 范例


**范例1**
```json

```

***

## 显示等待窗口

### 功能描述
显示一个等待用户完成某个操作的提示窗口。

### 官方文档
https://getquicker.net/KC/Help/Doc/showwaitwin

### 内部名称
sys:showWaitWin

### 传入参数


**mode**

名称: 操作

说明: 请选择操作类型

类型: 选项-Enum

默认值: show



**title**

名称: 窗口标题

类型: 字符串-Text

默认值: 完成后继续

必填: True



**prompt**

名称: 提示文字

说明: 提示文字内容

类型: 字符串-Text

默认值: 请在完成操作后点下面的按钮

必填: True



**winLocation**

名称: 窗口位置

说明: 在哪里显示选择窗口

类型: 选项-Enum

默认值: BottomRight



**progress**

名称: 进度条参数

说明: 请以 当前值/总数 的格式传入（可使用插值方式）。 比如：40/80

类型: 字符串-Text



**btnText**

名称: 默认按钮上的文字

说明: 默认按键仅用于关闭窗口。文字内容为空时隐藏默认按钮。

类型: 字符串-Text

默认值: 完成

必填: True



**operations**

名称: 附加操作按钮

说明: 每行定义一个按钮，格式为 “文本” 或 “显示文本|值”。显示在默认按钮的左侧。

类型: 字符串-Text

必填: True



**fontsize**

名称: 文字大小

说明: 按钮上文字的大小，单位为逻辑像素。

类型: 数字(小数)-Number

默认值: 12

必填: True



**iconSize**

名称: 图标大小

说明: 按钮上图标的大小，单位为逻辑像素。

类型: 数字(小数)-Number

默认值: 16

必填: True



**autoCloseSeconds**

名称: 自动关闭

说明: 几秒后自动关闭。0表示不自动关闭。

类型: 数字(小数)-Number

默认值: 0



**stopActionIfClose**

名称: 关闭窗口时（点右上角x按钮）后停止动作

类型: 布尔值-Boolean

默认值: True



**activateMode**

名称: 激活模式

类型: 选项-Enum

默认值: NotActivatable



**help**

名称: 帮助按钮内容

说明: 点击弹出显示帮助内容，MarkDown格式

类型: 字符串-Text



### 传出参数


**isClosed**

名称: 是否已关闭

说明: 等待窗口是否已经关闭了

类型: 布尔值-Boolean



**selectedOperation**

名称: 选择的按钮

说明: 选择的后续操作项

类型: 字符串-Text



### 范例


**范例1**
```json

```

***

## 如果

### 功能描述
依据条件执行操作

### 官方文档
https://getquicker.net/KC/Help/Doc/if

### 内部名称
sys:simpleIf

### 传入参数


**condition**

名称: 如果

说明: 是否符合指定的条件

类型: 布尔值-Boolean



### 传出参数
无

### 范例


**范例1**
```json

```

***

## SMTP发送邮件

### 功能描述
使用SMTP协议发送邮件

### 官方文档
https://getquicker.net/KC/Help/Doc/smtp

### 内部名称
sys:smtp

### 传入参数


**server**

名称: 邮件服务器

说明: 邮件服务器的域名或IP

类型: 字符串-Text

必填: True



**port**

名称: 端口

说明: Smtp端口号

类型: 数字(整数)-Integer

默认值: 25

必填: True



**useSsl**

名称: 使用加密连接

说明: 是否使用TLS连接（通常为587端口）。

类型: 布尔值-Boolean

默认值: False



**account**

名称: 帐号

说明: 发信帐号

类型: 字符串-Text

必填: True



**password**

名称: 密码

说明: 发信帐号的密码

类型: 字符串-Text

必填: True



**sender**

名称: 发信邮箱

说明: 发信帐号所对应的Email地址

类型: 字符串-Text

必填: True



**senderName**

名称: 发件人名称

说明: 发件人的显示名称（可选）

类型: 字符串-Text

必填: True



**to**

名称: 收件人

说明: 收件人Email地址，多个的话使用小写逗号分隔。

类型: 字符串-Text

必填: True



**cc**

名称: 抄送

说明: 抄送给的Email地址列表，多个的话使用小写逗号分隔。

类型: 字符串-Text

必填: True



**bcc**

名称: 密送

说明: 密送给的Email地址列表，多个的话使用小写逗号分隔。

类型: 字符串-Text

必填: True



**subject**

名称: 邮件主题

说明: 邮件的主题

类型: 字符串-Text

必填: True



**content**

名称: 邮件正文

说明: 邮件正文内容

类型: 字符串-Text



**attachList**

名称: 附件

说明: 附件文件列表。多个时每行一个。

类型: 字符串-Text



**isHtml**

名称: 内容为html

说明: 邮件内容是否为HTML格式

类型: 布尔值-Boolean

默认值: False



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



### 范例


**范例1**
```json

```

***

## 停止(return)

### 功能描述
停止动作或从子程序中返回

### 官方文档
https://getquicker.net/KC/Help/Doc/stop

### 内部名称
sys:stop

### 传入参数


**method**

名称: 操作类型

类型: 选项-Enum

默认值: default



**isError**

名称: 标记为出错

说明: 用作子程序或被其他动作调用时，返回出错状态。

类型: 布尔值-Boolean

默认值: False



**return**

名称: 返回值

说明: 被其他动作调用时，返回的动作结果。

类型: 字符串-Text



**showMessage**

名称: 提示消息

说明: 显示的提示信息。

类型: 字符串-Text



### 传出参数
无

### 范例


**范例1**
```json

```

***

## 比较文本

### 功能描述
文本比较

### 官方文档
https://getquicker.net/KC/Help/Doc/strCompare

### 内部名称
sys:strCompare

### 传入参数


**param1**

名称: 文本1

说明: 被比较的文本

类型: 字符串-Text

必填: True



**type**

名称: 类型

说明: 比较方式

类型: 选项-Enum

默认值: >

必填: True



**param2**

名称: 文本2

说明: 对比文本。拼音匹配时，也可用于指定拼音、拼音首字母。

类型: 字符串-Text

必填: True



**case**

名称: 区分大小写

说明: 是否区分大小写

类型: 布尔值-Boolean

默认值: False



### 传出参数


**value**

名称: 值

说明: 比较结果是否为真

类型: 布尔值-Boolean



### 范例


**范例1**
```json

```

***

## 文本处理

### 功能描述
各种文本处理功能

### 官方文档
https://getquicker.net/KC/Help/Doc/stringprocess

### 内部名称
sys:stringProcess

### 传入参数


**data**

名称: 待处理内容

说明: 需要进行文本处理的内容

类型: 字符串-Text



**method**

名称: 处理

说明: 对文本进行什么处理

类型: 选项-Enum



**srcEncoding**

名称: 编码

类型: 字符串-Text

默认值: utf-8



**dstEncoding**

名称: 目标编码

类型: 字符串-Text

默认值: gbk



**start**

名称: 开始位置

说明: 开始截取/插入位置，从0开始。如果为负值，表示从文本末尾开始向前的字符数。

类型: 数字(整数)-Integer

默认值: 0



**value**

名称: 内容

说明: 插入或追加的内容

类型: 字符串-Text



**length**

名称: 长度

说明: 截取或移除字符个数。截取时，0表示开始位置以后的所有内容，负值表示截取到结束前的多少个字符。

类型: 数字(整数)-Integer

默认值: 0



**totalWidth**

名称: 总宽度

说明: 补齐后的总字符数

类型: 数字(整数)-Integer

默认值: 10



**paddingChar**

名称: 填充字符

说明: 补齐时使用的填充字符，默认为空格。

类型: 字符串-Text

默认值:  



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**output**

名称: 结果

说明: 处理后的文本

类型: 字符串-Text



**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



### 范例


**范例1**
```json

```

***

## 运行子程序

### 功能描述
运行子程序

### 官方文档
https://getquicker.net/KC/Help/Doc/subprogram

### 内部名称
sys:subprogram

### 传入参数


**subProgram**

名称: 子程序

说明: 调用哪个子程序

类型: 字符串-Text

必填: True



**summary**

名称: Summary

说明: 内部使用

类型: 字符串-Text



**skipDebugOutput**

名称: 跳过调试输出

说明: 调试运行动作时，不输出子程序内部调试信息

类型: 布尔值-Boolean

默认值: False



**stopIfFail**

名称: 失败后停止

说明: 子程序运行失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 子程序是否运行成功

类型: 布尔值-Boolean



### 范例


**范例1**
```json

```

***

## 临时云存储

### 功能描述
将文本、文件、图片临时保存到云端并得到网址。

### 官方文档
https://getquicker.net/KC/Help/Doc/tempcloudstore

### 内部名称
sys:tempcloudstore

### 传入参数


**dataType**

名称: 数据类型

类型: 选项-Enum

默认值: text

必填: True



**text**

名称: 文本内容

说明: 要保存的文本内容

类型: 字符串-Text

必填: True



**imageVar**

名称: 图片变量

说明: 要保存的图片变量

类型: 图片-Image



**file**

名称: 文件路径

说明: 要保存的文件路径

类型: 字符串-Text

必填: True



**expireSeconds**

名称: 超时时间

说明: 请求超时时间（秒数）

类型: 数字(小数)-Number

默认值: 2.5



**useRandomFileName**

名称: 生成随机文件名

说明: 是否使用随机的文件名（仅适用于上传文件的情况）

类型: 布尔值-Boolean

默认值: False



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



**url**

名称: 网址

说明: 生成的访问网址

类型: 字符串-Text



### 范例


**范例1**
```json

```

***

## 用户输入

### 功能描述
请用户输入内容。

### 官方文档
https://getquicker.net/KC/Help/Doc/userInput

### 内部名称
sys:userInput

### 传入参数


**type**

名称: 类型

说明: 输入内容的类型

类型: 选项-Enum

默认值: text

必填: True



**prompt**

名称: 提示文字

说明: 提示用户输入什么内容。显示在输入框上方。

类型: 字符串-Text

默认值: 请输入内容

必填: True



**defaultValue**

名称: 默认值

说明: 默认填写到输入框中的内容

类型: 字符串-Text



**texttools**

名称: 文本选择工具

说明: 鼠标悬浮在文本框上时显示的小工具

类型: 字符串-Text



**extraSettings**

名称: 扩展设置

说明: 可用于自定义文本选择工具，详情请参考文档。

类型: 字符串-Text



**pattern**

名称: 验证表达式

说明: 正则验证表达式

类型: 字符串-Text



**isRequired**

名称: 必填

说明: 是否必须填写内容

类型: 布尔值-Boolean

默认值: False



**fontfamily**

名称: 字体名称

说明: 可选。设置字体名称。如有2个字体，使用逗号分隔。

类型: 字符串-Text



**fontsize**

名称: 字体大小

类型: 数字(小数)-Number

默认值: 14

必填: True



**winLocation**

名称: 窗口位置

说明: 在哪里显示选择窗口

类型: 选项-Enum

默认值: CenterScreen



**imeState**

名称: 输入法状态

类型: 选项-Enum

默认值: NO_CONTROL



**submitWithReturn**

名称: 回车提交结果（Shift+回车换行）

类型: 布尔值-Boolean

默认值: False



**restoreFocus**

名称: 恢复活动窗口

说明: 用户输入后，是否将焦点还原到之前的活动窗口

类型: 布尔值-Boolean

默认值: True



**closeOnDeactivated**

名称: 失去焦点后关闭窗口

类型: 布尔值-Boolean

默认值: False



**help**

名称: 帮助按钮内容

说明: 点击弹出显示帮助内容，MarkDown格式

类型: 字符串-Text



**topMost**

名称: 置顶显示

类型: 布尔值-Boolean

默认值: False



**stopIfFail**

名称: 失败后停止

说明: 用户取消后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



**textValue**

名称: 文本值

说明: 文本类型的输入值

类型: 字符串-Text



**numberValue**

名称: 数字值

说明: 数字类型的输入值

类型: 数字(小数)-Number



**datetimeValue**

名称: 日期时间值

类型: 时间日期-DateTime



**isEmpty**

名称: 是否为空

说明: 用户是否没有输入内容

类型: 布尔值-Boolean



### 范例


**范例1**
```json

```

***

## 等待剪贴板内容改变

### 功能描述
等待剪贴板的内容发生改变。等待第三方工具（如截图工具）完成操作并更新剪贴板。

### 官方文档
https://getquicker.net/KC/Help/Doc/waitclipboardchange

### 内部名称
sys:waitClipboardChange

### 传入参数


**maxWaitSeconds**

名称: 最长等待秒数

说明: 超过等待时间剪贴板未改变，则结束等待。

类型: 数字(小数)-Number

默认值: 10

必填: True



**recentChangeMs**

名称: 包含临近的改变

说明: 包含在此之前一定时间内(毫秒)发生的改变。

类型: 数字(整数)-Integer

默认值: 10

必填: True



**monitorWaitWin**

名称: 等待窗口关闭时取消

说明: 结合“等待窗口”模块，如果等待窗口关闭，则停止等待剪贴板变化。

类型: 布尔值-Boolean

默认值: False



**stopIfFail**

名称: 失败后中止动作

说明: 超时后剪贴板仍未改变，是否中止动作。

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否改变

说明: 剪贴板内容是否改变了

类型: 布尔值-Boolean



### 范例


**范例1**
```json

```

***

## 等待时间

### 功能描述
等待指定的毫秒数

### 官方文档
https://getquicker.net/KC/Help/Doc/delay

### 内部名称
sys:delay

### 传入参数


**delayMs**

名称: 等待时间

说明: 等待时间毫秒数

类型: 数字(整数)-Integer

默认值: 100

必填: True



**monitorWaitWin**

名称: 等待窗口关闭时取消

说明: 结合“等待窗口”模块，如果等待窗口关闭，则停止等待。仅当等待时间超过1000ms时生效

类型: 布尔值-Boolean

默认值: False



### 传出参数
无

### 范例


**范例1**
```json

```

***

## 窗口操作

### 功能描述
Window窗口相关操作

### 官方文档
https://getquicker.net/KC/Help/Doc/windowoperations

### 内部名称
sys:windowOperations

### 传入参数


**type**

名称: 类型

说明: 操作类型

类型: 选项-Enum

默认值: move

必填: True



**hWnd**

名称: 窗口句柄

说明: 要操作的窗口句柄（数字）。0或留空表示操作前台窗口。

类型: 数字(整数)-Integer



**x**

名称: X坐标

说明: 窗口左上角X坐标

类型: 数字(整数)-Integer

默认值: 100



**y**

名称: Y坐标

说明: 窗口左上角Y坐标

类型: 数字(整数)-Integer

默认值: 100



**width**

名称: 宽度

说明: 窗口宽度。-1时表示不更改窗口尺寸。

类型: 数字(整数)-Integer

默认值: 500



**height**

名称: 高度

说明: 窗口高度。-1时表示不更改窗口尺寸。

类型: 数字(整数)-Integer

默认值: 500



**area**

名称: 目标位置

说明: 窗口左,上,右,下的位置坐标

类型: 字符串-Text

默认值: 25%,25%,75%,75%



**showCmd**

名称: 显示状态

说明: 窗口显示状态，具体说明请参考Win32接口。

类型: 选项-Enum

默认值: 3

必填: True



**alpha**

名称: 不透明度Alpha

说明: 数字0-255：0为全透明，255为不透明。-数字：将当前透明度增加一些。+数字：将透明度减少一些。

类型: 字符串-Text

默认值: 128



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



**isTopmost**

名称: 是否置顶

说明: 操作后窗口是否为置顶

类型: 布尔值-Boolean



### 范例


**范例1**
```json

```

***

## 写入剪贴板

### 功能描述
将文本或图片等内容写入剪贴板

### 官方文档
https://getquicker.net/KC/Help/Doc/writeClipboard

### 内部名称
sys:writeClipboard

### 传入参数


**type**

名称: 类型

说明: 操作类型

类型: 选项-Enum

默认值: auto

必填: True



**customFormat**

名称: 格式名

说明: 自定义的剪贴板格式名

类型: 字符串-Text

必填: True



**input**

名称: 输入

说明: 要写入剪贴板的数据

类型: 任意类型-Any

必填: True



**html**

名称: HTML内容

说明: HTML代码片段

类型: 字符串-Text

必填: True



**text**

名称: 文本内容

说明: 纯文本格式内容。

类型: 字符串-Text

必填: True



**imageVar**

名称: 图片(变量)

说明: 要写入剪贴板的图片内容

类型: 图片-Image



**fastMode**

名称: 快速模式

说明: 不需要处理图片中的透明通道时选择

类型: 布尔值-Boolean

默认值: False



**successMsg**

名称: 成功后提示

说明: 可选。写入成功后提示消息，如“XXX已写入剪贴板”。

类型: 字符串-Text

必填: True



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



### 范例


**范例1**
```json

```

***

## 文件放入剪贴板

### 功能描述
将文件或文件列表存入剪贴板

### 官方文档
https://getquicker.net/KC/Help/Doc/filetoclipboard

### 内部名称
sys:fileToClipboard

### 传入参数


**file**

名称: 单个文件

说明: 要存入剪贴板的文件(夹)路径（与文件列表二选一）

类型: 字符串-Text



**list**

名称: 文件列表

说明: 要存入剪贴板的多个文件路径（与单个文件二选一）

类型: 文本列表-List



**useCut**

名称: 剪切文件

说明: 是否剪切文件

类型: 布尔值-Boolean

默认值: False



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



### 范例


**范例1**
```json

```

***

## WebView2浏览器窗口

### 功能描述
基于微软Edge浏览器内核的组件，需要安装Edge最新预览版方可使用。

### 官方文档
https://getquicker.net/KC/Help/Doc/webview2

### 内部名称
sys:webview2

### 传入参数


**type**

名称: 操作类型

类型: 选项-Enum

默认值: OpenUrl



**url**

名称: 网址或HTML内容

说明: 网页地址/文件路径或html代码内容

类型: 字符串-Text

必填: True



**urlList**

名称: 网址列表

说明: 每行一个：网址，或“标题|网址”，或“[图标]标题|网址”格式。

类型: 文本列表-List

必填: True



**additionalBrowserArguments**

名称: 附加的浏览器参数

说明: 用于设置代理等用途

类型: 字符串-Text

必填: True



**virtualHostToFolder**

名称: 虚拟主机映射

说明: 将文件夹映射为虚拟主机名。格式：主机名|文件夹路径。多个时，每行一个。
在html中可以使用https://servername/path/to/file.png的格式访问文件。

类型: 字符串-Text

必填: True



**userAgent**

名称: User Agent

说明: 可选。自定义UserAgent

类型: 字符串-Text



**title**

名称: 窗口标题

说明: 窗口标题文字。未设置时，自动使用网页标题。

类型: 字符串-Text

必填: True



**icon**

名称: 窗口图标

说明: 显示在窗口左上角的图标。支持fa:内置图报名:#RRGGBB或图标网址。

类型: 字符串-Text



**defaultBgColor**

名称: 默认背景色

说明: 可选。设置窗口的默认背景色。

类型: 字符串-Text



**autoCloseKey**

名称: 窗口标识

说明: (仅必要时使用)用于关闭之前打开的具有此标识的WebView2窗口。使用=表示当前动作ID。

类型: 字符串-Text

默认值: =



**modeForExists**

名称: 如果窗口已存在

类型: 选项-Enum

默认值: SkipThisStep



**script**

名称: JS脚本

说明: 可选。

类型: 字符串-Text

必填: True



**sendMessage**

名称: 消息内容

说明: Json格式的消息内容。词典变量会自动转换成json。

类型: 字符串-Text

必填: True



**winLocation**

名称: 窗口位置

说明: 在哪里显示选择窗口

类型: 选项-Enum

默认值: CenterScreen



**winSize**

名称: 窗口尺寸/位置

说明: 设置选择窗口的尺寸，格式为：宽度,高度。支持像素数值或屏幕宽高百分比，详情请参考模块文档。
“窗口位置” 类型为 “自定义位置” 时用于指定显示位置，格式为：left,top,right,bottom

类型: 字符串-Text



**defaultDownloadFolderPath**

名称: 默认下载文件夹

说明: 默认的文件下载存储目录

类型: 字符串-Text



**profileName**

名称: Profile

说明: 当需要同时登录一个网站的多个账号时，可以创建独立的Profile

类型: 字符串-Text



**topMost**

名称: 置顶显示

类型: 布尔值-Boolean

默认值: False



**showInTaskbar**

名称: 显示任务栏图标

类型: 布尔值-Boolean

默认值: True



**noActivate**

名称: 不占用焦点

说明: 不占用焦点时也无法在窗口中输入文字

类型: 布尔值-Boolean

默认值: False



**closeWhenLostFocus**

名称: 失去焦点后

类型: 选项-Enum

默认值: False



**escCloseWindow**

名称: 按Esc关闭窗口

类型: 布尔值-Boolean

默认值: False



**showToolbar**

名称: 显示工具栏

类型: 布尔值-Boolean

默认值: False



**windowStyle**

名称: 窗口风格

类型: 选项-Enum

默认值: normal



**clearCookies**

名称: 关闭窗口时清理Cookie

类型: 布尔值-Boolean

默认值: False



**addDevTool**

名称: 添加DevTools桥

类型: 布尔值-Boolean

默认值: False



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功。获取窗口信息时，窗口是否存在。

类型: 布尔值-Boolean



**isInstalled**

名称: 是否安装WebView2

类型: 布尔值-Boolean



**hWnd**

名称: 窗口句柄

类型: 数字(整数)-Integer



**webView**

名称: WebView2对象

说明: 可用于在C#脚本中使用，需运行在UI线程中。注意避免循环引用。

类型: 对象(Object)-Object



**lastLocation**

名称: 窗口位置

说明: 返回窗口坐标范围。格式为：left,top,right,bottom

类型: 字符串-Text



**currUri**

名称: 当前网址

说明: 浏览器当前网址

类型: 字符串-Text



**docTitle**

名称: 网页标题

类型: 字符串-Text



**sourceCode**

名称: 网页代码

类型: 字符串-Text



**cookies**

名称: Cookie

类型: 字符串-Text



**previewImage**

名称: 预览图

类型: 图片-Image



**isNavCompleted**

名称: 导航是否已结束

说明: 是否已完成网页加载过程

类型: 布尔值-Boolean



**scriptResult**

名称: 脚本运行结果

说明: json编码的脚本运行结果内容

类型: 字符串-Text



### 范例


**范例1**
```json

```

***

## 屏幕取色/颜色转换与计算

### 功能描述
转换颜色值及相关计算处理

### 官方文档
https://getquicker.net/KC/Help/Doc/color

### 内部名称
sys:color

### 传入参数


**type**

名称: 类型

说明: 比较方式

类型: 选项-Enum

默认值: fromString

必填: True



**colorStr**

名称: 颜色

说明: 颜色的文本值, 格式支持：#223344, #FF223344(ARGB顺序), Red, rgb(200,200,200), rgba(200,200,200,0.5), CMYK(0,0,0,0)或CMYK:0,0,0,0

类型: 字符串-Text

必填: True



**location**

名称: 坐标

说明: 格式为:“横坐标X,纵坐标Y”

类型: 字符串-Text

默认值: 0,0

必填: True



**format**

名称: 输出文本格式

说明: 输出的颜色文本值格式，用以转换颜色值的格式

类型: 选项-Enum

默认值: HEX_RGB

必填: True



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



**A**

名称: 透明度值

说明: Alpha值（0-255）0表示透明

类型: 数字(小数)-Number



**R**

名称: 红色值

说明: R值（0-255）

类型: 数字(小数)-Number



**G**

名称: 绿色值

说明: G值（0-255）

类型: 数字(小数)-Number



**B**

名称: 蓝色值

说明: B值（0-255）

类型: 数字(小数)-Number



**Hue**

名称: 色相

说明: Hue值（0-360）

类型: 数字(小数)-Number



**HslS**

名称: HSL.S

说明: HSL颜色空间的饱和度S

类型: 数字(小数)-Number



**HslL**

名称: HSL.L

说明: HSL颜色空间的亮度值L

类型: 数字(小数)-Number



**HsvS**

名称: HSV.S

说明: HSV颜色空间的饱和度S

类型: 数字(小数)-Number



**HsvV**

名称: HSV.V

说明: HSV颜色空间的明度V

类型: 数字(小数)-Number



**textValue**

名称: 文本值

说明: 输出颜色的文本值，格式请在输入参数中选择

类型: 字符串-Text



### 范例


**范例1**
```json

```

***

## 计算时间

### 功能描述
时间相关的计算操作

### 官方文档
https://getquicker.net/KC/Help/Doc/computetime

### 内部名称
sys:computeTime

### 传入参数


**type**

名称: 类型

说明: 比较方式

类型: 选项-Enum

默认值: getdate

必填: True



**time1**

名称: 日期时间

说明: 要计算的时间值

类型: 时间日期-DateTime

必填: True



**time2**

名称: 日期时间2

说明: 要计算的第二个时间值

类型: 时间日期-DateTime

必填: True



**formatString**

名称: 格式化字符串

说明: 时间差转换为文本时的格式化字符串。d:天数,hh:小时,mm:分钟,ss:秒。符号.:需要使用\转义

类型: 字符串-Text

默认值: d\.hh\:mm\:ss

必填: True



**addYears**

名称: 添加年数

说明: 添加指定的年数（整数）

类型: 数字(小数)-Number

默认值: 0



**addMonths**

名称: 添加月数

说明: 添加指定的月数（整数）结果不跨月，如1月31日增加1个月等于2月28日。

类型: 数字(小数)-Number

默认值: 0



**addDays**

名称: 添加天数

说明: 添加指定的天数（可以为小数）

类型: 数字(小数)-Number

默认值: 0



**addHours**

名称: 添加小时数

说明: 添加指定的小时数（可以为小数）

类型: 数字(小数)-Number

默认值: 0



**addMinutes**

名称: 添加分钟数

说明: 添加指定的分钟数（可以为小数）

类型: 数字(小数)-Number

默认值: 0



**addSeconds**

名称: 添加秒数

说明: 添加指定的秒数（可以为小数）

类型: 数字(小数)-Number

默认值: 0



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



**resultTime**

名称: 结果时间

说明: 计算的结果时间

类型: 时间日期-DateTime



**totalDays**

名称: 总天数

说明: 间隔的总天数值

类型: 数字(小数)-Number



**totalHours**

名称: 总小时数

说明: 间隔的总小时数

类型: 数字(小数)-Number



**totalMinutes**

名称: 总分钟数

说明: 间隔的总分钟数值

类型: 数字(小数)-Number



**totalSeconds**

名称: 总秒数

说明: 间隔的总秒数数值

类型: 数字(小数)-Number



**textValue**

名称: 文本值

说明: 时间间隔的文本结果

类型: 字符串-Text



### 范例


**范例1**
```json

```

***

## 词典操作

### 功能描述
对词典变量进行添加、删除等操作

### 官方文档
https://getquicker.net/KC/Help/Doc/dictoperations

### 内部名称
sys:dictOperations

### 传入参数


**type**

名称: 操作类型

类型: 选项-Enum

默认值: setOriginValue



**dict**

名称: 词典

说明: 要操作的词典变量

类型: 词典-Dict



**queryString**

名称: 查询字符串

说明: 要解析的查询字符串

类型: 字符串-Text



**key**

名称: 键

说明: 要操作元素的键值。

类型: 字符串-Text



**value**

名称: 值

说明: 要保存的内容

类型: 字符串-Text



**returnEmptyIfKeyNotExist**

名称: 键不存在时返回空值

说明: 此时不作为失败处理

类型: 布尔值-Boolean

默认值: False



**ignoreCase**

名称: 忽略键的大小写

类型: 布尔值-Boolean

默认值: False



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: False



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



**value**

名称: 结果

说明: 操作后的输出（取的元素值、键列表、值列表等）

类型: 任意类型-Any



### 范例


**范例1**
```json

```

***

## 使用Everything搜索文件

### 功能描述
调用Everything提供的接口搜索文件

### 官方文档
https://getquicker.net/KC/Help/Doc/everythingsearch

### 内部名称
sys:everythingsearch

### 传入参数


**search**

名称: 搜索内容

说明: 要搜索的内容，格式与直接在everything软件中搜索时相同。

类型: 字符串-Text

必填: True



**folder**

名称: 限定目录

说明: 可选。在指定目录下搜索（包含子目录）。

类型: 字符串-Text



**ext**

名称: 扩展名

说明: 可选。半角分号分隔的扩展名列表。如“txt;docx;xslx;”

类型: 字符串-Text



**matchWholeFilename**

名称: 匹配完整文件名

说明: 匹配整个文件名。0表示否，1表示是。

类型: 布尔值-Boolean

默认值: 0



**matchWholeWord**

名称: 匹配整个单词

说明: 匹配整个单词。如 quicker.exe 将会匹配：quicker.exe, quicker.exe.config等。0表示否，1表示是。

类型: 布尔值-Boolean

默认值: 1



**matchPath**

名称: 匹配路径

说明: 匹配路径的不同部分，而不仅是文件名。

类型: 布尔值-Boolean

默认值: 0



**matchCase**

名称: 匹配大小写

说明: 是否大小写敏感。0表示否，1表示是。

类型: 布尔值-Boolean

默认值: 0



**useRegex**

名称: 使用正则匹配

说明: 是否使用正则匹配。0表示否，1表示是。

类型: 布尔值-Boolean

默认值: 0



**maxCount**

名称: 最大结果数量

说明: -1表示不限制

类型: 数字(整数)-Integer

默认值: 100

必填: True



**sort**

名称: 排序方式

类型: 选项-Enum

默认值: 1

必填: True



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



**pathList**

名称: 路径列表

类型: 文本列表-List



**resultCount**

名称: 结果个数

类型: 数字(整数)-Integer



**rawResult**

名称: 原始结果

类型: 对象(Object)-Object



### 范例


**范例1**
```json

```

***

## 文件和目录操作

### 功能描述
文件和目录操作。请确保路径是合法的。

### 官方文档
https://getquicker.net/KC/Help/Doc/fileoperation

### 内部名称
sys:fileOperation

### 传入参数


**type**

名称: 操作类型

说明: 操作类型

类型: 选项-Enum

必填: True



**path**

名称: 路径

说明: 要操作的文件或文件夹路径

类型: 字符串-Text



**dstPath**

名称: 目标路径/名称

说明: 复制/移动的目标路径或新文件、文件名。详情请参考文档。

类型: 字符串-Text



**searchPattern**

名称: 搜索内容

说明: 筛选文件或目录名。可以包含通配符*和?，或“regex:正则表达式”。搜索文件时也可以为分号隔开的多个后缀名如.jpg;.png;.bmp

类型: 字符串-Text

默认值: *



**isAll**

名称: 包含子目录

说明: 包含子目录中的(否则只搜索顶层目录)

类型: 布尔值-Boolean

默认值: False



**overwrite**

名称: 覆盖已有

说明: 如果目标位置已存在文件，是否覆盖？

类型: 布尔值-Boolean

默认值: False



**stopIfFail**

名称: 失败后中止动作

说明: 如果操作异常，是否终止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



**files**

名称: 路径列表

说明: 搜索到的文件或文件夹列表

类型: 文本列表-List



**resultPath**

名称: 结果路径

说明: 结果文件路径

类型: 字符串-Text



### 范例


**范例1**
```json

```

***

## 生成临时文件路径

### 功能描述
根据指定的扩展名生成一个随机的临时文件名（完整路径），供后续步骤写入文件使用。

### 官方文档
https://getquicker.net/KC/Help/Doc/gentempfilepath

### 内部名称
sys:GenTempFilePath

### 传入参数


**ext**

名称: 扩展名

说明: 生成临时文件的扩展名

类型: 字符串-Text

默认值: .txt

必填: True



### 传出参数


**filePath**

名称: 文件路径

说明: 生成的临时文件路径

类型: 字符串-Text



### 范例


**范例1**
```json

```

***

## 获取选择的文件(夹)/选择特定文件

### 功能描述
获取资源管理器、桌面等位置选择的文件或文件夹的路径

### 官方文档
https://getquicker.net/KC/Help/Doc/getselectedfiles

### 内部名称
sys:getSelectedFiles

### 传入参数


**operation**

名称: 操作类型

类型: 选项-Enum

默认值: getSelection



**waitMs**

名称: 等待剪贴板时间

说明: 通过复制方式获取选择文件时，等待剪贴板变化的最长时间毫秒数。

类型: 数字(整数)-Integer

默认值: 200



**sortType**

名称: 排序文件列表

说明: 获取多个文件时，根据需要可以对文件列表进行排序。仅支持文件。

类型: 选项-Enum

默认值: Default



**pathList**

名称: 路径或文件名

说明: 要选中的路径或文件名。支持使用 “regex:表达式” “pinyin:筛选” 选择匹配的文件。

类型: 字符串-Text



**stopIfFail**

名称: 失败后中止动作

说明: 获取失败后，是否停止后续动作的执行。

类型: 布尔值-Boolean

默认值: True



**winHandle**

名称: 指定窗口句柄

说明: 指定要操作的资源管理器窗口，留空时表示前台窗口。（仅支持资源管理器）

类型: 数字(整数)-Integer



### 传出参数


**isSuccess**

名称: 是否成功

说明: 是否成功获得文件列表

类型: 布尔值-Boolean



**files**

名称: 路径列表

说明: 所有选中的文件和文件夹的路径列表

类型: 文本列表-List



**firstFile**

名称: 首个路径

说明: 选择1个文件(夹)时，返回其路径；选择多个时，返回第一个的路径。

类型: 字符串-Text



**fileNames**

名称: 文件(夹)名列表

说明: 所有选中的文件和文件夹的名称的列表（不包含所在路径）

类型: 文本列表-List



**firstFileName**

名称: 首个文件(夹)名

说明: 选择1个文件(夹)时，返回其名称；选择多个时，返回第一个的名称。

类型: 字符串-Text



**fileCount**

名称: 文件个数

说明: 选择的文件个数

类型: 数字(整数)-Integer



### 范例


**范例1**
```json

```

***

## 读取文件

### 功能描述
将读取的文本或图片内容写入变量。

### 官方文档
https://getquicker.net/KC/Help/Doc/readFile

### 内部名称
sys:readFile

### 传入参数


**path**

名称: 文件路径

说明: 要读取的文件的完整路径。

类型: 字符串-Text

必填: True



**type**

名称: 格式

说明: 文件内容类型

类型: 选项-Enum

默认值: text

必填: True



**encoding**

名称: 文件编码

说明: 文件的编码格式

类型: 选项-Enum

默认值: utf-8

必填: True



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**txt**

名称: 文本内容

说明: 读取的文本文件的内容

类型: 字符串-Text



**image**

名称: 图片内容

说明: 读取的图片文件的内容

类型: 图片-Image



**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



### 范例


**范例1**
```json

```

***

## 选择文件

### 功能描述
用文件选择对话框选择要打开或保存的文件

### 官方文档
https://getquicker.net/KC/Help/Doc/selectfile

### 内部名称
sys:selectFile

### 传入参数


**type**

名称: 操作类型

说明: 打开文件：选择一个已存在的文件。保存文件：选择文件要保存的目标位置。

类型: 选项-Enum

默认值: openFile

必填: True



**filter**

名称: 文件类型筛选器

说明: 文件类型筛选器，格式为：类型1|扩展名1|类型2|扩展名2。如：文本文件(*.txt)|*.txt|C#文件|*.cs|所有文件|*.*

类型: 字符串-Text

默认值: 文本文件|*.txt|所有文件|*.*



**defaultExt**

名称: 默认扩展名

说明: 默认的文件扩展名，应该是筛选器里的一种

类型: 字符串-Text

默认值: .txt



**initDir**

名称: 初始路径

说明: 初始文件夹路径

类型: 字符串-Text



**initFileName**

名称: 初始文件名

说明: 预选选择或设置的文件名

类型: 字符串-Text



**title**

名称: 对话框标题

说明: 选择窗口的标题

类型: 字符串-Text



**topMost**

名称: 置顶显示

说明: 是否置置顶显示窗口。

类型: 布尔值-Boolean

默认值: True



**stopIfFail**

名称: 取消后停止

说明: 取消后是否停止动作运行

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 是否成功选择了路径。

类型: 布尔值-Boolean



**path**

名称: 路径

说明: 选择的文件路径。

类型: 字符串-Text



**pathList**

名称: 路径列表

说明: 选择的文件路径列表。

类型: 文本列表-List



### 范例


**范例1**
```json

```

***

## 选择文件夹

### 功能描述
文件夹选择对话框

### 官方文档
https://getquicker.net/KC/Help/Doc/selectfolder

### 内部名称
sys:selectFolder

### 传入参数


**prompt**

名称: 提示文字

说明: 选择窗口的标题

类型: 字符串-Text

默认值: 请选择文件夹

必填: True



**initDir**

名称: 初始路径

说明: 初始文件夹路径

类型: 字符串-Text



**showOpenedDirs**

名称: 显示已打开的文件夹

说明: 显示当前在资源管理器窗口中打开的文件夹。

类型: 布尔值-Boolean

默认值: True



**stopIfFail**

名称: 取消后停止

说明: 取消后是否停止动作运行

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 是否成功选择了路径。

类型: 布尔值-Boolean



**path**

名称: 路径

说明: 选择的文件夹路径。

类型: 字符串-Text



### 范例


**范例1**
```json

```

***

## 写入文本文件

### 功能描述
将内容写入文本文件

### 官方文档
https://getquicker.net/KC/Help/Doc/writetextfile

### 内部名称
sys:WriteTextFile

### 传入参数


**content**

名称: 内容

说明: 要写入文件的内容

类型: 字符串-Text

必填: True



**filePath**

名称: 文件路径

说明: 要写入的完整文件路径（包含文件名）

类型: 字符串-Text

必填: True



**encoding**

名称: 文件编码

说明: 写入文件的编码格式

类型: 选项-Enum

默认值: utf-8

必填: True



**addUtf8Bom**

名称: 添加UTF-BOM

说明: UTF8编码文件是否写入BOM标记

类型: 布尔值-Boolean

默认值: False



**appendMode**

名称: 添加到文件末尾

说明: 如果文件已存在，则添加到文件的末尾

类型: 布尔值-Boolean

默认值: False



**addNewLine**

名称: 添加空行

说明: 在文件末尾添加空行

类型: 布尔值-Boolean

默认值: False



**newLineChars**

名称: 统一换行字符

类型: 选项-Enum

必填: True



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



### 范例


**范例1**
```json

```

***

## Zip压缩打包

### 功能描述
Zip压缩或解压缩

### 官方文档
https://getquicker.net/KC/Help/Doc/zip

### 内部名称
sys:zip

### 传入参数


**type**

名称: 操作类型

类型: 选项-Enum

默认值: Zip



**sourcePath**

名称: 源路径

说明: 待压缩的文件夹或文件路径。多个文件时每个文件一行。

类型: 字符串-Text

必填: True



**targetZipFile**

名称: Zip文件路径

说明: 压缩时：目标文件的路径。留空时自动生成临时文件。点(.)表示待压缩的文件夹或文件所在位置。

类型: 字符串-Text

必填: True



**sourceZipFile**

名称: Zip文件路径

说明: 待解压的文件路径。

类型: 字符串-Text

必填: True



**keepBaseFolder**

名称: 源路径为单个文件夹时，压缩整个文件夹（保留文件夹名称）

类型: 布尔值-Boolean

默认值: False



**outputPath**

名称: 目标路径

说明: 解压缩的目标路径, 点(.)表示zip文件所在的文件夹, 星(*)表示以zip文件名创建的子文件夹。

类型: 字符串-Text

必填: True



**password**

名称: 密码

说明: 压缩文件密码

类型: 字符串-Text



**comment**

名称: 备注

说明: 压缩文件注释内容

类型: 字符串-Text



**level**

名称: 级别

说明: 压缩级别，0-9。0表示不压缩（速度快），9表示压缩到最小（速度慢）

类型: 数字(整数)-Integer

默认值: 1



**overwrite**

名称: 自动覆盖文件

类型: 布尔值-Boolean

默认值: False



**skipOverwriteError**

名称: 覆盖失败时忽略

说明: 忽略掉无法覆盖的情况

类型: 布尔值-Boolean

默认值: False



**showProgress**

名称: 显示进度条

说明: 仅支持解压缩或压缩单个文件夹。

类型: 布尔值-Boolean

默认值: False



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



**resultPath**

名称: 结果路径

说明: 生成的zip文件完整路径，或解压缩后的完整路径

类型: 字符串-Text



### 范例


**范例1**
```json

```

***

## 屏幕截图

### 功能描述
截取屏幕区域

### 官方文档
https://getquicker.net/KC/Help/Doc/screencapture

### 内部名称
sys:screenCapture

### 传入参数


**type**

名称: 截图类型

说明: 截取图片的屏幕区域类型

类型: 选项-Enum

默认值: select



**area**

名称: 截图区域

说明: 要截取的屏幕坐标位置（像素值），格式为：left,top,right,bottom。默认不包含右边和底边像素。

类型: 字符串-Text



**windowHandle**

名称: 窗口句柄

说明: 要截取的窗口句柄数字。0或留空表示截取前台窗口。

类型: 数字(整数)-Integer

默认值: 0



**delay**

名称: 截图前延迟时间

说明: 等待多少毫秒后开始截图

类型: 数字(整数)-Integer

默认值: 0

必填: True



**preSelectArea**

名称: 预选截图区域

说明: 非必要请勿设置。预先选择的截图区域，格式为：left,top,right,bottom。默认不包含右边和底边像素。

类型: 字符串-Text



**includeRightBottomBorder**

名称: 预选截图区域包含右边和底边像素

说明: 包含时，当指定 0,0,2,2 的时候，截图的大小为3*3, 否则为2*2

类型: 布尔值-Boolean

默认值: True



**toClip**

名称: 写入剪贴板

说明: 截屏图片是否写入到剪贴板中

类型: 布尔值-Boolean

默认值: False



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**img**

名称: 图片

说明: 截图的图片

类型: 图片-Image



**rect**

名称: 截图区域

说明: 图片的截取区域(left,top,right,bottom)。

类型: 字符串-Text



**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



### 范例


**范例1**
```json

```

***

## 生成二维码

### 功能描述
将文本转换为二维码

### 官方文档
https://getquicker.net/KC/Help/Doc/createqrcode

### 内部名称
sys:createQrCode

### 传入参数


**code**

名称: 文本

说明: 要转换为二维码的内容

类型: 字符串-Text

必填: True



**pixelsPerModule**

名称: 每模块像素数

类型: 数字(整数)-Integer

默认值: 4



**darkColor**

名称: 暗色

说明: #AARRGGBB格式的颜色值

类型: 字符串-Text

默认值: #FF000000



**lightColor**

名称: 亮色

说明: #AARRGGBB格式的颜色值

类型: 字符串-Text

默认值: #FFFFFFFF



**icon**

名称: 图标

说明: 图片变量或图标文件路径

类型: 图片-Image



**iconPercent**

名称: 图标占比

说明: 百分比数字（只填数字，不写百分号）

类型: 数字(整数)-Integer

默认值: 15



**iconBorderWidth**

名称: 图标边框宽度

说明: 最小为1

类型: 数字(整数)-Integer

默认值: 6



**drawQuietZones**

名称: 绘制外框

类型: 布尔值-Boolean

默认值: 1



**saveToPdfPath**

名称: 输出pdf文件

类型: 字符串-Text



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



**img**

名称: 二维码图片

说明: 生成的二维码图片对象

类型: 图片-Image



**svg**

名称: SVG格式结果

说明: Svg格式结果代码

类型: 字符串-Text



**ascii**

名称: Ascii格式结果

说明: Ascii字符格式结果代码

类型: 字符串-Text



### 范例


**范例1**
```json

```

***

## 手写板

### 功能描述
手写内容，生成图片对象。

### 官方文档
https://getquicker.net/KC/Help/Doc/whiteboard

### 内部名称
sys:whiteboard

### 传入参数


**winPosition**

名称: 窗口位置

说明: 可选。指定显示位置，格式为：left,top,right,bottom。支持像素数值或屏幕宽高百分比。

类型: 字符串-Text

默认值: 15%,30%,85%,70%



**bgColor**

名称: 绘图区背景颜色

说明: 绘图窗口的背景颜色。格式为#AARRGGBB

类型: 字符串-Text

默认值: #FFFFFFFF



**penColor**

名称: 画笔颜色

说明: 画笔颜色。格式为#AARRGGBB

类型: 字符串-Text

默认值: #FFFF0000



**enableTransparent**

名称: 使用透明无边框窗口

说明: 不显示窗口标题栏，绘图区透明，可以看到底层窗口内容。

类型: 布尔值-Boolean

默认值: False



**imageWithBackground**

名称: 图片包含背景内容

说明: 使用透明窗口时，结果图片是否包含背景内容。

类型: 布尔值-Boolean

默认值: False



**stopIfFail**

名称: 取消后停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



**result**

名称: 结果图片

类型: 图片-Image



### 范例


**范例1**
```json

```

***

## 读取图片信息

### 功能描述
获取图片的尺寸或exif信息

### 官方文档
https://getquicker.net/KC/Help/Doc/imageinfo

### 内部名称
sys:imageinfo

### 传入参数


**sourceType**

名称: 图片来源

类型: 选项-Enum

默认值: var



**bmpFile**

名称: 文件路径

说明: 图片文件的完整路径

类型: 字符串-Text

必填: True



**bmpVar**

名称: 图片变量

类型: 图片-Image

必填: True



**autoRotate**

名称: 计算旋转后的宽高

说明: 如果Exif中包含旋转角度信息，则获取旋转后的宽高

类型: 布尔值-Boolean

默认值: False



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



**width**

名称: 宽度

类型: 数字(整数)-Integer



**height**

名称: 高度

类型: 数字(整数)-Integer



**rotateDegree**

名称: 旋转角度

类型: 数字(整数)-Integer



**dateTimeOriginal**

名称: 拍摄时间

类型: 时间日期-DateTime



**exifData**

名称: Exif数据

说明: 转换为文本格式的exif数据（词典格式，请参考模块文档）

类型: 词典-Dict



**rawExifData**

名称: 原始属性数据

说明: 原始Exif数据(词典格式，请参考模块文档)

类型: 词典-Dict



**fileTypeFromData**

名称: 内容图片格式

说明: 根据文件内容判断的文件格式（可能不准确），用于在无法根据扩展名得到图片格式的情况下使用。

类型: 字符串-Text



### 范例


**范例1**
```json

```

***

## 图片处理

### 功能描述
图片处理和变换

### 官方文档
https://getquicker.net/KC/Help/Doc/imgprocess

### 内部名称
sys:imgProcess

### 传入参数


**img**

名称: 图片

说明: 要转换的图片

类型: 图片-Image

必填: True



**type**

名称: 操作类型

说明: 对图片的转换操作类型

类型: 选项-Enum

默认值: resize_percent



**resizePercent**

名称: 缩放比例

说明: 缩小或放大到原来的百分之多少

类型: 数字(小数)-Number

默认值: 50



**maxWidth**

名称: 最大宽度

说明: 最大宽度(像素数)，0表示自动

类型: 数字(整数)-Integer

默认值: 0



**maxHeight**

名称: 最大高度

说明: 最大高度(像素数)，0表示自动

类型: 数字(整数)-Integer

默认值: 0



**rotation**

名称: 旋转方式

说明: 顺时针角度。0:不旋转, 1:90°, 2:180°, 3:270°, 其他值请参考模块文档。

类型: 数字(整数)-Integer

默认值: 0



**filterParams**

名称: 处理参数

说明: 每行设定一个处理步骤，具体设置请参考文档

类型: 字符串-Text



**iconFilePath**

名称: 图标文件保存路径

说明: 保存图标文件(.ico)的完整路径

类型: 字符串-Text

必填: True



**iconSize**

名称: 图标大小

说明: 图标中的位图大小，单位为像素。多尺寸图标可用英文逗号风格

类型: 字符串-Text

默认值: 256,48,32,16

必填: True



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



**result**

名称: 结果图片

说明: 处理后的图片

类型: 图片-Image



### 范例


**范例1**
```json

```

***

## 识别二维码

### 功能描述
识别图片中的二维码

### 官方文档
https://getquicker.net/KC/Help/Doc/readqrcode

### 内部名称
sys:readQrCode

### 传入参数


**img**

名称: 输入图片

说明: 要识别二维码的图片

类型: 图片-Image

必填: True



**tryNetwork**

名称: 本地识别失败后尝试在线识别服务

说明: 在线服务拥有更强识别能力（频率限制2秒/次，仅专业版提供）。

类型: 布尔值-Boolean

默认值: False



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



**code**

名称: 值

说明: 识别出的二维码内容

类型: 字符串-Text



**codeList**

名称: 全部二维码值

说明: 当一个图片含有多个二维码，且需要返回所有结果时使用。

类型: 文本列表-List



### 范例


**范例1**
```json

```

***

## 显示图片

### 功能描述
在屏幕上显示图片。输入文件路径/url或图片变量。

### 官方文档
https://getquicker.net/KC/Help/Doc/showImage

### 内部名称
sys:showImage

### 传入参数


**source**

名称: 操作/来源

说明: 图片来源类型

类型: 选项-Enum

默认值: var



**path**

名称: 路径/网址

说明: 图片文件的路径或网址。

类型: 字符串-Text

必填: True



**imgVar**

名称: 图片变量

说明: 从指定变量中加载图片

类型: 图片-Image

必填: True



**scale**

名称: 初始缩放比例

说明: 可以为小数，1表示原始大小，-1表示对大图自动调整缩放比例

类型: 数字(小数)-Number

默认值: 1

必填: True



**opacity**

名称: 不透明度

说明: 0-1之间的小数，1为完全不透明，0为完全透明。

类型: 数字(小数)-Number

默认值: 1

必填: True



**autoCloseKey**

名称: 唯一性标识

说明: (仅必要时使用)自动关闭之前打开的具有此标识的图片窗口。

类型: 字符串-Text



**autoCloseTime**

名称: 自动关闭时间

说明: 几秒后自动关闭，可以为小数。0：不自动关闭。

类型: 数字(小数)-Number

默认值: 0

必填: True



**winLocation**

名称: 显示位置

说明: 图片显示位置

类型: 选项-Enum

默认值: Auto



**winPosition**

名称: 位置坐标

说明: 仅用于位置为“自定义位置”类型。格式为:left,top或left,top,right,bottom

类型: 字符串-Text



**waitClose**

名称: 等待图片关闭

说明: 是否等待图片关闭后再执行后续步骤

类型: 布尔值-Boolean

默认值: False



**showDropShadow**

名称: 显示阴影

说明: 是否显示边框阴影

类型: 布尔值-Boolean

默认值: True



**showTaskbarIcon**

名称: 显示任务栏图标

说明: 是否显示任务栏图标

类型: 布尔值-Boolean

默认值: True



**topMost**

名称: 是否置顶显示

说明: 是否置顶显示图片

类型: 布尔值-Boolean

默认值: True



**noActivate**

名称: 不激活窗口

说明: 图片窗口显示时不抢占焦点（无法通过Esc关闭）

类型: 布尔值-Boolean

默认值: False



**closeWhenLostFocus**

名称: 丢失焦点时自动关闭

类型: 布尔值-Boolean

默认值: False



**tooltip**

名称: ToolTip提示文字

类型: 字符串-Text



### 传出参数


**isExists**

名称: 是否存在

说明: 是否存在指定标识的窗口

类型: 布尔值-Boolean



**hwnd**

名称: 窗口句柄

说明: 新创建的图片窗口的句柄

类型: 数字(整数)-Integer



**finalPosition**

名称: 最终贴图位置

说明: 移动窗口后的贴图位置格式为left,top,right,bottom。显示图片（开启“等待图片关闭” 选项）或获取当前打开的图片窗口信息时有效。

类型: 字符串-Text



**windowIdList**

名称: 窗口标识列表

类型: 文本列表-List



### 范例


**范例1**
```json

```

***

## 临时图床

### 功能描述
将图片上传到临时（1分钟后删除）的图床，用以搜图等场景。勿上传非法内容。

### 官方文档
https://getquicker.net/KC/Help/Doc/tempImgBed

### 内部名称
sys:tempImgBed

### 传入参数


**imgVar**

名称: 图片变量

说明: 指定要上传的图片变量。

类型: 图片-Image



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



**url**

名称: 网址

说明: 图片的临时网址

类型: 字符串-Text



### 范例


**范例1**
```json

```

***

## 图片/Base64 转换

### 功能描述
图片和Base64转换

### 官方文档
https://getquicker.net/KC/Help/Doc/imgtobase64

### 内部名称
sys:imgToBase64

### 传入参数


**type**

名称: 操作类型

说明: 转换操作类型

类型: 选项-Enum

默认值: imgToBase64



**img**

名称: 图片

说明: 要转换的图片（图片变量或文件路径）

类型: 图片-Image

必填: True



**addHeader**

名称: 添加data头

说明: 是否添加“data:image/png;base64,”头

类型: 布尔值-Boolean

默认值: False



**base64**

名称: Base64编码

说明: 要转换的编码文本

类型: 字符串-Text

必填: True



### 传出参数


**code**

名称: Base64编码

说明: Base64编码结果

类型: 字符串-Text



**img**

名称: 图片

说明: 转换输出的图片

类型: 图片-Image



### 范例


**范例1**
```json

```

***

## 写入图片文件

### 功能描述
将图片内容写入文件

### 官方文档
https://getquicker.net/KC/Help/Doc/writeimagefile

### 内部名称
sys:WriteImageFile

### 传入参数


**content**

名称: 内容图片

说明: 要写入文件的图片（变量）

类型: 图片-Image

必填: True



**filePath**

名称: 文件路径

说明: 要写入的文件完整路径（包含文件名）

类型: 字符串-Text

必填: True



**quality**

名称: 图片质量

说明: 保存为JPG格式时的图片质量参数。范围10-100。

类型: 字符串-Text

默认值: 95

必填: True



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



### 范例


**范例1**
```json

```

***

## 列表操作

### 功能描述
对列表变量进行添加、删除等操作

### 官方文档
https://getquicker.net/KC/Help/Doc/listoperations

### 内部名称
sys:listOperations

### 传入参数


**list**

名称: 列表

说明: 要操作的列表变量

类型: 文本列表-List



**type**

名称: 操作类型

类型: 选项-Enum

默认值: none



**list2**

名称: 列表2

说明: 要拼接的列表

类型: 文本列表-List



**pos**

名称: 序号

说明: 目标元素的序号，从0开始。负值表示从后向前的第几个。

类型: 数字(整数)-Integer

默认值: 0



**length**

名称: 长度

说明: 操作元素的数量

类型: 数字(整数)-Integer

默认值: 1



**item**

名称: 值

说明: 要插入或更新的值，或筛选关键词

类型: 字符串-Text



**orderByScore**

名称: 按匹配程度排序

说明: 筛选结果按匹配程度倒序排列

类型: 布尔值-Boolean

默认值: False



**pattern**

名称: 正则表达式

说明: 要匹配的正则表达式。

类型: 字符串-Text



### 传出参数


**value**

名称: 结果

说明: 操作后的输出（取的元素值、排序、切片或拼接后的列表等）

类型: 任意类型-Any



**isEmpty**

名称: 是否为空

说明: 空返回true，非空返回false

类型: 布尔值-Boolean



**length**

名称: 列表长度

说明: 列表包含的元素数量，截断或拼接后输出结果列表的长度

类型: 数字(整数)-Integer



**index**

名称: 序号

说明: 值在列表里的序号，-1表示不存在

类型: 数字(整数)-Integer



**filterOutItems**

名称: 剩余项列表

说明: 不符合筛选条件的项的列表

类型: 任意类型-Any



### 范例


**范例1**
```json

```

***

## 管理和排序列表

### 功能描述
对列表内容进行手工排序、添加、删除等操作

### 官方文档
https://getquicker.net/KC/Help/Doc/managelist

### 内部名称
sys:manageList

### 传入参数


**list**

名称: 列表

说明: 要操作的列表变量。直接选择对应变量，不要使用表达式。

类型: 文本列表-List



**winTitle**

名称: 窗口标题

类型: 字符串-Text



**note**

名称: 提示信息

类型: 字符串-Text



**parseData**

名称: 解析菜单数据

说明: 解析 “[图标]标题(tooltip)|值” 格式的数据并显示图标。

类型: 布尔值-Boolean

默认值: False



**seperator**

名称: 分隔符

说明: 解析菜单数据时，显示内容与值之间的分隔符，默认为竖线'|'

类型: 字符串-Text

默认值: |



**windowSize**

名称: 窗口宽度

说明: 可选，在需要自定义窗口宽度的情况下使用。最小值为200。

类型: 字符串-Text



**allowAdd**

名称: 允许添加项

类型: 布尔值-Boolean

默认值: True



**allowEdit**

名称: 允许编辑项

类型: 布尔值-Boolean

默认值: True



**allowDelete**

名称: 允许删除项

类型: 布尔值-Boolean

默认值: True



**stopIfFail**

名称: 取消后停止动作

类型: 布尔值-Boolean

默认值: False



**help**

名称: 帮助按钮内容

说明: 点击弹出显示帮助内容，MarkDown格式

类型: 字符串-Text



**titleDelegate**

名称: 显示内容提取表达式

说明: 可选，在不解析菜单数据时自定义每一项的显示内容。使用方式请参考模块文档。

类型: 字符串-Text



### 传出参数


**isSuccess**

名称: 是否确认

说明: 是否点击了确认按钮

类型: 布尔值-Boolean



### 范例


**范例1**
```json

```

***

## 赋值

### 功能描述
为变量赋值。

### 官方文档
https://getquicker.net/KC/Help/Doc/assign

### 内部名称
sys:assign

### 传入参数


**input**

名称: 输入

说明: 要赋值给变量的内容，可以直接是其他变量，也可以直接输入值或使用插值格式。

类型: 任意类型-Any

必填: True



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



**output**

名称: 输出

说明: 将数据写入到变量中

类型: 任意类型-Any



### 范例


**范例1**
```json

```

***

## 注释

### 功能描述
使用注释将步骤分组，描述后续步骤的目的。

### 官方文档
https://getquicker.net/KC/Help/Doc/comment

### 内部名称
sys:comment

### 传入参数


**note**

名称: 注释内容

说明: 注释内容

类型: 字符串-Text



### 传出参数
无

### 范例


**范例1**
```json

```

***

## 计算

### 功能描述
对表达式进行计算。

### 官方文档
https://getquicker.net/KC/Help/Doc/compute

### 内部名称
sys:compute

### 传入参数


**expression**

名称: 表达式

说明: 要计算的表达式

类型: 字符串-Text

默认值: 1+1

必填: True



**evalVar**

名称: 增强模式

说明: 支持在表达式中使用{变量名}和Math对象

类型: 布尔值-Boolean

默认值: False



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



**output**

名称: 结果

说明: 将表达式计算结果写入变量

类型: 任意类型-Any



### 范例


**范例1**
```json

```

***

## 生成Guid

### 功能描述
生成一个新的Guid(全局唯一ID标示符)，并转换为文本格式。

### 官方文档
https://getquicker.net/KC/Help/Doc/newguid

### 内部名称
sys:newGuid

### 传入参数


**format**

名称: 格式

说明: 转换为文本时使用的格式

类型: 选项-Enum

默认值: D



**upper**

名称: 大写

说明: 字母输出为大写格式。

类型: 布尔值-Boolean

默认值: False



### 传出参数


**output**

名称: 内容

说明: 将获得的文本写入到变量

类型: 字符串-Text



### 范例


**范例1**
```json

```

***

## 多字段表单

### 功能描述
使用表单窗口编辑多个变量的值。

### 官方文档
https://getquicker.net/KC/Help/Doc/form

### 内部名称
sys:form

### 传入参数


**operation**

名称: 工作模式

说明: 工作模式：编辑某个词典的值，或编辑一些变量的值

类型: 选项-Enum

默认值: variables



**dictVar**

名称: 词典变量

说明: 表单需要编辑的词典变量

类型: 词典-Dict



**title**

名称: 窗口标题

说明: 表单窗口标题文字

类型: 字符串-Text

默认值: 填写表单

必填: True



**formDef**

名称: 表单定义

类型: 表单-Form

必填: True



**formForDictDef**

名称: 表单定义(词典)

类型: 表单(词典)-FormForDict

必填: True



**dynamicFormForDictDef**

名称: 表单定义(词典)

说明: JSON格式的表单定义数据。格式说明请参考模块文档。

类型: 字符串-Text

必填: True



**help**

名称: 提示文字

说明: 帮助用户填写表单的提示文字。

类型: 字符串-Text



**markdownhelp**

名称: 帮助按钮内容

说明: 点击弹出显示帮助内容，MarkDown格式。

类型: 字符串-Text



**titleColumnWidth**

名称: 标题列宽度

说明: 左侧字段标题区域的宽度(逻辑像素)。负值，如-200表示自适应列宽且最大宽度为200。

类型: 数字(小数)-Number

默认值: 100



**windowWidth**

名称: 窗口宽度

说明: 逻辑像素，最小400。

类型: 数字(小数)-Number

默认值: 500

必填: True



**defaultInputWidth**

名称: 输入框默认宽度

说明: 逻辑像素，0表示自动宽度。

类型: 数字(小数)-Number

默认值: 0

必填: True



**windowHeight**

名称: 窗口最大高度

说明: 逻辑像素，0表示默认。设置时请填写大于100的值。

类型: 数字(小数)-Number

默认值: 0

必填: True



**restoreFocus**

名称: 恢复活动窗口

说明: 用户输入后，是否将焦点还原到之前的活动窗口

类型: 布尔值-Boolean

默认值: False



**topMost**

名称: 置顶显示

类型: 布尔值-Boolean

默认值: False



**confirm**

名称: 自定义“确定”按钮标题

说明: 仅在需要时填写。使用"_字符"的形式定义触发字符,如"_S"表示Alt+S可直接触发按钮

类型: 字符串-Text



**customButtons**

名称: 自定义按钮

说明: 使用"标题|返回值"的形式定义按钮，多个按钮用换行分隔。

类型: 字符串-Text



**selectedGroup**

名称: 选择的分组

说明: 使用分组标签页时，默认选择的分组。

类型: 字符串-Text



**winLocation**

名称: 窗口位置类型

说明: 在哪里显示选择窗口

类型: 选项-Enum

默认值: CenterScreen



**winSize**

名称: 位置

说明: 当 “窗口位置” 类型为 “自定义位置” 时用于指定显示位置，格式为：left,top,right,bottom

类型: 字符串-Text



**disableEnterSubmit**

名称: 关闭Enter提交表单功能

类型: 布尔值-Boolean

默认值: False



**stopIfFail**

名称: 取消后停止

说明: 取消后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



**button**

名称: 点击的按钮

说明: 默认的确认按钮返回值为空，自定义按钮返回值为自定义的值。

类型: 字符串-Text



**selectedGroup**

名称: 选择的分组

说明: 关闭时所选择的标签页分组。

类型: 字符串-Text



### 范例


**范例1**
```json

```

***

## 重放键鼠操作

### 功能描述
重放录制好的键鼠操作数据。

### 官方文档
https://getquicker.net/KC/Help/Doc/playrecord

### 内部名称
sys:playRecords

### 传入参数


**data**

名称: 录制数据

说明: 录制的键鼠操作数据

类型: 字符串-Text

必填: True



**speed**

名称: 重放速度

说明: 重放操作的速度

类型: 数字(小数)-Number

默认值: 2

必填: True



### 传出参数
无

### 范例


**范例1**
```json

```

***

## 录制键鼠操作

### 功能描述
录制键鼠操作过程

### 官方文档
https://getquicker.net/KC/Help/Doc/record

### 内部名称
sys:record

### 传入参数


**autoStart**

名称: 自动开始录制

说明: 2秒后是否自动开始录制

类型: 布尔值-Boolean

默认值: True



**recordMouseMove**

名称: 录制鼠标移动过程

说明: 是否录制鼠标的中间移动过程，仅必要时开启。关闭时仅记录点击位置。

类型: 布尔值-Boolean

默认值: True



**prepareSeconds**

名称: 准备时间

说明: 开始录制前的倒计时秒数（支持小数）

类型: 数字(小数)-Number

默认值: 2



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



**output**

名称: 录制数据

说明: 录制的结果数据

类型: 字符串-Text



### 范例


**范例1**
```json

```

***

## 运行脚本

### 功能描述
运行脚本。

### 官方文档
https://getquicker.net/KC/Help/Doc/runScript

### 内部名称
sys:runScript

### 传入参数


**script**

名称: 脚本内容

说明: 要运行的脚本内容

类型: 字符串-Text

必填: True



**type**

名称: 脚本类型

说明: 要执行的脚本类型

类型: 选项-Enum

默认值: CMD_K

必填: True



**ext**

名称: 扩展名

说明: 自定义脚本文件的扩展名(如: .ps1 )

类型: 字符串-Text

必填: True



**encoding**

名称: 文件编码

说明: 写入文件的编码格式

类型: 选项-Enum

默认值: default

必填: True



**runner**

名称: 使用指定软件

说明: 使用指定的程序运行脚本。如果双击脚本可以直接运行，则不需要指定。

类型: 字符串-Text

必填: True



**argTemplate**

名称: 命令行参数模板

说明: 使用指定软件时指定命令行参数的格式。%FILE% 代替脚本文件的路径。

类型: 字符串-Text

默认值: %FILE%

必填: True



**outputEncoding**

名称: 控制台输出编码

说明: 控制台输出编码。如果输出遇到乱码，尝试修改此选项。

类型: 选项-Enum

默认值: oem

必填: True



**workingDir**

名称: 工作目录

说明: 不填写（自动为资源管理器的当前目录或桌面目录）或具体的工作目录路径。

类型: 字符串-Text



**runAsAdmin**

名称: 以管理员身份运行

说明: 是否以管理员身份运行脚本。隐藏窗口或输出控制台内容时，不支持以管理员身份运行。

类型: 布尔值-Boolean

默认值: False



**waitToExit**

名称: 等待进程结束

说明: 等待此进程结束后再进行后续操作

类型: 布尔值-Boolean

默认值: False



### 传出参数


**stdout**

名称: 控制台输出

说明: 捕获控制台输出(输出stdout，为空时输出stderr)，会自动等待进程结束。输出此内容时，命令行窗口将不显示。

类型: 字符串-Text



**stdoutOnly**

名称: 标准输出

说明: 捕获标准输出(stdout)，会自动等待进程结束。输出此内容时，命令行窗口将不显示。

类型: 字符串-Text



**stderr**

名称: 错误输出

说明: 捕获错误输出(stderr)，会自动等待进程结束。输出此内容时，命令行窗口将不显示。

类型: 字符串-Text



### 范例


**范例1**
```json

```

***

## 状态存取

### 功能描述
存取状态数据；更新动作的徽标文字；设置附加的动作右键菜单项

### 官方文档
https://getquicker.net/KC/Help/Doc/stateStorage

### 内部名称
sys:stateStorage

### 传入参数


**type**

名称: 操作类型

类型: 选项-Enum

默认值: readActionState

必填: True



**key**

名称: 名称

说明: 存储或读取的状态条目名称。

类型: 字符串-Text



**defaultValue**

名称: 默认值

说明: 读取失败的时候返回的值

类型: 字符串-Text



**value**

名称: 值

说明: 要保存的状态值。使用*NULL*删除此状态的存储。

类型: 字符串-Text



**inputIfEmpty**

名称: 为空时请用户输入

说明: 如果读到的状态值为空，则弹出对话框请用户输入值。启用此选项时，请保持默认值为空。

类型: 布尔值-Boolean

默认值: False



**prompt**

名称: 用户输入提示

说明: 需要用户输入变量内容时，给用户的输入提示。

类型: 字符串-Text



**badgeText**

名称: 徽标文字

说明: 在动作右上角显示的提示文字

类型: 字符串-Text



**badgeColor**

名称: 徽标颜色

说明: 在动作右上角显示的徽标底色。留空表示透明。

类型: 字符串-Text



**badgeTextColor**

名称: 徽标文字颜色

类型: 字符串-Text



**actionContextMenu**

名称: 附加的右键菜单项

说明: 附加的动作右键菜单，格式请参考文档

类型: 字符串-Text



**overlayIcon**

名称: 徽标图标

说明: 使用内置矢量图标：“fa:图标名称:图标颜色”。如：“fa:Solid_Circle:#FF0000”

类型: 字符串-Text



### 传出参数


**isSuccess**

名称: 是否成功

说明: 是否成功获取了值

类型: 布尔值-Boolean



**value**

名称: 值

说明: 读取到的值

类型: 任意类型-Any



**isEmpty**

名称: 是否为空

说明: 读取到的值是否为空

类型: 布尔值-Boolean



### 范例


**范例1**
```json

```

***

## 下载文件

### 功能描述
下载网络文件(请勿用于下载大文件)

### 官方文档
https://getquicker.net/KC/Help/Doc/download

### 内部名称
sys:download

### 传入参数


**url**

名称: 网址

说明: 要下载的文件网址

类型: 字符串-Text

默认值: https://

必填: True



**savePath**

名称: 保存文件夹

说明: 下载文件的保存位置（文件夹的路径）

类型: 字符串-Text

必填: True



**saveName**

名称: 保存文件名

说明: 可选。为空时自动判断文件名。

类型: 字符串-Text

必填: True



**ua**

名称: UserAgent

说明: 可选。

类型: 字符串-Text



**header**

名称: 请求头

说明: 发送的HttpHeader。每行一个header，格式为Name:Value

类型: 字符串-Text



**cookie**

名称: Cookie

说明: 请求的cookie内容

类型: 字符串-Text



**expireSeconds**

名称: 超时秒数

说明: 长时间未接收到数据时，中止下载。

类型: 数字(小数)-Number

默认值: 10



**skipCertVerify**

名称: 忽略HTTPS证书验证

类型: 布尔值-Boolean

默认值: False



**showProgress**

名称: 显示进度条

说明: 是否显示下载进度条

类型: 布尔值-Boolean

默认值: False



**autoRename**

名称: 如果文件已存在，自动重命名下载的文件

说明: 在文件名后面增加“_序号”避免重复。否则将会覆盖已有文件。

类型: 布尔值-Boolean

默认值: False



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 是否成功下载了文件

类型: 布尔值-Boolean



**savedPath**

名称: 文件路径

说明: 文件的完整保存路径

类型: 字符串-Text



**contentMd5**

名称: 内容MD5

说明: 内容MD5值，不是所有请求都会返回此内容。

类型: 字符串-Text



**eTag**

名称: ETag

说明: 响应头Etag值，不是所有请求都会返回此内容。

类型: 字符串-Text



### 范例


**范例1**
```json

```

***

## 基础OCR

### 功能描述
获取图片中的文字

### 官方文档
https://getquicker.net/KC/Help/Doc/basic-ocr

### 内部名称
sys:basic-ocr

### 传入参数


**operation**

名称: 接口/引擎

说明: OCR接口或引擎。离线引擎安装方式请参考模块文档。

类型: 选项-Enum

默认值: QuickerServerOcr

必填: True



**apiKey**

名称: ApiKey

说明: 请填写OCR帐号的ApiKey

类型: 字符串-Text

必填: True



**secretKey**

名称: SecretKey

说明: 请填写OCR帐号的SecretKey

类型: 字符串-Text

必填: True



**imgVar**

名称: 图片变量

说明: 从指定变量中加载图片

类型: 图片-Image

必填: True



**punctuationType**

名称: 转换标点符号

说明: 合并文本时，是否转换标点符号

类型: 选项-Enum

默认值: no

必填: True



**mergeChapter**

名称: 合并段落

说明: 是否智能合并段落。

类型: 选项-Enum

默认值: no

必填: True



**interface**

名称: 接口名称或网址

说明: 接口的完整网址，或 https://aip.baidubce.com/rest/2.0/ocr/v1/ 后面的部分

类型: 字符串-Text



**options**

名称: 附加参数

说明: 请参考百度官方/Quicker服务接口说明。每行一个参数，使用option:value的格式。

类型: 词典-Dict



**lang**

名称: 语言

说明: 待识别内容的语言。表格识别仅支持中英混合和英文。

类型: 字符串-Text



**offlineMode**

名称: 离线模式

说明: 是否使用离线引擎。自动：安装离线引擎时使用离线，否则使用在线。

类型: 选项-Enum

默认值: Auto



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



**content**

名称: 合并后结果

说明: 合并在一起的的文本内容

类型: 字符串-Text



**textList**

名称: 行列表

说明: OCR识别结果，列表格式，每行一项。

类型: 文本列表-List



**rawData**

名称: 原始结果

说明: API接口返回的完整内容

类型: 字符串-Text



**rawObject**

名称: 原始结果JObject对象

说明: 返回结果的JObject对象

类型: 对象(Object)-Object



### 范例


**范例1**
```json

```

***

## 弹窗提示或确认

### 功能描述
弹窗显示提示或确认对话框

### 官方文档
https://getquicker.net/KC/Help/Doc/msgbox

### 内部名称
sys:MsgBox

### 传入参数


**operation**

名称: 模式

类型: 选项-Enum

默认值: default



**message**

名称: 消息内容

说明: 弹窗显示的消息内容。“自定义”模式时，也支持“MD:Markdown内容”。

类型: 字符串-Text

默认值: Hello.

必填: True



**title**

名称: 标题

说明: 消息窗口标题。留空时自动使用动作名称。

类型: 字符串-Text

默认值: Quicker

必填: True



**icon**

名称: 图标

说明: 消息窗口图标

类型: 选项-Enum

默认值: Asterisk

必填: True



**customIcon**

名称: 图标

说明: 消息窗口图标。

类型: 字符串-Text

默认值: Information

必填: True



**buttons**

名称: 按钮

说明: 消息窗口图标

类型: 选项-Enum

默认值: OK

必填: True



**customButtons**

名称: 按钮

说明: 每行定义一个按钮，格式为 “文本” 或 “[图标]显示文本(提示内容)|值”。

类型: 字符串-Text

默认值: [fa:Regular_Check:#4caf50]是(_Y)|Yes
[fa:Regular_Times:#dc3545]否(_N)|No
[fa:Light_Undo:#444444]取消(_C)|Cancel

必填: True



**defaultButton**

名称: 默认按钮

说明: 指定默认按钮的值。默认按钮以高亮颜色显示，可直接回车选择。

类型: 字符串-Text

默认值: Yes

必填: True



**restoreFocus**

名称: 恢复活动窗口

说明: 关闭弹窗后，是否将焦点还原到之前的活动窗口

类型: 布尔值-Boolean

默认值: True



### 传出参数


**result**

名称: 选择的按钮

说明: 点击的按钮，标准模式下结果可能为OK,Cancel,Yes,No，自定义模式下为按钮的值。

类型: 字符串-Text



**okOrYes**

名称: 是否确认

说明: 选择的按钮是否为“确定”或“是”

类型: 布尔值-Boolean



### 范例


**范例1**
```json

```

***

## 生成随机数

### 功能描述
生成随机数

### 官方文档
https://getquicker.net/KC/Help/Doc/randomnum

### 内部名称
sys:randomNum

### 传入参数


**min**

名称: 最小值

说明: 随机数范围的最小值（结果大于或等于此值）

类型: 数字(整数)-Integer

默认值: 0

必填: True



**max**

名称: 最大值

说明: 随机数范围的最大值（结果小于此值）

类型: 数字(整数)-Integer

默认值: 100

必填: True



### 传出参数


**output**

名称: 随机数

说明: 生成的随机数

类型: 数字(整数)-Integer



### 范例


**范例1**
```json

```

***

## Excel对象操作

### 功能描述
操作Excel的某个对象

### 官方文档
https://getquicker.net/KC/Help/Doc/excelobjects

### 内部名称
sys:excelObjects

### 传入参数


**operation**

名称: 操作类型

说明: 操作类型

类型: 选项-Enum

必填: True



**path**

名称: 文件/模板路径

说明: 完整路径。创建工作簿时，用于指定模板文件。

类型: 字符串-Text



**workbook**

名称: 工作簿对象

说明: 根据具体操作，可用参数不同。请参考文档。

类型: 对象(Object)-Object



**params**

名称: 参数

说明: 根据具体操作，可用参数不同。请参考文档。

类型: 字符串-Text



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



**activeWorkbook**

名称: 活动工作簿

说明: ActiveWorkbook

类型: 对象(Object)-Object



**activeSheet**

名称: 活动工作表

说明: ActiveSheet

类型: 对象(Object)-Object



**worksheetNames**

名称: 工作表名称的列表

说明: Worksheets

类型: 文本列表-List



**worksheets**

名称: 工作表对象列表

说明: Worksheets

类型: 对象(Object)-Object



**workbookPath**

名称: 工作簿路径

说明: Worksheets

类型: 字符串-Text



**application**

名称: Application对象

说明: Application对象的引用

类型: 对象(Object)-Object



### 范例


**范例1**
```json

```

***

## Excel区域操作

### 功能描述
操作Excel的某个区域或单元格

### 官方文档
https://getquicker.net/KC/Help/Doc/excelrange

### 内部名称
sys:excelRange

### 传入参数


**range**

名称: 区域

说明: 可以输入区域变量、留空(表示当前选择区域）、used(表示当前工作表的使用区域)或区域范围如A1:E9等，请参考文档。

类型: 对象(Object)-Object



**subRange**

名称: 限定子范围

说明: 根据需要，将要操作的目标限定为一个子区域

类型: 选项-Enum

默认值: FullArea

必填: True



**operation**

名称: 操作类型

说明: 操作类型

类型: 选项-Enum

默认值: SetValue

必填: True



**value**

名称: 参数

说明: 要设置的内容

类型: 任意类型-Any



**cellSize**

名称: 行高,列宽

说明: -表示不改变，auto表示自动，数字表示具体值。如auto,auto表示自适应高度和宽度

类型: 任意类型-Any



**style**

名称: 格式

说明: 要设置的格式内容。每行一个格式设置，请参考模块文档了解详细参数设置。

类型: 字符串-Text



**methods**

名称: 方法

说明: 要调用的方法，每行一个。格式请参考文档。

类型: 字符串-Text



**replaceWhat**

名称: 查找内容

说明: 要替换的内容

类型: 字符串-Text

必填: True



**replaceTo**

名称: 替换为

说明: 替换成的内容

类型: 字符串-Text

必填: True



**replaceEscapeWhat**

名称: 转义“查找内容”

说明: 替换“查找内容”中的转义字符（\r,\n,\t）

类型: 布尔值-Boolean

默认值: False



**replaceEscapeTo**

名称: 转义“替换为”

说明: 替换“替换为”中的转义字符（\r,\n,\t）

类型: 布尔值-Boolean

默认值: True



**replaceMatchCase**

名称: 区分大小写

类型: 布尔值-Boolean

默认值: False



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



**value**

名称: 值

说明: 单元格的值

类型: 任意类型-Any



**text**

名称: 文本

说明: 单元格的显示文本

类型: 字符串-Text



**formula**

名称: 公式

说明: 单元格的公式值

类型: 字符串-Text



**numberFormat**

名称: 数值格式

说明: 单元格数值格式值

类型: 字符串-Text



**address**

名称: 位置引用

说明: 区域位置范围

类型: 字符串-Text



**column**

名称: 列号

说明: 左上角单元格从1开始的列数

类型: 数字(整数)-Integer



**row**

名称: 行号

说明: 左上角单元格从1开始的行数

类型: 数字(整数)-Integer



**colNum**

名称: 列数

说明: 区域包含的列数

类型: 数字(整数)-Integer



**rowNum**

名称: 行数

说明: 区域包含的行数

类型: 数字(整数)-Integer



**style**

名称: 格式信息

说明: 单元格的格式

类型: 字符串-Text



**range**

名称: 区域对象

说明: Range对象

类型: 对象(Object)-Object



**sheet**

名称: 工作表对象

说明: WorkSheet对象

类型: 对象(Object)-Object



### 范例


**范例1**
```json

```

***

## 输入法状态

### 功能描述
获取或更改当前的输入法中英文状态，避免在发送热键时受影响。

### 官方文档
https://getquicker.net/KC/Help/Doc/imecontrol

### 内部名称
sys:imeControl

### 传入参数


**operation**

名称: 操作类型

说明: 要执行的操作。所有操作仅在输入法启用的情况下有效。

类型: 选项-Enum

默认值: GET_STATE

必填: True



### 传出参数


**isEnabled**

名称: 是否为中文状态

类型: 布尔值-Boolean



### 范例


**范例1**
```json

```

***

## 运行C#代码

### 功能描述
执行C#代码片段。代码中应包含主函数Exec(stepContext)，请参考文档说明。

### 官方文档
https://getquicker.net/KC/Help/Doc/csscript

### 内部名称
sys:csscript

### 传入参数


**mode**

名称: 运行模式

说明: 普通模式：在Quicker进程中执行；低权限模式：在单独的进程中执行，可用于COM操作。

类型: 选项-Enum

默认值: normal

必填: True



**script**

名称: 脚本内容

说明: 要运行的脚本内容

类型: 字符串-Text

默认值: //.cs  文件类型，便于外部编辑时使用
// 引用必要的命名空间
using System.Windows.Forms;

// Quicker将会调用的函数。可以根据需要修改返回值类型。
public static void Exec(Quicker.Public.IStepContext context)
{
    //var oldValue = context.GetVarValue("varName");  // 读取动作里的变量值
    //MessageBox.Show(oldValue as string);
    //context.SetVarValue("varName", "从脚本输出的内容。"); // 向变量里输出值
    MessageBox.Show("Hello World!");
}


必填: True



**scriptForLp**

名称: 脚本内容

说明: 要运行的脚本内容

类型: 字符串-Text

默认值: //.cs  文件类型，便于外部编辑时使用
// 引用必要的命名空间
using System.Windows.Forms;

// Quicker将会调用的函数
public static string Exec(string paramValue)
{
    System.Windows.Forms.MessageBox.Show("Hello World!");
    return "Hello World!";
}


必填: True



**scriptForAssembly**

名称: 脚本内容

说明: 要运行的脚本内容

类型: 字符串-Text

默认值: //.cs  文件类型，便于外部编辑时使用
// 引用必要的命名空间
using System.Windows.Forms;

namespace MyNamespace
{
    // Quicker将会调用的函数
    public static class MyClass
    {
        public static string Exec(string paramValue)
        {
            System.Windows.Forms.MessageBox.Show("Hello World!");
            return "Hello World!";
        }
    }
}


必填: True



**paramValue**

名称: 参数值

说明: 传递给Exec的参数

类型: 字符串-Text

必填: True



**reference**

名称: 引用DLL库

说明: 要引用的DLL文件，每行一个。

类型: 字符串-Text



**waitResp**

名称: 等待返回

说明: 是否等待脚本返回结果

类型: 布尔值-Boolean

默认值: True



**runOnUiThread**

名称: 执行线程

说明: 是否在界面线程上运行代码。如果在脚本中使用了wpf窗口，请选中此项。

类型: 选项-Enum

默认值: auto



**enableCache**

名称: 允许缓存程序集

说明: 是否使用缓存的程序集

类型: 布尔值-Boolean

默认值: False



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



**waitMs**

名称: 最长等待时间(ms)

说明: 最长的等待返回结果的，毫秒数

类型: 数字(小数)-Number

默认值: 10000

必填: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



**resp**

名称: 返回内容

说明: 脚本执行返回的结果文本

类型: 字符串-Text



**rtn**

名称: 返回内容

说明: Exec方法的返回值

类型: 字符串-Text



**rtnAssembly**

名称: 程序集对象

说明: 生成的Assembly对象（已经加载）

类型: 对象(Object)-Object



**assemblyPath**

名称: 程序集路径

说明: 生成的Assembly路径

类型: 字符串-Text



### 范例


**范例1**
```json

```

***

## 运行Javascript代码

### 功能描述
执行Js代码片段。代码中应包含主函数exec()，请参考文档。

### 官方文档
https://getquicker.net/KC/Help/Doc/jsscript

### 内部名称
sys:jsscript

### 传入参数


**script**

名称: 脚本内容

说明: 要运行的脚本内容

类型: 字符串-Text

默认值: //.js 主函数 exec()
function exec(){
 var localName = quickerGetVar('text');  // 读取text变量值, (text 是动作里的变量)
 quickerSetVar('text', 'Hello, ' + localName ); //输出修改后的值到text变量中。
 return 0; //返回0表示成功。返回其他数字表示失败。
}


必填: True



**allClr**

名称: 允许访问.Net程序集

说明: 是否需要在js代码中访问.Net程序集

类型: 布尔值-Boolean

默认值: False



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



**return**

名称: 返回值

说明: 脚本代码返回的数字值。

类型: 数字(整数)-Integer



### 范例


**范例1**
```json

```

***

## 运行Python代码

### 功能描述
执行Python代码片段。

### 官方文档
https://getquicker.net/KC/Help/Doc/pythonscript

### 内部名称
sys:pythonscript

### 传入参数


**script**

名称: 脚本内容

说明: 要运行的脚本内容

类型: 字符串-Text

默认值: ##.py 
quicker.context.SetVarValue('text', 'hello world')


必填: True



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



### 范例


**范例1**
```json

```

***

## 等待按键

### 功能描述
等待用户按下某个按键

### 官方文档
https://getquicker.net/KC/Help/Doc/waitkeyboard

### 内部名称
sys:waitKeyboard

### 传入参数


**operation**

名称: 操作类型

类型: 选项-Enum

默认值: waitKeyDown



**waitingKeys**

名称: 等待的按键

说明: 可选，留空表示任意键盘按键。格式请参考文档。

类型: 字符串-Text



**modifierKeys**

名称: 修饰键

说明: 可选。逗号分隔的ctrl,shift,alt,win组合。仅用于等待组合快捷键。修饰键不会被拦截。

类型: 字符串-Text



**maxWaitSeconds**

名称: 最长等待秒数

说明: 0为永久超时超过等待时间，则结束等待。

类型: 数字(小数)-Number

默认值: 0

必填: True



**filterEvent**

名称: 拦截原始按键事件

说明: 避免按键输入到窗口中 (仅对键盘按键有效)

类型: 布尔值-Boolean

默认值: True



**waitKeyUp**

名称: 等待按键抬起

说明: 等待按键抬起后再返回 (仅对键盘按键有效)

类型: 布尔值-Boolean

默认值: False



**ignoreSimulated**

名称: 忽略模拟的按键

说明: 是否忽略（不检测）模拟的按键消息

类型: 布尔值-Boolean

默认值: False



**help**

名称: 提示信息

说明: 等待按键时显示的提示文字

类型: 字符串-Text

默认值: 请按键...



**fontfamily**

名称: 字体名称

说明: 可选。设置字体名称。如有多个字体，使用逗号分隔。

类型: 字符串-Text



**winLocation**

名称: 提示窗口位置

说明: 在哪里显示提示窗口

类型: 选项-Enum

默认值: TopCenter



**mouseThrough**

名称: 鼠标穿透

说明: 鼠标是否可以穿透提示窗口点击下面的内容

类型: 布尔值-Boolean

默认值: True



**stopIfFail**

名称: 失败后停止动作

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 步骤执行是否成功

说明: 步骤执行是否成功

类型: 布尔值-Boolean



**keyCode**

名称: 键名

说明: 按键名，具体请参考模块文档。

类型: 字符串-Text



**keyValue**

名称: 键值

说明: 按键数值，具体请参考模块文档。

类型: 数字(整数)-Integer



**holdTimeMs**

名称: 按下保持时间

说明: 按下保持时间，单位毫秒。仅支持键盘按键。

类型: 数字(整数)-Integer



### 范例


**范例1**
```json

```

***

## 窗口界面控制(FlaUI)

### 功能描述
触发Windows窗口的菜单/按钮等控件(通过FlaUI库实现)。

### 官方文档
https://getquicker.net/KC/Help/Doc/uiautomation

### 内部名称
sys:flauiautomation

### 传入参数


**type**

名称: 操作类型

说明: 操作类型。按下和抬起需要配对使用。

类型: 选项-Enum

默认值: TriggerMenu



**window**

名称: 窗口句柄

说明: 要操作哪个窗口的控件。不填写=使用前台窗口；或窗口句柄数字。

类型: 字符串-Text



**menuPath**

名称: 菜单路径

说明: 菜单的展开路径。每行写一个级别的菜单名（需完全匹配）

类型: 字符串-Text



**expandDelay**

名称: 展开延时

说明: 等待下级菜单展开的时间(ms)

类型: 数字(整数)-Integer

默认值: 200



**control**

名称: 控件XPath或Name

说明: 控件的XPath或Name。XPath以/开始。

类型: 字符串-Text



**controlType**

名称: 控件类型

说明: 可选。当有多个名称相同但类型不同的控件时区分。

类型: 选项-Enum

默认值: 0



**controlOperation**

名称: 动作

说明: 对控件执行的操作。

类型: 选项-Enum

默认值: Auto



**value**

名称: 值

说明: 仅用于 “设置值” 操作。

类型: 字符串-Text



**pointLocation**

名称: 坐标位置

说明: 指定要检查的控件的屏幕坐标位置，格式为“x,y”

类型: 字符串-Text



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



**value**

名称: 值

说明: 控件的值

类型: 字符串-Text



**controlText**

名称: 文本

说明: 获取控件上的文本。根据控件不同，可能从Value、Text、Name等信息获取。

类型: 字符串-Text



**rect**

名称: 位置

说明: 控件坐标位置

类型: 字符串-Text



**controlName**

名称: 控件名称

类型: 字符串-Text



**controlType**

名称: 控件类型

类型: 字符串-Text



**controlXPath**

名称: 控件XPath

类型: 字符串-Text



**controlTypeId**

名称: 控件类型ID

类型: 数字(整数)-Integer



**controlInfo**

名称: 其他信息

类型: 词典-Dict



**controlIsEnabled**

名称: 是否启用

说明: 控件未处于禁用状态

类型: 布尔值-Boolean



**controlIsVisible**

名称: 是否可见

说明: 控件是否在屏幕上。

类型: 布尔值-Boolean



**element**

名称: 原始对象

说明: 返回控件的AutomationElement对象

类型: 对象(Object)-Object



### 范例


**范例1**
```json

```

***

## 按键操作

### 功能描述
单个键盘按键的操作控制或状态获取

### 官方文档
https://getquicker.net/KC/Help/Doc/keyoperation

### 内部名称
sys:keyoperation

### 传入参数


**type**

名称: 类型

说明: 操作类型。按下和抬起需要配对使用。

类型: 选项-Enum

默认值: get_key_state



**key**

名称: 按键

说明: 要操作或检查状态的按键(单个)。可以为键值或键名，具体请参考文档。

类型: 字符串-Text



**getRealMouseState**

名称: 获取按键的实际状态（在远程时无法获取）

类型: 布尔值-Boolean

默认值: False



**keepMs**

名称: 保持按下时间

说明: 保持此虚拟键按下的时间（毫秒数），之后会自动抬起。

类型: 数字(整数)-Integer

默认值: 1000



### 传出参数


**isDown**

名称: 是否按下

说明: 此按键是否为按下状态

类型: 布尔值-Boolean



**isToggled**

名称: 是否锁定

说明: 此按键是否为锁定状态，仅对CapsLock、NumLock等按键有效。

类型: 布尔值-Boolean



### 范例


**范例1**
```json

```

***

## 窗口界面控制

### 功能描述
触发Windows窗口的菜单/按钮等控件。

### 官方文档
https://getquicker.net/KC/Help/Doc/uiautomation

### 内部名称
sys:uiautomation

### 传入参数


**type**

名称: 操作类型

说明: 操作类型。按下和抬起需要配对使用。

类型: 选项-Enum

默认值: TriggerMenu



**window**

名称: 窗口句柄

说明: 要操作哪个窗口的控件。不填写=使用前台窗口；或窗口句柄数字。

类型: 字符串-Text



**menuPath**

名称: 菜单路径

说明: 菜单的展开路径。每行写一个级别的菜单名（需完全匹配）

类型: 字符串-Text



**expandDelay**

名称: 展开延时

说明: 等待下级菜单展开的时间(ms)

类型: 数字(整数)-Integer

默认值: 200



**control**

名称: 控件名

说明: 控件名，请确保唯一性。

类型: 字符串-Text



**controlType**

名称: 控件类型

说明: 可选。当有多个名称相同但类型不同的控件时区分。

类型: 选项-Enum

默认值: 0



**controlOperation**

名称: 动作

说明: 对控件执行的操作。

类型: 选项-Enum

默认值: Auto



**value**

名称: 值

说明: 仅用于 “设置值” 操作。

类型: 字符串-Text



**path**

名称: 路径

说明: 要更新的路径

类型: 字符串-Text



**autoCreateDir**

名称: 自动创建文件夹

说明: 如果目录不存在则自动创建。

类型: 选项-Enum

默认值: no



**pointLocation**

名称: 坐标位置

说明: 指定要检查的控件的屏幕坐标位置，格式为“x,y”

类型: 字符串-Text



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



**value**

名称: 值

说明: 控件的值

类型: 字符串-Text



**controlText**

名称: 文本

说明: 获取控件上的文本。根据控件不同，可能从Value、Text、Name等信息获取。

类型: 字符串-Text



**rect**

名称: 位置

说明: 控件坐标位置

类型: 字符串-Text



**controlName**

名称: 控件名称

类型: 字符串-Text



**controlType**

名称: 控件类型

类型: 字符串-Text



**controlIsEnabled**

名称: 是否启用

说明: 控件未处于禁用状态

类型: 布尔值-Boolean



**controlIsVisible**

名称: 是否可见

说明: 控件是否在屏幕上。

类型: 布尔值-Boolean



**controlNativeWindowHandle**

名称: 原始句柄

说明: 控件的原始窗口句柄(NativeWindowHandle)

类型: 数字(整数)-Integer



**controlTypeId**

名称: 控件类型ID

类型: 数字(整数)-Integer



### 范例


**范例1**
```json

```

***

## 获取字符信息

### 功能描述
获取字符信息

### 官方文档
https://getquicker.net/KC/Help/Doc/charInfo

### 内部名称
sys:charInfo

### 传入参数


**char**

名称: 字符

说明: 要获取编码的字符，如果是多个字符，则取第一个。

类型: 字符串-Text

默认值: 中

必填: True



### 传出参数


**unicodeNum**

名称: Unicode编码(数字)

说明: 字符的Unicode编码数字

类型: 数字(整数)-Integer



**unicodeHex**

名称: Unicode编码(十六进制)

说明: 字符的Unicode编码数字的十六进制，如“中”的Unicode编码十六进制为“4E2D”

类型: 字符串-Text



**pinyinFirstChar**

名称: 拼音首字母

说明: 字母的拼音首字母(仅第一个常用读音)

类型: 字符串-Text



**pinyin**

名称: 拼音

说明: 字母的拼音(多音字只输出第一个常用读音)

类型: 字符串-Text



**pinyinFirstCharAll**

名称: 拼音首字母(全部)

说明: 字母的拼音首字母(多音字输出所有读音)

类型: 字符串-Text



**pinyinAll**

名称: 拼音(全部)

说明: 字母的拼音(多音字输出所有读音，空格分隔)

类型: 字符串-Text



### 范例


**范例1**
```json

```

***

## 组合成文本

### 功能描述
将（多个）变量组合成一段文本。

### 官方文档
https://getquicker.net/KC/Help/Doc/formatstring

### 内部名称
sys:formatString

### 传入参数


**formatString**

名称: 格式化字符串

说明: 使用C#的String.Format语法。

类型: 字符串-Text

默认值: {0}

必填: True



**p0**

名称: 参数0

说明: 第 0 个参数

类型: 任意类型-Any



**p1**

名称: 参数1

说明: 第 1 个参数

类型: 任意类型-Any



**p2**

名称: 参数2

说明: 第 2 个参数

类型: 任意类型-Any



**p3**

名称: 参数3

说明: 第 3 个参数

类型: 任意类型-Any



**p4**

名称: 参数4

说明: 第 4 个参数

类型: 任意类型-Any



### 传出参数


**output**

名称: 结果

说明: 生成的文本内容

类型: 字符串-Text



### 范例


**范例1**
```json

```

***

## 提取HTML内容

### 功能描述
从HTML代码中提取内容

### 官方文档
https://getquicker.net/KC/Help/Doc/htmlextract

### 内部名称
sys:htmlExtract

### 传入参数


**operation**

名称: 操作类型

类型: 选项-Enum

默认值: extractText



**source**

名称: 源HTML

说明: 原始HTML内容，或网址，或根节点对象

类型: 字符串-Text

必填: True



**encoding**

名称: 网页编码类型

说明: 通过网址加载内容时，使用指定的编码。留空时默认为UTF8。

类型: 字符串-Text



**xpath**

名称: 节点XPath

说明: 内容的XPath，详细说明请参考文档

类型: 字符串-Text

必填: True



**selectTarget**

名称: 提取方式

说明: 提取单个节点还是符合条件的所有节点。

类型: 选项-Enum

默认值: single



**returnType**

名称: 提取内容类型

说明: 要提取的节点信息。

类型: 选项-Enum

默认值: InnerHtml



**attribute**

名称: 属性名称

说明: 仅在提取节点属性时有效。指定属性的名称。

类型: 字符串-Text



**writeToSheet**

名称: 写入工作表对象

说明: 将提取到的表格内容写入工作表对象中。

类型: 对象(Object)-Object



**stopIfFail**

名称: 失败后停止动作

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 步骤执行是否成功

说明: 步骤执行是否成功

类型: 布尔值-Boolean



**value**

名称: 提取值

说明: 提取的内容。请确保结果类型和变量类型匹配。

类型: 任意类型-Any



**rootNode**

名称: 根节点

说明: 整个HTML源内容对应的HtmlNode节点对象，可用于后续处理使用。

类型: 任意类型-Any



### 范例


**范例1**
```json

```

***

## 列表合并成文本

### 功能描述
将列表拼接为一段文本

### 官方文档
https://getquicker.net/KC/Help/Doc/joinlist

### 内部名称
sys:joinList

### 传入参数


**list**

名称: 输入

说明: 要拼接为文本的列表

类型: 文本列表-List

必填: True



**separator**

名称: 分隔文本

说明: 拼接内容时，两项之间的内容。

类型: 字符串-Text

默认值: ,

必填: True



**escapeSeparator**

名称: 转义“分隔文本”

说明: 替换“分隔文本”中的转义字符（\r,\n,\t）

类型: 布尔值-Boolean

默认值: False



### 传出参数


**output**

名称: 结果

说明: 生成的文本内容

类型: 字符串-Text



### 范例


**范例1**
```json

```

***

## 提取JSON内容

### 功能描述
提取Json文本中的信息

### 官方文档
https://getquicker.net/KC/Help/Doc/jsonExtract

### 内部名称
sys:jsonExtract

### 传入参数


**data**

名称: 输入

说明: 要从中提取内容的Json文本或JToken对象

类型: 字符串-Text

必填: True



**p0**

名称: 提取路径0

类型: 字符串-Text



**p1**

名称: 提取路径1

类型: 字符串-Text



**p2**

名称: 提取路径2

类型: 字符串-Text



**p3**

名称: 提取路径3

类型: 字符串-Text



**p4**

名称: 提取路径4

类型: 字符串-Text



**dateAsString**

名称: 日期时间按照文本处理

说明: 保留原有数据格式

类型: 布尔值-Boolean

默认值: False



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否没有异常

类型: 布尔值-Boolean



**v0**

名称: 值0

说明: 提取到的内容，和提取路径对应

类型: 任意类型-Any



**v1**

名称: 值1

说明: 提取到的内容，和提取路径对应

类型: 任意类型-Any



**v2**

名称: 值2

说明: 提取到的内容，和提取路径对应

类型: 任意类型-Any



**v3**

名称: 值3

说明: 提取到的内容，和提取路径对应

类型: 任意类型-Any



**v4**

名称: 值4

说明: 提取到的内容，和提取路径对应

类型: 任意类型-Any



**rootToken**

名称: 根对象

说明: 整个输入内容解析后获得的JToken对象。可用于后续使用。

类型: 对象(Object)-Object



### 范例


**范例1**
```json

```

***

## 提取文件路径信息/生成路径

### 功能描述
从文件路径中提取文件名、文件夹等信息

### 官方文档
https://getquicker.net/KC/Help/Doc/pathExtraction

### 内部名称
sys:pathExtraction

### 传入参数


**operation**

名称: 操作类型

类型: 选项-Enum

默认值: getInfo



**path**

名称: 路径

说明: 待处理或拼接的路径

类型: 字符串-Text

必填: True



**newExtension**

名称: 新的扩展名

说明: 新的扩展名，如：.png

类型: 字符串-Text

必填: True



**newFileName**

名称: 新的文件名

说明: 新的文件名，如：abcd.png

类型: 字符串-Text

必填: True



**newFileNameWithoutExt**

名称: 新的文件名

说明: 新的文件名(不包含扩展名），如：newfile

类型: 字符串-Text

必填: True



**newDir**

名称: 目标目录路径

说明: 目标存储路径，如：d:\Work\Test

类型: 字符串-Text

必填: True



**path2**

名称: 路径部分2

类型: 字符串-Text

必填: True



**path3**

名称: 路径部分3

类型: 字符串-Text

必填: True



**path4**

名称: 路径部分4

类型: 字符串-Text

必填: True



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 提取过程是否没有遇到异常

类型: 布尔值-Boolean



**resultPath**

名称: 结果路径

说明: 生成的结果路径

类型: 字符串-Text



**name**

名称: 文件名

说明: 去除路径的文件名

类型: 字符串-Text



**nameNoExt**

名称: 文件名(去掉扩展名)

说明: 去除扩展名的文件名

类型: 字符串-Text



**ext**

名称: 扩展名

说明: 文件的扩展名

类型: 字符串-Text



**path**

名称: 所在文件夹路径

说明: 父目录路径

类型: 字符串-Text



### 范例


**范例1**
```json

```

***

## 正则提取

### 功能描述
使用正则表达式提取指定内容

### 官方文档
https://getquicker.net/KC/Help/Doc/regexextract

### 内部名称
sys:regexExtract

### 传入参数


**getGroup**

名称: 提取方式

说明: 输出的内容根据提取内容有所不同，请参考模块文档。

类型: 选项-Enum

默认值: 0

必填: True



**data**

名称: 输入

说明: 要提取内容的文本

类型: 字符串-Text

必填: True



**pattern**

名称: 正则表达式

说明: 用于提取内容的正则表达式

类型: 字符串-Text

必填: True



**ignoreCase**

名称: 忽略大小写

说明: 不区分英文大小写

类型: 布尔值-Boolean

默认值: False



**singleLine**

名称: 单行模式

说明: 此模式下“.”能匹配任意字符，包括换行符。(否则匹配除了\n外的任意字符)

类型: 布尔值-Boolean

默认值: False



**multiLine**

名称: 多行模式

说明: 此模式下^和$可以分别匹配行首和行尾。(否则匹配输入内容的开始和结束)

类型: 布尔值-Boolean

默认值: False



**rightToLeft**

名称: 从右向左

说明: 从右向左查找匹配内容

类型: 布尔值-Boolean

默认值: False



**stopIfFail**

名称: 失败后中止动作

说明: 操作失败后，是否停止后续动作的执行。

类型: 布尔值-Boolean

默认值: True



### 传出参数


**matches**

名称: 所有匹配列表

说明: 返回所有的匹配项

类型: 文本列表-List



**match1 **

名称: 匹配1

说明: 第1个匹配项的值

类型: 任意类型-Any



**match2 **

名称: 匹配2

说明: 第2个匹配项的值

类型: 任意类型-Any



**match3 **

名称: 匹配3

说明: 第3个匹配项的值

类型: 任意类型-Any



**match4 **

名称: 匹配4

说明: 第4个匹配项的值

类型: 任意类型-Any



**match5 **

名称: 匹配5

说明: 第5个匹配项的值

类型: 任意类型-Any



**matchObj**

名称: Match对象

说明: 首个匹配的原始的C#语言Match对象，可以在表达式中使用

类型: 对象(Object)-Object



**matchesCollection**

名称: Matches集合

说明: 所有匹配的原始Match对象集合(MatchCollection)，可以在表达式中使用

类型: 对象(Object)-Object



**isSuccess**

名称: 是否成功

说明: 是否匹配成功

类型: 布尔值-Boolean



### 范例


**范例1**
```json

```

***

## 文本窗口

### 功能描述
在独立的窗口中显示文本。

### 官方文档
https://getquicker.net/KC/Help/Doc/showText

### 内部名称
sys:showText

### 传入参数


**type**

名称: 操作类型

说明: 是否等待窗口关闭后继续

类型: 选项-Enum

默认值: NO_WAIT



**text**

名称: 文本内容

说明: 要显示的文本内容

类型: 字符串-Text

必填: True



**title**

名称: 窗口标题

说明: 窗口标题文字

类型: 字符串-Text

默认值: 文本窗口

必填: True



**operations**

名称: 工具栏操作

说明: 用于显示在窗口工具栏。每行一个选项，格式为 “文本” 或 “显示文本|值”。

类型: 字符串-Text

必填: True



**autoCloseKey**

名称: 文本窗口标识

说明: 可选。自动更新或关闭之前打开的具有此标识的文本窗口。使用‘=’表示当前动作id。

类型: 字符串-Text

默认值: =



**winLocation**

名称: 窗口位置类型

说明: 在哪里显示选择窗口

类型: 选项-Enum

默认值: CenterScreen



**winSize**

名称: 窗口尺寸/位置

说明: 设置选择窗口的尺寸，格式为：宽度,高度。支持逻辑像素数值或屏幕宽高百分比，详情请参考模块文档。
“窗口位置” 类型为 “自定义位置” 时用于指定显示位置，格式为：left,top,right,bottom

类型: 字符串-Text



**fontsize**

名称: 字体大小

说明: 默认的字体大小

类型: 数字(小数)-Number

默认值: 14

必填: True



**fontfamily**

名称: 字体名称

说明: 可选。设置字体名称。如有多个字体，使用逗号分隔。

类型: 字符串-Text



**bgColor**

名称: 背景颜色

说明: 可选。格式为#RRGGBB

类型: 字符串-Text



**textColor**

名称: 文字颜色

说明: 可选。格式为#RRGGBB

类型: 字符串-Text



**highlight**

名称: 语法高亮

类型: 选项-Enum



**autoSaveToState**

名称: 自动保存到状态

说明: 指定状态Key。文本内容将自动保存到状态中。

类型: 字符串-Text



**topMost**

名称: 置顶显示

类型: 布尔值-Boolean

默认值: False



**enableEscClose**

名称: Esc 键关闭窗口

类型: 布尔值-Boolean

默认值: True



**closeWhenLostFocus**

名称: 失去焦点自动关闭

类型: 布尔值-Boolean

默认值: False



**showLineNum**

名称: 显示行号

类型: 布尔值-Boolean

默认值: True



**autoWrap**

名称: 自动换行显示

类型: 布尔值-Boolean

默认值: True



**showBuildInToolbar**

名称: 显示内置工具栏

类型: 布尔值-Boolean

默认值: True



**copyWholeLine**

名称: 未选择内容时，复制或剪切整行

类型: 布尔值-Boolean

默认值: False



**caretPosition**

名称: 光标位置

说明: 0表示最前面，-1表示最后面，其它数字表示某个具体字符位置。

类型: 数字(整数)-Integer

默认值: 0

必填: True



**advancedSettings**

名称: 高级设置

说明: 请参考模块文档。

类型: 字符串-Text



**updateIfExists**

名称: 如果窗口存在，则直接更新窗口内容（而不是关闭后打开新窗口）

类型: 布尔值-Boolean

默认值: False



**stopIfFail**

名称: 失败后停止

说明: 失败后是否停止动作

类型: 布尔值-Boolean

默认值: True



### 传出参数


**isSuccess**

名称: 是否成功

说明: 操作是否成功

类型: 布尔值-Boolean



**isWindowExists**

名称: 窗口是否存在

类型: 布尔值-Boolean



**selectedOperation**

名称: 选择的项

说明: 选择的后续操作项

类型: 字符串-Text



**resultText**

名称: 结果文本

说明: 文本框内的所有文本

类型: 字符串-Text



**selectedText**

名称: 选中的文本

说明: 文本框内选中的文本

类型: 字符串-Text



**windowHandle**

名称: 窗口句柄

类型: 数字(整数)-Integer



**windowPosition**

名称: 窗口位置

说明: 窗口的最终显示位置

类型: 字符串-Text



**allWindows**

名称: 所有窗口

说明: 词典类型，key为窗口的句柄，value为窗口的标识。获取全部窗口时，为了安全，仅限自己开发的动作使用。

类型: 词典-Dict



### 范例


**范例1**
```json

```

***

## 拆分文本为列表

### 功能描述
将文本拆分为列表

### 官方文档
https://getquicker.net/KC/Help/Doc/splitstring

### 内部名称
sys:splitString

### 传入参数


**data**

名称: 输入

说明: 要拆分为列表的文本

类型: 字符串-Text

必填: True



**separator**

名称: 分隔

说明: 拆分分隔符

类型: 字符串-Text

默认值: ,

必填: True



**escapeSeparator**

名称: 转义分隔符

说明: 转义分隔符\r\n\t字符

类型: 布尔值-Boolean

默认值: False



**multiSeparator**

名称: 使用多个分隔符拆分列表

说明: 每行指定一个。

类型: 布尔值-Boolean

默认值: False



**removeEmpty**

名称: 滤除空值

说明: 滤除没有内容的文本

类型: 布尔值-Boolean

默认值: True

必填: True



### 传出参数


**output**

名称: 结果

说明: 生成的文本内容

类型: 文本列表-List



### 范例


**范例1**
```json

```

***

## 替换文本

### 功能描述
替换文本中的指定内容

### 官方文档
https://getquicker.net/KC/Help/Doc/strReplace

### 内部名称
sys:strReplace

### 传入参数


**type**

名称: 操作类型

类型: 选项-Enum

默认值: single

必填: True



**input**

名称: 输入

说明: 要提取内容的文本

类型: 字符串-Text

必填: True



**batchReplaceData**

名称: 查找和替换内容

说明: 每行一对查找和替换内容，中间使用|||或|分隔。例如将a替换成A，写作:a|A 或 a|||A

类型: 字符串-Text

必填: True



**old**

名称: 查找内容

说明: 要替换的内容

类型: 字符串-Text

必填: True



**new**

名称: 替换为

说明: 替换成的内容

类型: 字符串-Text

必填: True



**escapeOld**

名称: 转义“查找内容”

说明: 替换“查找内容”中的转义字符（\r,\n,\t）

类型: 布尔值-Boolean

默认值: False



**replaceEscapes**

名称: 转义“替换为”

说明: 替换“替换为”中的转义字符（\r,\n,\t）

类型: 布尔值-Boolean

默认值: True



**useRegex**

名称: 使用正则替换

类型: 布尔值-Boolean

默认值: False



**ignoreCase**

名称: 忽略大小写

类型: 布尔值-Boolean

默认值: False



**singleLine**

名称: 正则：单行

说明: 此模式下“.”能匹配任意字符，包括换行符。(否则匹配除了\n外的任意字符)

类型: 布尔值-Boolean

默认值: True



**multiLine**

名称: 正则：多行

说明: 此模式下^和$可以分别匹配行首和行尾。(否则匹配输入内容的开始和结束)

类型: 布尔值-Boolean

默认值: False



### 传出参数


**output**

名称: 结果

说明: 替换后的文本

类型: 字符串-Text



### 范例


**范例1**
```json

```

***

## 字数统计

### 功能描述
统计文本行数、字符数等

### 官方文档
https://getquicker.net/KC/Help/Doc/textcounter

### 内部名称
sys:textCounter

### 传入参数


**content**

名称: 文本

说明: 要统计的内容

类型: 字符串-Text

必填: True



### 传出参数


**line**

名称: 行数

类型: 数字(整数)-Integer



**char**

名称: 字符数

类型: 数字(整数)-Integer



**visableChar**

名称: 可见字符数

类型: 数字(整数)-Integer



**cnChar**

名称: 汉字数

类型: 数字(整数)-Integer



### 范例


**范例1**
```json

```

***
