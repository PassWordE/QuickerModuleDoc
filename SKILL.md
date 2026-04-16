skill: quicker_action_compact_v3
schema:
  module: [name, doc_slug, desc, inputs, outputs]
  input: [type, req(1|0), default|null, desc|null]
  output: [type, desc|null]
globals:
  doc_base: https://getquicker.net/KC/Help/Doc/
  root: [Variables, Steps, SubPrograms]
  step_req: [StepRunnerKey, InputParams, OutputParams]
  step_opt: [IfSteps, ElseSteps, Note, Disabled, Collapsed, DelayMs]
  input_param: {VarKey: var|null, Value: literal|$$|$=|null}
  output_param: var|null
  string_modes: {raw: literal, interp: $$...{var}..., code: $=...return ...}
  types: {T0: Text, T1: Number, T2: Boolean, T3: Image, T4: List, T6: DateTime, T7: KeyCode, T9: Enum, T10: Dict, T11: Form, T12: Integer, T13: Table, T14: FormForDict, T98: Object, T99: Any}
  win_location: {Auto: 系统默认, WithMouse1: 跟随鼠标(指针周围), WithMouse2: 跟随鼠标(指针右下/偏移), CenterScreen: 屏幕中间, TopLeft: 屏幕左上, TopCenter: 屏幕中上, TopRight: 屏幕右上, BottomLeft: 屏幕左下, BottomCenter: 屏幕中下, BottomRight: 屏幕右下, LeftCenter: 屏幕左中, RightCenter: 屏幕右中, FullScreen: 全屏, Manual: 自定义位置}
  ai_rules: [精确使用StepRunnerKey, 仅声明实际使用变量, JSON字段名大小写保持原样, 变量名按任务语义重命名, 模块选择优先key>desc>io, 边缘行为以doc_base+doc_slug为准]
modules:
  "sys:activateProcessMainWindow":
    - "激活进程主窗口"
    - "activateprocessmainwindow"
    - "找到指定进程的主窗口并使其显示在前台。"
    - {"process":["T0",1,null,"请输入要验证的进程名称或pid。进程名通常是exe的文件名去掉后缀，比如记事本程序的进程名称为notepad"],"className":["T0",0,null,"未能获取主窗口时（如窗口隐藏），可以尝试根据类名查找窗口，支持正则"],"windowTitle":["T0",0,null,"未能获取主窗口时，根据窗口标题查找，支持正则"],"hotkey":["T0",0,null,"软件最小化到托盘时，使用指定的全局热键激活窗口"],"path":["T0",1,null,"如果进程不存在，可以根据此路径启动程序"],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","是否成功激活了进程主窗口"],"pid":["T12","进程ID"],"mainWinHandle":["T12","进程的主窗口句柄"],"mainWinTitle":["T0",null]}
  "sys:break":
    - "跳出循环（break）"
    - "break"
    - "跳出循环（“每个” 或 “重复” 模块）"
    - {}
    - {}
  "sys:checkPathExists":
    - "检查路径/获取文件信息"
    - "checkPathExists"
    - "检查指定的文件或文件夹是否存在。"
    - {"path":["T0",1,null,"文件或文件夹的完整路径"]}
    - {"isExists":["T2",null],"isFile":["T2",null],"fileLength":["T12",null],"isFolder":["T2",null],"isReadonly":["T2",null],"isHidden":["T2",null],"isSystem":["T2",null],"fileCount":["T12","仅对文件夹路径有效，输出时需要耗费一定时间扫描文件夹"],"totalLength":["T12","仅对文件夹路径有效，输出时需要耗费一定时间扫描文件夹"],"createTime":["T6",null],"editTime":["T6",null],"metaData":["T10","获取文件的扩展信息，值为词典类型"],"lnkTarget":["T0","快捷方式文件的目标文件"],"lnkArguments":["T0","快捷方式中的命令行参数"],"md5hash":["T0","获取文件的MD5哈希值。仅对文件有效，大文件需要一些时间扫描"],"sha1hash":["T0","获取文件的SHA1哈希值。仅对文件有效，大文件需要一些时间扫描"],"sha256hash":["T0","获取文件的SHA256哈希值。仅对文件有效，大文件需要一些时间扫描"],"crc32hash":["T0","获取文件的CRC32哈希值。仅对文件有效，大文件需要一些时间扫描"]}
  "sys:checkProcessExists":
    - "检查程序已启动/获取进程信息"
    - "checkprocessexists"
    - "检查指定的应用程序是否已经启动。"
    - {"process":["T0",1,null,"请输入要验证的进程名称或id。通常是exe的文件名去掉后缀，比如记事本程序的进程名称为notepad"],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","可能会因为无法访问高权限进程等原因而失败。进程未启动不会导致操作失败"],"isExists":["T2","指定的进程是否运行。如果已运行，返回True，否则返回False"],"pid":["T12","找到的第一个匹配进程的ID"],"pidList":["T4","具有相同进程名的所有进程的ID列表"],"path":["T0","进程的应用程序路径"],"mainWinHandle":["T12",null],"mainwinTitle":["T0",null],"startTime":["T6",null]}
  "sys:clouddata":
    - "云状态存取"
    - "clouddata"
    - "根据键值读取或写入网络数据。"
    - {"type":["T9(readGlobalState: 从网络读取数据; saveGlobalState: 写入数据到网络)",1,"readGlobalState",null],"key":["T0",0,null,"存储或读取的数据条目名称(键)"],"value":["T0",0,null,"要保存的数据值。使用*NULL*删除此状态的存储"],"expireSeconds":["T1",0,"2.5","请求超时时间（秒数）"],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","操作是否成功"],"value":["T99","读取到的状态内容"],"err":["T0","出错时输出的错误信息"],"errCode":["T0","从云服务商返回的错误代码。NoSuchKey=不存在此状态"]}
  "sys:cloud_oss":
    - "第三方云存储/图床"
    - "cloud_oss"
    - "使用第三方云服务上传文件。"
    - {"operation":["T9(Upload: 上传)",1,"Upload",null],"vendor":["T9(Aliyun: 阿里云OSS; Tencent: 腾讯云COS; Qiniu: 七牛云)",1,"Aliyun",null],"vendorSettings":["T0",0,null,null],"key":["T0",0,null,"留空时自动生成对象名。如果以/结尾，则在此基础上自动生成对象名"],"content":["T99",0,null,"要上传的文件路径、其它文本内容或图片变量"],"customDomain":["T0",0,null,"如\"https://files.example.com\""],"extraHeaders":["T0",0,null,"设置厂商相关的特定http头"],"expireSeconds":["T12",1,"180","请求超时时间（秒数）"]}
    - {"isSuccess":["T2","操作是否成功"],"vendorUrl":["T0",null],"customUrl":["T0","设置了自定义域名时会生成此网址"]}
  "sys:continue":
    - "跳过后续步骤(continue)"
    - "continue"
    - "跳过后续步骤（循环内部），开始下一次循环。在循环内部使用。"
    - {}
    - {}
  "sys:each":
    - "每个"
    - "each"
    - "对列表的每项执行处理"
    - {"input":["T4",1,null,"要处理的列表"],"useMultiThread":["T9(0: 单线程(顺序执行); 1: 多线程(同时执行))",0,"0","⚠通常不要选择! 请阅读文档详细了解后再使用"],"threadDelay":["T12",0,"5","多线程运行时，每个线程之间的启动时间间隔毫秒数"],"concurrentThreadNum":["T12",0,"4","最多同时启动的线程数，请根据电脑配置和任务内容设置"],"timeoutMs":["T12",0,"-1","所有线程开启后，等待的超时时间，单位：毫秒。-1:不设置超时时间"],"useLocalContext":["T2",0,"False","此时只能读取变量，不能更新变量（词典、列表等引用传递的除外）"],"waitAny":["T2",0,"False","任意一个线程结束即可"],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"item":["T99","列表中的每项，每次循环赋予当前项的值。在子步骤中应该对本输出进行处理"],"count":["T12","本次循环，处理到了第几项"],"isSuccess":["T2","操作是否成功"]}
  "sys:getActiveProcessInfo":
    - "获取前台进程信息"
    - "getactiveprocessinfo"
    - "获取当前活动窗口进程的信息。"
    - {"stopIfFail":["T2",0,"True","获取进程信息失败后是否停止动作"]}
    - {"path":["T0","获得的进程路径"],"procName":["T0","进程名称"],"pid":["T12","进程ID"],"isSuccess":["T2","是否成功获得进程信息"]}
  "sys:getChromeUrl":
    - "获取浏览器网址"
    - "getchromeurl"
    - "获取当前浏览器网址。"
    - {"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"output":["T0","当前标签网址URL"],"isSuccess":["T2","操作是否成功"]}
  "sys:getClipboardFiles":
    - "获取剪贴板文件列表"
    - "getclipboardfiles"
    - "获取剪贴板中复制的文件(或文件夹)的路径列表"
    - {"stopIfFail":["T2",0,"True","获取选中的文本失败后，是否停止后续动作的执行"]}
    - {"isSuccess":["T2","是否成功获得文件列表"],"output":["T4","从剪贴板获取的文件路径列表"],"elapsedMs":["T12","剪贴板最后更新是在多少毫秒以前"]}
  "sys:getClipboardImage":
    - "获取剪贴板图片"
    - "getclipboardimage"
    - "读取剪贴板中的图片内容输出到图片变量中。"
    - {"stopIfFail":["T2",0,"True","获取失败后，是否停止后续动作的执行"]}
    - {"isSuccess":["T2","是否成功获得剪贴板图片"],"output":["T3","将获得的图片写入到变量"],"elapsedMs":["T12","剪贴板最后更新是在多少毫秒以前"]}
  "sys:getClipboardText":
    - "获取剪贴板文本"
    - "getClipboardText"
    - "读取剪贴板中的文本内容"
    - {"format":["T9(UnicodeText: 纯文本; Rtf; Html; CommaSeparatedValue: 带逗号分隔的值(csv); Custom: 自定义格式名)",0,"UnicodeText","需要读取的剪贴板文本内容格式。通常请使用Unicode纯文本格式"],"customFormat":["T0",0,null,"自定义的剪贴板格式名，请和实际剪贴板格式名一致。只支持实际为文本类型的内容"],"encoding":["T9",1,"utf-8","读取自定义格式时候使用的编码类型"],"waitMs":["T12",0,"400","每10ms重试一次，直到获取到文本。为0时不重试"],"stopIfFail":["T2",0,"True","获取选中的文本失败后，是否停止后续动作的执行"]}
    - {"isSuccess":["T2","是否成功获得文本"],"output":["T0","将获得的文本内容写入到变量"],"cleanHtml":["T0","HTML的主要内容。<!--StartFragment-->和<!--EndFragment-->之间的部分"],"htmlDoc":["T0","仅去除剪贴板头部信息的完整HTML文档内容。包含<html>等标签，可直接保存为.html文件"],"url":["T0","从网页中复制内容时，可能会携带网址信息"],"elapsedMs":["T12","剪贴板最后更新是在多少毫秒以前"]}
  "sys:getCurrentTime":
    - "获取日期时间"
    - "gettime"
    - "获取当前或从文本、unix时间戳转换日期时间"
    - {"source":["T9(currTime: 当前时间; fromString: 从文本转换; fromUnixTimeStamp: 从Unix时间戳转换(秒); Source_UnixTimeStampMs: 从Unix时间戳转换(毫秒); fromVar: 时间变量)",0,"currTime","时间数据来源"],"useUtc":["T2",0,"False","是表示使用UTC时间，否表示使用本地时间（电脑的当前时间）"],"timeStr":["T0",0,null,"待转换为时间值的文本"],"inputCulture":["T0(CURRENT: 当前系统语言; zh-CN; en-US; ja-JP; ko-KR; fr-FR; de-DE; es-ES; it-IT; ru-RU; pt-BR)",0,"CURRENT","，待解析文本的语言文化。如zh-CN表示中文简体，en-US表示英文美国等。详情请参考文档"],"inputFormat":["T0",0,null,"，待解析文本的数据格式，如yyyy表示4位数年份，MM表示2位数月份等。详情请参考文档"],"timeVar":["T6",0,null,"时间变量"],"timeStampStr":["T0",0,null,"从1970年1月1日开始所经过的秒数或毫秒数。根据需要开启或关闭使用UTC时间选项"],"addDays":["T1",0,"0","添加指定的天数（可以为小数/负数）"],"addHours":["T1",0,"0","添加指定的小时数（可以为小数/负数）"],"addMinutes":["T1",0,"0","添加指定的分钟数（可以为小数/负数）"],"addSeconds":["T1",0,"0","添加指定的秒数（可以为小数/负数）"],"addMonths":["T1",0,"0","添加指定的月数（整数）结果不跨月，如1月31日增加1个月等于2月28日"],"format":["T0",0,"yyyy-MM-dd HH:mm:ss","文本值的输出格式，请参考c#语言DateTime.ToString()的参数文档"],"outputCulture":["T0",0,"CURRENT","指定将时间值格式化为文本时所使用的语言文化。如zh-CN表示中文简体，en-US表示美国英文等"],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","操作是否成功"],"output":["T6","日期时间类型的结果时间"],"strValue":["T0","按‘文本值格式’参数转换后的文本格式值"],"timeStamp":["T12","获取Unix时间戳（1970年1月1日0时到指定时间的秒数）"],"timeStampMs":["T12","获取Unix时间戳（1970年1月1日0时到指定时间的毫秒数）"],"year":["T12","年份值"],"month":["T12","月份值"],"day":["T12","日期值"],"hour":["T12","当前小时数，24小时制"],"minute":["T12","当前分钟数"],"second":["T12","当前秒数"],"dayOfWeek":["T12","本周的第几天，周日为0，周一为1，以此类推"],"dayOfYear":["T12","本年的第几天"]}
  "sys:getExplorerPath":
    - "获取资源管理器路径/跳转路径"
    - "getexplorerpath"
    - "获取资源管理器的当前文件夹路径。"
    - {"operation":["T9(getPath: 获取路径; setPath: 设置路径)",0,"getPath",null],"path":["T0",0,null,null],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"output":["T0","当前资源管理器窗口的路径"],"allPathList":["T4","所有资源管理器窗口中打开的路径列表"],"lastPath":["T0","最近访问的资源管理器窗口的路径"],"isSuccess":["T2","操作是否成功"]}
  "sys:getFolderPath":
    - "获取系统路径"
    - "getfolderpath"
    - "返回指定的特殊目录路径。"
    - {"folder":["T9",1,null,"Windows的特殊目录类型，详情请搜索“Environment.SpecialFolder”"]}
    - {"path":["T0","返回的完整路径"]}
  "sys:getSelectedText":
    - "获取选中的文本"
    - "get_selected_text"
    - "获取选中的文字"
    - {"format":["T9(UnicodeText: 纯文本(默认); Rtf; Html; CommaSeparatedValue: 逗号分隔的值(csv))",0,"UnicodeText","需要读取的剪贴板文本内容格式。通常请使用Unicode纯文本格式"],"waitMs":["T12",0,"250","模拟复制键后，等待剪贴板变化的最长时间毫秒数"],"repeat":["T12",0,"0","【已过时，仅为兼容性保留】失败后重试的次数"],"trim":["T2",0,"False","去除内容前后的空白（包括空行）"],"tryNoClipboard":["T2",0,"False","通过UIAutomation方式获取（某些情况可能出现无法完整获取文字、失去换行信息等问题）"],"useActionParam":["T2",0,"False","没有传递参数时仍尝试获取选中的文本"],"stopIfFail":["T2",0,"True","获取选中的文本失败后，是否停止后续动作的执行"]}
    - {"isSuccess":["T2","是否成功获取了文本"],"output":["T0","将获得的文本写入到变量"],"cleanHtml":["T0","剪贴板HTML的主要内容<!--StartFragment-->和<!--EndFragment-->之间的部分"],"outputEncoded":["T0","对选中的内容进行URL编码处理后的结果，通常用于拼接网址"],"url":["T0","从网页中复制内容时，可能会携带网址信息"]}
  "sys:getSysInfo":
    - "获取系统或动作信息"
    - "getsysinfo"
    - "返回Windows系统信息。"
    - {}
    - {"MachineName":["T0",null],"userName":["T0","当前登录到电脑的用户名"],"userDomainName":["T0","当前用户的网络域名（DomainName）"],"OsVersion":["T0",null],"isWin10":["T2",null],"isWin11":["T2",null],"isAutoRun":["T2","是否开机自动启动Quicker"],"startupSeconds":["T1","可参考任务管理器中显示的正常运行时间"],"isLocked":["T2",null],"sysEnv":["T10",null],"primaryScreenRes":["T0",null],"isFullscreen":["T2",null],"isNetworkConnected":["T2",null],"lanIp":["T0",null],"quickerVersion":["T12",null],"isPro":["T2","当前用户是否使用专业版软件"],"unionId":["T0","一个标识用户身份的字符串"],"hasBaiduAccount":["T2","已经在设置中添加了自有百度OCR帐号"],"runnedSeconds":["T1","Quicker启动后运行的秒数"],"actionId":["T0","当前运行的动作ID"],"actionName":["T0","当前运行的动作名称"],"sharedActionId":["T0","当前动作的动作库ID"],"sharedActionRevision":["T12","当前安装的动作版本"],"actionCount":["T12","当前动作运行中的实例个数(包含此实例)"],"isDebugging":["T2","是否正在调试运行动作"],"trigger":["T0","动作的触发方式"],"textParam":["T0","传入动作的文本上下文参数"],"imageParam":["T3","传入动作的图片上下文参数"],"isWinInDarkMode":["T2","true表示深色模式，false表示浅色模式"],"quickerThemeMode":["T0","可能为：light/dark/auto_light/auto_dark。auto_light/auto_dark表示为跟随windows，当前为浅色或深色模式"]}
  "sys:getWindowTitle":
    - "获取窗口信息/查找窗口"
    - "getwindowtitle"
    - "获取指定窗口的标题等信息。"
    - {"which":["T9(foreground: 前台窗口; selectWindow: 选择一个窗口; pointing: 弹出面板前鼠标位置的窗口(可能为子窗口); pointing_root: 弹出面板前鼠标位置窗口的根窗口; pointing_now: 当前鼠标位置的窗口(可能为子窗口); pointing_now_root: 当前鼠标位置窗口的根窗口; fromHwnd: 句柄指定的窗口; findWindow: 查找顶层窗口 (单个窗口); top_windows: 所有顶层窗口; findChildWindow: 查找子窗口/控件 (单个窗口); child_windows: 查找子窗口 (多个窗口))",1,"foreground","判断哪个窗口的信息"],"hWnd":["T12",0,null,"未指定时使用前台窗口句柄"],"className":["T0",0,null,"要查找窗口的类名（ClassName），为空时不检查此项"],"windowName":["T0",0,null,"要查找窗口的标题，为空时不检查此项"],"procIdOrName":["T0",0,null,"要查找窗口所属的进程名或pid，为空时不检查此项"],"onlyVisible":["T9",0,"default",null],"requireTitle":["T2",0,"True",null],"useRegex":["T2",0,"False",null],"winRectIncludeInvisibleBorder":["T2",0,"False",null],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","操作是否成功"],"output":["T0","窗口的标题文字"],"className":["T0","窗口的 Class Name"],"handle":["T12","窗口的句柄"],"pid":["T12","窗口所属进程的ID"],"procName":["T0","进程名称"],"path":["T0","获得的进程路径"],"parent":["T12",null],"root":["T12",null],"rootOwner":["T12",null],"rect":["T0","文本值，格式为:Left,Top,Right,Bottom,Width,Height"],"rectNoSize":["T0","文本值，格式为:Left,Top,Right,Bottom。如:0,0,100,100"],"rectDict":["T10","词典值，属性为:Left,Top,Right,Bottom,Width,Height"],"isTopmost":["T2",null],"isVisible":["T2",null],"showState":["T12","1:普通，2:最小化，3:最大化"],"alpha":["T12","窗口的透明度，范围为0-255。0表示全透明"],"allChildWindows":["T10","词典值，Key为窗口句柄，Value为窗口标题"],"topLevelWindows":["T10","词典值，Key为窗口句柄，Value为窗口标题"]}
  "sys:group":
    - "步骤组"
    - "group"
    - "一组有关的模块（方便整体禁用、删除等）"
    - {"skipErr":["T2",0,"False","忽略内部步骤的错误，继续允许后续代码"],"skipWhenDebugging":["T2",0,"False","用以减少不必要的调试输出"],"useMultiThread":["T2",0,"False","⚠通常不要选择! 请阅读文档详细了解后再使用"],"waitAny":["T2",0,"False","任意一个线程结束即可"]}
    - {"isSuccess":["T2","内部步骤是否运行成功"],"errorMessage":["T0",null]}
  "sys:http":
    - "HTTP请求"
    - "http"
    - "发送HTTP请求，并获取返回结果"
    - {"url":["T0",1,"https://","要打开的网页地址"],"method":["T9(GET, POST, PUT, DELETE, PATCH, HEAD, OPTIONS)",1,"GET","Http请求的类型"],"header":["T0",0,null,"发送的HttpHeader。每行一个header，格式为Name:Value"],"cookie":["T0",0,null,"请求的cookie内容"],"bodyType":["T9(JSON, FORM: 文本表单, FILE: MultiPart表单, BinaryFile: 单个文件或图片变量(二进制), Text: 纯文本)",1,"JSON","Http 请求体的内容"],"body":["T0",0,null,"Http 请求 BODY。格式要求详见模块帮助"],"contentType":["T0",0,null,"上传内容的ContentType，适用于“单个文件或图片变量（二进制）”或“纯文本” 请求体类型"],"resultType":["T9(Text: 文本, Image: 图片, File: 文件)",1,"Text","Http请求的结果类型"],"ua":["T0",0,"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/112.0.0.0 Safari/537.36",null],"expireSeconds":["T1",0,"100","请求超时时间（秒数）"],"noAutoRedirect":["T2",0,"False","是否禁止自动跳转"],"showProgress":["T2",0,"False","是否显示上传下载进度条"],"skipCertVerify":["T2",0,"False",null],"forceProxy":["T2",0,"False","即使系统设置中未启用代理，本步骤仍然使用代理访问"],"stopIfFail":["T2",0,"True","失败后是否停止动作"],"useSSE":["T2",0,"False","调用AI接口时使用，通过子程序处理接收到的流式响应内容"],"sseSpName":["T0",0,null,"用于处理接收到的流式响应消息，每次收到调用一次，通过data输入变量接收内容"]}
    - {"isSuccess":["T2","是否操作成功"],"statusCode":["T12","返回的http请求状态码"],"respHeaders":["T10","返回的HTTP响应Headers"],"respCookies":["T10","返回的Cookies"],"content":["T0","返回的文本内容"],"imgResult":["T3","返回的图片内容"]}
  "sys:if":
    - "如果/否则"
    - "if"
    - "依据条件执行操作"
    - {"condition":["T2",0,null,"是否符合指定的条件"]}
    - {}
  "sys:keyInput":
    - "模拟按键A（录入）"
    - "keyinput"
    - "模拟键盘输入"
    - {"keys":["T7",1,null,"模拟的按键内容"],"repeat":["T12",0,"1",null],"interval":["T12",0,"1","每次重复之间的间隔毫秒数"],"holdMs":["T12",0,"-1","普通键（非Ctrl/Alt/Shift/Win）在抬起前保持的时间。-1表示使用默认设置。 某些直接模拟按键无法生效的软件中可以尝试增加此值"]}
    - {}
  "sys:mouse":
    - "鼠标输入"
    - "mouse"
    - "模拟鼠标输入"
    - {"type":["T9(restore: 还原鼠标位置; move: 移动距离; moveTo: 移动到(x,y分别指定); moveToXy: 移动到(x,y一同指定); click: 单击; dbclick: 双击; down: 按下; up: 抬起; scroll: 滚动; ctrlDown: 按下Ctrl; ctrlUp: 松开Ctrl; shiftDown: 按下Shift; shiftUp: 松开Shift; toWinTL: 移动到窗口位置：相对于窗口左上角; toWinTR: 移动到窗口位置：相对于窗口右上角; toWinBL: 移动到窗口位置：相对于窗口左下角; toWinBR: 移动到窗口位置：相对于窗口右下角; toWinCenter: 移动到窗口位置：窗口中心; moveToWinXy: 移动到窗口位置：xy一同指定; locateByBitmap: 移动到位图位置(图片文件); locateByBitmapVar: 移动到位图位置(图片变量); getMouseOriginPosition: 获取鼠标位置(弹出面板前位置); getMouseCurrentPosition: 获取鼠标位置及指针类型(当前位置); showIndicator: 显示鼠标位置提示)",1,"restore","操作类型"],"hWnd":["T12",0,null,"目标窗口的句柄。留空或 0 表示操作前台窗口"],"btn":["T9(left: 左键; right: 右键; middle: 中键; x1: X1; x2: X2)",1,"left","操作哪个按钮"],"bmp":["T0",1,null,"需要在屏幕中查找的位图路径。位图必须和屏幕图像完全匹配，不能压缩。此时X、Y的值为相对于搜索位图的左上角的偏移"],"bmpVar":["T3",1,null,"需要在屏幕中查找的位图。位图必须和屏幕图像完全匹配，不能压缩。此时X、Y的值为相对于搜索位图的左上角的偏移"],"bmpTargetType":["T9(MainScreen: 主屏幕; CurrentWindow: 当前窗口; Rect: 坐标范围)",0,"MainScreen","位图查找范围"],"searchRect":["T0",0,null,"当“查找范围”为“坐标范围”时有效，格式为：left,top,right,bottom"],"bmpPosition":["T9(Center: 位图中间; TopLeft: 左上角; TopRight: 右上角; BottomLeft: 左下角; BottomRight: 右下角)",0,"Center","查找到图片后，鼠标指针移动到的位置"],"bmpColorError":["T12",0,"10","匹配像素时允许每个颜色通道的偏差值0-100，0表示精确匹配，速度最快"],"maxFindCount":["T12",0,"1","找图的最大匹配数量。将对每个查找到的目标执行附加动作"],"retryCount":["T12",0,"1","未找到位图时的重试次数。每次重试间隔300ms"],"x":["T12",1,"0","水平方向的坐标/坐标偏移/移动距离(像素) 或 滚动数量（clicks。正值向右，负值向左）"],"y":["T12",1,"0","垂直方向的坐标/坐标偏移/移动距离 或 滚动数量（clicks。正值向前，负值向后）"],"xy":["T0",1,null,"格式为：x,y，如：100,200。也可以使用百分比表示，如：50%,50% 表示屏幕中心"],"xyForWin":["T0",1,null,"格式为：x,y，如：100,200（相对于窗口左上角向右100，向下200）。也可以使用百分比表示，如：50%,50% 表示窗口中心"],"slowMove":["T2",0,"False","逐渐移动而不是直接移动到目标位置"],"extAction":["T9(none: 无; left: 左键单击; leftDbClick: 左键双击; right: 右键单击; middle: 中键单击)",1,"none","移动位置后，需要执行的动作"],"restoreMousePos":["T2",0,"False",null],"stopIfFail":["T2",0,"True","获取位置失败后，是否停止后续动作的执行"]}
    - {"isSuccess":["T2",null],"mouseLocation":["T0","格式为X,Y的文本"],"mouseX":["T12","鼠标位置X坐标"],"mouseY":["T12","鼠标位置Y坐标"],"cursorType":["T0","当前的鼠标指针形状类型"]}
  "sys:notify":
    - "提示消息"
    - "notify"
    - "显示可以自动消失的消息提示。"
    - {"type":["T9(Success: 成功; Info: 信息; Warning: 告警; Error: 错误; WindowsToast: Windows 通知 (win10+))",1,"Info","消息的类型"],"msg":["T0",1,null,"显示的消息内容"],"maxLines":["T12",1,"0","显示内容的最大行数，0表示不限"],"style":["T9(Default: 默认(显示在屏幕底部); Style2: 风格2(显示在屏幕右侧))",1,"Default",null],"clickAction":["T0",0,null,"点击时运行命令（如网址等可以在Win+R中执行的文本，仅支持默认风格提示）。默认为复制提示文字"]}
    - {}
  "sys:numCompare":
    - "比较数字"
    - "numcompare"
    - "比较数字大小。"
    - {"param1":["T1",1,"0","左侧的数字"],"type":["T9(>; >=; =; <; <=)",1,">","比较方式"],"param2":["T1",1,"0","右侧的数字"]}
    - {"value":["T2","比较结果是否为真"]}
  "sys:openUrl":
    - "打开网址"
    - "openurl"
    - "打开指定的网址"
    - {"url":["T0",1,"https://","要打开的网页地址"],"browser":["T9",1,"default","使用什么浏览器打开网址"],"exePath":["T0",1,null,"浏览器exe程序路径"],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","操作是否成功"]}
  "sys:outputText":
    - "发送文本到窗口"
    - "outputtext"
    - "将文本输出到活动窗口中"
    - {"content":["T0",1,null,"要输出的内容"],"method":["T9(input: 模拟输入; paste: 复制到剪贴板后粘贴(Ctrl+V))",1,"paste","发送内容使用的方法"],"delayBeforePaste":["T12",0,"50","毫秒数。写入剪贴板以后，等待指定的时间后再发送粘贴按键(Ctrl+V)"],"delayAfterPaste":["T12",0,"10","毫秒数。发送粘贴按键(Ctrl+V)之后等待的毫秒数"],"delayBetweenChar":["T12",0,"0","模拟输入下一个字符之前等待的毫秒数"],"appendReturn":["T2",0,"False","发送内容后，在末尾输入回车"],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","步骤是否成功完成"]}
  "sys:playSound":
    - "播放声音"
    - "playsound"
    - "播放声音提示或声音文件。"
    - {"type":["T9(LOCAL: 内置声音提示; EXTERN: 电脑文件或网络文件; TTS: 朗读文本(系统TTS))",0,"LOCAL",null],"localSound":["T9(info: 信息; snip: 截图; succeed: 成功; warning: 警告; wrong: 错误)",0,"info",null],"uri":["T0",0,null,"音乐文件的本地路径或网址"],"text":["T0",0,null,"需要朗读的文本"],"wait":["T2",0,null,null],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","操作是否成功"]}
  "sys:quickeroperations":
    - "Quicker操作"
    - "quickeroperations"
    - "调用Quicker的某个功能"
    - {"type":["T9(showPanel: 显示面板; showSearch: 显示搜索框; closeSearch: 关闭搜索框; showCircleMenu: 显示轮盘菜单 (点击); togglePause: 禁用/启用; runLastAction: 运行最后使用的动作; startAppVoiceInput: 启动App语音输入; stopAllActions: 停止运行中的动作; reinstallMouseHook: 重新加载键鼠挂钩; ResetKeyboard: 重置键盘状态; showDashboardWindow: 显示仪表盘窗口; toggleTextFloatWindow: 开启/关闭文本悬浮窗功能; showConfigWindow: 显示配置窗口; showExeSettingWindow: 显示场景与动作管理窗口; closeAllFloatWindow: 关闭所有悬浮按钮; loadProfile: 加载动作页; loadExeProfiles: 加载指定应用程序的所有动作页(锁定切换); loadExeProfilesNoLock: 加载指定应用程序的所有动作页(不锁定切换); ToggleLockPanel: 锁定/解锁 动作页自动切换; editAction: 编辑动作; RestartQuicker: 重启Quicker; SetPushActiveClient: 推送服务：设置为活动客户端; StartSearchWithAction: 使用当前动作进行实时搜索; SearchWithCertainAction: 使用指定动作进行实时搜索; operation_show_context_menu: 显示剪贴板上下文菜单; LoadSkin: 加载外观/切换主题(专业版功能); ExitQuicker: 退出Quicker; FloatAction: 悬浮动作(专业版功能); ToggleFloatButtons: 切换所有悬浮按钮显示; ShowHideImageWindows: 显示或隐藏所有图片窗口; RemoveAction: 删除当前动作; GetActionInfo: 根据ID获取动作信息)",1,"showPanel","操作类型"],"profileId":["T0",1,null,"请在场景与动作管理中，查看动作页信息获取ID"],"actionId":["T0",1,null,"在动作上点右键->信息可以查看动作信息。使用名称时不能有重名动作。获取动作信息时仅可填写动作Id。编辑动作时，使用%%id或%%name格式，可用于编辑公共子程序"],"position":["T0",1,"200,200","坐标，格式为：left,top"],"exe":["T0",1,null,"场景关联的exe文件名。请参考场景与动作管理窗口左侧应用列表"],"activatePointWindow":["T2",0,"0",null],"followMousePosition":["T2",0,"True",null],"searchText":["T0",0,null,"预先放入搜索框的内容"],"skinId":["T0",1,null,"请在外观网页中复制外观ID"],"theme":["T9(\"\": 不改变; auto: 跟随Windows; light: 浅色; dark: 暗色; toggle: 切换浅色和暗色)",0,null,"切换为浅色或暗色模式"],"viewMode":["T9(HideAll: 隐藏全部; ByProcess: 自动(按关联进程切换); ShowAll: 显示全部; ToggleHideAndAuto: 切换隐藏和自动)",0,"ByProcess",null],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","步骤是否成功完成"],"actionList":["T4",null],"actionTitle":["T0",null],"actionIcon":["T0",null]}
  "sys:repeat":
    - "重复"
    - "repeat"
    - "循环指定的次数，或符合某个条件时中止"
    - {"count":["T12",0,"1","重复次数，除非符合条件提前中止。-1表示无限循环"],"stopCondition":["T2",0,null,"条件满足时停止循环（每次循环开始时检查）"],"startIndex":["T12",0,"0","计数序号的开始值，通常应该为0"],"repeatDelayMs":["T12",0,"1","每次循环之间的间隔毫秒数。如果为0，请确保循环内部有其他等待步骤，避免连续循环占用较多资源"],"progressBarTitle":["T0",0,null,"如果设置了此参数，则在循环过程中会显示一个进度条，标题为此参数的值"]}
    - {"count":["T12","计数序号，表示第几次循环"]}
  "sys:reportProgress":
    - "显示进度条"
    - "reportProgress"
    - "显示/更新进度条"
    - {"type":["T9(REQUEST_ID: 创建进度条; UPDATE_PROGRESS: 更新进度; REMOVE: 去除进度条)",1,"REQUEST_ID","操作类型"],"progressId":["T12",0,"0","进度条的序号，用于后续更新或删除进度条"],"title":["T0",0,null,"进度条的标题(显示在进度条上方)"],"percentage":["T1",0,"0","0到100之间的数字"],"text":["T0",0,null,"显示在进度条下方"]}
    - {"progressId":["T12","进度条的序号，用于后续更新或删除进度条"]}
  "sys:restoreActiveWindow":
    - "恢复活动窗口"
    - "restoreactivewindow"
    - "如果活动窗口改变了（比如使用了参数输入步骤）,使用此动作恢复窗口焦点。"
    - {}
    - {}
  "sys:runAction":
    - "运行或停止动作"
    - "runaction"
    - "执行指定的其他动作"
    - {"type":["T9(StartAction: 运行动作; StopAction: 停止动作; ShowActionContextMenu: 显示动作右键菜单; StartCurrentAction: 运行当前动作(注意避免产生循环或递归); StopOtherInstance: 停止当前动作的其它实例; GetRunningActionCount: 获取动作运行个数(自己编写动作时可用))",1,"StartAction","操作类型"],"actionId":["T0",1,null,"要运行的其他动作的ID或名称(使用名称时需要完全匹配且不能有重名动作)"],"onlyCustomMenu":["T2",0,"False","不显示编辑、复制等菜单"],"inputParam":["T0",1,null,"传递给目标动作的参数。存储在该动作的quicker_in_param变量中"],"wait":["T2",0,"True","是否等待此动作运行结束再执行后续动作（如需获取目标动作的输出，需选中此项）"],"debug":["T2",0,"False","是否以调试模式运行动作"],"hideMessage":["T2",0,"False","仅对非动作库安装的动作有效"],"stopIfFail":["T2",0,"True","如果未找到目标动作，是否停止当前动作"]}
    - {"isSuccess":["T2","操作是否成功"],"actionTitle":["T0","运行的动作名称"],"count":["T1","动作正在运行的个数"],"output":["T0","被调用动作的输出"]}
  "sys:run":
    - "运行或打开"
    - "run"
    - "运行软件或命令，打开文件、文件夹或网址。效果类似于在Windows“运行”对话框中执行命令。"
    - {"path":["T0",1,null,"要运行的命令或打开的文件路径、网址、URI等"],"arg":["T0",0,null,"程序参数"],"setWorkingDir":["T0",0,"1","可输入 0或留空(不设置,由windows默认)、1(软件所在目录)、具体的工作目录路径"],"windowStyle":["T9(0: 普通(Normal); 1: 隐藏(Hidden); 2: 最小化(Minimized); 3: 最大化(Maximized))",0,"0","设置期望的窗口风格，是否有效依赖于具体的软件"],"runas":["T2",0,"False","以管理员身份运行软件或命令"],"waitInputIdle":["T2",0,"False","等待进程完成后了初始化，可以接受用户输入"],"waitExit":["T2",0,"False","等待进程结束后再执行后续操作步骤"],"activateWindowIfRunning":["T2",0,"False","如果程序已经在运行，则尝试激活其窗口"],"activateWindowHotkey":["T0",0,null,"对于支持快捷键激活窗口的软件，设置该快捷键。支持“模拟按键B”语法"],"alternativePath":["T0",0,null,"文件在多个电脑上路径不同时，使用备用路径填写其他电脑上的文件路径"],"username":["T0",0,null,"使用指定的用户运行"],"password":["T0",0,null,"用户名对应的密码"],"outputEncoding":["T9(utf8: UTF8; oem: OEM)",1,"oem","控制台输出编码。如果输出遇到乱码，尝试修改此选项"],"envVariables":["T0",0,null,"为应用程序设置特定的环境变量值。每行一个，格式“变量名=值”，如“CONFIG_FILE=d:\\config.json”"],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","操作是否成功"],"pid":["T12","进程ID"],"mainWinHandle":["T12","进程的主窗口句柄"],"mainWinTitle":["T0",null],"stdout":["T0","慎用！仅用于控制台程序，会自动等待进程结束。输出stdout，为空时输出stderr"],"stdoutOnly":["T0","慎用！捕获控制台程序的stdout输出，会自动等待进程结束"],"stderr":["T0","慎用！捕获控制台程序的stderr输出，会自动等待进程结束"],"exitCode":["T12","进程的ExitCode，会自动等待进程结束"]}
  "sys:searchBmp":
    - "屏幕找图/找色/找字"
    - "searchBmp"
    - "在屏幕上查找图片里的内容出现的位置"
    - {"bmp":["T0",1,null,"需要在屏幕中查找的位图路径。位图必须和屏幕图像完全匹配，不能压缩。此时X、Y的值为相对于搜索位图的左上角的偏移"],"bmpVar":["T3",1,null,"需要在屏幕中查找的位图。位图必须和屏幕图像完全匹配，不能压缩。此时X、Y的值为相对于搜索位图的左上角的偏移"],"searchText":["T0",0,null,"要查找的文字。可使用多行指定多组文字，找到任意一组即可"],"color":["T0",1,"#FF0000","要查找的颜色，如#FF0000"],"bmpTargetType":["T9(AllScreens: 所有屏幕; Rect: 坐标范围; CurrentWindow: 当前窗口; MainScreen: 主屏幕)",0,"MainScreen","位图查找范围"],"searchRect":["T0",0,null,"当“查找范围”为“坐标范围”时有效，格式为：left,top,right,bottom"],"bmpPosition":["T9(Center: 位图中间; TopLeft: 左上角; TopRight: 右上角; BottomLeft: 左下角; BottomRight: 右下角)",0,"Center","定位点相对位图的位置"],"x":["T12",1,"0","定位点水平坐标偏移量（正值向右）"],"y":["T12",1,"0","定位点垂直坐标偏移量（正值向下）"],"bmpColorError":["T12",0,"10","匹配像素时允许每个颜色通道的偏差值0-100，0表示精确匹配，速度最快"],"maxFindCount":["T12",0,"1","找图的最大匹配数量。将对每个查找到的目标执行附加动作"],"retryCount":["T12",0,"0","未找到位图时的重试次数。每次重试间隔300ms"],"ignoreWindowsOcr":["T2",0,"False",null],"ignoreBgColor":["T2",0,"True","如果查找图片的4个顶点颜色一致，则认为是背景色，找图时忽略此颜色"],"stopIfFail":["T2",0,"True","获取位置失败后，是否停止后续动作的执行"]}
    - {"isSuccess":["T2",null],"firstPoint":["T0","第一个匹配点坐标，格式为：x坐标,y坐标"],"allPoints":["T4","所有的匹配点列表"],"imgIndex":["T12","从多个图片或多组文字中查找时，返回匹配到的图片或文字组序号，从0开始"]}
  "sys:SelectFileInExplorer":
    - "在资源管理器中定位文件"
    - "selectfileinexplorer"
    - "在资源管理器中选中文件"
    - {"path":["T0",1,null,"要定位的文件完整路径"],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","操作是否成功"]}
  "sys:select":
    - "用户选择"
    - "userselect"
    - "请用户选择一个选项。"
    - {"type":["T9(single: 单选; multi: 多选)",1,"single",null],"prompt":["T0",1,"请选择",null],"note":["T0",0,null,null],"items":["T0",1,null,"每行一个选项，格式为 “文本” 或 “显示文本|值”。如需显示图标，格式请参考文档"],"defaultValue":["T0",0,null,"预先选择的项"],"defaultValueMulti":["T0",0,null,"多选时默认选项，每行一个"],"showFilter":["T9",0,"auto","是否显示筛选框。仅在且使用焦点时有效"],"filterContent":["T0",0,null,"预先显示的筛选内容"],"imeState":["T9(NO_CONTROL: 不控制; ON: 开启; OFF: 关闭)",0,"NO_CONTROL","筛选框输入法状态"],"operations":["T0",0,null,"每行定义一个操作，具体格式请参考文档"],"fontsize":["T1",1,"12",null],"fontfamily":["T0",0,null,"设置字体名称。如有多个字体，使用逗号分隔"],"iconsize":["T1",1,"16",null],"autoCloseSeconds":["T1",0,"0","几秒后自动关闭选择窗口。0表示不自动关闭"],"winLocation":["T9",0,"WithMouse1","在哪里显示选择窗口"],"maxWinSize":["T0",0,null,"设置选择窗口的最大尺寸，格式为：宽度,高度。支持像素数值或屏幕宽高百分比，详情请参考模块文档。 “窗口位置” 类型为 “自定义位置” 时用于指定显示位置，格式为：left,top,right,bottom"],"keepLastPos":["T9(0: 不保持; 3: 保持本次运行的上次位置(左上角); 1: 保持本次运行的上次位置+宽度; 5: 保持本次运行的上次位置+尺寸; 7: 保持本次运行的上次窗口尺寸; 4: 总是保持上次位置(左上角); 2: 总是保持上次位置+宽度; 6: 总是保持上次位置+尺寸; 8: 总是保持上次窗口尺寸)",0,"1","重复显示选择窗口时，保持上次的显示位置"],"noKeyboard":["T2",0,"False","不抢占其他应用的焦点。此时无法使用键盘选择选项，只能用鼠标操作"],"closeOnDeactivated":["T2",0,"False",null],"restoreForeground":["T2",0,"True","将前台窗口还原为弹窗前的活动窗口。否则将会还原到最后一个活动窗口上"],"allowOkWhenEmpty":["T2",0,"False",null],"enableQuickConfirm":["T2",0,"True",null],"topMost":["T2",0,"True",null],"windowKey":["T0",0,null,"再次运行动作时，可根据标识自动关闭前一个窗口并在该位置显示新窗口"],"help":["T0",0,null,"点击弹出显示帮助内容，MarkDown格式"],"stopIfCancel":["T2",0,"True","取消选择后是否停止动作"]}
    - {"isSuccess":["T2","是否成功选择了选项/点击了保存按钮"],"textValue":["T0","选中选项的值"],"selectedIndex":["T12","选择的项在列表里的序号数字，从0开始"],"selectedIndexList":["T4","所有选择的项的序号列表"],"multiSelected":["T4","所有选择的项的值的列表"],"extraOperation":["T0","选择的右键菜单或全局菜单项的值"],"selectedFullItems":["T99","选择选项的完整定义内容（不仅仅返回选项值）"],"selectedItemTitle":["T0","所选中选项的标题"],"filterContent":["T0","最后使用的筛选词"]}
  "sys:sendKeys":
    - "模拟按键B（参数）"
    - "sendKeys"
    - "发送按键和文本"
    - {"keys":["T0",0,null,"要发送的按键序列，使用C#语言SendKeys.Send()语法，具体请参考教程文档"]}
    - {}
  "sys:sendMessage":
    - "向窗口发送消息"
    - "sendMessage"
    - "使用SendMessage Win32Api向窗口发送消息。使用方法请搜索SendMessage Win32 API接口。"
    - {"operation":["T9(SendMessage: SendMessage(等待返回，LParam为数字); SendMessageTextLParam: SendMessage(等待返回，LParam为文本); PostMessage: PostMessage(不等待返回))",0,"SendMessage",null],"hWnd":["T12",0,null,"留空或0表示前台窗口"],"wMsg":["T0",0,null,"要发送的消息"],"wParam":["T0",0,null,null],"lParam":["T0",0,"0",null],"textLParam":["T0",0,null,"文本内容"],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","操作是否成功"],"rtn":["T12","返回值，依据消息的不同具有不同的含义，请查询对应API的文档"]}
  "sys:showWaitWin":
    - "显示等待窗口"
    - "showwaitwin"
    - "显示一个等待用户完成某个操作的提示窗口。用户点击等待窗口下部的按钮，窗口将关闭。点击右上角的X按钮，将会弹窗询问是否终止当前动作。"
    - {"mode":["T9(show: 显示窗口; update: 更新窗口; check: 检查是否关闭; close: 关闭窗口(如果还开着的话); waitClose: 等待用户关闭; showAndWaitClose: 显示窗口并等待用户关闭)",0,"show","请选择操作类型"],"title":["T0",1,"完成后继续",null],"prompt":["T0",1,"请在完成操作后点下面的按钮","提示文字内容"],"winLocation":["T9",0,"BottomRight","在哪里显示选择窗口"],"progress":["T0",0,null,"请以 当前值/总数 的格式传入（可使用插值方式）。 比如：40/80"],"btnText":["T0",1,"完成","默认按键仅用于关闭窗口。文字内容为空时隐藏默认按钮"],"operations":["T0",1,null,"每行定义一个按钮，格式为 “文本” 或 “显示文本|值”。显示在默认按钮的左侧"],"fontsize":["T1",1,"12","按钮上文字的大小，单位为逻辑像素"],"iconSize":["T1",1,"16","按钮上图标的大小，单位为逻辑像素"],"autoCloseSeconds":["T1",0,"0","几秒后自动关闭。0表示不自动关闭"],"stopActionIfClose":["T2",0,"True",null],"activateMode":["T9(NotActivatable: 不支持激活(不占用焦点，仅能使用鼠标操作); NotActivated: 支持激活，打开时不抢占焦点; AutoActivate: 支持激活，打开时抢占焦点)",0,"NotActivatable",null],"help":["T0",0,null,"点击弹出显示帮助内容，MarkDown格式"]}
    - {"isClosed":["T2","等待窗口是否已经关闭了"],"selectedOperation":["T0","选择的后续操作项"]}
  "sys:simpleIf":
    - "如果"
    - "if"
    - "依据条件执行操作"
    - {"condition":["T2",0,null,"是否符合指定的条件"]}
    - {}
  "sys:smtp":
    - "SMTP发送邮件"
    - "smtp"
    - "使用SMTP协议发送邮件"
    - {"server":["T0",1,null,"邮件服务器的域名或IP"],"port":["T12",1,"25","Smtp端口号"],"useSsl":["T2",0,"False","是否使用TLS连接（通常为587端口）"],"account":["T0",1,null,"发信帐号"],"password":["T0",1,null,"发信帐号的密码"],"sender":["T0",1,null,"发信帐号所对应的Email地址"],"senderName":["T0",1,null,"发件人的显示名称（）"],"to":["T0",1,null,"收件人Email地址，多个的话使用小写逗号分隔"],"cc":["T0",1,null,"抄送给的Email地址列表，多个的话使用小写逗号分隔"],"bcc":["T0",1,null,"密送给的Email地址列表，多个的话使用小写逗号分隔"],"subject":["T0",1,null,"邮件的主题"],"content":["T0",0,null,"邮件正文内容"],"attachList":["T0",0,null,"附件文件列表。多个时每行一个"],"isHtml":["T2",0,"False","邮件内容是否为HTML格式"],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","操作是否成功"]}
  "sys:stop":
    - "停止(return)"
    - "stop"
    - "停止动作或从子程序中返回"
    - {"method":["T9(default: 默认：停止动作或从子程序返回; forcestop: 停止动作：停止整个动作(即使在子程序中))",0,"default",null],"isError":["T2",0,"False","用作子程序或被其他动作调用时，返回出错状态"],"return":["T0",0,null,"被其他动作调用时，返回的动作结果"],"showMessage":["T0",0,null,"显示的提示信息"]}
    - {}
  "sys:strCompare":
    - "比较文本"
    - "strCompare"
    - "文本比较"
    - {"param1":["T0",1,null,"被比较的文本"],"type":["T9(>; =; <; contains: 包含; startsWith: 以指定内容开始; endsWith: 以指定内容结束; match: 正则匹配; pinyinMatch: 包含指定内容，或匹配拼音、拼音首字母)",1,">","比较方式"],"param2":["T0",1,null,"对比文本。拼音匹配时，也可用于指定拼音、拼音首字母"],"case":["T2",0,"False","是否区分大小写"]}
    - {"value":["T2","比较结果是否为真"]}
  "sys:stringProcess":
    - "文本处理"
    - "stringprocess"
    - "各种文本处理功能"
    - {"data":["T0",0,null,"需要进行文本处理的内容"],"method":["T9(toUpper: 英文转大写; toLower: 英文转小写; reverse: 前后反转; substring: 截取; trimStart: 去除前面空白字符; trimEnd: 去除后面空白字符; trim: 去除前后空白字符; urlEncode: URL编码; urlDecode: URL解码 (+解码为空格); urlDataDecode: URL数据解码 (保留+号); htmlEncode: Html编码; htmlDecode: Html解码; intercappedToSentence: 组合词拆分成句子(thisIsChina=>this Is China); base64Encode: Base64编码; base64Decode: Base64解码; removeEmptyLine: 去除空行; mergeEmptyLine: 合并多个空行; sortLinesAsc: 排序多行A-Z; sortLinesDesc: 排序多行Z-A; reverseLines: 翻转多行顺序; toTitleCase: 首字母大写; formatJson: 格式化JSON; md5: 计算MD5哈希; sha256Hash: 计算SHA256哈希; sha1Hash: 计算SHA1哈希; escapeJson: 转义文本为合法Json值; DecodeUnicode: 解码Unicode字串(\\\\uXXXX转普通字符); convertEncoding: 转换编码; toCnNum: 金额数字转换为大写; cn2num: 中文转数字; num2cn: 数字转中文; ExpandEnvironmentVariables: 替换环境变量; padLeft: 从左侧补齐长度; padRight: 从右侧补齐长度; insert: 插入内容; append: 追加内容; remove: 移除内容; removeZeroWidthChars: 移除零宽字符; html2text: HTML转纯文本)",0,null,"对文本进行什么处理"],"srcEncoding":["T0",0,"utf-8",null],"dstEncoding":["T0",0,"gbk",null],"start":["T12",0,"0","开始截取/插入位置，从0开始。如果为负值，表示从文本末尾开始向前的字符数"],"value":["T0",0,null,"插入或追加的内容"],"length":["T12",0,"0","截取或移除字符个数。截取时，0表示开始位置以后的所有内容，负值表示截取到结束前的多少个字符"],"totalWidth":["T12",0,"10","补齐后的总字符数"],"paddingChar":["T0",0,null,"补齐时使用的填充字符，默认为空格"],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"output":["T0","处理后的文本"],"isSuccess":["T2","操作是否成功"]}
  "sys:subprogram":
    - "运行子程序"
    - "subprogram"
    - "运行子程序"
    - {"subProgram":["T0",1,null,"调用哪个子程序"],"summary":["T0",0,null,"内部使用"],"skipDebugOutput":["T2",0,"False","调试运行动作时，不输出子程序内部调试信息"],"stopIfFail":["T2",0,"True","子程序运行失败后是否停止动作"]}
    - {"isSuccess":["T2","子程序是否运行成功"]}
  "sys:tempcloudstore":
    - "临时云存储"
    - "tempcloudstore"
    - "将文本、文件、图片临时保存到云端并得到网址。"
    - {"dataType":["T9(text: 文本内容; file: 文件; imageVar: 图片变量)",1,"text",null],"text":["T0",1,null,"要保存的文本内容"],"imageVar":["T3",0,null,"要保存的图片变量"],"file":["T0",1,null,"要保存的文件路径"],"expireSeconds":["T1",0,"2.5","请求超时时间（秒数）"],"useRandomFileName":["T2",0,"False","是否使用随机的文件名（仅适用于上传文件的情况）"],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","操作是否成功"],"url":["T0","生成的访问网址"]}
  "sys:userInput":
    - "用户输入"
    - "userInput"
    - "请用户输入内容。"
    - {"type":["T9(text: 单行文本; multiline: 多行文本; number: 数字; date_time: 日期时间)",1,"text","输入内容的类型"],"prompt":["T0",1,"请输入内容","提示用户输入什么内容。显示在输入框上方"],"defaultValue":["T0",0,null,"默认填写到输入框中的内容"],"texttools":["T0",0,null,"鼠标悬浮在文本框上时显示的小工具"],"extraSettings":["T0",0,null,"可用于自定义文本选择工具，详情请参考文档"],"pattern":["T0",0,null,"正则验证表达式"],"isRequired":["T2",0,"False","是否必须填写内容"],"fontfamily":["T0",0,null,"设置字体名称。如有2个字体，使用逗号分隔"],"fontsize":["T1",1,"14",null],"winLocation":["T9",0,"CenterScreen","在哪里显示选择窗口"],"imeState":["T9(NO_CONTROL: 不控制; ON: 开启; OFF: 关闭)",0,"NO_CONTROL",null],"submitWithReturn":["T2",0,"False",null],"restoreFocus":["T2",0,"True","用户输入后，是否将焦点还原到之前的活动窗口"],"closeOnDeactivated":["T2",0,"False",null],"help":["T0",0,null,"点击弹出显示帮助内容，MarkDown格式"],"topMost":["T2",0,"False",null],"stopIfFail":["T2",0,"True","用户取消后是否停止动作"]}
    - {"isSuccess":["T2","操作是否成功"],"textValue":["T0","文本类型的输入值"],"numberValue":["T1","数字类型的输入值"],"datetimeValue":["T6",null],"isEmpty":["T2","用户是否没有输入内容"]}
  "sys:waitClipboardChange":
    - "等待剪贴板内容改变"
    - "waitclipboardchange"
    - "等待剪贴板的内容发生改变。等待第三方工具（如截图工具）完成操作并更新剪贴板。"
    - {"maxWaitSeconds":["T1",1,"10","超过等待时间剪贴板未改变，则结束等待"],"recentChangeMs":["T12",1,"10","包含在此之前一定时间内(毫秒)发生的改变"],"monitorWaitWin":["T2",0,"False","结合“等待窗口”模块，如果等待窗口关闭，则停止等待剪贴板变化"],"stopIfFail":["T2",0,"True","超时后剪贴板仍未改变，是否中止动作"]}
    - {"isSuccess":["T2","剪贴板内容是否改变了"]}
  "sys:delay":
    - "等待时间"
    - "delay"
    - "等待指定的毫秒数"
    - {"delayMs":["T12",1,"100","等待时间毫秒数"],"monitorWaitWin":["T2",0,"False","结合“等待窗口”模块，如果等待窗口关闭，则停止等待。仅当等待时间超过1000ms时生效"]}
    - {}
  "sys:windowOperations":
    - "窗口操作"
    - "windowoperations"
    - "Window窗口相关操作"
    - {"type":["T9(move: 移动窗口; move_ex: 移动窗口(增强); setTopmost: 置顶窗口; toggleTopMost: 切换置顶状态; removeTopmost: 取消置顶窗口; setBottom: 置底窗口; show: 设置显示状态; SET_FOREGROUND: 设置为前台窗口; close: 关闭; kill: 强制关闭; set_trans: 设置或更新透明度)",1,"move","操作类型"],"hWnd":["T12",0,null,"要操作的窗口句柄（数字）。0或留空表示操作前台窗口"],"x":["T12",0,"100","窗口左上角X坐标"],"y":["T12",0,"100","窗口左上角Y坐标"],"width":["T12",0,"500","窗口宽度。-1时表示不更改窗口尺寸"],"height":["T12",0,"500","窗口高度。-1时表示不更改窗口尺寸"],"area":["T0",0,"25%,25%,75%,75%","窗口左,上,右,下的位置坐标"],"showCmd":["T9(3: 最大化(SW_MAXIMIZE); 6: 最小化(SW_MINIMIZE); 9: 显示并恢复大小(SW_RESTORE); 0: 隐藏(SW_HIDE); 5: 显示(SW_SHOW); TOGGLE_MAXMIZE: 切换最大化/恢复)",1,"3","窗口显示状态，具体说明请参考Win32接口"],"alpha":["T0",0,"128","数字0-255：0为全透明，255为不透明。-数字：将当前透明度增加一些。+数字：将透明度减少一些"],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","操作是否成功"],"isTopmost":["T2","操作后窗口是否为置顶"]}
  "sys:writeClipboard":
    - "写入剪贴板"
    - "writeClipboard"
    - "将文本或图片等内容写入剪贴板"
    - {"type":["T9(auto; html; text; image; rtf; csv; custom: 自定义格式; clear; clearHistory: 清空剪贴板历史(Win10+))",1,"auto","操作类型"],"customFormat":["T0",1,null,"自定义的剪贴板格式名"],"input":["T99",1,null,"要写入剪贴板的数据"],"html":["T0",1,null,"HTML代码片段"],"text":["T0",1,null,"纯文本格式内容"],"imageVar":["T3",0,null,"要写入剪贴板的图片内容"],"fastMode":["T2",0,"False","不需要处理图片中的透明通道时选择"],"successMsg":["T0",1,null,"写入成功后提示消息，如“XXX已写入剪贴板”"],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","操作是否成功"]}
  "sys:fileToClipboard":
    - "文件放入剪贴板"
    - "filetoclipboard"
    - "将文件或文件列表存入剪贴板"
    - {"file":["T0",0,null,"要存入剪贴板的文件(夹)路径（与文件列表二选一）"],"list":["T4",0,null,"要存入剪贴板的多个文件路径（与单个文件二选一）"],"useCut":["T2",0,"False","是否剪切文件"],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","操作是否成功"]}
  "sys:webview2":
    - "WebView2浏览器窗口"
    - "webview2"
    - "基于微软Edge浏览器内核的组件，需要安装Edge最新预览版方可使用。"
    - {"type":["T9(OpenUrl: 打开网页; OpenAndWaitLoad: 打开网页并等待加载完成; OpenUrlAndWaitClose: 打开网页并等待窗口关闭; SendMessage: 发送消息; ExecuteScript: 执行脚本; CheckWindowState: 获取窗口状态; Close: 关闭窗口(如果尚未关闭); Reload: 重新加载/刷新; Stop: 停止加载; CheckInstalled: 检查是否安装WebView2; MultiTab_OpenUrl: 【多标签】打开网址; MultiColumn_OpenUrl: 【多列】打开网址)",0,"OpenUrl",null],"url":["T0",1,null,"网页地址/文件路径或html代码内容"],"urlList":["T4",1,null,"每行一个：网址，或“标题|网址”，或“[图标]标题|网址”格式"],"additionalBrowserArguments":["T0",1,null,"用于设置代理等用途"],"virtualHostToFolder":["T0",1,null,"将文件夹映射为虚拟主机名。格式：主机名|文件夹路径。多个时，每行一个。 在html中可以使用https://servername/path/to/file.png的格式访问文件"],"userAgent":["T0",0,null,"自定义UserAgent"],"title":["T0",1,null,"窗口标题文字。未设置时，自动使用网页标题"],"icon":["T0",0,null,"显示在窗口左上角的图标。支持fa:内置图报名:#RRGGBB或图标网址"],"defaultBgColor":["T0",0,null,"设置窗口的默认背景色"],"autoCloseKey":["T0",0,"=","(仅必要时使用)用于关闭之前打开的具有此标识的WebView2窗口。使用=表示当前动作ID"],"modeForExists":["T9(SkipThisStep: 跳过此步骤; UpdateUrl: 更新网址; UpdateUrlAndPosition: 更新网址和窗口位置; RecreateWindow: 关闭并重建窗口; BringToFront: 激活窗口)",0,"SkipThisStep",null],"script":["T0",1,null,null],"sendMessage":["T0",1,null,"Json格式的消息内容。词典变量会自动转换成json"],"winLocation":["T9",0,"CenterScreen","在哪里显示选择窗口"],"winSize":["T0",0,null,"设置选择窗口的尺寸，格式为：宽度,高度。支持像素数值或屏幕宽高百分比，详情请参考模块文档。 “窗口位置” 类型为 “自定义位置” 时用于指定显示位置，格式为：left,top,right,bottom"],"defaultDownloadFolderPath":["T0",0,null,"默认的文件下载存储目录"],"profileName":["T0",0,null,"当需要同时登录一个网站的多个账号时，可以创建独立的Profile"],"topMost":["T2",0,"False",null],"showInTaskbar":["T2",0,"True",null],"noActivate":["T2",0,"False","不占用焦点时也无法在窗口中输入文字"],"closeWhenLostFocus":["T9(false: 不执行操作; true: 关闭窗口; hide: 隐藏窗口; minimize: 最小化窗口; close_if_not_topmost: 如果未置顶，关闭窗口; hide_if_not_topmost: 如果未置顶，隐藏窗口; minimize_if_not_topmost: 如果未置顶，最小化窗口)",0,"False",null],"escCloseWindow":["T2",0,"False",null],"showToolbar":["T2",0,"False",null],"windowStyle":["T9(normal: 正常; none: 无边框)",0,"normal",null],"clearCookies":["T2",0,"False",null],"addDevTool":["T2",0,"False",null],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","操作是否成功。获取窗口信息时，窗口是否存在"],"isInstalled":["T2",null],"hWnd":["T12",null],"webView":["T98","可用于在C#脚本中使用，需运行在UI线程中。注意避免循环引用"],"lastLocation":["T0","返回窗口坐标范围。格式为：left,top,right,bottom"],"currUri":["T0","浏览器当前网址"],"docTitle":["T0",null],"sourceCode":["T0",null],"cookies":["T0",null],"previewImage":["T3",null],"isNavCompleted":["T2","是否已完成网页加载过程"],"scriptResult":["T0","json编码的脚本运行结果内容"]}
  "sys:color":
    - "屏幕取色/颜色转换与计算"
    - "color"
    - "转换颜色值及相关计算处理"
    - {"type":["T9(fromString: 通过文本指定颜色; selectFromScreen: 从屏幕选取颜色; fromScreenPosition: 取屏幕指定位置颜色; editOrSelectColor: 编辑/选择颜色)",1,"fromString","比较方式"],"colorStr":["T0",1,null,"颜色的文本值, 格式支持：#223344, #FF223344(ARGB顺序), Red, rgb(200,200,200), rgba(200,200,200,0.5), CMYK(0,0,0,0)或CMYK:0,0,0,0"],"location":["T0",1,"0,0","格式为:“横坐标X,纵坐标Y”"],"format":["T9(HEX_RGB: 十六进制RGB: #6496C8; HEX_ARGB: 十六进制ARGB: #FF6496C8; rgba: HTML: rgba(100,150,200,1); rgb: HTML: rgb(100,150,200); DOT_RGB: RGB: 100,150,200; DOT_RGBA: RGBA: 100,150,200,255; DOT_ARGB: ARGB: 255,100,150,200; float_rgba: 浮点: 0.39f, 0.59f, 0.78f, 1.00f; Swift: Swift: UIColor(red:0.39, green:0.59, blue:0.78, alpha:1.00); CMYK: CMYK: 50,25,0,22; HSL: hsl(210,47.6%,58.8%); hsla: hsla(210,47.6%,58.8%,1); HSV_HSB: HSV/HSB: 210°,50,78.4)",1,"HEX_RGB","输出的颜色文本值格式，用以转换颜色值的格式"],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","操作是否成功"],"A":["T1","Alpha值（0-255）0表示透明"],"R":["T1","R值（0-255）"],"G":["T1","G值（0-255）"],"B":["T1","B值（0-255）"],"Hue":["T1","Hue值（0-360）"],"HslS":["T1","HSL颜色空间的饱和度S"],"HslL":["T1","HSL颜色空间的亮度值L"],"HsvS":["T1","HSV颜色空间的饱和度S"],"HsvV":["T1","HSV颜色空间的明度V"],"textValue":["T0","输出颜色的文本值，格式请在输入参数中选择"]}
  "sys:computeTime":
    - "计算时间"
    - "computetime"
    - "时间相关的计算操作"
    - {"type":["T9(getdate: 取日期值(去除当天的时间部分); timespan: 计算时间差(日期时间2 减 日期时间); endtime: 计算结束时间; localToUtc: 本地时间转换为UTC时间; utcToLocal: UTC时间转换为本地时间)",1,"getdate","比较方式"],"time1":["T6",1,null,"要计算的时间值"],"time2":["T6",1,null,"要计算的第二个时间值"],"formatString":["T0",1,"d\\.hh\\:mm\\:ss","时间差转换为文本时的格式化字符串。d:天数,hh:小时,mm:分钟,ss:秒。符号.:需要使用\\转义"],"addYears":["T1",0,"0","添加指定的年数（整数）"],"addMonths":["T1",0,"0","添加指定的月数（整数）结果不跨月，如1月31日增加1个月等于2月28日"],"addDays":["T1",0,"0","添加指定的天数（可以为小数）"],"addHours":["T1",0,"0","添加指定的小时数（可以为小数）"],"addMinutes":["T1",0,"0","添加指定的分钟数（可以为小数）"],"addSeconds":["T1",0,"0","添加指定的秒数（可以为小数）"],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","操作是否成功"],"resultTime":["T6","计算的结果时间"],"totalDays":["T1","间隔的总天数值"],"totalHours":["T1","间隔的总小时数"],"totalMinutes":["T1","间隔的总分钟数值"],"totalSeconds":["T1","间隔的总秒数数值"],"textValue":["T0","时间间隔的文本结果"]}
  "sys:dictOperations":
    - "词典操作"
    - "dictoperations"
    - "对词典变量进行添加、删除等操作"
    - {"type":["T9(get: 取值; set: 设置值 (文本类型); setOriginValue: 设置值 (变量原始类型); remove: 删除一项; clear: 清空; keyList: 获取键(Key)列表; valueList: 获取值列表; reverse: 翻转键值; queryStringToDict: 查询字符串转换为词典(name1=value1&name2=value2...); dictToQueryString: 词典转换为查询字符串; dictToQueryStringNoEncode: 词典转换为查询字符串(不对键和值进行URL编码))",0,"setOriginValue",null],"dict":["T10",0,null,"要操作的词典变量"],"queryString":["T0",0,null,"要解析的查询字符串"],"key":["T0",0,null,"要操作元素的键值"],"value":["T0",0,null,"要保存的内容"],"returnEmptyIfKeyNotExist":["T2",0,"False","此时不作为失败处理"],"ignoreCase":["T2",0,"False",null],"stopIfFail":["T2",0,"False","失败后是否停止动作"]}
    - {"isSuccess":["T2","操作是否成功"],"value":["T99","操作后的输出（取的元素值、键列表、值列表等）"]}
  "sys:everythingsearch":
    - "使用Everything搜索文件"
    - "everythingsearch"
    - "调用Everything提供的接口搜索文件"
    - {"search":["T0",1,null,"要搜索的内容，格式与直接在everything软件中搜索时相同"],"folder":["T0",0,null,"在指定目录下搜索（包含子目录）"],"ext":["T0",0,null,"半角分号分隔的扩展名列表。如“txt;docx;xslx;”"],"matchWholeFilename":["T2",0,"0","匹配整个文件名。0表示否，1表示是"],"matchWholeWord":["T2",0,"1","匹配整个单词。如 quicker.exe 将会匹配：quicker.exe, quicker.exe.config等。0表示否，1表示是"],"matchPath":["T2",0,"0","匹配路径的不同部分，而不仅是文件名"],"matchCase":["T2",0,"0","是否大小写敏感。0表示否，1表示是"],"useRegex":["T2",0,"0","是否使用正则匹配。0表示否，1表示是"],"maxCount":["T12",1,"100","-1表示不限制"],"sort":["T9(1: 名称顺序 NAME_ASCENDING; 2: 名称倒序 NAME_DESCENDING; 3: 路径顺序 PATH_ASCENDING; 4: 路径倒序 PATH_DESCENDING; 5: 大小顺序 SIZE_ASCENDING; 6: 大小倒序 SIZE_DESCENDING; 7: 扩展名顺序 EXTENSION_ASCENDING; 8: 扩展名倒序 EXTENSION_DESCENDING; 9: 类型名顺序 TYPE_NAME_ASCENDING; 10: 类型名倒序 TYPE_NAME_DESCENDING; 11: 创建时间顺序 DATE_CREATED_ASCENDING; 12: 创建时间倒序 DATE_CREATED_DESCENDING; 13: 修改时间顺序 DATE_MODIFIED_ASCENDING; 14: 修改时间倒序 DATE_MODIFIED_DESCENDING; 15: 属性顺序 ATTRIBUTES_ASCENDING; 16: 属性倒序 ATTRIBUTES_DESCENDING; 17: 文件列表文件名顺序 FILE_LIST_FILENAME_ASCENDING; 18: 文件列表文件名倒序 FILE_LIST_FILENAME_DESCENDING; 19: 运行次数顺序 RUN_COUNT_ASCENDING; 20: 运行次数倒序 RUN_COUNT_DESCENDING; 21: 最后变更时间顺序 DATE_RECENTLY_CHANGED_ASCENDING; 22: 最后变更时间倒序 DATE_RECENTLY_CHANGED_DESCENDING; 23: 最后访问时间顺序 DATE_ACCESSED_ASCENDING; 24: 最后访问时间倒序 DATE_ACCESSED_DESCENDING; 25: 最后运行时间顺序 DATE_RUN_ASCENDING; 26: 最后运行时间倒序 DATE_RUN_DESCENDING)",1,"1",null],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","操作是否成功"],"pathList":["T4",null],"resultCount":["T12",null],"rawResult":["T98",null]}
  "sys:fileOperation":
    - "文件和目录操作"
    - "fileoperation"
    - "文件和目录操作。请确保路径是合法的。"
    - {"type":["T9(copyInto: 复制到指定目录下; copyIntoWithShell: 复制到指定目录下(Windows); copyTo: 复制为(指定结果名称或路径); moveInto: 移动到指定目录下; moveIntoWithShell: 移动到指定目录下(Windows); rename: 移动/重命名为(指定结果名称或完整路径); deleteFile: 删除文件(不支持文件夹); deleteEmptyFolder: 删除空文件夹; recycle: 移入回收站; recycleNoUi: 移入回收站(安静模式，自动确认操作); makeDir: 创建文件夹; createFile: 创建空文件; enumFiles: 获取文件夹内的文件; enumDirs: 获取文件夹内的子文件夹; copyFile: 复制文件/文件夹(自动)【不建议使用】; moveFile: 移动/重命名文件(夹)(自动)【不建议使用】)",1,null,"操作类型"],"path":["T0",0,null,"要操作的文件或文件夹路径"],"dstPath":["T0",0,null,"复制/移动的目标路径或新文件、文件名。详情请参考文档"],"searchPattern":["T0",0,"*","筛选文件或目录名。可以包含通配符*和?，或“regex:正则表达式”。搜索文件时也可以为分号隔开的多个后缀名如.jpg;.png;.bmp"],"isAll":["T2",0,"False","包含子目录中的(否则只搜索顶层目录)"],"overwrite":["T2",0,"False","如果目标位置已存在文件，是否覆盖？"],"stopIfFail":["T2",0,"True","如果操作异常，是否终止动作"]}
    - {"isSuccess":["T2","操作是否成功"],"files":["T4","搜索到的文件或文件夹列表"],"resultPath":["T0","结果文件路径"]}
  "sys:GenTempFilePath":
    - "生成临时文件路径"
    - "gentempfilepath"
    - "根据指定的扩展名生成一个随机的临时文件名（完整路径），供后续步骤写入文件使用。"
    - {"ext":["T0",1,".txt","生成临时文件的扩展名"]}
    - {"filePath":["T0","生成的临时文件路径"]}
  "sys:getSelectedFiles":
    - "获取选择的文件(夹)/选择特定文件"
    - "getselectedfiles"
    - "获取资源管理器、桌面等位置选择的文件或文件夹的路径"
    - {"operation":["T9(getSelection: 获取选择的文件; setSelection: 设置选择的文件)",0,"getSelection",null],"waitMs":["T12",0,"200","通过复制方式获取选择文件时，等待剪贴板变化的最长时间毫秒数"],"sortType":["T9(Default: 默认(文件名自然排序); Origin: 原始(系统返回顺序); FileName: 文件名(字母顺序); FileNameNature: 文件名(自然顺序); FileSizeAsc: 文件大小(从小到大); FileSizeDesc: 文件大小(从大到小); CreationTimeDesc: 创建时间(从新到旧); CreationTimeAsc: 创建时间(从旧到新); LastAccessTimeDesc: 最后访问时间(从晚到早); LastAccessTimeAsc: 最后访问时间(从早到晚); LastWriteTimeDesc: 最后写入时间(从晚到早); LastWriteTimeAsc: 最后写入时间(从早到晚))",0,"Default","获取多个文件时，根据需要可以对文件列表进行排序。仅支持文件"],"pathList":["T0",0,null,"要选中的路径或文件名。支持使用 “regex:表达式” “pinyin:筛选” 选择匹配的文件"],"stopIfFail":["T2",0,"True","获取失败后，是否停止后续动作的执行"],"winHandle":["T12",0,null,"指定要操作的资源管理器窗口，留空时表示前台窗口。（仅支持资源管理器）"]}
    - {"isSuccess":["T2","是否成功获得文件列表"],"files":["T4","所有选中的文件和文件夹的路径列表"],"firstFile":["T0","选择1个文件(夹)时，返回其路径；选择多个时，返回第一个的路径"],"fileNames":["T4","所有选中的文件和文件夹的名称的列表（不包含所在路径）"],"firstFileName":["T0","选择1个文件(夹)时，返回其名称；选择多个时，返回第一个的名称"],"fileCount":["T12","选择的文件个数"]}
  "sys:readFile":
    - "读取文件"
    - "readFile"
    - "将读取的文本或图片内容写入变量。"
    - {"path":["T0",1,null,"要读取的文件的完整路径"],"type":["T9(text: 文本; image: 图片)",1,"text","文件内容类型"],"encoding":["T9",1,"utf-8","文件的编码格式"],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"txt":["T0","读取的文本文件的内容"],"image":["T3","读取的图片文件的内容"],"isSuccess":["T2","操作是否成功"]}
  "sys:selectFile":
    - "选择文件"
    - "selectfile"
    - "用文件选择对话框选择要打开或保存的文件"
    - {"type":["T9(saveFile: 保存文件; openFile: 打开文件; openMultiFile: 打开多个文件)",1,"openFile","打开文件：选择一个已存在的文件。保存文件：选择文件要保存的目标位置"],"filter":["T0",0,"文本文件|*.txt|所有文件|*.*","文件类型筛选器，格式为：类型1|扩展名1|类型2|扩展名2。如：文本文件(*.txt)|*.txt|C#文件|*.cs|所有文件|*.*"],"defaultExt":["T0",0,".txt","默认的文件扩展名，应该是筛选器里的一种"],"initDir":["T0",0,null,"初始文件夹路径"],"initFileName":["T0",0,null,"预选选择或设置的文件名"],"title":["T0",0,null,"选择窗口的标题"],"topMost":["T2",0,"True","是否置置顶显示窗口"],"stopIfFail":["T2",0,"True","取消后是否停止动作运行"]}
    - {"isSuccess":["T2","是否成功选择了路径"],"path":["T0","选择的文件路径"],"pathList":["T4","选择的文件路径列表"]}
  "sys:selectFolder":
    - "选择文件夹"
    - "selectfolder"
    - "文件夹选择对话框"
    - {"prompt":["T0",1,"请选择文件夹","选择窗口的标题"],"initDir":["T0",0,null,"初始文件夹路径"],"showOpenedDirs":["T2",0,"True","显示当前在资源管理器窗口中打开的文件夹"],"stopIfFail":["T2",0,"True","取消后是否停止动作运行"]}
    - {"isSuccess":["T2","是否成功选择了路径"],"path":["T0","选择的文件夹路径"]}
  "sys:WriteTextFile":
    - "写入文本文件"
    - "writetextfile"
    - "将内容写入文本文件"
    - {"content":["T0",1,null,"要写入文件的内容"],"filePath":["T0",1,null,"要写入的完整文件路径（包含文件名）"],"encoding":["T9",1,"utf-8","写入文件的编码格式"],"addUtf8Bom":["T2",0,"False","UTF8编码文件是否写入BOM标记"],"appendMode":["T2",0,"False","如果文件已存在，则添加到文件的末尾"],"addNewLine":["T2",0,"False","在文件末尾添加空行"],"newLineChars":["T9(: 默认(不处理); \\r\\n; \\r; \\n)",1,null,null],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","操作是否成功"]}
  "sys:zip":
    - "Zip压缩打包"
    - "zip"
    - "Zip压缩或解压缩"
    - {"type":["T9(Zip: 创建Zip文件; Unzip: 解压缩Zip文件)",0,"Zip",null],"sourcePath":["T0",1,null,"待压缩的文件夹或文件路径。多个文件时每个文件一行"],"targetZipFile":["T0",1,null,"压缩时：目标文件的路径。留空时自动生成临时文件。点(.)表示待压缩的文件夹或文件所在位置"],"sourceZipFile":["T0",1,null,"待解压的文件路径"],"keepBaseFolder":["T2",0,"False",null],"outputPath":["T0",1,null,"解压缩的目标路径, 点(.)表示zip文件所在的文件夹, 星(*)表示以zip文件名创建的子文件夹"],"password":["T0",0,null,"压缩文件密码"],"comment":["T0",0,null,"压缩文件注释内容"],"level":["T12",0,"1","压缩级别，0-9。0表示不压缩（速度快），9表示压缩到最小（速度慢）"],"overwrite":["T2",0,"False",null],"skipOverwriteError":["T2",0,"False","忽略掉无法覆盖的情况"],"showProgress":["T2",0,"False","仅支持解压缩或压缩单个文件夹"],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","操作是否成功"],"resultPath":["T0","生成的zip文件完整路径，或解压缩后的完整路径"]}
  "sys:screenCapture":
    - "屏幕截图"
    - "screencapture"
    - "截取屏幕区域"
    - {"type":["T9(select: 选择区域; full_screen: 所有屏幕; primary_screen: 主屏幕; fixed_area: 固定区域; window: 窗口 (屏幕可见内容); windowBackground: 窗口 (支持后台显示))",0,"select","截取图片的屏幕区域类型"],"area":["T0",0,null,"要截取的屏幕坐标位置（像素值），格式为：left,top,right,bottom。默认不包含右边和底边像素"],"windowHandle":["T12",0,"0","要截取的窗口句柄数字。0或留空表示截取前台窗口"],"delay":["T12",1,"0","等待多少毫秒后开始截图"],"preSelectArea":["T0",0,null,"非必要请勿设置。预先选择的截图区域，格式为：left,top,right,bottom。默认不包含右边和底边像素"],"includeRightBottomBorder":["T2",0,"True","包含时，当指定 0,0,2,2 的时候，截图的大小为3*3, 否则为2*2"],"toClip":["T2",0,"False","截屏图片是否写入到剪贴板中"],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"img":["T3","截图的图片"],"rect":["T0","图片的截取区域(left,top,right,bottom)"],"isSuccess":["T2","操作是否成功"]}
  "sys:createQrCode":
    - "生成二维码"
    - "createqrcode"
    - "将文本转换为二维码"
    - {"code":["T0",1,null,"要转换为二维码的内容"],"pixelsPerModule":["T12",0,"4",null],"darkColor":["T0",0,"#FF000000","#AARRGGBB格式的颜色值"],"lightColor":["T0",0,"#FFFFFFFF","#AARRGGBB格式的颜色值"],"icon":["T3",0,null,"图片变量或图标文件路径"],"iconPercent":["T12",0,"15","百分比数字（只填数字，不写百分号）"],"iconBorderWidth":["T12",0,"6","最小为1"],"drawQuietZones":["T2",0,"1",null],"saveToPdfPath":["T0",0,null,null],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","操作是否成功"],"img":["T3","生成的二维码图片对象"],"svg":["T0","Svg格式结果代码"],"ascii":["T0","Ascii字符格式结果代码"]}
  "sys:whiteboard":
    - "手写板"
    - "whiteboard"
    - "手写内容，生成图片对象。"
    - {"winPosition":["T0",0,"15%,30%,85%,70%","指定显示位置，格式为：left,top,right,bottom。支持像素数值或屏幕宽高百分比"],"bgColor":["T0",0,"#FFFFFFFF","绘图窗口的背景颜色。格式为#AARRGGBB"],"penColor":["T0",0,"#FFFF0000","画笔颜色。格式为#AARRGGBB"],"enableTransparent":["T2",0,"False","不显示窗口标题栏，绘图区透明，可以看到底层窗口内容"],"imageWithBackground":["T2",0,"False","使用透明窗口时，结果图片是否包含背景内容"],"stopIfFail":["T2",0,"True",null]}
    - {"isSuccess":["T2","操作是否成功"],"result":["T3",null]}
  "sys:imageinfo":
    - "读取图片信息"
    - "imageinfo"
    - "获取图片的尺寸或exif信息"
    - {"sourceType":["T9(var: 图片变量; file: 图片文件)",0,"var",null],"bmpFile":["T0",1,null,"图片文件的完整路径"],"bmpVar":["T3",1,null,null],"autoRotate":["T2",0,"False","如果Exif中包含旋转角度信息，则获取旋转后的宽高"],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","操作是否成功"],"width":["T12",null],"height":["T12",null],"rotateDegree":["T12",null],"dateTimeOriginal":["T6",null],"exifData":["T10","转换为文本格式的exif数据（词典格式，请参考模块文档）"],"rawExifData":["T10","原始Exif数据(词典格式，请参考模块文档)"],"fileTypeFromData":["T0","根据文件内容判断的文件格式（可能不准确），用于在无法根据扩展名得到图片格式的情况下使用"]}
  "sys:imgProcess":
    - "图片处理"
    - "imgprocess"
    - "图片处理和变换"
    - {"img":["T3",1,null,"要转换的图片"],"type":["T9(resize_percent: 缩放图片(指定比例); resize_pixel: 缩小图片(指定像素); Clone: 复制图片; Invert: 反色; GrayScale: 灰度; Rotate: 旋转; Filters: 组合处理; GenerateIco: 生成图标文件(.ico))",0,"resize_percent","对图片的转换操作类型"],"resizePercent":["T1",0,"50","缩小或放大到原来的百分之多少"],"maxWidth":["T12",0,"0","最大宽度(像素数)，0表示自动"],"maxHeight":["T12",0,"0","最大高度(像素数)，0表示自动"],"rotation":["T12",0,"0","顺时针角度。0:不旋转, 1:90°, 2:180°, 3:270°, 其他值请参考模块文档"],"filterParams":["T0",0,null,"每行设定一个处理步骤，具体设置请参考文档"],"iconFilePath":["T0",1,null,"保存图标文件(.ico)的完整路径"],"iconSize":["T0",1,"256,48,32,16","图标中的位图大小，单位为像素。多尺寸图标可用英文逗号风格"],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","操作是否成功"],"result":["T3","处理后的图片"]}
  "sys:readQrCode":
    - "识别二维码"
    - "readqrcode"
    - "识别图片中的二维码"
    - {"img":["T3",1,null,"要识别二维码的图片"],"tryNetwork":["T2",0,"False","在线服务拥有更强识别能力（频率限制2秒/次，仅专业版提供）"],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","操作是否成功"],"code":["T0","识别出的二维码内容"],"codeList":["T4","当一个图片含有多个二维码，且需要返回所有结果时使用"]}
  "sys:showImage":
    - "显示图片"
    - "showImage"
    - "在屏幕上显示图片。输入文件路径/url或图片变量。"
    - {"source":["T9(file: 显示：图片文件或网络图片; var: 显示：变量中的图片; clipboard: 显示：剪贴板图片; closeWindow: 关闭图片窗口; getState: 获取图片窗口信息; getImageWindows: 获取所有图片窗口标识)",0,"var","图片来源类型"],"path":["T0",1,null,"图片文件的路径或网址"],"imgVar":["T3",1,null,"从指定变量中加载图片"],"scale":["T1",1,"1","可以为小数，1表示原始大小，-1表示对大图自动调整缩放比例"],"opacity":["T1",1,"1","0-1之间的小数，1为完全不透明，0为完全透明"],"autoCloseKey":["T0",0,null,"(仅必要时使用)自动关闭之前打开的具有此标识的图片窗口"],"autoCloseTime":["T1",1,"0","几秒后自动关闭，可以为小数。0：不自动关闭"],"winLocation":["T9",0,"Auto","图片显示位置"],"winPosition":["T0",0,null,"仅用于位置为“自定义位置”类型。格式为:left,top或left,top,right,bottom"],"waitClose":["T2",0,"False","是否等待图片关闭后再执行后续步骤"],"showDropShadow":["T2",0,"True","是否显示边框阴影"],"showTaskbarIcon":["T2",0,"True","是否显示任务栏图标"],"topMost":["T2",0,"True","是否置顶显示图片"],"noActivate":["T2",0,"False","图片窗口显示时不抢占焦点（无法通过Esc关闭）"],"closeWhenLostFocus":["T2",0,"False",null],"tooltip":["T0",0,null,null]}
    - {"isExists":["T2","是否存在指定标识的窗口"],"hwnd":["T12","新创建的图片窗口的句柄"],"finalPosition":["T0","移动窗口后的贴图位置格式为left,top,right,bottom。显示图片（开启“等待图片关闭” 选项）或获取当前打开的图片窗口信息时有效"],"windowIdList":["T4",null]}
  "sys:tempImgBed":
    - "临时图床"
    - "tempImgBed"
    - "将图片上传到临时（1分钟后删除）的图床，用以搜图等场景。勿上传非法内容。"
    - {"imgVar":["T3",0,null,"指定要上传的图片变量"],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","操作是否成功"],"url":["T0","图片的临时网址"]}
  "sys:imgToBase64":
    - "图片/Base64 转换"
    - "imgtobase64"
    - "图片和Base64转换"
    - {"type":["T9(imgToBase64: 图片或文件转Base64文本; base64ToImg: Base64文本转图片)",0,"imgToBase64","转换操作类型"],"img":["T3",1,null,"要转换的图片（图片变量或文件路径）"],"addHeader":["T2",0,"False","是否添加“data:image/png;base64,”头"],"base64":["T0",1,null,"要转换的编码文本"]}
    - {"code":["T0","Base64编码结果"],"img":["T3","转换输出的图片"]}
  "sys:WriteImageFile":
    - "写入图片文件"
    - "writeimagefile"
    - "将图片内容写入文件"
    - {"content":["T3",1,null,"要写入文件的图片（变量）"],"filePath":["T0",1,null,"要写入的文件完整路径（包含文件名）"],"quality":["T0",1,"95","保存为JPG格式时的图片质量参数。范围10-100"],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","操作是否成功"]}
  "sys:listOperations":
    - "列表操作"
    - "listoperations"
    - "对列表变量进行添加、删除等操作"
    - {"list":["T4",0,null,"要操作的列表变量"],"type":["T9(none: 无操作(仅用于获取列表信息); getAt: 读取某位置元素; append: 添加元素到末尾; insertAt: 插入元素; setAt: 设置/更新某序号元素; remove: 去除元素(指定值，有多个时去除第一个); removeAllByValue: 去除元素(指定值，有多个时去除全部); removeAt: 去除元素(指定位置); removeByMatch: 去除元素(匹配正则表达式的项); removeByNotMatch: 去除元素(不匹配正则表达式的项); clear: 清空列表; sortAsc: 排序A-Z(输出到结果); sortDesc: 排序Z-A(输出到结果); sortAscNature: 自然排序A-Z(输出到结果); FileSizeAsc: 排序文件列表：文件大小(从小到大); FileSizeDesc: 排序文件列表：文件大小(从大到小); CreationTimeDesc: 排序文件列表：创建时间(从新到旧); CreationTimeAsc: 排序文件列表：创建时间(从旧到新); LastAccessTimeDesc: 排序文件列表：最后访问时间(从晚到早); LastAccessTimeAsc: 排序文件列表：最后访问时间(从早到晚); LastWriteTimeDesc: 排序文件列表：最后写入时间(从晚到早); LastWriteTimeAsc: 排序文件列表：最后写入时间(从早到晚); reverse: 倒置; sub: 截取(输出到结果); concat: 拼接(输出到结果); distinct: 去除重复(输出到结果); indexOf: 获取值的序号; filterByRegex: 筛选(正则,输出到结果); filterByDefault: 筛选(模糊匹配,输出到结果); filterByContains: 筛选(包含); filterByStarts: 筛选(开始); filterByEnds: 筛选(结束))",0,"none",null],"list2":["T4",0,null,"要拼接的列表"],"pos":["T12",0,"0","目标元素的序号，从0开始。负值表示从后向前的第几个"],"length":["T12",0,"1","操作元素的数量"],"item":["T0",0,null,"要插入或更新的值，或筛选关键词"],"orderByScore":["T2",0,"False","筛选结果按匹配程度倒序排列"],"pattern":["T0",0,null,"要匹配的正则表达式"]}
    - {"value":["T99","操作后的输出（取的元素值、排序、切片或拼接后的列表等）"],"isEmpty":["T2","空返回true，非空返回false"],"length":["T12","列表包含的元素数量，截断或拼接后输出结果列表的长度"],"index":["T12","值在列表里的序号，-1表示不存在"],"filterOutItems":["T99","不符合筛选条件的项的列表"]}
  "sys:manageList":
    - "管理和排序列表"
    - "managelist"
    - "对列表内容进行手工排序、添加、删除等操作"
    - {"list":["T4",0,null,"要操作的列表变量。直接选择对应变量，不要使用表达式"],"winTitle":["T0",0,null,null],"note":["T0",0,null,null],"parseData":["T2",0,"False","解析 “[图标]标题(tooltip)|值” 格式的数据并显示图标"],"seperator":["T0",0,"|","解析菜单数据时，显示内容与值之间的分隔符，默认为竖线'|'"],"windowSize":["T0",0,null,"，在需要自定义窗口宽度的情况下使用。最小值为200"],"allowAdd":["T2",0,"True",null],"allowEdit":["T2",0,"True",null],"allowDelete":["T2",0,"True",null],"stopIfFail":["T2",0,"False",null],"help":["T0",0,null,"点击弹出显示帮助内容，MarkDown格式"],"titleDelegate":["T0",0,null,"，在不解析菜单数据时自定义每一项的显示内容。使用方式请参考模块文档"]}
    - {"isSuccess":["T2","是否点击了确认按钮"]}
  "sys:assign":
    - "赋值"
    - "assign"
    - "为变量赋值。使用频率最高的模块，支持文本字符串或插值格式或C#代码模式。"
    - {"input":["T99",1,null,"要赋值给变量的内容，可以直接是其他变量，也可以直接输入值或使用插值格式"],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","操作是否成功"],"output":["T99","将数据写入到变量中"]}
  "sys:comment":
    - "注释"
    - "comment"
    - "使用注释来描述后续步骤的目的。"
    - {"note":["T0",0,null,"注释内容"]}
    - {}
  "sys:compute":
    - "计算"
    - "compute"
    - "对表达式进行计算。"
    - {"expression":["T0",1,"1+1","要计算的表达式"],"evalVar":["T2",0,"False","支持在表达式中使用{变量名}和Math对象"],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","操作是否成功"],"output":["T99","将表达式计算结果写入变量"]}
  "sys:newGuid":
    - "生成Guid"
    - "newguid"
    - "生成一个新的Guid(全局唯一ID标示符)，并转换为文本格式。"
    - {"format":["T9(D: 默认：00000000-0000-0000-0000-000000000000; N: 去除连字符：00000000000000000000000000000000; B: 大括号包围：{00000000-0000-0000-0000-000000000000}; P: 小括号包围：(00000000-0000-0000-0000-000000000000); X: 十六进制：{0x00000000,0x0000,0x0000,{0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00}})",0,"D","转换为文本时使用的格式"],"upper":["T2",0,"False","字母输出为大写格式"]}
    - {"output":["T0","将获得的文本写入到变量"]}
  "sys:form":
    - "多字段表单"
    - "form"
    - "使用表单窗口编辑多个变量的值。"
    - {"operation":["T9(variables: 编辑动作变量的值; dict: 编辑词典数据; dict_dynamic: 编辑词典数据(动态))",0,"variables","工作模式：编辑某个词典的值，或编辑一些变量的值"],"dictVar":["T10",0,null,"表单需要编辑的词典变量"],"title":["T0",1,"填写表单","表单窗口标题文字"],"formDef":["T11",1,null,null],"formForDictDef":["T14",1,null,null],"dynamicFormForDictDef":["T0",1,null,"JSON格式的表单定义数据。格式说明请参考模块文档"],"help":["T0",0,null,"帮助用户填写表单的提示文字"],"markdownhelp":["T0",0,null,"点击弹出显示帮助内容，MarkDown格式"],"titleColumnWidth":["T1",0,"100","左侧字段标题区域的宽度(逻辑像素)。负值，如-200表示自适应列宽且最大宽度为200"],"windowWidth":["T1",1,"500","逻辑像素，最小400"],"defaultInputWidth":["T1",1,"0","逻辑像素，0表示自动宽度"],"windowHeight":["T1",1,"0","逻辑像素，0表示默认。设置时请填写大于100的值"],"restoreFocus":["T2",0,"False","用户输入后，是否将焦点还原到之前的活动窗口"],"topMost":["T2",0,"False",null],"confirm":["T0",0,null,"仅在需要时填写。使用\"_字符\"的形式定义触发字符,如\"_S\"表示Alt+S可直接触发按钮"],"customButtons":["T0",0,null,"使用\"标题|返回值\"的形式定义按钮，多个按钮用换行分隔"],"selectedGroup":["T0",0,null,"使用分组标签页时，默认选择的分组"],"winLocation":["T9",0,"CenterScreen","在哪里显示选择窗口"],"winSize":["T0",0,null,"当 “窗口位置” 类型为 “自定义位置” 时用于指定显示位置，格式为：left,top,right,bottom"],"disableEnterSubmit":["T2",0,"False",null],"stopIfFail":["T2",0,"True","取消后是否停止动作"]}
    - {"isSuccess":["T2","操作是否成功"],"button":["T0","默认的确认按钮返回值为空，自定义按钮返回值为自定义的值"],"selectedGroup":["T0","关闭时所选择的标签页分组"]}
  "sys:playRecords":
    - "重放键鼠操作"
    - "playrecord"
    - "重放录制好的键鼠操作数据。"
    - {"data":["T0",1,null,"录制的键鼠操作数据"],"speed":["T1",1,"2","重放操作的速度"]}
    - {}
  "sys:record":
    - "录制键鼠操作"
    - "record"
    - "录制键鼠操作过程，录制的数据使用绝对坐标"
    - {"autoStart":["T2",0,"True","2秒后是否自动开始录制"],"recordMouseMove":["T2",0,"True","是否录制鼠标的中间移动过程，仅必要时开启。关闭时仅记录点击位置"],"prepareSeconds":["T1",0,"2","开始录制前的倒计时秒数（支持小数）"],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","操作是否成功"],"output":["T0","录制的结果数据"]}
  "sys:runScript":
    - "运行脚本"
    - "runScript"
    - "此模块用于执行一段脚本代码。除了CMD命令，其他脚本类型将会在执行时先将脚本存入临时文件，然后执行此临时文件。"
    - {"script":["T0",1,null,"要运行的脚本内容"],"type":["T9(CMD_K: CMD命令 (完成后保留窗口); CMD_C: CMD命令 (完成后关闭窗口); CMD_H: CMD命令 (隐藏命令行窗口); BAT: BAT批处理脚本(.bat); CMD_F: CMD批处理脚本(.cmd); PS: PowerShell脚本(.ps1); AHK: AutoHotKey脚本(.ahk); CUSTOM: 自定义脚本类型)",1,"CMD_K","要执行的脚本类型"],"ext":["T0",1,null,"自定义脚本文件的扩展名(如: .ps1 )"],"encoding":["T9",1,"default","写入文件的编码格式"],"runner":["T0",1,null,"使用指定的程序运行脚本。如果双击脚本可以直接运行，则不需要指定"],"argTemplate":["T0",1,"%FILE%","使用指定软件时指定命令行参数的格式。%FILE% 代替脚本文件的路径"],"outputEncoding":["T9",1,"oem","控制台输出编码。如果输出遇到乱码，尝试修改此选项"],"workingDir":["T0",0,null,"不填写（自动为资源管理器的当前目录或桌面目录）或具体的工作目录路径"],"runAsAdmin":["T2",0,"False","是否以管理员身份运行脚本。隐藏窗口或输出控制台内容时，不支持以管理员身份运行"],"waitToExit":["T2",0,"False","等待此进程结束后再进行后续操作"]}
    - {"stdout":["T0","捕获控制台输出(输出stdout，为空时输出stderr)，会自动等待进程结束。输出此内容时，命令行窗口将不显示"],"stdoutOnly":["T0","捕获标准输出(stdout)，会自动等待进程结束。输出此内容时，命令行窗口将不显示"],"stderr":["T0","捕获错误输出(stderr)，会自动等待进程结束。输出此内容时，命令行窗口将不显示"]}
  "sys:stateStorage":
    - "状态存取"
    - "stateStorage"
    - "存取状态数据；更新动作的徽标文字；设置附加的动作右键菜单项"
    - {"type":["T9(readActionState: 读取动作状态; saveActionState: 写入动作状态; UpdateActionBadge: 设置徽标文字; UpdateOverlyIcon: 设置徽标图标; UpdateContextMenu: 设置附加的右键菜单项; readGlobalState: 【谨慎使用】读取全局状态; saveGlobalState: 【谨慎使用】写入全局状态)",1,"readActionState",null],"key":["T0",0,null,"存储或读取的状态条目名称"],"defaultValue":["T0",0,null,"读取失败的时候返回的值"],"value":["T0",0,null,"要保存的状态值。使用*NULL*删除此状态的存储"],"inputIfEmpty":["T2",0,"False","如果读到的状态值为空，则弹出对话框请用户输入值。启用此选项时，请保持默认值为空"],"prompt":["T0",0,null,"需要用户输入变量内容时，给用户的输入提示"],"badgeText":["T0",0,null,"在动作右上角显示的提示文字"],"badgeColor":["T0",0,null,"在动作右上角显示的徽标底色。留空表示透明"],"badgeTextColor":["T0",0,null,null],"actionContextMenu":["T0",0,null,"附加的动作右键菜单，格式请参考文档"],"overlayIcon":["T0",0,null,"使用内置矢量图标：“fa:图标名称:图标颜色”。如：“fa:Solid_Circle:#FF0000”"]}
    - {"isSuccess":["T2","是否成功获取了值"],"value":["T99","读取到的值"],"isEmpty":["T2","读取到的值是否为空"]}
  "sys:download":
    - "下载文件"
    - "download"
    - "下载网络文件(请勿用于下载大文件)"
    - {"url":["T0",1,"https://","要下载的文件网址"],"savePath":["T0",1,null,"下载文件的保存位置（文件夹的路径）"],"saveName":["T0",1,null,"为空时自动判断文件名"],"ua":["T0",0,null,null],"header":["T0",0,null,"发送的HttpHeader。每行一个header，格式为Name:Value"],"cookie":["T0",0,null,"请求的cookie内容"],"expireSeconds":["T1",0,"10","长时间未接收到数据时，中止下载"],"skipCertVerify":["T2",0,"False",null],"showProgress":["T2",0,"False","是否显示下载进度条"],"autoRename":["T2",0,"False","在文件名后面增加“_序号”避免重复。否则将会覆盖已有文件"],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","是否成功下载了文件"],"savedPath":["T0","文件的完整保存路径"],"contentMd5":["T0","内容MD5值，不是所有请求都会返回此内容"],"eTag":["T0","响应头Etag值，不是所有请求都会返回此内容"],"downloadSize":["T0","下载文件的大小（字节数）"]}
  "sys:basic-ocr":
    - "基础OCR"
    - "basic-ocr"
    - "获取图片中的文字"
    - {"operation":["T9(QuickerServerOcr: Quicker OCR引擎; WindowsOcr: Windows10/11 内置OCR引擎; baidu-basic: 百度通用文字识别(自定义帐号); baidu-quicker: 百度通用文字识别(Quicker帐号); baidu-custom: 百度自定义接口识别(自定义帐号); table_quicker: 表格识别(Quicker服务))",1,"QuickerServerOcr","OCR接口或引擎。离线引擎安装方式请参考模块文档"],"apiKey":["T0",1,null,"请填写OCR帐号的ApiKey"],"secretKey":["T0",1,null,"请填写OCR帐号的SecretKey"],"imgVar":["T3",1,null,"从指定变量中加载图片"],"punctuationType":["T9(no: 不转换; sbc: 全角符号; dbc: 半角符号)",1,"no","合并文本时，是否转换标点符号"],"mergeChapter":["T9(no: 不合并; merge: 合并)",1,"no","是否智能合并段落"],"interface":["T0(general_basic: 通用文字识别(标准版); general: 通用文字识别(标准含位置版); accurate_basic: 通用文字识别(高精度版); accurate: 通用文字识别(高精度含位置版); handwriting: 手写文字识别; numbers: 数字识别; doc_analysis_office: 办公文档识别; form: 表格文字识别(同步接口); qrcode: 二维码识别)",0,null,"接口的完整网址，或 https://aip.baidubce.com/rest/2.0/ocr/v1/ 后面的部分"],"options":["T10",0,null,"请参考百度官方/Quicker服务接口说明。每行一个参数，使用option:value的格式"],"lang":["T0(CHN_ENG: 中英混合; ENG: 英语; KOR: 韩语; JAP: 日语; CHT: 繁体中文; LAT: 拉丁语; ARA: 阿拉伯语)",0,null,"待识别内容的语言。表格识别仅支持中英混合和英文"],"offlineMode":["T9(Auto: 自动; OnlineOnly: 仅使用在线服务; OfflineOnly: 仅使用离线引擎)",0,"Auto","是否使用离线引擎。自动：安装离线引擎时使用离线，否则使用在线"],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","操作是否成功"],"content":["T0","合并在一起的的文本内容"],"textList":["T4","OCR识别结果，列表格式，每行一项"],"rawData":["T0","API接口返回的完整内容"],"rawObject":["T98","返回结果的JObject对象"]}
  "sys:MsgBox":
    - "弹窗提示或确认"
    - "msgbox"
    - "弹窗显示提示或确认对话框，这个对话框会占用焦点，并且会在手动关闭之前一直显示在屏幕上。动作也会停留在这个步骤，等待关闭后再继续执行。标准模式：类似于windows内置弹窗，支持固定图标和按钮组合；自定义模式：可自定义图标和按钮，显示内容比较灵活。"
    - {"operation":["T9(default: 标准; custom: 自定义)",0,"default",null],"message":["T0",1,"Hello.","弹窗显示的消息内容。“自定义”模式时，也支持“MD:Markdown内容”"],"title":["T0",1,"Quicker","消息窗口标题。留空时自动使用动作名称"],"icon":["T9(: 无; Information: 信息; Question: 疑问; Warning: 警告; Error: 错误)",1,"Asterisk","消息窗口图标"],"customIcon":["T0",1,"Information","消息窗口图标"],"buttons":["T9",1,"OK","消息窗口图标"],"customButtons":["T0",1,"[fa:Regular_Check:#4caf50]是(_Y)|Yes [fa:Regular_Times:#dc3545]否(_N)|No [fa:Light_Undo:#444444]取消(_C)|Cancel","每行定义一个按钮，格式为 “文本” 或 “[图标]显示文本(提示内容)|值”"],"defaultButton":["T0",1,"Yes","指定默认按钮的值。默认按钮以高亮颜色显示，可直接回车选择"],"restoreFocus":["T2",0,"True","关闭弹窗后，是否将焦点还原到之前的活动窗口"]}
    - {"result":["T0","点击的按钮，标准模式下结果可能为OK,Cancel,Yes,No，自定义模式下为按钮的值"],"okOrYes":["T2","选择的按钮是否为“确定”或“是”"]}
  "sys:randomNum":
    - "生成随机数"
    - "randomnum"
    - "生成随机数"
    - {"min":["T12",1,"0","随机数范围的最小值（结果大于或等于此值）"],"max":["T12",1,"100","随机数范围的最大值（结果小于此值）"]}
    - {"output":["T12","生成的随机数"]}
  "sys:excelObjects":
    - "Excel对象操作"
    - "excelobjects"
    - "操作Excel的某个对象"
    - {"operation":["T9(ApplicationInfo: 获取当前Excel应用信息; OpenFile: 工作簿: 打开工作簿; SaveWorkbook: 工作簿: 保存工作簿; CloseWorkbook: 工作簿: 关闭工作簿; CreateWorkbook: 工作簿: 创建工作簿; SelectWorksheet: 工作表：选择工作表)",1,null,"操作类型"],"path":["T0",0,null,"完整路径。创建工作簿时，用于指定模板文件"],"workbook":["T98",0,null,"根据具体操作，可用参数不同。请参考文档"],"params":["T0",0,null,"根据具体操作，可用参数不同。请参考文档"],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","操作是否成功"],"activeWorkbook":["T98","ActiveWorkbook"],"activeSheet":["T98","ActiveSheet"],"worksheetNames":["T4","Worksheets"],"worksheets":["T98","Worksheets"],"workbookPath":["T0","Worksheets"],"application":["T98","Application对象的引用"]}
  "sys:excelRange":
    - "Excel区域操作"
    - "excelrange"
    - "操作Excel的某个区域或单元格，只能操作通过Quicker打开的excel工作簿"
    - {"range":["T98",0,null,"可以输入区域变量、留空(表示当前选择区域）、used(表示当前工作表的使用区域)或区域范围如A1:E9等，请参考文档"],"subRange":["T9(FullArea: 整个区域; FirstRow: 区域内的第一行; FirstColumn: 区域内的第一列; LastRow: 区域内最后一行; LastColumn: 区域内最后一列; ActiveCell: 活动单元格; EntireRow: 整行(包含区域外); EntireColumn: 整列(包含区域外); Rows: 所有行(区域范围内); Columns: 所有列(区域范围内))",1,"FullArea","根据需要，将要操作的目标限定为一个子区域"],"operation":["T9(SetValue: 设置值; SetFormula: 设置公式; SetNumberFormat: 设置数值格式; SetCellSize: 行高,列宽; SetStyle: 设置格式; CallMethod: 调用方法; Replace: 替换内容; GetRangeInfo: 获取区域信息)",1,"SetValue","操作类型"],"value":["T99",0,null,"要设置的内容"],"cellSize":["T99",0,null,"-表示不改变，auto表示自动，数字表示具体值。如auto,auto表示自适应高度和宽度"],"style":["T0",0,null,"要设置的格式内容。每行一个格式设置，请参考模块文档了解详细参数设置"],"methods":["T0",0,null,"要调用的方法，每行一个。格式请参考文档"],"replaceWhat":["T0",1,null,"要替换的内容"],"replaceTo":["T0",1,null,"替换成的内容"],"replaceEscapeWhat":["T2",0,"False","替换“查找内容”中的转义字符（\\r,\\n,\\t）"],"replaceEscapeTo":["T2",0,"True","替换“替换为”中的转义字符（\\r,\\n,\\t）"],"replaceMatchCase":["T2",0,"False",null],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","操作是否成功"],"value":["T99","单元格的值"],"text":["T0","单元格的显示文本"],"formula":["T0","单元格的公式值"],"numberFormat":["T0","单元格数值格式值"],"address":["T0","区域位置范围"],"column":["T12","左上角单元格从1开始的列数"],"row":["T12","左上角单元格从1开始的行数"],"colNum":["T12","区域包含的列数"],"rowNum":["T12","区域包含的行数"],"style":["T0","单元格的格式"],"range":["T98","Range对象"],"sheet":["T98","WorkSheet对象"]}
  "sys:imeControl":
    - "输入法状态"
    - "imecontrol"
    - "获取或更改当前的输入法中英文状态，避免在发送热键时受影响。"
    - {"operation":["T9(ENABLE: 切换为中文; DISABLE: 切换为英文; RESTORE: 恢复; GET_STATE: 是否为中文状态？)",1,"GET_STATE","要执行的操作。所有操作仅在输入法启用的情况下有效"]}
    - {"isEnabled":["T2",null]}
  "sys:csscript":
    - "运行C#代码"
    - "csscript"
    - "执行C#代码片段。代码中应包含主函数Exec(stepContext)，请参考文档说明。"
    - {"mode":["T9(normal_roslyn: 普通模式v2 (Roslyn); normal: 普通模式v1 (CodeDOM); low_permission_roslyn: 低权限模式v2 (Roslyn); low_permission: 低权限模式v1 (CodeDOM); generate_assembly: 生成程序集)",1,"normal","普通模式：在Quicker进程中执行；低权限模式：在单独的进程中执行，可用于COM操作"],"script":["T0",1,"//.cs 文件类型，便于外部编辑时使用<br>// 引用必要的命名空间<br>using System.Windows.Forms;<br><br>// Quicker将会调用的函数。可以根据需要修改返回值类型。<br>public static void Exec(Quicker.Public.IStepContext context)<br>{<br> //var oldValue = context.GetVarValue(\"varName\"); // 读取动作里的变量值<br> //MessageBox.Show(oldValue as string);<br> //context.SetVarValue(\"varName\", \"从脚本输出的内容。\"); // 向变量里输出值<br> MessageBox.Show(\"Hello World!\");<br>}<br> | True |<br>| scriptForLp | 脚本内容 | 要运行的脚本内容 | (0)字符串-Text | //.cs 文件类型，便于外部编辑时使用<br>// 引用必要的命名空间<br>using System.Windows.Forms;<br><br>// Quicker将会调用的函数<br>public static string Exec(string paramValue)<br>{<br> System.Windows.Forms.MessageBox.Show(\"Hello World!\");<br> return \"Hello World!\";<br>}<br> | True |<br>| scriptForAssembly | 脚本内容 | 要运行的脚本内容 | (0)字符串-Text | //.cs 文件类型，便于外部编辑时使用<br>// 引用必要的命名空间<br>using System.Windows.Forms;<br><br>namespace MyNamespace<br>{<br> // Quicker将会调用的函数<br> public static class MyClass<br> {<br> public static string Exec(string paramValue)<br> {<br> System.Windows.Forms.MessageBox.Show(\"Hello World!\");<br> return \"Hello World!\";<br> }<br> }<br>}<br>","要运行的脚本内容"],"paramValue":["T0",1,null,"传递给Exec的参数"],"reference":["T0",0,null,"要引用的DLL文件，每行一个"],"waitResp":["T2",0,"True","是否等待脚本返回结果"],"runOnUiThread":["T9",0,"auto","是否在界面线程上运行代码。如果在脚本中使用了wpf窗口，请选中此项"],"enableCache":["T2",0,"False","是否使用缓存的程序集"],"stopIfFail":["T2",0,"True","失败后是否停止动作"],"waitMs":["T1",1,"10000","最长的等待返回结果的，毫秒数"]}
    - {"isSuccess":["T2","操作是否成功"],"resp":["T0","脚本执行返回的结果文本"],"rtn":["T0","Exec方法的返回值"],"rtnAssembly":["T98","生成的Assembly对象（已经加载）"],"assemblyPath":["T0","生成的Assembly路径"]}
  "sys:jsscript":
    - "运行Javascript代码"
    - "jsscript"
    - "执行Js代码片段。代码中应包含主函数exec()，请参考文档。"
    - {"script":["T0",1,"//.js 主函数 exec()<br>function exec(){<br> var localName = quickerGetVar('text'); // 读取text变量值, (text 是动作里的变量)<br> quickerSetVar<br>'text', 'Hello, ' + localName ); //输出修改后的值到text变量中。<br> return 0; //返回0表示成功。返回其他数字表示失败。<br>}<br>","要运行的脚本内容"],"allClr":["T2",0,"False","是否需要在js代码中访问.Net程序集"],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","操作是否成功"],"return":["T12","脚本代码返回的数字值"]}
  "sys:pythonscript":
    - "运行Python代码"
    - "pythonscript"
    - "执行Python代码片段。"
    - {"script":["T0",1,"##.py <br>quicker.context.SetVarValue<br>'text', 'hello world')<br>","要运行的脚本内容"],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","操作是否成功"]}
  "sys:waitKeyboard":
    - "等待按键"
    - "waitkeyboard"
    - "等待用户按下某个按键"
    - {"operation":["T9",0,"waitKeyDown",null],"waitingKeys":["T0",0,null,"，留空表示任意键盘按键。格式请参考文档"],"modifierKeys":["T0",0,null,"逗号分隔的ctrl,shift,alt,win组合。仅用于等待组合快捷键。修饰键不会被拦截"],"maxWaitSeconds":["T1",1,"0","0为永久超时超过等待时间，则结束等待"],"filterEvent":["T2",0,"True","避免按键输入到窗口中 (仅对键盘按键有效)"],"waitKeyUp":["T2",0,"False","等待按键抬起后再返回 (仅对键盘按键有效)"],"ignoreSimulated":["T2",0,"False","是否忽略（不检测）模拟的按键消息"],"help":["T0",0,"请按键...","等待按键时显示的提示文字"],"fontfamily":["T0",0,null,"设置字体名称。如有多个字体，使用逗号分隔"],"winLocation":["T9",0,"TopCenter","在哪里显示提示窗口"],"mouseThrough":["T2",0,"True","鼠标是否可以穿透提示窗口点击下面的内容"],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","步骤执行是否成功"],"keyCode":["T0","按键名，具体请参考模块文档"],"keyValue":["T12","按键数值，具体请参考模块文档"],"holdTimeMs":["T12","按下保持时间，单位毫秒。仅支持键盘按键"]}
  "sys:flauiautomation":
    - "窗口界面控制(FlaUI)"
    - "uiautomation"
    - "触发Windows窗口的菜单/按钮等控件(通过FlaUI库实现)。"
    - {"type":["T9(TriggerMenu: 触发窗口菜单; TriggerControl: 触发窗口控件; GetControlInfo: 获取窗口控件信息; GetCursorPointControlInfo: 获取鼠标指针位置控件信息; GetControlInfoByPosition: 获取指定位置控件信息; GetFocusedControlInfo: 获取焦点控件信息)",0,"TriggerMenu","操作类型。按下和抬起需要配对使用"],"window":["T0",0,null,"要操作哪个窗口的控件。不填写=使用前台窗口；或窗口句柄数字"],"menuPath":["T0",0,null,"菜单的展开路径。每行写一个级别的菜单名（需完全匹配）"],"expandDelay":["T12",0,"200","等待下级菜单展开的时间(ms)"],"control":["T0",0,null,"控件的XPath或Name。XPath以/开始"],"controlType":["T9",0,"0","当有多个名称相同但类型不同的控件时区分"],"controlOperation":["T9(Auto: 自动; Invoke: 调用(按钮、菜单项等); LeftClick: 鼠标左键单击; MiddleClick: 鼠标中键单击; RightClick: 鼠标右键单击; LeftDoubleClick: 鼠标左键双击; Select: 单选：选择(单选框、标签页等); AddToSelection: 多选：添加到多选(多选列表等); RemoveFromSelection: 多选：从多选中移除(多选列表); ToggleItemSelection: 多选：切换选中状态; Expand: 展开折叠：展开(菜单等); Collapse: 展开折叠：折叠(菜单等); ToggleExpandCollapse: 展开折叠：切换展开折叠(菜单等); Toggle: 切换：切换(检查框等); ToggleOn: 切换：开(检查框等); ToggleOff: 切换：关(检查框等); SetValue: 设置值)",0,"Auto","对控件执行的操作"],"value":["T0",0,null,"仅用于 “设置值” 操作"],"pointLocation":["T0",0,null,"指定要检查的控件的屏幕坐标位置，格式为“x,y”"],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","操作是否成功"],"value":["T0","控件的值"],"controlText":["T0","获取控件上的文本。根据控件不同，可能从Value、Text、Name等信息获取"],"rect":["T0","控件坐标位置"],"controlName":["T0",null],"controlType":["T0",null],"controlXPath":["T0",null],"controlTypeId":["T12",null],"controlInfo":["T10",null],"controlIsEnabled":["T2","控件未处于禁用状态"],"controlIsVisible":["T2","控件是否在屏幕上"],"element":["T98","返回控件的AutomationElement对象"]}
  "sys:keyoperation":
    - "按键操作"
    - "keyoperation"
    - "单个键盘按键的操作控制或状态获取"
    - {"type":["T9(get_key_state: 获取按键状态; key_down: 按下按键; key_up: 抬起按键; key_keydown_v1: 按下Quicker虚拟键V1; key_keyup_v1: 抬起Quicker虚拟键V1)",0,"get_key_state","操作类型。按下和抬起需要配对使用"],"key":["T0",0,null,"要操作或检查状态的按键(单个)。可以为键值或键名，具体请参考文档"],"getRealMouseState":["T2",0,"False",null],"keepMs":["T12",0,"1000","保持此虚拟键按下的时间（毫秒数），之后会自动抬起"]}
    - {"isDown":["T2","此按键是否为按下状态"],"isToggled":["T2","此按键是否为锁定状态，仅对CapsLock、NumLock等按键有效"]}
  "sys:uiautomation":
    - "窗口界面控制"
    - "uiautomation"
    - "触发Windows窗口的菜单/按钮等控件。"
    - {"type":["T9(TriggerMenu: 触发窗口菜单; TriggerControl: 触发窗口控件; GetControlInfo: 获取窗口控件信息; GetCursorPointControlInfo: 获取鼠标指针位置控件信息; GetFocusedControlInfo: 获取焦点控件信息; GetControlInfoByPosition: 获取指定位置控件信息; UpdateSaveAsDialogPath)",0,"TriggerMenu","操作类型。按下和抬起需要配对使用"],"window":["T0",0,null,"要操作哪个窗口的控件。不填写=使用前台窗口；或窗口句柄数字"],"menuPath":["T0",0,null,"菜单的展开路径。每行写一个级别的菜单名（需完全匹配）"],"expandDelay":["T12",0,"200","等待下级菜单展开的时间(ms)"],"control":["T0",0,null,"控件名，请确保唯一性"],"controlType":["T9",0,"0","当有多个名称相同但类型不同的控件时区分"],"controlOperation":["T9(Auto: 自动; Invoke: 调用(按钮、菜单项等); LeftClick: 鼠标左键单击; MiddleClick: 鼠标中键单击; RightClick: 鼠标右键单击; LeftDoubleClick: 鼠标左键双击; Select: 单选：选择(单选框、标签页等); AddToSelection: 多选：添加到多选(多选列表等); RemoveFromSelection: 多选：从多选中移除(多选列表); ToggleItemSelection: 多选：切换选中状态; Expand: 展开折叠：展开(菜单等); Collapse: 展开折叠：折叠(菜单等); ToggleExpandCollapse: 展开折叠：切换展开折叠(菜单等); Toggle: 切换：切换(检查框等); ToggleOn: 切换：开(检查框等); ToggleOff: 切换：关(检查框等); SetValue: 设置值)",0,"Auto","对控件执行的操作"],"value":["T0",0,null,"仅用于 “设置值” 操作"],"path":["T0",0,null,"要更新的路径"],"autoCreateDir":["T9(no: 不自动创建; auto: 自动创建：自动(根据后缀自动判断路径为文件还是文件夹路径); asFilePath: 自动创建：给定文件路径; asFolderPath: 自动创建：给定文件夹路径)",0,"no","如果目录不存在则自动创建"],"pointLocation":["T0",0,null,"指定要检查的控件的屏幕坐标位置，格式为“x,y”"],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","操作是否成功"],"value":["T0","控件的值"],"controlText":["T0","获取控件上的文本。根据控件不同，可能从Value、Text、Name等信息获取"],"rect":["T0","控件坐标位置"],"controlName":["T0",null],"controlType":["T0",null],"controlIsEnabled":["T2","控件未处于禁用状态"],"controlIsVisible":["T2","控件是否在屏幕上"],"controlNativeWindowHandle":["T12","控件的原始窗口句柄(NativeWindowHandle)"],"controlTypeId":["T12",null]}
  "sys:charInfo":
    - "获取字符信息"
    - "charInfo"
    - "获取字符信息"
    - {"char":["T0",1,"中","要获取编码的字符，如果是多个字符，则取第一个"]}
    - {"unicodeNum":["T12","字符的Unicode编码数字"],"unicodeHex":["T0","字符的Unicode编码数字的十六进制，如“中”的Unicode编码十六进制为“4E2D”"],"pinyinFirstChar":["T0","字母的拼音首字母(仅第一个常用读音)"],"pinyin":["T0","字母的拼音(多音字只输出第一个常用读音)"],"pinyinFirstCharAll":["T0","字母的拼音首字母(多音字输出所有读音)"],"pinyinAll":["T0","字母的拼音(多音字输出所有读音，空格分隔)"]}
  "sys:formatString":
    - "组合成文本"
    - "formatstring"
    - "将（多个）变量组合成一段文本。"
    - {"formatString":["T0",1,"{0}","使用C#的String.Format语法"],"p0":["T99",0,null,"第 0 个参数"],"p1":["T99",0,null,"第 1 个参数"],"p2":["T99",0,null,"第 2 个参数"],"p3":["T99",0,null,"第 3 个参数"],"p4":["T99",0,null,"第 4 个参数"]}
    - {"output":["T0","生成的文本内容"]}
  "sys:htmlExtract":
    - "提取HTML内容"
    - "htmlextract"
    - "从HTML代码中提取内容"
    - {"operation":["T9(extractText: 读取文本内容; extractText: 读取表格内容)",0,"extractText",null],"source":["T0(auto: 自动检测 (加载两次); gb2312: GB2312编码; utf-8: UTF8编码)",1,null,"原始HTML内容，或网址，或根节点对象"],"encoding":["T0",0,null,"通过网址加载内容时，使用指定的编码。留空时默认为UTF8"],"xpath":["T0",1,null,"内容的XPath，详细说明请参考文档"],"selectTarget":["T9(single: 第一个符合条件的节点; all: 所有符合条件的节点)",0,"single","提取单个节点还是符合条件的所有节点"],"returnType":["T9(InnerHtml: innerHtml 内部HTML; InnerText: innerText 内部文本; OuterHtml: outerHTML 节点全部HTML; Attribute: Attribute 节点的某个属性; Node: 节点对象)",0,"InnerHtml","要提取的节点信息"],"attribute":["T0",0,null,"仅在提取节点属性时有效。指定属性的名称"],"writeToSheet":["T98",0,null,"将提取到的表格内容写入工作表对象中"],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","步骤执行是否成功"],"value":["T99","提取的内容。请确保结果类型和变量类型匹配"],"rootNode":["T99","整个HTML源内容对应的HtmlNode节点对象，可用于后续处理使用"]}
  "sys:joinList":
    - "列表合并成文本"
    - "joinlist"
    - "将列表拼接为一段文本"
    - {"list":["T4",1,null,"要拼接为文本的列表"],"separator":["T0",1,",","拼接内容时，两项之间的内容"],"escapeSeparator":["T2",0,"False","替换“分隔文本”中的转义字符（\\r,\\n,\\t）"]}
    - {"output":["T0","生成的文本内容"]}
  "sys:jsonExtract":
    - "提取JSON内容"
    - "jsonExtract"
    - "提取Json文本中的信息"
    - {"data":["T0",1,null,"要从中提取内容的Json文本或JToken对象"],"p0":["T0",0,null,null],"p1":["T0",0,null,null],"p2":["T0",0,null,null],"p3":["T0",0,null,null],"p4":["T0",0,null,null],"dateAsString":["T2",0,"False","保留原有数据格式"],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","操作是否没有异常"],"v0":["T99","提取到的内容，和提取路径对应"],"v1":["T99","提取到的内容，和提取路径对应"],"v2":["T99","提取到的内容，和提取路径对应"],"v3":["T99","提取到的内容，和提取路径对应"],"v4":["T99","提取到的内容，和提取路径对应"],"rootToken":["T98","整个输入内容解析后获得的JToken对象。可用于后续使用"]}
  "sys:pathExtraction":
    - "提取文件路径信息/生成路径"
    - "pathExtraction"
    - "从文件路径中提取文件名、文件夹等信息"
    - {"operation":["T9(getInfo: 提取文件路径信息; changeExt: 更改扩展名，其它不变; changeName: 更改文件名(含扩展名)，所在目录不变; changeNameWithoutExt: 更改文件名(不含扩展名和所在目录); changeDir: 更改所在目录，文件名不变; combine: 合并路径 (拼接))",0,"getInfo",null],"path":["T0",1,null,"待处理或拼接的路径"],"newExtension":["T0",1,null,"新的扩展名，如：.png"],"newFileName":["T0",1,null,"新的文件名，如：abcd.png"],"newFileNameWithoutExt":["T0",1,null,"新的文件名(不包含扩展名），如：newfile"],"newDir":["T0",1,null,"目标存储路径，如：d:\\Work\\Test"],"path2":["T0",1,null,null],"path3":["T0",1,null,null],"path4":["T0",1,null,null],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","提取过程是否没有遇到异常"],"resultPath":["T0","生成的结果路径"],"name":["T0","去除路径的文件名"],"nameNoExt":["T0","去除扩展名的文件名"],"ext":["T0","文件的扩展名"],"path":["T0","父目录路径"]}
  "sys:regexExtract":
    - "正则提取"
    - "regexextract"
    - "使用正则表达式提取指定内容"
    - {"getGroup":["T9(0: 各匹配项的值; 1: 第一个匹配项的组; 2: 各匹配项的组)",1,"0","输出的内容根据提取内容有所不同，请参考模块文档"],"data":["T0",1,null,"要提取内容的文本"],"pattern":["T0",1,null,"用于提取内容的正则表达式"],"ignoreCase":["T2",0,"False","不区分英文大小写"],"singleLine":["T2",0,"False","此模式下“.”能匹配任意字符，包括换行符。(否则匹配除了\\n外的任意字符)"],"multiLine":["T2",0,"False","此模式下^和$可以分别匹配行首和行尾。(否则匹配输入内容的开始和结束)"],"rightToLeft":["T2",0,"False","从右向左查找匹配内容"],"stopIfFail":["T2",0,"True","操作失败后，是否停止后续动作的执行"]}
    - {"matches":["T4","返回所有的匹配项"],"match1":["T99","第1个匹配项的值"],"match2":["T99","第2个匹配项的值"],"match3":["T99","第3个匹配项的值"],"match4":["T99","第4个匹配项的值"],"match5":["T99","第5个匹配项的值"],"matchObj":["T98","首个匹配的原始的C#语言Match对象，可以在表达式中使用"],"matchesCollection":["T98","所有匹配的原始Match对象集合(MatchCollection)，可以在表达式中使用"],"isSuccess":["T2","是否匹配成功"]}
  "sys:showText":
    - "文本窗口"
    - "showText"
    - "在独立的窗口中显示文本。"
    - {"type":["T9(NO_WAIT: 显示窗口，不等待关闭(立即开始执行后续的步骤); WAIT: 显示窗口，等待关闭; CLOSE_WINDOW: 关闭窗口; GET_WIN_INFO: 获取窗口信息; APPEND_TEXT: 追加内容; ACTIVATE_WINDOW: 显示和激活窗口; WAIT_CLOSE: 等待窗口关闭; GET_ALL_WINDOWS: 获取所有文本窗口; GET_ACTION_WINDOWS: 获取当前动作创建的所有文本窗口)",0,"NO_WAIT","是否等待窗口关闭后继续"],"text":["T0",1,null,"要显示的文本内容"],"title":["T0",1,"文本窗口","窗口标题文字"],"operations":["T0",1,null,"用于显示在窗口工具栏。每行一个选项，格式为 “文本” 或 “显示文本|值”"],"autoCloseKey":["T0",0,"=","自动更新或关闭之前打开的具有此标识的文本窗口。使用‘=’表示当前动作id"],"winLocation":["T9",0,"CenterScreen","在哪里显示选择窗口"],"winSize":["T0",0,null,"设置选择窗口的尺寸，格式为：宽度,高度。支持逻辑像素数值或屏幕宽高百分比，详情请参考模块文档。 “窗口位置” 类型为 “自定义位置” 时用于指定显示位置，格式为：left,top,right,bottom"],"fontsize":["T1",1,"14","默认的字体大小"],"fontfamily":["T0",0,null,"设置字体名称。如有多个字体，使用逗号分隔"],"bgColor":["T0",0,null,"格式为#RRGGBB"],"textColor":["T0",0,null,"格式为#RRGGBB"],"highlight":["T9",0,null,null],"autoSaveToState":["T0",0,null,"指定状态Key。文本内容将自动保存到状态中"],"topMost":["T2",0,"False",null],"enableEscClose":["T2",0,"True",null],"closeWhenLostFocus":["T2",0,"False",null],"showLineNum":["T2",0,"True",null],"autoWrap":["T2",0,"True",null],"showBuildInToolbar":["T2",0,"True",null],"copyWholeLine":["T2",0,"False",null],"caretPosition":["T12",1,"0","0表示最前面，-1表示最后面，其它数字表示某个具体字符位置"],"advancedSettings":["T0",0,null,"请参考模块文档"],"updateIfExists":["T2",0,"False",null],"stopIfFail":["T2",0,"True","失败后是否停止动作"]}
    - {"isSuccess":["T2","操作是否成功"],"isWindowExists":["T2",null],"selectedOperation":["T0","选择的后续操作项"],"resultText":["T0","文本框内的所有文本"],"selectedText":["T0","文本框内选中的文本"],"windowHandle":["T12",null],"windowPosition":["T0","窗口的最终显示位置"],"allWindows":["T10","词典类型，key为窗口的句柄，value为窗口的标识。获取全部窗口时，为了安全，仅限自己开发的动作使用"]}
  "sys:splitString":
    - "拆分文本为列表"
    - "splitstring"
    - "将文本拆分为列表"
    - {"data":["T0",1,null,"要拆分为列表的文本"],"separator":["T0",1,",","拆分分隔符"],"escapeSeparator":["T2",0,"False","转义分隔符\\r\\n\\t字符"],"multiSeparator":["T2",0,"False","每行指定一个"],"removeEmpty":["T2",1,"True","滤除没有内容的文本"]}
    - {"output":["T4","生成的文本内容"]}
  "sys:strReplace":
    - "替换文本"
    - "strReplace"
    - "替换文本中的指定内容"
    - {"type":["T9(single: 普通(替换一种内容); batch: 批量(替换多种内容))",1,"single",null],"input":["T0",1,null,"要提取内容的文本"],"batchReplaceData":["T0",1,null,"每行一对查找和替换内容，中间使用|||或|分隔。例如将a替换成A，写作:a|A 或 a|||A"],"old":["T0",1,null,"要替换的内容"],"new":["T0",1,null,"替换成的内容"],"escapeOld":["T2",0,"False","替换“查找内容”中的转义字符（\\r,\\n,\\t）"],"replaceEscapes":["T2",0,"True","替换“替换为”中的转义字符（\\r,\\n,\\t）"],"useRegex":["T2",0,"False",null],"ignoreCase":["T2",0,"False",null],"singleLine":["T2",0,"True","此模式下“.”能匹配任意字符，包括换行符。(否则匹配除了\\n外的任意字符)"],"multiLine":["T2",0,"False","此模式下^和$可以分别匹配行首和行尾。(否则匹配输入内容的开始和结束)"]}
    - {"output":["T0","替换后的文本"]}
  "sys:textCounter":
    - "字数统计"
    - "textcounter"
    - "统计文本行数、字符数等"
    - {"content":["T0",1,null,"要统计的内容"]}
    - {"line":["T12",null],"char":["T12",null],"visableChar":["T12",null],"cnChar":["T12",null]}
  "sys:officehelper":
    - "Office软件辅助"
    - "officehelper"
    - "辅助控制Office软件"
    - {"operation":["T9(execVBA: 执行VBA宏代码; setFormats: 设置格式/对象属性赋值; executeMsoCommand: 执行界面命令; getProgId: 获取ProgId)",1,"execVBA",null],"appType":["T9(word_wps: Word或WPS文字(根据前台进程自动识别); word; wps: wps文字; excel_et: EXCEL或WPS表格(根据前台进程自动识别); excel; et: wps表格; powerpoint_wpp: PowerPoint或WPS幻灯片(根据前台进程自动识别); powerpoint; wpp)",1,"word_wps",null],"code":["T0",0,"Sub Hello() MsgBox \"Hello World\" End Sub","宏的名称，或VBA代码（将执行第一个找到的Sub或Function）"],"waitResp":["数字(小数)-Number",0,"10000","最长的等待返回结果的，毫秒数"],"command":["T0",0,null,"界面按钮所对应的命令ID"],"formats":["T0",0,null,null]}
    - {"isSuccess":["T2","操作是否成功"],"progId":["T0","获取程序的Progld，可用于在C#里得到对应的Application对象"]}
  "sys:excelreadwrite":
    - "Excel文件读写"
    - "excelreadwrite"
    - "读取Excel文件内容或写入Excel文件"
    - {"operation":["T9(load: 打开Workbook; newWorkbook: 创建Workbook; save: 保存Workbook; getSheet: 获取Sheet; createSheet: 创建Sheet; getRow: 获取行; getCellByValue: 查找单元格(根据值); getCell: 读取单元格; setCell: 写入单元格; writeData: 写入多行数据; mergeCells: 合并单元格; freezePane: 冻结窗格; autoFilter: 自动筛选; setStyle: 设置区域单元格样式; readData: 批量提取数据; batchReplace: 批量模板替换)",1,null,null],"filePath":["T0",0,null,"要打开或写入的Excel文件路径"],"fileType":["T9(XSSF: .xlsx 2007版Excel; HSSF: xls 2003版Excel)",0,null,null],"workbook":["T99",0,null,"需要操作的工作簿对象"],"sheetIndex":["T0",0,null,"以0开始计算的序号或名称"],"sheetName":["T0",0,null,"要打开的工作表名称"],"rowIndex":["T12",0,"0","以0开始计算的序号"],"cellValue":["T0",0,null,"设置单元格的值"],"worksheet":["T99",0,null,"需要操作的工作表对象"],"cellAddress":["T0",0,null,"类似于\"D5\"这样的单元格位置名称。或在下方使用行序号和单元格序号指定（两种二选一）"],"cellIndex":["T12",0,"0","单元格在所在行里的序号，从0开始"],"cellType":["T9(\"\": 自动; String: 文本; Numeric: 数字或日期; Boolean: 布尔; Formula: 公式; Blank: 空白)",0,null,null],"dataFormat":["T0",0,null,"设置单元格的DataFormat"],"cellLink":["T0",0,null,"可以为网址、邮件地址（mailto:who@domain.com)工作表名称、文件路径"],"sourceData":["T99",0,null,"可以为工作表对象、表格变量或对象列表"],"columnMapping":["T0",0,null,"复制哪些字段信息到目标工作表。请参考文档了解使用方法"],"writeTitleRow":["T2",0,"True","是否输出标题行"],"cellRange":["T0",0,null,"类似于\"A1:B5\"格式，或\"开始行号,结束行号,开始列号,结束列号方式(从0开始的序号)"],"styleData":["T0",0,null,null],"readDataMap":["T0",0,null,"每行一条规则：“字段:[工作表序号或名称]单元格地址”"],"replaceDict":["T10",0,null,"词典格式数据。键为要查找的字段，值为要填充的内容"],"replacePrefixSuffix":["T0",0,"{{\\r\\n}}","第一行写前缀，第二行写后缀。“前缀+字段名+后缀“组成要查找和替换的目标，如”{{姓名}}”"]}
    - {"isSuccess":["T2","操作是否成功"],"workbook":["T99","用于在后续步骤中继续操作工作簿"],"numberOfSheets":["T12","工作簿中的工作表个数"],"worksheetNameList":["T4","工作簿中的工作表名列表"],"sheet":["T99","返回指定的工作表。加载文件时返回工作簿中的第一个工作表对象"],"firstRow":["T12","工作表首行序号"],"lastRow":["T12","工作表有内容的最后一行序号"],"names":["T0","工作簿中定义的名称数据，返回json格式"],"firstCellNum":["T12","工作表有内容的最后一行序号"],"lastCellNum":["T12","一行的最后一个单元格的序号"],"cellAddress":["T99","查找到的单元格地址"],"hasValue":["T2","单元格是否有值"],"cellValue":["T0","单元格的值"],"cellTextValue":["T0","文本格式的单元格内容"],"cellType":["T0","单元格的类型"],"cellFormula":["T0","单元格的公式值"],"cellDataFormatString":["T0","数据格式的字符串表示"],"dictData":["T10","从工作薄加载的数据"]}
  "sys:shelloperation":
    - "Shell文件操作"
    - "shelloperation"
    - "针对文件的Windows Shell相关操作"
    - {"operation":["T9(getverb: 获取文件的可用动词列表(verb); )",1,"getverb: 获取文件的可用动词列表（verb）; execverb: 对文件执行动词（verb）; gettitles: 获取文件的可用菜单标题列表; execbytitle: 对文件执行菜单（指定菜单标题）; showmenu: 显示系统上下文菜单",null],"pathOrExt":["T0",0,".txt","需要获取可用动词的文件类型，可使用扩展名如.txt或提供完整文件名"],"pathList":["T4",0,null,"要操作文件的完整路径的列表。每个文件将会被依次调用"],"verb":["T0",0,null,"Shell操作动词，需要在当前电脑上支持才能正常运行"],"title":["T0",0,null,"菜单上的标题文字，需要准确匹配"]}
    - {"isSuccess":["T2","操作是否成功"],"verbs":["T4","每项格式为：描述文字|动词"],"titles":["T4",null]}
  "sys:tableoperation":
    - "表格数据操作"
    - "tableoperation"
    - "表格变量的相关处理操作"
    - {"table":["T13",1,null,"要操作的表格变量"]}
    - {"isSuccess":["T2","操作是否成功"],"rows":["T99","符合条件的行的数组 |"],"columns":["T99","表格的列的信息列表（DataTable.Columns） |"],"rowCount":["T12","表格内的数据行数"],"firstRow":["T99","第一个符合条件的行或新添加的行，可输出为词典对象"],"affectedRowCount":["T0","更新或删除、筛选的行数"],"isConfirmed":["T2","是否点击了确认按钮"],"selectedRows":["T99","选择的所有行的列表"]}
  "sys:customwindow":
    - "自定义窗口"
    - "customwindow"
    - "创建和显示自定义窗口"
    - {}
    - {"isSuccess":["T2","操作是否成功"],"result":["T0","通过close:result返回的结果"],"windowLocation":["T0",null],"windowHandle":["T12",null],"windowList":["T99","IList<Window>对象"]}
  "sys:custompanel":
    - "自定义操作窗"
    - "custompanel"
    - "自定义悬浮操作窗口，点击后直接执行操作，不隐藏。"
    - {}
    - {"isSuccess":["T2","操作是否成功"],"winHandle":["T12","操作窗的窗口句柄"],"selectedItemData":["T0","选择的操作项的data属性数据"],"selectedItem":["T99","选择的操作项的CommonOperationltem对象"],"currentGroup":["T99","当使用标签分组显示时，关闭窗口时所停留的标签分组名称"],"buttonItemData":["T0","点击的是按钮的菜单时，所对应按钮的操作项Data数据"],"buttonItem":["T99","点击的是按钮的菜单时，所对应按钮的CommonOperationltem对象"],"isWindowVisible":["T2","可能会因为关联进程而隐藏"],"isWindowExpanded":["T2",null]}
  "sys:dboperation":
    - "数据库查询"
    - "dboperation"
    - "对数据库执行SQL语句并返回结果"
    - {}
    - {"isSuccess":["T2","操作是否成功"],"dataTableResult":["T13","获取表格类型的行结果"],"listResult":["T99","获得动态对象列表类型的结果"],"firstItem":["T99","如果只需要返回结果的第一行，可以使用此项输出，支持词典或任意对象。没有结果时返回null"],"rowCount":["T12",null],"rowsAffected":["T12",null],"scalarResult":["T0",null]}
  "sys:inputScript":
    - "多步骤输入"
    - "inputscript"
    - "多步骤键盘组合输入 <details> <summary>详细说明</summary> ``` 每行一个步骤指令。 //开始的行作为注释。 指令的格式为：命令:参数。 特殊情况下无法分行填写时，也可以写在一行，并使用;;表示换行。 支持的命令类型如下： 键盘命令 input 模拟键入纯文本（不受输入法影响）。如：input:hello world，你好 世界。 input2 模拟键入纯文本，支持使用转义字符。 如\\t内容\\r\\n换行中的\\t表示tab，\\r\\n表示换行。 sendkeys 使用模拟按键B的语法键入内容。如： sendkeys:{LEFT 2} 发送2个向左的方向键用于移动光标位置。 delay 等待时间（毫秒数）如：delay:1000 等待1秒钟 paste 粘贴内容，如：paste:hello world 将hello world写入剪贴板后模拟Ctrl+V进行粘贴。 keydown 按下按键：如：keydown:F1 按下F1键，或keydown:#175按下音量增加键（#+键值数字）。 注意应该在后续步骤中使用keyup命令抬起按键。键名可参考：微软官方文档。 keyup 抬起按键，格式同上，如：keyup:F1。 keypress 点击（按下并抬起）按键，格式同上。 hotkey 发送组合快捷键。如：hotkey:Ctrl+S ，数字键请使用D+数字表示，如hotkey:Ctrl+Alt+D1。 鼠标命令 moveto 移动鼠标指针到一个绝对坐标。如：moveto:100,200 将鼠标指针移动到 (100,200)位置。1.30.0版本开始支持百分比数值，如：moveto:50%,50%将鼠标移动到主屏幕中心。 move 将鼠标指针移动一定距离（相对于当前位置），参数为“水平方向像素数,垂直方向像素数”。如：move:10,-10 将指针向右和向上分别移动10个像素。 click 点击鼠标某个按键。参数为鼠标按键名，可选：left/right/middle/x1/x2。如：click:left 点击左键。 dbclick 双击鼠标某个按键。参数格式同上。 down 按下某个鼠标按键。参数格式同上。需要特别注意：按下和抬起鼠标按键要完全配对。 up 抬起某个鼠标按键。参数格式同上。 wheel 垂直滚动，单位为clicks（可以理解为“行”）。正值表示向前（远离用户，滚动区域内容向下），负值表示向后（朝向用户，滚动区域内容向上）。 wheeldelta 垂直滚动。单位为1/120 click。更细微的滚动。 hwheel 水平滚动，单位为clicks（可以理解为“行”）。正值表示滚动区域内容向左，负值表示滚动区域内容向右。 hwheeldelta 水平滚动，单位为1/120 click。 组合命令 pastefile 粘贴文件（将文件写入剪贴板后模拟Ctrl+V）。参数为文件完整路径，多个文件使用英文半角分号隔开。如：pastefile:d:\\test.png ， pastefile:d:\\test1.png;d:\\test2.txt pasteimage 粘贴图片（将图片文件读取为图片后写入剪贴板，然后模拟Ctrl+V，注意写入剪贴板的是图片对象而非图片文件）。如：pasteimage:d:\\test.png 只支持单个图片。 ``` </details>"
    - {"data":["T0",1,null,"模拟输入的步骤列表详细格式请参考模块文档"]}
    - {"isSuccess":["T2","操作是否成功"]}
  "sys:showmenu":
    - "显示菜单"
    - "showmenu"
    - "显示一个菜单"
    - {}
    - {"isSuccess":["T2","操作是否成功"],"selectedItemData":["T0","选择的菜单项的data属性数据"],"selectedItem":["T99","选择的菜单项的CommonOperationltem对象"]}
  "sys:fileSystemWatch":
    - "文件系统监控"
    - "filesystemwatch"
    - "监控指定文件夹下文件或目录的变化（创建/删除/变更/重命名）。支持两种工作方式：1）等待事件发生后继续运行动作。2）持续监控，事件发生后调用设定好的子程序。"
    - {}
    - {"isSuccess":["T2","操作是否成功"],"fullPath":["T0","发生变更的文件（夹）路径，或重命名后的新路径"],"changedType":["T0",null],"oldFullPath":["T0","重命名时的原始路径"]}
