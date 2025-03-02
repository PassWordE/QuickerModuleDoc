**Quicker文档**

[TOC]

# Quicker介绍

Quicker是一个Windows上的积木式编程软件，用它编写的程序叫“动作”，它具有诸多模块，每个模块都有自己的功能，通过这些模块的组合，我们可以完成各种各样的功能。

每个模块在动作中可以有自己的变量，通过变量我们可以实现一些动态的效果，模块在动作中我们也叫做“步骤”（Step），一个步骤就是一个模块。

Quicker的动作是用JSON格式编写的，JSON是一种轻量级的数据交换格式，它易于阅读和编写，同时也易于机器解析和生成。

Quicker的动作可以通过API调用，也可以通过快捷键调用。

---

# 模块编写及部分参数说明

**C#代码支持**

Quicker内部使用C#实现，故而原生支持C#代码使用

在任何支持字符串参数输入的模块中，都可以使用C#代码模式或插值模式

> 使用“$$”开头则使用插值模式，插值模式支持变量字符串混杂拼接，被一对花括号{}包裹的是变量，例如：$$今天日期{date}，捡到{money}元

> 使用“$=”开头则使用C#代码模式
> 
> 例子1：$=({mouseX}-100) + "," + ({mouseY}-100) + "," + ({mouseX}+100) + "," + ({mouseY}+100)
> 
> 例子2，IF模块中直接进行逻辑判断：$={money} > 200
> 
> 例子3，使用return返回值：
```
$=
var a = {money}*2.5;
var b = a + 3;
return b;
```

**JSON格式说明**

```json
{
  //使用的变量列表
  "Variables": [
    {
      // 变量名称
      "Key": "text",
      // 变量类型编号，例如0就代表字符串类型
      "Type": 0,
      // 注释
      "Desc": "默认文本变量",
      // 变量初始值
      "DefaultValue": "123",
      // 变量的值是否保存到硬盘中
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      // 变量分组名称（方便阅读）
      "Group": ""
    }
  ],
  //步骤列表
  "Steps": [
    {
      "StepRunnerKey": "sys:getSelectedText",//模块内部名称
      // 输入参数列表
      "InputParams": {
        "其他输入参数名称": {
          "VarKey": null,
          "Value": "UnicodeText"//其他输入参数值
        },
        // 步骤运行失败后是否中止动作
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"// 1：中止；0：不中止
        },
        //···其他输入参数等等
      },
      // 输出参数列表
      "OutputParams": {
        // 步骤运行是否成功，布尔值
        "isSuccess": null,
        // 步骤运行如果出错，返回的出错信息
        "errMessage": null,
        "其他输出参数a": null,// 输出到哪个变量中去，比如"text"(输出到变量的情况下必须包裹在双引号中)，为null则不输出到具体变量中去,
        "其他输出参数b": null,
        //···其他输出参数等等，输出参数和输入参数不一样，它没有“VarKey”，所以参数名称后直接就是值
      },
      "IfSteps": null,
      "ElseSteps": null,
      // 注释
      "Note": "",
      // 步骤是否禁用（被禁用的步骤代码块将不会被运行，类似其他编程语音中的注释）
      "Disabled": false,
      // 步骤块是否收缩起来（仅用于可读性），true收缩代码块，false展开代码块
      "Collapsed": false,
      // 本步骤运行后延迟多少毫秒运行下一个步骤
      "DelayMs": 0
    }
  ],
  // 子程序，忽略即可
  "SubPrograms": []
}
```

**某些参数：WinLocation**

Auto: `系统默认`
WithMouse1: `跟随鼠标（指针周围）`
WithMouse2: `跟随鼠标（指针右下,会偏移）`
CenterScreen: `屏幕中间`
TopLeft: `屏幕左上`
TopCenter: `屏幕中上`
TopRight: `屏幕右上`
BottomLeft: `屏幕左下`
BottomCenter: `屏幕中下`
BottomRight: `屏幕右下`
LeftCenter: `屏幕左中`
RightCenter: `屏幕右中`
FullScreen: `全屏`
Manual: `自定义位置`

***

# 其他示例动作

 <details>
 <summary>合并选择的文本文件到以“合并文本”+时间戳+后缀名的新文件中去，合并完成后提示是否删除原文件</summary>

```json
{
  "Variables": [
    {
      "Key": "files",
      "Type": 4,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "item",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "txt",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "allFilesText",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "filePath",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "时间戳",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "后缀名",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "okOrYes",
      "Type": 2,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "当前删除文件路径",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:getSelectedFiles",
      "InputParams": {
        "operation": {
          "VarKey": null,
          "Value": "getSelection"
        },
        "waitMs": {
          "VarKey": null,
          "Value": "200"
        },
        "sortType": {
          "VarKey": null,
          "Value": "Default"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "files": "files",
        "firstFile": null,
        "fileNames": null,
        "firstFileName": null,
        "fileCount": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:each",
      "InputParams": {
        "input": {
          "VarKey": "files",
          "Value": null
        },
        "useMultiThread": {
          "VarKey": null,
          "Value": "0"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "item": "item",
        "count": null,
        "isSuccess": null,
        "errMessage": null
      },
      "IfSteps": [
        {
          "StepRunnerKey": "sys:readFile",
          "InputParams": {
            "path": {
              "VarKey": "item",
              "Value": null
            },
            "type": {
              "VarKey": null,
              "Value": "text"
            },
            "encoding": {
              "VarKey": null,
              "Value": "auto"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "txt": "txt",
            "isSuccess": null,
            "errMessage": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:assign",
          "InputParams": {
            "input": {
              "VarKey": null,
              "Value": "$={allFilesText}+\"\\n\"+{txt}"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "isSuccess": null,
            "output": "allFilesText",
            "errMessage": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": [],
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:pathExtraction",
      "InputParams": {
        "operation": {
          "VarKey": null,
          "Value": "getInfo"
        },
        "path": {
          "VarKey": null,
          "Value": "$={files}[0]"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "name": null,
        "nameNoExt": null,
        "ext": "后缀名",
        "path": "filePath",
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:getCurrentTime",
      "InputParams": {
        "source": {
          "VarKey": null,
          "Value": "currTime"
        },
        "useUtc": {
          "VarKey": null,
          "Value": "0"
        },
        "addDays": {
          "VarKey": null,
          "Value": "0"
        },
        "addHours": {
          "VarKey": null,
          "Value": "0"
        },
        "addMinutes": {
          "VarKey": null,
          "Value": "0"
        },
        "addSeconds": {
          "VarKey": null,
          "Value": "0"
        },
        "addMonths": {
          "VarKey": null,
          "Value": "0"
        },
        "format": {
          "VarKey": null,
          "Value": "yyyyMMddHHmmss"
        },
        "outputCulture": {
          "VarKey": null,
          "Value": "CURRENT"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "output": null,
        "strValue": "时间戳",
        "timeStamp": null,
        "timeStampMs": null,
        "year": null,
        "month": null,
        "day": null,
        "hour": null,
        "minute": null,
        "second": null,
        "dayOfWeek": null,
        "dayOfYear": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:assign",
      "InputParams": {
        "input": {
          "VarKey": null,
          "Value": "$={filePath}+\"\\\\\"+\"合并文本-\"+{时间戳}+{后缀名}"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "output": "filePath",
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:WriteTextFile",
      "InputParams": {
        "content": {
          "VarKey": "allFilesText",
          "Value": null
        },
        "filePath": {
          "VarKey": "filePath",
          "Value": null
        },
        "encoding": {
          "VarKey": null,
          "Value": "utf-8"
        },
        "addUtf8Bom": {
          "VarKey": null,
          "Value": "0"
        },
        "appendMode": {
          "VarKey": null,
          "Value": "0"
        },
        "addNewLine": {
          "VarKey": null,
          "Value": "1"
        },
        "newLineChars": {
          "VarKey": null,
          "Value": ""
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:notify",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "Success"
        },
        "msg": {
          "VarKey": null,
          "Value": "$$【{filePath}】\r\n\r\n已创建成功！"
        },
        "maxLines": {
          "VarKey": null,
          "Value": "0"
        },
        "style": {
          "VarKey": null,
          "Value": "Style2"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:MsgBox",
      "InputParams": {
        "operation": {
          "VarKey": null,
          "Value": "default"
        },
        "message": {
          "VarKey": null,
          "Value": "是否删除源文件？"
        },
        "title": {
          "VarKey": null,
          "Value": "巴德文件合并"
        },
        "icon": {
          "VarKey": null,
          "Value": "Question"
        },
        "buttons": {
          "VarKey": null,
          "Value": "YesNo"
        },
        "restoreFocus": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "result": null,
        "okOrYes": "okOrYes"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:simpleIf",
      "InputParams": {
        "condition": {
          "VarKey": "okOrYes",
          "Value": null
        }
      },
      "OutputParams": {},
      "IfSteps": [
        {
          "StepRunnerKey": "sys:each",
          "InputParams": {
            "input": {
              "VarKey": "files",
              "Value": null
            },
            "useMultiThread": {
              "VarKey": null,
              "Value": "0"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "item": "当前删除文件路径",
            "count": null,
            "isSuccess": null,
            "errMessage": null
          },
          "IfSteps": [
            {
              "StepRunnerKey": "sys:fileOperation",
              "InputParams": {
                "type": {
                  "VarKey": null,
                  "Value": "deleteFile"
                },
                "path": {
                  "VarKey": "当前删除文件路径",
                  "Value": null
                },
                "stopIfFail": {
                  "VarKey": null,
                  "Value": "1"
                }
              },
              "OutputParams": {
                "isSuccess": null,
                "errMessage": null
              },
              "IfSteps": null,
              "ElseSteps": null,
              "Note": "",
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            }
          ],
          "ElseSteps": [],
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": [],
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
 </details>

---

# 模块介绍

## 1.激活进程主窗口

**功能描述**
> 找到指定进程的主窗口并使其显示在前台。

**官方文档**
> https://getquicker.net/KC/Help/Doc/activateprocessmainwindow

**内部名称**
> sys:activateProcessMainWindow

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| process | 进程名称/pid | 请输入要验证的进程名称或pid。进程名通常是exe的文件名去掉后缀，比如记事本程序的进程名称为notepad。 | (0)字符串-Text |  | True |
| className | 窗口类名 | 选填。未能获取主窗口时（如窗口隐藏），可以尝试根据类名查找窗口，支持正则。 | (0)字符串-Text |  | False |
| windowTitle | 窗口标题 | 选填。未能获取主窗口时，根据窗口标题查找，支持正则。 | (0)字符串-Text |  | False |
| hotkey | 热键 | 选填。软件最小化到托盘时，使用指定的全局热键激活窗口。 | (0)字符串-Text |  | False |
| path | 程序路径 | 选填。如果进程不存在，可以根据此路径启动程序。 | (0)字符串-Text |  | True |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 是否成功激活了进程主窗口 | (2)布尔值-Boolean |
| pid | PID | 进程ID | (12)数字(整数)-Integer |
| mainWinHandle | 主窗口句柄 | 进程的主窗口句柄 | (12)数字(整数)-Integer |
| mainWinTitle | 主窗口标题 |  | (0)字符串-Text |

</details>
<details>
<summary>范例</summary>


**激活{pid}进程的主窗口，未能获取到窗口类名时，查找窗口类名"abcbbc"，或者查找窗口标题"TellMe123"，如果进程不存在，以{path}路径启动程序**
返回值
* 是否成功：{isSuccess}
* PID：{pid}
* 主窗口句柄：{mainWinHandle}
* 主窗口标题：{mainWinTitle}
* 错误信息：{errMessage}

代码
```json
{
  "Variables": [
    {
      "Key": "pid",
      "Type": 12,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "path",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "procId",
      "Type": 12,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "mainWinHandle",
      "Type": 12,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "mainWinTitle",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "errMessage",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "isSuccess",
      "Type": 2,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:activateProcessMainWindow",
      "InputParams": {
        "process": {
          "VarKey": "pid",
          "Value": null
        },
        "className": {
          "VarKey": null,
          "Value": "$=\"abc\" + \"bbc\""
        },
        "windowTitle": {
          "VarKey": null,
          "Value": "$=\r\nvar x = \"TellMe\";\r\nvar b = 123;\r\nreturn x + b;"
        },
        "hotkey": {
          "VarKey": null,
          "Value": ""
        },
        "path": {
          "VarKey": "path",
          "Value": null
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": "isSuccess",
        "pid": "procId",
        "mainWinHandle": "mainWinHandle",
        "mainWinTitle": "mainWinTitle",
        "errMessage": "errMessage"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 2.跳出循环（break）

**功能描述**
> 跳出循环（“每个” 或 “重复” 模块）

**官方文档**
> https://getquicker.net/KC/Help/Doc/break

**内部名称**
> sys:break

<details>
<summary>传入参数</summary>
无
</details>
<details>
<summary>传出参数</summary>
无
</details>
<details>
<summary>范例</summary>

**列表{星期列表}中记载了周一至周日共7个字符串，循环到第4个时（{星期几}是运行序号，序号0时是第一个，{星期几}这个字段做了备注: (循环序号的起始为0，和其他编程语言的for循环一样)）在屏幕下方显示“当前是星期四”，跳出循环（跳出循环的步骤写了注释“跳出当前循环”），然后在屏幕右边显示“程序运行结束”**
```json
{
  "Variables": [
    {
      "Key": "星期列表",
      "Type": 4,
      "Desc": "",
      "DefaultValue": "周一\r\n周二\r\n周三\r\n周四\r\n周五\r\n周六\r\n周日",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "星期几",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "本次循环到第几个",
      "Type": 12,
      "Desc": "循环序号的起始为0，和其他编程语言的for循环一样",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:each",
      "InputParams": {
        "input": {
          "VarKey": "星期列表",
          "Value": null
        },
        "useMultiThread": {
          "VarKey": null,
          "Value": "0"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "item": "星期几",
        "count": "本次循环到第几个",
        "isSuccess": null,
        "errMessage": null
      },
      "IfSteps": [
        {
          "StepRunnerKey": "sys:simpleIf",
          "InputParams": {
            "condition": {
              "VarKey": null,
              "Value": "$={本次循环到第几个}==3"
            }
          },
          "OutputParams": {},
          "IfSteps": [
            {
              "StepRunnerKey": "sys:notify",
              "InputParams": {
                "type": {
                  "VarKey": null,
                  "Value": "Info"
                },
                "msg": {
                  "VarKey": null,
                  "Value": "$=\"当前是\" + {星期几}"
                },
                "maxLines": {
                  "VarKey": null,
                  "Value": "0"
                },
                "style": {
                  "VarKey": null,
                  "Value": "Default"
                },
                "clickAction": {
                  "VarKey": null,
                  "Value": ""
                }
              },
              "OutputParams": {},
              "IfSteps": null,
              "ElseSteps": null,
              "Note": "",
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            },
            {
              "StepRunnerKey": "sys:break",
              "InputParams": {},
              "OutputParams": {},
              "IfSteps": null,
              "ElseSteps": null,
              "Note": "跳出当前循环",
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            }
          ],
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:notify",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "Success"
        },
        "msg": {
          "VarKey": null,
          "Value": "程序运行结束"
        },
        "maxLines": {
          "VarKey": null,
          "Value": "0"
        },
        "style": {
          "VarKey": null,
          "Value": "Style2"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 3.检查路径/获取文件信息

**功能描述**
> 检查指定的文件或文件夹是否存在。

**官方文档**
> https://getquicker.net/KC/Help/Doc/checkPathExists

**内部名称**
> sys:checkPathExists

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| path | 路径 | 文件或文件夹的完整路径。 | (0)字符串-Text |  | True |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isExists | 路径是否存在 |  | (2)布尔值-Boolean |
| isFile | 是否为文件 |  | (2)布尔值-Boolean |
| fileLength | 文件长度 |  | (12)数字(整数)-Integer |
| isFolder | 是否为文件夹 |  | (2)布尔值-Boolean |
| isReadonly | 是否只读 |  | (2)布尔值-Boolean |
| isHidden | 是否隐藏 |  | (2)布尔值-Boolean |
| isSystem | 是否为系统文件 |  | (2)布尔值-Boolean |
| fileCount | 文件夹内文件个数 | 仅对文件夹路径有效，输出时需要耗费一定时间扫描文件夹 | (12)数字(整数)-Integer |
| totalLength | 文件夹大小 | 仅对文件夹路径有效，输出时需要耗费一定时间扫描文件夹 | (12)数字(整数)-Integer |
| createTime | 创建时间 |  | (6)时间日期-DateTime |
| editTime | 更新时间 |  | (6)时间日期-DateTime |
| metaData | 文件扩展信息 | 获取文件的扩展信息，值为词典类型。 | (10)词典-Dict |
| lnkTarget | lnk目标路径 | 快捷方式文件的目标文件 | (0)字符串-Text |
| lnkArguments | lnk命令行参数 | 快捷方式中的命令行参数 | (0)字符串-Text |
| md5hash | MD5 哈希值 | 获取文件的MD5哈希值。仅对文件有效，大文件需要一些时间扫描。 | (0)字符串-Text |
| sha1hash | SHA1 哈希值 | 获取文件的SHA1哈希值。仅对文件有效，大文件需要一些时间扫描。 | (0)字符串-Text |
| sha256hash | SHA256 哈希值 | 获取文件的SHA256哈希值。仅对文件有效，大文件需要一些时间扫描。 | (0)字符串-Text |
| crc32hash | CRC32 哈希值 | 获取文件的CRC32哈希值。仅对文件有效，大文件需要一些时间扫描。 | (0)字符串-Text |

</details>
<details>
<summary>范例</summary>

**获取{folder}\1.txt的文件信息，如果文件长度{fileLength}大于500字节，在屏幕下方显示“文件长度大于500”，否则在屏幕下方显示“文件长度：{fileLength}小于500，md5为：{md5hash}”并结束动作**
```json
{
  "Variables": [
    {
      "Key": "fileLength",
      "Type": 12,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "md5hash",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "folder",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:checkPathExists",
      "InputParams": {
        "path": {
          "VarKey": null,
          "Value": "$${folder}\\1.txt"
        }
      },
      "OutputParams": {
        "isExists": null,
        "isFile": null,
        "fileLength": "fileLength",
        "isFolder": null,
        "isReadonly": null,
        "isHidden": null,
        "isSystem": null,
        "fileCount": null,
        "totalLength": null,
        "createTime": null,
        "editTime": null,
        "metaData": null,
        "lnkTarget": null,
        "lnkArguments": null,
        "md5hash": "md5hash",
        "sha1hash": null,
        "sha256hash": null,
        "crc32hash": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:simpleIf",
      "InputParams": {
        "condition": {
          "VarKey": null,
          "Value": "$={fileLength}<500"
        }
      },
      "OutputParams": {},
      "IfSteps": [
        {
          "StepRunnerKey": "sys:stop",
          "InputParams": {
            "method": {
              "VarKey": null,
              "Value": "default"
            },
            "isError": {
              "VarKey": null,
              "Value": "0"
            },
            "return": {
              "VarKey": null,
              "Value": ""
            },
            "showMessage": {
              "VarKey": null,
              "Value": "$$文件长度：{fileLength}小于500，md5为：{md5hash}"
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:notify",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "Info"
        },
        "msg": {
          "VarKey": null,
          "Value": "文件长度大于500"
        },
        "maxLines": {
          "VarKey": null,
          "Value": "0"
        },
        "style": {
          "VarKey": null,
          "Value": "Default"
        },
        "clickAction": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 4.检查程序已启动/获取进程信息

**功能描述**
> 检查指定的应用程序是否已经启动。

**官方文档**
> https://getquicker.net/KC/Help/Doc/checkprocessexists

**内部名称**
> sys:checkProcessExists

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| process | 进程名称/pid | 请输入要验证的进程名称或id。通常是exe的文件名去掉后缀，比如记事本程序的进程名称为notepad。 | (0)字符串-Text |  | True |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 操作是否成功 | 可能会因为无法访问高权限进程等原因而失败。进程未启动不会导致操作失败。 | (2)布尔值-Boolean |
| isExists | 是否运行 | 指定的进程是否运行。如果已运行，返回True，否则返回False | (2)布尔值-Boolean |
| pid | 进程ID | 找到的第一个匹配进程的ID | (12)数字(整数)-Integer |
| pidList | 所有进程ID列表 | 具有相同进程名的所有进程的ID列表 | (4)文本列表-List |
| path | 程序路径 | 进程的应用程序路径 | (0)字符串-Text |
| mainWinHandle | 主窗口句柄 |  | (12)数字(整数)-Integer |
| mainwinTitle | 主窗口标题 |  | (0)字符串-Text |
| startTime | 启动时间 |  | (6)时间日期-DateTime |

</details>
<details>
<summary>范例</summary>

**检查微信（WeChat）是否已启动，已启动则提示微信主窗口句柄，否则提示微信未启动**
```json
{
  "Variables": [
    {
      "Key": "handle",
      "Type": 12,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:checkProcessExists",
      "InputParams": {
        "process": {
          "VarKey": null,
          "Value": "WeChat"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "isExists": null,
        "pid": null,
        "pidList": null,
        "path": null,
        "mainWinHandle": "handle",
        "mainwinTitle": null,
        "startTime": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:if",
      "InputParams": {
        "condition": {
          "VarKey": null,
          "Value": "$={handle} > 0"
        }
      },
      "OutputParams": {},
      "IfSteps": [
        {
          "StepRunnerKey": "sys:notify",
          "InputParams": {
            "type": {
              "VarKey": null,
              "Value": "Info"
            },
            "msg": {
              "VarKey": null,
              "Value": "$=\"微信已启动，窗口句柄为\"+{handle}"
            },
            "maxLines": {
              "VarKey": null,
              "Value": "0"
            },
            "style": {
              "VarKey": null,
              "Value": "Default"
            },
            "clickAction": {
              "VarKey": null,
              "Value": ""
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": [
        {
          "StepRunnerKey": "sys:notify",
          "InputParams": {
            "type": {
              "VarKey": null,
              "Value": "Error"
            },
            "msg": {
              "VarKey": null,
              "Value": "微信未启动"
            },
            "maxLines": {
              "VarKey": null,
              "Value": "0"
            },
            "style": {
              "VarKey": null,
              "Value": "Default"
            },
            "clickAction": {
              "VarKey": null,
              "Value": ""
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 5.云状态存取

**功能描述**
> 根据键值读取或写入网络数据。

**官方文档**
> https://getquicker.net/KC/Help/Doc/clouddata

**内部名称**
> sys:clouddata

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| type | 操作类型 |  | (9)选项-Enum（readGlobalState: 从网络读取数据; saveGlobalState: 写入数据到网络） | readGlobalState | True |
| key | 状态名称 | 存储或读取的数据条目名称(键)。 | (0)字符串-Text |  | False |
| value | 内容 | 要保存的数据值。使用*NULL*删除此状态的存储。 | (0)字符串-Text |  | False |
| expireSeconds | 超时时间 | 请求超时时间（秒数） | (1)数字(小数)-Number | 2.5 | False |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| value | 内容 | 读取到的状态内容 | (99)任意类型-Any |
| err | 错误信息 | 出错时输出的错误信息。 | (0)字符串-Text |
| errCode | 错误代码 | 从云服务商返回的错误代码。NoSuchKey=不存在此状态。 | (0)字符串-Text |

</details>
<details>
<summary>范例</summary>

```json
{
  "Variables": [
    {
      "Key": "text",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "状态名称必须是字符串格式"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "步骤说明：写入“今天天气不错”到云存储“CloudKey”中\r\n如果写入*NULL*则删除云端数据（星号也需要写进去）"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:clouddata",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "saveGlobalState"
        },
        "key": {
          "VarKey": null,
          "Value": "CloudKey"
        },
        "value": {
          "VarKey": null,
          "Value": "今天天气不错"
        },
        "expireSeconds": {
          "VarKey": null,
          "Value": "2.5"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "err": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "步骤说明：写入云存储“CloudKey”中读取数据，并保存到变量“text”中去"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:clouddata",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "readGlobalState"
        },
        "key": {
          "VarKey": null,
          "Value": "CloudKey"
        },
        "expireSeconds": {
          "VarKey": null,
          "Value": "2.5"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "value": "text",
        "err": null,
        "errCode": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 6.第三方云存储/图床

**功能描述**
> 使用第三方云服务上传文件。

**官方文档**
> https://getquicker.net/KC/Help/Doc/cloud_oss

**内部名称**
> sys:cloud_oss

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| operation | 操作类型 |  | (9)选项-Enum（Upload: 上传） | Upload | True |
| vendor | 服务商 |  | (9)选项-Enum（Aliyun: 阿里云OSS; Tencent: 腾讯云COS; Qiniu: 七牛云） | Aliyun | True |
| vendorSettings | 服务商参数 |  | (0)字符串-Text |  | False |
| key | 对象名 | 可选。留空时自动生成对象名。如果以/结尾，则在此基础上自动生成对象名。 | (0)字符串-Text |  | False |
| content | 上传内容 | 要上传的文件路径、其它文本内容或图片变量。 | (99)任意类型-Any |  | False |
| customDomain | 自定义域名 | 如"https://files.example.com" | (0)字符串-Text |  | False |
| extraHeaders | 额外的请求头 | 可选。设置厂商相关的特定http头。 | (0)字符串-Text |  | False |
| expireSeconds | 超时时间 | 请求超时时间（秒数） | (12)数字(整数)-Integer | 180 | True |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| vendorUrl | 服务商网址 |  | (0)字符串-Text |
| customUrl | 对象网址 | 设置了自定义域名时会生成此网址。 | (0)字符串-Text |

</details>
<details>
<summary>范例</summary>

**从剪贴板上传图片到阿里云OSS，并返回MarkDown格式引用链接**
```json
{
  "Variables": [
    {
      "Key": "返回网址",
      "Type": 0,
      "Desc": "默认的文本变量",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "剪贴板图片",
      "Type": 3,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "是否为图片",
      "Type": 2,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "当前时间",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "剪贴板文件",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "是否为文件",
      "Type": 2,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "文件类型匹配",
      "Type": 2,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "文件后缀",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "对象路径",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "img/",
      "SaveState": true,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "EndPoint",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "服务节点，如：oss-cn-beijing.aliyuncs.com",
      "SaveState": true,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "AccessKey",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "您的AccessKey",
      "SaveState": true,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "AccessKeySecret",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "您的AccessKeySecret",
      "SaveState": true,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "Bucket",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "Bucket的名称",
      "SaveState": true,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "操作结果",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "打开次数",
      "Type": 12,
      "Desc": "",
      "DefaultValue": "0",
      "SaveState": true,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "上传成功",
      "Type": 2,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:simpleIf",
      "InputParams": {
        "condition": {
          "VarKey": null,
          "Value": "$= {打开次数} == 0"
        }
      },
      "OutputParams": {},
      "IfSteps": [
        {
          "StepRunnerKey": "sys:customwindow",
          "InputParams": {
            "type": {
              "VarKey": null,
              "Value": "ShowAndWaitClose"
            },
            "windowMarkup": {
              "VarKey": null,
              "Value": "<Window xmlns=\"http://schemas.microsoft.com/winfx/2006/xaml/presentation\"\r\n        xmlns:d=\"http://schemas.microsoft.com/expression/blend/2008\"\r\n        xmlns:x=\"http://schemas.microsoft.com/winfx/2006/xaml\"\r\n        xmlns:hc=\"https://handyorg.github.io/handycontrol\"\r\n        xmlns:mc=\"http://schemas.openxmlformats.org/markup-compatibility/2006\"\r\n        xmlns:qk=\"https://getquicker.net\"\r\n        Width=\"450\"\r\n        Height=\"350\"\r\n        Title=\"图库 Lite\"\r\n        ResizeMode=\"NoResize\"\r\n        mc:Ignorable=\"d\">\r\n    <Grid Width=\"450\">\r\n        <TabControl>\r\n            <TabItem Header=\"阿里云 OSS\" FontSize=\"14\" FontWeight=\"Bold\">\r\n                <Grid Background=\"#FFE5E5E5\" HorizontalAlignment=\"Left\" Width=\"450\">\r\n                    <TextBox HorizontalAlignment=\"Left\" Margin=\"149,25,0,0\" TextWrapping=\"Wrap\" Text=\"{Binding [EndPoint]}\" VerticalAlignment=\"Top\" Width=\"250\" FontWeight=\"Normal\"/>\r\n                    <TextBox HorizontalAlignment=\"Left\" Margin=\"149,65,0,0\" TextWrapping=\"Wrap\" Text=\"{Binding [AccessKey]}\" VerticalAlignment=\"Top\" Width=\"250\" FontWeight=\"Normal\"/>\r\n                    <TextBox HorizontalAlignment=\"Left\" Margin=\"149,105,0,0\" TextWrapping=\"Wrap\" Text=\"{Binding [AccessKeySecret]}\" VerticalAlignment=\"Top\" Width=\"250\" FontWeight=\"Normal\"/>\r\n                    <TextBox HorizontalAlignment=\"Left\" Margin=\"149,145,0,0\" TextWrapping=\"Wrap\" Text=\"{Binding [Bucket]}\" VerticalAlignment=\"Top\" Width=\"250\" FontWeight=\"Normal\"/>\r\n                    <TextBox HorizontalAlignment=\"Left\" Margin=\"149,185,0,0\" TextWrapping=\"Wrap\" Text=\"{Binding [对象路径]}\" VerticalAlignment=\"Top\" Width=\"250\" FontWeight=\"Normal\"/>\r\n                    <TextBlock HorizontalAlignment=\"Left\" Margin=\"80,30,0,0\" TextWrapping=\"Wrap\" Text=\"EndPoint\" VerticalAlignment=\"Top\" FontSize=\"14\" FontWeight=\"Bold\"/>\r\n                    <TextBlock HorizontalAlignment=\"Left\" Margin=\"51,70,0,0\" TextWrapping=\"Wrap\" Text=\"AccessKey ID\" VerticalAlignment=\"Top\" FontSize=\"14\" FontWeight=\"Bold\"/>\r\n                    <TextBlock HorizontalAlignment=\"Left\" Margin=\"23,110,0,0\" TextWrapping=\"Wrap\" Text=\"AccessKey Secret\" VerticalAlignment=\"Top\" FontSize=\"14\" FontWeight=\"Bold\"/>\r\n                    <TextBlock HorizontalAlignment=\"Left\" Margin=\"50,150,0,0\" TextWrapping=\"Wrap\" Text=\"Bucket Name\" VerticalAlignment=\"Top\" FontSize=\"14\" FontWeight=\"Bold\"/>\r\n                    <Button Content=\"确定\" HorizontalAlignment=\"Left\" Margin=\"136,230,0,0\" VerticalAlignment=\"Top\" qk:Att.Action=\"close:Yes\"/>\r\n                    <Button Content=\"取消\" HorizontalAlignment=\"Left\" Margin=\"280,230,0,0\" VerticalAlignment=\"Top\" qk:Att.Action=\"close:\"/>\r\n                    <TextBlock HorizontalAlignment=\"Left\" Margin=\"88,190,0,0\" TextWrapping=\"Wrap\" Text=\"对象路径\" VerticalAlignment=\"Top\" FontSize=\"14\" FontWeight=\"Bold\"/>\r\n                </Grid>\r\n            </TabItem>\r\n        </TabControl>\r\n\r\n    </Grid>\r\n\r\n</Window>"
            },
            "dataMapping": {
              "VarKey": null,
              "Value": "EndPoint:{EndPoint}\r\nAccessKey:{AccessKey}\r\nAccessKeySecret:{AccessKeySecret}\r\nBucket:{Bucket}\r\n对象路径:{对象路径}"
            },
            "windowId": {
              "VarKey": null,
              "Value": ""
            },
            "closeWhenDeactivate": {
              "VarKey": null,
              "Value": "false"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            },
            "cscode": {
              "VarKey": null,
              "Value": ""
            },
            "events": {
              "VarKey": null,
              "Value": ""
            },
            "autoCloseTime": {
              "VarKey": null,
              "Value": "0"
            },
            "activateMode": {
              "VarKey": null,
              "Value": "AutoActivate"
            },
            "winLocation": {
              "VarKey": null,
              "Value": "CenterScreen"
            },
            "winSize": {
              "VarKey": null,
              "Value": ""
            }
          },
          "OutputParams": {
            "isSuccess": null,
            "result": "操作结果",
            "errMessage": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:simpleIf",
          "InputParams": {
            "condition": {
              "VarKey": null,
              "Value": "$= {操作结果} == \"\""
            }
          },
          "OutputParams": {},
          "IfSteps": [
            {
              "StepRunnerKey": "sys:notify",
              "InputParams": {
                "type": {
                  "VarKey": null,
                  "Value": "Error"
                },
                "msg": {
                  "VarKey": null,
                  "Value": "未完善信息"
                },
                "maxLines": {
                  "VarKey": null,
                  "Value": "0"
                },
                "style": {
                  "VarKey": null,
                  "Value": "Default"
                },
                "clickAction": {
                  "VarKey": null,
                  "Value": ""
                }
              },
              "OutputParams": {},
              "IfSteps": null,
              "ElseSteps": null,
              "Note": "",
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            },
            {
              "StepRunnerKey": "sys:stop",
              "InputParams": {
                "method": {
                  "VarKey": null,
                  "Value": "default"
                },
                "isError": {
                  "VarKey": null,
                  "Value": "0"
                },
                "return": {
                  "VarKey": null,
                  "Value": ""
                },
                "showMessage": {
                  "VarKey": null,
                  "Value": ""
                }
              },
              "OutputParams": {},
              "IfSteps": null,
              "ElseSteps": null,
              "Note": "",
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            }
          ],
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": true,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:compute",
      "InputParams": {
        "expression": {
          "VarKey": null,
          "Value": "$${打开次数}+1"
        },
        "evalVar": {
          "VarKey": null,
          "Value": "0"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "output": "打开次数",
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:getClipboardImage",
      "InputParams": {
        "stopIfFail": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {
        "isSuccess": "是否为图片",
        "output": "剪贴板图片",
        "elapsedMs": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:getCurrentTime",
      "InputParams": {
        "source": {
          "VarKey": null,
          "Value": "currTime"
        },
        "useUtc": {
          "VarKey": null,
          "Value": "0"
        },
        "addDays": {
          "VarKey": null,
          "Value": "0"
        },
        "addHours": {
          "VarKey": null,
          "Value": "0"
        },
        "addMinutes": {
          "VarKey": null,
          "Value": "0"
        },
        "addSeconds": {
          "VarKey": null,
          "Value": "0"
        },
        "addMonths": {
          "VarKey": null,
          "Value": "0"
        },
        "format": {
          "VarKey": null,
          "Value": "yyyy-MM-dd HH:mm:ss"
        },
        "outputCulture": {
          "VarKey": null,
          "Value": "CURRENT"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "output": null,
        "strValue": "当前时间",
        "timeStamp": null,
        "timeStampMs": null,
        "year": null,
        "month": null,
        "day": null,
        "hour": null,
        "minute": null,
        "second": null,
        "dayOfWeek": null,
        "dayOfYear": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:regexExtract",
      "InputParams": {
        "getGroup": {
          "VarKey": null,
          "Value": "0"
        },
        "data": {
          "VarKey": "当前时间",
          "Value": null
        },
        "pattern": {
          "VarKey": null,
          "Value": "\\d+"
        },
        "ignoreCase": {
          "VarKey": null,
          "Value": "false"
        },
        "singleLine": {
          "VarKey": null,
          "Value": "false"
        },
        "multiLine": {
          "VarKey": null,
          "Value": "false"
        },
        "rightToLeft": {
          "VarKey": null,
          "Value": "false"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "matches": "当前时间",
        "match1 ": null,
        "match2 ": null,
        "match3 ": null,
        "match4 ": null,
        "match5 ": null,
        "matchesCollection": null,
        "isSuccess": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:joinList",
      "InputParams": {
        "list": {
          "VarKey": "当前时间",
          "Value": null
        },
        "separator": {
          "VarKey": null,
          "Value": ""
        },
        "escapeSeparator": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "output": "当前时间"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:if",
      "InputParams": {
        "condition": {
          "VarKey": null,
          "Value": "$= {是否为图片}"
        }
      },
      "OutputParams": {},
      "IfSteps": [
        {
          "StepRunnerKey": "sys:cloud_oss",
          "InputParams": {
            "operation": {
              "VarKey": null,
              "Value": "Upload"
            },
            "vendor": {
              "VarKey": null,
              "Value": "Aliyun"
            },
            "vendorSettings": {
              "VarKey": null,
              "Value": "$$Endpoint:https://{EndPoint}\r\nAccessKey:{AccessKey}\r\nAccessKeySecret:{AccessKeySecret}\r\nBucketName:{Bucket}"
            },
            "key": {
              "VarKey": null,
              "Value": "$${对象路径}{当前时间}.png"
            },
            "content": {
              "VarKey": "剪贴板图片",
              "Value": null
            },
            "customDomain": {
              "VarKey": null,
              "Value": ""
            },
            "extraHeaders": {
              "VarKey": null,
              "Value": ""
            },
            "expireSeconds": {
              "VarKey": null,
              "Value": "180"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "0"
            }
          },
          "OutputParams": {
            "isSuccess": "上传成功",
            "vendorUrl": "返回网址",
            "customUrl": null,
            "err": null,
            "errMessage": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:if",
          "InputParams": {
            "condition": {
              "VarKey": null,
              "Value": "$= {上传成功}"
            }
          },
          "OutputParams": {},
          "IfSteps": [
            {
              "StepRunnerKey": "sys:notify",
              "InputParams": {
                "type": {
                  "VarKey": null,
                  "Value": "Success"
                },
                "msg": {
                  "VarKey": null,
                  "Value": "上传成功"
                },
                "maxLines": {
                  "VarKey": null,
                  "Value": "0"
                },
                "style": {
                  "VarKey": null,
                  "Value": "Default"
                },
                "clickAction": {
                  "VarKey": null,
                  "Value": ""
                }
              },
              "OutputParams": {},
              "IfSteps": null,
              "ElseSteps": null,
              "Note": "",
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            }
          ],
          "ElseSteps": [
            {
              "StepRunnerKey": "sys:notify",
              "InputParams": {
                "type": {
                  "VarKey": null,
                  "Value": "Error"
                },
                "msg": {
                  "VarKey": null,
                  "Value": "上传失败，请检查网络或信息是否填写正确"
                },
                "maxLines": {
                  "VarKey": null,
                  "Value": "0"
                },
                "style": {
                  "VarKey": null,
                  "Value": "Default"
                },
                "clickAction": {
                  "VarKey": null,
                  "Value": ""
                }
              },
              "OutputParams": {},
              "IfSteps": null,
              "ElseSteps": null,
              "Note": "",
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            },
            {
              "StepRunnerKey": "sys:stop",
              "InputParams": {
                "method": {
                  "VarKey": null,
                  "Value": "default"
                },
                "isError": {
                  "VarKey": null,
                  "Value": "0"
                },
                "return": {
                  "VarKey": null,
                  "Value": ""
                },
                "showMessage": {
                  "VarKey": null,
                  "Value": ""
                }
              },
              "OutputParams": {},
              "IfSteps": null,
              "ElseSteps": null,
              "Note": "",
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            }
          ],
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": [
        {
          "StepRunnerKey": "sys:getClipboardFiles",
          "InputParams": {
            "stopIfFail": {
              "VarKey": null,
              "Value": "0"
            }
          },
          "OutputParams": {
            "isSuccess": "是否为文件",
            "output": "剪贴板文件",
            "elapsedMs": null,
            "errMessage": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:if",
          "InputParams": {
            "condition": {
              "VarKey": null,
              "Value": "$= {是否为文件}"
            }
          },
          "OutputParams": {},
          "IfSteps": [
            {
              "StepRunnerKey": "sys:regexExtract",
              "InputParams": {
                "getGroup": {
                  "VarKey": null,
                  "Value": "0"
                },
                "data": {
                  "VarKey": "剪贴板文件",
                  "Value": null
                },
                "pattern": {
                  "VarKey": null,
                  "Value": ".*\\.(jpg|png|gif|jpeg|tif|tiff|tga|bmp|dds|svg|eps|hdr|raw|avif)$"
                },
                "ignoreCase": {
                  "VarKey": null,
                  "Value": "false"
                },
                "singleLine": {
                  "VarKey": null,
                  "Value": "false"
                },
                "multiLine": {
                  "VarKey": null,
                  "Value": "false"
                },
                "rightToLeft": {
                  "VarKey": null,
                  "Value": "false"
                },
                "stopIfFail": {
                  "VarKey": null,
                  "Value": "1"
                }
              },
              "OutputParams": {
                "matches": null,
                "match1 ": null,
                "match2 ": null,
                "match3 ": null,
                "match4 ": null,
                "match5 ": null,
                "matchesCollection": null,
                "isSuccess": "文件类型匹配",
                "errMessage": null
              },
              "IfSteps": null,
              "ElseSteps": null,
              "Note": "",
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            },
            {
              "StepRunnerKey": "sys:if",
              "InputParams": {
                "condition": {
                  "VarKey": null,
                  "Value": "$= {文件类型匹配}"
                }
              },
              "OutputParams": {},
              "IfSteps": [
                {
                  "StepRunnerKey": "sys:regexExtract",
                  "InputParams": {
                    "getGroup": {
                      "VarKey": null,
                      "Value": "0"
                    },
                    "data": {
                      "VarKey": "剪贴板文件",
                      "Value": null
                    },
                    "pattern": {
                      "VarKey": null,
                      "Value": "\\.([^\\\\/]+)"
                    },
                    "ignoreCase": {
                      "VarKey": null,
                      "Value": "true"
                    },
                    "singleLine": {
                      "VarKey": null,
                      "Value": "false"
                    },
                    "multiLine": {
                      "VarKey": null,
                      "Value": "false"
                    },
                    "rightToLeft": {
                      "VarKey": null,
                      "Value": "false"
                    },
                    "stopIfFail": {
                      "VarKey": null,
                      "Value": "0"
                    }
                  },
                  "OutputParams": {
                    "matches": null,
                    "match1 ": "文件后缀",
                    "match2 ": null,
                    "match3 ": null,
                    "match4 ": null,
                    "match5 ": null,
                    "matchesCollection": null,
                    "isSuccess": null,
                    "errMessage": null
                  },
                  "IfSteps": null,
                  "ElseSteps": null,
                  "Note": "",
                  "Disabled": false,
                  "Collapsed": false,
                  "DelayMs": 0
                },
                {
                  "StepRunnerKey": "sys:cloud_oss",
                  "InputParams": {
                    "operation": {
                      "VarKey": null,
                      "Value": "Upload"
                    },
                    "vendor": {
                      "VarKey": null,
                      "Value": "Aliyun"
                    },
                    "vendorSettings": {
                      "VarKey": null,
                      "Value": "$$Endpoint:https://{EndPoint}\r\nAccessKey:{AccessKey}\r\nAccessKeySecret:{AccessKeySecret}\r\nBucketName:{Bucket}"
                    },
                    "key": {
                      "VarKey": null,
                      "Value": "$${对象路径}{当前时间}{文件后缀}"
                    },
                    "content": {
                      "VarKey": "剪贴板文件",
                      "Value": null
                    },
                    "customDomain": {
                      "VarKey": null,
                      "Value": ""
                    },
                    "extraHeaders": {
                      "VarKey": null,
                      "Value": ""
                    },
                    "expireSeconds": {
                      "VarKey": null,
                      "Value": "180"
                    },
                    "stopIfFail": {
                      "VarKey": null,
                      "Value": "0"
                    }
                  },
                  "OutputParams": {
                    "isSuccess": "上传成功",
                    "vendorUrl": "返回网址",
                    "customUrl": null,
                    "err": null,
                    "errMessage": null
                  },
                  "IfSteps": null,
                  "ElseSteps": null,
                  "Note": "",
                  "Disabled": false,
                  "Collapsed": false,
                  "DelayMs": 0
                },
                {
                  "StepRunnerKey": "sys:if",
                  "InputParams": {
                    "condition": {
                      "VarKey": null,
                      "Value": "$= {上传成功}"
                    }
                  },
                  "OutputParams": {},
                  "IfSteps": [
                    {
                      "StepRunnerKey": "sys:notify",
                      "InputParams": {
                        "type": {
                          "VarKey": null,
                          "Value": "Success"
                        },
                        "msg": {
                          "VarKey": null,
                          "Value": "上传成功"
                        },
                        "maxLines": {
                          "VarKey": null,
                          "Value": "0"
                        },
                        "style": {
                          "VarKey": null,
                          "Value": "Default"
                        },
                        "clickAction": {
                          "VarKey": null,
                          "Value": ""
                        }
                      },
                      "OutputParams": {},
                      "IfSteps": null,
                      "ElseSteps": null,
                      "Note": "",
                      "Disabled": false,
                      "Collapsed": false,
                      "DelayMs": 0
                    }
                  ],
                  "ElseSteps": [
                    {
                      "StepRunnerKey": "sys:notify",
                      "InputParams": {
                        "type": {
                          "VarKey": null,
                          "Value": "Error"
                        },
                        "msg": {
                          "VarKey": null,
                          "Value": "上传失败，请检查网络或信息是否填写正确"
                        },
                        "maxLines": {
                          "VarKey": null,
                          "Value": "0"
                        },
                        "style": {
                          "VarKey": null,
                          "Value": "Default"
                        },
                        "clickAction": {
                          "VarKey": null,
                          "Value": ""
                        }
                      },
                      "OutputParams": {},
                      "IfSteps": null,
                      "ElseSteps": null,
                      "Note": "",
                      "Disabled": false,
                      "Collapsed": false,
                      "DelayMs": 0
                    },
                    {
                      "StepRunnerKey": "sys:stop",
                      "InputParams": {
                        "method": {
                          "VarKey": null,
                          "Value": "default"
                        },
                        "isError": {
                          "VarKey": null,
                          "Value": "0"
                        },
                        "return": {
                          "VarKey": null,
                          "Value": ""
                        },
                        "showMessage": {
                          "VarKey": null,
                          "Value": ""
                        }
                      },
                      "OutputParams": {},
                      "IfSteps": null,
                      "ElseSteps": null,
                      "Note": "",
                      "Disabled": false,
                      "Collapsed": false,
                      "DelayMs": 0
                    }
                  ],
                  "Note": "",
                  "Disabled": false,
                  "Collapsed": false,
                  "DelayMs": 0
                }
              ],
              "ElseSteps": [
                {
                  "StepRunnerKey": "sys:notify",
                  "InputParams": {
                    "type": {
                      "VarKey": null,
                      "Value": "Error"
                    },
                    "msg": {
                      "VarKey": null,
                      "Value": "未获取到剪贴板图片"
                    },
                    "maxLines": {
                      "VarKey": null,
                      "Value": "0"
                    },
                    "style": {
                      "VarKey": null,
                      "Value": "Default"
                    },
                    "clickAction": {
                      "VarKey": null,
                      "Value": ""
                    }
                  },
                  "OutputParams": {},
                  "IfSteps": null,
                  "ElseSteps": null,
                  "Note": "",
                  "Disabled": false,
                  "Collapsed": false,
                  "DelayMs": 0
                },
                {
                  "StepRunnerKey": "sys:stop",
                  "InputParams": {
                    "method": {
                      "VarKey": null,
                      "Value": "default"
                    },
                    "isError": {
                      "VarKey": null,
                      "Value": "0"
                    },
                    "return": {
                      "VarKey": null,
                      "Value": ""
                    },
                    "showMessage": {
                      "VarKey": null,
                      "Value": ""
                    }
                  },
                  "OutputParams": {},
                  "IfSteps": null,
                  "ElseSteps": null,
                  "Note": "",
                  "Disabled": false,
                  "Collapsed": false,
                  "DelayMs": 0
                }
              ],
              "Note": "",
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            }
          ],
          "ElseSteps": [
            {
              "StepRunnerKey": "sys:notify",
              "InputParams": {
                "type": {
                  "VarKey": null,
                  "Value": "Error"
                },
                "msg": {
                  "VarKey": null,
                  "Value": "未获取到剪贴板图片"
                },
                "maxLines": {
                  "VarKey": null,
                  "Value": "0"
                },
                "style": {
                  "VarKey": null,
                  "Value": "Default"
                },
                "clickAction": {
                  "VarKey": null,
                  "Value": ""
                }
              },
              "OutputParams": {},
              "IfSteps": null,
              "ElseSteps": null,
              "Note": "",
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            },
            {
              "StepRunnerKey": "sys:stop",
              "InputParams": {
                "method": {
                  "VarKey": null,
                  "Value": "default"
                },
                "isError": {
                  "VarKey": null,
                  "Value": "0"
                },
                "return": {
                  "VarKey": null,
                  "Value": ""
                },
                "showMessage": {
                  "VarKey": null,
                  "Value": ""
                }
              },
              "OutputParams": {},
              "IfSteps": null,
              "ElseSteps": null,
              "Note": "",
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            }
          ],
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:writeClipboard",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "auto"
        },
        "input": {
          "VarKey": null,
          "Value": "$$![]({返回网址})"
        },
        "successMsg": {
          "VarKey": null,
          "Value": ""
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 7.跳过后续步骤(continue)

**功能描述**
> 跳过后续步骤（循环内部），开始下一次循环。在循环内部使用。

**官方文档**
> https://getquicker.net/KC/Help/Doc/continue

**内部名称**
> sys:continue

<details>
<summary>传入参数</summary>
无
</details>
<details>
<summary>传出参数</summary>
无
</details>
<details>
<summary>范例</summary>

**无限循环，每次循环给count+1，count大于等于10时结束动作**
```json
{
  "Variables": [
    {
      "Key": "count",
      "Type": 12,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:repeat",
      "InputParams": {
        "count": {
          "VarKey": null,
          "Value": "-1"
        },
        "stopCondition": {
          "VarKey": null,
          "Value": ""
        },
        "startIndex": {
          "VarKey": null,
          "Value": "0"
        },
        "repeatDelayMs": {
          "VarKey": null,
          "Value": "1"
        },
        "progressBarTitle": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {
        "count": "count"
      },
      "IfSteps": [
        {
          "StepRunnerKey": "sys:if",
          "InputParams": {
            "condition": {
              "VarKey": null,
              "Value": "$={count}<10"
            }
          },
          "OutputParams": {},
          "IfSteps": [
            {
              "StepRunnerKey": "sys:continue",
              "InputParams": {},
              "OutputParams": {},
              "IfSteps": null,
              "ElseSteps": null,
              "Note": null,
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            }
          ],
          "ElseSteps": [
            {
              "StepRunnerKey": "sys:stop",
              "InputParams": {
                "method": {
                  "VarKey": null,
                  "Value": "default"
                },
                "isError": {
                  "VarKey": null,
                  "Value": "0"
                },
                "return": {
                  "VarKey": null,
                  "Value": ""
                },
                "showMessage": {
                  "VarKey": null,
                  "Value": ""
                }
              },
              "OutputParams": {},
              "IfSteps": null,
              "ElseSteps": null,
              "Note": "",
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            }
          ],
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 8.每个

**功能描述**
> 对列表的每项执行处理

**官方文档**
> https://getquicker.net/KC/Help/Doc/each

**内部名称**
> sys:each

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| input | 列表 | 要处理的列表 | (4)文本列表-List |  | True |
| useMultiThread | 线程模式 | ⚠通常不要选择! 请阅读文档详细了解后再使用。 | (9)选项-Enum（0: 单线程（顺序执行）; 1: 多线程（同时执行）） | 0 | False |
| threadDelay | 线程启动间隔 | 多线程运行时，每个线程之间的启动时间间隔毫秒数。 | (12)数字(整数)-Integer | 5 | False |
| concurrentThreadNum | 同时线程数 | 最多同时启动的线程数，请根据电脑配置和任务内容设置。 | (12)数字(整数)-Integer | 4 | False |
| timeoutMs | 超时毫秒数 | 所有线程开启后，等待的超时时间，单位：毫秒。-1:不设置超时时间 | (12)数字(整数)-Integer | -1 | False |
| useLocalContext | 为线程创建独立上下文 | 此时只能读取变量，不能更新变量（词典、列表等引用传递的除外） | (2)布尔值-Boolean | False | False |
| waitAny | WaitAny模式 | 任意一个线程结束即可。 | (2)布尔值-Boolean | False | False |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| item | 项 | 列表中的每项，每次循环赋予当前项的值。在子步骤中应该对本输出进行处理。 | (99)任意类型-Any |
| count | 计数 | 本次循环，处理到了第几项。 | (12)数字(整数)-Integer |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |

</details>
<details>
<summary>范例</summary>

**[范例参考<跳出循环>](#2.跳出循环（break）)**
</details>

***

## 9.获取前台进程信息

**功能描述**
> 获取当前活动窗口进程的信息。

**官方文档**
> https://getquicker.net/KC/Help/Doc/getactiveprocessinfo

**内部名称**
> sys:getActiveProcessInfo

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| stopIfFail | 失败后中止动作 | 获取进程信息失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| path | 程序路径 | 获得的进程路径 | (0)字符串-Text |
| procName | 进程名 | 进程名称 | (0)字符串-Text |
| pid | PID | 进程ID | (12)数字(整数)-Integer |
| isSuccess | 是否成功 | 是否成功获得进程信息 | (2)布尔值-Boolean |

</details>
<details>
<summary>范例</summary>

**获取进程名称、程序路径、pid**
```json
{
  "Variables": [
    {
      "Key": "进程名称",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "程序路径",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "pid",
      "Type": 12,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:getActiveProcessInfo",
      "InputParams": {
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "path": "程序路径",
        "procName": "进程名称",
        "pid": "pid",
        "isSuccess": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 10.获取浏览器网址

**功能描述**
> 获取当前浏览器网址。

**官方文档**
> https://getquicker.net/KC/Help/Doc/getchromeurl

**内部名称**
> sys:getChromeUrl

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| output | 网址 | 当前标签网址URL | (0)字符串-Text |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |

</details>
<details>
<summary>范例</summary>

```json
{
  "Variables": [
    {
      "Key": "link",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:getChromeUrl",
      "InputParams": {
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "output": "link",
        "isSuccess": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 11.获取剪贴板文件列表

**功能描述**
> 获取剪贴板中复制的文件(或文件夹)的路径列表

**官方文档**
> https://getquicker.net/KC/Help/Doc/getclipboardfiles

**内部名称**
> sys:getClipboardFiles

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| stopIfFail | 失败后中止动作 | 获取选中的文本失败后，是否停止后续动作的执行。 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 是否成功获得文件列表 | (2)布尔值-Boolean |
| output | 文件列表 | 从剪贴板获取的文件路径列表 | (4)文本列表-List |
| elapsedMs | 已更新时间 | 剪贴板最后更新是在多少毫秒以前 | (12)数字(整数)-Integer |

</details>
<details>
<summary>范例</summary>

```json
{
  "Variables": [
    {
      "Key": "list",
      "Type": 4,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:getClipboardFiles",
      "InputParams": {
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "output": "list",
        "elapsedMs": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 12.获取剪贴板图片

**功能描述**
> 读取剪贴板中的图片内容输出到图片变量中。

**官方文档**
> https://getquicker.net/KC/Help/Doc/getclipboardimage

**内部名称**
> sys:getClipboardImage

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| stopIfFail | 失败后中止动作 | 获取失败后，是否停止后续动作的执行。 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 是否成功获得剪贴板图片 | (2)布尔值-Boolean |
| output | 结果图片 | 将获得的图片写入到变量 | (3)图片-Image |
| elapsedMs | 已更新时间 | 剪贴板最后更新是在多少毫秒以前 | (12)数字(整数)-Integer |

</details>
<details>
<summary>范例</summary>

```json
{
  "Variables": [
    {
      "Key": "clipImage",
      "Type": 3,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:getClipboardImage",
      "InputParams": {
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "output": "clipImage",
        "elapsedMs": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 13.获取剪贴板文本

**功能描述**
> 读取剪贴板中的文本内容

**官方文档**
> https://getquicker.net/KC/Help/Doc/getClipboardText

**内部名称**
> sys:getClipboardText

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| format | 文本数据格式 | 需要读取的剪贴板文本内容格式。通常请使用Unicode纯文本格式。 | (9)选项-Enum（UnicodeText: 纯文本; Rtf; Html; CommaSeparatedValue: 带逗号分隔的值(csv); Custom: 自定义格式名） | UnicodeText | False |
| customFormat | 格式名称 | 自定义的剪贴板格式名，请和实际剪贴板格式名一致。只支持实际为文本类型的内容。 | (0)字符串-Text |  | False |
| encoding | 文本编码 | 读取自定义格式时候使用的编码类型 | (9)选项-Enum | utf-8 | True |
| waitMs | 重试时间 | 每10ms重试一次，直到获取到文本。为0时不重试。 | (12)数字(整数)-Integer | 400 | False |
| stopIfFail | 失败后中止动作 | 获取选中的文本失败后，是否停止后续动作的执行。 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 是否成功获得文本 | (2)布尔值-Boolean |
| output | 完整结果内容 | 将获得的文本内容写入到变量 | (0)字符串-Text |
| cleanHtml | 主要HTML片段 | HTML的主要内容。<!--StartFragment-->和<!--EndFragment-->之间的部分 | (0)字符串-Text |
| htmlDoc | 完整的HTML文档 | 仅去除剪贴板头部信息的完整HTML文档内容。包含<html>等标签，可直接保存为.html文件。 | (0)字符串-Text |
| url | 来源网址 | 从网页中复制内容时，可能会携带网址信息。 | (0)字符串-Text |
| elapsedMs | 已更新时间 | 剪贴板最后更新是在多少毫秒以前 | (12)数字(整数)-Integer |

</details>
<details>
<summary>范例</summary>


**获取文本到text变量**
```json
{
  "Variables": [
    {
      "Key": "text",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:getClipboardText",
      "InputParams": {
        "format": {
          "VarKey": null,
          "Value": "UnicodeText"
        },
        "waitMs": {
          "VarKey": null,
          "Value": "400"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "output": "text",
        "url": null,
        "elapsedMs": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```

**获取HTML Format格式文本**
```json
{
  "Variables": [
    {
      "Key": "text",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:getClipboardText",
      "InputParams": {
        "format": {
          "VarKey": null,
          "Value": "Custom"
        },
        "customFormat": {
          "VarKey": null,
          "Value": "HTML Format"
        },
        "encoding": {
          "VarKey": null,
          "Value": "utf-8"
        },
        "waitMs": {
          "VarKey": null,
          "Value": "400"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "output": "text",
        "url": null,
        "elapsedMs": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 14.获取日期时间

**功能描述**
> 获取当前或从文本、unix时间戳转换日期时间

**官方文档**
> https://getquicker.net/KC/Help/Doc/gettime

**内部名称**
> sys:getCurrentTime

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| source | 时间来源 | 时间数据来源 | (9)选项-Enum（currTime: 当前时间; fromString: 从文本转换; fromUnixTimeStamp: 从Unix时间戳转换(秒); Source_UnixTimeStampMs: 从Unix时间戳转换(毫秒); fromVar: 时间变量） | currTime | False |
| useUtc | 使用UTC时间 | 是表示使用UTC时间，否表示使用本地时间（电脑的当前时间）。 | (2)布尔值-Boolean | False | False |
| timeStr | 待解析文本 | 待转换为时间值的文本 | (0)字符串-Text |  | False |
| inputCulture | 语言文化 | 可选，待解析文本的语言文化。如zh-CN表示中文简体，en-US表示英文美国等。详情请参考文档。 | (0)字符串-Text（CURRENT: 当前系统语言; zh-CN; en-US; ja-JP; ko-KR; fr-FR; de-DE; es-ES; it-IT; ru-RU; pt-BR） | CURRENT | False |
| inputFormat | 数据格式 | 可选，待解析文本的数据格式，如yyyy表示4位数年份，MM表示2位数月份等。详情请参考文档。 | (0)字符串-Text |  | False |
| timeVar | 时间变量 | 时间变量 | (6)时间日期-DateTime |  | False |
| timeStampStr | Unix时间戳值 | 从1970年1月1日开始所经过的秒数或毫秒数。根据需要开启或关闭使用UTC时间选项。 | (0)字符串-Text |  | False |
| addDays | 添加天数 | 添加指定的天数（可以为小数/负数） | (1)数字(小数)-Number | 0 | False |
| addHours | 添加小时数 | 添加指定的小时数（可以为小数/负数） | (1)数字(小数)-Number | 0 | False |
| addMinutes | 添加分钟数 | 添加指定的分钟数（可以为小数/负数） | (1)数字(小数)-Number | 0 | False |
| addSeconds | 添加秒数 | 添加指定的秒数（可以为小数/负数） | (1)数字(小数)-Number | 0 | False |
| addMonths | 添加月数 | 添加指定的月数（整数）结果不跨月，如1月31日增加1个月等于2月28日。 | (1)数字(小数)-Number | 0 | False |
| format | 输出文本值格式 | 文本值的输出格式，请参考c#语言DateTime.ToString()的参数文档。 | (0)字符串-Text | yyyy-MM-dd HH:mm:ss | False |
| outputCulture | 输出语言文化 | 可选。指定将时间值格式化为文本时所使用的语言文化。如zh-CN表示中文简体，en-US表示美国英文等。 | (0)字符串-Text | CURRENT | False |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| output | 时间值 | 日期时间类型的结果时间 | (6)时间日期-DateTime |
| strValue | 文本值 | 按‘文本值格式’参数转换后的文本格式值 | (0)字符串-Text |
| timeStamp | UNIX时间戳(s) | 获取Unix时间戳（1970年1月1日0时到指定时间的秒数） | (12)数字(整数)-Integer |
| timeStampMs | UNIX时间戳(ms) | 获取Unix时间戳（1970年1月1日0时到指定时间的毫秒数） | (12)数字(整数)-Integer |
| year | 年 | 年份值 | (12)数字(整数)-Integer |
| month | 月 | 月份值 | (12)数字(整数)-Integer |
| day | 日 | 日期值 | (12)数字(整数)-Integer |
| hour | 时 | 当前小时数，24小时制。 | (12)数字(整数)-Integer |
| minute | 分 | 当前分钟数。 | (12)数字(整数)-Integer |
| second | 秒 | 当前秒数。 | (12)数字(整数)-Integer |
| dayOfWeek | 周第几天 | 本周的第几天，周日为0，周一为1，以此类推。 | (12)数字(整数)-Integer |
| dayOfYear | 年第几天 | 本年的第几天。 | (12)数字(整数)-Integer |

</details>
<details>
<summary>范例</summary>

**获取当前时间1天2小时3分钟后的时间**
```json
{
  "Variables": [
    {
      "Key": "datetime",
      "Type": 6,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:getCurrentTime",
      "InputParams": {
        "source": {
          "VarKey": null,
          "Value": "currTime"
        },
        "useUtc": {
          "VarKey": null,
          "Value": "0"
        },
        "addDays": {
          "VarKey": null,
          "Value": "1"
        },
        "addHours": {
          "VarKey": null,
          "Value": "2"
        },
        "addMinutes": {
          "VarKey": null,
          "Value": "3"
        },
        "addSeconds": {
          "VarKey": null,
          "Value": "0"
        },
        "addMonths": {
          "VarKey": null,
          "Value": "0"
        },
        "format": {
          "VarKey": null,
          "Value": "yyyy-MM-dd HH:mm:ss"
        },
        "outputCulture": {
          "VarKey": null,
          "Value": "CURRENT"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "output": "datetime",
        "strValue": null,
        "timeStamp": null,
        "timeStampMs": null,
        "year": null,
        "month": null,
        "day": null,
        "hour": null,
        "minute": null,
        "second": null,
        "dayOfWeek": null,
        "dayOfYear": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 15.获取资源管理器路径/跳转路径

**功能描述**
> 获取资源管理器的当前文件夹路径。

**官方文档**
> https://getquicker.net/KC/Help/Doc/getexplorerpath

**内部名称**
> sys:getExplorerPath

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| operation | 操作类型 |  | (9)选项-Enum（getPath: 获取路径; setPath: 设置路径） | getPath | False |
| path | 路径 |  | (0)字符串-Text |  | False |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| output | 当前窗口路径 | 当前资源管理器窗口的路径 | (0)字符串-Text |
| allPathList | 所有打开的路径 | 所有资源管理器窗口中打开的路径列表 | (4)文本列表-List |
| lastPath | 最近访问的路径 | 最近访问的资源管理器窗口的路径 | (0)字符串-Text |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |

</details>
<details>
<summary>范例</summary>

**获取资源管理器当前路径**
```json
{
  "Variables": [
    {
      "Key": "path",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:getExplorerPath",
      "InputParams": {
        "operation": {
          "VarKey": null,
          "Value": "getPath"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "output": "path",
        "allPathList": null,
        "lastPath": null,
        "isSuccess": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 16.获取系统路径

**功能描述**
> 返回指定的特殊目录路径。

**官方文档**
> https://getquicker.net/KC/Help/Doc/getfolderpath

**内部名称**
> sys:getFolderPath

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| folder | 目录类型 | Windows的特殊目录类型，详情请搜索“Environment.SpecialFolder”。 | (9)选项-Enum |  | True |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| path | 路径 | 返回的完整路径 | (0)字符串-Text |

</details>
<details>
<summary>范例</summary>

**获取桌面路径**
```json
{
  "Variables": [
    {
      "Key": "path",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:getFolderPath",
      "InputParams": {
        "folder": {
          "VarKey": null,
          "Value": "Desktop"
        }
      },
      "OutputParams": {
        "path": "path"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 17.获取选中的文本

**功能描述**
> 获取选中的文字

**官方文档**
> https://getquicker.net/KC/Help/Doc/get_selected_text

**内部名称**
> sys:getSelectedText

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| format | 文本数据格式 | 需要读取的剪贴板文本内容格式。通常请使用Unicode纯文本格式。 | (9)选项-Enum（UnicodeText: 纯文本（默认）; Rtf; Html; CommaSeparatedValue: 逗号分隔的值（csv）） | UnicodeText | False |
| waitMs | 等待剪贴板时间 | 模拟复制键后，等待剪贴板变化的最长时间毫秒数。 | (12)数字(整数)-Integer | 250 | False |
| repeat | 重试次数 | 【已过时，仅为兼容性保留】失败后重试的次数。 | (12)数字(整数)-Integer | 0 | False |
| trim | 去除前后的空白 | 去除内容前后的空白（包括空行）。 | (2)布尔值-Boolean | False | False |
| tryNoClipboard | 尝试不通过剪贴板的方式获取 | 通过UIAutomation方式获取（某些情况可能出现无法完整获取文字、失去换行信息等问题） | (2)布尔值-Boolean | False | False |
| useActionParam | 如果为动作传递了参数，使用参数值作为获取的结果 | 没有传递参数时仍尝试获取选中的文本。 | (2)布尔值-Boolean | False | False |
| stopIfFail | 失败后中止动作 | 获取选中的文本失败后，是否停止后续动作的执行。 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 是否成功获取了文本 | (2)布尔值-Boolean |
| output | 内容 | 将获得的文本写入到变量 | (0)字符串-Text |
| cleanHtml | 去除封装的HTML | 剪贴板HTML的主要内容<!--StartFragment-->和<!--EndFragment-->之间的部分 | (0)字符串-Text |
| outputEncoded | URL编码的内容 | 对选中的内容进行URL编码处理后的结果，通常用于拼接网址。 | (0)字符串-Text |
| url | 来源网址 | 从网页中复制内容时，可能会携带网址信息。 | (0)字符串-Text |

</details>
<details>
<summary>范例</summary>

**最长等待250毫秒获取选中文本并去除文本前后空白，失败后中止动作。**
```json
{
  "Variables": [
    {
      "Key": "text",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:getSelectedText",
      "InputParams": {
        "format": {
          "VarKey": null,
          "Value": "UnicodeText"
        },
        "waitMs": {
          "VarKey": null,
          "Value": "250"
        },
        "repeat": {
          "VarKey": null,
          "Value": "0"
        },
        "trim": {
          "VarKey": null,
          "Value": "1"
        },
        "tryNoClipboard": {
          "VarKey": null,
          "Value": "0"
        },
        "useActionParam": {
          "VarKey": null,
          "Value": "0"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "output": "text",
        "outputEncoded": null,
        "url": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 18.获取系统或动作信息

**功能描述**
> 返回Windows系统信息。

**官方文档**
> https://getquicker.net/KC/Help/Doc/getsysinfo

**内部名称**
> sys:getSysInfo

<details>
<summary>传入参数</summary>
无
</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| MachineName | 机器名 |  | (0)字符串-Text |
| userName | 用户名 | 当前登录到电脑的用户名 | (0)字符串-Text |
| userDomainName | 用户域名 | 当前用户的网络域名（DomainName） | (0)字符串-Text |
| OsVersion | 系统版本号 |  | (0)字符串-Text |
| isWin10 | 是否为Win10或以上 |  | (2)布尔值-Boolean |
| isWin11 | 是否为Win11 |  | (2)布尔值-Boolean |
| isAutoRun | 是否自动启动 | 是否开机自动启动Quicker | (2)布尔值-Boolean |
| startupSeconds | 系统正常运行秒数 | 可参考任务管理器中显示的正常运行时间。 | (1)数字(小数)-Number |
| isLocked | Windows是否锁定 |  | (2)布尔值-Boolean |
| sysEnv | 环境变量 |  | (10)词典-Dict |
| primaryScreenRes | 主屏分辨率 |  | (0)字符串-Text |
| isFullscreen | 前台窗口是否为全屏状态 |  | (2)布尔值-Boolean |
| isNetworkConnected | 是否联网 |  | (2)布尔值-Boolean |
| lanIp | 本机局域网IP |  | (0)字符串-Text |
| quickerVersion | Quicker版本 |  | (12)数字(整数)-Integer |
| isPro | 是否为专业版 | 当前用户是否使用专业版软件。 | (2)布尔值-Boolean |
| unionId | UnionId | 一个标识用户身份的字符串 | (0)字符串-Text |
| hasBaiduAccount | 已设置自有百度OCR帐号 | 已经在设置中添加了自有百度OCR帐号。 | (2)布尔值-Boolean |
| runnedSeconds | Quicker启动秒数 | Quicker启动后运行的秒数 | (1)数字(小数)-Number |
| actionId | 动作ID | 当前运行的动作ID | (0)字符串-Text |
| actionName | 动作名称 | 当前运行的动作名称 | (0)字符串-Text |
| sharedActionId | 动作库ID | 当前动作的动作库ID | (0)字符串-Text |
| sharedActionRevision | 动作版本号 | 当前安装的动作版本 | (12)数字(整数)-Integer |
| actionCount | 运行个数 | 当前动作运行中的实例个数(包含此实例) | (12)数字(整数)-Integer |
| isDebugging | 是否调试运行 | 是否正在调试运行动作 | (2)布尔值-Boolean |
| trigger | 触发方式 | 动作的触发方式 | (0)字符串-Text |
| textParam | 文本上下文参数 | 传入动作的文本上下文参数 | (0)字符串-Text |
| imageParam | 图片上下文参数 | 传入动作的图片上下文参数 | (3)图片-Image |
| isWinInDarkMode | Windows是否为深色模式 | true表示深色模式，false表示浅色模式。 | (2)布尔值-Boolean |
| quickerThemeMode | Quicker主题模式 | 可能为：light/dark/auto_light/auto_dark。auto_light/auto_dark表示为跟随windows，当前为浅色或深色模式。 | (0)字符串-Text |

</details>
<details>
<summary>范例</summary>

**获取当前动作名称，动作ID，电脑机器名称，是否为Quicker专业版，Quicker版本号**
```json
{
  "Variables": [
    {
      "Key": "MachineName",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "isPro",
      "Type": 2,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "quickerVersion",
      "Type": 12,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "actionId",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "actionName",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:getSysInfo",
      "InputParams": {},
      "OutputParams": {
        "MachineName": "MachineName",
        "userName": null,
        "userDomainName": null,
        "OsVersion": null,
        "isWin10": null,
        "isWin11": null,
        "isAutoRun": null,
        "startupSeconds": null,
        "isLocked": null,
        "sysEnv": null,
        "primaryScreenRes": null,
        "isFullscreen": null,
        "isNetworkConnected": null,
        "lanIp": null,
        "quickerVersion": "quickerVersion",
        "isPro": "isPro",
        "unionId": null,
        "hasBaiduAccount": null,
        "runnedSeconds": null,
        "actionId": "actionId",
        "actionName": "actionName",
        "sharedActionId": null,
        "sharedActionRevision": null,
        "actionCount": null,
        "isDebugging": null,
        "trigger": null,
        "textParam": null,
        "imageParam": null,
        "isWinInDarkMode": null,
        "quickerThemeMode": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 19.获取窗口信息/查找窗口

**功能描述**
> 获取指定窗口的标题等信息。

**官方文档**
> https://getquicker.net/KC/Help/Doc/getwindowtitle

**内部名称**
> sys:getWindowTitle

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| which | 目标窗口 | 判断哪个窗口的信息 | (9)选项-Enum（foreground: 前台窗口; selectWindow: 选择一个窗口; pointing: 弹出面板前鼠标位置的窗口（可能为子窗口）; pointing_root: 弹出面板前鼠标位置窗口的根窗口; pointing_now: 当前鼠标位置的窗口（可能为子窗口）; pointing_now_root: 当前鼠标位置窗口的根窗口; fromHwnd: 句柄指定的窗口; findWindow: 查找顶层窗口 (单个窗口); top_windows: 所有顶层窗口; findChildWindow: 查找子窗口/控件 (单个窗口); child_windows: 查找子窗口 (多个窗口)） | foreground | True |
| hWnd | 窗口句柄hWnd | 未指定时使用前台窗口句柄 | (12)数字(整数)-Integer |  | False |
| className | 窗口类名 | 要查找窗口的类名（ClassName），为空时不检查此项。 | (0)字符串-Text |  | False |
| windowName | 窗口名称 | 要查找窗口的标题，为空时不检查此项。 | (0)字符串-Text |  | False |
| procIdOrName | 进程名/pid | 要查找窗口所属的进程名或pid，为空时不检查此项。 | (0)字符串-Text |  | False |
| onlyVisible | 仅可见窗口 |  | (9)选项-Enum | default | False |
| requireTitle | 仅名称(标题)不为空的窗口 |  | (2)布尔值-Boolean | True | False |
| useRegex | 使用正则匹配窗口类名和标题 |  | (2)布尔值-Boolean | False | False |
| winRectIncludeInvisibleBorder | 窗口位置包含不可见边框（阴影区域） |  | (2)布尔值-Boolean | False | False |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| output | 窗口标题 | 窗口的标题文字 | (0)字符串-Text |
| className | 类名 | 窗口的 Class Name | (0)字符串-Text |
| handle | 句柄 | 窗口的句柄 | (12)数字(整数)-Integer |
| pid | 进程ID | 窗口所属进程的ID | (12)数字(整数)-Integer |
| procName | 进程名 | 进程名称 | (0)字符串-Text |
| path | 程序路径 | 获得的进程路径 | (0)字符串-Text |
| parent | 父窗口句柄 |  | (12)数字(整数)-Integer |
| root | 根窗口句柄 |  | (12)数字(整数)-Integer |
| rootOwner | 根所有者窗口句柄 |  | (12)数字(整数)-Integer |
| rect | 窗口位置 | 文本值，格式为:Left,Top,Right,Bottom,Width,Height。 | (0)字符串-Text |
| rectNoSize | 窗口位置(不含尺寸) | 文本值，格式为:Left,Top,Right,Bottom。如:0,0,100,100 | (0)字符串-Text |
| rectDict | 窗口位置(词典值) | 词典值，属性为:Left,Top,Right,Bottom,Width,Height | (10)词典-Dict |
| isTopmost | 是否置顶 |  | (2)布尔值-Boolean |
| isVisible | 是否可见 |  | (2)布尔值-Boolean |
| showState | 显示状态 | 1:普通，2:最小化，3:最大化。 | (12)数字(整数)-Integer |
| alpha | 不透明度 | 窗口的透明度，范围为0-255。0表示全透明 | (12)数字(整数)-Integer |
| allChildWindows | 所有子窗口 | 词典值，Key为窗口句柄，Value为窗口标题 | (10)词典-Dict |
| topLevelWindows | 所有顶层窗口 | 词典值，Key为窗口句柄，Value为窗口标题 | (10)词典-Dict |

</details>
<details>
<summary>范例</summary>

**获取前台窗口句柄**
```json
{
  "Variables": [
    {
      "Key": "handle",
      "Type": 12,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:getWindowTitle",
      "InputParams": {
        "which": {
          "VarKey": null,
          "Value": "foreground"
        },
        "winRectIncludeInvisibleBorder": {
          "VarKey": null,
          "Value": "0"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "output": null,
        "className": null,
        "handle": "handle",
        "pid": null,
        "procName": null,
        "path": null,
        "parent": null,
        "root": null,
        "rootOwner": null,
        "rect": null,
        "rectNoSize": null,
        "rectDict": null,
        "isTopmost": null,
        "isVisible": null,
        "showState": null,
        "alpha": null,
        "allChildWindows": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```

**获取前台窗口下名称为"咿呀咿呀"的子窗口句柄和窗口位置，获取失败不会停止动作，如果获取到则显示窗口位置信息**
```json
{
  "Variables": [
    {
      "Key": "handle",
      "Type": 12,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "rectDict",
      "Type": 10,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "isSuccess",
      "Type": 2,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:getWindowTitle",
      "InputParams": {
        "which": {
          "VarKey": null,
          "Value": "findChildWindow"
        },
        "hWnd": {
          "VarKey": null,
          "Value": ""
        },
        "className": {
          "VarKey": null,
          "Value": ""
        },
        "windowName": {
          "VarKey": null,
          "Value": "咿呀咿呀"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {
        "isSuccess": "isSuccess",
        "handle": "handle",
        "rectNoSize": null,
        "rectDict": "rectDict",
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:simpleIf",
      "InputParams": {
        "condition": {
          "VarKey": "isSuccess",
          "Value": null
        }
      },
      "OutputParams": {},
      "IfSteps": [
        {
          "StepRunnerKey": "sys:notify",
          "InputParams": {
            "type": {
              "VarKey": null,
              "Value": "Info"
            },
            "msg": {
              "VarKey": "rectDict",
              "Value": null
            },
            "maxLines": {
              "VarKey": null,
              "Value": "0"
            },
            "style": {
              "VarKey": null,
              "Value": "Default"
            },
            "clickAction": {
              "VarKey": null,
              "Value": ""
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 20.步骤组

**功能描述**
> 一组有关的模块（方便整体禁用、删除等）

**官方文档**
> https://getquicker.net/KC/Help/Doc/group

**内部名称**
> sys:group

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| skipErr | 忽略错误 | 忽略内部步骤的错误，继续允许后续代码 | (2)布尔值-Boolean | False | False |
| skipWhenDebugging | 调试运行时不输出调试内容 | 用以减少不必要的调试输出 | (2)布尔值-Boolean | False | False |
| useMultiThread | 使用多线程 | ⚠通常不要选择! 请阅读文档详细了解后再使用。 | (2)布尔值-Boolean | False | False |
| waitAny | 多线程使用WaitAny模式 | 任意一个线程结束即可。 | (2)布尔值-Boolean | False | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 内部步骤是否运行成功 | (2)布尔值-Boolean |
| errorMessage | 错误消息 |  | (0)字符串-Text |

</details>
<details>
<summary>范例</summary>


**多线程同时运行两个步骤组，第一个步骤组内容为：等待3000毫秒，如果用户未按下“弹窗提示或确认”模块任何按钮，则模拟按下键盘左Alt+Y组合键以快速点击第一个按钮；第二个步骤内容为“弹窗提示或确认模块”，其中有3个按钮，默认的按钮值为Yes。两个线程都运行结束后，显示按钮的值**
```json
{
  "Variables": [
    {
      "Key": "btn",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:group",
      "InputParams": {
        "skipErr": {
          "VarKey": null,
          "Value": "0"
        },
        "skipWhenDebugging": {
          "VarKey": null,
          "Value": "0"
        },
        "useMultiThread": {
          "VarKey": null,
          "Value": "1"
        },
        "waitAny": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "errorMessage": null
      },
      "IfSteps": [
        {
          "StepRunnerKey": "sys:group",
          "InputParams": {},
          "OutputParams": {},
          "IfSteps": [
            {
              "StepRunnerKey": "sys:delay",
              "InputParams": {
                "delayMs": {
                  "VarKey": null,
                  "Value": "3000"
                },
                "monitorWaitWin": {
                  "VarKey": null,
                  "Value": "0"
                }
              },
              "OutputParams": {},
              "IfSteps": null,
              "ElseSteps": null,
              "Note": "",
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            },
            {
              "StepRunnerKey": "sys:simpleIf",
              "InputParams": {
                "condition": {
                  "VarKey": null,
                  "Value": "$={btn}==\"\""
                }
              },
              "OutputParams": {},
              "IfSteps": [
                {
                  "StepRunnerKey": "sys:keyInput",
                  "InputParams": {
                    "keys": {
                      "VarKey": null,
                      "Value": "{\"CtrlKeys\":[164],\"Keys\":[89]}"
                    },
                    "repeat": {
                      "VarKey": null,
                      "Value": "1"
                    },
                    "interval": {
                      "VarKey": null,
                      "Value": "1"
                    },
                    "holdMs": {
                      "VarKey": null,
                      "Value": "-1"
                    }
                  },
                  "OutputParams": {},
                  "IfSteps": null,
                  "ElseSteps": null,
                  "Note": "",
                  "Disabled": false,
                  "Collapsed": false,
                  "DelayMs": 0
                }
              ],
              "ElseSteps": null,
              "Note": "",
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            }
          ],
          "ElseSteps": [],
          "Note": null,
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:group",
          "InputParams": {},
          "OutputParams": {},
          "IfSteps": [
            {
              "StepRunnerKey": "sys:MsgBox",
              "InputParams": {
                "operation": {
                  "VarKey": null,
                  "Value": "custom"
                },
                "message": {
                  "VarKey": null,
                  "Value": "Hello."
                },
                "title": {
                  "VarKey": null,
                  "Value": "Quicker"
                },
                "customIcon": {
                  "VarKey": null,
                  "Value": "Information"
                },
                "customButtons": {
                  "VarKey": null,
                  "Value": "[fa:Regular_Check:#4caf50]第一个按钮(_Y)|按钮1\r\n[fa:Regular_Times:#dc3545]第二个按钮(_N)|按钮2\r\n[fa:Light_Undo:#444444]取消(_C)|Cancel"
                },
                "defaultButton": {
                  "VarKey": null,
                  "Value": "Yes"
                },
                "restoreFocus": {
                  "VarKey": null,
                  "Value": "1"
                }
              },
              "OutputParams": {
                "result": "btn"
              },
              "IfSteps": null,
              "ElseSteps": null,
              "Note": "",
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            }
          ],
          "ElseSteps": [],
          "Note": null,
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": [],
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:notify",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "Info"
        },
        "msg": {
          "VarKey": "btn",
          "Value": null
        },
        "maxLines": {
          "VarKey": null,
          "Value": "0"
        },
        "style": {
          "VarKey": null,
          "Value": "Default"
        },
        "clickAction": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 21.HTTP请求

**功能描述**
> 发送HTTP请求，并获取返回结果

**官方文档**
> https://getquicker.net/KC/Help/Doc/http

**内部名称**
> sys:http

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| url | 网址 | 要打开的网页地址 | (0)字符串-Text | https:// | True |
| method | 方法 | Http请求的类型 | (9)选项-Enum（GET, POST, PUT, DELETE, PATCH, HEAD, OPTIONS） | GET | True |
| header | 请求头 | 发送的HttpHeader。每行一个header，格式为Name:Value | (0)字符串-Text |  | False |
| cookie | Cookie | 请求的cookie内容 | (0)字符串-Text |  | False |
| bodyType | 请求体类型 | Http 请求体的内容 | (9)选项-Enum（JSON, FORM: 文本表单, FILE: MultiPart表单, BinaryFile: 单个文件或图片变量（二进制）, Text: 纯文本） | JSON | True |
| body | 请求体 | Http 请求 BODY。格式要求详见模块帮助。 | (0)字符串-Text |  | False |
| contentType | 内容类型 | 选填。上传内容的ContentType，适用于“单个文件或图片变量（二进制）”或“纯文本” 请求体类型。 | (0)字符串-Text |  | False |
| resultType | 结果类型 | Http请求的结果类型 | (9)选项-Enum（Text: 文本, Image: 图片, File: 文件） | Text | True |
| ua | UserAgent |  | (0)字符串-Text | Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/112.0.0.0 Safari/537.36 | False |
| expireSeconds | 超时时间 | 请求超时时间（秒数） | (1)数字(小数)-Number | 100 | False |
| noAutoRedirect | 禁止重定向 | 是否禁止自动跳转 | (2)布尔值-Boolean | False | False |
| showProgress | 显示进度条 | 是否显示上传下载进度条 | (2)布尔值-Boolean | False | False |
| skipCertVerify | 忽略HTTPS证书验证 |  | (2)布尔值-Boolean | False | False |
| forceProxy | 强制使用代理 | 即使系统设置中未启用代理，本步骤仍然使用代理访问。 | (2)布尔值-Boolean | False | False |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |
| useSSE | 启用SSE流式响应 | 调用AI接口时使用，通过子程序处理接收到的流式响应内容 | (2)布尔值-Boolean | False | False |
| sseSpName | SSE流式响应处理子程序 | 用于处理接收到的流式响应消息，每次收到调用一次，通过data输入变量接收内容。 | (0)字符串-Text |  | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 是否操作成功 | (2)布尔值-Boolean |
| statusCode | 状态码 | 返回的http请求状态码 | (12)数字(整数)-Integer |
| respHeaders | 响应头 | 返回的HTTP响应Headers | (10)词典-Dict |
| respCookies | 响应Cookies | 返回的Cookies | (10)词典-Dict |
| content | 文本结果 | 返回的文本内容 | (0)字符串-Text |
| imgResult | 图片结果 | 返回的图片内容 | (3)图片-Image |

</details>
<details>
<summary>范例</summary>


**获取选中文本，判断选中文本是否以“熊曰开头”，是的话HTTP请求进行解密，否则HTTP请求进行加密。最后将返回的文本发送到窗口中去**
```json
{
  "Variables": [
    {
      "Key": "熊曰",
      "Type": 0,
      "Desc": "默认的文本变量",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "原始文本",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:getSelectedText",
      "InputParams": {
        "format": {
          "VarKey": null,
          "Value": "UnicodeText"
        },
        "repeat": {
          "VarKey": null,
          "Value": "2"
        },
        "useActionParam": {
          "VarKey": null,
          "Value": "1"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "output": "原始文本",
        "outputEncoded": null,
        "url": null,
        "isSuccess": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "http://hi.pcmoe.net/index.html"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:if",
      "InputParams": {
        "condition": {
          "VarKey": null,
          "Value": "$= {原始文本}.IndexOf(\"熊曰：\", StringComparison.OrdinalIgnoreCase) >= 0"
        }
      },
      "OutputParams": {},
      "IfSteps": [
        {
          "StepRunnerKey": "sys:comment",
          "InputParams": {
            "note": {
              "VarKey": null,
              "Value": "解密"
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:http",
          "InputParams": {
            "url": {
              "VarKey": null,
              "Value": "http://hi.pcmoe.net/bear.php"
            },
            "method": {
              "VarKey": null,
              "Value": "POST"
            },
            "header": {
              "VarKey": null,
              "Value": "connection:keep-alive\r\nx-requested-with:XMLHttpRequest\r\ndnt:1\r\nx-token:07B97AA644E8\r\naccept:*/*\r\nreferer:http://hi.pcmoe.net/index.html\r\naccept-language:zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7"
            },
            "cookie": {
              "VarKey": null,
              "Value": ""
            },
            "bodyType": {
              "VarKey": null,
              "Value": "FORM"
            },
            "body": {
              "VarKey": null,
              "Value": "$$mode=Bear&code=Decode&txt={原始文本}"
            },
            "contentType": {
              "VarKey": null,
              "Value": ""
            },
            "resultType": {
              "VarKey": null,
              "Value": "Text"
            },
            "ua": {
              "VarKey": null,
              "Value": "Mozilla/5.0 (Linux; Android 6.0; Nexus 5 Build/MRA58N) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/93.0.4577.63 Mobile Safari/537.36 Edg/93.0.961.38"
            },
            "expireSeconds": {
              "VarKey": null,
              "Value": "100"
            },
            "noAutoRedirect": {
              "VarKey": null,
              "Value": "0"
            },
            "showProgress": {
              "VarKey": null,
              "Value": "0"
            },
            "skipCertVerify": {
              "VarKey": null,
              "Value": "0"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "isSuccess": null,
            "statusCode": null,
            "respHeaders": null,
            "respCookies": null,
            "content": "熊曰",
            "imgResult": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": [
        {
          "StepRunnerKey": "sys:comment",
          "InputParams": {
            "note": {
              "VarKey": null,
              "Value": "加密"
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:stringProcess",
          "InputParams": {
            "data": {
              "VarKey": "原始文本",
              "Value": null
            },
            "method": {
              "VarKey": null,
              "Value": "urlEncode"
            },
            "srcEncoding": {
              "VarKey": null,
              "Value": "utf-8"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "output": "原始文本",
            "isSuccess": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:http",
          "InputParams": {
            "url": {
              "VarKey": null,
              "Value": "http://hi.pcmoe.net/bear.php"
            },
            "method": {
              "VarKey": null,
              "Value": "POST"
            },
            "header": {
              "VarKey": null,
              "Value": "connection:keep-alive\r\nx-requested-with:XMLHttpRequest\r\ndnt:1\r\nx-token:07B97AA644E8\r\naccept:*/*\r\nreferer:http://hi.pcmoe.net/index.html\r\naccept-language:zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7"
            },
            "cookie": {
              "VarKey": null,
              "Value": ""
            },
            "bodyType": {
              "VarKey": null,
              "Value": "FORM"
            },
            "body": {
              "VarKey": null,
              "Value": "$$mode=Bear&code=Encode&txt={原始文本}"
            },
            "contentType": {
              "VarKey": null,
              "Value": ""
            },
            "resultType": {
              "VarKey": null,
              "Value": "Text"
            },
            "ua": {
              "VarKey": null,
              "Value": "Mozilla/5.0 (Linux; Android 6.0; Nexus 5 Build/MRA58N) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/93.0.4577.63 Mobile Safari/537.36 Edg/93.0.961.38"
            },
            "expireSeconds": {
              "VarKey": null,
              "Value": "100"
            },
            "noAutoRedirect": {
              "VarKey": null,
              "Value": "0"
            },
            "showProgress": {
              "VarKey": null,
              "Value": "0"
            },
            "skipCertVerify": {
              "VarKey": null,
              "Value": "0"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "isSuccess": null,
            "statusCode": null,
            "respHeaders": null,
            "respCookies": null,
            "content": "熊曰",
            "imgResult": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:outputText",
      "InputParams": {
        "content": {
          "VarKey": "熊曰",
          "Value": null
        },
        "method": {
          "VarKey": null,
          "Value": "paste"
        },
        "delayBeforePaste": {
          "VarKey": null,
          "Value": "50"
        },
        "delayAfterPaste": {
          "VarKey": null,
          "Value": "10"
        },
        "appendReturn": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 22.如果/否则

**功能描述**
> 依据条件执行操作

**官方文档**
> https://getquicker.net/KC/Help/Doc/if

**内部名称**
> sys:if

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| condition | 如果 | 是否符合指定的条件 | (2)布尔值-Boolean |  | False |

</details>
<details>
<summary>传出参数</summary>
无
</details>
<details>
<summary>范例</summary>

见其他模块相关即可

</details>

***

## 23.模拟按键A（录入）

**功能描述**
> 模拟键盘输入

**官方文档**
> https://getquicker.net/KC/Help/Doc/keyinput

**内部名称**
> sys:keyInput

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| keys | 按键 | 模拟的按键内容 | (7)按键码 |  | True |
| repeat | 重复次数 |  | (12)数字(整数)-Integer | 1 | False |
| interval | 重复间隔(毫秒) | 每次重复之间的间隔毫秒数 | (12)数字(整数)-Integer | 1 | False |
| holdMs | 保持毫秒数 | 普通键（非Ctrl/Alt/Shift/Win）在抬起前保持的时间。-1表示使用默认设置。
 某些直接模拟按键无法生效的软件中可以尝试增加此值。 | (12)数字(整数)-Integer | -1 | False |

</details>
<details>
<summary>传出参数</summary>
无
</details>
<details>
<summary>范例</summary>

**模拟按下LeftAlt+LeftCtrl+LeftShift+G并循环3次，每次间隔20毫秒**
```json
{
  "Variables": [],
  "Steps": [
    {
      "StepRunnerKey": "sys:keyInput",
      "InputParams": {
        "keys": {
          "VarKey": null,
          "Value": "{\"CtrlKeys\":[164,162,160],\"Keys\":[71]}"
        },
        "repeat": {
          "VarKey": null,
          "Value": "3"
        },
        "interval": {
          "VarKey": null,
          "Value": "20"
        },
        "holdMs": {
          "VarKey": null,
          "Value": "-1"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 24.鼠标输入

**功能描述**
> 模拟鼠标输入

**官方文档**
> https://getquicker.net/KC/Help/Doc/mouse

**内部名称**
> sys:mouse

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| type | 类型 | 操作类型 | (9)选项-Enum（restore: 还原鼠标位置; move: 移动距离; moveTo: 移动到(x,y分别指定); moveToXy: 移动到(x,y一同指定); click: 单击; dbclick: 双击; down: 按下; up: 抬起; scroll: 滚动; ctrlDown: 按下Ctrl; ctrlUp: 松开Ctrl; shiftDown: 按下Shift; shiftUp: 松开Shift; toWinTL: 移动到窗口位置：相对于窗口左上角; toWinTR: 移动到窗口位置：相对于窗口右上角; toWinBL: 移动到窗口位置：相对于窗口左下角; toWinBR: 移动到窗口位置：相对于窗口右下角; toWinCenter: 移动到窗口位置：窗口中心; moveToWinXy: 移动到窗口位置：xy一同指定; locateByBitmap: 移动到位图位置(图片文件); locateByBitmapVar: 移动到位图位置(图片变量); getMouseOriginPosition: 获取鼠标位置(弹出面板前位置); getMouseCurrentPosition: 获取鼠标位置及指针类型(当前位置); showIndicator: 显示鼠标位置提示） | restore | True |
| hWnd | 窗口句柄 | 目标窗口的句柄。留空或 0 表示操作前台窗口。 | (12)数字(整数)-Integer |  | False |
| btn | 按钮 | 操作哪个按钮 | (9)选项-Enum（left: 左键; right: 右键; middle: 中键; x1: X1; x2: X2） | left | True |
| bmp | 位图路径 | 需要在屏幕中查找的位图路径。位图必须和屏幕图像完全匹配，不能压缩。此时X、Y的值为相对于搜索位图的左上角的偏移。 | (0)字符串-Text |  | True |
| bmpVar | 位图变量 | 需要在屏幕中查找的位图。位图必须和屏幕图像完全匹配，不能压缩。此时X、Y的值为相对于搜索位图的左上角的偏移。 | (3)图片-Image |  | True |
| bmpTargetType | 查找范围 | 位图查找范围 | (9)选项-Enum（MainScreen: 主屏幕; CurrentWindow: 当前窗口; Rect: 坐标范围） | MainScreen | False |
| searchRect | 查找坐标范围 | 当“查找范围”为“坐标范围”时有效，格式为：left,top,right,bottom | (0)字符串-Text |  | False |
| bmpPosition | 定位位置 | 查找到图片后，鼠标指针移动到的位置 | (9)选项-Enum（Center: 位图中间; TopLeft: 左上角; TopRight: 右上角; BottomLeft: 左下角; BottomRight: 右下角） | Center | False |
| bmpColorError | 颜色容差 | 匹配像素时允许每个颜色通道的偏差值0-100，0表示精确匹配，速度最快。 | (12)数字(整数)-Integer | 10 | False |
| maxFindCount | 最大匹配数量 | 找图的最大匹配数量。将对每个查找到的目标执行附加动作。 | (12)数字(整数)-Integer | 1 | False |
| retryCount | 重试次数 | 未找到位图时的重试次数。每次重试间隔300ms。 | (12)数字(整数)-Integer | 1 | False |
| x | X | 水平方向的坐标/坐标偏移/移动距离(像素) 或 滚动数量（clicks。正值向右，负值向左） | (12)数字(整数)-Integer | 0 | True |
| y | Y | 垂直方向的坐标/坐标偏移/移动距离 或 滚动数量（clicks。正值向前，负值向后） | (12)数字(整数)-Integer | 0 | True |
| xy | 坐标 | 格式为：x,y，如：100,200。也可以使用百分比表示，如：50%,50% 表示屏幕中心。 | (0)字符串-Text |  | True |
| xyForWin | 相对坐标 | 格式为：x,y，如：100,200（相对于窗口左上角向右100，向下200）。也可以使用百分比表示，如：50%,50% 表示窗口中心。 | (0)字符串-Text |  | True |
| slowMove | 逐渐移动到目标 | 逐渐移动而不是直接移动到目标位置。 | (2)布尔值-Boolean | False | False |
| extAction | 移动后操作 | 移动位置后，需要执行的动作 | (9)选项-Enum（none: 无; left: 左键单击; leftDbClick: 左键双击; right: 右键单击; middle: 中键单击） | none | True |
| restoreMousePos | 操作完成后恢复鼠标位置 |  | (2)布尔值-Boolean | False | False |
| stopIfFail | 失败后中止动作 | 获取位置失败后，是否停止后续动作的执行。 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 找图定位是否成功 |  | (2)布尔值-Boolean |
| mouseLocation | 鼠标位置 | 格式为X,Y的文本 | (0)字符串-Text |
| mouseX | 鼠标位置X | 鼠标位置X坐标 | (12)数字(整数)-Integer |
| mouseY | 鼠标位置Y | 鼠标位置Y坐标 | (12)数字(整数)-Integer |
| cursorType | 光标类型 | 当前的鼠标指针形状类型 | (0)字符串-Text |

</details>
<details>
<summary>范例</summary>

**鼠标移动到200,300并双击鼠标左键然后回到原位，接着逐渐移动到500,800并单击鼠标中键**
```json
{
  "Variables": [],
  "Steps": [
    {
      "StepRunnerKey": "sys:mouse",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "moveToXy"
        },
        "xy": {
          "VarKey": null,
          "Value": "200,300"
        },
        "slowMove": {
          "VarKey": null,
          "Value": "0"
        },
        "extAction": {
          "VarKey": null,
          "Value": "leftDbClick"
        },
        "restoreMousePos": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:mouse",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "moveToXy"
        },
        "xy": {
          "VarKey": null,
          "Value": "500,800"
        },
        "slowMove": {
          "VarKey": null,
          "Value": "1"
        },
        "extAction": {
          "VarKey": null,
          "Value": "middle"
        },
        "restoreMousePos": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 25.提示消息

**功能描述**
> 显示可以自动消失的消息提示。

**官方文档**
> https://getquicker.net/KC/Help/Doc/notify

**内部名称**
> sys:notify

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| type | 类型 | 消息的类型 | (9)选项-Enum（Success: 成功; Info: 信息; Warning: 告警; Error: 错误; WindowsToast: Windows 通知 (win10+)） | Info | True |
| msg | 消息内容 | 显示的消息内容 | (0)字符串-Text |  | True |
| maxLines | 最大行数 | 显示内容的最大行数，0表示不限 | (12)数字(整数)-Integer | 0 | True |
| style | 风格 |  | (9)选项-Enum（Default: 默认（显示在屏幕底部）; Style2: 风格2（显示在屏幕右侧）） | Default | True |
| clickAction | 点击命令 | 点击时运行命令（如网址等可以在Win+R中执行的文本，仅支持默认风格提示）。默认为复制提示文字。 | (0)字符串-Text |  | False |

</details>
<details>
<summary>传出参数</summary>
无
</details>
<details>
<summary>范例</summary>

**弹出一条“此消息可点击”的通知，点击后带参（当前动作标题）运行当前动作，并提示**
```json
{
  "Variables": [],
  "Steps": [
    {
      "StepRunnerKey": "sys:if",
      "InputParams": {
        "condition": {
          "VarKey": null,
          "Value": "$={quicker_in_param}!=\"\""
        }
      },
      "OutputParams": {},
      "IfSteps": [
        {
          "StepRunnerKey": "sys:notify",
          "InputParams": {
            "type": {
              "VarKey": null,
              "Value": "Info"
            },
            "msg": {
              "VarKey": null,
              "Value": "$${quicker_in_param}"
            },
            "maxLines": {
              "VarKey": null,
              "Value": "0"
            },
            "style": {
              "VarKey": null,
              "Value": "Default"
            },
            "clickAction": {
              "VarKey": null,
              "Value": ""
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": [
        {
          "StepRunnerKey": "sys:notify",
          "InputParams": {
            "type": {
              "VarKey": null,
              "Value": "Info"
            },
            "msg": {
              "VarKey": null,
              "Value": "此消息可点击"
            },
            "maxLines": {
              "VarKey": null,
              "Value": "0"
            },
            "style": {
              "VarKey": null,
              "Value": "Default"
            },
            "clickAction": {
              "VarKey": null,
              "Value": "$=\"quicker:runaction:\" + _context.ActionId + \"?\" + _context.ActionTitle"
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 26.比较数字

**功能描述**
> 比较数字大小。

**官方文档**
> https://getquicker.net/KC/Help/Doc/numcompare

**内部名称**
> sys:numCompare

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| param1 | 数字1 | 左侧的数字 | (1)数字(小数)-Number | 0 | True |
| type | 类型 | 比较方式 | (9)选项-Enum（>; >=; =; <; <=） | > | True |
| param2 | 数字2 | 右侧的数字 | (1)数字(小数)-Number | 0 | True |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| value | 值 | 比较结果是否为真 | (2)布尔值-Boolean |

</details>
<details>
<summary>范例</summary>

**判断数字1是否大于等于3**
```json
{
  "Variables": [
    {
      "Key": "value",
      "Type": 2,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:numCompare",
      "InputParams": {
        "param1": {
          "VarKey": null,
          "Value": "1"
        },
        "type": {
          "VarKey": null,
          "Value": ">="
        },
        "param2": {
          "VarKey": null,
          "Value": "3"
        }
      },
      "OutputParams": {
        "value": "value"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 27.打开网址

**功能描述**
> 打开指定的网址

**官方文档**
> https://getquicker.net/KC/Help/Doc/openurl

**内部名称**
> sys:openUrl

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| url | 网址 | 要打开的网页地址 | (0)字符串-Text | https:// | True |
| browser | 浏览器 | 使用什么浏览器打开网址 | (9)选项-Enum | default | True |
| exePath | 浏览器程序路径 | 浏览器exe程序路径 | (0)字符串-Text |  | True |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |

</details>
<details>
<summary>范例</summary>


**默认浏览器打开https://www.baidu.com**
```json
{
  "Variables": [],
  "Steps": [
    {
      "StepRunnerKey": "sys:openUrl",
      "InputParams": {
        "url": {
          "VarKey": null,
          "Value": "https://www.baidu.com"
        },
        "browser": {
          "VarKey": null,
          "Value": "default"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 28.发送文本到窗口

**功能描述**
> 将文本输出到活动窗口中

**官方文档**
> https://getquicker.net/KC/Help/Doc/outputtext

**内部名称**
> sys:outputText

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| content | 内容 | 要输出的内容 | (0)字符串-Text |  | True |
| method | 方法 | 发送内容使用的方法 | (9)选项-Enum（input: 模拟输入; paste: 复制到剪贴板后粘贴(Ctrl+V)） | paste | True |
| delayBeforePaste | 粘贴前延时 | 毫秒数。写入剪贴板以后，等待指定的时间后再发送粘贴按键(Ctrl+V) | (12)数字(整数)-Integer | 50 | False |
| delayAfterPaste | 粘贴后延时 | 毫秒数。发送粘贴按键(Ctrl+V)之后等待的毫秒数 | (12)数字(整数)-Integer | 10 | False |
| delayBetweenChar | 字符间延迟 | 模拟输入下一个字符之前等待的毫秒数。 | (12)数字(整数)-Integer | 0 | False |
| appendReturn | 在末尾添加回车 | 发送内容后，在末尾输入回车 | (2)布尔值-Boolean | False | False |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 步骤是否成功 | 步骤是否成功完成 | (2)布尔值-Boolean |

</details>
<details>
<summary>范例</summary>

**模拟输入Quicker123到窗口中去，每个字符之间等待3毫秒，输入完毕后添加回车**
```json
{
  "Variables": [],
  "Steps": [
    {
      "StepRunnerKey": "sys:outputText",
      "InputParams": {
        "content": {
          "VarKey": null,
          "Value": "Quicker123"
        },
        "method": {
          "VarKey": null,
          "Value": "input"
        },
        "delayBetweenChar": {
          "VarKey": null,
          "Value": "3"
        },
        "appendReturn": {
          "VarKey": null,
          "Value": "1"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 29.播放声音

**功能描述**
> 播放声音提示或声音文件。

**官方文档**
> https://getquicker.net/KC/Help/Doc/playsound

**内部名称**
> sys:playSound

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| type | 类型 |  | (9)选项-Enum（LOCAL: 内置声音提示; EXTERN: 电脑文件或网络文件; TTS: 朗读文本（系统TTS）） | LOCAL | False |
| localSound | 提示音类型 |  | (9)选项-Enum（info: 信息; snip: 截图; succeed: 成功; warning: 警告; wrong: 错误） | info | False |
| uri | 路径或URL | 音乐文件的本地路径或网址。 | (0)字符串-Text |  | False |
| text | 文本内容 | 需要朗读的文本。 | (0)字符串-Text |  | False |
| wait | 等待播放完成 |  | (2)布尔值-Boolean |  | False |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |

</details>
<details>
<summary>范例</summary>

**播放内置声音提示：成功，并等待播放完成**
```json
{
  "Variables": [],
  "Steps": [
    {
      "StepRunnerKey": "sys:playSound",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "LOCAL"
        },
        "localSound": {
          "VarKey": null,
          "Value": "succeed"
        },
        "wait": {
          "VarKey": null,
          "Value": "1"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 30.Quicker操作

**功能描述**
> 调用Quicker的某个功能

**官方文档**
> https://getquicker.net/KC/Help/Doc/quickeroperations

**内部名称**
> sys:quickeroperations

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| type | 类型 | 操作类型 | (9)选项-Enum（showPanel: 显示面板; showSearch: 显示搜索框; closeSearch: 关闭搜索框; showCircleMenu: 显示轮盘菜单 (点击); togglePause: 禁用/启用; runLastAction: 运行最后使用的动作; startAppVoiceInput: 启动App语音输入; stopAllActions: 停止运行中的动作; reinstallMouseHook: 重新加载键鼠挂钩; ResetKeyboard: 重置键盘状态; showDashboardWindow: 显示仪表盘窗口; toggleTextFloatWindow: 开启/关闭文本悬浮窗功能; showConfigWindow: 显示配置窗口; showExeSettingWindow: 显示场景与动作管理窗口; closeAllFloatWindow: 关闭所有悬浮按钮; loadProfile: 加载动作页; loadExeProfiles: 加载指定应用程序的所有动作页（锁定切换）; loadExeProfilesNoLock: 加载指定应用程序的所有动作页（不锁定切换）; ToggleLockPanel: 锁定/解锁 动作页自动切换; editAction: 编辑动作; RestartQuicker: 重启Quicker; SetPushActiveClient: 推送服务：设置为活动客户端; StartSearchWithAction: 使用当前动作进行实时搜索; SearchWithCertainAction: 使用指定动作进行实时搜索; operation_show_context_menu: 显示剪贴板上下文菜单; LoadSkin: 加载外观/切换主题(专业版功能); ExitQuicker: 退出Quicker; FloatAction: 悬浮动作(专业版功能); ToggleFloatButtons: 切换所有悬浮按钮显示; ShowHideImageWindows: 显示或隐藏所有图片窗口; RemoveAction: 删除当前动作; GetActionInfo: 根据ID获取动作信息） | showPanel | True |
| profileId | 动作页ID | 请在场景与动作管理中，查看动作页信息获取ID。 | (0)字符串-Text |  | True |
| actionId | 动作ID或名称 | 在动作上点右键->信息可以查看动作信息。使用名称时不能有重名动作。获取动作信息时仅可填写动作Id。编辑动作时，使用%%id或%%name格式，可用于编辑公共子程序。 | (0)字符串-Text |  | True |
| position | 位置 | 坐标，格式为：left,top | (0)字符串-Text | 200,200 | True |
| exe | 场景标识 | 场景关联的exe文件名。请参考场景与动作管理窗口左侧应用列表。 | (0)字符串-Text |  | True |
| activatePointWindow | 自动激活鼠标位置窗口 |  | (2)布尔值-Boolean | 0 | False |
| followMousePosition | 跟随鼠标位置 |  | (2)布尔值-Boolean | True | False |
| searchText | 预置的搜索内容 | 预先放入搜索框的内容 | (0)字符串-Text |  | False |
| skinId | 外观ID | 请在外观网页中复制外观ID | (0)字符串-Text |  | True |
| theme | 主题模式 | 可选切换为浅色或暗色模式 | (9)选项-Enum（"": 不改变; auto: 跟随Windows; light: 浅色; dark: 暗色; toggle: 切换浅色和暗色） |  | False |
| viewMode | 显示状态 |  | (9)选项-Enum（HideAll: 隐藏全部; ByProcess: 自动(按关联进程切换); ShowAll: 显示全部; ToggleHideAndAuto: 切换隐藏和自动） | ByProcess | False |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 步骤是否成功 | 步骤是否成功完成 | (2)布尔值-Boolean |
| actionList | 动作列表 |  | (4)文本列表-List |
| actionTitle | 动作标题 |  | (0)字符串-Text |
| actionIcon | 动作图标 |  | (0)字符串-Text |

</details>
<details>
<summary>范例</summary>

**打开Quicker配置窗口**
```json
{
  "Variables": [],
  "Steps": [
    {
      "StepRunnerKey": "sys:quickeroperations",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "showConfigWindow"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 31.重复

**功能描述**
> 循环指定的次数，或符合某个条件时中止

**官方文档**
> https://getquicker.net/KC/Help/Doc/repeat

**内部名称**
> sys:repeat

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| count | 次数 | 重复次数，除非符合条件提前中止。-1表示无限循环。 | (12)数字(整数)-Integer | 1 | False |
| stopCondition | 中止条件 | 选填。条件满足时停止循环（每次循环开始时检查）。 | (2)布尔值-Boolean |  | False |
| startIndex | 计数开始值 | 计数序号的开始值，通常应该为0。 | (12)数字(整数)-Integer | 0 | False |
| repeatDelayMs | 循环间隔时间 | 每次循环之间的间隔毫秒数。如果为0，请确保循环内部有其他等待步骤，避免连续循环占用较多资源。 | (12)数字(整数)-Integer | 1 | False |
| progressBarTitle | 进度条标题 | 如果设置了此参数，则在循环过程中会显示一个进度条，标题为此参数的值。 | (0)字符串-Text |  | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| count | 计数 | 计数序号，表示第几次循环。 | (12)数字(整数)-Integer |

</details>
<details>
<summary>范例</summary>

**循环100次，每次间隔30毫秒，当前运行次数为count变量，当count等于50时终止循环**
```json
{
  "Variables": [
    {
      "Key": "count",
      "Type": 12,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:repeat",
      "InputParams": {
        "count": {
          "VarKey": null,
          "Value": "100"
        },
        "stopCondition": {
          "VarKey": null,
          "Value": "$={count}==50"
        },
        "startIndex": {
          "VarKey": null,
          "Value": "0"
        },
        "repeatDelayMs": {
          "VarKey": null,
          "Value": "30"
        },
        "progressBarTitle": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {
        "count": "count"
      },
      "IfSteps": [
        {
          "StepRunnerKey": "sys:notify",
          "InputParams": {
            "type": {
              "VarKey": null,
              "Value": "Info"
            },
            "msg": {
              "VarKey": "count",
              "Value": null
            },
            "maxLines": {
              "VarKey": null,
              "Value": "0"
            },
            "style": {
              "VarKey": null,
              "Value": "Default"
            },
            "clickAction": {
              "VarKey": null,
              "Value": ""
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 32.显示进度条

**功能描述**
> 显示/更新进度条

**官方文档**
> https://getquicker.net/KC/Help/Doc/reportProgress

**内部名称**
> sys:reportProgress

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| type | 类型 | 操作类型 | (9)选项-Enum（REQUEST_ID: 创建进度条; UPDATE_PROGRESS: 更新进度; REMOVE: 去除进度条） | REQUEST_ID | True |
| progressId | 进度条ID | 进度条的序号，用于后续更新或删除进度条 | (12)数字(整数)-Integer | 0 | False |
| title | 进度条标题 | 进度条的标题(显示在进度条上方) | (0)字符串-Text |  | False |
| percentage | 进度百分比 | 0到100之间的数字 | (1)数字(小数)-Number | 0 | False |
| text | 说明文字 | 显示在进度条下方 | (0)字符串-Text |  | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| progressId | 进度条ID | 进度条的序号，用于后续更新或删除进度条 | (12)数字(整数)-Integer |

</details>
<details>
<summary>范例</summary>

**创建一个进度条，ID为progressId。创建一个循环100次的循环，每次间隔30毫秒，当前运行次数为count变量，每次运行更新进度条：标题为循环100次，底部文字为“这是一行底部说明文字”，当count等于50时终止循环，循环结束后移除进度条**
```json
{
  "Variables": [
    {
      "Key": "count",
      "Type": 12,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "progressId",
      "Type": 12,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:reportProgress",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "REQUEST_ID"
        }
      },
      "OutputParams": {
        "progressId": "progressId"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:repeat",
      "InputParams": {
        "count": {
          "VarKey": null,
          "Value": "100"
        },
        "stopCondition": {
          "VarKey": null,
          "Value": "$={count}==50"
        },
        "startIndex": {
          "VarKey": null,
          "Value": "0"
        },
        "repeatDelayMs": {
          "VarKey": null,
          "Value": "30"
        },
        "progressBarTitle": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {
        "count": "count"
      },
      "IfSteps": [
        {
          "StepRunnerKey": "sys:reportProgress",
          "InputParams": {
            "type": {
              "VarKey": null,
              "Value": "UPDATE_PROGRESS"
            },
            "progressId": {
              "VarKey": "progressId",
              "Value": null
            },
            "title": {
              "VarKey": null,
              "Value": "循环100次"
            },
            "percentage": {
              "VarKey": "count",
              "Value": null
            },
            "text": {
              "VarKey": null,
              "Value": "这是一行底部说明文字"
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:notify",
          "InputParams": {
            "type": {
              "VarKey": null,
              "Value": "Info"
            },
            "msg": {
              "VarKey": "count",
              "Value": null
            },
            "maxLines": {
              "VarKey": null,
              "Value": "0"
            },
            "style": {
              "VarKey": null,
              "Value": "Default"
            },
            "clickAction": {
              "VarKey": null,
              "Value": ""
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:reportProgress",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "REMOVE"
        },
        "progressId": {
          "VarKey": "progressId",
          "Value": null
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 33.恢复活动窗口

**功能描述**
> 如果活动窗口改变了（比如使用了参数输入步骤）,使用此动作恢复窗口焦点。

**官方文档**
> https://getquicker.net/KC/Help/Doc/restoreactivewindow

**内部名称**
> sys:restoreActiveWindow

<details>
<summary>传入参数</summary>
无
</details>
<details>
<summary>传出参数</summary>
无
</details>
<details>
<summary>范例</summary>

```json
{
  "Variables": [],
  "Steps": [
    {
      "StepRunnerKey": "sys:restoreActiveWindow",
      "InputParams": {},
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": null,
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 34.运行或停止动作

**功能描述**
> 执行指定的其他动作

**官方文档**
> https://getquicker.net/KC/Help/Doc/runaction

**内部名称**
> sys:runAction

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| type | 类型 | 操作类型 | (9)选项-Enum（StartAction: 运行动作; StopAction: 停止动作; ShowActionContextMenu: 显示动作右键菜单; StartCurrentAction: 运行当前动作（注意避免产生循环或递归）; StopOtherInstance: 停止当前动作的其它实例; GetRunningActionCount: 获取动作运行个数（自己编写动作时可用）） | StartAction | True |
| actionId | 目标动作 | 要运行的其他动作的ID或名称(使用名称时需要完全匹配且不能有重名动作) | (0)字符串-Text |  | True |
| onlyCustomMenu | 仅显示动作的自定义菜单 | 不显示编辑、复制等菜单 | (2)布尔值-Boolean | False | False |
| inputParam | 命令参数 | 传递给目标动作的参数。存储在该动作的quicker_in_param变量中。 | (0)字符串-Text |  | True |
| wait | 等待运行结束 | 是否等待此动作运行结束再执行后续动作（如需获取目标动作的输出，需选中此项） | (2)布尔值-Boolean | True | False |
| debug | 调试模式运行 | 是否以调试模式运行动作 | (2)布尔值-Boolean | False | False |
| hideMessage | 不显示提示消息 | 仅对非动作库安装的动作有效 | (2)布尔值-Boolean | False | False |
| stopIfFail | 失败后停止 | 如果未找到目标动作，是否停止当前动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| actionTitle | 动作名称 | 运行的动作名称。 | (0)字符串-Text |
| count | 运行个数 | 动作正在运行的个数 | (1)数字(小数)-Number |
| output | 动作输出 | 被调用动作的输出。 | (0)字符串-Text |

</details>
<details>
<summary>范例</summary>

**本动作中有2个步骤。1：停止当前动作的其他实例；2：带参数“123”以“调试模式”运行“窗口测试”动作，并等待动作运行结束**
```json
{
  "Variables": [],
  "Steps": [
    {
      "StepRunnerKey": "sys:runAction",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "StopOtherInstance"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:runAction",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "StartAction"
        },
        "actionId": {
          "VarKey": null,
          "Value": "窗口测试"
        },
        "inputParam": {
          "VarKey": null,
          "Value": "123"
        },
        "wait": {
          "VarKey": null,
          "Value": "1"
        },
        "debug": {
          "VarKey": null,
          "Value": "1"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "actionTitle": null,
        "output": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 35.运行或打开

**功能描述**
> 运行软件或命令，打开文件、文件夹或网址。效果类似于在Windows“运行”对话框中执行命令。

**官方文档**
> https://getquicker.net/KC/Help/Doc/run

**内部名称**
> sys:run

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| path | 路径或命令 | 要运行的命令或打开的文件路径、网址、URI等。 | (0)字符串-Text |  | True |
| arg | 参数(可选) | 程序参数 | (0)字符串-Text |  | False |
| setWorkingDir | 工作目录 | 可输入 0或留空(不设置,由windows默认)、1(软件所在目录)、具体的工作目录路径。 | (0)字符串-Text | 1 | False |
| windowStyle | 窗口风格 | 设置期望的窗口风格，是否有效依赖于具体的软件。 | (9)选项-Enum（0: 普通(Normal); 1: 隐藏(Hidden); 2: 最小化(Minimized); 3: 最大化(Maximized)） | 0 | False |
| runas | 以管理员身份运行 | 以管理员身份运行软件或命令。 | (2)布尔值-Boolean | False | False |
| waitInputIdle | 等待启动完成 | 等待进程完成后了初始化，可以接受用户输入。 | (2)布尔值-Boolean | False | False |
| waitExit | 等待进程结束 | 等待进程结束后再执行后续操作步骤。 | (2)布尔值-Boolean | False | False |
| activateWindowIfRunning | 如果程序已运行则尝试激活窗口 | 如果程序已经在运行，则尝试激活其窗口。 | (2)布尔值-Boolean | False | False |
| activateWindowHotkey | 激活窗口快捷键 | 对于支持快捷键激活窗口的软件，设置该快捷键。支持“模拟按键B”语法。 | (0)字符串-Text |  | False |
| alternativePath | 备用路径 | 文件在多个电脑上路径不同时，使用备用路径填写其他电脑上的文件路径。 | (0)字符串-Text |  | False |
| username | 用户名 | 使用指定的用户运行 | (0)字符串-Text |  | False |
| password | 密码 | 用户名对应的密码 | (0)字符串-Text |  | False |
| outputEncoding | 控制台输出编码 | 控制台输出编码。如果输出遇到乱码，尝试修改此选项。 | (9)选项-Enum（utf8: UTF8; oem: OEM） | oem | True |
| envVariables | 环境变量 | 为应用程序设置特定的环境变量值。每行一个，格式“变量名=值”，如“CONFIG_FILE=d:\config.json” | (0)字符串-Text |  | False |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| pid | PID | 进程ID | (12)数字(整数)-Integer |
| mainWinHandle | 主窗口句柄 | 进程的主窗口句柄 | (12)数字(整数)-Integer |
| mainWinTitle | 主窗口标题 |  | (0)字符串-Text |
| stdout | 控制台输出 | 慎用！仅用于控制台程序，会自动等待进程结束。输出stdout，为空时输出stderr。 | (0)字符串-Text |
| stdoutOnly | stdout输出 | 慎用！捕获控制台程序的stdout输出，会自动等待进程结束 | (0)字符串-Text |
| stderr | stderr输出 | 慎用！捕获控制台程序的stderr输出，会自动等待进程结束 | (0)字符串-Text |
| exitCode | 退出代码 | 进程的ExitCode，会自动等待进程结束。 | (12)数字(整数)-Integer |

</details>
<details>
<summary>范例</summary>

**带参数“123”以管理员身份最小化运行“XX.exe”，返回主窗口句柄mainWinHandle，工作目录为软件所在目录，等待进程启动完成和启动结束后执行下一个步骤（输出“启动完毕”）**
```json
{
  "Variables": [
    {
      "Key": "mainWinHandle",
      "Type": 12,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:run",
      "InputParams": {
        "path": {
          "VarKey": null,
          "Value": "XX.exe"
        },
        "arg": {
          "VarKey": null,
          "Value": "123"
        },
        "runas": {
          "VarKey": null,
          "Value": "true"
        },
        "activateWindowIfRunning": {
          "VarKey": null,
          "Value": "false"
        },
        "activateWindowHotkey": {
          "VarKey": null,
          "Value": ""
        },
        "alternativePath": {
          "VarKey": null,
          "Value": ""
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        },
        "setWorkingDir": {
          "VarKey": null,
          "Value": "1"
        },
        "windowStyle": {
          "VarKey": null,
          "Value": "2"
        },
        "waitInputIdle": {
          "VarKey": null,
          "Value": "true"
        },
        "waitExit": {
          "VarKey": null,
          "Value": "true"
        },
        "username": {
          "VarKey": null,
          "Value": ""
        },
        "password": {
          "VarKey": null,
          "Value": ""
        },
        "outputEncoding": {
          "VarKey": null,
          "Value": "oem"
        },
        "envVariables": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "pid": null,
        "mainWinHandle": "mainWinHandle",
        "mainWinTitle": null,
        "stdout": null,
        "stdoutOnly": null,
        "stderr": null,
        "exitCode": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:notify",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "Info"
        },
        "msg": {
          "VarKey": null,
          "Value": "启动完毕"
        },
        "maxLines": {
          "VarKey": null,
          "Value": "0"
        },
        "style": {
          "VarKey": null,
          "Value": "Default"
        },
        "clickAction": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 36.屏幕找图/找色/找字

**功能描述**
> 在屏幕上查找图片里的内容出现的位置

**官方文档**
> https://getquicker.net/KC/Help/Doc/searchBmp

**内部名称**
> sys:searchBmp

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| type | 类型 | 操作类型 | (9)（locateByBitmapFile: 查找图片(文件); locateByBitmapVar: 查找图片(变量); locateByColor: 查找颜色; locateByText: 查找文字） | locateByBitmapFile | True |
| bmp | 位图路径 | 需要在屏幕中查找的位图路径。位图必须和屏幕图像完全匹配，不能压缩。此时X、Y的值为相对于搜索位图的左上角的偏移。 | (0)字符串-Text |  | True |
| bmpVar | 位图变量 | 需要在屏幕中查找的位图。位图必须和屏幕图像完全匹配，不能压缩。此时X、Y的值为相对于搜索位图的左上角的偏移。 | (3)图片-Image |  | True |
| searchText | 文字 | 要查找的文字。可使用多行指定多组可选文字，找到任意一组即可。 | (0)字符串-Text |  | False |
| color | 颜色 | 要查找的颜色，如#FF0000 | (0)字符串-Text | #FF0000 | True |
| bmpTargetType | 查找范围 | 位图查找范围 | (9)选项-Enum（AllScreens: 所有屏幕; Rect: 坐标范围; CurrentWindow: 当前窗口; MainScreen: 主屏幕） | MainScreen | False |
| searchRect | 查找坐标范围 | 可选。当“查找范围”为“坐标范围”时有效，格式为：left,top,right,bottom | (0)字符串-Text |  | False |
| bmpPosition | 定位位置 | 定位点相对位图的位置 | (9)选项-Enum（Center: 位图中间; TopLeft: 左上角; TopRight: 右上角; BottomLeft: 左下角; BottomRight: 右下角） | Center | False |
| x | X偏移 | 定位点水平坐标偏移量（正值向右） | (12)数字(整数)-Integer | 0 | True |
| y | Y偏移 | 定位点垂直坐标偏移量（正值向下） | (12)数字(整数)-Integer | 0 | True |
| bmpColorError | 颜色容差 | 匹配像素时允许每个颜色通道的偏差值0-100，0表示精确匹配，速度最快。 | (12)数字(整数)-Integer | 10 | False |
| maxFindCount | 最大匹配 | 找图的最大匹配数量。将对每个查找到的目标执行附加动作。 | (12)数字(整数)-Integer | 1 | False |
| retryCount | 重试次数 | 未找到位图时的重试次数。每次重试间隔300ms。 | (12)数字(整数)-Integer | 0 | False |
| ignoreWindowsOcr | 跳过WindowsOCR引擎 |  | (2)布尔值-Boolean | False | False |
| ignoreBgColor | 忽略背景色 | 如果查找图片的4个顶点颜色一致，则认为是背景色，找图时忽略此颜色。 | (2)布尔值-Boolean | True | False |
| stopIfFail | 失败后中止动作 | 获取位置失败后，是否停止后续动作的执行。 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 |  | (2)布尔值-Boolean |
| firstPoint | 第一个匹配点 | 第一个匹配点坐标，格式为：x坐标,y坐标 | (0)字符串-Text |
| allPoints | 所有匹配点 | 所有的匹配点列表 | (4)文本列表-List |
| imgIndex | 匹配序号 | 从多个图片或多组文字中查找时，返回匹配到的图片或文字组序号，从0开始。 | (12)数字(整数)-Integer |

</details>
<details>
<summary>范例</summary>

**在坐标范围200,300,800,500查找文字“王中王”，最多重试2次，跳过WindowsOCR引擎，找到后定位点XY分别偏移3和4，第一个匹配点firstPoint，所有匹配点allPoints**
```json
{
  "Variables": [
    {
      "Key": "firstPoint",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "allPoints",
      "Type": 4,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:searchBmp",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "locateByText"
        },
        "searchText": {
          "VarKey": null,
          "Value": "王中王"
        },
        "bmpTargetType": {
          "VarKey": null,
          "Value": "Rect"
        },
        "searchRect": {
          "VarKey": null,
          "Value": "200,300,800,500"
        },
        "x": {
          "VarKey": null,
          "Value": "3"
        },
        "y": {
          "VarKey": null,
          "Value": "4"
        },
        "retryCount": {
          "VarKey": null,
          "Value": "2"
        },
        "ignoreWindowsOcr": {
          "VarKey": null,
          "Value": "true"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "firstPoint": "firstPoint",
        "allPoints": "allPoints",
        "imgIndex": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 37.在资源管理器中定位文件

**功能描述**
> 在资源管理器中选中文件

**官方文档**
> https://getquicker.net/KC/Help/Doc/selectfileinexplorer

**内部名称**
> sys:SelectFileInExplorer

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| path | 路径 | 要定位的文件完整路径。 | (0)字符串-Text |  | True |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |

</details>
<details>
<summary>范例</summary>

**在资源管理器中定位C:\Windows\System32\notepad.exe**
```json
{
  "Variables": [],
  "Steps": [
    {
      "StepRunnerKey": "sys:SelectFileInExplorer",
      "InputParams": {
        "path": {
          "VarKey": null,
          "Value": "C:\\Windows\\System32\\notepad.exe"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 38.用户选择

**功能描述**
> 请用户选择一个选项。

**官方文档**
> https://getquicker.net/KC/Help/Doc/userselect

**内部名称**
> sys:select

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| type | 类型 |  | (9)选项-Enum（single: 单选; multi: 多选） | single | True |
| prompt | 窗口标题 |  | (0)字符串-Text | 请选择 | True |
| note | 提示信息 |  | (0)字符串-Text |  | False |
| items | 选项 | 每行一个选项，格式为 “文本” 或 “显示文本|值”。如需显示图标，格式请参考文档。 | (0)字符串-Text |  | True |
| defaultValue | 默认值 | 预先选择的项 | (0)字符串-Text |  | False |
| defaultValueMulti | 默认值 | 多选时默认选项，每行一个 | (0)字符串-Text |  | False |
| showFilter | 启用筛选 | 是否显示筛选框。仅在且使用焦点时有效。 | (9)选项-Enum | auto | False |
| filterContent | 筛选内容 | 预先显示的筛选内容 | (0)字符串-Text |  | False |
| imeState | 输入法状态 | 筛选框输入法状态 | (9)选项-Enum（NO_CONTROL: 不控制; ON: 开启; OFF: 关闭） | NO_CONTROL | False |
| operations | 右键/全局菜单 | 每行定义一个操作，具体格式请参考文档。 | (0)字符串-Text |  | False |
| fontsize | 字体大小 |  | (1)数字(小数)-Number | 12 | True |
| fontfamily | 字体名称 | 可选。设置字体名称。如有多个字体，使用逗号分隔。 | (0)字符串-Text |  | False |
| iconsize | 图标大小 |  | (1)数字(小数)-Number | 16 | True |
| autoCloseSeconds | 自动关闭 | 几秒后自动关闭选择窗口。0表示不自动关闭。 | (1)数字(小数)-Number | 0 | False |
| winLocation | 窗口位置 | 在哪里显示选择窗口 | (9)选项-Enum | WithMouse1 | False |
| maxWinSize | 最大尺寸/位置坐标 | 可选。设置选择窗口的最大尺寸，格式为：宽度,高度。支持像素数值或屏幕宽高百分比，详情请参考模块文档。 “窗口位置” 类型为 “自定义位置” 时用于指定显示位置，格式为：left,top,right,bottom | (0)字符串-Text |  | False |
| keepLastPos | 使用上次位置 | 重复显示选择窗口时，保持上次的显示位置。 | (9)选项-Enum（0: 不保持; 3: 保持本次运行的上次位置(左上角); 1: 保持本次运行的上次位置+宽度; 5: 保持本次运行的上次位置+尺寸; 7: 保持本次运行的上次窗口尺寸; 4: 总是保持上次位置(左上角); 2: 总是保持上次位置+宽度; 6: 总是保持上次位置+尺寸; 8: 总是保持上次窗口尺寸） | 1 | False |
| noKeyboard | 不使用焦点 | 不抢占其他应用的焦点。此时无法使用键盘选择选项，只能用鼠标操作。 | (2)布尔值-Boolean | False | False |
| closeOnDeactivated | 失去焦点后关闭窗口（仅在使用焦点时有效） |  | (2)布尔值-Boolean | False | False |
| restoreForeground | 恢复活动窗口到弹出前 | 将前台窗口还原为弹窗前的活动窗口。否则将会还原到最后一个活动窗口上。 | (2)布尔值-Boolean | True | False |
| allowOkWhenEmpty | 允许不选择任何选项时点击确定 |  | (2)布尔值-Boolean | False | False |
| enableQuickConfirm | 启用快速确认（点击选项后立即确认选择并关闭窗口） |  | (2)布尔值-Boolean | True | False |
| topMost | 置顶显示 |  | (2)布尔值-Boolean | True | False |
| windowKey | 窗口标识 | 再次运行动作时，可根据标识自动关闭前一个窗口并在该位置显示新窗口。 | (0)字符串-Text |  | False |
| help | 帮助按钮内容 | 点击弹出显示帮助内容，MarkDown格式 | (0)字符串-Text |  | False |
| stopIfCancel | 取消后停止 | 取消选择后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否确认 | 是否成功选择了选项/点击了保存按钮 | (2)布尔值-Boolean |
| textValue | 选择的项(值) | 选中选项的值 | (0)字符串-Text |
| selectedIndex | 索引号 | 选择的项在列表里的序号数字，从0开始。 | (12)数字(整数)-Integer |
| selectedIndexList | 索引号列表 | 所有选择的项的序号列表 | (4)文本列表-List |
| multiSelected | 选择的项值列表 | 所有选择的项的值的列表 | (4)文本列表-List |
| extraOperation | 选择的菜单 | 选择的右键菜单或全局菜单项的值 | (0)字符串-Text |
| selectedFullItems | 选择的完整选项 | 选择选项的完整定义内容（不仅仅返回选项值） | (99)任意类型-Any |
| selectedItemTitle | 选择的选项标题 | 所选中选项的标题 | (0)字符串-Text |
| filterContent | 筛选内容 | 最后使用的筛选词 | (0)字符串-Text |

</details>
<details>
<summary>范例</summary>

**出现在屏幕中间的多选菜单，标题“选择想吃的”，底部提示文字“可多选”，选项有番茄香蕉苹果（苹果使用了font awesome图标），默认选中“番茄”和“香蕉”，不允许在不选择任何选项时点击确定，返回所选值multiSelected**
```json
{
  "Variables": [
    {
      "Key": "multiSelected",
      "Type": 4,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:select",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "multi"
        },
        "prompt": {
          "VarKey": null,
          "Value": "选择想吃的"
        },
        "note": {
          "VarKey": null,
          "Value": "可多选"
        },
        "items": {
          "VarKey": null,
          "Value": "番茄|Tomato\r\n香蕉|Banana\r\n[fa:Light_Pen:#99AAFF]苹果|Apple"
        },
        "defaultValueMulti": {
          "VarKey": null,
          "Value": "Banana\r\nTomato"
        },
        "showFilter": {
          "VarKey": null,
          "Value": "auto"
        },
        "filterContent": {
          "VarKey": null,
          "Value": ""
        },
        "winLocation": {
          "VarKey": null,
          "Value": "CenterScreen"
        },
        "maxWinSize": {
          "VarKey": null,
          "Value": ""
        },
        "keepLastPos": {
          "VarKey": null,
          "Value": "1"
        },
        "closeOnDeactivated": {
          "VarKey": null,
          "Value": "0"
        },
        "restoreForeground": {
          "VarKey": null,
          "Value": "1"
        },
        "allowOkWhenEmpty": {
          "VarKey": null,
          "Value": "0"
        },
        "topMost": {
          "VarKey": null,
          "Value": "1"
        },
        "stopIfCancel": {
          "VarKey": null,
          "Value": "1"
        },
        "imeState": {
          "VarKey": null,
          "Value": "NO_CONTROL"
        },
        "operations": {
          "VarKey": null,
          "Value": ""
        },
        "fontsize": {
          "VarKey": null,
          "Value": "12"
        },
        "fontfamily": {
          "VarKey": null,
          "Value": ""
        },
        "iconsize": {
          "VarKey": null,
          "Value": "16"
        },
        "autoCloseSeconds": {
          "VarKey": null,
          "Value": "0"
        },
        "noKeyboard": {
          "VarKey": null,
          "Value": "false"
        },
        "windowKey": {
          "VarKey": null,
          "Value": ""
        },
        "help": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "selectedIndexList": null,
        "multiSelected": "multiSelected",
        "extraOperation": null,
        "selectedFullItems": null,
        "filterContent": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```

**出现在鼠标位置的单选菜单，标题“选择想玩的”，底部提示文字“双击确认”，选项有滑板旱冰跑步（跑步使用了自定义值Run），默认选中“旱冰”，不启用筛选，允许在不选择任何选项时点击确定，返回所选值textValue**
```json
{
  "Variables": [
    {
      "Key": "textValue",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:select",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "single"
        },
        "prompt": {
          "VarKey": null,
          "Value": "选择想玩的"
        },
        "note": {
          "VarKey": null,
          "Value": "双击确认"
        },
        "items": {
          "VarKey": null,
          "Value": "滑板\r\n旱冰\r\n跑步|Run"
        },
        "defaultValue": {
          "VarKey": null,
          "Value": "旱冰"
        },
        "showFilter": {
          "VarKey": null,
          "Value": "0"
        },
        "filterContent": {
          "VarKey": null,
          "Value": ""
        },
        "winLocation": {
          "VarKey": null,
          "Value": "WithMouse1"
        },
        "maxWinSize": {
          "VarKey": null,
          "Value": ""
        },
        "keepLastPos": {
          "VarKey": null,
          "Value": "1"
        },
        "closeOnDeactivated": {
          "VarKey": null,
          "Value": "0"
        },
        "restoreForeground": {
          "VarKey": null,
          "Value": "1"
        },
        "allowOkWhenEmpty": {
          "VarKey": null,
          "Value": "1"
        },
        "enableQuickConfirm": {
          "VarKey": null,
          "Value": "1"
        },
        "topMost": {
          "VarKey": null,
          "Value": "1"
        },
        "stopIfCancel": {
          "VarKey": null,
          "Value": "1"
        },
        "imeState": {
          "VarKey": null,
          "Value": "NO_CONTROL"
        },
        "operations": {
          "VarKey": null,
          "Value": ""
        },
        "fontsize": {
          "VarKey": null,
          "Value": "12"
        },
        "fontfamily": {
          "VarKey": null,
          "Value": ""
        },
        "iconsize": {
          "VarKey": null,
          "Value": "16"
        },
        "autoCloseSeconds": {
          "VarKey": null,
          "Value": "0"
        },
        "noKeyboard": {
          "VarKey": null,
          "Value": "false"
        },
        "windowKey": {
          "VarKey": null,
          "Value": ""
        },
        "help": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "textValue": "textValue",
        "selectedIndex": null,
        "extraOperation": null,
        "selectedFullItems": null,
        "selectedItemTitle": null,
        "filterContent": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 39.模拟按键B（参数）

**功能描述**
> 发送按键和文本

**官方文档**
> https://getquicker.net/KC/Help/Doc/sendKeys

**内部名称**
> sys:sendKeys

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| keys | 按键序列 | 要发送的按键序列，使用C#语言SendKeys.Send()语法，具体请参考教程文档。 | (0)字符串-Text |  | False |

</details>
<details>
<summary>传出参数</summary>
无
</details>
<details>
<summary>范例</summary>

**模拟发送d键**
```json
{
  "Variables": [],
  "Steps": [
    {
      "StepRunnerKey": "sys:sendKeys",
      "InputParams": {
        "keys": {
          "VarKey": null,
          "Value": "d"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 40.向窗口发送消息

**功能描述**
> 使用SendMessage Win32Api向窗口发送消息。使用方法请搜索SendMessage Win32 API接口。

**官方文档**
> https://getquicker.net/KC/Help/Doc/sendMessage

**内部名称**
> sys:sendMessage

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| operation | 操作类型 |  | (9)选项-Enum（SendMessage: SendMessage(等待返回，LParam为数字); SendMessageTextLParam: SendMessage(等待返回，LParam为文本); PostMessage: PostMessage(不等待返回)） | SendMessage | False |
| hWnd | 窗口句柄hWnd | 留空或0表示前台窗口 | (12)数字(整数)-Integer |  | False |
| wMsg | 消息 | 要发送的消息。 | (0)字符串-Text |  | False |
| wParam | wParam参数 |  | (0)字符串-Text |  | False |
| lParam | lParam参数 |  | (0)字符串-Text | 0 | False |
| textLParam | lParam参数(文本) | 文本内容 | (0)字符串-Text |  | False |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| rtn | 返回值 | 返回值，依据消息的不同具有不同的含义，请查询对应API的文档。 | (12)数字(整数)-Integer |

</details>
<details>
<summary>范例</summary>

**对前台窗口进行“最大化”，等待1000毫秒后“最小化”，再等待1000毫秒后“还原窗口”**
```json
{
  "Variables": [
    {
      "Key": "hwnd",
      "Type": 1,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": null,
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:getWindowTitle",
      "InputParams": {
        "which": {
          "VarKey": null,
          "Value": "foreground"
        }
      },
      "OutputParams": {
        "output": null,
        "className": null,
        "handle": "hwnd"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:sendMessage",
      "InputParams": {
        "hWnd": {
          "VarKey": "hwnd",
          "Value": null
        },
        "wMsg": {
          "VarKey": null,
          "Value": "0x0112"
        },
        "wParam": {
          "VarKey": null,
          "Value": "0xF030"
        },
        "lParam": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {
        "isSuccess": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "最大化窗口",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:delay",
      "InputParams": {
        "delayMs": {
          "VarKey": null,
          "Value": "1000"
        },
        "monitorWaitWin": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:sendMessage",
      "InputParams": {
        "hWnd": {
          "VarKey": "hwnd",
          "Value": null
        },
        "wMsg": {
          "VarKey": null,
          "Value": "0x0112"
        },
        "wParam": {
          "VarKey": null,
          "Value": "0xF020"
        },
        "lParam": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {
        "isSuccess": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "最小化窗口",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:delay",
      "InputParams": {
        "delayMs": {
          "VarKey": null,
          "Value": "1000"
        },
        "monitorWaitWin": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:sendMessage",
      "InputParams": {
        "hWnd": {
          "VarKey": "hwnd",
          "Value": null
        },
        "wMsg": {
          "VarKey": null,
          "Value": "0x0112"
        },
        "wParam": {
          "VarKey": null,
          "Value": "0xF120"
        },
        "lParam": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {
        "isSuccess": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "还原窗口",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 41.显示等待窗口

**功能描述**
> 显示一个等待用户完成某个操作的提示窗口。用户点击等待窗口下部的按钮，窗口将关闭。点击右上角的X按钮，将会弹窗询问是否终止当前动作。

**官方文档**
> https://getquicker.net/KC/Help/Doc/showwaitwin

**内部名称**
> sys:showWaitWin

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| mode | 操作 | 请选择操作类型 | (9)选项-Enum（show: 显示窗口; update: 更新窗口; check: 检查是否关闭; close: 关闭窗口(如果还开着的话); waitClose: 等待用户关闭; showAndWaitClose: 显示窗口并等待用户关闭） | show | False |
| title | 窗口标题 |  | (0)字符串-Text | 完成后继续 | True |
| prompt | 提示文字 | 提示文字内容 | (0)字符串-Text | 请在完成操作后点下面的按钮 | True |
| winLocation | 窗口位置 | 在哪里显示选择窗口 | (9)选项-Enum | BottomRight | False |
| progress | 进度条参数 | 请以 当前值/总数 的格式传入（可使用插值方式）。 比如：40/80 | (0)字符串-Text |  | False |
| btnText | 默认按钮上的文字 | 默认按键仅用于关闭窗口。文字内容为空时隐藏默认按钮。 | (0)字符串-Text | 完成 | True |
| operations | 附加操作按钮 | 每行定义一个按钮，格式为 “文本” 或 “显示文本|值”。显示在默认按钮的左侧。 | (0)字符串-Text |  | True |
| fontsize | 文字大小 | 按钮上文字的大小，单位为逻辑像素。 | (1)数字(小数)-Number | 12 | True |
| iconSize | 图标大小 | 按钮上图标的大小，单位为逻辑像素。 | (1)数字(小数)-Number | 16 | True |
| autoCloseSeconds | 自动关闭 | 几秒后自动关闭。0表示不自动关闭。 | (1)数字(小数)-Number | 0 | False |
| stopActionIfClose | 关闭窗口时（点右上角x按钮）后停止动作 |  | (2)布尔值-Boolean | True | False |
| activateMode | 激活模式 |  | (9)选项-Enum（NotActivatable: 不支持激活（不占用焦点，仅能使用鼠标操作）; NotActivated: 支持激活，打开时不抢占焦点; AutoActivate: 支持激活，打开时抢占焦点） | NotActivatable | False |
| help | 帮助按钮内容 | 点击弹出显示帮助内容，MarkDown格式 | (0)字符串-Text |  | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isClosed | 是否已关闭 | 等待窗口是否已经关闭了 | (2)布尔值-Boolean |
| selectedOperation | 选择的按钮 | 选择的后续操作项 | (0)字符串-Text |

</details>
<details>
<summary>范例</summary>

```json
{
  "Variables": [],
  "Steps": [
    {
      "StepRunnerKey": "sys:showWaitWin",
      "InputParams": {
        "mode": {
          "VarKey": null,
          "Value": "show"
        },
        "title": {
          "VarKey": null,
          "Value": "完成后继续"
        },
        "prompt": {
          "VarKey": null,
          "Value": "请在完成操作后点下面的按钮"
        },
        "winLocation": {
          "VarKey": null,
          "Value": "BottomRight"
        },
        "progress": {
          "VarKey": null,
          "Value": ""
        },
        "btnText": {
          "VarKey": null,
          "Value": "完成"
        },
        "operations": {
          "VarKey": null,
          "Value": ""
        },
        "fontsize": {
          "VarKey": null,
          "Value": "12"
        },
        "iconSize": {
          "VarKey": null,
          "Value": "16"
        },
        "stopActionIfClose": {
          "VarKey": null,
          "Value": "1"
        },
        "autoCloseSeconds": {
          "VarKey": null,
          "Value": "0"
        },
        "activateMode": {
          "VarKey": null,
          "Value": "NotActivatable"
        },
        "help": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 42.如果

**功能描述**
> 依据条件执行操作

**官方文档**
> https://getquicker.net/KC/Help/Doc/if

**内部名称**
> sys:simpleIf

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| condition | 如果 | 是否符合指定的条件 | (2)布尔值-Boolean |  | False |

</details>
<details>
<summary>传出参数</summary>
无
</details>
<details>
<summary>范例</summary>

参考其他范例即可

</details>

***

## 43.SMTP发送邮件

**功能描述**
> 使用SMTP协议发送邮件

**官方文档**
> https://getquicker.net/KC/Help/Doc/smtp

**内部名称**
> sys:smtp

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| server | 邮件服务器 | 邮件服务器的域名或IP | (0)字符串-Text |  | True |
| port | 端口 | Smtp端口号 | (12)数字(整数)-Integer | 25 | True |
| useSsl | 使用加密连接 | 是否使用TLS连接（通常为587端口）。 | (2)布尔值-Boolean | False | False |
| account | 帐号 | 发信帐号 | (0)字符串-Text |  | True |
| password | 密码 | 发信帐号的密码 | (0)字符串-Text |  | True |
| sender | 发信邮箱 | 发信帐号所对应的Email地址 | (0)字符串-Text |  | True |
| senderName | 发件人名称 | 发件人的显示名称（可选） | (0)字符串-Text |  | True |
| to | 收件人 | 收件人Email地址，多个的话使用小写逗号分隔。 | (0)字符串-Text |  | True |
| cc | 抄送 | 抄送给的Email地址列表，多个的话使用小写逗号分隔。 | (0)字符串-Text |  | True |
| bcc | 密送 | 密送给的Email地址列表，多个的话使用小写逗号分隔。 | (0)字符串-Text |  | True |
| subject | 邮件主题 | 邮件的主题 | (0)字符串-Text |  | True |
| content | 邮件正文 | 邮件正文内容 | (0)字符串-Text |  | False |
| attachList | 附件 | 附件文件列表。多个时每行一个。 | (0)字符串-Text |  | False |
| isHtml | 内容为html | 邮件内容是否为HTML格式 | (2)布尔值-Boolean | False | False |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |

</details>
<details>
<summary>范例</summary>

```json
{
  "Variables": [],
  "Steps": [
    {
      "StepRunnerKey": "sys:smtp",
      "InputParams": {
        "server": {
          "VarKey": null,
          "Value": ""
        },
        "port": {
          "VarKey": null,
          "Value": "25"
        },
        "useSsl": {
          "VarKey": null,
          "Value": "false"
        },
        "account": {
          "VarKey": null,
          "Value": "acc@1.com"
        },
        "password": {
          "VarKey": null,
          "Value": "mypwd"
        },
        "sender": {
          "VarKey": null,
          "Value": "admin@1.com"
        },
        "senderName": {
          "VarKey": null,
          "Value": "测试员"
        },
        "to": {
          "VarKey": null,
          "Value": "b@1.com,a@1.com"
        },
        "cc": {
          "VarKey": null,
          "Value": "cc@163.com"
        },
        "bcc": {
          "VarKey": null,
          "Value": ""
        },
        "subject": {
          "VarKey": null,
          "Value": "测试结果"
        },
        "content": {
          "VarKey": null,
          "Value": "你好呀"
        },
        "attachList": {
          "VarKey": null,
          "Value": ""
        },
        "isHtml": {
          "VarKey": null,
          "Value": "false"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 44.停止(return)

**功能描述**
> 停止动作或从子程序中返回

**官方文档**
> https://getquicker.net/KC/Help/Doc/stop

**内部名称**
> sys:stop

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| method | 操作类型 |  | (9)选项-Enum（default: 默认：停止动作或从子程序返回; forcestop: 停止动作：停止整个动作(即使在子程序中)） | default | False |
| isError | 标记为出错 | 用作子程序或被其他动作调用时，返回出错状态。 | (2)布尔值-Boolean | False | False |
| return | 返回值 | 被其他动作调用时，返回的动作结果。 | (0)字符串-Text |  | False |
| showMessage | 提示消息 | 显示的提示信息。 | (0)字符串-Text |  | False |

</details>
<details>
<summary>传出参数</summary>
无
</details>
<details>
<summary>范例</summary>

参见其他范例

</details>

***

## 45.比较文本

**功能描述**
> 文本比较

**官方文档**
> https://getquicker.net/KC/Help/Doc/strCompare

**内部名称**
> sys:strCompare

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| param1 | 文本1 | 被比较的文本 | (0)字符串-Text |  | True |
| type | 类型 | 比较方式 | (9)选项-Enum（>; =; <; contains: 包含; startsWith: 以指定内容开始; endsWith: 以指定内容结束; match: 正则匹配; pinyinMatch: 包含指定内容，或匹配拼音、拼音首字母） | > | True |
| param2 | 文本2 | 对比文本。拼音匹配时，也可用于指定拼音、拼音首字母。 | (0)字符串-Text |  | True |
| case | 区分大小写 | 是否区分大小写 | (2)布尔值-Boolean | False | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| value | 值 | 比较结果是否为真 | (2)布尔值-Boolean |

</details>
<details>
<summary>范例</summary>

**判断剪贴板字符串是否包含动作参数**
```json
{
  "Variables": [],
  "Steps": [
    {
      "StepRunnerKey": "sys:strCompare",
      "InputParams": {
        "param1": {
          "VarKey": "[cliptext]",
          "Value": null
        },
        "type": {
          "VarKey": null,
          "Value": "contains"
        },
        "param2": {
          "VarKey": "quicker_in_param",
          "Value": null
        },
        "case": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {
        "value": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 46.文本处理

**功能描述**
> 各种文本处理功能

**官方文档**
> https://getquicker.net/KC/Help/Doc/stringprocess

**内部名称**
> sys:stringProcess

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| data | 待处理内容 | 需要进行文本处理的内容 | (0)字符串-Text |  | False |
| method | 处理 | 对文本进行什么处理 | (9)选项-Enum（toUpper: 英文转大写; toLower: 英文转小写; reverse: 前后反转; substring: 截取; trimStart: 去除前面空白字符; trimEnd: 去除后面空白字符; trim: 去除前后空白字符; urlEncode: URL编码; urlDecode: URL解码 (+解码为空格); urlDataDecode: URL数据解码 (保留+号); htmlEncode: Html编码; htmlDecode: Html解码; intercappedToSentence: 组合词拆分成句子(thisIsChina=>this Is China); base64Encode: Base64编码; base64Decode: Base64解码; removeEmptyLine: 去除空行; mergeEmptyLine: 合并多个空行; sortLinesAsc: 排序多行A-Z; sortLinesDesc: 排序多行Z-A; reverseLines: 翻转多行顺序; toTitleCase: 首字母大写; formatJson: 格式化JSON; md5: 计算MD5哈希; sha256Hash: 计算SHA256哈希; sha1Hash: 计算SHA1哈希; escapeJson: 转义文本为合法Json值; DecodeUnicode: 解码Unicode字串(\\uXXXX转普通字符); convertEncoding: 转换编码; toCnNum: 金额数字转换为大写; cn2num: 中文转数字; num2cn: 数字转中文; ExpandEnvironmentVariables: 替换环境变量; padLeft: 从左侧补齐长度; padRight: 从右侧补齐长度; insert: 插入内容; append: 追加内容; remove: 移除内容; removeZeroWidthChars: 移除零宽字符; html2text: HTML转纯文本） |  | False |
| srcEncoding | 编码 |  | (0)字符串-Text | utf-8 | False |
| dstEncoding | 目标编码 |  | (0)字符串-Text | gbk | False |
| start | 开始位置 | 开始截取/插入位置，从0开始。如果为负值，表示从文本末尾开始向前的字符数。 | (12)数字(整数)-Integer | 0 | False |
| value | 内容 | 插入或追加的内容 | (0)字符串-Text |  | False |
| length | 长度 | 截取或移除字符个数。截取时，0表示开始位置以后的所有内容，负值表示截取到结束前的多少个字符。 | (12)数字(整数)-Integer | 0 | False |
| totalWidth | 总宽度 | 补齐后的总字符数 | (12)数字(整数)-Integer | 10 | False |
| paddingChar | 填充字符 | 补齐时使用的填充字符，默认为空格。 | (0)字符串-Text |   | False |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| output | 结果 | 处理后的文本 | (0)字符串-Text |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |

</details>
<details>
<summary>范例</summary>

**将剪贴板字符串首字母大写后写入剪贴板，并提示“over”**
```json
{
  "Variables": [
    {
      "Key": "output",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:stringProcess",
      "InputParams": {
        "data": {
          "VarKey": "[cliptext]",
          "Value": null
        },
        "method": {
          "VarKey": null,
          "Value": "toTitleCase"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "output": "output",
        "isSuccess": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:writeClipboard",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "auto"
        },
        "input": {
          "VarKey": "output",
          "Value": null
        },
        "successMsg": {
          "VarKey": null,
          "Value": "over"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 47.运行子程序

**功能描述**
> 运行子程序

**官方文档**
> https://getquicker.net/KC/Help/Doc/subprogram

**内部名称**
> sys:subprogram

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| subProgram | 子程序 | 调用哪个子程序 | (0)字符串-Text |  | True |
| summary | Summary | 内部使用 | (0)字符串-Text |  | False |
| skipDebugOutput | 跳过调试输出 | 调试运行动作时，不输出子程序内部调试信息 | (2)布尔值-Boolean | False | False |
| stopIfFail | 失败后停止 | 子程序运行失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 子程序是否运行成功 | (2)布尔值-Boolean |

</details>
<details>
<summary>范例</summary>

**范例1**
```json

```
</details>

***

## 48.临时云存储

**功能描述**
> 将文本、文件、图片临时保存到云端并得到网址。

**官方文档**
> https://getquicker.net/KC/Help/Doc/tempcloudstore

**内部名称**
> sys:tempcloudstore

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| dataType | 数据类型 |  | (9)选项-Enum（text: 文本内容; file: 文件; imageVar: 图片变量） | text | True |
| text | 文本内容 | 要保存的文本内容 | (0)字符串-Text |  | True |
| imageVar | 图片变量 | 要保存的图片变量 | (3)图片-Image |  | False |
| file | 文件路径 | 要保存的文件路径 | (0)字符串-Text |  | True |
| expireSeconds | 超时时间 | 请求超时时间（秒数） | (1)数字(小数)-Number | 2.5 | False |
| useRandomFileName | 生成随机文件名 | 是否使用随机的文件名（仅适用于上传文件的情况） | (2)布尔值-Boolean | False | False |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| url | 网址 | 生成的访问网址 | (0)字符串-Text |

</details>
<details>
<summary>范例</summary>

**将图片imageVar临时上传至Quicker并获得临时访问地址**
```json
{
  "Variables": [
    {
      "Key": "imageVar",
      "Type": 3,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "url",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:tempcloudstore",
      "InputParams": {
        "dataType": {
          "VarKey": null,
          "Value": "imageVar"
        },
        "imageVar": {
          "VarKey": "imageVar",
          "Value": null
        },
        "expireSeconds": {
          "VarKey": null,
          "Value": "2.5"
        },
        "useRandomFileName": {
          "VarKey": null,
          "Value": "0"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "url": "url",
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 49.用户输入

**功能描述**
> 请用户输入内容。

**官方文档**
> https://getquicker.net/KC/Help/Doc/userInput

**内部名称**
> sys:userInput

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| type | 类型 | 输入内容的类型 | (9)选项-Enum（text: 单行文本; multiline: 多行文本; number: 数字; date_time: 日期时间） | text | True |
| prompt | 提示文字 | 提示用户输入什么内容。显示在输入框上方。 | (0)字符串-Text | 请输入内容 | True |
| defaultValue | 默认值 | 默认填写到输入框中的内容 | (0)字符串-Text |  | False |
| texttools | 文本选择工具 | 鼠标悬浮在文本框上时显示的小工具 | (0)字符串-Text |  | False |
| extraSettings | 扩展设置 | 可用于自定义文本选择工具，详情请参考文档。 | (0)字符串-Text |  | False |
| pattern | 验证表达式 | 正则验证表达式 | (0)字符串-Text |  | False |
| isRequired | 必填 | 是否必须填写内容 | (2)布尔值-Boolean | False | False |
| fontfamily | 字体名称 | 可选。设置字体名称。如有2个字体，使用逗号分隔。 | (0)字符串-Text |  | False |
| fontsize | 字体大小 |  | (1)数字(小数)-Number | 14 | True |
| winLocation | 窗口位置 | 在哪里显示选择窗口 | (9)选项-Enum | CenterScreen | False |
| imeState | 输入法状态 |  | (9)选项-Enum（NO_CONTROL: 不控制; ON: 开启; OFF: 关闭） | NO_CONTROL | False |
| submitWithReturn | 回车提交结果（Shift+回车换行） |  | (2)布尔值-Boolean | False | False |
| restoreFocus | 恢复活动窗口 | 用户输入后，是否将焦点还原到之前的活动窗口 | (2)布尔值-Boolean | True | False |
| closeOnDeactivated | 失去焦点后关闭窗口 |  | (2)布尔值-Boolean | False | False |
| help | 帮助按钮内容 | 点击弹出显示帮助内容，MarkDown格式 | (0)字符串-Text |  | False |
| topMost | 置顶显示 |  | (2)布尔值-Boolean | False | False |
| stopIfFail | 失败后停止 | 用户取消后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| textValue | 文本值 | 文本类型的输入值 | (0)字符串-Text |
| numberValue | 数字值 | 数字类型的输入值 | (1)数字(小数)-Number |
| datetimeValue | 日期时间值 |  | (6)时间日期-DateTime |
| isEmpty | 是否为空 | 用户是否没有输入内容 | (2)布尔值-Boolean |

</details>
<details>
<summary>范例</summary>

**弹框要求用户输入家庭住址，必填，默认值“xx省xx市xx区xx路xx号xx小区xx栋xx单元xxx房”，输入内容返回到变量address；接着弹框要求输入出生年份，非必填，失去焦点后关闭窗口，返回内容到变量year**
```json
{
  "Variables": [
    {
      "Key": "address",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "year",
      "Type": 1,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:userInput",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "text"
        },
        "prompt": {
          "VarKey": null,
          "Value": "输入你的家庭住址"
        },
        "defaultValue": {
          "VarKey": null,
          "Value": "xx省xx市xx区xx路xx号xx小区xx栋xx单元xxx房"
        },
        "pattern": {
          "VarKey": null,
          "Value": ""
        },
        "isRequired": {
          "VarKey": null,
          "Value": "1"
        },
        "restoreFocus": {
          "VarKey": null,
          "Value": "1"
        },
        "closeOnDeactivated": {
          "VarKey": null,
          "Value": "0"
        },
        "topMost": {
          "VarKey": null,
          "Value": "0"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        },
        "texttools": {
          "VarKey": null,
          "Value": ""
        },
        "extraSettings": {
          "VarKey": null,
          "Value": ""
        },
        "fontfamily": {
          "VarKey": null,
          "Value": ""
        },
        "fontsize": {
          "VarKey": null,
          "Value": "14"
        },
        "winLocation": {
          "VarKey": null,
          "Value": "CenterScreen"
        },
        "imeState": {
          "VarKey": null,
          "Value": "NO_CONTROL"
        },
        "help": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "textValue": "address",
        "isEmpty": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:userInput",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "number"
        },
        "prompt": {
          "VarKey": null,
          "Value": "输入你的出生年份"
        },
        "defaultValue": {
          "VarKey": null,
          "Value": ""
        },
        "pattern": {
          "VarKey": null,
          "Value": ""
        },
        "isRequired": {
          "VarKey": null,
          "Value": "0"
        },
        "restoreFocus": {
          "VarKey": null,
          "Value": "1"
        },
        "closeOnDeactivated": {
          "VarKey": null,
          "Value": "1"
        },
        "topMost": {
          "VarKey": null,
          "Value": "0"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        },
        "fontfamily": {
          "VarKey": null,
          "Value": ""
        },
        "fontsize": {
          "VarKey": null,
          "Value": "14"
        },
        "winLocation": {
          "VarKey": null,
          "Value": "CenterScreen"
        },
        "help": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "textValue": null,
        "numberValue": "year",
        "isEmpty": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 50.等待剪贴板内容改变

**功能描述**
> 等待剪贴板的内容发生改变。等待第三方工具（如截图工具）完成操作并更新剪贴板。

**官方文档**
> https://getquicker.net/KC/Help/Doc/waitclipboardchange

**内部名称**
> sys:waitClipboardChange

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| maxWaitSeconds | 最长等待秒数 | 超过等待时间剪贴板未改变，则结束等待。 | (1)数字(小数)-Number | 10 | True |
| recentChangeMs | 包含临近的改变 | 包含在此之前一定时间内(毫秒)发生的改变。 | (12)数字(整数)-Integer | 10 | True |
| monitorWaitWin | 等待窗口关闭时取消 | 结合“等待窗口”模块，如果等待窗口关闭，则停止等待剪贴板变化。 | (2)布尔值-Boolean | False | False |
| stopIfFail | 失败后中止动作 | 超时后剪贴板仍未改变，是否中止动作。 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否改变 | 剪贴板内容是否改变了 | (2)布尔值-Boolean |

</details>
<details>
<summary>范例</summary>

**等待剪贴板内容改变，最长等待15秒，并且包含在此之前10毫秒内发生的改变**
```json
{
  "Variables": [],
  "Steps": [
    {
      "StepRunnerKey": "sys:waitClipboardChange",
      "InputParams": {
        "maxWaitSeconds": {
          "VarKey": null,
          "Value": "15"
        },
        "recentChangeMs": {
          "VarKey": null,
          "Value": "10"
        },
        "monitorWaitWin": {
          "VarKey": null,
          "Value": "0"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 51.等待时间

**功能描述**
> 等待指定的毫秒数

**官方文档**
> https://getquicker.net/KC/Help/Doc/delay

**内部名称**
> sys:delay

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| delayMs | 等待时间 | 等待时间毫秒数 | (12)数字(整数)-Integer | 100 | True |
| monitorWaitWin | 等待窗口关闭时取消 | 结合“等待窗口”模块，如果等待窗口关闭，则停止等待。仅当等待时间超过1000ms时生效 | (2)布尔值-Boolean | False | False |

</details>
<details>
<summary>传出参数</summary>
无
</details>
<details>
<summary>范例</summary>

**等待123毫秒**
```json
{
  "Variables": [],
  "Steps": [
    {
      "StepRunnerKey": "sys:delay",
      "InputParams": {
        "delayMs": {
          "VarKey": null,
          "Value": "123"
        },
        "monitorWaitWin": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 52.窗口操作

**功能描述**
> Window窗口相关操作

**官方文档**
> https://getquicker.net/KC/Help/Doc/windowoperations

**内部名称**
> sys:windowOperations

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| type | 类型 | 操作类型 | (9)选项-Enum（move: 移动窗口; move_ex: 移动窗口(增强); setTopmost: 置顶窗口; toggleTopMost: 切换置顶状态; removeTopmost: 取消置顶窗口; setBottom: 置底窗口; show: 设置显示状态; SET_FOREGROUND: 设置为前台窗口; close: 关闭; kill: 强制关闭; set_trans: 设置或更新透明度） | move | True |
| hWnd | 窗口句柄 | 要操作的窗口句柄（数字）。0或留空表示操作前台窗口。 | (12)数字(整数)-Integer |  | False |
| x | X坐标 | 窗口左上角X坐标 | (12)数字(整数)-Integer | 100 | False |
| y | Y坐标 | 窗口左上角Y坐标 | (12)数字(整数)-Integer | 100 | False |
| width | 宽度 | 窗口宽度。-1时表示不更改窗口尺寸。 | (12)数字(整数)-Integer | 500 | False |
| height | 高度 | 窗口高度。-1时表示不更改窗口尺寸。 | (12)数字(整数)-Integer | 500 | False |
| area | 目标位置 | 窗口左,上,右,下的位置坐标 | (0)字符串-Text | 25%,25%,75%,75% | False |
| showCmd | 显示状态 | 窗口显示状态，具体说明请参考Win32接口。 | (9)选项-Enum（3: 最大化(SW_MAXIMIZE); 6: 最小化(SW_MINIMIZE); 9: 显示并恢复大小(SW_RESTORE); 0: 隐藏(SW_HIDE); 5: 显示(SW_SHOW); TOGGLE_MAXMIZE: 切换最大化/恢复） | 3 | True |
| alpha | 不透明度Alpha | 数字0-255：0为全透明，255为不透明。-数字：将当前透明度增加一些。+数字：将透明度减少一些。 | (0)字符串-Text | 128 | False |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| isTopmost | 是否置顶 | 操作后窗口是否为置顶 | (2)布尔值-Boolean |

</details>
<details>
<summary>范例</summary>

**移动句柄为hWnd的窗口至x123,y456坐标，并调整窗口大小为400x600；接着将窗口透明度Alpha设为5**
```json
{
  "Variables": [
    {
      "Key": "hWnd",
      "Type": 12,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:windowOperations",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "move"
        },
        "hWnd": {
          "VarKey": "hWnd",
          "Value": null
        },
        "x": {
          "VarKey": null,
          "Value": "123"
        },
        "y": {
          "VarKey": null,
          "Value": "456"
        },
        "width": {
          "VarKey": null,
          "Value": "400"
        },
        "height": {
          "VarKey": null,
          "Value": "600"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:windowOperations",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "set_trans"
        },
        "hWnd": {
          "VarKey": "hWnd",
          "Value": null
        },
        "alpha": {
          "VarKey": null,
          "Value": "50"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 53.写入剪贴板

**功能描述**
> 将文本或图片等内容写入剪贴板

**官方文档**
> https://getquicker.net/KC/Help/Doc/writeClipboard

**内部名称**
> sys:writeClipboard

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| type | 类型 | 操作类型 | (9)选项-Enum（auto; html; text; image; rtf; csv; custom: 自定义格式; clear; clearHistory: 清空剪贴板历史(Win10+)） | auto | True |
| customFormat | 格式名 | 自定义的剪贴板格式名 | (0)字符串-Text |  | True |
| input | 输入 | 要写入剪贴板的数据 | (99)任意类型-Any |  | True |
| html | HTML内容 | HTML代码片段 | (0)字符串-Text |  | True |
| text | 文本内容 | 纯文本格式内容。 | (0)字符串-Text |  | True |
| imageVar | 图片(变量) | 要写入剪贴板的图片内容 | (3)图片-Image |  | False |
| fastMode | 快速模式 | 不需要处理图片中的透明通道时选择 | (2)布尔值-Boolean | False | False |
| successMsg | 成功后提示 | 可选。写入成功后提示消息，如“XXX已写入剪贴板”。 | (0)字符串-Text |  | True |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |

</details>
<details>
<summary>范例</summary>

**将图片imageVar写入剪贴板，并且启用快速模式，完成后提示over**
```json
{
  "Variables": [
    {
      "Key": "imageVar",
      "Type": 3,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:writeClipboard",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "image"
        },
        "imageVar": {
          "VarKey": "imageVar",
          "Value": null
        },
        "fastMode": {
          "VarKey": null,
          "Value": "1"
        },
        "successMsg": {
          "VarKey": null,
          "Value": "over"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 54.文件放入剪贴板

**功能描述**
> 将文件或文件列表存入剪贴板

**官方文档**
> https://getquicker.net/KC/Help/Doc/filetoclipboard

**内部名称**
> sys:fileToClipboard

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| file | 单个文件 | 要存入剪贴板的文件(夹)路径（与文件列表二选一） | (0)字符串-Text |  | False |
| list | 文件列表 | 要存入剪贴板的多个文件路径（与单个文件二选一） | (4)文本列表-List |  | False |
| useCut | 剪切文件 | 是否剪切文件 | (2)布尔值-Boolean | False | False |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |

</details>
<details>
<summary>范例</summary>

**将文件D:\1.js和F:\3.txt放入剪贴板**
```json
{
  "Variables": [],
  "Steps": [
    {
      "StepRunnerKey": "sys:fileToClipboard",
      "InputParams": {
        "file": {
          "VarKey": null,
          "Value": ""
        },
        "list": {
          "VarKey": null,
          "Value": "D:\\1.js\r\nF:\\3.txt"
        },
        "useCut": {
          "VarKey": null,
          "Value": "false"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 55.WebView2浏览器窗口

**功能描述**
> 基于微软Edge浏览器内核的组件，需要安装Edge最新预览版方可使用。

**官方文档**
> https://getquicker.net/KC/Help/Doc/webview2

**内部名称**
> sys:webview2

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| type | 操作类型 |  | (9)选项-Enum（OpenUrl: 打开网页; OpenAndWaitLoad: 打开网页并等待加载完成; OpenUrlAndWaitClose: 打开网页并等待窗口关闭; SendMessage: 发送消息; ExecuteScript: 执行脚本; CheckWindowState: 获取窗口状态; Close: 关闭窗口(如果尚未关闭); Reload: 重新加载/刷新; Stop: 停止加载; CheckInstalled: 检查是否安装WebView2; MultiTab_OpenUrl: 【多标签】打开网址; MultiColumn_OpenUrl: 【多列】打开网址） | OpenUrl | False |
| url | 网址或HTML内容 | 网页地址/文件路径或html代码内容 | (0)字符串-Text |  | True |
| urlList | 网址列表 | 每行一个：网址，或“标题|网址”，或“[图标]标题|网址”格式。 | (4)文本列表-List |  | True |
| additionalBrowserArguments | 附加的浏览器参数 | 用于设置代理等用途 | (0)字符串-Text |  | True |
| virtualHostToFolder | 虚拟主机映射 | 将文件夹映射为虚拟主机名。格式：主机名|文件夹路径。多个时，每行一个。
 在html中可以使用https://servername/path/to/file.png的格式访问文件。 | (0)字符串-Text |  | True |
| userAgent | User Agent | 可选。自定义UserAgent | (0)字符串-Text |  | False |
| title | 窗口标题 | 窗口标题文字。未设置时，自动使用网页标题。 | (0)字符串-Text |  | True |
| icon | 窗口图标 | 显示在窗口左上角的图标。支持fa:内置图报名:#RRGGBB或图标网址。 | (0)字符串-Text |  | False |
| defaultBgColor | 默认背景色 | 可选。设置窗口的默认背景色。 | (0)字符串-Text |  | False |
| autoCloseKey | 窗口标识 | (仅必要时使用)用于关闭之前打开的具有此标识的WebView2窗口。使用=表示当前动作ID。 | (0)字符串-Text | = | False |
| modeForExists | 如果窗口已存在 |  | (9)选项-Enum（SkipThisStep: 跳过此步骤; UpdateUrl: 更新网址; UpdateUrlAndPosition: 更新网址和窗口位置; RecreateWindow: 关闭并重建窗口; BringToFront: 激活窗口） | SkipThisStep | False |
| script | JS脚本 | 可选。 | (0)字符串-Text |  | True |
| sendMessage | 消息内容 | Json格式的消息内容。词典变量会自动转换成json。 | (0)字符串-Text |  | True |
| winLocation | 窗口位置 | 在哪里显示选择窗口 | (9)选项-Enum | CenterScreen | False |
| winSize | 窗口尺寸/位置 | 设置选择窗口的尺寸，格式为：宽度,高度。支持像素数值或屏幕宽高百分比，详情请参考模块文档。 “窗口位置” 类型为 “自定义位置” 时用于指定显示位置，格式为：left,top,right,bottom | (0)字符串-Text |  | False |
| defaultDownloadFolderPath | 默认下载文件夹 | 默认的文件下载存储目录 | (0)字符串-Text |  | False |
| profileName | Profile | 当需要同时登录一个网站的多个账号时，可以创建独立的Profile | (0)字符串-Text |  | False |
| topMost | 置顶显示 |  | (2)布尔值-Boolean | False | False |
| showInTaskbar | 显示任务栏图标 |  | (2)布尔值-Boolean | True | False |
| noActivate | 不占用焦点 | 不占用焦点时也无法在窗口中输入文字 | (2)布尔值-Boolean | False | False |
| closeWhenLostFocus | 失去焦点后 |  | (9)选项-Enum（false: 不执行操作; true: 关闭窗口; hide: 隐藏窗口; minimize: 最小化窗口; close_if_not_topmost: 如果未置顶，关闭窗口; hide_if_not_topmost: 如果未置顶，隐藏窗口; minimize_if_not_topmost: 如果未置顶，最小化窗口） | False | False |
| escCloseWindow | 按Esc关闭窗口 |  | (2)布尔值-Boolean | False | False |
| showToolbar | 显示工具栏 |  | (2)布尔值-Boolean | False | False |
| windowStyle | 窗口风格 |  | (9)选项-Enum（normal: 正常; none: 无边框） | normal | False |
| clearCookies | 关闭窗口时清理Cookie |  | (2)布尔值-Boolean | False | False |
| addDevTool | 添加DevTools桥 |  | (2)布尔值-Boolean | False | False |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功。获取窗口信息时，窗口是否存在。 | (2)布尔值-Boolean |
| isInstalled | 是否安装WebView2 |  | (2)布尔值-Boolean |
| hWnd | 窗口句柄 |  | (12)数字(整数)-Integer |
| webView | WebView2对象 | 可用于在C#脚本中使用，需运行在UI线程中。注意避免循环引用。 | (98)对象(Object)-Object |
| lastLocation | 窗口位置 | 返回窗口坐标范围。格式为：left,top,right,bottom | (0)字符串-Text |
| currUri | 当前网址 | 浏览器当前网址 | (0)字符串-Text |
| docTitle | 网页标题 |  | (0)字符串-Text |
| sourceCode | 网页代码 |  | (0)字符串-Text |
| cookies | Cookie |  | (0)字符串-Text |
| previewImage | 预览图 |  | (3)图片-Image |
| isNavCompleted | 导航是否已结束 | 是否已完成网页加载过程 | (2)布尔值-Boolean |
| scriptResult | 脚本运行结果 | json编码的脚本运行结果内容 | (0)字符串-Text |

</details>
<details>
<summary>范例</summary>

**在WebView中更新动作变量与调用子程序**
```json
{
  "Variables": [
    {
      "Key": "text",
      "Type": 0,
      "Desc": "默认的文本变量",
      "DefaultValue": "这是默认值。",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "dict",
      "Type": 10,
      "Desc": "",
      "DefaultValue": "a:111\r\nb:2222\r\nc:3333",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "list",
      "Type": 4,
      "Desc": "",
      "DefaultValue": "aaaa\r\nbbb\r\nccc\r\nddd\r\neee",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:webview2",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "OpenUrlAndWaitClose"
        },
        "url": {
          "VarKey": null,
          "Value": "<html>\r\n<head>\r\n<title>Quicker测试</title>\r\n</head>\r\n<body>\r\n<h1>WebView测试</h1>\r\n\r\n<button onclick='readVar()'>读取变量值</button>\r\n<button onclick='setVar()'>设置变量值并关闭窗口</button>\r\n<button onclick='testSubprogram()'>子程序</button>\r\n\r\n<button onclick='testSubprogramWithNetwork()'>汉字转拼音</button>\r\n<hr>\r\n<div id='content'>\r\n</div>\r\n\r\n<script>\r\n    window.chrome.webview.addEventListener('message', event => alert(event.data));\r\n\r\n    // 同步方式\r\n    async function readVar(){\r\n    \t// 返回文本变量\r\n        alert(await $quicker.getVar(\"text\"));\r\n        \r\n        // 返回列表变量（转换成文本数组）\r\n        alert(chrome.webview.hostObjects.sync.v.getVar(\"list\"));\r\n        \r\n        // 返回词典所有内容的json文本（示例为异步方式）\r\n        var v = await chrome.webview.hostObjects.v;\r\n        var dict = await v.getVar(\"dict\");\r\n        alert(dict);\r\n        \r\n        // 返回词典的某个键的值\r\n        alert(chrome.webview.hostObjects.sync.v.getDictItemValue(\"dict\",\"c\"));\r\n    };\r\n\t\r\n\tfunction setVar(){\r\n\t\t// 设置列表变量值\r\n\t \tchrome.webview.hostObjects.sync.v.setVar(\"list\", ['a1','b2','c3','d4']);\r\n\t \r\n\t \t// 设置文本值\r\n       \tchrome.webview.hostObjects.sync.v.setVar(\"text\", \"Hello world from js code\");\r\n       \r\n       \t// 设置词典值\r\n       \tchrome.webview.hostObjects.sync.v.setDictByJson(\"dict\", \"{a: 1, b: 2}\");\r\n       \r\n       \t// 设置词典的某一个键的值\r\n        chrome.webview.hostObjects.sync.v.setDictItemValue(\"dict\", \"c\", 3);\r\n       \r\n       \twindow.close();\r\n    };\r\n    \r\n    // 调用子程序：返回原始输入值\r\n    async function testSubprogram(){\r\n    \tvar obj = {input:'Hello Quicker!', age:3};\r\n    \tawait $quicker.subprogram('test', JSON.stringify(obj), false, (success, data) => {\r\n    \t\talert('success:' + success + '\\n' + data);\r\n    \t});    \t\r\n    }\r\n    \r\n    // 调用子程序进行网络请求\r\n    async function testSubprogramWithNetwork(){\r\n    \tvar cn = prompt(\"请输入汉字字符串：\", \"中国人\");\r\n    \tif (cn != null){\r\n    \t\tvar inParams = {input : cn, separator: ','};\r\n    \t\tawait $quicker.subprogram('转换拼音', JSON.stringify(inParams), false,\r\n    \t\t\t(success, data) => {\r\n    \t\t\t\tif (success){\r\n    \t\t\t\t\tvar result = JSON.parse(data);\r\n    \t\t\t\t\tdocument.getElementById('content').innerText = result.output;\r\n    \t\t\t\t}else{\r\n    \t\t\t\t\talert('出错了：' + data);\r\n    \t\t\t\t}\r\n    \t\t\t});\r\n    \t}\r\n    }\r\n</script>\r\n</body>\r\n</html>"
        },
        "virtualHostToFolder": {
          "VarKey": null,
          "Value": ""
        },
        "title": {
          "VarKey": null,
          "Value": "测试浏览器插件"
        },
        "autoCloseKey": {
          "VarKey": null,
          "Value": "okok"
        },
        "script": {
          "VarKey": null,
          "Value": ""
        },
        "winLocation": {
          "VarKey": null,
          "Value": "CenterScreen"
        },
        "winSize": {
          "VarKey": null,
          "Value": ""
        },
        "topMost": {
          "VarKey": null,
          "Value": "0"
        },
        "showInTaskbar": {
          "VarKey": null,
          "Value": "1"
        },
        "noActivate": {
          "VarKey": null,
          "Value": "0"
        },
        "closeWhenLostFocus": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {
        "isSuccess": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:notify",
      "InputParams": {
        "msg": {
          "VarKey": null,
          "Value": "$$js修改后的变量值：\r\n{text}\r\n====\r\n{list}\r\n====\r\n{dict}"
        },
        "maxLines": {
          "VarKey": null,
          "Value": "0"
        },
        "type": {
          "VarKey": null,
          "Value": "Info"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```

**一键获取临时邮箱**
```json
{
  "Variables": [
    {
      "Key": "返回结果",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "email",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "配置_保存的邮箱",
      "Type": 4,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": true,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "选择的操作",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "res",
      "Type": 99,
      "Desc": "返回结果的JObject",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:group",
      "InputParams": {
        "skipErr": {
          "VarKey": null,
          "Value": "0"
        },
        "skipWhenDebugging": {
          "VarKey": null,
          "Value": "0"
        },
        "useMultiThread": {
          "VarKey": null,
          "Value": "0"
        },
        "waitAny": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "errorMessage": null
      },
      "IfSteps": [
        {
          "StepRunnerKey": "sys:simpleIf",
          "InputParams": {
            "condition": {
              "VarKey": null,
              "Value": "$= String.Equals({quicker_in_param}, \"已保存邮箱列表\", StringComparison.OrdinalIgnoreCase)"
            }
          },
          "OutputParams": {},
          "IfSteps": [
            {
              "StepRunnerKey": "sys:manageList",
              "InputParams": {
                "list": {
                  "VarKey": "配置_保存的邮箱",
                  "Value": null
                },
                "winTitle": {
                  "VarKey": null,
                  "Value": ""
                },
                "note": {
                  "VarKey": null,
                  "Value": ""
                },
                "parseData": {
                  "VarKey": null,
                  "Value": "0"
                },
                "seperator": {
                  "VarKey": null,
                  "Value": "|"
                },
                "windowSize": {
                  "VarKey": null,
                  "Value": ""
                },
                "allowAdd": {
                  "VarKey": null,
                  "Value": "1"
                },
                "allowEdit": {
                  "VarKey": null,
                  "Value": "1"
                },
                "allowDelete": {
                  "VarKey": null,
                  "Value": "1"
                },
                "stopIfFail": {
                  "VarKey": null,
                  "Value": "0"
                },
                "help": {
                  "VarKey": null,
                  "Value": ""
                },
                "titleDelegate": {
                  "VarKey": null,
                  "Value": ""
                }
              },
              "OutputParams": {
                "isSuccess": null,
                "errMessage": null
              },
              "IfSteps": null,
              "ElseSteps": null,
              "Note": "",
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            },
            {
              "StepRunnerKey": "sys:stop",
              "InputParams": {
                "method": {
                  "VarKey": null,
                  "Value": "default"
                },
                "isError": {
                  "VarKey": null,
                  "Value": "0"
                },
                "return": {
                  "VarKey": null,
                  "Value": ""
                },
                "showMessage": {
                  "VarKey": null,
                  "Value": ""
                }
              },
              "OutputParams": {},
              "IfSteps": null,
              "ElseSteps": null,
              "Note": "",
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            }
          ],
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": true,
          "DelayMs": 0
        }
      ],
      "ElseSteps": [],
      "Note": "动作右键",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:form",
      "InputParams": {
        "operation": {
          "VarKey": null,
          "Value": "variables"
        },
        "title": {
          "VarKey": null,
          "Value": "选择操作"
        },
        "formDef": {
          "VarKey": null,
          "Value": "{\"Fields\":[{\"FieldKey\":\"email\",\"DictVarType\":null,\"Label\":\"邮箱\",\"HelpText\":\"输入或下拉选择保存的邮箱后可以查看邮件\",\"HelpLink\":null,\"InputMethod\":11,\"SelectionItems\":\"$${配置_保存的邮箱}\",\"IsRequired\":false,\"MinValue\":\"\",\"MaxValue\":\"\",\"Pattern\":\"\",\"InputWidth\":\"\",\"MaxLength\":0,\"ImeState\":null,\"TextTools\":\"\",\"ExtraSettings\":\"\",\"VisibleExpression\":\"\",\"DefaultValue\":null,\"ColumnWidth\":0.0,\"OnlyDate\":false,\"ReadOnly\":false,\"Group\":\"\"}]}"
        },
        "help": {
          "VarKey": null,
          "Value": ""
        },
        "titleColumnWidth": {
          "VarKey": null,
          "Value": "100"
        },
        "windowWidth": {
          "VarKey": null,
          "Value": "500"
        },
        "windowHeight": {
          "VarKey": null,
          "Value": "0"
        },
        "restoreFocus": {
          "VarKey": null,
          "Value": "0"
        },
        "topMost": {
          "VarKey": null,
          "Value": "false"
        },
        "disableEnterSubmit": {
          "VarKey": null,
          "Value": "0"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        },
        "markdownhelp": {
          "VarKey": null,
          "Value": ""
        },
        "defaultInputWidth": {
          "VarKey": null,
          "Value": "0"
        },
        "confirm": {
          "VarKey": null,
          "Value": "📬查看邮件"
        },
        "customButtons": {
          "VarKey": null,
          "Value": "获取新邮箱|获取新邮箱"
        },
        "selectedGroup": {
          "VarKey": null,
          "Value": ""
        },
        "winLocation": {
          "VarKey": null,
          "Value": "CenterScreen"
        },
        "winSize": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "button": "选择的操作",
        "selectedGroup": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:simpleIf",
      "InputParams": {
        "condition": {
          "VarKey": null,
          "Value": "$= String.IsNullOrWhiteSpace({选择的操作})"
        }
      },
      "OutputParams": {},
      "IfSteps": [
        {
          "StepRunnerKey": "sys:simpleIf",
          "InputParams": {
            "condition": {
              "VarKey": null,
              "Value": "$= String.IsNullOrWhiteSpace({email})"
            }
          },
          "OutputParams": {},
          "IfSteps": [
            {
              "StepRunnerKey": "sys:notify",
              "InputParams": {
                "type": {
                  "VarKey": null,
                  "Value": "Error"
                },
                "msg": {
                  "VarKey": null,
                  "Value": "邮箱不能为空！"
                },
                "maxLines": {
                  "VarKey": null,
                  "Value": "0"
                },
                "style": {
                  "VarKey": null,
                  "Value": "Default"
                },
                "clickAction": {
                  "VarKey": null,
                  "Value": ""
                }
              },
              "OutputParams": {},
              "IfSteps": null,
              "ElseSteps": null,
              "Note": "",
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            },
            {
              "StepRunnerKey": "sys:stop",
              "InputParams": {
                "method": {
                  "VarKey": null,
                  "Value": "default"
                },
                "isError": {
                  "VarKey": null,
                  "Value": "0"
                },
                "return": {
                  "VarKey": null,
                  "Value": ""
                },
                "showMessage": {
                  "VarKey": null,
                  "Value": ""
                }
              },
              "OutputParams": {},
              "IfSteps": null,
              "ElseSteps": null,
              "Note": "",
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            }
          ],
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": true,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:notify",
          "InputParams": {
            "type": {
              "VarKey": null,
              "Value": "Info"
            },
            "msg": {
              "VarKey": null,
              "Value": "正在获取邮件中..."
            },
            "maxLines": {
              "VarKey": null,
              "Value": "0"
            },
            "style": {
              "VarKey": null,
              "Value": "Default"
            },
            "clickAction": {
              "VarKey": null,
              "Value": ""
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:webview2",
          "InputParams": {
            "type": {
              "VarKey": null,
              "Value": "OpenUrl"
            },
            "url": {
              "VarKey": null,
              "Value": "$$<!DOCTYPE html>\r\n<html lang='zh'>\r\n<head>\r\n    <meta charset='UTF-8'>\r\n    <meta name='viewport' content='width=device-width, initial-scale=1.0'>\r\n    <title>邮箱收件箱</title>\r\n    <style>\r\n        :root {\r\n            --primary-color: #1a73e8;\r\n            --bg-color: #f8fafc;\r\n            --text-color: #333;\r\n            --hover-color: #f0f2f5;\r\n            --shadow-sm: 0 1px 3px rgba(0,0,0,0.1);\r\n            --shadow-md: 0 4px 6px rgba(0,0,0,0.1);\r\n            --shadow-lg: 0 10px 15px rgba(0,0,0,0.1);\r\n            --transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);\r\n        }\r\n\r\n        * {\r\n            margin: 0;\r\n            padding: 0;\r\n            box-sizing: border-box;\r\n            font-family: 'Segoe UI', 'Microsoft YaHei', sans-serif;\r\n        }\r\n\r\n        body {\r\n            background-color: var(--bg-color);\r\n            color: var(--text-color);\r\n        }\r\n\r\n        .header {\r\n            background: rgba(255, 255, 255, 0.9);\r\n            backdrop-filter: blur(10px);\r\n            -webkit-backdrop-filter: blur(10px);\r\n            padding: 1.2rem 2rem;\r\n            box-shadow: var(--shadow-sm);\r\n            position: fixed;\r\n            width: 100%;\r\n            top: 0;\r\n            z-index: 100;\r\n            transition: var(--transition);\r\n        }\r\n\r\n        .header:hover {\r\n            box-shadow: var(--shadow-md);\r\n        }\r\n\r\n        .header-content {\r\n            display: flex;\r\n            justify-content: space-between;\r\n            align-items: center;\r\n            max-width: 1200px;\r\n            margin: 0 auto;\r\n        }\r\n\r\n        .email-address {\r\n            font-size: 1.2rem;\r\n            color: var(--primary-color);\r\n            font-weight: 500;\r\n            opacity: 0;\r\n            animation: slideIn 0.5s ease forwards;\r\n        }\r\n\r\n        .email-count {\r\n            background: var(--primary-color);\r\n            color: white;\r\n            padding: 0.5rem 1.2rem;\r\n            border-radius: 20px;\r\n            font-size: 0.9rem;\r\n            box-shadow: var(--shadow-sm);\r\n            transition: var(--transition);\r\n            opacity: 0;\r\n            animation: slideIn 0.5s ease 0.2s forwards;\r\n        }\r\n\r\n        .email-count:hover {\r\n            transform: translateY(-2px);\r\n            box-shadow: var(--shadow-md);\r\n        }\r\n\r\n        .container {\r\n            max-width: 1200px;\r\n            margin: 100px auto 0;\r\n            padding: 20px;\r\n        }\r\n\r\n        .email-list {\r\n            background: white;\r\n            border-radius: 16px;\r\n            box-shadow: var(--shadow-sm);\r\n            overflow: hidden;\r\n            opacity: 0;\r\n            animation: fadeIn 0.8s ease 0.4s forwards;\r\n        }\r\n\r\n        .email-item {\r\n            padding: 1.2rem 1.8rem;\r\n            border-bottom: 1px solid #eee;\r\n            cursor: pointer;\r\n            transition: var(--transition);\r\n            display: flex;\r\n            justify-content: space-between;\r\n            align-items: center;\r\n            opacity: 0;\r\n            animation: slideUp 0.5s ease forwards;\r\n            animation-delay: calc(var(--index) * 0.1s);\r\n        }\r\n\r\n        .email-item:hover {\r\n            background-color: var(--hover-color);\r\n            transform: translateX(5px);\r\n            box-shadow: inset 4px 0 0 var(--primary-color);\r\n        }\r\n\r\n        .email-item:last-child {\r\n            border-bottom: none;\r\n        }\r\n\r\n        .email-left {\r\n            flex: 1;\r\n        }\r\n\r\n        .email-subject {\r\n            font-weight: 500;\r\n            margin-bottom: 0.5rem;\r\n        }\r\n\r\n        .email-from {\r\n            color: #666;\r\n            font-size: 0.9rem;\r\n        }\r\n\r\n        .email-right {\r\n            text-align: right;\r\n            min-width: 150px;\r\n        }\r\n\r\n        .email-time {\r\n            color: #666;\r\n            font-size: 0.9rem;\r\n        }\r\n\r\n        .email-size {\r\n            color: #999;\r\n            font-size: 0.8rem;\r\n            margin-top: 0.3rem;\r\n        }\r\n\r\n        .modal {\r\n            display: none;\r\n            position: fixed;\r\n            top: 0;\r\n            left: 0;\r\n            width: 100%;\r\n            height: 100%;\r\n            background: rgba(0,0,0,0.5);\r\n            z-index: 1000;\r\n            opacity: 0;\r\n            transition: opacity 0.3s ease;\r\n        }\r\n\r\n        .modal.show {\r\n            opacity: 1;\r\n        }\r\n\r\n        .modal-content {\r\n            position: relative;\r\n            background: white;\r\n            margin: 50px auto;\r\n            padding: 25px;\r\n            width: 90%;\r\n            max-width: 800px;\r\n            max-height: 80vh;\r\n            overflow-y: auto;\r\n            border-radius: 16px;\r\n            box-shadow: var(--shadow-lg);\r\n            transform: translateY(-20px);\r\n            opacity: 0;\r\n            transition: var(--transition);\r\n        }\r\n\r\n        .modal.show .modal-content {\r\n            transform: translateY(0);\r\n            opacity: 1;\r\n        }\r\n\r\n        .close {\r\n            position: absolute;\r\n            right: 20px;\r\n            top: 10px;\r\n            font-size: 28px;\r\n            cursor: pointer;\r\n            color: #666;\r\n        }\r\n\r\n        .close:hover {\r\n            color: #333;\r\n        }\r\n\r\n        .modal-header {\r\n            margin-bottom: 20px;\r\n            padding-bottom: 10px;\r\n            border-bottom: 1px solid #eee;\r\n        }\r\n\r\n        .modal-subject {\r\n            font-size: 1.5rem;\r\n            margin-bottom: 10px;\r\n        }\r\n\r\n        .modal-info {\r\n            color: #666;\r\n            font-size: 0.9rem;\r\n        }\r\n\r\n        .modal-body {\r\n            line-height: 1.6;\r\n        }\r\n\r\n        @keyframes slideIn {\r\n            from {\r\n                transform: translateX(-20px);\r\n                opacity: 0;\r\n            }\r\n            to {\r\n                transform: translateX(0);\r\n                opacity: 1;\r\n            }\r\n        }\r\n\r\n        @keyframes fadeIn {\r\n            from {\r\n                opacity: 0;\r\n            }\r\n            to {\r\n                opacity: 1;\r\n            }\r\n        }\r\n\r\n        @keyframes slideUp {\r\n            from {\r\n                transform: translateY(20px);\r\n                opacity: 0;\r\n            }\r\n            to {\r\n                transform: translateY(0);\r\n                opacity: 1;\r\n            }\r\n        }\r\n        \r\n\r\n        /* 添加加载状态样式 */\r\n        .loading {\r\n            position: fixed;\r\n            top: 0;\r\n            left: 0;\r\n            right: 0;\r\n            bottom: 0;\r\n            background: rgba(255, 255, 255, 0.9);\r\n            display: flex;\r\n            justify-content: center;\r\n            align-items: center;\r\n            z-index: 2000;\r\n        }\r\n\r\n        .loading-spinner {\r\n            width: 50px;\r\n            height: 50px;\r\n            border: 3px solid var(--primary-color);\r\n            border-radius: 50%;\r\n            border-top-color: transparent;\r\n            animation: spin 1s linear infinite;\r\n        }\r\n\r\n        .empty-state {\r\n            text-align: center;\r\n            padding: 40px;\r\n            color: #666;\r\n        }\r\n\r\n        @keyframes spin {\r\n            to {\r\n                transform: rotate(360deg);\r\n            }\r\n        }\r\n\r\n        /* 修改刷新按钮位置和样式 */\r\n        .refresh-container {\r\n            position: relative;\r\n            margin-left: 20px;\r\n            display: inline-flex;\r\n            align-items: center;\r\n        }\r\n\r\n        .refresh-button {\r\n            width: 40px;\r\n            height: 40px;\r\n            position: relative;\r\n            border-radius: 50%;\r\n            background: var(--primary-color);\r\n            border: none;\r\n            cursor: pointer;\r\n            box-shadow: 0 2px 8px rgba(26, 115, 232, 0.3);\r\n            transition: all 0.3s ease;\r\n            overflow: hidden;\r\n        }\r\n\r\n        .refresh-button:hover {\r\n            transform: translateY(-2px);\r\n            box-shadow: 0 4px 12px rgba(26, 115, 232, 0.4);\r\n        }\r\n\r\n        .refresh-button:active {\r\n            transform: translateY(0);\r\n        }\r\n\r\n        .refresh-icon {\r\n            position: absolute;\r\n            top: 50%;\r\n            left: 50%;\r\n            transform: translate(-50%, -50%);\r\n            width: 24px;\r\n            height: 24px;\r\n            color: white;\r\n        }\r\n\r\n        /* 修改旋转动画 */\r\n        .refresh-button.loading .refresh-icon {\r\n            animation: refreshRotate 1s infinite linear;\r\n        }\r\n\r\n        @keyframes refreshRotate {\r\n            from {\r\n                transform: translate(-50%, -50%) rotate(0deg);\r\n            }\r\n            to {\r\n                transform: translate(-50%, -50%) rotate(360deg);\r\n            }\r\n        }\r\n\r\n        .refresh-ripple {\r\n            position: absolute;\r\n            top: 50%;\r\n            left: 50%;\r\n            transform: translate(-50%, -50%);\r\n            width: 0;\r\n            height: 0;\r\n            background: rgba(255, 255, 255, 0.4);\r\n            border-radius: 50%;\r\n            opacity: 1;\r\n            transition: all 0.6s ease-out;\r\n        }\r\n\r\n        .refresh-button.clicked .refresh-ripple {\r\n            width: 150%;\r\n            height: 150%;\r\n            opacity: 0;\r\n        }\r\n\r\n        /* 添加提示文字样式 */\r\n        .refresh-tooltip {\r\n            position: absolute;\r\n            bottom: -30px;\r\n            left: 50%;\r\n            transform: translateX(-50%);\r\n            background: rgba(0, 0, 0, 0.8);\r\n            color: white;\r\n            padding: 5px 10px;\r\n            border-radius: 4px;\r\n            font-size: 12px;\r\n            opacity: 0;\r\n            visibility: hidden;\r\n            transition: all 0.3s ease;\r\n            white-space: nowrap;\r\n        }\r\n\r\n        .refresh-button:hover .refresh-tooltip {\r\n            opacity: 1;\r\n            visibility: visible;\r\n            transform: translateX(-50%) translateY(0);\r\n        }\r\n\r\n        @keyframes success-scale {\r\n            0% { transform: scale(1); }\r\n            50% { transform: scale(1.2); }\r\n            100% { transform: scale(1); }\r\n        }\r\n\r\n        /* 添加邮件列表刷新动画 */\r\n        .email-list.refreshing .email-item {\r\n            animation: itemRefresh 0.5s ease-out;\r\n            opacity: 0.5;\r\n            pointer-events: none;\r\n        }\r\n\r\n        @keyframes itemRefresh {\r\n            0% {\r\n                transform: translateX(0);\r\n                opacity: 1;\r\n            }\r\n            50% {\r\n                transform: translateX(-10px);\r\n                opacity: 0.5;\r\n            }\r\n            100% {\r\n                transform: translateX(0);\r\n                opacity: 0.5;\r\n            }\r\n        }\r\n\r\n        /* 修改加载动画样式 */\r\n        .loading-overlay {\r\n            position: absolute;\r\n            top: 0;\r\n            left: 0;\r\n            right: 0;\r\n            bottom: 0;\r\n            background: rgba(255, 255, 255, 0.8);\r\n            display: flex;\r\n            justify-content: center;\r\n            align-items: center;\r\n            opacity: 0;\r\n            visibility: hidden;\r\n            transition: all 0.3s ease;\r\n        }\r\n\r\n        .loading-overlay.show {\r\n            opacity: 1;\r\n            visibility: visible;\r\n        }\r\n\r\n        .loading-dots {\r\n            display: flex;\r\n            gap: 8px;\r\n        }\r\n\r\n        .loading-dots span {\r\n            width: 8px;\r\n            height: 8px;\r\n            background: var(--primary-color);\r\n            border-radius: 50%;\r\n            animation: dotPulse 1s infinite;\r\n        }\r\n\r\n        .loading-dots span:nth-child(2) {\r\n            animation-delay: 0.2s;\r\n        }\r\n\r\n        .loading-dots span:nth-child(3) {\r\n            animation-delay: 0.4s;\r\n        }\r\n\r\n        @keyframes dotPulse {\r\n            0%, 100% { transform: scale(1); opacity: 0.3; }\r\n            50% { transform: scale(1.2); opacity: 1; }\r\n        }\r\n    </style>\r\n</head>\r\n<body>\r\n    <div id=\"loading\" class=\"loading\">\r\n        <div class=\"loading-spinner\"></div>\r\n    </div>\r\n\r\n    <header class='header'>\r\n        <div class='header-content'>\r\n            <div class='email-address' id=\"emailAddress\"></div>\r\n            <div style=\"display: flex; align-items: center;\">\r\n                <div class='email-count' id=\"emailCount\"></div>\r\n                <div class=\"refresh-container\">\r\n                    <button class=\"refresh-button\" id=\"refreshButton\" onclick=\"handleRefresh()\">\r\n                        <svg class=\"refresh-icon\" viewBox=\"0 0 24 24\" fill=\"none\" xmlns=\"http://www.w3.org/2000/svg\">\r\n                            <path d=\"M17.65 6.35C16.2 4.9 14.21 4 12 4C7.58 4 4.01 7.58 4.01 12C4.01 16.42 7.58 20 12 20C15.73 20 18.84 17.45 19.73 14H17.65C16.83 16.33 14.61 18 12 18C8.69 18 6 15.31 6 12C6 8.69 8.69 6 12 6C13.66 6 15.14 6.69 16.22 7.78L13 11H20V4L17.65 6.35Z\" fill=\"currentColor\"/>\r\n                        </svg>\r\n                        <div class=\"refresh-ripple\"></div>\r\n                        <span class=\"refresh-tooltip\">刷新邮件列表</span>\r\n                    </button>\r\n                </div>\r\n            </div>\r\n        </div>\r\n    </header>\r\n\r\n    <div class='container'>\r\n        <div class='email-list' id=\"emailList\">\r\n            <!-- 邮件列表将通过 JavaScript 动态插入 -->\r\n        </div>\r\n        <div class=\"loading-overlay\" id=\"listLoadingOverlay\">\r\n            <div class=\"loading-dots\">\r\n                <span></span>\r\n                <span></span>\r\n                <span></span>\r\n            </div>\r\n        </div>\r\n    </div>\r\n\r\n    <div id='emailModal' class='modal'>\r\n        <div class='modal-content'>\r\n            <span class='close'>&times;</span>\r\n            <div class='modal-header'>\r\n                <h2 class='modal-subject' id='modalSubject'></h2>\r\n                <div class='modal-info' id='modalInfo'></div>\r\n            </div>\r\n            <div class='modal-body' id='modalBody'></div>\r\n        </div>\r\n    </div>\r\n\r\n    <script>\r\n        const EMAIL = '{email}';\r\n        const API_URL = `https://api.pearktrue.cn/api/email?type=receive&email=${ EMAIL}`;\r\n\r\n        // 初始化页面\r\n        async function initializeEmailViewer() {\r\n            const loadingOverlay = document.getElementById('listLoadingOverlay');\r\n            loadingOverlay.classList.add('show');\r\n            \r\n            try {\r\n                // 添加错误处理和超时控制\r\n                const controller = new AbortController();\r\n                const timeoutId = setTimeout(() => controller.abort(), 10000); // 10秒超时\r\n\r\n                const response = await fetch(API_URL, {\r\n                    method: 'GET',\r\n                    signal: controller.signal,\r\n                    // 添加必要的请求头\r\n                    headers: {\r\n                        'Accept': 'application/json',\r\n                        'Origin': 'null'\r\n                    },\r\n                    // 允许跨域请求\r\n                    mode: 'cors'\r\n                });\r\n\r\n                clearTimeout(timeoutId);\r\n\r\n                if (!response.ok) {\r\n                    throw new Error(`HTTP error! status: ${ response.status}`);\r\n                }\r\n\r\n                const data = await response.json();\r\n                \r\n                // 更新邮箱地址\r\n                document.getElementById('emailAddress').textContent = EMAIL;\r\n\r\n                if (data.msg === \"暂无邮件\") {\r\n                    // 显示空状态\r\n                    document.getElementById('emailCount').style.display = 'none';\r\n                    document.getElementById('emailList').innerHTML = `\r\n                        <div class=\"empty-state\">\r\n                            <h2>暂无邮件</h2>\r\n                            <p>当前邮箱没有收到任何邮件</p>\r\n                        </div>\r\n                    `;\r\n                } else {\r\n                    // 显示邮件数量\r\n                    document.getElementById('emailCount').textContent = `共 ${ data.count} 封邮件`;\r\n                    \r\n                    // 对邮件按时间排序（最新的在前）\r\n                    const sortedEmails = data.receivedata.sort((a, b) => {\r\n                        const timeA = new Date(a.time.replace(/-/g, '/'));\r\n                        const timeB = new Date(b.time.replace(/-/g, '/'));\r\n                        return timeB - timeA; // 降序排列\r\n                    });\r\n                    \r\n                    // 生成邮件列表\r\n                    const emailListHtml = sortedEmails.map((email, index) => `\r\n                        <div class='email-item' style=\"--index: ${index + 1}\">\r\n                            <div class='email-left'>\r\n                                <div class='email-subject'>${ email.subject}</div>\r\n                                <div class='email-from'>${ email.from}</div>\r\n                            </div>\r\n                            <div class='email-right'>\r\n                                <div class='email-time'>${ email.time}</div>\r\n                                <div class='email-size'>${ email.size}</div>\r\n                            </div>\r\n                        </div>\r\n                    `).join('');\r\n                    \r\n                    document.getElementById('emailList').innerHTML = emailListHtml;\r\n\r\n                    // 添加点击事件时也使用排序后的数组\r\n                    document.querySelectorAll('.email-item').forEach((item, index) => {\r\n                        item.addEventListener('click', () => {\r\n                            const email = sortedEmails[index];\r\n                            document.getElementById('modalSubject').textContent = email.subject;\r\n                            document.getElementById('modalInfo').innerHTML = `\r\n                                从: ${ email.from}<br>\r\n                                时间: ${ email.time}<br>\r\n                                大小: ${ email.size}\r\n                            `;\r\n                            document.getElementById('modalBody').innerHTML = email.body.html || email.body.text;\r\n                            \r\n                            const modal = document.getElementById('emailModal');\r\n                            modal.style.display = 'block';\r\n                            requestAnimationFrame(() => {\r\n                                modal.classList.add('show');\r\n                            });\r\n                        });\r\n                    });\r\n                }\r\n            } catch (error) {\r\n                console.error('获取邮件失败:', error);\r\n                \r\n                // 提供更详细的错误信息\r\n                let errorMessage = '获取邮件数据时出现错误';\r\n                if (error.name === 'AbortError') {\r\n                    errorMessage = '请求超时，请检查网络连接';\r\n                } else if (error.message.includes('Failed to fetch')) {\r\n                    errorMessage = '网络请求失败，请检查网络连接或跨域设置';\r\n                }\r\n\r\n                document.getElementById('emailList').innerHTML = `\r\n                    <div class=\"empty-state\">\r\n                        <h2>加载失败</h2>\r\n                        <p>${ errorMessage}</p>\r\n                        <button onclick=\"retryLoad()\" style=\"\r\n                            margin-top: 20px;\r\n                            padding: 10px 20px;\r\n                            background: var(--primary-color);\r\n                            color: white;\r\n                            border: none;\r\n                            border-radius: 5px;\r\n                            cursor: pointer;\r\n                        \">重试</button>\r\n                    </div>\r\n                `;\r\n            } finally {\r\n                loadingOverlay.classList.remove('show');\r\n                document.getElementById('loading').style.display = 'none';\r\n            }\r\n        }\r\n\r\n        // 添加重试功能\r\n        function retryLoad() {\r\n            document.getElementById('loading').style.display = 'flex';\r\n            initializeEmailViewer();\r\n        }\r\n\r\n        // 模态框关闭逻辑\r\n        const modal = document.getElementById('emailModal');\r\n        const closeBtn = document.getElementsByClassName('close')[0];\r\n\r\n        closeBtn.onclick = function() {\r\n            modal.classList.remove('show');\r\n            setTimeout(() => {\r\n                modal.style.display = 'none';\r\n            }, 300);\r\n        }\r\n\r\n        window.onclick = function(event) {\r\n            if (event.target == modal) {\r\n                closeBtn.onclick();\r\n            }\r\n        }\r\n\r\n        // 修改刷新处理函数\r\n        async function handleRefresh() {\r\n            const button = document.getElementById('refreshButton');\r\n            const ripple = button.querySelector('.refresh-ripple');\r\n            const emailList = document.getElementById('emailList');\r\n            const loadingOverlay = document.getElementById('listLoadingOverlay');\r\n            \r\n            if (button.classList.contains('loading')) return;\r\n            \r\n            // 添加刷新效果\r\n            button.classList.add('clicked', 'loading');\r\n            emailList.classList.add('refreshing');\r\n            loadingOverlay.classList.add('show');\r\n            \r\n            // 重置波纹效果\r\n            setTimeout(() => {\r\n                button.classList.remove('clicked');\r\n                ripple.style.width = '0';\r\n                ripple.style.height = '0';\r\n            }, 600);\r\n\r\n            try {\r\n                await initializeEmailViewer();\r\n                \r\n                // 成功动画\r\n                button.classList.remove('loading');\r\n                button.style.animation = 'success-scale 0.5s ease';\r\n                setTimeout(() => {\r\n                    button.style.animation = '';\r\n                }, 500);\r\n            } catch (error) {\r\n                button.classList.remove('loading');\r\n            } finally {\r\n                emailList.classList.remove('refreshing');\r\n                loadingOverlay.classList.remove('show');\r\n            }\r\n        }\r\n\r\n        // 页面加载完成后初始化\r\n        document.addEventListener('DOMContentLoaded', initializeEmailViewer);\r\n    </script>\r\n</body>\r\n</html> "
            },
            "additionalBrowserArguments": {
              "VarKey": null,
              "Value": ""
            },
            "virtualHostToFolder": {
              "VarKey": null,
              "Value": ""
            },
            "userAgent": {
              "VarKey": null,
              "Value": ""
            },
            "title": {
              "VarKey": null,
              "Value": "临时邮箱"
            },
            "icon": {
              "VarKey": null,
              "Value": ""
            },
            "defaultBgColor": {
              "VarKey": null,
              "Value": ""
            },
            "autoCloseKey": {
              "VarKey": null,
              "Value": "="
            },
            "modeForExists": {
              "VarKey": null,
              "Value": "SkipThisStep"
            },
            "script": {
              "VarKey": null,
              "Value": ""
            },
            "winLocation": {
              "VarKey": null,
              "Value": "CenterScreen"
            },
            "winSize": {
              "VarKey": null,
              "Value": "50%,50%"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            },
            "defaultDownloadFolderPath": {
              "VarKey": null,
              "Value": ""
            },
            "profileName": {
              "VarKey": null,
              "Value": ""
            },
            "topMost": {
              "VarKey": null,
              "Value": "false"
            },
            "showInTaskbar": {
              "VarKey": null,
              "Value": "true"
            },
            "noActivate": {
              "VarKey": null,
              "Value": "false"
            },
            "closeWhenLostFocus": {
              "VarKey": null,
              "Value": "false"
            },
            "escCloseWindow": {
              "VarKey": null,
              "Value": "false"
            },
            "showToolbar": {
              "VarKey": null,
              "Value": "false"
            },
            "windowStyle": {
              "VarKey": null,
              "Value": "normal"
            },
            "clearCookies": {
              "VarKey": null,
              "Value": "0"
            },
            "addDevTool": {
              "VarKey": null,
              "Value": "0"
            }
          },
          "OutputParams": {
            "isSuccess": null,
            "hWnd": null,
            "webView": null,
            "errMessage": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": null,
      "Note": "选择【查看邮件】",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:simpleIf",
      "InputParams": {
        "condition": {
          "VarKey": null,
          "Value": "$= String.Equals({选择的操作}, \"获取新邮箱\", StringComparison.OrdinalIgnoreCase)"
        }
      },
      "OutputParams": {},
      "IfSteps": [
        {
          "StepRunnerKey": "sys:http",
          "InputParams": {
            "url": {
              "VarKey": null,
              "Value": "$$https://api.pearktrue.cn/api/email/?type=get"
            },
            "method": {
              "VarKey": null,
              "Value": "GET"
            },
            "header": {
              "VarKey": null,
              "Value": ""
            },
            "cookie": {
              "VarKey": null,
              "Value": ""
            },
            "resultType": {
              "VarKey": null,
              "Value": "Text"
            },
            "ua": {
              "VarKey": null,
              "Value": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/112.0.0.0 Safari/537.36"
            },
            "expireSeconds": {
              "VarKey": null,
              "Value": "100"
            },
            "noAutoRedirect": {
              "VarKey": null,
              "Value": "0"
            },
            "showProgress": {
              "VarKey": null,
              "Value": "0"
            },
            "skipCertVerify": {
              "VarKey": null,
              "Value": "0"
            },
            "forceProxy": {
              "VarKey": null,
              "Value": "0"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            },
            "useSSE": {
              "VarKey": null,
              "Value": "0"
            },
            "sseSpName": {
              "VarKey": null,
              "Value": ""
            }
          },
          "OutputParams": {
            "isSuccess": null,
            "statusCode": null,
            "respHeaders": null,
            "respCookies": null,
            "content": "返回结果",
            "imgResult": null,
            "errMessage": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:assign",
          "InputParams": {
            "input": {
              "VarKey": null,
              "Value": "$= return JsonConvert.DeserializeObject<Dictionary<string, string>>({返回结果});"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "isSuccess": null,
            "output": "res",
            "errMessage": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:MsgBox",
          "InputParams": {
            "operation": {
              "VarKey": null,
              "Value": "custom"
            },
            "message": {
              "VarKey": null,
              "Value": "$= \"成功获取临时邮箱：\" + \"\\n\" +\r\n{res}[\"email\"]"
            },
            "title": {
              "VarKey": null,
              "Value": "下一步操作"
            },
            "customIcon": {
              "VarKey": null,
              "Value": "Information"
            },
            "customButtons": {
              "VarKey": null,
              "Value": "[fa:Solid_Copy:#4caf50]复制|copy\r\n[fa:Solid_Save:#dc3545]保存|save"
            },
            "defaultButton": {
              "VarKey": null,
              "Value": "copy"
            },
            "restoreFocus": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "result": "选择的操作"
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:simpleIf",
          "InputParams": {
            "condition": {
              "VarKey": null,
              "Value": "$= String.Equals({选择的操作}, \"copy\", StringComparison.OrdinalIgnoreCase)"
            }
          },
          "OutputParams": {},
          "IfSteps": [
            {
              "StepRunnerKey": "sys:writeClipboard",
              "InputParams": {
                "type": {
                  "VarKey": null,
                  "Value": "auto"
                },
                "input": {
                  "VarKey": null,
                  "Value": "$= {res}[\"email\"]"
                },
                "successMsg": {
                  "VarKey": null,
                  "Value": "复制成功！"
                },
                "stopIfFail": {
                  "VarKey": null,
                  "Value": "1"
                }
              },
              "OutputParams": {
                "isSuccess": null,
                "errMessage": null
              },
              "IfSteps": null,
              "ElseSteps": null,
              "Note": "",
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            },
            {
              "StepRunnerKey": "sys:stop",
              "InputParams": {
                "method": {
                  "VarKey": null,
                  "Value": "default"
                },
                "isError": {
                  "VarKey": null,
                  "Value": "0"
                },
                "return": {
                  "VarKey": null,
                  "Value": ""
                },
                "showMessage": {
                  "VarKey": null,
                  "Value": ""
                }
              },
              "OutputParams": {},
              "IfSteps": null,
              "ElseSteps": null,
              "Note": "",
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            }
          ],
          "ElseSteps": null,
          "Note": "选择【copy】",
          "Disabled": false,
          "Collapsed": true,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:simpleIf",
          "InputParams": {
            "condition": {
              "VarKey": null,
              "Value": "$= String.Equals({选择的操作}, \"save\", StringComparison.OrdinalIgnoreCase)"
            }
          },
          "OutputParams": {},
          "IfSteps": [
            {
              "StepRunnerKey": "sys:listOperations",
              "InputParams": {
                "list": {
                  "VarKey": "配置_保存的邮箱",
                  "Value": null
                },
                "type": {
                  "VarKey": null,
                  "Value": "append"
                },
                "item": {
                  "VarKey": null,
                  "Value": "$={res}[\"email\"]"
                }
              },
              "OutputParams": {
                "isEmpty": null,
                "length": null
              },
              "IfSteps": null,
              "ElseSteps": null,
              "Note": "",
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            },
            {
              "StepRunnerKey": "sys:notify",
              "InputParams": {
                "type": {
                  "VarKey": null,
                  "Value": "Success"
                },
                "msg": {
                  "VarKey": null,
                  "Value": "保存成功！"
                },
                "maxLines": {
                  "VarKey": null,
                  "Value": "0"
                },
                "style": {
                  "VarKey": null,
                  "Value": "Default"
                },
                "clickAction": {
                  "VarKey": null,
                  "Value": ""
                }
              },
              "OutputParams": {},
              "IfSteps": null,
              "ElseSteps": null,
              "Note": "",
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            }
          ],
          "ElseSteps": null,
          "Note": "选择【save】",
          "Disabled": false,
          "Collapsed": true,
          "DelayMs": 0
        }
      ],
      "ElseSteps": null,
      "Note": "选择【获取新邮箱】",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```

</details>

***

## 56.屏幕取色/颜色转换与计算

**功能描述**
> 转换颜色值及相关计算处理

**官方文档**
> https://getquicker.net/KC/Help/Doc/color

**内部名称**
> sys:color

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| type | 类型 | 比较方式 | (9)选项-Enum（fromString: 通过文本指定颜色; selectFromScreen: 从屏幕选取颜色; fromScreenPosition: 取屏幕指定位置颜色; editOrSelectColor: 编辑/选择颜色） | fromString | True |
| colorStr | 颜色 | 颜色的文本值, 格式支持：#223344, #FF223344(ARGB顺序), Red, rgb(200,200,200), rgba(200,200,200,0.5), CMYK(0,0,0,0)或CMYK:0,0,0,0 | (0)字符串-Text |  | True |
| location | 坐标 | 格式为:“横坐标X,纵坐标Y” | (0)字符串-Text | 0,0 | True |
| format | 输出文本格式 | 输出的颜色文本值格式，用以转换颜色值的格式 | (9)选项-Enum（HEX_RGB: 十六进制RGB: #6496C8; HEX_ARGB: 十六进制ARGB: #FF6496C8; rgba: HTML: rgba(100,150,200,1); rgb: HTML: rgb(100,150,200); DOT_RGB: RGB: 100,150,200; DOT_RGBA: RGBA: 100,150,200,255; DOT_ARGB: ARGB: 255,100,150,200; float_rgba: 浮点: 0.39f, 0.59f, 0.78f, 1.00f; Swift: Swift: UIColor(red:0.39, green:0.59, blue:0.78, alpha:1.00); CMYK: CMYK: 50,25,0,22; HSL: hsl(210,47.6%,58.8%); hsla: hsla(210,47.6%,58.8%,1); HSV_HSB: HSV/HSB: 210°,50,78.4） | HEX_RGB | True |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| A | 透明度值 | Alpha值（0-255）0表示透明 | (1)数字(小数)-Number |
| R | 红色值 | R值（0-255） | (1)数字(小数)-Number |
| G | 绿色值 | G值（0-255） | (1)数字(小数)-Number |
| B | 蓝色值 | B值（0-255） | (1)数字(小数)-Number |
| Hue | 色相 | Hue值（0-360） | (1)数字(小数)-Number |
| HslS | HSL.S | HSL颜色空间的饱和度S | (1)数字(小数)-Number |
| HslL | HSL.L | HSL颜色空间的亮度值L | (1)数字(小数)-Number |
| HsvS | HSV.S | HSV颜色空间的饱和度S | (1)数字(小数)-Number |
| HsvV | HSV.V | HSV颜色空间的明度V | (1)数字(小数)-Number |
| textValue | 文本值 | 输出颜色的文本值，格式请在输入参数中选择 | (0)字符串-Text |

</details>
<details>
<summary>范例</summary>

**选中文本格式的颜色代码，并将其转为16进制RGB颜色值，然后发送文本到窗口**
```json
{
  "Variables": [
    {
      "Key": "color",
      "Type": 0,
      "Desc": "默认的文本变量",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:getSelectedText",
      "InputParams": {
        "format": {
          "VarKey": null,
          "Value": "UnicodeText"
        },
        "repeat": {
          "VarKey": null,
          "Value": "0"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {
        "output": "color",
        "isSuccess": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:color",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "editOrSelectColor"
        },
        "colorStr": {
          "VarKey": "color",
          "Value": null
        },
        "format": {
          "VarKey": null,
          "Value": "HEX_RGB"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "A": null,
        "R": null,
        "G": null,
        "B": null,
        "Hue": null,
        "HslS": null,
        "HslL": null,
        "HsvS": null,
        "HsvV": null,
        "textValue": "color"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:outputText",
      "InputParams": {
        "content": {
          "VarKey": "color",
          "Value": null
        },
        "method": {
          "VarKey": null,
          "Value": "paste"
        },
        "delayBeforePaste": {
          "VarKey": null,
          "Value": "50"
        },
        "delayAfterPaste": {
          "VarKey": null,
          "Value": "10"
        },
        "appendReturn": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 57.计算时间

**功能描述**
> 时间相关的计算操作

**官方文档**
> https://getquicker.net/KC/Help/Doc/computetime

**内部名称**
> sys:computeTime

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| type | 类型 | 比较方式 | (9)选项-Enum（getdate: 取日期值（去除当天的时间部分）; timespan: 计算时间差（日期时间2 减 日期时间）; endtime: 计算结束时间; localToUtc: 本地时间转换为UTC时间; utcToLocal: UTC时间转换为本地时间） | getdate | True |
| time1 | 日期时间 | 要计算的时间值 | (6)时间日期-DateTime |  | True |
| time2 | 日期时间2 | 要计算的第二个时间值 | (6)时间日期-DateTime |  | True |
| formatString | 格式化字符串 | 时间差转换为文本时的格式化字符串。d:天数,hh:小时,mm:分钟,ss:秒。符号.:需要使用\转义 | (0)字符串-Text | d\.hh\:mm\:ss | True |
| addYears | 添加年数 | 添加指定的年数（整数） | (1)数字(小数)-Number | 0 | False |
| addMonths | 添加月数 | 添加指定的月数（整数）结果不跨月，如1月31日增加1个月等于2月28日。 | (1)数字(小数)-Number | 0 | False |
| addDays | 添加天数 | 添加指定的天数（可以为小数） | (1)数字(小数)-Number | 0 | False |
| addHours | 添加小时数 | 添加指定的小时数（可以为小数） | (1)数字(小数)-Number | 0 | False |
| addMinutes | 添加分钟数 | 添加指定的分钟数（可以为小数） | (1)数字(小数)-Number | 0 | False |
| addSeconds | 添加秒数 | 添加指定的秒数（可以为小数） | (1)数字(小数)-Number | 0 | False |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| resultTime | 结果时间 | 计算的结果时间 | (6)时间日期-DateTime |
| totalDays | 总天数 | 间隔的总天数值 | (1)数字(小数)-Number |
| totalHours | 总小时数 | 间隔的总小时数 | (1)数字(小数)-Number |
| totalMinutes | 总分钟数 | 间隔的总分钟数值 | (1)数字(小数)-Number |
| totalSeconds | 总秒数 | 间隔的总秒数数值 | (1)数字(小数)-Number |
| textValue | 文本值 | 时间间隔的文本结果 | (0)字符串-Text |

</details>
<details>
<summary>范例</summary>

**获取time1经过2年3个月4天5小时6分钟后的时间并存入time2变量，接下来计算time2减去time1总共有多少个小时并存入totalHours变量**
```json
{
  "Variables": [
    {
      "Key": "time1",
      "Type": 6,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "time2",
      "Type": 6,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "totalHours",
      "Type": 1,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:computeTime",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "endtime"
        },
        "time1": {
          "VarKey": "time1",
          "Value": null
        },
        "addYears": {
          "VarKey": null,
          "Value": "2"
        },
        "addMonths": {
          "VarKey": null,
          "Value": "3"
        },
        "addDays": {
          "VarKey": null,
          "Value": "4"
        },
        "addHours": {
          "VarKey": null,
          "Value": "5"
        },
        "addMinutes": {
          "VarKey": null,
          "Value": "6"
        },
        "addSeconds": {
          "VarKey": null,
          "Value": "0"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "resultTime": "time2",
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:computeTime",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "timespan"
        },
        "time1": {
          "VarKey": "time2",
          "Value": null
        },
        "time2": {
          "VarKey": "time1",
          "Value": null
        },
        "formatString": {
          "VarKey": null,
          "Value": "d\\.hh\\:mm\\:ss"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "totalDays": null,
        "totalHours": "totalHours",
        "totalMinutes": null,
        "totalSeconds": null,
        "textValue": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 58.词典操作

**功能描述**
> 对词典变量进行添加、删除等操作

**官方文档**
> https://getquicker.net/KC/Help/Doc/dictoperations

**内部名称**
> sys:dictOperations

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| type | 操作类型 |  | (9)选项-Enum（get: 取值; set: 设置值 (文本类型); setOriginValue: 设置值 (变量原始类型); remove: 删除一项; clear: 清空; keyList: 获取键(Key)列表; valueList: 获取值列表; reverse: 翻转键值; queryStringToDict: 查询字符串转换为词典(name1=value1&name2=value2...); dictToQueryString: 词典转换为查询字符串; dictToQueryStringNoEncode: 词典转换为查询字符串(不对键和值进行URL编码)） | setOriginValue | False |
| dict | 词典 | 要操作的词典变量 | (10)词典-Dict |  | False |
| queryString | 查询字符串 | 要解析的查询字符串 | (0)字符串-Text |  | False |
| key | 键 | 要操作元素的键值。 | (0)字符串-Text |  | False |
| value | 值 | 要保存的内容 | (0)字符串-Text |  | False |
| returnEmptyIfKeyNotExist | 键不存在时返回空值 | 此时不作为失败处理 | (2)布尔值-Boolean | False | False |
| ignoreCase | 忽略键的大小写 |  | (2)布尔值-Boolean | False | False |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | False | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| value | 结果 | 操作后的输出（取的元素值、键列表、值列表等） | (99)任意类型-Any |

</details>
<details>
<summary>范例</summary>

```json
{
  "Variables": [
    {
      "Key": "示例词典",
      "Type": 10,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": null,
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "示例列表",
      "Type": 4,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": null,
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "x的值",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": null,
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "词典的键列表",
      "Type": 0,
      "Desc": "书名列表",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": null,
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "词典的值列表",
      "Type": 0,
      "Desc": "书的内容",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": null,
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "赋值：把词典当作一个作文全集，现在开始把作文放进去，一篇一篇的放。一个作文名（键），对作文的内容（值）。注意！！！放的时候作文名（键）不能重复，否则会直接无视，放不进来。但是作文的内容（值）可以一样。"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:assign",
      "InputParams": {
        "input": {
          "VarKey": null,
          "Value": "111:词典里面的第一个值\r\n222:第2 个了\r\n333:我只能是3了\r\nup:我是上\r\ndown:我是下的坐标\r\nx:我是x坐标999\r\ny:我是一y坐标222"
        }
      },
      "OutputParams": {
        "output": "示例词典"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "赋值给词典",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:assign",
      "InputParams": {
        "input": {
          "VarKey": null,
          "Value": "AAA:aaa\r\nbbb:BBB\r\nCCC:ccc"
        }
      },
      "OutputParams": {
        "output": "示例列表"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "给列表赋值",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "设置值：词典里面可以放文本，数字，时间，列表，甚至是词典（词典里面放词典）等等。放列表就相当与直接把某一类型的很多篇作文当进去。取的时候就要知道类型名，然后再取作文名。"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:dictOperations",
      "InputParams": {
        "dict": {
          "VarKey": "示例词典",
          "Value": null
        },
        "type": {
          "VarKey": null,
          "Value": "set"
        },
        "key": {
          "VarKey": null,
          "Value": "我是示例列表"
        },
        "value": {
          "VarKey": "示例列表",
          "Value": null
        },
        "ignoreCase": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {
        "value": null,
        "isSuccess": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "把列表放到词典里，并且把键名设置为：我是示例列表",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "取值：键就相当于作文名，值就相当于作文的内容。你要取作文就先要知道作文名，我有作文名了，就能取到作文，就能得到内容，也就是值。"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:dictOperations",
      "InputParams": {
        "dict": {
          "VarKey": "示例词典",
          "Value": null
        },
        "type": {
          "VarKey": null,
          "Value": "get"
        },
        "key": {
          "VarKey": null,
          "Value": "x"
        },
        "value": {
          "VarKey": null,
          "Value": ""
        },
        "ignoreCase": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {
        "value": "x的值",
        "isSuccess": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "删除值：一些不需要的作文就要从作文全集拿出去。通过作文名找到，然后把这篇作文拿出去，查找目录上消除这篇作文名（键），当然作文的内容（值）自然也就没了。"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:dictOperations",
      "InputParams": {
        "dict": {
          "VarKey": "示例词典",
          "Value": null
        },
        "type": {
          "VarKey": null,
          "Value": "remove"
        },
        "key": {
          "VarKey": null,
          "Value": "y"
        },
        "value": {
          "VarKey": null,
          "Value": ""
        },
        "ignoreCase": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {
        "value": null,
        "isSuccess": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "删除名叫y的作文",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "取列表：就相当与开篇的目录，得到作文名列表（键列表），同样的，可以获取到作文的内容列表。"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:dictOperations",
      "InputParams": {
        "dict": {
          "VarKey": "示例词典",
          "Value": null
        },
        "type": {
          "VarKey": null,
          "Value": "keyList"
        },
        "key": {
          "VarKey": null,
          "Value": ""
        },
        "value": {
          "VarKey": null,
          "Value": ""
        },
        "ignoreCase": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {
        "value": "词典的键列表",
        "isSuccess": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:dictOperations",
      "InputParams": {
        "dict": {
          "VarKey": "示例词典",
          "Value": null
        },
        "type": {
          "VarKey": null,
          "Value": "valueList"
        },
        "key": {
          "VarKey": null,
          "Value": ""
        },
        "value": {
          "VarKey": null,
          "Value": ""
        },
        "ignoreCase": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {
        "value": "词典的值列表",
        "isSuccess": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:showText",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "NO_WAIT"
        },
        "text": {
          "VarKey": null,
          "Value": "$$x的值：\r\n{x的值}\r\n\r\n键列表：\r\n{词典的键列表}\r\n\r\n值列表：\r\n{词典的值列表}\r\n\r\n最后这个词典的样子，示例词典：\r\n{示例词典}\r\n\r\n"
        },
        "title": {
          "VarKey": null,
          "Value": "结果内容"
        },
        "operations": {
          "VarKey": null,
          "Value": ""
        },
        "winLocation": {
          "VarKey": null,
          "Value": "CenterScreen"
        }
      },
      "OutputParams": {
        "selectedOperation": null,
        "resultText": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 59.使用Everything搜索文件

**功能描述**
> 调用Everything提供的接口搜索文件

**官方文档**
> https://getquicker.net/KC/Help/Doc/everythingsearch

**内部名称**
> sys:everythingsearch

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| search | 搜索内容 | 要搜索的内容，格式与直接在everything软件中搜索时相同。 | (0)字符串-Text |  | True |
| folder | 限定目录 | 可选。在指定目录下搜索（包含子目录）。 | (0)字符串-Text |  | False |
| ext | 扩展名 | 可选。半角分号分隔的扩展名列表。如“txt;docx;xslx;” | (0)字符串-Text |  | False |
| matchWholeFilename | 匹配完整文件名 | 匹配整个文件名。0表示否，1表示是。 | (2)布尔值-Boolean | 0 | False |
| matchWholeWord | 匹配整个单词 | 匹配整个单词。如 quicker.exe 将会匹配：quicker.exe, quicker.exe.config等。0表示否，1表示是。 | (2)布尔值-Boolean | 1 | False |
| matchPath | 匹配路径 | 匹配路径的不同部分，而不仅是文件名。 | (2)布尔值-Boolean | 0 | False |
| matchCase | 匹配大小写 | 是否大小写敏感。0表示否，1表示是。 | (2)布尔值-Boolean | 0 | False |
| useRegex | 使用正则匹配 | 是否使用正则匹配。0表示否，1表示是。 | (2)布尔值-Boolean | 0 | False |
| maxCount | 最大结果数量 | -1表示不限制 | (12)数字(整数)-Integer | 100 | True |
| sort | 排序方式 |  | (9)选项-Enum（1: 名称顺序 NAME_ASCENDING; 2: 名称倒序 NAME_DESCENDING; 3: 路径顺序 PATH_ASCENDING; 4: 路径倒序 PATH_DESCENDING; 5: 大小顺序 SIZE_ASCENDING; 6: 大小倒序 SIZE_DESCENDING; 7: 扩展名顺序 EXTENSION_ASCENDING; 8: 扩展名倒序 EXTENSION_DESCENDING; 9: 类型名顺序 TYPE_NAME_ASCENDING; 10: 类型名倒序 TYPE_NAME_DESCENDING; 11: 创建时间顺序 DATE_CREATED_ASCENDING; 12: 创建时间倒序 DATE_CREATED_DESCENDING; 13: 修改时间顺序 DATE_MODIFIED_ASCENDING; 14: 修改时间倒序 DATE_MODIFIED_DESCENDING; 15: 属性顺序 ATTRIBUTES_ASCENDING; 16: 属性倒序 ATTRIBUTES_DESCENDING; 17: 文件列表文件名顺序 FILE_LIST_FILENAME_ASCENDING; 18: 文件列表文件名倒序 FILE_LIST_FILENAME_DESCENDING; 19: 运行次数顺序 RUN_COUNT_ASCENDING; 20: 运行次数倒序 RUN_COUNT_DESCENDING; 21: 最后变更时间顺序 DATE_RECENTLY_CHANGED_ASCENDING; 22: 最后变更时间倒序 DATE_RECENTLY_CHANGED_DESCENDING; 23: 最后访问时间顺序 DATE_ACCESSED_ASCENDING; 24: 最后访问时间倒序 DATE_ACCESSED_DESCENDING; 25: 最后运行时间顺序 DATE_RUN_ASCENDING; 26: 最后运行时间倒序 DATE_RUN_DESCENDING） | 1 | True |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| pathList | 路径列表 |  | (4)文本列表-List |
| resultCount | 结果个数 |  | (12)数字(整数)-Integer |
| rawResult | 原始结果 |  | (98)对象(Object)-Object |

</details>
<details>
<summary>范例</summary>

**在D:\Zr下搜索a.txt，匹配完整文件名，匹配整个单词，匹配大小写，最大结果数量为1，结果存入pathList；然后输出pathList的第一个元素**
```json
{
  "Variables": [
    {
      "Key": "pathList",
      "Type": 4,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:everythingsearch",
      "InputParams": {
        "search": {
          "VarKey": null,
          "Value": "a.txt"
        },
        "folder": {
          "VarKey": null,
          "Value": "D:\\Zr"
        },
        "ext": {
          "VarKey": null,
          "Value": ""
        },
        "matchWholeFilename": {
          "VarKey": null,
          "Value": "1"
        },
        "matchWholeWord": {
          "VarKey": null,
          "Value": "1"
        },
        "matchPath": {
          "VarKey": null,
          "Value": "0"
        },
        "matchCase": {
          "VarKey": null,
          "Value": "1"
        },
        "useRegex": {
          "VarKey": null,
          "Value": "0"
        },
        "maxCount": {
          "VarKey": null,
          "Value": "1"
        },
        "sort": {
          "VarKey": null,
          "Value": "1"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "pathList": "pathList",
        "resultCount": null,
        "rawResult": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:notify",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "Info"
        },
        "msg": {
          "VarKey": null,
          "Value": "$={pathList}[0]"
        },
        "maxLines": {
          "VarKey": null,
          "Value": "0"
        },
        "style": {
          "VarKey": null,
          "Value": "Default"
        },
        "clickAction": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 60.文件和目录操作

**功能描述**
> 文件和目录操作。请确保路径是合法的。

**官方文档**
> https://getquicker.net/KC/Help/Doc/fileoperation

**内部名称**
> sys:fileOperation

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| type | 操作类型 | 操作类型 | (9)选项-Enum（copyInto: 复制到指定目录下; copyIntoWithShell: 复制到指定目录下(Windows); copyTo: 复制为（指定结果名称或路径）; moveInto: 移动到指定目录下; moveIntoWithShell: 移动到指定目录下(Windows); rename: 移动/重命名为（指定结果名称或完整路径）; deleteFile: 删除文件（不支持文件夹）; deleteEmptyFolder: 删除空文件夹; recycle: 移入回收站; recycleNoUi: 移入回收站（安静模式，自动确认操作）; makeDir: 创建文件夹; createFile: 创建空文件; enumFiles: 获取文件夹内的文件; enumDirs: 获取文件夹内的子文件夹; copyFile: 复制文件/文件夹（自动）【不建议使用】; moveFile: 移动/重命名文件(夹)（自动）【不建议使用】） |  | True |
| path | 路径 | 要操作的文件或文件夹路径 | (0)字符串-Text |  | False |
| dstPath | 目标路径/名称 | 复制/移动的目标路径或新文件、文件名。详情请参考文档。 | (0)字符串-Text |  | False |
| searchPattern | 搜索内容 | 筛选文件或目录名。可以包含通配符*和?，或“regex:正则表达式”。搜索文件时也可以为分号隔开的多个后缀名如.jpg;.png;.bmp | (0)字符串-Text | * | False |
| isAll | 包含子目录 | 包含子目录中的(否则只搜索顶层目录) | (2)布尔值-Boolean | False | False |
| overwrite | 覆盖已有 | 如果目标位置已存在文件，是否覆盖？ | (2)布尔值-Boolean | False | False |
| stopIfFail | 失败后中止动作 | 如果操作异常，是否终止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| files | 路径列表 | 搜索到的文件或文件夹列表 | (4)文本列表-List |
| resultPath | 结果路径 | 结果文件路径 | (0)字符串-Text |

</details>
<details>
<summary>范例</summary>

**在当前文件夹下创建指定名称的docx文件并打开**
```json
{
  "Variables": [
    {
      "Key": "path",
      "Type": 0,
      "Desc": "当前路径",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": null,
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "filename",
      "Type": 0,
      "Desc": "用户输入的文件名，不包含扩展名",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": null,
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "isSuccess",
      "Type": 2,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": null,
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "fullPath",
      "Type": 0,
      "Desc": "完整路径",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": null,
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "quickerVersion",
      "Type": 1,
      "Desc": "Quicker版本号",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": null,
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:getSysInfo",
      "InputParams": {},
      "OutputParams": {
        "MachineName": null,
        "userName": null,
        "userDomainName": null,
        "OsVersion": null,
        "isWin10": null,
        "startupSeconds": null,
        "sysEnv": null,
        "quickerVersion": "quickerVersion",
        "runnedSeconds": null,
        "actionId": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:if",
      "InputParams": {
        "condition": {
          "VarKey": null,
          "Value": "$${quickerVersion} < 1000011"
        }
      },
      "OutputParams": {},
      "IfSteps": [
        {
          "StepRunnerKey": "sys:notify",
          "InputParams": {
            "msg": {
              "VarKey": null,
              "Value": "需要Quicker 1.0.11或更新版本支持。"
            },
            "type": {
              "VarKey": null,
              "Value": "Warning"
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:stop",
          "InputParams": {},
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": [],
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:getExplorerPath",
      "InputParams": {},
      "OutputParams": {
        "output": "path"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "得到当前文件夹路径"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:userInput",
      "InputParams": {
        "prompt": {
          "VarKey": null,
          "Value": "请输入文件名"
        },
        "type": {
          "VarKey": null,
          "Value": "text"
        },
        "defaultValue": {
          "VarKey": null,
          "Value": "xxx文件"
        },
        "pattern": {
          "VarKey": null,
          "Value": ""
        },
        "restoreFocus": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {
        "textValue": "filename",
        "numberValue": null,
        "isEmpty": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "组合成完整文件名"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:assign",
      "InputParams": {
        "input": {
          "VarKey": null,
          "Value": "$${path}/{filename}.docx"
        }
      },
      "OutputParams": {
        "output": "fullPath"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "创建文件"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:fileOperation",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "createFile"
        },
        "path": {
          "VarKey": "fullPath",
          "Value": null
        },
        "dstPath": {
          "VarKey": null,
          "Value": ""
        },
        "searchPattern": {
          "VarKey": null,
          "Value": "*"
        },
        "isAll": {
          "VarKey": null,
          "Value": "0"
        },
        "overwrite": {
          "VarKey": null,
          "Value": "0"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {
        "files": null,
        "isSuccess": "isSuccess"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "如果创建成功了，则打开"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:if",
      "InputParams": {
        "condition": {
          "VarKey": "isSuccess",
          "Value": null
        }
      },
      "OutputParams": {},
      "IfSteps": [
        {
          "StepRunnerKey": "sys:run",
          "InputParams": {
            "path": {
              "VarKey": "fullPath",
              "Value": null
            },
            "arg": {
              "VarKey": null,
              "Value": ""
            },
            "setWorkingDir": {
              "VarKey": null,
              "Value": ""
            },
            "windowStyle": {
              "VarKey": null,
              "Value": "0"
            },
            "runas": {
              "VarKey": null,
              "Value": "0"
            },
            "waitInputIdle": {
              "VarKey": null,
              "Value": "0"
            },
            "waitExit": {
              "VarKey": null,
              "Value": "0"
            },
            "alternativePath": {
              "VarKey": null,
              "Value": ""
            }
          },
          "OutputParams": {
            "pid": null,
            "mainWinHandle": null,
            "mainWinTitle": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": [],
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 61.生成临时文件路径

**功能描述**
> 根据指定的扩展名生成一个随机的临时文件名（完整路径），供后续步骤写入文件使用。

**官方文档**
> https://getquicker.net/KC/Help/Doc/gentempfilepath

**内部名称**
> sys:GenTempFilePath

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| ext | 扩展名 | 生成临时文件的扩展名 | (0)字符串-Text | .txt | True |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| filePath | 文件路径 | 生成的临时文件路径 | (0)字符串-Text |

</details>
<details>
<summary>范例</summary>

**生成txt临时文件名称到filePath变量**
```json
{
  "Variables": [
    {
      "Key": "filePath",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:GenTempFilePath",
      "InputParams": {
        "ext": {
          "VarKey": null,
          "Value": ".txt"
        }
      },
      "OutputParams": {
        "filePath": "filePath"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 62.获取选择的文件(夹)/选择特定文件

**功能描述**
> 获取资源管理器、桌面等位置选择的文件或文件夹的路径

**官方文档**
> https://getquicker.net/KC/Help/Doc/getselectedfiles

**内部名称**
> sys:getSelectedFiles

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| operation | 操作类型 |  | (9)选项-Enum（getSelection: 获取选择的文件; setSelection: 设置选择的文件） | getSelection | False |
| waitMs | 等待剪贴板时间 | 通过复制方式获取选择文件时，等待剪贴板变化的最长时间毫秒数。 | (12)数字(整数)-Integer | 200 | False |
| sortType | 排序文件列表 | 获取多个文件时，根据需要可以对文件列表进行排序。仅支持文件。 | (9)选项-Enum（Default: 默认（文件名自然排序）; Origin: 原始（系统返回顺序）; FileName: 文件名（字母顺序）; FileNameNature: 文件名（自然顺序）; FileSizeAsc: 文件大小（从小到大）; FileSizeDesc: 文件大小（从大到小）; CreationTimeDesc: 创建时间（从新到旧）; CreationTimeAsc: 创建时间（从旧到新）; LastAccessTimeDesc: 最后访问时间（从晚到早）; LastAccessTimeAsc: 最后访问时间（从早到晚）; LastWriteTimeDesc: 最后写入时间（从晚到早）; LastWriteTimeAsc: 最后写入时间（从早到晚）） | Default | False |
| pathList | 路径或文件名 | 要选中的路径或文件名。支持使用 “regex:表达式” “pinyin:筛选” 选择匹配的文件。 | (0)字符串-Text |  | False |
| stopIfFail | 失败后中止动作 | 获取失败后，是否停止后续动作的执行。 | (2)布尔值-Boolean | True | False |
| winHandle | 指定窗口句柄 | 指定要操作的资源管理器窗口，留空时表示前台窗口。（仅支持资源管理器） | (12)数字(整数)-Integer |  | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 是否成功获得文件列表 | (2)布尔值-Boolean |
| files | 路径列表 | 所有选中的文件和文件夹的路径列表 | (4)文本列表-List |
| firstFile | 首个路径 | 选择1个文件(夹)时，返回其路径；选择多个时，返回第一个的路径。 | (0)字符串-Text |
| fileNames | 文件(夹)名列表 | 所有选中的文件和文件夹的名称的列表（不包含所在路径） | (4)文本列表-List |
| firstFileName | 首个文件(夹)名 | 选择1个文件(夹)时，返回其名称；选择多个时，返回第一个的名称。 | (0)字符串-Text |
| fileCount | 文件个数 | 选择的文件个数 | (12)数字(整数)-Integer |

</details>
<details>
<summary>范例</summary>

**获取选择的第一个文件**
```json
{
  "Variables": [
    {
      "Key": "firstFile",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:getSelectedFiles",
      "InputParams": {
        "operation": {
          "VarKey": null,
          "Value": "getSelection"
        },
        "waitMs": {
          "VarKey": null,
          "Value": "200"
        },
        "sortType": {
          "VarKey": null,
          "Value": "Default"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "files": null,
        "firstFile": "firstFile",
        "fileNames": null,
        "firstFileName": null,
        "fileCount": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 63.读取文件

**功能描述**
> 将读取的文本或图片内容写入变量。

**官方文档**
> https://getquicker.net/KC/Help/Doc/readFile

**内部名称**
> sys:readFile

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| path | 文件路径 | 要读取的文件的完整路径。 | (0)字符串-Text |  | True |
| type | 格式 | 文件内容类型 | (9)选项-Enum（text: 文本; image: 图片） | text | True |
| encoding | 文件编码 | 文件的编码格式 | (9)选项-Enum | utf-8 | True |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| txt | 文本内容 | 读取的文本文件的内容 | (0)字符串-Text |
| image | 图片内容 | 读取的图片文件的内容 | (3)图片-Image |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |

</details>
<details>
<summary>范例</summary>

**读取下载目录下的a.txt并用文本窗口显示出来**
```json
{
  "Variables": [
    {
      "Key": "folder",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "filePath",
      "Type": 0,
      "Desc": "文件路径",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "fileContent",
      "Type": 0,
      "Desc": "文件内容",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "isSuccess",
      "Type": 2,
      "Desc": "读取文件是否成功",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": null,
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:getFolderPath",
      "InputParams": {
        "folder": {
          "VarKey": null,
          "Value": "Downloads"
        }
      },
      "OutputParams": {
        "path": "folder"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "获取下载目录路径",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:pathExtraction",
      "InputParams": {
        "operation": {
          "VarKey": null,
          "Value": "combine"
        },
        "path": {
          "VarKey": "folder",
          "Value": null
        },
        "path2": {
          "VarKey": null,
          "Value": "a.txt"
        }
      },
      "OutputParams": {
        "resultPath": "filePath"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "生成 a.txt 的完整路径",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:readFile",
      "InputParams": {
        "path": {
          "VarKey": "filePath",
          "Value": null
        },
        "type": {
          "VarKey": null,
          "Value": "text"
        },
        "encoding": {
          "VarKey": null,
          "Value": "utf-8"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {
        "txt": "fileContent",
        "isSuccess": "isSuccess",
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "读取文件内容",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:if",
      "InputParams": {
        "condition": {
          "VarKey": "isSuccess",
          "Value": null
        }
      },
      "OutputParams": {},
      "IfSteps": [
        {
          "StepRunnerKey": "sys:showText",
          "InputParams": {
            "type": {
              "VarKey": null,
              "Value": "NO_WAIT"
            },
            "text": {
              "VarKey": "fileContent",
              "Value": null
            },
            "title": {
              "VarKey": null,
              "Value": "a.txt 内容"
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "显示文件内容",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": [
        {
          "StepRunnerKey": "sys:notify",
          "InputParams": {
            "type": {
              "VarKey": null,
              "Value": "Error"
            },
            "msg": {
              "VarKey": null,
              "Value": "无法读取 a.txt 文件"
            },
            "maxLines": {
              "VarKey": null,
              "Value": "0"
            },
            "style": {
              "VarKey": null,
              "Value": "Default"
            },
            "clickAction": {
              "VarKey": null,
              "Value": ""
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "显示错误消息",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "Note": "检查读取是否成功",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 64.选择文件

**功能描述**
> 用文件选择对话框选择要打开或保存的文件

**官方文档**
> https://getquicker.net/KC/Help/Doc/selectfile

**内部名称**
> sys:selectFile

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| type | 操作类型 | 打开文件：选择一个已存在的文件。保存文件：选择文件要保存的目标位置。 | (9)选项-Enum（saveFile: 保存文件; openFile: 打开文件; openMultiFile: 打开多个文件） | openFile | True |
| filter | 文件类型筛选器 | 文件类型筛选器，格式为：类型1|扩展名1|类型2|扩展名2。如：文本文件(*.txt)|*.txt|C#文件|*.cs|所有文件|*.* | (0)字符串-Text | 文本文件|*.txt|所有文件|*.* | False |
| defaultExt | 默认扩展名 | 默认的文件扩展名，应该是筛选器里的一种 | (0)字符串-Text | .txt | False |
| initDir | 初始路径 | 初始文件夹路径 | (0)字符串-Text |  | False |
| initFileName | 初始文件名 | 预选选择或设置的文件名 | (0)字符串-Text |  | False |
| title | 对话框标题 | 选择窗口的标题 | (0)字符串-Text |  | False |
| topMost | 置顶显示 | 是否置置顶显示窗口。 | (2)布尔值-Boolean | True | False |
| stopIfFail | 取消后停止 | 取消后是否停止动作运行 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 是否成功选择了路径。 | (2)布尔值-Boolean |
| path | 路径 | 选择的文件路径。 | (0)字符串-Text |
| pathList | 路径列表 | 选择的文件路径列表。 | (4)文本列表-List |

</details>
<details>
<summary>范例</summary>

**选择多个文件，返回选择的文件名列表pathList**
```json
{
  "Variables": [
    {
      "Key": "pathList",
      "Type": 4,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:selectFile",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "openMultiFile"
        },
        "filter": {
          "VarKey": null,
          "Value": "文本文件|*.txt|所有文件|*.*"
        },
        "defaultExt": {
          "VarKey": null,
          "Value": ".txt"
        },
        "initDir": {
          "VarKey": null,
          "Value": ""
        },
        "initFileName": {
          "VarKey": null,
          "Value": ""
        },
        "title": {
          "VarKey": null,
          "Value": ""
        },
        "topMost": {
          "VarKey": null,
          "Value": "1"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "pathList": "pathList",
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 65.选择文件夹

**功能描述**
> 文件夹选择对话框

**官方文档**
> https://getquicker.net/KC/Help/Doc/selectfolder

**内部名称**
> sys:selectFolder

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| prompt | 提示文字 | 选择窗口的标题 | (0)字符串-Text | 请选择文件夹 | True |
| initDir | 初始路径 | 初始文件夹路径 | (0)字符串-Text |  | False |
| showOpenedDirs | 显示已打开的文件夹 | 显示当前在资源管理器窗口中打开的文件夹。 | (2)布尔值-Boolean | True | False |
| stopIfFail | 取消后停止 | 取消后是否停止动作运行 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 是否成功选择了路径。 | (2)布尔值-Boolean |
| path | 路径 | 选择的文件夹路径。 | (0)字符串-Text |

</details>
<details>
<summary>范例</summary>

**让用户在D:\\选择文件夹，返回选择的path**
```json
{
  "Variables": [
    {
      "Key": "path",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:selectFolder",
      "InputParams": {
        "prompt": {
          "VarKey": null,
          "Value": "请选择文件夹"
        },
        "initDir": {
          "VarKey": null,
          "Value": "D:\\"
        },
        "showOpenedDirs": {
          "VarKey": null,
          "Value": "1"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "path": "path",
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 66.写入文本文件

**功能描述**
> 将内容写入文本文件

**官方文档**
> https://getquicker.net/KC/Help/Doc/writetextfile

**内部名称**
> sys:WriteTextFile

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| content | 内容 | 要写入文件的内容 | (0)字符串-Text |  | True |
| filePath | 文件路径 | 要写入的完整文件路径（包含文件名） | (0)字符串-Text |  | True |
| encoding | 文件编码 | 写入文件的编码格式 | (9)选项-Enum | utf-8 | True |
| addUtf8Bom | 添加UTF-BOM | UTF8编码文件是否写入BOM标记 | (2)布尔值-Boolean | False | False |
| appendMode | 添加到文件末尾 | 如果文件已存在，则添加到文件的末尾 | (2)布尔值-Boolean | False | False |
| addNewLine | 添加空行 | 在文件末尾添加空行 | (2)布尔值-Boolean | False | False |
| newLineChars | 统一换行字符 |  | (9)选项-Enum（: 默认（不处理）; \r\n; \r; \n） |  | True |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |

</details>
<details>
<summary>范例</summary>

**将“abcdefg”写入D:\\1.txt，统一换行字符为\r\n，如果文件已存在，则添加到文件末尾**
```json
{
  "Variables": [],
  "Steps": [
    {
      "StepRunnerKey": "sys:WriteTextFile",
      "InputParams": {
        "content": {
          "VarKey": null,
          "Value": "abcdefg"
        },
        "filePath": {
          "VarKey": null,
          "Value": "D:\\1.txt"
        },
        "encoding": {
          "VarKey": null,
          "Value": "utf-8"
        },
        "addUtf8Bom": {
          "VarKey": null,
          "Value": "0"
        },
        "appendMode": {
          "VarKey": null,
          "Value": "1"
        },
        "addNewLine": {
          "VarKey": null,
          "Value": "0"
        },
        "newLineChars": {
          "VarKey": null,
          "Value": "\r\n"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 67.Zip压缩打包

**功能描述**
> Zip压缩或解压缩

**官方文档**
> https://getquicker.net/KC/Help/Doc/zip

**内部名称**
> sys:zip

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| type | 操作类型 |  | (9)选项-Enum（Zip: 创建Zip文件; Unzip: 解压缩Zip文件） | Zip | False |
| sourcePath | 源路径 | 待压缩的文件夹或文件路径。多个文件时每个文件一行。 | (0)字符串-Text |  | True |
| targetZipFile | Zip文件路径 | 压缩时：目标文件的路径。留空时自动生成临时文件。点(.)表示待压缩的文件夹或文件所在位置。 | (0)字符串-Text |  | True |
| sourceZipFile | Zip文件路径 | 待解压的文件路径。 | (0)字符串-Text |  | True |
| keepBaseFolder | 源路径为单个文件夹时，压缩整个文件夹（保留文件夹名称） |  | (2)布尔值-Boolean | False | False |
| outputPath | 目标路径 | 解压缩的目标路径, 点(.)表示zip文件所在的文件夹, 星(*)表示以zip文件名创建的子文件夹。 | (0)字符串-Text |  | True |
| password | 密码 | 压缩文件密码 | (0)字符串-Text |  | False |
| comment | 备注 | 压缩文件注释内容 | (0)字符串-Text |  | False |
| level | 级别 | 压缩级别，0-9。0表示不压缩（速度快），9表示压缩到最小（速度慢） | (12)数字(整数)-Integer | 1 | False |
| overwrite | 自动覆盖文件 |  | (2)布尔值-Boolean | False | False |
| skipOverwriteError | 覆盖失败时忽略 | 忽略掉无法覆盖的情况 | (2)布尔值-Boolean | False | False |
| showProgress | 显示进度条 | 仅支持解压缩或压缩单个文件夹。 | (2)布尔值-Boolean | False | False |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| resultPath | 结果路径 | 生成的zip文件完整路径，或解压缩后的完整路径 | (0)字符串-Text |

</details>
<details>
<summary>范例</summary>

```json
{
  "Variables": [
    {
      "Key": "savedPath",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "解压成功",
      "Type": 2,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "resultPath",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:zip",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "Unzip"
        },
        "sourceZipFile": {
          "VarKey": "savedPath",
          "Value": null
        },
        "outputPath": {
          "VarKey": null,
          "Value": "."
        },
        "password": {
          "VarKey": null,
          "Value": ""
        },
        "overwrite": {
          "VarKey": null,
          "Value": "1"
        },
        "skipOverwriteError": {
          "VarKey": null,
          "Value": "0"
        },
        "showProgress": {
          "VarKey": null,
          "Value": "1"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {
        "isSuccess": "解压成功",
        "resultPath": "resultPath",
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 68.屏幕截图

**功能描述**
> 截取屏幕区域

**官方文档**
> https://getquicker.net/KC/Help/Doc/screencapture

**内部名称**
> sys:screenCapture

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| type | 截图类型 | 截取图片的屏幕区域类型 | (9)选项-Enum（select: 选择区域; full_screen: 所有屏幕; primary_screen: 主屏幕; fixed_area: 固定区域; window: 窗口 (屏幕可见内容); windowBackground: 窗口 (支持后台显示)） | select | False |
| area | 截图区域 | 要截取的屏幕坐标位置（像素值），格式为：left,top,right,bottom。默认不包含右边和底边像素。 | (0)字符串-Text |  | False |
| windowHandle | 窗口句柄 | 要截取的窗口句柄数字。0或留空表示截取前台窗口。 | (12)数字(整数)-Integer | 0 | False |
| delay | 截图前延迟时间 | 等待多少毫秒后开始截图 | (12)数字(整数)-Integer | 0 | True |
| preSelectArea | 预选截图区域 | 非必要请勿设置。预先选择的截图区域，格式为：left,top,right,bottom。默认不包含右边和底边像素。 | (0)字符串-Text |  | False |
| includeRightBottomBorder | 预选截图区域包含右边和底边像素 | 包含时，当指定 0,0,2,2 的时候，截图的大小为3*3, 否则为2*2 | (2)布尔值-Boolean | True | False |
| toClip | 写入剪贴板 | 截屏图片是否写入到剪贴板中 | (2)布尔值-Boolean | False | False |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| img | 图片 | 截图的图片 | (3)图片-Image |
| rect | 截图区域 | 图片的截取区域(left,top,right,bottom)。 | (0)字符串-Text |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |

</details>
<details>
<summary>范例</summary>

**等待30毫秒后截图屏幕上200,300,500,800的区域存入变量img和剪贴板，并将所截图区域坐标存入rect变量**
```json
{
  "Variables": [
    {
      "Key": "rect",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "img",
      "Type": 3,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:screenCapture",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "fixed_area"
        },
        "area": {
          "VarKey": null,
          "Value": "200,300,500,800"
        },
        "delay": {
          "VarKey": null,
          "Value": "30"
        },
        "toClip": {
          "VarKey": null,
          "Value": "1"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        },
        "includeRightBottomBorder": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "img": "img",
        "rect": "rect",
        "isSuccess": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 69.生成二维码

**功能描述**
> 将文本转换为二维码

**官方文档**
> https://getquicker.net/KC/Help/Doc/createqrcode

**内部名称**
> sys:createQrCode

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| code | 文本 | 要转换为二维码的内容 | (0)字符串-Text |  | True |
| pixelsPerModule | 每模块像素数 |  | (12)数字(整数)-Integer | 4 | False |
| darkColor | 暗色 | #AARRGGBB格式的颜色值 | (0)字符串-Text | #FF000000 | False |
| lightColor | 亮色 | #AARRGGBB格式的颜色值 | (0)字符串-Text | #FFFFFFFF | False |
| icon | 图标 | 图片变量或图标文件路径 | (3)图片-Image |  | False |
| iconPercent | 图标占比 | 百分比数字（只填数字，不写百分号） | (12)数字(整数)-Integer | 15 | False |
| iconBorderWidth | 图标边框宽度 | 最小为1 | (12)数字(整数)-Integer | 6 | False |
| drawQuietZones | 绘制外框 |  | (2)布尔值-Boolean | 1 | False |
| saveToPdfPath | 输出pdf文件 |  | (0)字符串-Text |  | False |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| img | 二维码图片 | 生成的二维码图片对象 | (3)图片-Image |
| svg | SVG格式结果 | Svg格式结果代码 | (0)字符串-Text |
| ascii | Ascii格式结果 | Ascii字符格式结果代码 | (0)字符串-Text |

</details>
<details>
<summary>范例</summary>

**将文本abcd转为二维码图片img**
```json
{
  "Variables": [
    {
      "Key": "img",
      "Type": 3,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:createQrCode",
      "InputParams": {
        "code": {
          "VarKey": null,
          "Value": "abcd"
        },
        "pixelsPerModule": {
          "VarKey": null,
          "Value": "4"
        },
        "darkColor": {
          "VarKey": null,
          "Value": "#FF000000"
        },
        "lightColor": {
          "VarKey": null,
          "Value": "#FFFFFFFF"
        },
        "icon": {
          "VarKey": null,
          "Value": ""
        },
        "iconPercent": {
          "VarKey": null,
          "Value": "15"
        },
        "iconBorderWidth": {
          "VarKey": null,
          "Value": "6"
        },
        "drawQuietZones": {
          "VarKey": null,
          "Value": "1"
        },
        "saveToPdfPath": {
          "VarKey": null,
          "Value": ""
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "img": "img",
        "svg": null,
        "ascii": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 70.手写板

**功能描述**
> 手写内容，生成图片对象。

**官方文档**
> https://getquicker.net/KC/Help/Doc/whiteboard

**内部名称**
> sys:whiteboard

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| winPosition | 窗口位置 | 可选。指定显示位置，格式为：left,top,right,bottom。支持像素数值或屏幕宽高百分比。 | (0)字符串-Text | 15%,30%,85%,70% | False |
| bgColor | 绘图区背景颜色 | 绘图窗口的背景颜色。格式为#AARRGGBB | (0)字符串-Text | #FFFFFFFF | False |
| penColor | 画笔颜色 | 画笔颜色。格式为#AARRGGBB | (0)字符串-Text | #FFFF0000 | False |
| enableTransparent | 使用透明无边框窗口 | 不显示窗口标题栏，绘图区透明，可以看到底层窗口内容。 | (2)布尔值-Boolean | False | False |
| imageWithBackground | 图片包含背景内容 | 使用透明窗口时，结果图片是否包含背景内容。 | (2)布尔值-Boolean | False | False |
| stopIfFail | 取消后停止动作 |  | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| result | 结果图片 |  | (3)图片-Image |

</details>
<details>
<summary>范例</summary>

```json
{
  "Variables": [
    {
      "Key": "img",
      "Type": 3,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "rect",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "isSuccess",
      "Type": 2,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:whiteboard",
      "InputParams": {
        "winPosition": {
          "VarKey": "rect",
          "Value": null
        },
        "bgColor": {
          "VarKey": null,
          "Value": "#0F5B89F5"
        },
        "penColor": {
          "VarKey": null,
          "Value": "#FFFF0000"
        },
        "enableTransparent": {
          "VarKey": null,
          "Value": "1"
        },
        "imageWithBackground": {
          "VarKey": null,
          "Value": "1"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {
        "isSuccess": "isSuccess",
        "result": "img",
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 71.读取图片信息

**功能描述**
> 获取图片的尺寸或exif信息

**官方文档**
> https://getquicker.net/KC/Help/Doc/imageinfo

**内部名称**
> sys:imageinfo

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| sourceType | 图片来源 |  | (9)选项-Enum（var: 图片变量; file: 图片文件） | var | False |
| bmpFile | 文件路径 | 图片文件的完整路径 | (0)字符串-Text |  | True |
| bmpVar | 图片变量 |  | (3)图片-Image |  | True |
| autoRotate | 计算旋转后的宽高 | 如果Exif中包含旋转角度信息，则获取旋转后的宽高 | (2)布尔值-Boolean | False | False |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| width | 宽度 |  | (12)数字(整数)-Integer |
| height | 高度 |  | (12)数字(整数)-Integer |
| rotateDegree | 旋转角度 |  | (12)数字(整数)-Integer |
| dateTimeOriginal | 拍摄时间 |  | (6)时间日期-DateTime |
| exifData | Exif数据 | 转换为文本格式的exif数据（词典格式，请参考模块文档） | (10)词典-Dict |
| rawExifData | 原始属性数据 | 原始Exif数据(词典格式，请参考模块文档) | (10)词典-Dict |
| fileTypeFromData | 内容图片格式 | 根据文件内容判断的文件格式（可能不准确），用于在无法根据扩展名得到图片格式的情况下使用。 | (0)字符串-Text |

</details>
<details>
<summary>范例</summary>

```json
{
  "Variables": [
    {
      "Key": "width",
      "Type": 12,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "height",
      "Type": 12,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:imageinfo",
      "InputParams": {
        "sourceType": {
          "VarKey": null,
          "Value": "file"
        },
        "bmpFile": {
          "VarKey": null,
          "Value": "D:\\1.png"
        },
        "autoRotate": {
          "VarKey": null,
          "Value": "1"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "width": "width",
        "height": "height",
        "rotateDegree": null,
        "dateTimeOriginal": null,
        "exifData": null,
        "rawExifData": null,
        "fileTypeFromData": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 72.图片处理

**功能描述**
> 图片处理和变换

**官方文档**
> https://getquicker.net/KC/Help/Doc/imgprocess

**内部名称**
> sys:imgProcess

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| img | 图片 | 要转换的图片 | (3)图片-Image |  | True |
| type | 操作类型 | 对图片的转换操作类型 | (9)选项-Enum（resize_percent: 缩放图片(指定比例); resize_pixel: 缩小图片(指定像素); Clone: 复制图片; Invert: 反色; GrayScale: 灰度; Rotate: 旋转; Filters: 组合处理; GenerateIco: 生成图标文件(.ico)） | resize_percent | False |
| resizePercent | 缩放比例 | 缩小或放大到原来的百分之多少 | (1)数字(小数)-Number | 50 | False |
| maxWidth | 最大宽度 | 最大宽度(像素数)，0表示自动 | (12)数字(整数)-Integer | 0 | False |
| maxHeight | 最大高度 | 最大高度(像素数)，0表示自动 | (12)数字(整数)-Integer | 0 | False |
| rotation | 旋转方式 | 顺时针角度。0:不旋转, 1:90°, 2:180°, 3:270°, 其他值请参考模块文档。 | (12)数字(整数)-Integer | 0 | False |
| filterParams | 处理参数 | 每行设定一个处理步骤，具体设置请参考文档 | (0)字符串-Text |  | False |
| iconFilePath | 图标文件保存路径 | 保存图标文件(.ico)的完整路径 | (0)字符串-Text |  | True |
| iconSize | 图标大小 | 图标中的位图大小，单位为像素。多尺寸图标可用英文逗号风格 | (0)字符串-Text | 256,48,32,16 | True |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| result | 结果图片 | 处理后的图片 | (3)图片-Image |

</details>
<details>
<summary>范例</summary>

**列表文件亮度增加30%，对比对比度增加30%，注释掉的行（用于生成灰度图像），自动旋转，高于指定亮度的像素修改为白色**
```json
{
  "Variables": [
    {
      "Key": "path",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "fileList",
      "Type": 4,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "prefix",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "processed_",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "savePath",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:getSelectedFiles",
      "InputParams": {
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "files": "fileList",
        "firstFile": "path",
        "isSuccess": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:each",
      "InputParams": {
        "input": {
          "VarKey": "fileList",
          "Value": null
        },
        "useMultiThread": {
          "VarKey": null,
          "Value": "0"
        },
        "threadDelay": {
          "VarKey": null,
          "Value": "5"
        }
      },
      "OutputParams": {
        "item": "path",
        "count": null
      },
      "IfSteps": [
        {
          "StepRunnerKey": "sys:assign",
          "InputParams": {
            "input": {
              "VarKey": null,
              "Value": "$= Path.Combine(Path.GetDirectoryName({path}), {prefix}+Path.GetFileName({path}))"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "isSuccess": null,
            "output": "savePath"
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:imgProcess",
          "InputParams": {
            "img": {
              "VarKey": null,
              "Value": ""
            },
            "type": {
              "VarKey": null,
              "Value": "Filters"
            },
            "filterParams": {
              "VarKey": null,
              "Value": "$$\r\nLoad:{path}\r\nBrightness:30\r\nContrast:30\r\nAutoRotate:\r\nWhiteThreshold:220\r\nSave:{savePath}"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "isSuccess": null,
            "result": null,
            "errMessage": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 73.识别二维码

**功能描述**
> 识别图片中的二维码

**官方文档**
> https://getquicker.net/KC/Help/Doc/readqrcode

**内部名称**
> sys:readQrCode

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| img | 输入图片 | 要识别二维码的图片 | (3)图片-Image |  | True |
| tryNetwork | 本地识别失败后尝试在线识别服务 | 在线服务拥有更强识别能力（频率限制2秒/次，仅专业版提供）。 | (2)布尔值-Boolean | False | False |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| code | 值 | 识别出的二维码内容 | (0)字符串-Text |
| codeList | 全部二维码值 | 当一个图片含有多个二维码，且需要返回所有结果时使用。 | (4)文本列表-List |

</details>

***

## 74.显示图片

**功能描述**
> 在屏幕上显示图片。输入文件路径/url或图片变量。

**官方文档**
> https://getquicker.net/KC/Help/Doc/showImage

**内部名称**
> sys:showImage

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| source | 操作/来源 | 图片来源类型 | (9)选项-Enum（file: 显示：图片文件或网络图片; var: 显示：变量中的图片; clipboard: 显示：剪贴板图片; closeWindow: 关闭图片窗口; getState: 获取图片窗口信息; getImageWindows: 获取所有图片窗口标识） | var | False |
| path | 路径/网址 | 图片文件的路径或网址。 | (0)字符串-Text |  | True |
| imgVar | 图片变量 | 从指定变量中加载图片 | (3)图片-Image |  | True |
| scale | 初始缩放比例 | 可以为小数，1表示原始大小，-1表示对大图自动调整缩放比例 | (1)数字(小数)-Number | 1 | True |
| opacity | 不透明度 | 0-1之间的小数，1为完全不透明，0为完全透明。 | (1)数字(小数)-Number | 1 | True |
| autoCloseKey | 唯一性标识 | (仅必要时使用)自动关闭之前打开的具有此标识的图片窗口。 | (0)字符串-Text |  | False |
| autoCloseTime | 自动关闭时间 | 几秒后自动关闭，可以为小数。0：不自动关闭。 | (1)数字(小数)-Number | 0 | True |
| winLocation | 显示位置 | 图片显示位置 | (9)选项-Enum | Auto | False |
| winPosition | 位置坐标 | 仅用于位置为“自定义位置”类型。格式为:left,top或left,top,right,bottom | (0)字符串-Text |  | False |
| waitClose | 等待图片关闭 | 是否等待图片关闭后再执行后续步骤 | (2)布尔值-Boolean | False | False |
| showDropShadow | 显示阴影 | 是否显示边框阴影 | (2)布尔值-Boolean | True | False |
| showTaskbarIcon | 显示任务栏图标 | 是否显示任务栏图标 | (2)布尔值-Boolean | True | False |
| topMost | 是否置顶显示 | 是否置顶显示图片 | (2)布尔值-Boolean | True | False |
| noActivate | 不激活窗口 | 图片窗口显示时不抢占焦点（无法通过Esc关闭） | (2)布尔值-Boolean | False | False |
| closeWhenLostFocus | 丢失焦点时自动关闭 |  | (2)布尔值-Boolean | False | False |
| tooltip | ToolTip提示文字 |  | (0)字符串-Text |  | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isExists | 是否存在 | 是否存在指定标识的窗口 | (2)布尔值-Boolean |
| hwnd | 窗口句柄 | 新创建的图片窗口的句柄 | (12)数字(整数)-Integer |
| finalPosition | 最终贴图位置 | 移动窗口后的贴图位置格式为left,top,right,bottom。显示图片（开启“等待图片关闭” 选项）或获取当前打开的图片窗口信息时有效。 | (0)字符串-Text |
| windowIdList | 窗口标识列表 |  | (4)文本列表-List |

</details>
<details>
<summary>范例</summary>

**显示剪贴板图片，并在按下W后关闭图片显示**
```json
{
  "Variables": [],
  "Steps": [
    {
      "StepRunnerKey": "sys:showImage",
      "InputParams": {
        "source": {
          "VarKey": null,
          "Value": "clipboard"
        },
        "scale": {
          "VarKey": null,
          "Value": "-1"
        },
        "opacity": {
          "VarKey": null,
          "Value": "0.7"
        },
        "autoCloseKey": {
          "VarKey": null,
          "Value": "abc"
        },
        "autoCloseTime": {
          "VarKey": null,
          "Value": "0"
        },
        "winLocation": {
          "VarKey": null,
          "Value": "CenterScreen"
        },
        "winPosition": {
          "VarKey": null,
          "Value": ""
        },
        "waitClose": {
          "VarKey": null,
          "Value": "false"
        },
        "showDropShadow": {
          "VarKey": null,
          "Value": "true"
        },
        "showTaskbarIcon": {
          "VarKey": null,
          "Value": "true"
        },
        "topMost": {
          "VarKey": null,
          "Value": "true"
        },
        "noActivate": {
          "VarKey": null,
          "Value": "0"
        },
        "closeWhenLostFocus": {
          "VarKey": null,
          "Value": "0"
        },
        "tooltip": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {
        "hwnd": null,
        "finalPosition": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:waitKeyboard",
      "InputParams": {
        "operation": {
          "VarKey": null,
          "Value": "waitKeyDown"
        },
        "waitingKeys": {
          "VarKey": null,
          "Value": "W"
        },
        "modifierKeys": {
          "VarKey": null,
          "Value": ""
        },
        "maxWaitSeconds": {
          "VarKey": null,
          "Value": "0"
        },
        "filterEvent": {
          "VarKey": null,
          "Value": "1"
        },
        "waitKeyUp": {
          "VarKey": null,
          "Value": "0"
        },
        "ignoreSimulated": {
          "VarKey": null,
          "Value": "0"
        },
        "help": {
          "VarKey": null,
          "Value": "请按键..."
        },
        "winLocation": {
          "VarKey": null,
          "Value": "TopCenter"
        },
        "mouseThrough": {
          "VarKey": null,
          "Value": "1"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        },
        "fontfamily": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "keyCode": null,
        "keyValue": null,
        "holdTimeMs": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:showImage",
      "InputParams": {
        "source": {
          "VarKey": null,
          "Value": "closeWindow"
        },
        "autoCloseKey": {
          "VarKey": null,
          "Value": "abc"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 75.临时图床

**功能描述**
> 将图片上传到临时（1分钟后删除）的图床，用以搜图等场景。勿上传非法内容。

**官方文档**
> https://getquicker.net/KC/Help/Doc/tempImgBed

**内部名称**
> sys:tempImgBed

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| imgVar | 图片变量 | 指定要上传的图片变量。 | (3)图片-Image |  | False |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| url | 网址 | 图片的临时网址 | (0)字符串-Text |

</details>
<details>
<summary>范例</summary>

```json
{
  "Variables": [
    {
      "Key": "imgVar",
      "Type": 3,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "url",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:tempImgBed",
      "InputParams": {
        "imgVar": {
          "VarKey": "imgVar",
          "Value": null
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "url": "url",
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 76.图片/Base64 转换

**功能描述**
> 图片和Base64转换

**官方文档**
> https://getquicker.net/KC/Help/Doc/imgtobase64

**内部名称**
> sys:imgToBase64

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| type | 操作类型 | 转换操作类型 | (9)选项-Enum（imgToBase64: 图片或文件转Base64文本; base64ToImg: Base64文本转图片） | imgToBase64 | False |
| img | 图片 | 要转换的图片（图片变量或文件路径） | (3)图片-Image |  | True |
| addHeader | 添加data头 | 是否添加“data:image/png;base64,”头 | (2)布尔值-Boolean | False | False |
| base64 | Base64编码 | 要转换的编码文本 | (0)字符串-Text |  | True |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| code | Base64编码 | Base64编码结果 | (0)字符串-Text |
| img | 图片 | 转换输出的图片 | (3)图片-Image |

</details>
<details>
<summary>范例</summary>

```json
{
  "Variables": [
    {
      "Key": "imgVar",
      "Type": 3,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "code",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:imgToBase64",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "imgToBase64"
        },
        "img": {
          "VarKey": "imgVar",
          "Value": null
        },
        "addHeader": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {
        "code": "code"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:imgToBase64",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "base64ToImg"
        },
        "base64": {
          "VarKey": "code",
          "Value": null
        }
      },
      "OutputParams": {
        "img": "imgVar"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 77.写入图片文件

**功能描述**
> 将图片内容写入文件

**官方文档**
> https://getquicker.net/KC/Help/Doc/writeimagefile

**内部名称**
> sys:WriteImageFile

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| content | 内容图片 | 要写入文件的图片（变量） | (3)图片-Image |  | True |
| filePath | 文件路径 | 要写入的文件完整路径（包含文件名） | (0)字符串-Text |  | True |
| quality | 图片质量 | 保存为JPG格式时的图片质量参数。范围10-100。 | (0)字符串-Text | 95 | True |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |

</details>
<details>
<summary>范例</summary>

```json
{
  "Variables": [
    {
      "Key": "img",
      "Type": 3,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:WriteImageFile",
      "InputParams": {
        "content": {
          "VarKey": "img",
          "Value": null
        },
        "filePath": {
          "VarKey": null,
          "Value": "D:\\1.jpg"
        },
        "quality": {
          "VarKey": null,
          "Value": "95"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 78.列表操作

**功能描述**
> 对列表变量进行添加、删除等操作

**官方文档**
> https://getquicker.net/KC/Help/Doc/listoperations

**内部名称**
> sys:listOperations

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| list | 列表 | 要操作的列表变量 | (4)文本列表-List |  | False |
| type | 操作类型 |  | (9)选项-Enum（none: 无操作（仅用于获取列表信息）; getAt: 读取某位置元素; append: 添加元素到末尾; insertAt: 插入元素; setAt: 设置/更新某序号元素; remove: 去除元素(指定值，有多个时去除第一个); removeAllByValue: 去除元素(指定值，有多个时去除全部); removeAt: 去除元素(指定位置); removeByMatch: 去除元素(匹配正则表达式的项); removeByNotMatch: 去除元素(不匹配正则表达式的项); clear: 清空列表; sortAsc: 排序A-Z（输出到结果）; sortDesc: 排序Z-A（输出到结果）; sortAscNature: 自然排序A-Z（输出到结果）; FileSizeAsc: 排序文件列表：文件大小（从小到大）; FileSizeDesc: 排序文件列表：文件大小（从大到小）; CreationTimeDesc: 排序文件列表：创建时间（从新到旧）; CreationTimeAsc: 排序文件列表：创建时间（从旧到新）; LastAccessTimeDesc: 排序文件列表：最后访问时间（从晚到早）; LastAccessTimeAsc: 排序文件列表：最后访问时间（从早到晚）; LastWriteTimeDesc: 排序文件列表：最后写入时间（从晚到早）; LastWriteTimeAsc: 排序文件列表：最后写入时间（从早到晚）; reverse: 倒置; sub: 截取（输出到结果）; concat: 拼接（输出到结果）; distinct: 去除重复（输出到结果）; indexOf: 获取值的序号; filterByRegex: 筛选（正则,输出到结果）; filterByDefault: 筛选（模糊匹配,输出到结果）; filterByContains: 筛选（包含）; filterByStarts: 筛选（开始）; filterByEnds: 筛选（结束）） | none | False |
| list2 | 列表2 | 要拼接的列表 | (4)文本列表-List |  | False |
| pos | 序号 | 目标元素的序号，从0开始。负值表示从后向前的第几个。 | (12)数字(整数)-Integer | 0 | False |
| length | 长度 | 操作元素的数量 | (12)数字(整数)-Integer | 1 | False |
| item | 值 | 要插入或更新的值，或筛选关键词 | (0)字符串-Text |  | False |
| orderByScore | 按匹配程度排序 | 筛选结果按匹配程度倒序排列 | (2)布尔值-Boolean | False | False |
| pattern | 正则表达式 | 要匹配的正则表达式。 | (0)字符串-Text |  | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| value | 结果 | 操作后的输出（取的元素值、排序、切片或拼接后的列表等） | (99)任意类型-Any |
| isEmpty | 是否为空 | 空返回true，非空返回false | (2)布尔值-Boolean |
| length | 列表长度 | 列表包含的元素数量，截断或拼接后输出结果列表的长度 | (12)数字(整数)-Integer |
| index | 序号 | 值在列表里的序号，-1表示不存在 | (12)数字(整数)-Integer |
| filterOutItems | 剩余项列表 | 不符合筛选条件的项的列表 | (99)任意类型-Any |

</details>
<details>
<summary>范例</summary>

**显示结果为：小明,19,跑步\r\n小红,18,走路**
```json
{
  "Variables": [
    {
      "Key": "选中的姓名们",
      "Type": 4,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "姓名们",
      "Type": 4,
      "Desc": "",
      "DefaultValue": "小红\r\n小明\r\n小西",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "年龄们",
      "Type": 4,
      "Desc": "",
      "DefaultValue": "18\r\n19\r\n20",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "爱好们",
      "Type": 4,
      "Desc": "",
      "DefaultValue": "走路\r\n跑步\r\n飞行",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "姓名",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "年龄",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "爱好",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "i",
      "Type": 12,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "结果",
      "Type": 4,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:assign",
      "InputParams": {
        "input": {
          "VarKey": null,
          "Value": "小明\r\n小红"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "output": "选中的姓名们",
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:each",
      "InputParams": {
        "input": {
          "VarKey": "选中的姓名们",
          "Value": null
        },
        "useMultiThread": {
          "VarKey": null,
          "Value": "0"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "item": "姓名",
        "count": null,
        "isSuccess": null,
        "errMessage": null
      },
      "IfSteps": [
        {
          "StepRunnerKey": "sys:listOperations",
          "InputParams": {
            "list": {
              "VarKey": "姓名们",
              "Value": null
            },
            "type": {
              "VarKey": null,
              "Value": "indexOf"
            },
            "item": {
              "VarKey": "姓名",
              "Value": null
            }
          },
          "OutputParams": {
            "isEmpty": null,
            "length": null,
            "index": "i"
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:listOperations",
          "InputParams": {
            "list": {
              "VarKey": "年龄们",
              "Value": null
            },
            "type": {
              "VarKey": null,
              "Value": "getAt"
            },
            "pos": {
              "VarKey": "i",
              "Value": null
            }
          },
          "OutputParams": {
            "value": "年龄",
            "isEmpty": null,
            "length": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:listOperations",
          "InputParams": {
            "list": {
              "VarKey": "爱好们",
              "Value": null
            },
            "type": {
              "VarKey": null,
              "Value": "getAt"
            },
            "pos": {
              "VarKey": "i",
              "Value": null
            }
          },
          "OutputParams": {
            "value": "爱好",
            "isEmpty": null,
            "length": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:listOperations",
          "InputParams": {
            "list": {
              "VarKey": "结果",
              "Value": null
            },
            "type": {
              "VarKey": null,
              "Value": "append"
            },
            "item": {
              "VarKey": null,
              "Value": "$${姓名},{年龄},{爱好}"
            }
          },
          "OutputParams": {
            "isEmpty": null,
            "length": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "↓ 展示数据"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:showText",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "NO_WAIT"
        },
        "text": {
          "VarKey": "结果",
          "Value": null
        },
        "title": {
          "VarKey": null,
          "Value": "文本窗口"
        },
        "autoCloseKey": {
          "VarKey": null,
          "Value": "="
        },
        "topMost": {
          "VarKey": null,
          "Value": "false"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        },
        "operations": {
          "VarKey": null,
          "Value": ""
        },
        "winLocation": {
          "VarKey": null,
          "Value": "CenterScreen"
        },
        "winSize": {
          "VarKey": null,
          "Value": ""
        },
        "fontsize": {
          "VarKey": null,
          "Value": "14"
        },
        "fontfamily": {
          "VarKey": null,
          "Value": ""
        },
        "bgColor": {
          "VarKey": null,
          "Value": ""
        },
        "textColor": {
          "VarKey": null,
          "Value": ""
        },
        "highlight": {
          "VarKey": null,
          "Value": ""
        },
        "autoSaveToState": {
          "VarKey": null,
          "Value": ""
        },
        "enableEscClose": {
          "VarKey": null,
          "Value": "true"
        },
        "closeWhenLostFocus": {
          "VarKey": null,
          "Value": "false"
        },
        "showLineNum": {
          "VarKey": null,
          "Value": "true"
        },
        "autoWrap": {
          "VarKey": null,
          "Value": "true"
        },
        "showBuildInToolbar": {
          "VarKey": null,
          "Value": "true"
        },
        "copyWholeLine": {
          "VarKey": null,
          "Value": "false"
        },
        "caretPosition": {
          "VarKey": null,
          "Value": "0"
        },
        "advancedSettings": {
          "VarKey": null,
          "Value": ""
        },
        "updateIfExists": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "windowHandle": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 79.管理和排序列表

**功能描述**
> 对列表内容进行手工排序、添加、删除等操作

**官方文档**
> https://getquicker.net/KC/Help/Doc/managelist

**内部名称**
> sys:manageList

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| list | 列表 | 要操作的列表变量。直接选择对应变量，不要使用表达式。 | (4)文本列表-List |  | False |
| winTitle | 窗口标题 |  | (0)字符串-Text |  | False |
| note | 提示信息 |  | (0)字符串-Text |  | False |
| parseData | 解析菜单数据 | 解析 “[图标]标题(tooltip)|值” 格式的数据并显示图标。 | (2)布尔值-Boolean | False | False |
| seperator | 分隔符 | 解析菜单数据时，显示内容与值之间的分隔符，默认为竖线'|' | (0)字符串-Text | | | False |
| windowSize | 窗口宽度 | 可选，在需要自定义窗口宽度的情况下使用。最小值为200。 | (0)字符串-Text |  | False |
| allowAdd | 允许添加项 |  | (2)布尔值-Boolean | True | False |
| allowEdit | 允许编辑项 |  | (2)布尔值-Boolean | True | False |
| allowDelete | 允许删除项 |  | (2)布尔值-Boolean | True | False |
| stopIfFail | 取消后停止动作 |  | (2)布尔值-Boolean | False | False |
| help | 帮助按钮内容 | 点击弹出显示帮助内容，MarkDown格式 | (0)字符串-Text |  | False |
| titleDelegate | 显示内容提取表达式 | 可选，在不解析菜单数据时自定义每一项的显示内容。使用方式请参考模块文档。 | (0)字符串-Text |  | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否确认 | 是否点击了确认按钮 | (2)布尔值-Boolean |

</details>
<details>
<summary>范例</summary>

**将选中文本文件手动调整拼接顺序后进行合并**
```json
{
  "Variables": [
    {
      "Key": "选中文件",
      "Type": 4,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "每个文件路径",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "文本内容",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "路径",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "保存",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "确定",
      "Type": 2,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "文件数",
      "Type": 12,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:getSelectedFiles",
      "InputParams": {
        "operation": {
          "VarKey": null,
          "Value": "getSelection"
        },
        "waitMs": {
          "VarKey": null,
          "Value": "200"
        },
        "sortType": {
          "VarKey": null,
          "Value": "Origin"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "files": "选中文件",
        "firstFile": "路径",
        "fileNames": null,
        "firstFileName": null,
        "fileCount": "文件数",
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:if",
      "InputParams": {
        "condition": {
          "VarKey": null,
          "Value": "$= {文件数} <= 1"
        }
      },
      "OutputParams": {},
      "IfSteps": [
        {
          "StepRunnerKey": "sys:notify",
          "InputParams": {
            "type": {
              "VarKey": null,
              "Value": "Error"
            },
            "msg": {
              "VarKey": null,
              "Value": "文件数量错误"
            },
            "maxLines": {
              "VarKey": null,
              "Value": "0"
            },
            "style": {
              "VarKey": null,
              "Value": "Default"
            },
            "clickAction": {
              "VarKey": null,
              "Value": ""
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": [
        {
          "StepRunnerKey": "sys:manageList",
          "InputParams": {
            "list": {
              "VarKey": "选中文件",
              "Value": null
            },
            "winTitle": {
              "VarKey": null,
              "Value": "排序或删除"
            },
            "note": {
              "VarKey": null,
              "Value": ""
            },
            "parseData": {
              "VarKey": null,
              "Value": "0"
            },
            "seperator": {
              "VarKey": null,
              "Value": "|"
            },
            "windowSize": {
              "VarKey": null,
              "Value": ""
            },
            "allowAdd": {
              "VarKey": null,
              "Value": "0"
            },
            "allowEdit": {
              "VarKey": null,
              "Value": "0"
            },
            "allowDelete": {
              "VarKey": null,
              "Value": "1"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            },
            "help": {
              "VarKey": null,
              "Value": ""
            },
            "titleDelegate": {
              "VarKey": null,
              "Value": "Path.GetFileName(x);"
            }
          },
          "OutputParams": {
            "isSuccess": null,
            "errMessage": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "手动调整拼接顺序",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:pathExtraction",
          "InputParams": {
            "operation": {
              "VarKey": null,
              "Value": "getInfo"
            },
            "path": {
              "VarKey": "路径",
              "Value": null
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "isSuccess": null,
            "name": null,
            "nameNoExt": null,
            "ext": null,
            "path": "路径",
            "errMessage": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "提取路径",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:selectFile",
          "InputParams": {
            "type": {
              "VarKey": null,
              "Value": "saveFile"
            },
            "filter": {
              "VarKey": null,
              "Value": "文本文件|*.txt|所有文件|*.*"
            },
            "defaultExt": {
              "VarKey": null,
              "Value": ".txt"
            },
            "initDir": {
              "VarKey": "路径",
              "Value": null
            },
            "initFileName": {
              "VarKey": null,
              "Value": "拼接文本"
            },
            "title": {
              "VarKey": null,
              "Value": ""
            },
            "topMost": {
              "VarKey": null,
              "Value": "1"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "isSuccess": null,
            "path": "保存",
            "errMessage": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:WriteTextFile",
          "InputParams": {
            "content": {
              "VarKey": null,
              "Value": ""
            },
            "filePath": {
              "VarKey": "保存",
              "Value": null
            },
            "encoding": {
              "VarKey": null,
              "Value": "utf-8"
            },
            "addUtf8Bom": {
              "VarKey": null,
              "Value": "0"
            },
            "appendMode": {
              "VarKey": null,
              "Value": "0"
            },
            "addNewLine": {
              "VarKey": null,
              "Value": "0"
            },
            "newLineChars": {
              "VarKey": null,
              "Value": ""
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "isSuccess": null,
            "errMessage": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:each",
          "InputParams": {
            "input": {
              "VarKey": "选中文件",
              "Value": null
            },
            "useMultiThread": {
              "VarKey": null,
              "Value": "0"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "item": "每个文件路径",
            "count": null,
            "isSuccess": null,
            "errMessage": null
          },
          "IfSteps": [
            {
              "StepRunnerKey": "sys:readFile",
              "InputParams": {
                "path": {
                  "VarKey": "每个文件路径",
                  "Value": null
                },
                "type": {
                  "VarKey": null,
                  "Value": "text"
                },
                "encoding": {
                  "VarKey": null,
                  "Value": "auto"
                },
                "stopIfFail": {
                  "VarKey": null,
                  "Value": "1"
                }
              },
              "OutputParams": {
                "txt": "文本内容",
                "isSuccess": null,
                "errMessage": null
              },
              "IfSteps": null,
              "ElseSteps": null,
              "Note": "",
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            },
            {
              "StepRunnerKey": "sys:WriteTextFile",
              "InputParams": {
                "content": {
                  "VarKey": "文本内容",
                  "Value": null
                },
                "filePath": {
                  "VarKey": "保存",
                  "Value": null
                },
                "encoding": {
                  "VarKey": null,
                  "Value": "utf-8"
                },
                "addUtf8Bom": {
                  "VarKey": null,
                  "Value": "0"
                },
                "appendMode": {
                  "VarKey": null,
                  "Value": "1"
                },
                "addNewLine": {
                  "VarKey": null,
                  "Value": "1"
                },
                "newLineChars": {
                  "VarKey": null,
                  "Value": ""
                },
                "stopIfFail": {
                  "VarKey": null,
                  "Value": "1"
                }
              },
              "OutputParams": {
                "isSuccess": null,
                "errMessage": null
              },
              "IfSteps": null,
              "ElseSteps": null,
              "Note": "",
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            }
          ],
          "ElseSteps": null,
          "Note": "迭代文件列表",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:MsgBox",
          "InputParams": {
            "operation": {
              "VarKey": null,
              "Value": "default"
            },
            "message": {
              "VarKey": null,
              "Value": "是否删除文本中空行？"
            },
            "title": {
              "VarKey": null,
              "Value": "TXT拼接"
            },
            "icon": {
              "VarKey": null,
              "Value": "Question"
            },
            "buttons": {
              "VarKey": null,
              "Value": "OKCancel"
            },
            "restoreFocus": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "result": null,
            "okOrYes": "确定"
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:simpleIf",
          "InputParams": {
            "condition": {
              "VarKey": null,
              "Value": "$= {确定} == true"
            }
          },
          "OutputParams": {},
          "IfSteps": [
            {
              "StepRunnerKey": "sys:readFile",
              "InputParams": {
                "path": {
                  "VarKey": "保存",
                  "Value": null
                },
                "type": {
                  "VarKey": null,
                  "Value": "text"
                },
                "encoding": {
                  "VarKey": null,
                  "Value": "auto"
                },
                "stopIfFail": {
                  "VarKey": null,
                  "Value": "1"
                }
              },
              "OutputParams": {
                "txt": "文本内容",
                "isSuccess": null,
                "errMessage": null
              },
              "IfSteps": null,
              "ElseSteps": null,
              "Note": "",
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            },
            {
              "StepRunnerKey": "sys:strReplace",
              "InputParams": {
                "type": {
                  "VarKey": null,
                  "Value": "single"
                },
                "input": {
                  "VarKey": "文本内容",
                  "Value": null
                },
                "old": {
                  "VarKey": null,
                  "Value": "^\\r?\\n"
                },
                "new": {
                  "VarKey": null,
                  "Value": ""
                },
                "escapeOld": {
                  "VarKey": null,
                  "Value": "false"
                },
                "replaceEscapes": {
                  "VarKey": null,
                  "Value": "false"
                },
                "useRegex": {
                  "VarKey": null,
                  "Value": "true"
                },
                "ignoreCase": {
                  "VarKey": null,
                  "Value": "false"
                },
                "singleLine": {
                  "VarKey": null,
                  "Value": "false"
                },
                "multiLine": {
                  "VarKey": null,
                  "Value": "true"
                }
              },
              "OutputParams": {
                "output": "文本内容"
              },
              "IfSteps": null,
              "ElseSteps": null,
              "Note": "查找^\\n替换空",
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            },
            {
              "StepRunnerKey": "sys:WriteTextFile",
              "InputParams": {
                "content": {
                  "VarKey": "文本内容",
                  "Value": null
                },
                "filePath": {
                  "VarKey": "保存",
                  "Value": null
                },
                "encoding": {
                  "VarKey": null,
                  "Value": "utf-8"
                },
                "addUtf8Bom": {
                  "VarKey": null,
                  "Value": "0"
                },
                "appendMode": {
                  "VarKey": null,
                  "Value": "0"
                },
                "addNewLine": {
                  "VarKey": null,
                  "Value": "1"
                },
                "newLineChars": {
                  "VarKey": null,
                  "Value": ""
                },
                "stopIfFail": {
                  "VarKey": null,
                  "Value": "1"
                }
              },
              "OutputParams": {
                "isSuccess": null,
                "errMessage": null
              },
              "IfSteps": null,
              "ElseSteps": null,
              "Note": "",
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            }
          ],
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 80.赋值

**功能描述**
> 为变量赋值。使用频率最高的模块，支持文本字符串或插值格式或C#代码模式。
**官方文档**
> https://getquicker.net/KC/Help/Doc/assign

**内部名称**
> sys:assign

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| input | 输入 | 要赋值给变量的内容，可以直接是其他变量，也可以直接输入值或使用插值格式。 | (99)任意类型-Any |  | True |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| output | 输出 | 将数据写入到变量中 | (99)任意类型-Any |

</details>
<details>
<summary>范例</summary>

**num最终值会是“233”，text最终值将是“233.abc”**
```json
{
  "Variables": [
    {
      "Key": "list",
      "Type": 4,
      "Desc": "",
      "DefaultValue": "233\r\n123",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "num",
      "Type": 12,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "text",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:assign",
      "InputParams": {
        "input": {
          "VarKey": null,
          "Value": "$=int.Parse({list}[0])"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "output": "num",
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:assign",
      "InputParams": {
        "input": {
          "VarKey": null,
          "Value": "$${num}.abc"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "output": "text",
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 81.注释

**功能描述**
> 使用注释来描述后续步骤的目的。

**官方文档**
> https://getquicker.net/KC/Help/Doc/comment

**内部名称**
> sys:comment

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| note | 注释内容 | 注释内容 | (0)字符串-Text |  | False |

</details>
<details>
<summary>传出参数</summary>
无
</details>
<details>
<summary>范例</summary>

```json
{
  "Variables": [],
  "Steps": [
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "这是一行注释"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 82.计算

**功能描述**
> 对表达式进行计算。

**官方文档**
> https://getquicker.net/KC/Help/Doc/compute

**内部名称**
> sys:compute

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| expression | 表达式 | 要计算的表达式 | (0)字符串-Text | 1+1 | True |
| evalVar | 增强模式 | 支持在表达式中使用{变量名}和Math对象 | (2)布尔值-Boolean | False | False |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| output | 结果 | 将表达式计算结果写入变量 | (99)任意类型-Any |

</details>
<details>
<summary>范例</summary>

**简单范例**
```json
{
  "Variables": [
    {
      "Key": "result",
      "Type": 99,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "a",
      "Type": 12,
      "Desc": "",
      "DefaultValue": "5",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "b",
      "Type": 12,
      "Desc": "",
      "DefaultValue": "6",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "计算数学公式"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:compute",
      "InputParams": {
        "expression": {
          "VarKey": null,
          "Value": "1+1"
        },
        "evalVar": {
          "VarKey": null,
          "Value": "0"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "output": "result"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:notify",
      "InputParams": {
        "msg": {
          "VarKey": "result",
          "Value": null
        },
        "maxLines": {
          "VarKey": null,
          "Value": "0"
        },
        "type": {
          "VarKey": null,
          "Value": "Info"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "计算包含变量的表达式"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:compute",
      "InputParams": {
        "expression": {
          "VarKey": null,
          "Value": "{a} * {b} "
        },
        "evalVar": {
          "VarKey": null,
          "Value": "1"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "output": "result"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:notify",
      "InputParams": {
        "msg": {
          "VarKey": "result",
          "Value": null
        },
        "maxLines": {
          "VarKey": null,
          "Value": "0"
        },
        "type": {
          "VarKey": null,
          "Value": "Info"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "返回其他类型的值"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:compute",
      "InputParams": {
        "expression": {
          "VarKey": null,
          "Value": "{a} > {b} "
        },
        "evalVar": {
          "VarKey": null,
          "Value": "1"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "output": "result"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:notify",
      "InputParams": {
        "msg": {
          "VarKey": "result",
          "Value": null
        },
        "maxLines": {
          "VarKey": null,
          "Value": "0"
        },
        "type": {
          "VarKey": null,
          "Value": "Info"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "使用Math对象"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:compute",
      "InputParams": {
        "expression": {
          "VarKey": null,
          "Value": "Math.Pow({a},{b})"
        },
        "evalVar": {
          "VarKey": null,
          "Value": "1"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "output": "result"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:notify",
      "InputParams": {
        "msg": {
          "VarKey": "result",
          "Value": null
        },
        "maxLines": {
          "VarKey": null,
          "Value": "0"
        },
        "type": {
          "VarKey": null,
          "Value": "Info"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```

**对每行计算后，在后面显示结果**
```json
{
  "Variables": [
    {
      "Key": "context",
      "Type": 0,
      "Desc": "默认的文本变量",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": null,
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "lines",
      "Type": 4,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": null,
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "result",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": null,
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "lineResult",
      "Type": 0,
      "Desc": "每行的结果",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": null,
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "resultList",
      "Type": 4,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "isSuccess",
      "Type": 2,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:getSelectedText",
      "InputParams": {
        "format": {
          "VarKey": null,
          "Value": "UnicodeText"
        },
        "waitMs": {
          "VarKey": null,
          "Value": "250"
        },
        "repeat": {
          "VarKey": null,
          "Value": "0"
        },
        "trim": {
          "VarKey": null,
          "Value": "0"
        },
        "tryNoClipboard": {
          "VarKey": null,
          "Value": "0"
        },
        "useActionParam": {
          "VarKey": null,
          "Value": "0"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "output": "context",
        "outputEncoded": null,
        "url": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "拆分成列表。 支持3种换行。"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:assign",
      "InputParams": {
        "input": {
          "VarKey": null,
          "Value": "$={context}.SplitToList(\"\\r\\n\",\"\\n\",\"\\r\")"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "output": "lines",
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:each",
      "InputParams": {
        "input": {
          "VarKey": "lines",
          "Value": null
        },
        "useMultiThread": {
          "VarKey": null,
          "Value": "0"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "item": "context",
        "count": null,
        "isSuccess": null,
        "errMessage": null
      },
      "IfSteps": [
        {
          "StepRunnerKey": "sys:comment",
          "InputParams": {
            "note": {
              "VarKey": null,
              "Value": "如果行不为空，则计算"
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:if",
          "InputParams": {
            "condition": {
              "VarKey": null,
              "Value": "$= !String.IsNullOrWhiteSpace({context})"
            }
          },
          "OutputParams": {},
          "IfSteps": [
            {
              "StepRunnerKey": "sys:compute",
              "InputParams": {
                "expression": {
                  "VarKey": "context",
                  "Value": null
                },
                "evalVar": {
                  "VarKey": null,
                  "Value": "0"
                },
                "stopIfFail": {
                  "VarKey": null,
                  "Value": "0"
                }
              },
              "OutputParams": {
                "isSuccess": "isSuccess",
                "output": "lineResult",
                "errMessage": null
              },
              "IfSteps": null,
              "ElseSteps": null,
              "Note": "",
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            },
            {
              "StepRunnerKey": "sys:comment",
              "InputParams": {
                "note": {
                  "VarKey": null,
                  "Value": "如果计算成功，则输出结果，否则原样输出"
                }
              },
              "OutputParams": {},
              "IfSteps": null,
              "ElseSteps": null,
              "Note": "",
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            },
            {
              "StepRunnerKey": "sys:if",
              "InputParams": {
                "condition": {
                  "VarKey": "isSuccess",
                  "Value": null
                }
              },
              "OutputParams": {},
              "IfSteps": [
                {
                  "StepRunnerKey": "sys:listOperations",
                  "InputParams": {
                    "list": {
                      "VarKey": "resultList",
                      "Value": null
                    },
                    "type": {
                      "VarKey": null,
                      "Value": "append"
                    },
                    "item": {
                      "VarKey": null,
                      "Value": "$${context} = {lineResult}"
                    }
                  },
                  "OutputParams": {
                    "isEmpty": null,
                    "length": null
                  },
                  "IfSteps": null,
                  "ElseSteps": null,
                  "Note": "",
                  "Disabled": false,
                  "Collapsed": false,
                  "DelayMs": 0
                }
              ],
              "ElseSteps": [
                {
                  "StepRunnerKey": "sys:listOperations",
                  "InputParams": {
                    "list": {
                      "VarKey": "resultList",
                      "Value": null
                    },
                    "type": {
                      "VarKey": null,
                      "Value": "append"
                    },
                    "item": {
                      "VarKey": null,
                      "Value": "$${context}"
                    }
                  },
                  "OutputParams": {
                    "isEmpty": null,
                    "length": null
                  },
                  "IfSteps": null,
                  "ElseSteps": null,
                  "Note": "",
                  "Disabled": false,
                  "Collapsed": false,
                  "DelayMs": 0
                }
              ],
              "Note": "",
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            }
          ],
          "ElseSteps": [
            {
              "StepRunnerKey": "sys:comment",
              "InputParams": {
                "note": {
                  "VarKey": null,
                  "Value": "空的情况，输出空行"
                }
              },
              "OutputParams": {},
              "IfSteps": null,
              "ElseSteps": null,
              "Note": "",
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            },
            {
              "StepRunnerKey": "sys:listOperations",
              "InputParams": {
                "list": {
                  "VarKey": "resultList",
                  "Value": null
                },
                "type": {
                  "VarKey": null,
                  "Value": "append"
                },
                "item": {
                  "VarKey": null,
                  "Value": "$${context}"
                }
              },
              "OutputParams": {
                "isEmpty": null,
                "length": null
              },
              "IfSteps": null,
              "ElseSteps": null,
              "Note": "",
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            }
          ],
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:formatString",
          "InputParams": {
            "formatString": {
              "VarKey": null,
              "Value": "$${result}\r\n{context} = {lineResult}"
            },
            "p0": {
              "VarKey": null,
              "Value": ""
            },
            "p1": {
              "VarKey": null,
              "Value": ""
            },
            "p2": {
              "VarKey": null,
              "Value": ""
            },
            "p3": {
              "VarKey": null,
              "Value": ""
            },
            "p4": {
              "VarKey": null,
              "Value": ""
            }
          },
          "OutputParams": {
            "output": "result"
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": null,
          "Disabled": true,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:outputText",
      "InputParams": {
        "content": {
          "VarKey": "resultList",
          "Value": null
        },
        "method": {
          "VarKey": null,
          "Value": "paste"
        },
        "delayBeforePaste": {
          "VarKey": null,
          "Value": "50"
        },
        "delayAfterPaste": {
          "VarKey": null,
          "Value": "10"
        },
        "appendReturn": {
          "VarKey": null,
          "Value": "0"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```

</details>

***

## 83.生成Guid

**功能描述**
> 生成一个新的Guid(全局唯一ID标示符)，并转换为文本格式。

**官方文档**
> https://getquicker.net/KC/Help/Doc/newguid

**内部名称**
> sys:newGuid

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| format | 格式 | 转换为文本时使用的格式 | (9)选项-Enum（D: 默认：00000000-0000-0000-0000-000000000000; N: 去除连字符：00000000000000000000000000000000; B: 大括号包围：{00000000-0000-0000-0000-000000000000}; P: 小括号包围：(00000000-0000-0000-0000-000000000000); X: 十六进制：{0x00000000,0x0000,0x0000,{0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00}}） | D | False |
| upper | 大写 | 字母输出为大写格式。 | (2)布尔值-Boolean | False | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| output | 内容 | 将获得的文本写入到变量 | (0)字符串-Text |

</details>


***

## 84.多字段表单

**功能描述**
> 使用表单窗口编辑多个变量的值。

**官方文档**
> https://getquicker.net/KC/Help/Doc/form

**内部名称**
> sys:form

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| operation | 工作模式 | 工作模式：编辑某个词典的值，或编辑一些变量的值 | (9)选项-Enum（variables: 编辑动作变量的值; dict: 编辑词典数据; dict_dynamic: 编辑词典数据（动态）） | variables | False |
| dictVar | 词典变量 | 表单需要编辑的词典变量 | (10)词典-Dict |  | False |
| title | 窗口标题 | 表单窗口标题文字 | (0)字符串-Text | 填写表单 | True |
| formDef | 表单定义 |  | (11)表单-Form |  | True |
| formForDictDef | 表单定义(词典) |  | (14)表单(词典)-FormForDict |  | True |
| dynamicFormForDictDef | 表单定义(词典) | JSON格式的表单定义数据。格式说明请参考模块文档。 | (0)字符串-Text |  | True |
| help | 提示文字 | 帮助用户填写表单的提示文字。 | (0)字符串-Text |  | False |
| markdownhelp | 帮助按钮内容 | 点击弹出显示帮助内容，MarkDown格式。 | (0)字符串-Text |  | False |
| titleColumnWidth | 标题列宽度 | 左侧字段标题区域的宽度(逻辑像素)。负值，如-200表示自适应列宽且最大宽度为200。 | (1)数字(小数)-Number | 100 | False |
| windowWidth | 窗口宽度 | 逻辑像素，最小400。 | (1)数字(小数)-Number | 500 | True |
| defaultInputWidth | 输入框默认宽度 | 逻辑像素，0表示自动宽度。 | (1)数字(小数)-Number | 0 | True |
| windowHeight | 窗口最大高度 | 逻辑像素，0表示默认。设置时请填写大于100的值。 | (1)数字(小数)-Number | 0 | True |
| restoreFocus | 恢复活动窗口 | 用户输入后，是否将焦点还原到之前的活动窗口 | (2)布尔值-Boolean | False | False |
| topMost | 置顶显示 |  | (2)布尔值-Boolean | False | False |
| confirm | 自定义“确定”按钮标题 | 仅在需要时填写。使用"_字符"的形式定义触发字符,如"_S"表示Alt+S可直接触发按钮 | (0)字符串-Text |  | False |
| customButtons | 自定义按钮 | 使用"标题|返回值"的形式定义按钮，多个按钮用换行分隔。 | (0)字符串-Text |  | False |
| selectedGroup | 选择的分组 | 使用分组标签页时，默认选择的分组。 | (0)字符串-Text |  | False |
| winLocation | 窗口位置类型 | 在哪里显示选择窗口 | (9)选项-Enum | CenterScreen | False |
| winSize | 位置 | 当 “窗口位置” 类型为 “自定义位置” 时用于指定显示位置，格式为：left,top,right,bottom | (0)字符串-Text |  | False |
| disableEnterSubmit | 关闭Enter提交表单功能 |  | (2)布尔值-Boolean | False | False |
| stopIfFail | 取消后停止 | 取消后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| button | 点击的按钮 | 默认的确认按钮返回值为空，自定义按钮返回值为自定义的值。 | (0)字符串-Text |
| selectedGroup | 选择的分组 | 关闭时所选择的标签页分组。 | (0)字符串-Text |

</details>
<details>
<summary>范例</summary>

**动态更新选择类型字段的可选值**
```json
{
  "Variables": [
    {
      "Key": "lastPath",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "item",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:form",
      "InputParams": {
        "operation": {
          "VarKey": null,
          "Value": "variables"
        },
        "title": {
          "VarKey": null,
          "Value": "填写表单"
        },
        "formDef": {
          "VarKey": null,
          "Value": "{\"Fields\":[{\"FieldKey\":\"item\",\"DictVarType\":null,\"Label\":\"item\",\"HelpText\":\"\",\"HelpLink\":null,\"InputMethod\":3,\"SelectionItems\":\"aaa\\r\\nbbb\\r\\nccc\",\"IsRequired\":false,\"MinValue\":\"\",\"MaxValue\":\"\",\"Pattern\":\"\",\"InputWidth\":\"\",\"MaxLength\":0,\"ImeState\":null,\"TextTools\":\"\",\"ExtraSettings\":\"\",\"VisibleExpression\":\"\",\"DefaultValue\":null,\"ColumnWidth\":0.0,\"OnlyDate\":false,\"ReadOnly\":false,\"Group\":\"\"},{\"FieldKey\":\"lastPath\",\"DictVarType\":null,\"Label\":\"lastPath\",\"HelpText\":\"\",\"HelpLink\":null,\"InputMethod\":3,\"SelectionItems\":\"$={item} + \\\"1\\\\r\\\\n\\\"\\r\\n+ {item} + \\\"2\\\\r\\\\n\\\"\\r\\n+ {item} + \\\"3\\\\r\\\\n\\\"\",\"IsRequired\":false,\"MinValue\":\"\",\"MaxValue\":\"\",\"Pattern\":\"\",\"InputWidth\":\"\",\"MaxLength\":0,\"ImeState\":null,\"TextTools\":\"\",\"ExtraSettings\":\"refresh_items\",\"VisibleExpression\":\"\",\"DefaultValue\":null,\"ColumnWidth\":0.0,\"OnlyDate\":false,\"ReadOnly\":false,\"Group\":\"\"}]}"
        },
        "help": {
          "VarKey": null,
          "Value": ""
        },
        "titleColumnWidth": {
          "VarKey": null,
          "Value": "100"
        },
        "windowWidth": {
          "VarKey": null,
          "Value": "500"
        },
        "windowHeight": {
          "VarKey": null,
          "Value": "0"
        },
        "restoreFocus": {
          "VarKey": null,
          "Value": "0"
        },
        "topMost": {
          "VarKey": null,
          "Value": "false"
        },
        "disableEnterSubmit": {
          "VarKey": null,
          "Value": "0"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        },
        "markdownhelp": {
          "VarKey": null,
          "Value": ""
        },
        "defaultInputWidth": {
          "VarKey": null,
          "Value": "0"
        },
        "confirm": {
          "VarKey": null,
          "Value": ""
        },
        "customButtons": {
          "VarKey": null,
          "Value": ""
        },
        "selectedGroup": {
          "VarKey": null,
          "Value": ""
        },
        "winLocation": {
          "VarKey": null,
          "Value": "CenterScreen"
        },
        "winSize": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "button": null,
        "selectedGroup": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```

**表单中对个别字段自动计算结果(注意：只能后面的字段依赖靠前的字段)**
```json
{
  "Variables": [
    {
      "Key": "x",
      "Type": 1,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "y",
      "Type": 1,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "z",
      "Type": 1,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "distance",
      "Type": 1,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "hwnd",
      "Type": 12,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "code",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "1",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "height",
      "Type": 12,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:form",
      "InputParams": {
        "operation": {
          "VarKey": null,
          "Value": "variables"
        },
        "title": {
          "VarKey": null,
          "Value": "矩形计算器"
        },
        "formDef": {
          "VarKey": null,
          "Value": "{\"Fields\":[{\"FieldKey\":\"x\",\"DictVarType\":null,\"Label\":\"x\",\"HelpText\":\"\",\"HelpLink\":null,\"InputMethod\":7,\"SelectionItems\":\"\",\"IsRequired\":false,\"MinValue\":\"\",\"MaxValue\":\"\",\"Pattern\":\"\",\"InputWidth\":\"\",\"MaxLength\":0,\"ImeState\":null,\"TextTools\":\"\",\"ExtraSettings\":\"\",\"VisibleExpression\":\"\",\"DefaultValue\":null,\"ColumnWidth\":0.0,\"OnlyDate\":false,\"ReadOnly\":false,\"Group\":\"\"},{\"FieldKey\":\"y\",\"DictVarType\":null,\"Label\":\"y\",\"HelpText\":\"\",\"HelpLink\":null,\"InputMethod\":7,\"SelectionItems\":\"\",\"IsRequired\":false,\"MinValue\":\"\",\"MaxValue\":\"\",\"Pattern\":\"\",\"InputWidth\":\"\",\"MaxLength\":0,\"ImeState\":null,\"TextTools\":\"\",\"ExtraSettings\":\"\",\"VisibleExpression\":\"\",\"DefaultValue\":null,\"ColumnWidth\":0.0,\"OnlyDate\":false,\"ReadOnly\":false,\"Group\":\"\"},{\"FieldKey\":\"z\",\"DictVarType\":null,\"Label\":\"面积\",\"HelpText\":\"\",\"HelpLink\":null,\"InputMethod\":41,\"SelectionItems\":\"\",\"IsRequired\":false,\"MinValue\":\"\",\"MaxValue\":\"\",\"Pattern\":\"\",\"InputWidth\":\"\",\"MaxLength\":0,\"ImeState\":null,\"TextTools\":\"\",\"ExtraSettings\":\"compute:$={x} * {y}\",\"VisibleExpression\":\"\",\"DefaultValue\":null,\"ColumnWidth\":0.0,\"OnlyDate\":false,\"ReadOnly\":false,\"Group\":\"\"},{\"FieldKey\":\"distance\",\"DictVarType\":null,\"Label\":\"斜边长\",\"HelpText\":\"\",\"HelpLink\":null,\"InputMethod\":1,\"SelectionItems\":\"\",\"IsRequired\":false,\"MinValue\":\"\",\"MaxValue\":\"\",\"Pattern\":\"\",\"InputWidth\":\"\",\"MaxLength\":0,\"ImeState\":null,\"TextTools\":\"\",\"ExtraSettings\":\"compute:$=Math.Sqrt({x} * {x} + {y} * {y})\",\"VisibleExpression\":\"\",\"DefaultValue\":null,\"ColumnWidth\":0.0,\"OnlyDate\":false,\"ReadOnly\":true,\"Group\":\"\"}]}"
        },
        "help": {
          "VarKey": null,
          "Value": ""
        },
        "titleColumnWidth": {
          "VarKey": null,
          "Value": "100"
        },
        "windowWidth": {
          "VarKey": null,
          "Value": "500"
        },
        "windowHeight": {
          "VarKey": null,
          "Value": "0"
        },
        "restoreFocus": {
          "VarKey": null,
          "Value": "0"
        },
        "topMost": {
          "VarKey": null,
          "Value": "false"
        },
        "disableEnterSubmit": {
          "VarKey": null,
          "Value": "0"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        },
        "markdownhelp": {
          "VarKey": null,
          "Value": ""
        },
        "defaultInputWidth": {
          "VarKey": null,
          "Value": "0"
        },
        "confirm": {
          "VarKey": null,
          "Value": ""
        },
        "customButtons": {
          "VarKey": null,
          "Value": ""
        },
        "selectedGroup": {
          "VarKey": null,
          "Value": ""
        },
        "winLocation": {
          "VarKey": null,
          "Value": "CenterScreen"
        },
        "winSize": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "button": null,
        "selectedGroup": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:form",
      "InputParams": {
        "operation": {
          "VarKey": null,
          "Value": "variables"
        },
        "title": {
          "VarKey": null,
          "Value": "使用depd避免意外更新"
        },
        "formDef": {
          "VarKey": null,
          "Value": "{\"Fields\":[{\"FieldKey\":\"code\",\"DictVarType\":null,\"Label\":\"页面尺寸\",\"HelpText\":\"\",\"HelpLink\":null,\"InputMethod\":3,\"SelectionItems\":\"1\\r\\n2\\r\\n3\\r\\n4\\r\\n5\\r\\n6\",\"IsRequired\":false,\"MinValue\":\"\",\"MaxValue\":\"\",\"Pattern\":\"\",\"InputWidth\":\"\",\"MaxLength\":0,\"ImeState\":null,\"TextTools\":\"\",\"ExtraSettings\":\"\",\"VisibleExpression\":\"\",\"DefaultValue\":null,\"ColumnWidth\":0.0,\"OnlyDate\":false,\"ReadOnly\":false,\"Group\":\"\"},{\"FieldKey\":\"height\",\"DictVarType\":null,\"Label\":\"水平边距\",\"HelpText\":\"\",\"HelpLink\":null,\"InputMethod\":7,\"SelectionItems\":\"\",\"IsRequired\":false,\"MinValue\":\"\",\"MaxValue\":\"\",\"Pattern\":\"\",\"InputWidth\":\"\",\"MaxLength\":0,\"ImeState\":null,\"TextTools\":\"\",\"ExtraSettings\":\"compute:Convert.ToInt32({code})*2\\r\\ndepd:code\",\"VisibleExpression\":\"\",\"DefaultValue\":null,\"ColumnWidth\":0.0,\"OnlyDate\":false,\"ReadOnly\":false,\"Group\":\"\"},{\"FieldKey\":\"hwnd\",\"DictVarType\":null,\"Label\":\"垂直边距\",\"HelpText\":\"\",\"HelpLink\":null,\"InputMethod\":7,\"SelectionItems\":\"\",\"IsRequired\":false,\"MinValue\":\"\",\"MaxValue\":\"\",\"Pattern\":\"\",\"InputWidth\":\"\",\"MaxLength\":0,\"ImeState\":null,\"TextTools\":\"\",\"ExtraSettings\":\"compute:Convert.ToInt32({code})*3\\r\\ndepd:code\",\"VisibleExpression\":\"\",\"DefaultValue\":null,\"ColumnWidth\":0.0,\"OnlyDate\":false,\"ReadOnly\":false,\"Group\":\"\"}]}"
        },
        "help": {
          "VarKey": null,
          "Value": "选择第一个选项后，下面两项可以自由修改。"
        },
        "titleColumnWidth": {
          "VarKey": null,
          "Value": "100"
        },
        "windowWidth": {
          "VarKey": null,
          "Value": "500"
        },
        "windowHeight": {
          "VarKey": null,
          "Value": "0"
        },
        "restoreFocus": {
          "VarKey": null,
          "Value": "0"
        },
        "topMost": {
          "VarKey": null,
          "Value": "false"
        },
        "disableEnterSubmit": {
          "VarKey": null,
          "Value": "0"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        },
        "markdownhelp": {
          "VarKey": null,
          "Value": ""
        },
        "defaultInputWidth": {
          "VarKey": null,
          "Value": "0"
        },
        "confirm": {
          "VarKey": null,
          "Value": ""
        },
        "customButtons": {
          "VarKey": null,
          "Value": ""
        },
        "selectedGroup": {
          "VarKey": null,
          "Value": ""
        },
        "winLocation": {
          "VarKey": null,
          "Value": "CenterScreen"
        },
        "winSize": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "button": null,
        "selectedGroup": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```

**通过Json数据或创建FormField对象列表生成表单**
```json
{
  "Variables": [
    {
      "Key": "userInfo",
      "Type": 10,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:dictOperations",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "setOriginValue"
        },
        "dict": {
          "VarKey": "userInfo",
          "Value": null
        },
        "key": {
          "VarKey": null,
          "Value": "age"
        },
        "value": {
          "VarKey": null,
          "Value": "29"
        },
        "ignoreCase": {
          "VarKey": null,
          "Value": "0"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {
        "isSuccess": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:form",
      "InputParams": {
        "operation": {
          "VarKey": null,
          "Value": "dict_dynamic"
        },
        "dictVar": {
          "VarKey": "userInfo",
          "Value": null
        },
        "title": {
          "VarKey": null,
          "Value": "填写表单"
        },
        "dynamicFormForDictDef": {
          "VarKey": null,
          "Value": "$=new List<Quicker.Public.Forms.FormField>{\r\n\tnew Quicker.Public.Forms.FormField(){\r\n\t\tFieldKey = \"name\",\r\n\t\tLabel  = \"姓名\",\r\n\t\tDictVarType = Quicker.Public.Actions.VarType.Text,\r\n\t\tInputMethod = Quicker.Public.Forms.InputMethod.TextBox,\r\n\t\tGroup = \"基本信息\",\r\n\t\tIsRequired = true\r\n\t},\r\n\tnew Quicker.Public.Forms.FormField(){\r\n\t\tFieldKey = \"age\",\r\n\t\tLabel  = \"年龄\",\r\n\t\tDictVarType = Quicker.Public.Actions.VarType.Integer,\r\n\t\tInputMethod = Quicker.Public.Forms.InputMethod.TextBox,\r\n\t\tGroup = \"基本信息\",\t\t\r\n\t\tIsRequired = true\r\n\t},\r\n\tnew Quicker.Public.Forms.FormField(){\r\n\t\tFieldKey = \"favor\",\r\n\t\tLabel  = \"爱好\",\r\n\t\tDictVarType = Quicker.Public.Actions.VarType.Text,\r\n\t\tInputMethod = Quicker.Public.Forms.InputMethod.DropDown,\r\n\t\tSelectionItems = \"足球\\r\\n篮球\\r\\n排球\\r\\n\",\r\n\t\tGroup = \"隐私信息\",\r\n\t\tIsRequired = true\r\n\t},\r\n\tnew Quicker.Public.Forms.FormField(){\r\n\t\tFieldKey = \"dyna\",\r\n\t\tLabel  = \"动态显示\",\r\n\t\tDictVarType = Quicker.Public.Actions.VarType.Text,\r\n\t\tInputMethod = Quicker.Public.Forms.InputMethod.TextBox,\r\n\t\tSelectionItems = \"\",\r\n\t\tGroup = \"隐私信息\",\r\n\t\tIsRequired = false,\r\n\t\tVisibleExpression = \"$= {favor} == \\\"篮球\\\"\"\r\n\t},\r\n}"
        },
        "help": {
          "VarKey": null,
          "Value": ""
        },
        "titleColumnWidth": {
          "VarKey": null,
          "Value": "100"
        },
        "windowWidth": {
          "VarKey": null,
          "Value": "500"
        },
        "windowHeight": {
          "VarKey": null,
          "Value": "0"
        },
        "restoreFocus": {
          "VarKey": null,
          "Value": "0"
        },
        "topMost": {
          "VarKey": null,
          "Value": "false"
        },
        "disableEnterSubmit": {
          "VarKey": null,
          "Value": "0"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        },
        "markdownhelp": {
          "VarKey": null,
          "Value": ""
        },
        "confirm": {
          "VarKey": null,
          "Value": ""
        },
        "customButtons": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "button": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:showText",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "NO_WAIT"
        },
        "text": {
          "VarKey": null,
          "Value": "$={userInfo}.ToJson(true);"
        },
        "title": {
          "VarKey": null,
          "Value": "结果内容"
        },
        "topMost": {
          "VarKey": null,
          "Value": "false"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        },
        "operations": {
          "VarKey": null,
          "Value": ""
        },
        "autoCloseKey": {
          "VarKey": null,
          "Value": ""
        },
        "winLocation": {
          "VarKey": null,
          "Value": "CenterScreen"
        },
        "winSize": {
          "VarKey": null,
          "Value": ""
        },
        "fontsize": {
          "VarKey": null,
          "Value": "14"
        },
        "fontfamily": {
          "VarKey": null,
          "Value": ""
        },
        "bgColor": {
          "VarKey": null,
          "Value": ""
        },
        "textColor": {
          "VarKey": null,
          "Value": ""
        },
        "highlight": {
          "VarKey": null,
          "Value": ""
        },
        "autoSaveToState": {
          "VarKey": null,
          "Value": ""
        },
        "closeWhenLostFocus": {
          "VarKey": null,
          "Value": "false"
        },
        "showLineNum": {
          "VarKey": null,
          "Value": "true"
        },
        "autoWrap": {
          "VarKey": null,
          "Value": "true"
        },
        "showBuildInToolbar": {
          "VarKey": null,
          "Value": "true"
        },
        "copyWholeLine": {
          "VarKey": null,
          "Value": "false"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "windowHandle": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```

</details>

***

## 85.重放键鼠操作

**功能描述**
> 重放录制好的键鼠操作数据。

**官方文档**
> https://getquicker.net/KC/Help/Doc/playrecord

**内部名称**
> sys:playRecords

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| data | 录制数据 | 录制的键鼠操作数据 | (0)字符串-Text |  | True |
| speed | 重放速度 | 重放操作的速度 | (1)数字(小数)-Number | 2 | True |

</details>
<details>
<summary>传出参数</summary>
无
</details>
<details>
<summary>范例</summary>

**简单示例**
```json
{
  "Variables": [],
  "Steps": [
    {
      "StepRunnerKey": "sys:playRecords",
      "InputParams": {
        "data": {
          "VarKey": null,
          "Value": "816;\tMC;\tLeft,693,2130,1;\r\n559;\tMC;\tLeft,1531,1274,1;\r\n707;\tKP;\tSpace;\r\n207;\tKD;\tLShiftKey;\r\n184;\tKP;\tH;\r\n59;\tKU;\tLShiftKey;\r\n103;\tKP;\tE;\r\n106;\tKP;\tL;\r\n152;\tKP;\tL;\r\n192;\tKP;\tO;\r\n152;\tKP;\tSpace;\r\n130;\tKD;\tLShiftKey;\r\n88;\tKP;\tW;\r\n72;\tKU;\tLShiftKey;\r\n76;\tKP;\tO;\r\n126;\tKP;\tR;\r\n83;\tKP;\tL;\r\n147;\tKP;\tD;\r\n216;\tKD;\tLShiftKey;\r\n131;\tKP;\tD1;\r\n80;\tKU;\tLShiftKey;\r\n71;\tKD;\tLShiftKey;\r\n40;\tKU;\tLShiftKey;"
        },
        "speed": {
          "VarKey": null,
          "Value": "2"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 86.录制键鼠操作

**功能描述**
> 录制键鼠操作过程，录制的数据使用绝对坐标

**官方文档**
> https://getquicker.net/KC/Help/Doc/record

**内部名称**
> sys:record

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| autoStart | 自动开始录制 | 2秒后是否自动开始录制 | (2)布尔值-Boolean | True | False |
| recordMouseMove | 录制鼠标移动过程 | 是否录制鼠标的中间移动过程，仅必要时开启。关闭时仅记录点击位置。 | (2)布尔值-Boolean | True | False |
| prepareSeconds | 准备时间 | 开始录制前的倒计时秒数（支持小数） | (1)数字(小数)-Number | 2 | False |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| output | 录制数据 | 录制的结果数据 | (0)字符串-Text |

</details>
<details>
<summary>范例</summary>

**录制并重放一遍**
```json
{
  "Variables": [
    {
      "Key": "output",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:record",
      "InputParams": {
        "autoStart": {
          "VarKey": null,
          "Value": "true"
        },
        "recordMouseMove": {
          "VarKey": null,
          "Value": "false"
        },
        "prepareSeconds": {
          "VarKey": null,
          "Value": "3.6"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "output": "output",
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:playRecords",
      "InputParams": {
        "data": {
          "VarKey": "output",
          "Value": null
        },
        "speed": {
          "VarKey": null,
          "Value": "2.5"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 87.运行脚本

**功能描述**
> 此模块用于执行一段脚本代码。除了CMD命令，其他脚本类型将会在执行时先将脚本存入临时文件，然后执行此临时文件。

**官方文档**
> https://getquicker.net/KC/Help/Doc/runScript

**内部名称**
> sys:runScript

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| script | 脚本内容 | 要运行的脚本内容 | (0)字符串-Text |  | True |
| type | 脚本类型 | 要执行的脚本类型 | (9)选项-Enum（CMD_K: CMD命令 (完成后保留窗口); CMD_C: CMD命令 (完成后关闭窗口); CMD_H: CMD命令 (隐藏命令行窗口); BAT: BAT批处理脚本(.bat); CMD_F: CMD批处理脚本(.cmd); PS: PowerShell脚本(.ps1); AHK: AutoHotKey脚本(.ahk); CUSTOM: 自定义脚本类型） | CMD_K | True |
| ext | 扩展名 | 自定义脚本文件的扩展名(如: .ps1 ) | (0)字符串-Text |  | True |
| encoding | 文件编码 | 写入文件的编码格式 | (9)选项-Enum | default | True |
| runner | 使用指定软件 | 使用指定的程序运行脚本。如果双击脚本可以直接运行，则不需要指定。 | (0)字符串-Text |  | True |
| argTemplate | 命令行参数模板 | 使用指定软件时指定命令行参数的格式。%FILE% 代替脚本文件的路径。 | (0)字符串-Text | %FILE% | True |
| outputEncoding | 控制台输出编码 | 控制台输出编码。如果输出遇到乱码，尝试修改此选项。 | (9)选项-Enum | oem | True |
| workingDir | 工作目录 | 不填写（自动为资源管理器的当前目录或桌面目录）或具体的工作目录路径。 | (0)字符串-Text |  | False |
| runAsAdmin | 以管理员身份运行 | 是否以管理员身份运行脚本。隐藏窗口或输出控制台内容时，不支持以管理员身份运行。 | (2)布尔值-Boolean | False | False |
| waitToExit | 等待进程结束 | 等待此进程结束后再进行后续操作 | (2)布尔值-Boolean | False | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| stdout | 控制台输出 | 捕获控制台输出(输出stdout，为空时输出stderr)，会自动等待进程结束。输出此内容时，命令行窗口将不显示。 | (0)字符串-Text |
| stdoutOnly | 标准输出 | 捕获标准输出(stdout)，会自动等待进程结束。输出此内容时，命令行窗口将不显示。 | (0)字符串-Text |
| stderr | 错误输出 | 捕获错误输出(stderr)，会自动等待进程结束。输出此内容时，命令行窗口将不显示。 | (0)字符串-Text |

</details>
<details>
<summary>范例</summary>

**一键断开网络，又一键开启网络**
```json
{
  "Variables": [
    {
      "Key": "text",
      "Type": 0,
      "Desc": "默认的文本变量",
      "DefaultValue": "",
      "SaveState": true,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "text2",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "状态开",
      "Type": 2,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": true,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:getCurrentTime",
      "InputParams": {
        "source": {
          "VarKey": null,
          "Value": "currTime"
        },
        "useUtc": {
          "VarKey": null,
          "Value": "0"
        },
        "addDays": {
          "VarKey": null,
          "Value": "0"
        },
        "addHours": {
          "VarKey": null,
          "Value": "0"
        },
        "addMinutes": {
          "VarKey": null,
          "Value": "0"
        },
        "addSeconds": {
          "VarKey": null,
          "Value": "0"
        },
        "addMonths": {
          "VarKey": null,
          "Value": "0"
        },
        "format": {
          "VarKey": null,
          "Value": "yyyy-MM-dd"
        },
        "outputCulture": {
          "VarKey": null,
          "Value": "CURRENT"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "output": null,
        "strValue": "text2",
        "timeStamp": null,
        "timeStampMs": null,
        "year": null,
        "month": null,
        "day": null,
        "hour": null,
        "minute": null,
        "second": null,
        "dayOfWeek": null,
        "dayOfYear": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:simpleIf",
      "InputParams": {
        "condition": {
          "VarKey": null,
          "Value": "$= {text} != {text2}"
        }
      },
      "OutputParams": {},
      "IfSteps": [
        {
          "StepRunnerKey": "sys:assign",
          "InputParams": {
            "input": {
              "VarKey": "text2",
              "Value": null
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "isSuccess": null,
            "output": "text",
            "errMessage": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:assign",
          "InputParams": {
            "input": {
              "VarKey": null,
              "Value": "true"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "isSuccess": null,
            "output": "状态开",
            "errMessage": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:notify",
          "InputParams": {
            "type": {
              "VarKey": null,
              "Value": "Info"
            },
            "msg": {
              "VarKey": null,
              "Value": "首次&每日首次使用\r\n默认执行断开网络！"
            },
            "maxLines": {
              "VarKey": null,
              "Value": "0"
            },
            "style": {
              "VarKey": null,
              "Value": "Default"
            },
            "clickAction": {
              "VarKey": null,
              "Value": ""
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:if",
      "InputParams": {
        "condition": {
          "VarKey": "状态开",
          "Value": null
        }
      },
      "OutputParams": {},
      "IfSteps": [
        {
          "StepRunnerKey": "sys:runScript",
          "InputParams": {
            "script": {
              "VarKey": null,
              "Value": "@echo off\r\nnetsh interface set interface \"Wi-Fi\" disable\r\nnetsh interface set interface \"以太网\" disable\r\necho 无线网络和有线网络已全部断开连接。"
            },
            "type": {
              "VarKey": null,
              "Value": "BAT"
            },
            "encoding": {
              "VarKey": null,
              "Value": "default"
            },
            "outputEncoding": {
              "VarKey": null,
              "Value": "oem"
            },
            "workingDir": {
              "VarKey": null,
              "Value": ""
            },
            "runAsAdmin": {
              "VarKey": null,
              "Value": "1"
            },
            "waitToExit": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "stdout": null,
            "stdoutOnly": null,
            "stderr": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:assign",
          "InputParams": {
            "input": {
              "VarKey": null,
              "Value": "false"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "isSuccess": null,
            "output": "状态开",
            "errMessage": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:notify",
          "InputParams": {
            "type": {
              "VarKey": null,
              "Value": "Success"
            },
            "msg": {
              "VarKey": null,
              "Value": "网 络  已 \r\n断 开 连接"
            },
            "maxLines": {
              "VarKey": null,
              "Value": "0"
            },
            "style": {
              "VarKey": null,
              "Value": "Default"
            },
            "clickAction": {
              "VarKey": null,
              "Value": ""
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": [
        {
          "StepRunnerKey": "sys:runScript",
          "InputParams": {
            "script": {
              "VarKey": null,
              "Value": "@echo off\r\nnetsh interface set interface \"Wi-Fi\" enable\r\nnetsh interface set interface \"以太网\" enable\r\necho 无线网络和有线网络已全部恢复连接。"
            },
            "type": {
              "VarKey": null,
              "Value": "BAT"
            },
            "encoding": {
              "VarKey": null,
              "Value": "default"
            },
            "outputEncoding": {
              "VarKey": null,
              "Value": "oem"
            },
            "workingDir": {
              "VarKey": null,
              "Value": ""
            },
            "runAsAdmin": {
              "VarKey": null,
              "Value": "1"
            },
            "waitToExit": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "stdout": null,
            "stdoutOnly": null,
            "stderr": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:assign",
          "InputParams": {
            "input": {
              "VarKey": null,
              "Value": "true"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "isSuccess": null,
            "output": "状态开",
            "errMessage": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:notify",
          "InputParams": {
            "type": {
              "VarKey": null,
              "Value": "Info"
            },
            "msg": {
              "VarKey": null,
              "Value": "网络已取消禁用"
            },
            "maxLines": {
              "VarKey": null,
              "Value": "0"
            },
            "style": {
              "VarKey": null,
              "Value": "Default"
            },
            "clickAction": {
              "VarKey": null,
              "Value": ""
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```


**安装grep存放在C:\Windows\grep目录下**
```json
{
  "Variables": [
    {
      "Key": "cache",
      "Type": 0,
      "Desc": "缓存",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "cache2",
      "Type": 0,
      "Desc": "缓存2号",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:notify",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "Info"
        },
        "msg": {
          "VarKey": null,
          "Value": "开始下载grep"
        },
        "maxLines": {
          "VarKey": null,
          "Value": "0"
        },
        "style": {
          "VarKey": null,
          "Value": "Default"
        },
        "clickAction": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:download",
      "InputParams": {
        "url": {
          "VarKey": null,
          "Value": "http://www.interlog.com/~tcharron/grep20d_win.zip"
        },
        "savePath": {
          "VarKey": null,
          "Value": "C:\\ProgramData\\Quicker"
        },
        "saveName": {
          "VarKey": null,
          "Value": ""
        },
        "ua": {
          "VarKey": null,
          "Value": ""
        },
        "header": {
          "VarKey": null,
          "Value": ""
        },
        "cookie": {
          "VarKey": null,
          "Value": ""
        },
        "expireSeconds": {
          "VarKey": null,
          "Value": "10"
        },
        "skipCertVerify": {
          "VarKey": null,
          "Value": "0"
        },
        "showProgress": {
          "VarKey": null,
          "Value": "1"
        },
        "autoRename": {
          "VarKey": null,
          "Value": "0"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "savedPath": "cache2",
        "contentMd5": null,
        "eTag": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "下载并把文件路径 -->{cache2}",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:notify",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "Success"
        },
        "msg": {
          "VarKey": null,
          "Value": "下载完成！"
        },
        "maxLines": {
          "VarKey": null,
          "Value": "0"
        },
        "style": {
          "VarKey": null,
          "Value": "Default"
        },
        "clickAction": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:zip",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "Unzip"
        },
        "sourceZipFile": {
          "VarKey": "cache2",
          "Value": null
        },
        "outputPath": {
          "VarKey": null,
          "Value": "C:\\Windows\\grep"
        },
        "password": {
          "VarKey": null,
          "Value": ""
        },
        "overwrite": {
          "VarKey": null,
          "Value": "0"
        },
        "skipOverwriteError": {
          "VarKey": null,
          "Value": "0"
        },
        "showProgress": {
          "VarKey": null,
          "Value": "0"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "resultPath": "cache",
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "{cache} --> 解压压缩包",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:runScript",
      "InputParams": {
        "script": {
          "VarKey": null,
          "Value": "$$setx Path \"%Path%;{cache}\" /m"
        },
        "type": {
          "VarKey": null,
          "Value": "CMD_H"
        },
        "encoding": {
          "VarKey": null,
          "Value": "default"
        },
        "outputEncoding": {
          "VarKey": null,
          "Value": "oem"
        },
        "workingDir": {
          "VarKey": null,
          "Value": ""
        },
        "runAsAdmin": {
          "VarKey": null,
          "Value": "1"
        },
        "waitToExit": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "stdout": null,
        "stdoutOnly": null,
        "stderr": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "添加系统环境变量",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:notify",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "Success"
        },
        "msg": {
          "VarKey": null,
          "Value": "安装完成！现在你可以在命令行中使用grep命令了！"
        },
        "maxLines": {
          "VarKey": null,
          "Value": "0"
        },
        "style": {
          "VarKey": null,
          "Value": "Default"
        },
        "clickAction": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:fileOperation",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "deleteFile"
        },
        "path": {
          "VarKey": "cache2",
          "Value": null
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "删除压缩包",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```

**EXCEL将相邻的相同内容单元格合并，支持多列，合并后不破坏原始数据和单元格格式(文本,日期,货币)**
```json
{
  "Variables": [],
  "Steps": [
    {
      "StepRunnerKey": "sys:runScript",
      "InputParams": {
        "script": {
          "VarKey": null,
          "Value": "Dim app, sh, rng, i, k, m\r\n'数组不需要申明，如果申明了，下面赋值时会报错：未引用设置到对象的实例。\r\nSet app = GetObject(, \"Excel.Application\")\r\n'2019WPS是ket.Application;2021WPS是excel.Application\r\n'EXCEL是Excel.Application\r\napp.ScreenUpdating = False\r\napp.DisplayAlerts = False\r\nSet sh = app.ActiveSheet\r\nSet rng = app.Selection\r\n'数组赋值时，要用对象.value\r\narr = rng.value\r\ncolnum = rng.Columns.Count\r\nrownum = rng.Rows.Count\r\nncol = rng.Column\r\nnrow = rng.Row\r\n'HH列有内容时,请修改为无内容列号\r\nLinShiLie = \"HH\"\r\n'If sh.cells(1,linshilie) <> \"\" then\r\n    'MsgBox \"临时调用HH1单元格，发现已有内容存在，请修改列号\",,\"Quicker提示             \"\r\n    'WScript.Quit\r\n'End If\r\nFor j = 1 To colnum\r\n    k = 1\r\n    For i = rownum To 2 Step -1\r\n        If arr(i, j) = arr(i - 1, j) Then\r\n            'k合并几个单元格\r\n            k = k + 1\r\n            If sh.Cells(nrow + rownum - (rownum - i + 1), ncol + j - 1).NumberFormatLocal <> \"G/通用格式\" Then\r\n                CellFormat = sh.Cells(nrow + rownum - (rownum - i + 1), ncol + j - 1).NumberFormatLocal\r\n            End If\r\n        Else\r\n            If k > 1 Then\r\n                up_no = rownum - k - kk + 1\r\n                sh.Cells(1, LinShiLie).Resize(k, 1).Merge\r\n                sh.Cells(1, LinShiLie).Resize(k, 1).Copy\r\n                sh.Cells(nrow + up_no - 1, ncol + j - 1).Resize(k, 1).PasteSpecial -4122\r\n                sh.Cells(1, LinShiLie).Resize(k, 1).UnMerge\r\n                If CellFormat <> \"\" Then\r\n                    sh.Cells(nrow + up_no - 1, ncol + j - 1).NumberFormatLocal = CellFormat\r\n                    CellFormat = \"\"\r\n                End If\r\n            End If\r\n            kk = k + kk\r\n            k = 1\r\n        End If\r\n    Next\r\n    '以下不能删,否则一列最后数据相同时不会合并\r\n    If k > 1 Then\r\n        up_no = rownum - k - kk + 1\r\n        sh.Cells(1, LinShiLie).Resize(k, 1).Merge\r\n        sh.Cells(1, LinShiLie).Resize(k, 1).Copy\r\n        sh.Cells(nrow + up_no - 1, ncol + j - 1).Resize(k, 1).PasteSpecial -4122\r\n        sh.Cells(1, LinShiLie).Resize(k, 1).UnMerge\r\n        If CellFormat <> \"\" Then\r\n            sh.Cells(nrow + up_no - 1, ncol + j - 1).NumberFormatLocal = CellFormat\r\n            CellFormat = \"\"\r\n        End If\r\n    End If\r\n    kk = 0\r\nNext\r\napp.ScreenUpdating = True\r\napp.DisplayAlerts = True\r\nSet app = Nothing\r\nSet sh = Nothing\r\nSet rng = Nothing"
        },
        "type": {
          "VarKey": null,
          "Value": "CUSTOM"
        },
        "ext": {
          "VarKey": null,
          "Value": "VBS"
        },
        "encoding": {
          "VarKey": null,
          "Value": "utf-16"
        },
        "runner": {
          "VarKey": null,
          "Value": ""
        },
        "argTemplate": {
          "VarKey": null,
          "Value": "%FILE%"
        },
        "outputEncoding": {
          "VarKey": null,
          "Value": "oem"
        },
        "workingDir": {
          "VarKey": null,
          "Value": ""
        },
        "runAsAdmin": {
          "VarKey": null,
          "Value": "0"
        },
        "waitToExit": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "stdout": null,
        "stdoutOnly": null,
        "stderr": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```

</details>

***

## 88.状态存取

**功能描述**
> 存取状态数据；更新动作的徽标文字；设置附加的动作右键菜单项

**官方文档**
> https://getquicker.net/KC/Help/Doc/stateStorage

**内部名称**
> sys:stateStorage

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| type | 操作类型 |  | (9)选项-Enum（readActionState: 读取动作状态; saveActionState: 写入动作状态; UpdateActionBadge: 设置徽标文字; UpdateOverlyIcon: 设置徽标图标; UpdateContextMenu: 设置附加的右键菜单项; readGlobalState: 【谨慎使用】读取全局状态; saveGlobalState: 【谨慎使用】写入全局状态） | readActionState | True |
| key | 名称 | 存储或读取的状态条目名称。 | (0)字符串-Text |  | False |
| defaultValue | 默认值 | 读取失败的时候返回的值 | (0)字符串-Text |  | False |
| value | 值 | 要保存的状态值。使用*NULL*删除此状态的存储。 | (0)字符串-Text |  | False |
| inputIfEmpty | 为空时请用户输入 | 如果读到的状态值为空，则弹出对话框请用户输入值。启用此选项时，请保持默认值为空。 | (2)布尔值-Boolean | False | False |
| prompt | 用户输入提示 | 需要用户输入变量内容时，给用户的输入提示。 | (0)字符串-Text |  | False |
| badgeText | 徽标文字 | 在动作右上角显示的提示文字 | (0)字符串-Text |  | False |
| badgeColor | 徽标颜色 | 在动作右上角显示的徽标底色。留空表示透明。 | (0)字符串-Text |  | False |
| badgeTextColor | 徽标文字颜色 |  | (0)字符串-Text |  | False |
| actionContextMenu | 附加的右键菜单项 | 附加的动作右键菜单，格式请参考文档 | (0)字符串-Text |  | False |
| overlayIcon | 徽标图标 | 使用内置矢量图标：“fa:图标名称:图标颜色”。如：“fa:Solid_Circle:#FF0000” | (0)字符串-Text |  | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 是否成功获取了值 | (2)布尔值-Boolean |
| value | 值 | 读取到的值 | (99)任意类型-Any |
| isEmpty | 是否为空 | 读取到的值是否为空 | (2)布尔值-Boolean |

</details>
<details>
<summary>范例</summary>

**将123存入状态abc；读取存储的状态abc，如果读取不到就返回-1，结果保存在value变量**
```json
{
  "Variables": [
    {
      "Key": "value",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:stateStorage",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "saveActionState"
        },
        "key": {
          "VarKey": null,
          "Value": "abc"
        },
        "value": {
          "VarKey": null,
          "Value": "123"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:stateStorage",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "readActionState"
        },
        "key": {
          "VarKey": null,
          "Value": "abc"
        },
        "defaultValue": {
          "VarKey": null,
          "Value": "-1"
        },
        "inputIfEmpty": {
          "VarKey": null,
          "Value": "0"
        },
        "prompt": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "value": "value",
        "isEmpty": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 89.下载文件

**功能描述**
> 下载网络文件(请勿用于下载大文件)

**官方文档**
> https://getquicker.net/KC/Help/Doc/download

**内部名称**
> sys:download

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| url | 网址 | 要下载的文件网址 | (0)字符串-Text | https:// | True |
| savePath | 保存文件夹 | 下载文件的保存位置（文件夹的路径） | (0)字符串-Text |  | True |
| saveName | 保存文件名 | 可选。为空时自动判断文件名。 | (0)字符串-Text |  | True |
| ua | UserAgent | 可选。 | (0)字符串-Text |  | False |
| header | 请求头 | 发送的HttpHeader。每行一个header，格式为Name:Value | (0)字符串-Text |  | False |
| cookie | Cookie | 请求的cookie内容 | (0)字符串-Text |  | False |
| expireSeconds | 超时秒数 | 长时间未接收到数据时，中止下载。 | (1)数字(小数)-Number | 10 | False |
| skipCertVerify | 忽略HTTPS证书验证 |  | (2)布尔值-Boolean | False | False |
| showProgress | 显示进度条 | 是否显示下载进度条 | (2)布尔值-Boolean | False | False |
| autoRename | 如果文件已存在，自动重命名下载的文件 | 在文件名后面增加“_序号”避免重复。否则将会覆盖已有文件。 | (2)布尔值-Boolean | False | False |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 是否成功下载了文件 | (2)布尔值-Boolean |
| savedPath | 文件路径 | 文件的完整保存路径 | (0)字符串-Text |
| contentMd5 | 内容MD5 | 内容MD5值，不是所有请求都会返回此内容。 | (0)字符串-Text |
| eTag | ETag | 响应头Etag值，不是所有请求都会返回此内容。 | (0)字符串-Text |
| downloadSize | 下载大小 | 下载文件的大小（字节数） | (0)字符串-Text |

</details>
<details>
<summary>范例</summary>

**下载并运行**
```json
{
  "Variables": [
    {
      "Key": "savedPath",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": true,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "path",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:getFolderPath",
      "InputParams": {
        "folder": {
          "VarKey": null,
          "Value": "ApplicationData"
        }
      },
      "OutputParams": {
        "path": "path"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:download",
      "InputParams": {
        "url": {
          "VarKey": null,
          "Value": "https://gitee.com/jinxi100/one/raw/master/%E5%89%AA%E5%88%87%E6%9D%BF%E5%B7%A5%E5%85%B7%20(1).exe"
        },
        "savePath": {
          "VarKey": "path",
          "Value": null
        },
        "saveName": {
          "VarKey": null,
          "Value": "剪切板工具.exe"
        },
        "ua": {
          "VarKey": null,
          "Value": ""
        },
        "header": {
          "VarKey": null,
          "Value": ""
        },
        "cookie": {
          "VarKey": null,
          "Value": ""
        },
        "expireSeconds": {
          "VarKey": null,
          "Value": "10"
        },
        "skipCertVerify": {
          "VarKey": null,
          "Value": "1"
        },
        "showProgress": {
          "VarKey": null,
          "Value": "1"
        },
        "autoRename": {
          "VarKey": null,
          "Value": "1"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "savedPath": "savedPath",
        "contentMd5": null,
        "eTag": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:run",
      "InputParams": {
        "path": {
          "VarKey": "savedPath",
          "Value": null
        },
        "arg": {
          "VarKey": null,
          "Value": ""
        },
        "runas": {
          "VarKey": null,
          "Value": "false"
        },
        "activateWindowIfRunning": {
          "VarKey": null,
          "Value": "false"
        },
        "activateWindowHotkey": {
          "VarKey": null,
          "Value": ""
        },
        "alternativePath": {
          "VarKey": null,
          "Value": ""
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        },
        "setWorkingDir": {
          "VarKey": null,
          "Value": "1"
        },
        "windowStyle": {
          "VarKey": null,
          "Value": "0"
        },
        "waitInputIdle": {
          "VarKey": null,
          "Value": "false"
        },
        "waitExit": {
          "VarKey": null,
          "Value": "false"
        },
        "username": {
          "VarKey": null,
          "Value": ""
        },
        "password": {
          "VarKey": null,
          "Value": ""
        },
        "outputEncoding": {
          "VarKey": null,
          "Value": "oem"
        },
        "envVariables": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "pid": null,
        "mainWinHandle": null,
        "mainWinTitle": null,
        "stdout": null,
        "stdoutOnly": null,
        "stderr": null,
        "exitCode": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 90.基础OCR

**功能描述**
> 获取图片中的文字

**官方文档**
> https://getquicker.net/KC/Help/Doc/basic-ocr

**内部名称**
> sys:basic-ocr

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| operation | 接口/引擎 | OCR接口或引擎。离线引擎安装方式请参考模块文档。 | (9)选项-Enum（QuickerServerOcr: Quicker OCR引擎; WindowsOcr: Windows10/11 内置OCR引擎; baidu-basic: 百度通用文字识别（自定义帐号）; baidu-quicker: 百度通用文字识别（Quicker帐号）; baidu-custom: 百度自定义接口识别（自定义帐号）; table_quicker: 表格识别（Quicker服务）） | QuickerServerOcr | True |
| apiKey | ApiKey | 请填写OCR帐号的ApiKey | (0)字符串-Text |  | True |
| secretKey | SecretKey | 请填写OCR帐号的SecretKey | (0)字符串-Text |  | True |
| imgVar | 图片变量 | 从指定变量中加载图片 | (3)图片-Image |  | True |
| punctuationType | 转换标点符号 | 合并文本时，是否转换标点符号 | (9)选项-Enum（no: 不转换; sbc: 全角符号; dbc: 半角符号） | no | True |
| mergeChapter | 合并段落 | 是否智能合并段落。 | (9)选项-Enum（no: 不合并; merge: 合并） | no | True |
| interface | 接口名称或网址 | 接口的完整网址，或 https://aip.baidubce.com/rest/2.0/ocr/v1/ 后面的部分 | (0)字符串-Text（general_basic: 通用文字识别（标准版）; general: 通用文字识别（标准含位置版）; accurate_basic: 通用文字识别（高精度版）; accurate: 通用文字识别（高精度含位置版）; handwriting: 手写文字识别; numbers: 数字识别; doc_analysis_office: 办公文档识别; form: 表格文字识别(同步接口); qrcode: 二维码识别） |  | False |
| options | 附加参数 | 请参考百度官方/Quicker服务接口说明。每行一个参数，使用option:value的格式。 | (10)词典-Dict |  | False |
| lang | 语言 | 待识别内容的语言。表格识别仅支持中英混合和英文。 | (0)字符串-Text（CHN_ENG: 中英混合; ENG: 英语; KOR: 韩语; JAP: 日语; CHT: 繁体中文; LAT: 拉丁语; ARA: 阿拉伯语） |  | False |
| offlineMode | 离线模式 | 是否使用离线引擎。自动：安装离线引擎时使用离线，否则使用在线。 | (9)选项-Enum（Auto: 自动; OnlineOnly: 仅使用在线服务; OfflineOnly: 仅使用离线引擎） | Auto | False |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| content | 合并后结果 | 合并在一起的的文本内容 | (0)字符串-Text |
| textList | 行列表 | OCR识别结果，列表格式，每行一项。 | (4)文本列表-List |
| rawData | 原始结果 | API接口返回的完整内容 | (0)字符串-Text |
| rawObject | 原始结果JObject对象 | 返回结果的JObject对象 | (98)对象(Object)-Object |

</details>
<details>
<summary>范例</summary>

**截图识别并自动复制结果**
```json
{
  "Variables": [
    {
      "Key": "text",
      "Type": 0,
      "Desc": "默认的文本变量",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": null,
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "img",
      "Type": 3,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "showWindow",
      "Type": 2,
      "Desc": "是否显示文本窗口",
      "DefaultValue": "1",
      "SaveState": true,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "autoCopy",
      "Type": 2,
      "Desc": "自动复制",
      "DefaultValue": "1",
      "SaveState": true,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "lang",
      "Type": 0,
      "Desc": "语言",
      "DefaultValue": "",
      "SaveState": true,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "设置处理"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:simpleIf",
      "InputParams": {
        "condition": {
          "VarKey": null,
          "Value": "$= {quicker_in_param} == \"settings\""
        }
      },
      "OutputParams": {},
      "IfSteps": [
        {
          "StepRunnerKey": "sys:form",
          "InputParams": {
            "operation": {
              "VarKey": null,
              "Value": "variables"
            },
            "title": {
              "VarKey": null,
              "Value": "动作设置"
            },
            "formDef": {
              "VarKey": null,
              "Value": "{\"Fields\":[{\"FieldKey\":\"lang\",\"DictVarType\":null,\"Label\":\"语言\",\"HelpText\":\"待识别内容的语言\",\"HelpLink\":null,\"InputMethod\":3,\"SelectionItems\":\"中英|\\r\\n英语|ENG\\r\\n韩语|KOR\\r\\n日语|JAP\\r\\n繁体中文|CHT\\r\\n拉丁语|LAT\\r\\n阿拉伯语|ARA\",\"IsRequired\":false,\"MinValue\":\"\",\"MaxValue\":\"\",\"Pattern\":\"\",\"InputWidth\":\"\",\"MaxLength\":0,\"ImeState\":null,\"TextTools\":\"\",\"VisibleExpression\":\"\",\"DefaultValue\":null,\"Group\":\"\"},{\"FieldKey\":\"autoCopy\",\"DictVarType\":null,\"Label\":\"自动复制识别结果\",\"HelpText\":\"\",\"HelpLink\":null,\"InputMethod\":6,\"SelectionItems\":\"\",\"IsRequired\":false,\"MinValue\":\"\",\"MaxValue\":\"\",\"Pattern\":\"\",\"InputWidth\":\"\",\"MaxLength\":0,\"ImeState\":null,\"TextTools\":\"\",\"VisibleExpression\":\"\",\"DefaultValue\":null,\"Group\":\"\"},{\"FieldKey\":\"showWindow\",\"DictVarType\":null,\"Label\":\"使用文本窗口显示识别结果\",\"HelpText\":\"\",\"HelpLink\":null,\"InputMethod\":6,\"SelectionItems\":\"\",\"IsRequired\":false,\"MinValue\":\"\",\"MaxValue\":\"\",\"Pattern\":\"\",\"InputWidth\":\"\",\"MaxLength\":0,\"ImeState\":null,\"TextTools\":\"\",\"VisibleExpression\":\"\",\"DefaultValue\":null,\"Group\":\"\"}]}"
            },
            "help": {
              "VarKey": null,
              "Value": ""
            },
            "titleColumnWidth": {
              "VarKey": null,
              "Value": "100"
            },
            "windowWidth": {
              "VarKey": null,
              "Value": "500"
            },
            "windowHeight": {
              "VarKey": null,
              "Value": "0"
            },
            "restoreFocus": {
              "VarKey": null,
              "Value": "0"
            },
            "topMost": {
              "VarKey": null,
              "Value": "false"
            },
            "disableEnterSubmit": {
              "VarKey": null,
              "Value": "0"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            },
            "markdownhelp": {
              "VarKey": null,
              "Value": ""
            },
            "confirm": {
              "VarKey": null,
              "Value": ""
            },
            "customButtons": {
              "VarKey": null,
              "Value": ""
            }
          },
          "OutputParams": {
            "isSuccess": null,
            "button": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:stateStorage",
          "InputParams": {
            "type": {
              "VarKey": null,
              "Value": "UpdateActionBadge"
            },
            "badgeText": {
              "VarKey": "lang",
              "Value": null
            },
            "badgeColor": {
              "VarKey": null,
              "Value": "#428ca7"
            },
            "badgeTextColor": {
              "VarKey": null,
              "Value": ""
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:stop",
          "InputParams": {
            "method": {
              "VarKey": null,
              "Value": "default"
            },
            "isError": {
              "VarKey": null,
              "Value": "0"
            },
            "return": {
              "VarKey": null,
              "Value": ""
            },
            "showMessage": {
              "VarKey": null,
              "Value": ""
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "更新按钮上的语言名字"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:stateStorage",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "UpdateActionBadge"
        },
        "badgeText": {
          "VarKey": "lang",
          "Value": null
        },
        "badgeColor": {
          "VarKey": null,
          "Value": "#428ca7"
        },
        "badgeTextColor": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "截屏"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:if",
      "InputParams": {
        "condition": {
          "VarKey": null,
          "Value": "$= {quicker_in_param}.IsNullOrEmpty() == false \r\n\t&& File.Exists({quicker_in_param})"
        }
      },
      "OutputParams": {},
      "IfSteps": [
        {
          "StepRunnerKey": "sys:readFile",
          "InputParams": {
            "path": {
              "VarKey": "quicker_in_param",
              "Value": null
            },
            "type": {
              "VarKey": null,
              "Value": "image"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "image": "img",
            "isSuccess": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": [
        {
          "StepRunnerKey": "sys:screenCapture",
          "InputParams": {
            "type": {
              "VarKey": null,
              "Value": "select"
            },
            "delay": {
              "VarKey": null,
              "Value": "200"
            },
            "toClip": {
              "VarKey": null,
              "Value": "0"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "img": "img",
            "rect": null,
            "isSuccess": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "OCR识别"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:basic-ocr",
      "InputParams": {
        "operation": {
          "VarKey": null,
          "Value": "QuickerServerOcr"
        },
        "imgVar": {
          "VarKey": "img",
          "Value": null
        },
        "punctuationType": {
          "VarKey": null,
          "Value": "no"
        },
        "mergeChapter": {
          "VarKey": null,
          "Value": "no"
        },
        "lang": {
          "VarKey": "lang",
          "Value": null
        },
        "offlineMode": {
          "VarKey": null,
          "Value": "Auto"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "content": "text",
        "textList": null,
        "rawData": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "根据设置复制内容和显示结果"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:simpleIf",
      "InputParams": {
        "condition": {
          "VarKey": "autoCopy",
          "Value": null
        }
      },
      "OutputParams": {},
      "IfSteps": [
        {
          "StepRunnerKey": "sys:writeClipboard",
          "InputParams": {
            "type": {
              "VarKey": null,
              "Value": "auto"
            },
            "input": {
              "VarKey": "text",
              "Value": null
            },
            "successMsg": {
              "VarKey": null,
              "Value": "$=\"已复制!\" + {text}.ToShortString(30)"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "isSuccess": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:simpleIf",
      "InputParams": {
        "condition": {
          "VarKey": "showWindow",
          "Value": null
        }
      },
      "OutputParams": {},
      "IfSteps": [
        {
          "StepRunnerKey": "sys:showText",
          "InputParams": {
            "type": {
              "VarKey": null,
              "Value": "NO_WAIT"
            },
            "text": {
              "VarKey": "text",
              "Value": null
            },
            "title": {
              "VarKey": null,
              "Value": "识别结果"
            },
            "autoCloseKey": {
              "VarKey": null,
              "Value": "="
            },
            "topMost": {
              "VarKey": null,
              "Value": "false"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            },
            "operations": {
              "VarKey": null,
              "Value": ""
            },
            "winLocation": {
              "VarKey": null,
              "Value": "CenterScreen"
            },
            "winSize": {
              "VarKey": null,
              "Value": ""
            },
            "fontsize": {
              "VarKey": null,
              "Value": "14"
            },
            "fontfamily": {
              "VarKey": null,
              "Value": ""
            },
            "bgColor": {
              "VarKey": null,
              "Value": ""
            },
            "textColor": {
              "VarKey": null,
              "Value": ""
            },
            "highlight": {
              "VarKey": null,
              "Value": ""
            },
            "autoSaveToState": {
              "VarKey": null,
              "Value": ""
            },
            "closeWhenLostFocus": {
              "VarKey": null,
              "Value": "false"
            },
            "showLineNum": {
              "VarKey": null,
              "Value": "true"
            },
            "autoWrap": {
              "VarKey": null,
              "Value": "true"
            },
            "showBuildInToolbar": {
              "VarKey": null,
              "Value": "true"
            },
            "copyWholeLine": {
              "VarKey": null,
              "Value": "false"
            },
            "caretPosition": {
              "VarKey": null,
              "Value": "0"
            },
            "updateIfExists": {
              "VarKey": null,
              "Value": "0"
            }
          },
          "OutputParams": {
            "isSuccess": null,
            "windowHandle": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 91.弹窗提示或确认

**功能描述**
> 弹窗显示提示或确认对话框，这个对话框会占用焦点，并且会在手动关闭之前一直显示在屏幕上。动作也会停留在这个步骤，等待关闭后再继续执行。标准模式：类似于windows内置弹窗，支持固定图标和按钮组合；自定义模式：可自定义图标和按钮，显示内容比较灵活。


**官方文档**
> https://getquicker.net/KC/Help/Doc/msgbox

**内部名称**
> sys:MsgBox

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| operation | 模式 |  | (9)选项-Enum（default: 标准; custom: 自定义） | default | False |
| message | 消息内容 | 弹窗显示的消息内容。“自定义”模式时，也支持“MD:Markdown内容”。 | (0)字符串-Text | Hello. | True |
| title | 标题 | 消息窗口标题。留空时自动使用动作名称。 | (0)字符串-Text | Quicker | True |
| icon | 图标 | 消息窗口图标 | (9)选项-Enum（: 无; Information: 信息; Question: 疑问; Warning: 警告; Error: 错误） | Asterisk | True |
| customIcon | 图标 | 消息窗口图标。 | (0)字符串-Text | Information | True |
| buttons | 按钮 | 消息窗口图标 | (9)选项-Enum | OK | True |
| customButtons | 按钮 | 每行定义一个按钮，格式为 “文本” 或 “[图标]显示文本(提示内容)|值”。 | (0)字符串-Text | [fa:Regular_Check:#4caf50]是(_Y)|Yes
[fa:Regular_Times:#dc3545]否(_N)|No
[fa:Light_Undo:#444444]取消(_C)|Cancel | True |
| defaultButton | 默认按钮 | 指定默认按钮的值。默认按钮以高亮颜色显示，可直接回车选择。 | (0)字符串-Text | Yes | True |
| restoreFocus | 恢复活动窗口 | 关闭弹窗后，是否将焦点还原到之前的活动窗口 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| result | 选择的按钮 | 点击的按钮，标准模式下结果可能为OK,Cancel,Yes,No，自定义模式下为按钮的值。 | (0)字符串-Text |
| okOrYes | 是否确认 | 选择的按钮是否为“确定”或“是” | (2)布尔值-Boolean |

</details>
<details>
<summary>范例</summary>

```json
{
  "Variables": [
    {
      "Key": "选择的结果",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": null,
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "是否确认",
      "Type": 2,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": null,
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "result",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:MsgBox",
      "InputParams": {
        "operation": {
          "VarKey": null,
          "Value": "default"
        },
        "message": {
          "VarKey": null,
          "Value": "Hello. 你好，这是一条弹窗提示消息。\r\n两个结果选一个哦~"
        },
        "title": {
          "VarKey": null,
          "Value": "标准风格弹窗"
        },
        "icon": {
          "VarKey": null,
          "Value": "Question"
        },
        "buttons": {
          "VarKey": null,
          "Value": "OKCancel"
        },
        "restoreFocus": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "result": "选择的结果",
        "okOrYes": "是否确认"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:notify",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "Info"
        },
        "msg": {
          "VarKey": null,
          "Value": "$$标准弹窗选择的结果：{选择的结果}\r\n是否确认：{是否确认}"
        },
        "maxLines": {
          "VarKey": null,
          "Value": "0"
        },
        "style": {
          "VarKey": null,
          "Value": "Default"
        },
        "clickAction": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:MsgBox",
      "InputParams": {
        "operation": {
          "VarKey": null,
          "Value": "custom"
        },
        "message": {
          "VarKey": null,
          "Value": "你好，这是一条自定义弹窗提示消息。\r\n第二行。"
        },
        "title": {
          "VarKey": null,
          "Value": "自定义弹窗"
        },
        "customIcon": {
          "VarKey": null,
          "Value": "fa:Solid_InfoCircle:#FF0000"
        },
        "customButtons": {
          "VarKey": null,
          "Value": "[fa:Light_Check:#28a745]是(_Y)|Yes\r\n[fa:Light_Times:#dc3545]否(_N)|No\r\n[fa:Light_Undo:#28a745]取消(_C)|Cancel\r\n测试"
        },
        "defaultButton": {
          "VarKey": null,
          "Value": "Yes"
        },
        "restoreFocus": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "result": "result"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:notify",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "Info"
        },
        "msg": {
          "VarKey": null,
          "Value": "$$自定义弹窗选择的结果：{result}"
        },
        "maxLines": {
          "VarKey": null,
          "Value": "0"
        },
        "style": {
          "VarKey": null,
          "Value": "Default"
        },
        "clickAction": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 92.生成随机数

**功能描述**
> 生成随机数

**官方文档**
> https://getquicker.net/KC/Help/Doc/randomnum

**内部名称**
> sys:randomNum

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| min | 最小值 | 随机数范围的最小值（结果大于或等于此值） | (12)数字(整数)-Integer | 0 | True |
| max | 最大值 | 随机数范围的最大值（结果小于此值） | (12)数字(整数)-Integer | 100 | True |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| output | 随机数 | 生成的随机数 | (12)数字(整数)-Integer |

</details>
<details>
<summary>范例</summary>

```json
{
  "Variables": [
    {
      "Key": "output",
      "Type": 12,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:randomNum",
      "InputParams": {
        "min": {
          "VarKey": null,
          "Value": "0"
        },
        "max": {
          "VarKey": null,
          "Value": "100"
        }
      },
      "OutputParams": {
        "output": "output"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 93.Excel对象操作

**功能描述**
> 操作Excel的某个对象

**官方文档**
> https://getquicker.net/KC/Help/Doc/excelobjects

**内部名称**
> sys:excelObjects

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| operation | 操作类型 | 操作类型 | (9)选项-Enum（ApplicationInfo: 获取当前Excel应用信息; OpenFile: 工作簿: 打开工作簿; SaveWorkbook: 工作簿: 保存工作簿; CloseWorkbook: 工作簿: 关闭工作簿; CreateWorkbook: 工作簿: 创建工作簿; SelectWorksheet: 工作表：选择工作表） |  | True |
| path | 文件/模板路径 | 完整路径。创建工作簿时，用于指定模板文件。 | (0)字符串-Text |  | False |
| workbook | 工作簿对象 | 根据具体操作，可用参数不同。请参考文档。 | (98)对象(Object)-Object |  | False |
| params | 参数 | 根据具体操作，可用参数不同。请参考文档。 | (0)字符串-Text |  | False |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| activeWorkbook | 活动工作簿 | ActiveWorkbook | (98)对象(Object)-Object |
| activeSheet | 活动工作表 | ActiveSheet | (98)对象(Object)-Object |
| worksheetNames | 工作表名称的列表 | Worksheets | (4)文本列表-List |
| worksheets | 工作表对象列表 | Worksheets | (98)对象(Object)-Object |
| workbookPath | 工作簿路径 | Worksheets | (0)字符串-Text |
| application | Application对象 | Application对象的引用 | (98)对象(Object)-Object |

</details>
<details>
<summary>范例</summary>

**选择一个或多个excel文件使用Quicker的excel模块打开，从而可以在Quicker中控制该文件**
```json
{
  "Variables": [
    {
      "Key": "filePath",
      "Type": 0,
      "Desc": "一个文件的路径",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "isSuccess",
      "Type": 2,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "files",
      "Type": 4,
      "Desc": "选择的文件列表",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "isOpened",
      "Type": 2,
      "Desc": "是否打开了文件",
      "DefaultValue": "0",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:getSelectedFiles",
      "InputParams": {
        "stopIfFail": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {
        "files": "files",
        "firstFile": "filePath",
        "isSuccess": "isSuccess"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "获取选择的文件，如果有的话，依次打开"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:simpleIf",
      "InputParams": {
        "condition": {
          "VarKey": "isSuccess",
          "Value": null
        }
      },
      "OutputParams": {},
      "IfSteps": [
        {
          "StepRunnerKey": "sys:each",
          "InputParams": {
            "input": {
              "VarKey": "files",
              "Value": null
            },
            "useMultiThread": {
              "VarKey": null,
              "Value": "0"
            },
            "threadDelay": {
              "VarKey": null,
              "Value": "5"
            }
          },
          "OutputParams": {
            "item": "filePath",
            "count": null
          },
          "IfSteps": [
            {
              "StepRunnerKey": "sys:simpleIf",
              "InputParams": {
                "condition": {
                  "VarKey": null,
                  "Value": "$= {filePath}.ToLower().EndsWith(\".xlsx\") || {filePath}.ToLower().EndsWith(\".xls\")"
                }
              },
              "OutputParams": {},
              "IfSteps": [
                {
                  "StepRunnerKey": "sys:excelObjects",
                  "InputParams": {
                    "operation": {
                      "VarKey": null,
                      "Value": "OpenFile"
                    },
                    "path": {
                      "VarKey": "filePath",
                      "Value": null
                    },
                    "params": {
                      "VarKey": null,
                      "Value": ""
                    },
                    "stopIfFail": {
                      "VarKey": null,
                      "Value": "1"
                    }
                  },
                  "OutputParams": {
                    "isSuccess": null,
                    "activeWorkbook": null,
                    "activeSheet": null,
                    "worksheetNames": null,
                    "worksheets": null,
                    "application": null
                  },
                  "IfSteps": null,
                  "ElseSteps": null,
                  "Note": "",
                  "Disabled": false,
                  "Collapsed": false,
                  "DelayMs": 0
                },
                {
                  "StepRunnerKey": "sys:assign",
                  "InputParams": {
                    "input": {
                      "VarKey": null,
                      "Value": "true"
                    }
                  },
                  "OutputParams": {
                    "output": "isOpened"
                  },
                  "IfSteps": null,
                  "ElseSteps": null,
                  "Note": "",
                  "Disabled": false,
                  "Collapsed": false,
                  "DelayMs": 0
                }
              ],
              "ElseSteps": null,
              "Note": "",
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            }
          ],
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": [],
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "如果没有打开任何文件，则创建一个"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:simpleIf",
      "InputParams": {
        "condition": {
          "VarKey": null,
          "Value": "$= !{isOpened}"
        }
      },
      "OutputParams": {},
      "IfSteps": [
        {
          "StepRunnerKey": "sys:excelObjects",
          "InputParams": {
            "operation": {
              "VarKey": null,
              "Value": "CreateWorkbook"
            },
            "path": {
              "VarKey": null,
              "Value": ""
            },
            "params": {
              "VarKey": null,
              "Value": ""
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "isSuccess": null,
            "activeWorkbook": null,
            "activeSheet": null,
            "worksheets": null,
            "application": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```

**从工作表中选择一个**
```json
{
  "Variables": [
    {
      "Key": "useMenu",
      "Type": 2,
      "Desc": "是否使用菜单方式",
      "DefaultValue": "0",
      "SaveState": true,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "hideCurrent",
      "Type": 2,
      "Desc": "隐藏当前工作表",
      "DefaultValue": "0",
      "SaveState": true,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "list",
      "Type": 4,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "worksheet",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "isSuccessUsingExcelObj",
      "Type": 2,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "activeSheet",
      "Type": 99,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "activeSheetName",
      "Type": 0,
      "Desc": "当前工作表名称",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "先取回当前活动工作簿的Sheet名称列表。\r\n第一项为活动工作表名称，后面为所有工作表的名称"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:simpleIf",
      "InputParams": {
        "condition": {
          "VarKey": null,
          "Value": "$={quicker_in_param} == \"settings\""
        }
      },
      "OutputParams": {},
      "IfSteps": [
        {
          "StepRunnerKey": "sys:form",
          "InputParams": {
            "operation": {
              "VarKey": null,
              "Value": "variables"
            },
            "title": {
              "VarKey": null,
              "Value": "动作设置"
            },
            "formDef": {
              "VarKey": null,
              "Value": "{\"Fields\":[{\"FieldKey\":\"useMenu\",\"DictVarType\":null,\"Label\":\"使用菜单方式选择（否则使用选择列表）\",\"HelpText\":\"是：菜单方式选择； 否：列表方式选择；\",\"HelpLink\":null,\"InputMethod\":6,\"SelectionItems\":\"\",\"IsRequired\":false,\"MinValue\":\"\",\"MaxValue\":\"\",\"Pattern\":\"\",\"InputWidth\":\"\",\"MaxLength\":0,\"ImeState\":null,\"TextTools\":\"\",\"VisibleExpression\":\"\",\"DefaultValue\":null,\"ColumnWidth\":0.0,\"Group\":\"\"},{\"FieldKey\":\"hideCurrent\",\"DictVarType\":null,\"Label\":\"隐藏当前工作表\",\"HelpText\":\"在菜单或选择中不显示当前工作表\",\"HelpLink\":null,\"InputMethod\":6,\"SelectionItems\":\"\",\"IsRequired\":false,\"MinValue\":\"\",\"MaxValue\":\"\",\"Pattern\":\"\",\"InputWidth\":\"\",\"MaxLength\":0,\"ImeState\":null,\"TextTools\":\"\",\"VisibleExpression\":\"\",\"DefaultValue\":null,\"ColumnWidth\":0.0,\"Group\":\"\"}]}"
            },
            "help": {
              "VarKey": null,
              "Value": ""
            },
            "titleColumnWidth": {
              "VarKey": null,
              "Value": "100"
            },
            "windowWidth": {
              "VarKey": null,
              "Value": "500"
            },
            "windowHeight": {
              "VarKey": null,
              "Value": "0"
            },
            "restoreFocus": {
              "VarKey": null,
              "Value": "0"
            },
            "topMost": {
              "VarKey": null,
              "Value": "false"
            },
            "disableEnterSubmit": {
              "VarKey": null,
              "Value": "0"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            },
            "markdownhelp": {
              "VarKey": null,
              "Value": ""
            },
            "confirm": {
              "VarKey": null,
              "Value": ""
            },
            "customButtons": {
              "VarKey": null,
              "Value": ""
            },
            "selectedGroup": {
              "VarKey": null,
              "Value": ""
            }
          },
          "OutputParams": {
            "isSuccess": null,
            "button": null,
            "selectedGroup": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:stop",
          "InputParams": {
            "method": {
              "VarKey": null,
              "Value": "default"
            },
            "isError": {
              "VarKey": null,
              "Value": "0"
            },
            "return": {
              "VarKey": null,
              "Value": ""
            },
            "showMessage": {
              "VarKey": null,
              "Value": "已保存设置"
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:excelObjects",
      "InputParams": {
        "operation": {
          "VarKey": null,
          "Value": "ApplicationInfo"
        },
        "params": {
          "VarKey": null,
          "Value": ""
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {
        "isSuccess": "isSuccessUsingExcelObj",
        "activeWorkbook": null,
        "activeSheet": "activeSheet",
        "worksheetNames": "list",
        "worksheets": null,
        "workbookPath": null,
        "application": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:if",
      "InputParams": {
        "condition": {
          "VarKey": "isSuccessUsingExcelObj",
          "Value": null
        }
      },
      "OutputParams": {},
      "IfSteps": [
        {
          "StepRunnerKey": "sys:assign",
          "InputParams": {
            "input": {
              "VarKey": null,
              "Value": "$={activeSheet}.Name"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "isSuccess": null,
            "output": "activeSheetName"
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": [
        {
          "StepRunnerKey": "sys:comment",
          "InputParams": {
            "note": {
              "VarKey": null,
              "Value": "低权限模式. 列表第一项为当前活动工作表名称。"
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:csscript",
          "InputParams": {
            "mode": {
              "VarKey": null,
              "Value": "low_permission_roslyn"
            },
            "scriptForLp": {
              "VarKey": null,
              "Value": "//.cs  文件类型，便于外部编辑时使用\r\n// 引用必要的命名空间\r\nusing System.Windows.Forms;\r\nusing System.Runtime.InteropServices;\r\nusing Excel = Microsoft.Office.Interop.Excel;\r\nusing Microsoft.Office.Interop.Excel;\r\n\r\n// Quicker将会调用的函数\r\npublic static string Exec(string paramValue)\r\n{\r\n\t\r\n\tExcel.Application xlApp = (Excel.Application)Marshal.GetActiveObject(\"Excel.Application\");\r\n\t\r\n\t\r\n\tvar list = new List<string>();\r\n\t\r\n\tlist.Add(((Excel.Worksheet)xlApp.ActiveWorkbook.ActiveSheet).Name);\r\n\t\r\n\tforeach (Worksheet sheet in xlApp.ActiveWorkbook.Worksheets)\r\n\t{\r\n\t\tlist.Add(sheet.Name);\r\n\t}\r\n\r\n\tstring sheets = String.Join(\"\\r\\n\", list);\r\n\t\r\n\t// 不要忘记释放COM对象\r\n\tMarshal.ReleaseComObject(xlApp);\r\n\t\r\n\treturn sheets;\r\n}\r\n"
            },
            "paramValue": {
              "VarKey": null,
              "Value": ""
            },
            "reference": {
              "VarKey": null,
              "Value": "Microsoft.Office.Interop.Excel.dll\r\n"
            },
            "waitResp": {
              "VarKey": null,
              "Value": "1"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            },
            "waitMs": {
              "VarKey": null,
              "Value": "10000"
            }
          },
          "OutputParams": {
            "isSuccess": null,
            "resp": "list"
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:assign",
          "InputParams": {
            "input": {
              "VarKey": null,
              "Value": "$={list}[0]"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "isSuccess": null,
            "output": "activeSheetName"
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:assign",
          "InputParams": {
            "input": {
              "VarKey": null,
              "Value": "$={list}.Skip(1)"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "isSuccess": null,
            "output": "list"
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "隐藏当前工作表名称时，从列表中滤除"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:simpleIf",
      "InputParams": {
        "condition": {
          "VarKey": "hideCurrent",
          "Value": null
        }
      },
      "OutputParams": {},
      "IfSteps": [
        {
          "StepRunnerKey": "sys:assign",
          "InputParams": {
            "input": {
              "VarKey": null,
              "Value": "$={list}.Where(x => x != {activeSheetName})"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "isSuccess": null,
            "output": "list"
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": [],
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "选择工作表"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:if",
      "InputParams": {
        "condition": {
          "VarKey": "useMenu",
          "Value": null
        }
      },
      "OutputParams": {},
      "IfSteps": [
        {
          "StepRunnerKey": "sys:showmenu",
          "InputParams": {
            "menuData": {
              "VarKey": null,
              "Value": "$={list}"
            },
            "fontsize": {
              "VarKey": null,
              "Value": "12"
            },
            "iconsize": {
              "VarKey": null,
              "Value": "16"
            },
            "maxHeight": {
              "VarKey": null,
              "Value": "0"
            },
            "useFocus": {
              "VarKey": null,
              "Value": "0"
            },
            "waitMenuClose": {
              "VarKey": null,
              "Value": "1"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "isSuccess": null,
            "selectedItemData": "worksheet",
            "selectedItem": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": [
        {
          "StepRunnerKey": "sys:select",
          "InputParams": {
            "type": {
              "VarKey": null,
              "Value": "single"
            },
            "prompt": {
              "VarKey": null,
              "Value": "切换工作表"
            },
            "note": {
              "VarKey": null,
              "Value": ""
            },
            "items": {
              "VarKey": "list",
              "Value": null
            },
            "defaultValue": {
              "VarKey": "activeSheetName",
              "Value": null
            },
            "showFilter": {
              "VarKey": null,
              "Value": "1"
            },
            "filterContent": {
              "VarKey": null,
              "Value": ""
            },
            "winLocation": {
              "VarKey": null,
              "Value": "WithMouse1"
            },
            "maxWinSize": {
              "VarKey": null,
              "Value": ""
            },
            "keepLastPos": {
              "VarKey": null,
              "Value": "1"
            },
            "closeOnDeactivated": {
              "VarKey": null,
              "Value": "0"
            },
            "restoreForeground": {
              "VarKey": null,
              "Value": "1"
            },
            "allowOkWhenEmpty": {
              "VarKey": null,
              "Value": "0"
            },
            "enableQuickConfirm": {
              "VarKey": null,
              "Value": "1"
            },
            "stopIfCancel": {
              "VarKey": null,
              "Value": "1"
            },
            "imeState": {
              "VarKey": null,
              "Value": "NO_CONTROL"
            },
            "operations": {
              "VarKey": null,
              "Value": ""
            },
            "fontsize": {
              "VarKey": null,
              "Value": "12"
            },
            "fontfamily": {
              "VarKey": null,
              "Value": ""
            },
            "iconsize": {
              "VarKey": null,
              "Value": "16"
            },
            "autoCloseSeconds": {
              "VarKey": null,
              "Value": "0"
            },
            "noKeyboard": {
              "VarKey": null,
              "Value": "0"
            },
            "windowKey": {
              "VarKey": null,
              "Value": ""
            },
            "help": {
              "VarKey": null,
              "Value": ""
            }
          },
          "OutputParams": {
            "isSuccess": null,
            "textValue": "worksheet",
            "selectedIndex": null,
            "extraOperation": null,
            "selectedFullItems": null,
            "selectedItemTitle": null,
            "filterContent": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "选择工作表"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:if",
      "InputParams": {
        "condition": {
          "VarKey": "isSuccessUsingExcelObj",
          "Value": null
        }
      },
      "OutputParams": {},
      "IfSteps": [
        {
          "StepRunnerKey": "sys:comment",
          "InputParams": {
            "note": {
              "VarKey": null,
              "Value": "高权限模式"
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:excelObjects",
          "InputParams": {
            "operation": {
              "VarKey": null,
              "Value": "SelectWorksheet"
            },
            "workbook": {
              "VarKey": null,
              "Value": ""
            },
            "params": {
              "VarKey": null,
              "Value": "$$name={worksheet}"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "isSuccess": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": [
        {
          "StepRunnerKey": "sys:csscript",
          "InputParams": {
            "mode": {
              "VarKey": null,
              "Value": "low_permission_roslyn"
            },
            "scriptForLp": {
              "VarKey": null,
              "Value": "//.cs  文件类型，便于外部编辑时使用\r\n// 引用必要的命名空间\r\nusing System.Windows.Forms;\r\nusing System.Runtime.InteropServices;\r\nusing Excel = Microsoft.Office.Interop.Excel;\r\nusing Microsoft.Office.Interop.Excel;\r\n\r\n// Quicker将会调用的函数\r\npublic static string Exec(string paramValue)\r\n{\r\n\t\r\n\tExcel.Application xlApp = (Excel.Application)Marshal.GetActiveObject(\"Excel.Application\");\r\n\t\r\n\t\r\n\t((Excel.Worksheet)xlApp.ActiveWorkbook.Sheets[paramValue]).Activate();\r\n\t\r\n\t// 不要忘记释放COM对象\r\n\tMarshal.ReleaseComObject(xlApp);\r\n\t\r\n\treturn \"\";\r\n}\r\n"
            },
            "paramValue": {
              "VarKey": "worksheet",
              "Value": null
            },
            "reference": {
              "VarKey": null,
              "Value": "Microsoft.Office.Interop.Excel.dll\r\n"
            },
            "waitResp": {
              "VarKey": null,
              "Value": "1"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            },
            "waitMs": {
              "VarKey": null,
              "Value": "10000"
            }
          },
          "OutputParams": {
            "isSuccess": null,
            "resp": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```

</details>

***

## 94.Excel区域操作

**功能描述**
> 操作Excel的某个区域或单元格，只能操作通过Quicker打开的excel工作簿

**官方文档**
> https://getquicker.net/KC/Help/Doc/excelrange

**内部名称**
> sys:excelRange

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| range | 区域 | 可以输入区域变量、留空(表示当前选择区域）、used(表示当前工作表的使用区域)或区域范围如A1:E9等，请参考文档。 | (98)对象(Object)-Object |  | False |
| subRange | 限定子范围 | 根据需要，将要操作的目标限定为一个子区域 | (9)选项-Enum（FullArea: 整个区域; FirstRow: 区域内的第一行; FirstColumn: 区域内的第一列; LastRow: 区域内最后一行; LastColumn: 区域内最后一列; ActiveCell: 活动单元格; EntireRow: 整行(包含区域外); EntireColumn: 整列(包含区域外); Rows: 所有行(区域范围内); Columns: 所有列(区域范围内)） | FullArea | True |
| operation | 操作类型 | 操作类型 | (9)选项-Enum（SetValue: 设置值; SetFormula: 设置公式; SetNumberFormat: 设置数值格式; SetCellSize: 行高,列宽; SetStyle: 设置格式; CallMethod: 调用方法; Replace: 替换内容; GetRangeInfo: 获取区域信息） | SetValue | True |
| value | 参数 | 要设置的内容 | (99)任意类型-Any |  | False |
| cellSize | 行高,列宽 | -表示不改变，auto表示自动，数字表示具体值。如auto,auto表示自适应高度和宽度 | (99)任意类型-Any |  | False |
| style | 格式 | 要设置的格式内容。每行一个格式设置，请参考模块文档了解详细参数设置。 | (0)字符串-Text |  | False |
| methods | 方法 | 要调用的方法，每行一个。格式请参考文档。 | (0)字符串-Text |  | False |
| replaceWhat | 查找内容 | 要替换的内容 | (0)字符串-Text |  | True |
| replaceTo | 替换为 | 替换成的内容 | (0)字符串-Text |  | True |
| replaceEscapeWhat | 转义“查找内容” | 替换“查找内容”中的转义字符（\r,\n,\t） | (2)布尔值-Boolean | False | False |
| replaceEscapeTo | 转义“替换为” | 替换“替换为”中的转义字符（\r,\n,\t） | (2)布尔值-Boolean | True | False |
| replaceMatchCase | 区分大小写 |  | (2)布尔值-Boolean | False | False |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| value | 值 | 单元格的值 | (99)任意类型-Any |
| text | 文本 | 单元格的显示文本 | (0)字符串-Text |
| formula | 公式 | 单元格的公式值 | (0)字符串-Text |
| numberFormat | 数值格式 | 单元格数值格式值 | (0)字符串-Text |
| address | 位置引用 | 区域位置范围 | (0)字符串-Text |
| column | 列号 | 左上角单元格从1开始的列数 | (12)数字(整数)-Integer |
| row | 行号 | 左上角单元格从1开始的行数 | (12)数字(整数)-Integer |
| colNum | 列数 | 区域包含的列数 | (12)数字(整数)-Integer |
| rowNum | 行数 | 区域包含的行数 | (12)数字(整数)-Integer |
| style | 格式信息 | 单元格的格式 | (0)字符串-Text |
| range | 区域对象 | Range对象 | (98)对象(Object)-Object |
| sheet | 工作表对象 | WorkSheet对象 | (98)对象(Object)-Object |

</details>
<details>
<summary>范例</summary>

**为区域设置序号**
```json
{
  "Variables": [
    {
      "Key": "row",
      "Type": 12,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:excelRange",
      "InputParams": {
        "range": {
          "VarKey": null,
          "Value": ""
        },
        "subRange": {
          "VarKey": null,
          "Value": "FullArea"
        },
        "operation": {
          "VarKey": null,
          "Value": "GetRangeInfo"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "value": null,
        "text": null,
        "formula": null,
        "numberFormat": null,
        "address": null,
        "column": null,
        "row": "row",
        "colNum": null,
        "rowNum": null,
        "style": null,
        "range": null,
        "sheet": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:excelRange",
      "InputParams": {
        "range": {
          "VarKey": null,
          "Value": ""
        },
        "subRange": {
          "VarKey": null,
          "Value": "FullArea"
        },
        "operation": {
          "VarKey": null,
          "Value": "SetFormula"
        },
        "value": {
          "VarKey": null,
          "Value": "$= \"=row() - \"  + ({row} -1)"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 95.输入法状态

**功能描述**
> 获取或更改当前的输入法中英文状态，避免在发送热键时受影响。

**官方文档**
> https://getquicker.net/KC/Help/Doc/imecontrol

**内部名称**
> sys:imeControl

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| operation | 操作类型 | 要执行的操作。所有操作仅在输入法启用的情况下有效。 | (9)选项-Enum（ENABLE: 切换为中文; DISABLE: 切换为英文; RESTORE: 恢复; GET_STATE: 是否为中文状态？） | GET_STATE | True |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isEnabled | 是否为中文状态 |  | (2)布尔值-Boolean |

</details>
<details>
<summary>范例</summary>

**切换为英文输入法**
```json
{
  "Variables": [],
  "Steps": [
    {
      "StepRunnerKey": "sys:imeControl",
      "InputParams": {
        "operation": {
          "VarKey": null,
          "Value": "DISABLE"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 96.运行C#代码

**功能描述**
> 执行C#代码片段。代码中应包含主函数Exec(stepContext)，请参考文档说明。

**官方文档**
> https://getquicker.net/KC/Help/Doc/csscript

**内部名称**
> sys:csscript

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| mode | 运行模式 | 普通模式：在Quicker进程中执行；低权限模式：在单独的进程中执行，可用于COM操作。 | (9)选项-Enum（normal_roslyn: 普通模式v2 (Roslyn); normal: 普通模式v1 (CodeDOM); low_permission_roslyn: 低权限模式v2 (Roslyn); low_permission: 低权限模式v1 (CodeDOM); generate_assembly: 生成程序集） | normal | True |
| script | 脚本内容 | 要运行的脚本内容 | (0)字符串-Text | //.cs  文件类型，便于外部编辑时使用<br>// 引用必要的命名空间<br>using System.Windows.Forms;<br><br>// Quicker将会调用的函数。可以根据需要修改返回值类型。<br>public static void Exec(Quicker.Public.IStepContext context)<br>{<br>    //var oldValue = context.GetVarValue("varName");  // 读取动作里的变量值<br>    //MessageBox.Show(oldValue as string);<br>    //context.SetVarValue("varName", "从脚本输出的内容。"); // 向变量里输出值<br>    MessageBox.Show("Hello World!");<br>}<br> | True |<br>| scriptForLp | 脚本内容 | 要运行的脚本内容 | (0)字符串-Text | //.cs  文件类型，便于外部编辑时使用<br>// 引用必要的命名空间<br>using System.Windows.Forms;<br><br>// Quicker将会调用的函数<br>public static string Exec(string paramValue)<br>{<br>    System.Windows.Forms.MessageBox.Show("Hello World!");<br>    return "Hello World!";<br>}<br> | True |<br>| scriptForAssembly | 脚本内容 | 要运行的脚本内容 | (0)字符串-Text | //.cs  文件类型，便于外部编辑时使用<br>// 引用必要的命名空间<br>using System.Windows.Forms;<br><br>namespace MyNamespace<br>{<br>    // Quicker将会调用的函数<br>    public static class MyClass<br>    {<br>        public static string Exec(string paramValue)<br>        {<br>            System.Windows.Forms.MessageBox.Show("Hello World!");<br>            return "Hello World!";<br>        }<br>    }<br>}<br> | True |
| paramValue | 参数值 | 传递给Exec的参数 | (0)字符串-Text |  | True |
| reference | 引用DLL库 | 要引用的DLL文件，每行一个。 | (0)字符串-Text |  | False |
| waitResp | 等待返回 | 是否等待脚本返回结果 | (2)布尔值-Boolean | True | False |
| runOnUiThread | 执行线程 | 是否在界面线程上运行代码。如果在脚本中使用了wpf窗口，请选中此项。 | (9)选项-Enum | auto | False |
| enableCache | 允许缓存程序集 | 是否使用缓存的程序集 | (2)布尔值-Boolean | False | False |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |
| waitMs | 最长等待时间(ms) | 最长的等待返回结果的，毫秒数 | (1)数字(小数)-Number | 10000 | True |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| resp | 返回内容 | 脚本执行返回的结果文本 | (0)字符串-Text |
| rtn | 返回内容 | Exec方法的返回值 | (0)字符串-Text |
| rtnAssembly | 程序集对象 | 生成的Assembly对象（已经加载） | (98)对象(Object)-Object |
| assemblyPath | 程序集路径 | 生成的Assembly路径 | (0)字符串-Text |

</details>
<details>
<summary>范例</summary>

**获取SSL证书到期时间**
```json
{
  "Variables": [
    {
      "Key": "domainList",
      "Type": 4,
      "Desc": "",
      "DefaultValue": "getquicker.net\r\nbaidu.com",
      "SaveState": true,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "result",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "domain",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "expireTime",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "port",
      "Type": 12,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "domainWithPort",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:simpleIf",
      "InputParams": {
        "condition": {
          "VarKey": null,
          "Value": "$={quicker_in_param} == \"settings\""
        }
      },
      "OutputParams": {},
      "IfSteps": [
        {
          "StepRunnerKey": "sys:userInput",
          "InputParams": {
            "type": {
              "VarKey": null,
              "Value": "multiline"
            },
            "prompt": {
              "VarKey": null,
              "Value": "请输入域名，每行一个，如：baidu.com"
            },
            "defaultValue": {
              "VarKey": "domainList",
              "Value": null
            },
            "pattern": {
              "VarKey": null,
              "Value": ""
            },
            "isRequired": {
              "VarKey": null,
              "Value": "1"
            },
            "submitWithReturn": {
              "VarKey": null,
              "Value": "0"
            },
            "restoreFocus": {
              "VarKey": null,
              "Value": "1"
            },
            "closeOnDeactivated": {
              "VarKey": null,
              "Value": "0"
            },
            "topMost": {
              "VarKey": null,
              "Value": "0"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            },
            "texttools": {
              "VarKey": null,
              "Value": ""
            },
            "extraSettings": {
              "VarKey": null,
              "Value": ""
            },
            "fontfamily": {
              "VarKey": null,
              "Value": ""
            },
            "fontsize": {
              "VarKey": null,
              "Value": "14"
            },
            "winLocation": {
              "VarKey": null,
              "Value": "CenterScreen"
            },
            "imeState": {
              "VarKey": null,
              "Value": "NO_CONTROL"
            },
            "help": {
              "VarKey": null,
              "Value": ""
            }
          },
          "OutputParams": {
            "isSuccess": null,
            "textValue": "domainList",
            "isEmpty": null,
            "errMessage": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:each",
      "InputParams": {
        "input": {
          "VarKey": "domainList",
          "Value": null
        },
        "useMultiThread": {
          "VarKey": null,
          "Value": "0"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "item": "domainWithPort",
        "count": null,
        "isSuccess": null,
        "errMessage": null
      },
      "IfSteps": [
        {
          "StepRunnerKey": "sys:assign",
          "InputParams": {
            "input": {
              "VarKey": null,
              "Value": ""
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "isSuccess": null,
            "output": "expireTime",
            "errMessage": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:if",
          "InputParams": {
            "condition": {
              "VarKey": null,
              "Value": "$={domainWithPort}.Contains(\":\")"
            }
          },
          "OutputParams": {},
          "IfSteps": [
            {
              "StepRunnerKey": "sys:assign",
              "InputParams": {
                "input": {
                  "VarKey": null,
                  "Value": "$=int.Parse({domainWithPort}.SplitToList(':')[1])"
                },
                "stopIfFail": {
                  "VarKey": null,
                  "Value": "1"
                }
              },
              "OutputParams": {
                "isSuccess": null,
                "output": "port",
                "errMessage": null
              },
              "IfSteps": null,
              "ElseSteps": null,
              "Note": "",
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            },
            {
              "StepRunnerKey": "sys:assign",
              "InputParams": {
                "input": {
                  "VarKey": null,
                  "Value": "$={domainWithPort}.SplitToList(':')[0]"
                },
                "stopIfFail": {
                  "VarKey": null,
                  "Value": "1"
                }
              },
              "OutputParams": {
                "isSuccess": null,
                "output": "domain",
                "errMessage": null
              },
              "IfSteps": null,
              "ElseSteps": null,
              "Note": "",
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            }
          ],
          "ElseSteps": [
            {
              "StepRunnerKey": "sys:assign",
              "InputParams": {
                "input": {
                  "VarKey": "domainWithPort",
                  "Value": null
                },
                "stopIfFail": {
                  "VarKey": null,
                  "Value": "1"
                }
              },
              "OutputParams": {
                "isSuccess": null,
                "output": "domain",
                "errMessage": null
              },
              "IfSteps": null,
              "ElseSteps": null,
              "Note": "",
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            },
            {
              "StepRunnerKey": "sys:assign",
              "InputParams": {
                "input": {
                  "VarKey": null,
                  "Value": "443"
                },
                "stopIfFail": {
                  "VarKey": null,
                  "Value": "1"
                }
              },
              "OutputParams": {
                "isSuccess": null,
                "output": "port",
                "errMessage": null
              },
              "IfSteps": null,
              "ElseSteps": null,
              "Note": "",
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            }
          ],
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:csscript",
          "InputParams": {
            "mode": {
              "VarKey": null,
              "Value": "normal"
            },
            "script": {
              "VarKey": null,
              "Value": "//.cs  文件类型，便于外部编辑时使用\r\n// 引用必要的命名空间\r\nusing System;\r\nusing System.Net.Security;\r\nusing System.Net.Sockets;\r\nusing System.Security.Cryptography.X509Certificates;\r\n\r\n// Quicker将会调用的函数。可以根据需要修改返回值类型。\r\npublic static void Exec(Quicker.Public.IStepContext context)\r\n{\r\n\t//var oldValue = context.GetVarValue(\"varName\");  // 读取动作里的变量值\r\n\t//MessageBox.Show(oldValue as string);\r\n\t//context.SetVarValue(\"varName\", \"从脚本输出的内容。\"); // 向变量里输出值\r\n\t//MessageBox.Show(\"Hello World!\");\r\n\t\r\n\tstring host = (string)context.GetVarValue(\"domain\");\r\n\tint port = (int)(long)context.GetVarValue(\"port\"); // SSL端口通常为443\r\n\tvar client = new TcpClient(host, port);\r\n\tvar sslStream = new SslStream(client.GetStream(), false,\r\n\t                              new RemoteCertificateValidationCallback(ValidateServerCertificate), null);\r\n\r\n\ttry\r\n\t{\r\n\t\tsslStream.AuthenticateAsClient(host);\r\n\t\tvar certificate = sslStream.RemoteCertificate;\r\n\t\tvar x509Certificate = new X509Certificate2(certificate);\r\n\t\t//Console.WriteLine(\"Certificate Expiry Date: \" + x509Certificate.GetExpirationDateString());\r\n\t\tcontext.SetVarValue(\"expireTime\", x509Certificate.GetExpirationDateString());\r\n\t}\r\n\tcatch (Exception e)\r\n\t{\r\n\t\tConsole.WriteLine(e.Message);\r\n\t\t\r\n\t\tcontext.SetVarValue(\"expireTime\", \"Error:\" + e.Message);\r\n\t}\r\n\tfinally\r\n\t{\r\n\t\tsslStream.Close();\r\n\t\tclient.Close();\r\n\t}\r\n\t\r\n\t\r\n}\r\n\r\n\r\n\r\n// 用于SSL验证的回调方法，这里简单通过所有验证\r\npublic static bool ValidateServerCertificate(\r\n\tobject sender,\r\n\tX509Certificate certificate,\r\n\tX509Chain chain,\r\n\tSslPolicyErrors sslPolicyErrors)\r\n{\r\n\treturn true; // 通过所有服务器证书\r\n    }"
            },
            "reference": {
              "VarKey": null,
              "Value": ""
            },
            "runOnUiThread": {
              "VarKey": null,
              "Value": "auto"
            },
            "enableCache": {
              "VarKey": null,
              "Value": "0"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "isSuccess": null,
            "rtn": null,
            "errMessage": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:assign",
          "InputParams": {
            "input": {
              "VarKey": null,
              "Value": "$={result} + {domainWithPort} + \":\\t\" + {expireTime} + \"\\t\" + ((int)(DateTime.Parse({expireTime}) - DateTime.Now).TotalDays) + \"天\" + \"\\r\\n\""
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "isSuccess": null,
            "output": "result",
            "errMessage": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:showText",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "NO_WAIT"
        },
        "text": {
          "VarKey": "result",
          "Value": null
        },
        "title": {
          "VarKey": null,
          "Value": "证书到期时间"
        },
        "autoCloseKey": {
          "VarKey": null,
          "Value": "="
        },
        "topMost": {
          "VarKey": null,
          "Value": "false"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        },
        "operations": {
          "VarKey": null,
          "Value": ""
        },
        "winLocation": {
          "VarKey": null,
          "Value": "CenterScreen"
        },
        "winSize": {
          "VarKey": null,
          "Value": ""
        },
        "fontsize": {
          "VarKey": null,
          "Value": "14"
        },
        "fontfamily": {
          "VarKey": null,
          "Value": ""
        },
        "bgColor": {
          "VarKey": null,
          "Value": ""
        },
        "textColor": {
          "VarKey": null,
          "Value": ""
        },
        "highlight": {
          "VarKey": null,
          "Value": ""
        },
        "autoSaveToState": {
          "VarKey": null,
          "Value": ""
        },
        "enableEscClose": {
          "VarKey": null,
          "Value": "true"
        },
        "closeWhenLostFocus": {
          "VarKey": null,
          "Value": "false"
        },
        "showLineNum": {
          "VarKey": null,
          "Value": "true"
        },
        "autoWrap": {
          "VarKey": null,
          "Value": "true"
        },
        "showBuildInToolbar": {
          "VarKey": null,
          "Value": "true"
        },
        "copyWholeLine": {
          "VarKey": null,
          "Value": "false"
        },
        "caretPosition": {
          "VarKey": null,
          "Value": "0"
        },
        "advancedSettings": {
          "VarKey": null,
          "Value": ""
        },
        "updateIfExists": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "windowHandle": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 97.运行Javascript代码

**功能描述**
> 执行Js代码片段。代码中应包含主函数exec()，请参考文档。

**官方文档**
> https://getquicker.net/KC/Help/Doc/jsscript

**内部名称**
> sys:jsscript

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| script | 脚本内容 | 要运行的脚本内容 | (0)字符串-Text | //.js 主函数 exec()<br>function exec(){<br> var localName = quickerGetVar('text');  // 读取text变量值, (text 是动作里的变量)<br> quickerSetVar<br>'text', 'Hello, ' + localName ); //输出修改后的值到text变量中。<br> return 0; //返回0表示成功。返回其他数字表示失败。<br>}<br> | True |
| allClr | 允许访问.Net程序集 | 是否需要在js代码中访问.Net程序集 | (2)布尔值-Boolean | False | False |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| return | 返回值 | 脚本代码返回的数字值。 | (12)数字(整数)-Integer |

</details>
<details>
<summary>范例</summary>

**将这种格式：3(NH4)2S + Sb2S5 -> 6NH4+ + 2SbS4 3+转换为：3(NH₄)₂S + Sb₂S₅ → 6NH₄⁺ + 2SbS₄³⁺；自动转换元素符号大小写（避免输入时频繁切换大小写字符，在输入后由动作统一处理替换）。**
```json
{
  "Variables": [
    {
      "Key": "origin",
      "Type": 0,
      "Desc": "ASC格式书写的",
      "DefaultValue": "3(NH4)2S + Sb2S5 -> 6NH4+ + 2SbS4 3+",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "result",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "resultHtml",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "元素表",
      "Type": 10,
      "Desc": "",
      "DefaultValue": "氢:H\r\n氦:He\r\n锂:Li\r\n铍:Be\r\n硼:B\r\n碳:C\r\n氮:N\r\n氧:O\r\n氟:F\r\n氖:Ne\r\n钠:Na\r\n镁:Mg\r\n铝:Al\r\n硅:Si\r\n磷:P\r\n硫:S\r\n氯:Cl\r\n氩:Ar\r\n钾:K\r\n钙:Ca\r\n钪:Sc\r\n钛:Ti\r\n钒:V\r\n铬:Cr\r\n锰:Mn\r\n铁:Fe\r\n镍:Ni\r\n铜:Cu\r\n锌:Zn\r\n镓:Ga\r\n锗:Ge\r\n砷:As\r\n硒:Se\r\n溴:Br\r\n氪:Kr\r\n铷:Rb\r\n锶:Sr\r\n钇:Y\r\n锆:Zr\r\n铌:Nb\r\n钼:Mo\r\n锝:Tc\r\n钌:Ru\r\n铑:Rh\r\n钯:Pd\r\n银:Ag\r\n镉:Cd\r\n铟:In\r\n锡:Sn\r\n锑:Sb\r\n碲:Te\r\n碘:I\r\n氙:Xe\r\n铯:Cs\r\n钡:Ba\r\n镧:La\r\n铈:Ce\r\n镨:Pr\r\n钕:Nd\r\n钷:Pm\r\n钐:Sm\r\n铕:Eu\r\n钆:Gd\r\n铽:Tb\r\n镝:Dy\r\n钬:Ho\r\n铒:Er\r\n铥:Tm\r\n镱:Yb\r\n镥:Lu\r\n铪:Hf\r\n钽:Ta\r\n钨:W\r\n铼:Re\r\n锇:Os\r\n铱:Ir\r\n铂:Pt\r\n金:Au\r\n汞:Hg\r\n铊:Tl\r\n铅:Pb\r\n铋:Bi\r\n砹:At\r\n氡:Rn\r\n钫:Fr\r\n镭:Ra\r\n锕:Ac\r\n钍:Th\r\n镤:Pa\r\n铀:U\r\n镎:NP\r\n钚:Pu\r\n镅:Am\r\n锔:Cm\r\n锫:Bk\r\n锎:Cf\r\n锿:Es\r\n镄:Fm\r\n钔:Md\r\n铹:Lr",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "format",
      "Type": 0,
      "Desc": "选择的输出格式",
      "DefaultValue": "unicode",
      "SaveState": true,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "enableReplaceChar",
      "Type": 2,
      "Desc": "自动转换大小写",
      "DefaultValue": "0",
      "SaveState": true,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "动作设置处理"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:simpleIf",
      "InputParams": {
        "condition": {
          "VarKey": null,
          "Value": "$={quicker_in_param} == \"settings\""
        }
      },
      "OutputParams": {},
      "IfSteps": [
        {
          "StepRunnerKey": "sys:form",
          "InputParams": {
            "title": {
              "VarKey": null,
              "Value": "填写表单"
            },
            "formDef": {
              "VarKey": null,
              "Value": "{\"Fields\":[{\"FieldKey\":\"enableReplaceChar\",\"Label\":\"自动转换大小写\",\"HelpText\":\"自动转换化学元素的大小写\",\"HelpLink\":null,\"InputMethod\":6,\"SelectionItems\":\"\",\"IsRequired\":false,\"MinValue\":\"\",\"MaxValue\":\"\",\"Pattern\":\"\",\"MaxLength\":0,\"ImeState\":null,\"TextTools\":\"\",\"VisibleExpression\":\"\"},{\"FieldKey\":\"format\",\"Label\":\"输出格式\",\"HelpText\":\"选择的输出格式\",\"HelpLink\":null,\"InputMethod\":3,\"SelectionItems\":\"Unicode特殊符号（纯文本，支持所有编辑器）|unicode\\r\\nHTML上下标标记（支持word编辑器）|html\",\"IsRequired\":true,\"MinValue\":\"\",\"MaxValue\":\"\",\"Pattern\":\"\",\"MaxLength\":0,\"ImeState\":null,\"TextTools\":\"\",\"VisibleExpression\":\"\"}]}"
            },
            "help": {
              "VarKey": null,
              "Value": ""
            },
            "titleColumnWidth": {
              "VarKey": null,
              "Value": "100"
            },
            "windowWidth": {
              "VarKey": null,
              "Value": "500"
            },
            "restoreFocus": {
              "VarKey": null,
              "Value": "0"
            },
            "topMost": {
              "VarKey": null,
              "Value": "false"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "isSuccess": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:stop",
          "InputParams": {
            "method": {
              "VarKey": null,
              "Value": "default"
            },
            "isError": {
              "VarKey": null,
              "Value": "0"
            },
            "return": {
              "VarKey": null,
              "Value": ""
            },
            "showMessage": {
              "VarKey": null,
              "Value": ""
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:getSelectedText",
      "InputParams": {
        "format": {
          "VarKey": null,
          "Value": "UnicodeText"
        },
        "repeat": {
          "VarKey": null,
          "Value": "0"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "output": "origin",
        "isSuccess": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "转换为unicode符号"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:jsscript",
      "InputParams": {
        "script": {
          "VarKey": null,
          "Value": "\r\nfunction ord(s)\r\n{\r\n    return s.charCodeAt();\r\n}\r\n\r\nfunction chr(i)\r\n{\r\n    return String.fromCharCode(i);\r\n}\r\n\r\nfunction Script(s)\r\n{\r\n    this[\"+\"] = s[0];\r\n    this[\"-\"] = s[1];\r\n    for (var i = 0; i < 10; i++) {\r\n        var c = chr(ord(\"0\") + i)\r\n        this[c] = s[2 + i];\r\n    }\r\n}\r\n\r\nScript.prototype.translate = function(s) {\r\n    var script = this;\r\n    var trans_char = function(c) {\r\n        var t = script[c];\r\n        if (t === undefined)\r\n            t = c;\r\n        return t;\r\n    }\r\n    return s.replace(/./g, trans_char);\r\n}\r\n\r\nvar sup = new Script(\"⁺⁻⁰¹²³⁴⁵⁶⁷⁸⁹\");\r\nvar sub = new Script(\"₊₋₀₁₂₃₄₅₆₇₈₉\");\r\nvar misc = {\r\n    \"->\": \"→\",\r\n    \"=\": \"⇌\",\r\n    \".\": \"·\",\r\n    \"*\": \"·\",\r\n};\r\n\r\nvar _regexp = [\r\n    /([\\]\\)A-Za-z])([0-9]*)([+-]?)/,\r\n    /(\\s+)([0-9]+[+-])/,\r\n    /(->|[=.*])/\r\n];\r\n_regexp = _regexp.map(function(re) { return re.source }).join(\"|\");\r\n_regexp = new RegExp(_regexp, \"g\");\r\n\r\nfunction translate(formula)\r\n{\r\n    var translate_one = function(match, g1, g1a, g1b, g2, g2a, g3)\r\n    {\r\n        if (g1 !== undefined)\r\n            return g1 + sub.translate(g1a) + sup.translate(g1b);\r\n        if (g2 !== undefined)\r\n            return sup.translate(g2a);\r\n        if (g3 !== undefined)\r\n            return misc[g3];\r\n    }\r\n    return formula.replace(_regexp, translate_one);\r\n}\r\n\r\n\r\n// 主函数 exec()\r\nfunction exec(){\r\n var asc = quickerGetVar('origin');  // 读取context变量值, (context 是动作里的变量)\r\n var result = translate(asc);\r\n quickerSetVar('result', result ); //输出修改后的值到name变量中。\r\n return 0; //返回0表示成功。返回其他数字表示失败。\r\n}\r\n"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "return": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:simpleIf",
      "InputParams": {
        "condition": {
          "VarKey": "enableReplaceChar",
          "Value": null
        }
      },
      "OutputParams": {},
      "IfSteps": [
        {
          "StepRunnerKey": "sys:comment",
          "InputParams": {
            "note": {
              "VarKey": null,
              "Value": "除 (C|N|P)o 中的 o，所有字母大写"
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:jsscript",
          "InputParams": {
            "script": {
              "VarKey": null,
              "Value": "//.js 主函数 exec()\r\nfunction exec(){\r\n var input = quickerGetVar('result');  // 读取text变量值, (text 是动作里的变量)\r\n var temp = input.replace(/(?<!C|N|P)o|[abcdefghijklmnpqrstuvwxyz]/g, function(a){\r\n   return a.toUpperCase();})\r\n quickerSetVar('result', temp); //输出修改后的值到text变量中。\r\n return 0; //返回0表示成功。返回其他数字表示失败。\r\n}\r\n"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "isSuccess": null,
            "return": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:comment",
          "InputParams": {
            "note": {
              "VarKey": null,
              "Value": "双字母元素大小写\r\n{元素表} 剔除了 Co No Po"
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:assign",
          "InputParams": {
            "input": {
              "VarKey": null,
              "Value": "$=\r\nvar yuansuList = {元素表}.Values.Cast<string>().Where(s => s.Length > 1).ToList();\r\n\r\nvar text = {result};\r\nforeach(var item in yuansuList){\r\n\ttext = text.Replace(item.ToUpper(), item);\r\n}\r\n\r\nreturn text;"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "isSuccess": null,
            "output": "result"
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "选择输出哪种格式"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:if",
      "InputParams": {
        "condition": {
          "VarKey": null,
          "Value": "$= {format} == \"unicode\""
        }
      },
      "OutputParams": {},
      "IfSteps": [
        {
          "StepRunnerKey": "sys:outputText",
          "InputParams": {
            "content": {
              "VarKey": "result",
              "Value": null
            },
            "method": {
              "VarKey": null,
              "Value": "paste"
            },
            "delayBeforePaste": {
              "VarKey": null,
              "Value": "50"
            },
            "delayAfterPaste": {
              "VarKey": null,
              "Value": "10"
            },
            "appendReturn": {
              "VarKey": null,
              "Value": "0"
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": [
        {
          "StepRunnerKey": "sys:comment",
          "InputParams": {
            "note": {
              "VarKey": null,
              "Value": "使用上下标格式，则替换为html代码，写入剪贴板后粘贴"
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:strReplace",
          "InputParams": {
            "type": {
              "VarKey": null,
              "Value": "batch"
            },
            "input": {
              "VarKey": "result",
              "Value": null
            },
            "batchReplaceData": {
              "VarKey": null,
              "Value": "([⁺⁻⁰¹²³⁴⁵⁶⁷⁸⁹]+)|||<sup>$1</sup>\r\n([₊₋₀₁₂₃₄₅₆₇₈₉]+)|||<sub>$1</sub>"
            },
            "escapeOld": {
              "VarKey": null,
              "Value": "0"
            },
            "replaceEscapes": {
              "VarKey": null,
              "Value": "1"
            },
            "useRegex": {
              "VarKey": null,
              "Value": "1"
            },
            "ignoreCase": {
              "VarKey": null,
              "Value": "0"
            },
            "singleLine": {
              "VarKey": null,
              "Value": "1"
            },
            "multiLine": {
              "VarKey": null,
              "Value": "0"
            }
          },
          "OutputParams": {
            "output": "resultHtml"
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:strReplace",
          "InputParams": {
            "type": {
              "VarKey": null,
              "Value": "batch"
            },
            "input": {
              "VarKey": "resultHtml",
              "Value": null
            },
            "batchReplaceData": {
              "VarKey": null,
              "Value": "⁺|+\r\n⁻|-\r\n⁰|0\r\n¹|1\r\n²|2\r\n³|3\r\n⁴|4\r\n⁵|5\r\n⁶|6\r\n⁷|7\r\n⁸|8\r\n⁹|9\r\n₊|+\r\n₋|-\r\n₀|0\r\n₁|1\r\n₂|2\r\n₃|3\r\n₄|4\r\n₅|5\r\n₆|6\r\n₇|7\r\n₈|8\r\n₉|9"
            },
            "escapeOld": {
              "VarKey": null,
              "Value": "0"
            },
            "replaceEscapes": {
              "VarKey": null,
              "Value": "1"
            },
            "useRegex": {
              "VarKey": null,
              "Value": "0"
            },
            "ignoreCase": {
              "VarKey": null,
              "Value": "0"
            },
            "singleLine": {
              "VarKey": null,
              "Value": "1"
            },
            "multiLine": {
              "VarKey": null,
              "Value": "0"
            }
          },
          "OutputParams": {
            "output": "resultHtml"
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:writeClipboard",
          "InputParams": {
            "type": {
              "VarKey": null,
              "Value": "html"
            },
            "html": {
              "VarKey": "resultHtml",
              "Value": null
            },
            "text": {
              "VarKey": "resultHtml",
              "Value": null
            },
            "successMsg": {
              "VarKey": null,
              "Value": ""
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "isSuccess": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:keyInput",
          "InputParams": {
            "keys": {
              "VarKey": null,
              "Value": "{\"CtrlKeys\":[162],\"Keys\":[86]}"
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "Note": "选择了unicode格式",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 98.运行Python代码

**功能描述**
> 执行Python代码片段。

**官方文档**
> https://getquicker.net/KC/Help/Doc/pythonscript

**内部名称**
> sys:pythonscript

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| script | 脚本内容 | 要运行的脚本内容 | (0)字符串-Text | ##.py <br>quicker.context.SetVarValue<br>'text', 'hello world')<br> | True |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |

</details>
<details>
<summary>范例</summary>

```json
{
  "Variables": [
    {
      "Key": "text",
      "Type": 0,
      "Desc": "默认的文本变量",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": null,
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:pythonscript",
      "InputParams": {
        "script": {
          "VarKey": null,
          "Value": "##.py \r\nquicker.context.SetVarValue('text', 'hello world')\r\n"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:notify",
      "InputParams": {
        "msg": {
          "VarKey": "text",
          "Value": null
        },
        "maxLines": {
          "VarKey": null,
          "Value": "0"
        },
        "type": {
          "VarKey": null,
          "Value": "Info"
        },
        "clickAction": {
          "VarKey": null,
          "Value": ""
        },
        "style": {
          "VarKey": null,
          "Value": "Default"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 99.等待按键

**功能描述**
> 等待用户按下某个按键

**官方文档**
> https://getquicker.net/KC/Help/Doc/waitkeyboard

**内部名称**
> sys:waitKeyboard

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| operation | 操作类型 |  | (9)选项-Enum | waitKeyDown | False |
| waitingKeys | 等待的按键 | 可选，留空表示任意键盘按键。格式请参考文档。 | (0)字符串-Text |  | False |
| modifierKeys | 修饰键 | 可选。逗号分隔的ctrl,shift,alt,win组合。仅用于等待组合快捷键。修饰键不会被拦截。 | (0)字符串-Text |  | False |
| maxWaitSeconds | 最长等待秒数 | 0为永久超时超过等待时间，则结束等待。 | (1)数字(小数)-Number | 0 | True |
| filterEvent | 拦截原始按键事件 | 避免按键输入到窗口中 (仅对键盘按键有效) | (2)布尔值-Boolean | True | False |
| waitKeyUp | 等待按键抬起 | 等待按键抬起后再返回 (仅对键盘按键有效) | (2)布尔值-Boolean | False | False |
| ignoreSimulated | 忽略模拟的按键 | 是否忽略（不检测）模拟的按键消息 | (2)布尔值-Boolean | False | False |
| help | 提示信息 | 等待按键时显示的提示文字 | (0)字符串-Text | 请按键... | False |
| fontfamily | 字体名称 | 可选。设置字体名称。如有多个字体，使用逗号分隔。 | (0)字符串-Text |  | False |
| winLocation | 提示窗口位置 | 在哪里显示提示窗口 | (9)选项-Enum | TopCenter | False |
| mouseThrough | 鼠标穿透 | 鼠标是否可以穿透提示窗口点击下面的内容 | (2)布尔值-Boolean | True | False |
| stopIfFail | 失败后停止动作 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 步骤执行是否成功 | 步骤执行是否成功 | (2)布尔值-Boolean |
| keyCode | 键名 | 按键名，具体请参考模块文档。 | (0)字符串-Text |
| keyValue | 键值 | 按键数值，具体请参考模块文档。 | (12)数字(整数)-Integer |
| holdTimeMs | 按下保持时间 | 按下保持时间，单位毫秒。仅支持键盘按键。 | (12)数字(整数)-Integer |

</details>
<details>
<summary>范例</summary>

**按下按键后显示键名和键值。按Esc退出**
```json
{
  "Variables": [
    {
      "Key": "keyValue",
      "Type": 1,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": null,
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "keyName",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": null,
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:repeat",
      "InputParams": {
        "count": {
          "VarKey": null,
          "Value": "-1"
        },
        "stopCondition": {
          "VarKey": null,
          "Value": "$${keyValue} == 27"
        }
      },
      "OutputParams": {
        "count": null
      },
      "IfSteps": [
        {
          "StepRunnerKey": "sys:waitKeyboard",
          "InputParams": {
            "help": {
              "VarKey": null,
              "Value": "请按键...\r\nA：执行A功能，B：执行B功能。\r\nEsc退出。\r\n"
            }
          },
          "OutputParams": {
            "keyCode": "keyName",
            "keyValue": "keyValue"
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:notify",
          "InputParams": {
            "msg": {
              "VarKey": null,
              "Value": "$${keyName}  --- {keyValue}"
            },
            "type": {
              "VarKey": null,
              "Value": "Info"
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 100.窗口界面控制(FlaUI)

**功能描述**
> 触发Windows窗口的菜单/按钮等控件(通过FlaUI库实现)。

**官方文档**
> https://getquicker.net/KC/Help/Doc/uiautomation

**内部名称**
> sys:flauiautomation

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| type | 操作类型 | 操作类型。按下和抬起需要配对使用。 | (9)选项-Enum（TriggerMenu: 触发窗口菜单; TriggerControl: 触发窗口控件; GetControlInfo: 获取窗口控件信息; GetCursorPointControlInfo: 获取鼠标指针位置控件信息; GetControlInfoByPosition: 获取指定位置控件信息; GetFocusedControlInfo: 获取焦点控件信息） | TriggerMenu | False |
| window | 窗口句柄 | 要操作哪个窗口的控件。不填写=使用前台窗口；或窗口句柄数字。 | (0)字符串-Text |  | False |
| menuPath | 菜单路径 | 菜单的展开路径。每行写一个级别的菜单名（需完全匹配） | (0)字符串-Text |  | False |
| expandDelay | 展开延时 | 等待下级菜单展开的时间(ms) | (12)数字(整数)-Integer | 200 | False |
| control | 控件XPath或Name | 控件的XPath或Name。XPath以/开始。 | (0)字符串-Text |  | False |
| controlType | 控件类型 | 可选。当有多个名称相同但类型不同的控件时区分。 | (9)选项-Enum | 0 | False |
| controlOperation | 动作 | 对控件执行的操作。 | (9)选项-Enum（Auto: 自动; Invoke: 调用（按钮、菜单项等）; LeftClick: 鼠标左键单击; MiddleClick: 鼠标中键单击; RightClick: 鼠标右键单击; LeftDoubleClick: 鼠标左键双击; Select: 单选：选择（单选框、标签页等）; AddToSelection: 多选：添加到多选（多选列表等）; RemoveFromSelection: 多选：从多选中移除（多选列表）; ToggleItemSelection: 多选：切换选中状态; Expand: 展开折叠：展开（菜单等）; Collapse: 展开折叠：折叠（菜单等）; ToggleExpandCollapse: 展开折叠：切换展开折叠（菜单等）; Toggle: 切换：切换（检查框等）; ToggleOn: 切换：开（检查框等）; ToggleOff: 切换：关（检查框等）; SetValue: 设置值） | Auto | False |
| value | 值 | 仅用于 “设置值” 操作。 | (0)字符串-Text |  | False |
| pointLocation | 坐标位置 | 指定要检查的控件的屏幕坐标位置，格式为“x,y” | (0)字符串-Text |  | False |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| value | 值 | 控件的值 | (0)字符串-Text |
| controlText | 文本 | 获取控件上的文本。根据控件不同，可能从Value、Text、Name等信息获取。 | (0)字符串-Text |
| rect | 位置 | 控件坐标位置 | (0)字符串-Text |
| controlName | 控件名称 |  | (0)字符串-Text |
| controlType | 控件类型 |  | (0)字符串-Text |
| controlXPath | 控件XPath |  | (0)字符串-Text |
| controlTypeId | 控件类型ID |  | (12)数字(整数)-Integer |
| controlInfo | 其他信息 |  | (10)词典-Dict |
| controlIsEnabled | 是否启用 | 控件未处于禁用状态 | (2)布尔值-Boolean |
| controlIsVisible | 是否可见 | 控件是否在屏幕上。 | (2)布尔值-Boolean |
| element | 原始对象 | 返回控件的AutomationElement对象 | (98)对象(Object)-Object |

</details>
<details>
<summary>范例</summary>

```json
{
  "Variables": [
    {
      "Key": "坐标",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "控件文本",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "控件名称",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "控件类型",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "选项",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "菜单",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "菜单列表",
      "Type": 4,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "controlXPath",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "XP",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "专业版",
      "Type": 2,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:mouse",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "getMouseCurrentPosition"
        }
      },
      "OutputParams": {
        "mouseLocation": "坐标",
        "mouseX": null,
        "mouseY": null,
        "cursorType": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:getSysInfo",
      "InputParams": {},
      "OutputParams": {
        "MachineName": null,
        "userName": null,
        "userDomainName": null,
        "OsVersion": null,
        "isWin10": null,
        "isWin11": null,
        "isAutoRun": null,
        "startupSeconds": null,
        "isLocked": null,
        "sysEnv": null,
        "primaryScreenRes": null,
        "isFullscreen": null,
        "isNetworkConnected": null,
        "lanIp": null,
        "quickerVersion": null,
        "isPro": "专业版",
        "unionId": null,
        "hasBaiduAccount": null,
        "runnedSeconds": null,
        "actionId": null,
        "actionName": null,
        "sharedActionId": null,
        "sharedActionRevision": null,
        "actionCount": null,
        "isDebugging": null,
        "trigger": null,
        "textParam": null,
        "imageParam": null,
        "isWinInDarkMode": null,
        "quickerThemeMode": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:uiautomation",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "GetCursorPointControlInfo"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "value": null,
        "controlText": "控件文本",
        "rect": null,
        "controlName": "控件名称",
        "controlType": "控件类型",
        "controlIsEnabled": null,
        "controlIsVisible": null,
        "controlNativeWindowHandle": null,
        "controlTypeId": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:flauiautomation",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "GetControlInfoByPosition"
        },
        "pointLocation": {
          "VarKey": "坐标",
          "Value": null
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "value": null,
        "controlText": null,
        "rect": null,
        "controlName": null,
        "controlType": null,
        "controlXPath": "controlXPath",
        "controlTypeId": null,
        "controlInfo": null,
        "controlIsEnabled": null,
        "controlIsVisible": null,
        "element": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:stringProcess",
      "InputParams": {
        "data": {
          "VarKey": "controlXPath",
          "Value": null
        },
        "method": {
          "VarKey": null,
          "Value": "substring"
        },
        "start": {
          "VarKey": null,
          "Value": "-30"
        },
        "length": {
          "VarKey": null,
          "Value": "0"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "output": "XP",
        "isSuccess": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:simpleIf",
      "InputParams": {
        "condition": {
          "VarKey": null,
          "Value": "$={控件名称} == \"\" || {控件文本} == \"\""
        }
      },
      "OutputParams": {},
      "IfSteps": [
        {
          "StepRunnerKey": "sys:flauiautomation",
          "InputParams": {
            "type": {
              "VarKey": null,
              "Value": "GetControlInfo"
            },
            "window": {
              "VarKey": null,
              "Value": ""
            },
            "control": {
              "VarKey": "controlXPath",
              "Value": null
            },
            "controlType": {
              "VarKey": null,
              "Value": "0"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "0"
            }
          },
          "OutputParams": {
            "isSuccess": null,
            "value": null,
            "controlText": "控件文本",
            "rect": null,
            "controlName": "控件名称",
            "controlType": null,
            "controlXPath": null,
            "controlTypeId": null,
            "controlInfo": null,
            "controlIsEnabled": null,
            "controlIsVisible": null,
            "element": null,
            "errMessage": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": [],
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:if",
      "InputParams": {
        "condition": {
          "VarKey": "专业版",
          "Value": null
        }
      },
      "OutputParams": {},
      "IfSteps": [
        {
          "StepRunnerKey": "sys:splitString",
          "InputParams": {
            "data": {
              "VarKey": null,
              "Value": "$${控件文本}\r\n{控件名称}\r\n类型：{控件类型}\r\n路径: ...{XP}({controlXPath})|{controlXPath}"
            },
            "separator": {
              "VarKey": null,
              "Value": "\\r\\n"
            },
            "escapeSeparator": {
              "VarKey": null,
              "Value": "1"
            },
            "multiSeparator": {
              "VarKey": null,
              "Value": "0"
            },
            "removeEmpty": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "output": "菜单列表"
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": [
        {
          "StepRunnerKey": "sys:splitString",
          "InputParams": {
            "data": {
              "VarKey": null,
              "Value": "$${控件文本}\r\n{控件名称}\r\n类型：{控件类型}"
            },
            "separator": {
              "VarKey": null,
              "Value": "\\r\\n"
            },
            "escapeSeparator": {
              "VarKey": null,
              "Value": "1"
            },
            "multiSeparator": {
              "VarKey": null,
              "Value": "0"
            },
            "removeEmpty": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "output": "菜单列表"
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "Note": "",
      "Disabled": false,
      "Collapsed": true,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:listOperations",
      "InputParams": {
        "list": {
          "VarKey": "菜单列表",
          "Value": null
        },
        "type": {
          "VarKey": null,
          "Value": "distinct"
        }
      },
      "OutputParams": {
        "value": "菜单",
        "isEmpty": null,
        "length": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:showmenu",
      "InputParams": {
        "menuData": {
          "VarKey": "菜单",
          "Value": null
        },
        "fontsize": {
          "VarKey": null,
          "Value": "12"
        },
        "iconsize": {
          "VarKey": null,
          "Value": "16"
        },
        "maxHeight": {
          "VarKey": null,
          "Value": "0"
        },
        "useFocus": {
          "VarKey": null,
          "Value": "0"
        },
        "waitMenuClose": {
          "VarKey": null,
          "Value": "1"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "selectedItemData": "选项",
        "selectedItem": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:strReplace",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "batch"
        },
        "input": {
          "VarKey": "选项",
          "Value": null
        },
        "batchReplaceData": {
          "VarKey": null,
          "Value": "C:\\|\r\nD:\\|\r\nE:\\|\r\nF:\\|\r\nG\\|\r\nH:\\|\r\nI:\\|"
        },
        "escapeOld": {
          "VarKey": null,
          "Value": "false"
        },
        "replaceEscapes": {
          "VarKey": null,
          "Value": "true"
        },
        "useRegex": {
          "VarKey": null,
          "Value": "false"
        },
        "ignoreCase": {
          "VarKey": null,
          "Value": "false"
        },
        "singleLine": {
          "VarKey": null,
          "Value": "true"
        },
        "multiLine": {
          "VarKey": null,
          "Value": "false"
        }
      },
      "OutputParams": {
        "output": "选项"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:writeClipboard",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "auto"
        },
        "input": {
          "VarKey": "选项",
          "Value": null
        },
        "successMsg": {
          "VarKey": null,
          "Value": "$$已复制：\r\n{选项}"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```

</details>

***

## 101.按键操作

**功能描述**
> 单个键盘按键的操作控制或状态获取

**官方文档**
> https://getquicker.net/KC/Help/Doc/keyoperation

**内部名称**
> sys:keyoperation

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| type | 类型 | 操作类型。按下和抬起需要配对使用。 | (9)选项-Enum（get_key_state: 获取按键状态; key_down: 按下按键; key_up: 抬起按键; key_keydown_v1: 按下Quicker虚拟键V1; key_keyup_v1: 抬起Quicker虚拟键V1） | get_key_state | False |
| key | 按键 | 要操作或检查状态的按键(单个)。可以为键值或键名，具体请参考文档。 | (0)字符串-Text |  | False |
| getRealMouseState | 获取按键的实际状态（在远程时无法获取） |  | (2)布尔值-Boolean | False | False |
| keepMs | 保持按下时间 | 保持此虚拟键按下的时间（毫秒数），之后会自动抬起。 | (12)数字(整数)-Integer | 1000 | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isDown | 是否按下 | 此按键是否为按下状态 | (2)布尔值-Boolean |
| isToggled | 是否锁定 | 此按键是否为锁定状态，仅对CapsLock、NumLock等按键有效。 | (2)布尔值-Boolean |

</details>
<details>
<summary>范例</summary>

**判断W是否按下，如未按下则按下1500毫秒然后松开**
```json
{
  "Variables": [
    {
      "Key": "isDown",
      "Type": 2,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:keyoperation",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "get_key_state"
        },
        "key": {
          "VarKey": null,
          "Value": "W"
        },
        "getRealMouseState": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {
        "isDown": "isDown",
        "isToggled": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:simpleIf",
      "InputParams": {
        "condition": {
          "VarKey": null,
          "Value": "$=!{isDown}"
        }
      },
      "OutputParams": {},
      "IfSteps": [
        {
          "StepRunnerKey": "sys:keyoperation",
          "InputParams": {
            "type": {
              "VarKey": null,
              "Value": "key_down"
            },
            "key": {
              "VarKey": null,
              "Value": "W"
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:delay",
          "InputParams": {
            "delayMs": {
              "VarKey": null,
              "Value": "1500"
            },
            "monitorWaitWin": {
              "VarKey": null,
              "Value": "0"
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:keyoperation",
          "InputParams": {
            "type": {
              "VarKey": null,
              "Value": "key_up"
            },
            "key": {
              "VarKey": null,
              "Value": "W"
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": [],
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```

</details>

***

## 102.窗口界面控制

**功能描述**
> 触发Windows窗口的菜单/按钮等控件。

**官方文档**
> https://getquicker.net/KC/Help/Doc/uiautomation

**内部名称**
> sys:uiautomation

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| type | 操作类型 | 操作类型。按下和抬起需要配对使用。 | (9)选项-Enum（TriggerMenu: 触发窗口菜单; TriggerControl: 触发窗口控件; GetControlInfo: 获取窗口控件信息; GetCursorPointControlInfo: 获取鼠标指针位置控件信息; GetFocusedControlInfo: 获取焦点控件信息; GetControlInfoByPosition: 获取指定位置控件信息; UpdateSaveAsDialogPath） | TriggerMenu | False |
| window | 窗口句柄 | 要操作哪个窗口的控件。不填写=使用前台窗口；或窗口句柄数字。 | (0)字符串-Text |  | False |
| menuPath | 菜单路径 | 菜单的展开路径。每行写一个级别的菜单名（需完全匹配） | (0)字符串-Text |  | False |
| expandDelay | 展开延时 | 等待下级菜单展开的时间(ms) | (12)数字(整数)-Integer | 200 | False |
| control | 控件名 | 控件名，请确保唯一性。 | (0)字符串-Text |  | False |
| controlType | 控件类型 | 可选。当有多个名称相同但类型不同的控件时区分。 | (9)选项-Enum | 0 | False |
| controlOperation | 动作 | 对控件执行的操作。 | (9)选项-Enum（Auto: 自动; Invoke: 调用（按钮、菜单项等）; LeftClick: 鼠标左键单击; MiddleClick: 鼠标中键单击; RightClick: 鼠标右键单击; LeftDoubleClick: 鼠标左键双击; Select: 单选：选择（单选框、标签页等）; AddToSelection: 多选：添加到多选（多选列表等）; RemoveFromSelection: 多选：从多选中移除（多选列表）; ToggleItemSelection: 多选：切换选中状态; Expand: 展开折叠：展开（菜单等）; Collapse: 展开折叠：折叠（菜单等）; ToggleExpandCollapse: 展开折叠：切换展开折叠（菜单等）; Toggle: 切换：切换（检查框等）; ToggleOn: 切换：开（检查框等）; ToggleOff: 切换：关（检查框等）; SetValue: 设置值） | Auto | False |
| value | 值 | 仅用于 “设置值” 操作。 | (0)字符串-Text |  | False |
| path | 路径 | 要更新的路径 | (0)字符串-Text |  | False |
| autoCreateDir | 自动创建文件夹 | 如果目录不存在则自动创建。 | (9)选项-Enum（no: 不自动创建; auto: 自动创建：自动（根据后缀自动判断路径为文件还是文件夹路径）; asFilePath: 自动创建：给定文件路径; asFolderPath: 自动创建：给定文件夹路径） | no | False |
| pointLocation | 坐标位置 | 指定要检查的控件的屏幕坐标位置，格式为“x,y” | (0)字符串-Text |  | False |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| value | 值 | 控件的值 | (0)字符串-Text |
| controlText | 文本 | 获取控件上的文本。根据控件不同，可能从Value、Text、Name等信息获取。 | (0)字符串-Text |
| rect | 位置 | 控件坐标位置 | (0)字符串-Text |
| controlName | 控件名称 |  | (0)字符串-Text |
| controlType | 控件类型 |  | (0)字符串-Text |
| controlIsEnabled | 是否启用 | 控件未处于禁用状态 | (2)布尔值-Boolean |
| controlIsVisible | 是否可见 | 控件是否在屏幕上。 | (2)布尔值-Boolean |
| controlNativeWindowHandle | 原始句柄 | 控件的原始窗口句柄(NativeWindowHandle) | (12)数字(整数)-Integer |
| controlTypeId | 控件类型ID |  | (12)数字(整数)-Integer |

</details>
<details>
<summary>范例</summary>

**资源管理器里切换到超大图标视图**
```json
{
  "Variables": [],
  "Steps": [
    {
      "StepRunnerKey": "sys:uiautomation",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "TriggerControl"
        },
        "window": {
          "VarKey": null,
          "Value": ""
        },
        "control": {
          "VarKey": null,
          "Value": "查看"
        },
        "controlType": {
          "VarKey": null,
          "Value": "0"
        },
        "controlOperation": {
          "VarKey": null,
          "Value": "Auto"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "切换到“查看”标签页",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:uiautomation",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "TriggerControl"
        },
        "window": {
          "VarKey": null,
          "Value": ""
        },
        "control": {
          "VarKey": null,
          "Value": "超大图标"
        },
        "controlType": {
          "VarKey": null,
          "Value": "0"
        },
        "controlOperation": {
          "VarKey": null,
          "Value": "Auto"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "点击“超大图标”视图类型",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```

**切换Win10的蓝牙开关**
```json
{
  "Variables": [],
  "Steps": [
    {
      "StepRunnerKey": "sys:run",
      "InputParams": {
        "path": {
          "VarKey": null,
          "Value": "ms-settings:"
        },
        "arg": {
          "VarKey": null,
          "Value": ""
        },
        "setWorkingDir": {
          "VarKey": null,
          "Value": ""
        },
        "windowStyle": {
          "VarKey": null,
          "Value": "0"
        },
        "runas": {
          "VarKey": null,
          "Value": "0"
        },
        "waitInputIdle": {
          "VarKey": null,
          "Value": "0"
        },
        "waitExit": {
          "VarKey": null,
          "Value": "0"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        },
        "alternativePath": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "pid": null,
        "mainWinHandle": null,
        "mainWinTitle": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:delay",
      "InputParams": {
        "delayMs": {
          "VarKey": null,
          "Value": "500"
        },
        "monitorWaitWin": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:uiautomation",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "TriggerControl"
        },
        "window": {
          "VarKey": null,
          "Value": ""
        },
        "control": {
          "VarKey": null,
          "Value": "设备"
        },
        "controlType": {
          "VarKey": null,
          "Value": "0"
        },
        "controlOperation": {
          "VarKey": null,
          "Value": "Auto"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:delay",
      "InputParams": {
        "delayMs": {
          "VarKey": null,
          "Value": "100"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": null,
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:uiautomation",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "TriggerControl"
        },
        "window": {
          "VarKey": null,
          "Value": ""
        },
        "control": {
          "VarKey": null,
          "Value": "蓝牙和其他设备"
        },
        "controlType": {
          "VarKey": null,
          "Value": "0"
        },
        "controlOperation": {
          "VarKey": null,
          "Value": "Auto"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:delay",
      "InputParams": {
        "delayMs": {
          "VarKey": null,
          "Value": "100"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": null,
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:uiautomation",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "TriggerControl"
        },
        "window": {
          "VarKey": null,
          "Value": ""
        },
        "control": {
          "VarKey": null,
          "Value": "蓝牙"
        },
        "controlType": {
          "VarKey": null,
          "Value": "0"
        },
        "controlOperation": {
          "VarKey": null,
          "Value": "Auto"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```

</details>

***

## 103.获取字符信息

**功能描述**
> 获取字符信息

**官方文档**
> https://getquicker.net/KC/Help/Doc/charInfo

**内部名称**
> sys:charInfo

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| char | 字符 | 要获取编码的字符，如果是多个字符，则取第一个。 | (0)字符串-Text | 中 | True |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| unicodeNum | Unicode编码(数字) | 字符的Unicode编码数字 | (12)数字(整数)-Integer |
| unicodeHex | Unicode编码(十六进制) | 字符的Unicode编码数字的十六进制，如“中”的Unicode编码十六进制为“4E2D” | (0)字符串-Text |
| pinyinFirstChar | 拼音首字母 | 字母的拼音首字母(仅第一个常用读音) | (0)字符串-Text |
| pinyin | 拼音 | 字母的拼音(多音字只输出第一个常用读音) | (0)字符串-Text |
| pinyinFirstCharAll | 拼音首字母(全部) | 字母的拼音首字母(多音字输出所有读音) | (0)字符串-Text |
| pinyinAll | 拼音(全部) | 字母的拼音(多音字输出所有读音，空格分隔) | (0)字符串-Text |

</details>
<details>
<summary>范例</summary>

```json
{
  "Variables": [
    {
      "Key": "pinyinFirstChar",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "pinyin",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:charInfo",
      "InputParams": {
        "char": {
          "VarKey": null,
          "Value": "中"
        }
      },
      "OutputParams": {
        "unicodeNum": null,
        "unicodeHex": null,
        "pinyinFirstChar": "pinyinFirstChar",
        "pinyin": "pinyin",
        "pinyinFirstCharAll": null,
        "pinyinAll": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 104.组合成文本

**功能描述**
> 将（多个）变量组合成一段文本。

**官方文档**
> https://getquicker.net/KC/Help/Doc/formatstring

**内部名称**
> sys:formatString

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| formatString | 格式化字符串 | 使用C#的String.Format语法。 | (0)字符串-Text | {0} | True |
| p0 | 参数0 | 第 0 个参数 | (99)任意类型-Any |  | False |
| p1 | 参数1 | 第 1 个参数 | (99)任意类型-Any |  | False |
| p2 | 参数2 | 第 2 个参数 | (99)任意类型-Any |  | False |
| p3 | 参数3 | 第 3 个参数 | (99)任意类型-Any |  | False |
| p4 | 参数4 | 第 4 个参数 | (99)任意类型-Any |  | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| output | 结果 | 生成的文本内容 | (0)字符串-Text |

</details>
<details>
<summary>范例</summary>

**数字变量进行格式化处理，输出为文本**
```json
{
  "Variables": [
    {
      "Key": "context",
      "Type": 0,
      "Desc": "默认的文本变量",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": null,
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "number",
      "Type": 1,
      "Desc": "",
      "DefaultValue": "12345.6789",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": null,
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:formatString",
      "InputParams": {
        "formatString": {
          "VarKey": null,
          "Value": "提示：请查看动作定义了解使用方法\r\n组合成文本模块的说明：https://www.yuque.com/quicker/help/formatstring\r\n\r\n默认格式: {0}\r\n\r\n--- 标准格式---\r\n参考网址：https://docs.microsoft.com/zh-cn/dotnet/standard/base-types/standard-numeric-format-strings\r\n货币格式C: C=> {0:C}   C2=> {0:C2}  C4=> {0:C4}\r\n十进制D 不支持（Quicker中的数字为decimal类型，d只适合于int类型）\r\n指数E: E=> {0:E}  E2=> {0:E2}\r\n定点F: F=> {0:F}  F2=> {0:F2}\r\n常规G: G=> {0:G}  G2=> {0:G2}\r\n数字N: N=> {0:N}  N2=> {0:N2}\r\n百分比P:P=> {0:P}  P1=> {0:P1} P2=> {0:P2} P3=> {0:P3}\r\n十六进制X:不支持\r\n\r\n---自定义格式---\r\n参考网址：https://docs.microsoft.com/zh-cn/dotnet/standard/base-types/custom-numeric-format-strings\r\n0 零占位符，用对应的数字（如果存在）替换零；否则，将在结果字符串中显示零。\r\n  00000000.000000 => {0:00000000.000000}\r\n# 数字占位符：用对应的数字（如果存在）替换“#”符号；否则，不会在结果字符串中显示任何数字。\r\n  ##### => {0:#####}    #.## => {0:#.##}\r\n. 确定小数点分隔符在结果字符串中的位置。\r\n  0.00 => {0:0.00}\r\n% 百分比占位符\t将数字乘以 100，并在结果字符串中插入本地化的百分比符号。\r\n  ##.0% => {0:##.0%}  ##,#.0%=>{0:##,#.0%}\r\n\r\n\r\n  "
        },
        "p0": {
          "VarKey": "number",
          "Value": null
        },
        "p1": {
          "VarKey": null,
          "Value": ""
        },
        "p2": {
          "VarKey": null,
          "Value": ""
        },
        "p3": {
          "VarKey": null,
          "Value": ""
        },
        "p4": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {
        "output": "context"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:showText",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "NO_WAIT"
        },
        "text": {
          "VarKey": "context",
          "Value": null
        },
        "title": {
          "VarKey": null,
          "Value": "结果内容"
        },
        "operations": {
          "VarKey": null,
          "Value": ""
        },
        "winLocation": {
          "VarKey": null,
          "Value": "CenterScreen"
        },
        "fontsize": {
          "VarKey": null,
          "Value": "14"
        },
        "fontfamily": {
          "VarKey": null,
          "Value": "Consolas"
        }
      },
      "OutputParams": {
        "selectedOperation": null,
        "resultText": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```

**将数字转换为选择的格式；可以根据需要添加更多的格式转换，请参考c# 数字格式化为字符串的文档**
```json
{
  "Variables": [
    {
      "Key": "context",
      "Type": 0,
      "Desc": "默认的文本变量",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": null,
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "num",
      "Type": 1,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": null,
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:getSelectedText",
      "InputParams": {
        "format": {
          "VarKey": null,
          "Value": "UnicodeText"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "output": "context",
        "isSuccess": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": null,
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:compute",
      "InputParams": {
        "expression": {
          "VarKey": null,
          "Value": "$${context}"
        }
      },
      "OutputParams": {
        "output": "num"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": null,
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:formatString",
      "InputParams": {
        "formatString": {
          "VarKey": null,
          "Value": "{0:N}\r\n{0:C}\r\n{0:P}\r\n{0:.00‰}\r\n{0:00.00}"
        },
        "p0": {
          "VarKey": "num",
          "Value": null
        },
        "p1": {
          "VarKey": null,
          "Value": ""
        },
        "p2": {
          "VarKey": null,
          "Value": ""
        },
        "p3": {
          "VarKey": null,
          "Value": ""
        },
        "p4": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {
        "output": "context"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": null,
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:select",
      "InputParams": {
        "prompt": {
          "VarKey": null,
          "Value": "请选择格式"
        },
        "items": {
          "VarKey": null,
          "Value": "$${context}"
        },
        "defaultValue": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {
        "textValue": "context"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": null,
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:outputText",
      "InputParams": {
        "content": {
          "VarKey": "context",
          "Value": null
        },
        "method": {
          "VarKey": null,
          "Value": "input"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": null,
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```

</details>

***

## 105.提取HTML内容

**功能描述**
> 从HTML代码中提取内容

**官方文档**
> https://getquicker.net/KC/Help/Doc/htmlextract

**内部名称**
> sys:htmlExtract

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| operation | 操作类型 |  | (9)选项-Enum（extractText: 读取文本内容; extractText: 读取表格内容）| extractText | False |
| source | 源HTML | 原始HTML内容，或网址，或根节点对象 | (0)字符串-Text（auto: 自动检测 (加载两次); gb2312: GB2312编码; utf-8: UTF8编码） |  | True |
| encoding | 网页编码类型 | 通过网址加载内容时，使用指定的编码。留空时默认为UTF8。 | (0)字符串-Text |  | False |
| xpath | 节点XPath | 内容的XPath，详细说明请参考文档 | (0)字符串-Text |  | True |
| selectTarget | 提取方式 | 提取单个节点还是符合条件的所有节点。 | (9)选项-Enum（single: 第一个符合条件的节点; all: 所有符合条件的节点） | single | False |
| returnType | 提取内容类型 | 要提取的节点信息。 | (9)选项-Enum（InnerHtml: innerHtml 内部HTML; InnerText: innerText 内部文本; OuterHtml: outerHTML 节点全部HTML; Attribute: Attribute 节点的某个属性; Node: 节点对象） | InnerHtml | False |
| attribute | 属性名称 | 仅在提取节点属性时有效。指定属性的名称。 | (0)字符串-Text |  | False |
| writeToSheet | 写入工作表对象 | 将提取到的表格内容写入工作表对象中。 | (98)对象(Object)-Object |  | False |
| stopIfFail | 失败后停止动作 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 步骤执行是否成功 | 步骤执行是否成功 | (2)布尔值-Boolean |
| value | 提取值 | 提取的内容。请确保结果类型和变量类型匹配。 | (99)任意类型-Any |
| rootNode | 根节点 | 整个HTML源内容对应的HtmlNode节点对象，可用于后续处理使用。 | (99)任意类型-Any |

</details>
<details>
<summary>范例</summary>

**将指定网址生成markdown，并写入剪贴板**
```json
{
  "Variables": [
    {
      "Key": "markdown",
      "Type": 0,
      "Desc": "生成的markdown内容",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "title",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "url",
      "Type": 0,
      "Desc": "网址",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "html",
      "Type": 0,
      "Desc": "html内容",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "description",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "获取网页HTML内容"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:http",
      "InputParams": {
        "url": {
          "VarKey": "url",
          "Value": null
        },
        "method": {
          "VarKey": null,
          "Value": "GET"
        },
        "header": {
          "VarKey": null,
          "Value": ""
        },
        "cookie": {
          "VarKey": null,
          "Value": ""
        },
        "resultType": {
          "VarKey": null,
          "Value": "Text"
        },
        "ua": {
          "VarKey": null,
          "Value": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.113 Safari/537.36"
        },
        "expireSeconds": {
          "VarKey": null,
          "Value": "100"
        },
        "noAutoRedirect": {
          "VarKey": null,
          "Value": "0"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "statusCode": null,
        "respHeaders": null,
        "respCookies": null,
        "content": "html",
        "imgResult": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "提取网页的Title和Description"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:htmlExtract",
      "InputParams": {
        "source": {
          "VarKey": "html",
          "Value": null
        },
        "xpath": {
          "VarKey": null,
          "Value": "html/head/title"
        },
        "selectTarget": {
          "VarKey": null,
          "Value": "single"
        },
        "returnType": {
          "VarKey": null,
          "Value": "InnerText"
        },
        "attribute": {
          "VarKey": null,
          "Value": ""
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "value": "title"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "提取标题",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:htmlExtract",
      "InputParams": {
        "source": {
          "VarKey": "html",
          "Value": null
        },
        "xpath": {
          "VarKey": null,
          "Value": "//meta[@name='description']"
        },
        "selectTarget": {
          "VarKey": null,
          "Value": "single"
        },
        "returnType": {
          "VarKey": null,
          "Value": "Attribute"
        },
        "attribute": {
          "VarKey": null,
          "Value": "content"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "value": "description"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "提取description",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "拼接为MarkDown链接，写入剪贴板"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:assign",
      "InputParams": {
        "input": {
          "VarKey": null,
          "Value": "$$[{title}]({url} '{description}')"
        }
      },
      "OutputParams": {
        "output": "markdown"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:writeClipboard",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "text"
        },
        "text": {
          "VarKey": "markdown",
          "Value": null
        },
        "successMsg": {
          "VarKey": null,
          "Value": "$$已写入剪贴板：\r\n{markdown}"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 106.列表合并成文本

**功能描述**
> 将列表拼接为一段文本

**官方文档**
> https://getquicker.net/KC/Help/Doc/joinlist

**内部名称**
> sys:joinList

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| list | 输入 | 要拼接为文本的列表 | (4)文本列表-List |  | True |
| separator | 分隔文本 | 拼接内容时，两项之间的内容。 | (0)字符串-Text | , | True |
| escapeSeparator | 转义“分隔文本” | 替换“分隔文本”中的转义字符（\r,\n,\t） | (2)布尔值-Boolean | False | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| output | 结果 | 生成的文本内容 | (0)字符串-Text |

</details>
<details>
<summary>范例</summary>

**转换结果为：a挨着b挨着c挨着d**
```json
{
  "Variables": [
    {
      "Key": "list",
      "Type": 4,
      "Desc": "",
      "DefaultValue": "a\r\nb\r\nc\r\nd",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "output",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:joinList",
      "InputParams": {
        "list": {
          "VarKey": "list",
          "Value": null
        },
        "separator": {
          "VarKey": null,
          "Value": "挨着"
        },
        "escapeSeparator": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {
        "output": "output"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 107.提取JSON内容

**功能描述**
> 提取Json文本中的信息

**官方文档**
> https://getquicker.net/KC/Help/Doc/jsonExtract

**内部名称**
> sys:jsonExtract

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| data | 输入 | 要从中提取内容的Json文本或JToken对象 | (0)字符串-Text |  | True |
| p0 | 提取路径0 |  | (0)字符串-Text |  | False |
| p1 | 提取路径1 |  | (0)字符串-Text |  | False |
| p2 | 提取路径2 |  | (0)字符串-Text |  | False |
| p3 | 提取路径3 |  | (0)字符串-Text |  | False |
| p4 | 提取路径4 |  | (0)字符串-Text |  | False |
| dateAsString | 日期时间按照文本处理 | 保留原有数据格式 | (2)布尔值-Boolean | False | False |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否没有异常 | (2)布尔值-Boolean |
| v0 | 值0 | 提取到的内容，和提取路径对应 | (99)任意类型-Any |
| v1 | 值1 | 提取到的内容，和提取路径对应 | (99)任意类型-Any |
| v2 | 值2 | 提取到的内容，和提取路径对应 | (99)任意类型-Any |
| v3 | 值3 | 提取到的内容，和提取路径对应 | (99)任意类型-Any |
| v4 | 值4 | 提取到的内容，和提取路径对应 | (99)任意类型-Any |
| rootToken | 根对象 | 整个输入内容解析后获得的JToken对象。可用于后续使用。 | (98)对象(Object)-Object |

</details>
<details>
<summary>范例</summary>

```json
{
  "Variables": [
    {
      "Key": "json",
      "Type": 0,
      "Desc": "json内容",
      "DefaultValue": "{\r\n  'Stores': [\r\n    'Lambton Quay',\r\n    'Willis Street'\r\n  ],\r\n  'Manufacturers': [\r\n    {\r\n      'Name': 'Acme Co',\r\n      'Products': [\r\n        {\r\n          'Name': 'Anvil',\r\n          'Price': 50\r\n        }\r\n      ]\r\n    },\r\n    {\r\n      'Name': 'Contoso',\r\n      'Products': [\r\n        {\r\n          'Name': 'Elbow Grease',\r\n          'Price': 99.95\r\n        },\r\n        {\r\n          'Name': 'Headlight Fluid',\r\n          'Price': 4\r\n        }\r\n      ]\r\n    }\r\n  ]\r\n}",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "list",
      "Type": 99,
      "Desc": "Manufacture对象列表",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "item",
      "Type": 99,
      "Desc": "列表的一项",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "rootToken",
      "Type": 99,
      "Desc": "根JToken对象，对应整个Json数据",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "oneName",
      "Type": 0,
      "Desc": "某个Manufacture的Name属性",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "index",
      "Type": 12,
      "Desc": "序号",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "nameList",
      "Type": 99,
      "Desc": "Name列表",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "提取所有的Manufacture对象到列表\r\n对列表中的每个Manufacture，显示其Name属性的值。"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:jsonExtract",
      "InputParams": {
        "data": {
          "VarKey": "json",
          "Value": null
        },
        "p0": {
          "VarKey": null,
          "Value": "Manufacturers"
        },
        "p1": {
          "VarKey": null,
          "Value": ""
        },
        "p2": {
          "VarKey": null,
          "Value": ""
        },
        "p3": {
          "VarKey": null,
          "Value": ""
        },
        "p4": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {
        "v0": "list",
        "v1": null,
        "v2": null,
        "v3": null,
        "v4": null,
        "rootToken": "rootToken"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:MsgBox",
      "InputParams": {
        "message": {
          "VarKey": null,
          "Value": "提取所有的Manufacture对象到列表\r\n对列表中的每个Manufacture，显示其Name属性的值。"
        },
        "title": {
          "VarKey": null,
          "Value": "Quicker"
        },
        "icon": {
          "VarKey": null,
          "Value": ""
        },
        "buttons": {
          "VarKey": null,
          "Value": "OK"
        }
      },
      "OutputParams": {
        "result": null,
        "okOrYes": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:each",
      "InputParams": {
        "input": {
          "VarKey": "list",
          "Value": null
        }
      },
      "OutputParams": {
        "item": "item",
        "count": "index"
      },
      "IfSteps": [
        {
          "StepRunnerKey": "sys:notify",
          "InputParams": {
            "msg": {
              "VarKey": null,
              "Value": "$= \"序号\" + {index}.ToString() + \" \" + {item}[\"Name\"]"
            },
            "maxLines": {
              "VarKey": null,
              "Value": "0"
            },
            "type": {
              "VarKey": null,
              "Value": "Info"
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:delay",
      "InputParams": {
        "delayMs": {
          "VarKey": null,
          "Value": "2000"
        },
        "monitorWaitWin": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "提取所有的Manufacture对象的Name属性到一个存放了所有Name的列表，\r\n对列表中的每个Name，显示其值。"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:jsonExtract",
      "InputParams": {
        "data": {
          "VarKey": "json",
          "Value": null
        },
        "p0": {
          "VarKey": null,
          "Value": "Manufacturers[*].Name"
        },
        "p1": {
          "VarKey": null,
          "Value": ""
        },
        "p2": {
          "VarKey": null,
          "Value": ""
        },
        "p3": {
          "VarKey": null,
          "Value": ""
        },
        "p4": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {
        "v0": "nameList",
        "v1": null,
        "v2": null,
        "v3": null,
        "v4": null,
        "rootToken": "rootToken"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:MsgBox",
      "InputParams": {
        "message": {
          "VarKey": null,
          "Value": "提取所有的Manufacture对象的Name属性到一个列表，\r\n对列表中的每个Name，显示其值。"
        },
        "title": {
          "VarKey": null,
          "Value": "Quicker"
        },
        "icon": {
          "VarKey": null,
          "Value": ""
        },
        "buttons": {
          "VarKey": null,
          "Value": "OK"
        }
      },
      "OutputParams": {
        "result": null,
        "okOrYes": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:each",
      "InputParams": {
        "input": {
          "VarKey": "nameList",
          "Value": null
        }
      },
      "OutputParams": {
        "item": "item",
        "count": "index"
      },
      "IfSteps": [
        {
          "StepRunnerKey": "sys:notify",
          "InputParams": {
            "msg": {
              "VarKey": null,
              "Value": "$= \"序号\" + {index}.ToString() + \" \" + {item}"
            },
            "maxLines": {
              "VarKey": null,
              "Value": "0"
            },
            "type": {
              "VarKey": null,
              "Value": "Info"
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:delay",
      "InputParams": {
        "delayMs": {
          "VarKey": null,
          "Value": "2000"
        },
        "monitorWaitWin": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "使用第一次提取时候保存的rootToken，提取json中的单个值"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:MsgBox",
      "InputParams": {
        "message": {
          "VarKey": null,
          "Value": "提取单个值 Manufacturers[0].Name"
        },
        "title": {
          "VarKey": null,
          "Value": "Quicker"
        },
        "icon": {
          "VarKey": null,
          "Value": ""
        },
        "buttons": {
          "VarKey": null,
          "Value": "OK"
        }
      },
      "OutputParams": {
        "result": null,
        "okOrYes": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:jsonExtract",
      "InputParams": {
        "data": {
          "VarKey": "rootToken",
          "Value": null
        },
        "p0": {
          "VarKey": null,
          "Value": "Manufacturers[0].Name"
        },
        "p1": {
          "VarKey": null,
          "Value": ""
        },
        "p2": {
          "VarKey": null,
          "Value": ""
        },
        "p3": {
          "VarKey": null,
          "Value": ""
        },
        "p4": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {
        "v0": "oneName",
        "v1": null,
        "v2": null,
        "v3": null,
        "v4": null,
        "rootToken": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:notify",
      "InputParams": {
        "msg": {
          "VarKey": "oneName",
          "Value": null
        },
        "maxLines": {
          "VarKey": null,
          "Value": "0"
        },
        "type": {
          "VarKey": null,
          "Value": "Info"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:delay",
      "InputParams": {
        "delayMs": {
          "VarKey": null,
          "Value": "2000"
        },
        "monitorWaitWin": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "使用表达式，读取第二个Manufacture的Name\r\n使用了两种写法。"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:MsgBox",
      "InputParams": {
        "message": {
          "VarKey": null,
          "Value": "使用表达式访问JToken中的内容\r\n$= \"方法1:\" + (string){rootToken}.SelectToken(\"Manufacturers[1].Name\")\r\n$= \"方法2\" + (string){rootToken}[\"Manufacturers\"][1][\"Name\"]"
        },
        "title": {
          "VarKey": null,
          "Value": "Quicker"
        },
        "icon": {
          "VarKey": null,
          "Value": ""
        },
        "buttons": {
          "VarKey": null,
          "Value": "OK"
        }
      },
      "OutputParams": {
        "result": null,
        "okOrYes": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:notify",
      "InputParams": {
        "msg": {
          "VarKey": null,
          "Value": "$= \"方法1:\" + (string){rootToken}.SelectToken(\"Manufacturers[1].Name\")"
        },
        "maxLines": {
          "VarKey": null,
          "Value": "0"
        },
        "type": {
          "VarKey": null,
          "Value": "Info"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:notify",
      "InputParams": {
        "msg": {
          "VarKey": null,
          "Value": "$= \"方法2\" + (string){rootToken}[\"Manufacturers\"][1][\"Name\"]"
        },
        "maxLines": {
          "VarKey": null,
          "Value": "0"
        },
        "type": {
          "VarKey": null,
          "Value": "Info"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 108.提取文件路径信息/生成路径

**功能描述**
> 从文件路径中提取文件名、文件夹等信息

**官方文档**
> https://getquicker.net/KC/Help/Doc/pathExtraction

**内部名称**
> sys:pathExtraction

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| operation | 操作类型 |  | (9)选项-Enum（getInfo: 提取文件路径信息; changeExt: 更改扩展名，其它不变; changeName: 更改文件名(含扩展名)，所在目录不变; changeNameWithoutExt: 更改文件名(不含扩展名和所在目录); changeDir: 更改所在目录，文件名不变; combine: 合并路径 (拼接)） | getInfo | False |
| path | 路径 | 待处理或拼接的路径 | (0)字符串-Text |  | True |
| newExtension | 新的扩展名 | 新的扩展名，如：.png | (0)字符串-Text |  | True |
| newFileName | 新的文件名 | 新的文件名，如：abcd.png | (0)字符串-Text |  | True |
| newFileNameWithoutExt | 新的文件名 | 新的文件名(不包含扩展名），如：newfile | (0)字符串-Text |  | True |
| newDir | 目标目录路径 | 目标存储路径，如：d:\Work\Test | (0)字符串-Text |  | True |
| path2 | 路径部分2 |  | (0)字符串-Text |  | True |
| path3 | 路径部分3 |  | (0)字符串-Text |  | True |
| path4 | 路径部分4 |  | (0)字符串-Text |  | True |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 提取过程是否没有遇到异常 | (2)布尔值-Boolean |
| resultPath | 结果路径 | 生成的结果路径 | (0)字符串-Text |
| name | 文件名 | 去除路径的文件名 | (0)字符串-Text |
| nameNoExt | 文件名(去掉扩展名) | 去除扩展名的文件名 | (0)字符串-Text |
| ext | 扩展名 | 文件的扩展名 | (0)字符串-Text |
| path | 所在文件夹路径 | 父目录路径 | (0)字符串-Text |

</details>
<details>
<summary>范例</summary>

```json
{
  "Variables": [
    {
      "Key": "name",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "nameNoExt",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "ext",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "path",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "resultPath",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:pathExtraction",
      "InputParams": {
        "operation": {
          "VarKey": null,
          "Value": "getInfo"
        },
        "path": {
          "VarKey": null,
          "Value": "D:\\Work\\Quicker\\doc\\icon.psd"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "name": "name",
        "nameNoExt": "nameNoExt",
        "ext": "ext",
        "path": "path"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:pathExtraction",
      "InputParams": {
        "operation": {
          "VarKey": null,
          "Value": "changeExt"
        },
        "path": {
          "VarKey": null,
          "Value": "D:\\Work\\Quicker\\doc\\icon.psd"
        },
        "newExtension": {
          "VarKey": null,
          "Value": ".jpg"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "resultPath": "resultPath"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:pathExtraction",
      "InputParams": {
        "operation": {
          "VarKey": null,
          "Value": "changeName"
        },
        "path": {
          "VarKey": null,
          "Value": "D:\\Work\\Quicker\\doc\\icon.psd"
        },
        "newFileName": {
          "VarKey": null,
          "Value": "icon_save_20220506_112233.psd"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "resultPath": "resultPath"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:pathExtraction",
      "InputParams": {
        "operation": {
          "VarKey": null,
          "Value": "changeDir"
        },
        "path": {
          "VarKey": null,
          "Value": "D:\\Work\\Quicker\\doc\\icon.psd"
        },
        "newDir": {
          "VarKey": null,
          "Value": "D:\\Backup\\20220105"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "resultPath": "resultPath"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:pathExtraction",
      "InputParams": {
        "operation": {
          "VarKey": null,
          "Value": "combine"
        },
        "path": {
          "VarKey": null,
          "Value": "d:\\Work"
        },
        "path2": {
          "VarKey": null,
          "Value": "media"
        },
        "path3": {
          "VarKey": null,
          "Value": "20220506"
        },
        "path4": {
          "VarKey": null,
          "Value": "abc.gif"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "resultPath": "resultPath"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 109.正则提取

**功能描述**
> 使用正则表达式提取指定内容

**官方文档**
> https://getquicker.net/KC/Help/Doc/regexextract

**内部名称**
> sys:regexExtract

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| getGroup | 提取方式 | 输出的内容根据提取内容有所不同，请参考模块文档。 | (9)选项-Enum（0: 各匹配项的值; 1: 第一个匹配项的组; 2: 各匹配项的组） | 0 | True |
| data | 输入 | 要提取内容的文本 | (0)字符串-Text |  | True |
| pattern | 正则表达式 | 用于提取内容的正则表达式 | (0)字符串-Text |  | True |
| ignoreCase | 忽略大小写 | 不区分英文大小写 | (2)布尔值-Boolean | False | False |
| singleLine | 单行模式 | 此模式下“.”能匹配任意字符，包括换行符。(否则匹配除了\n外的任意字符) | (2)布尔值-Boolean | False | False |
| multiLine | 多行模式 | 此模式下^和$可以分别匹配行首和行尾。(否则匹配输入内容的开始和结束) | (2)布尔值-Boolean | False | False |
| rightToLeft | 从右向左 | 从右向左查找匹配内容 | (2)布尔值-Boolean | False | False |
| stopIfFail | 失败后中止动作 | 操作失败后，是否停止后续动作的执行。 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| matches | 所有匹配列表 | 返回所有的匹配项 | (4)文本列表-List |
| match1  | 匹配1 | 第1个匹配项的值 | (99)任意类型-Any |
| match2  | 匹配2 | 第2个匹配项的值 | (99)任意类型-Any |
| match3  | 匹配3 | 第3个匹配项的值 | (99)任意类型-Any |
| match4  | 匹配4 | 第4个匹配项的值 | (99)任意类型-Any |
| match5  | 匹配5 | 第5个匹配项的值 | (99)任意类型-Any |
| matchObj | Match对象 | 首个匹配的原始的C#语言Match对象，可以在表达式中使用 | (98)对象(Object)-Object |
| matchesCollection | Matches集合 | 所有匹配的原始Match对象集合(MatchCollection)，可以在表达式中使用 | (98)对象(Object)-Object |
| isSuccess | 是否成功 | 是否匹配成功 | (2)布尔值-Boolean |

</details>
<details>
<summary>范例</summary>

```json
{
  "Variables": [
    {
      "Key": "source",
      "Type": 0,
      "Desc": "原始文本内容",
      "DefaultValue": "a1 b2 c3 d4\r\ne5 f6 g7 h8",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "allMatches",
      "Type": 4,
      "Desc": "所有匹配项的值列表",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "match1",
      "Type": 99,
      "Desc": "匹配项1",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "match2",
      "Type": 0,
      "Desc": "匹配项2",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "match3",
      "Type": 0,
      "Desc": "匹配项3",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "match4",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "match5",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "matchCollection",
      "Type": 99,
      "Desc": "Match对象集合",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "regExpression",
      "Type": 0,
      "Desc": "正则表达式",
      "DefaultValue": "([a-z])([0-9])",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "matchObj",
      "Type": 99,
      "Desc": "原始Match对象",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:regexExtract",
      "InputParams": {
        "getGroup": {
          "VarKey": null,
          "Value": "0"
        },
        "data": {
          "VarKey": "source",
          "Value": null
        },
        "pattern": {
          "VarKey": "regExpression",
          "Value": null
        },
        "ignoreCase": {
          "VarKey": null,
          "Value": "0"
        },
        "singleLine": {
          "VarKey": null,
          "Value": "0"
        },
        "multiLine": {
          "VarKey": null,
          "Value": "0"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "matches": "allMatches",
        "match1 ": "match1",
        "match2 ": "match2",
        "match3 ": "match3",
        "match4 ": "match4",
        "match5 ": "match5",
        "matchesCollection": null,
        "isSuccess": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:showText",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "WAIT"
        },
        "text": {
          "VarKey": null,
          "Value": "$$\r\n原始内容：{source}\r\n正则表达式：{regExpression}\r\n提取内容：各匹配项的值\r\n===================\r\n所有匹配项列表：\r\n{allMatches}\r\n===================\r\n匹配1:{match1}\r\n匹配2:{match2}\r\n匹配3:{match3}\r\n匹配4:{match4}\r\n匹配5:{match5}\r\n"
        },
        "title": {
          "VarKey": null,
          "Value": "结果内容"
        },
        "operations": {
          "VarKey": null,
          "Value": ""
        },
        "winLocation": {
          "VarKey": null,
          "Value": "CenterScreen"
        },
        "fontsize": {
          "VarKey": null,
          "Value": "14"
        },
        "fontfamily": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {
        "selectedOperation": null,
        "resultText": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "提取首个匹配项的组"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:regexExtract",
      "InputParams": {
        "getGroup": {
          "VarKey": null,
          "Value": "1"
        },
        "data": {
          "VarKey": "source",
          "Value": null
        },
        "pattern": {
          "VarKey": "regExpression",
          "Value": null
        },
        "ignoreCase": {
          "VarKey": null,
          "Value": "0"
        },
        "singleLine": {
          "VarKey": null,
          "Value": "1"
        },
        "multiLine": {
          "VarKey": null,
          "Value": "0"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "matches": "allMatches",
        "match1 ": "match1",
        "match2 ": "match2",
        "match3 ": "match3",
        "match4 ": "match4",
        "match5 ": "match5",
        "matchObj": "matchObj",
        "isSuccess": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:showText",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "WAIT"
        },
        "text": {
          "VarKey": null,
          "Value": "$$\r\n原始内容：{source}\r\n正则表达式：{regExpression}\r\n提取内容：第一个匹配项的组\r\n===================\r\n所有匹配项列表：\r\n{allMatches}\r\n===================\r\n匹配1:{match1}\r\n匹配2:{match2}\r\n匹配3:{match3}\r\n匹配4:{match4}\r\n匹配5:{match5}\r\n"
        },
        "title": {
          "VarKey": null,
          "Value": "结果内容"
        },
        "operations": {
          "VarKey": null,
          "Value": ""
        },
        "winLocation": {
          "VarKey": null,
          "Value": "CenterScreen"
        },
        "fontsize": {
          "VarKey": null,
          "Value": "14"
        },
        "fontfamily": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {
        "selectedOperation": null,
        "resultText": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "提取所有匹配项的组"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:regexExtract",
      "InputParams": {
        "getGroup": {
          "VarKey": null,
          "Value": "2"
        },
        "data": {
          "VarKey": "source",
          "Value": null
        },
        "pattern": {
          "VarKey": "regExpression",
          "Value": null
        },
        "ignoreCase": {
          "VarKey": null,
          "Value": "0"
        },
        "singleLine": {
          "VarKey": null,
          "Value": "1"
        },
        "multiLine": {
          "VarKey": null,
          "Value": "0"
        },
        "rightToLeft": {
          "VarKey": null,
          "Value": "false"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "matches": "allMatches",
        "match1 ": "match1",
        "match2 ": "match2",
        "match3 ": "match3",
        "match4 ": "match4",
        "match5 ": "match5",
        "matchesCollection": "matchCollection",
        "isSuccess": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:showText",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "WAIT"
        },
        "text": {
          "VarKey": null,
          "Value": "$$\r\n原始内容：{source}\r\n正则表达式：{regExpression}\r\n提取内容：所有匹配项的组\r\n===================\r\n所有匹配项列表：\r\n{allMatches}\r\n===================\r\n匹配1:{match1}\r\n匹配2:{match2}\r\n匹配3:{match3}\r\n匹配4:{match4}\r\n匹配5:{match5}\r\n"
        },
        "title": {
          "VarKey": null,
          "Value": "结果内容"
        },
        "operations": {
          "VarKey": null,
          "Value": ""
        },
        "winLocation": {
          "VarKey": null,
          "Value": "CenterScreen"
        },
        "fontsize": {
          "VarKey": null,
          "Value": "14"
        },
        "fontfamily": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {
        "selectedOperation": null,
        "resultText": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "在表达式中使用原始c#对象。"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:notify",
      "InputParams": {
        "msg": {
          "VarKey": null,
          "Value": "$= \"MatchCollection中Match对象数量=\" + {matchCollection}.Count + \"\\n\" \r\n+ \"首个Match的值：\" + {matchCollection}[0].Value"
        },
        "maxLines": {
          "VarKey": null,
          "Value": "0"
        },
        "type": {
          "VarKey": null,
          "Value": "Info"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:notify",
      "InputParams": {
        "msg": {
          "VarKey": null,
          "Value": "$= \"Match对象的Groupshul =\" + {matchObj}.Groups.Count + \"\\n\" \r\n+ \"首个group的值：\" + {matchObj}.Groups[1].Value"
        },
        "maxLines": {
          "VarKey": null,
          "Value": "0"
        },
        "type": {
          "VarKey": null,
          "Value": "Info"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 110.文本窗口

**功能描述**
> 在独立的窗口中显示文本。

**官方文档**
> https://getquicker.net/KC/Help/Doc/showText

**内部名称**
> sys:showText

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| type | 操作类型 | 是否等待窗口关闭后继续 | (9)选项-Enum（NO_WAIT: 显示窗口，不等待关闭（立即开始执行后续的步骤）; WAIT: 显示窗口，等待关闭; CLOSE_WINDOW: 关闭窗口; GET_WIN_INFO: 获取窗口信息; APPEND_TEXT: 追加内容; ACTIVATE_WINDOW: 显示和激活窗口; WAIT_CLOSE: 等待窗口关闭; GET_ALL_WINDOWS: 获取所有文本窗口; GET_ACTION_WINDOWS: 获取当前动作创建的所有文本窗口） | NO_WAIT | False |
| text | 文本内容 | 要显示的文本内容 | (0)字符串-Text |  | True |
| title | 窗口标题 | 窗口标题文字 | (0)字符串-Text | 文本窗口 | True |
| operations | 工具栏操作 | 用于显示在窗口工具栏。每行一个选项，格式为 “文本” 或 “显示文本|值”。 | (0)字符串-Text |  | True |
| autoCloseKey | 文本窗口标识 | 可选。自动更新或关闭之前打开的具有此标识的文本窗口。使用‘=’表示当前动作id。 | (0)字符串-Text | = | False |
| winLocation | 窗口位置类型 | 在哪里显示选择窗口 | (9)选项-Enum | CenterScreen | False |
| winSize | 窗口尺寸/位置 | 设置选择窗口的尺寸，格式为：宽度,高度。支持逻辑像素数值或屏幕宽高百分比，详情请参考模块文档。 “窗口位置” 类型为 “自定义位置” 时用于指定显示位置，格式为：left,top,right,bottom | (0)字符串-Text |  | False |
| fontsize | 字体大小 | 默认的字体大小 | (1)数字(小数)-Number | 14 | True |
| fontfamily | 字体名称 | 可选。设置字体名称。如有多个字体，使用逗号分隔。 | (0)字符串-Text |  | False |
| bgColor | 背景颜色 | 可选。格式为#RRGGBB | (0)字符串-Text |  | False |
| textColor | 文字颜色 | 可选。格式为#RRGGBB | (0)字符串-Text |  | False |
| highlight | 语法高亮 |  | (9)选项-Enum |  | False |
| autoSaveToState | 自动保存到状态 | 指定状态Key。文本内容将自动保存到状态中。 | (0)字符串-Text |  | False |
| topMost | 置顶显示 |  | (2)布尔值-Boolean | False | False |
| enableEscClose | Esc 键关闭窗口 |  | (2)布尔值-Boolean | True | False |
| closeWhenLostFocus | 失去焦点自动关闭 |  | (2)布尔值-Boolean | False | False |
| showLineNum | 显示行号 |  | (2)布尔值-Boolean | True | False |
| autoWrap | 自动换行显示 |  | (2)布尔值-Boolean | True | False |
| showBuildInToolbar | 显示内置工具栏 |  | (2)布尔值-Boolean | True | False |
| copyWholeLine | 未选择内容时，复制或剪切整行 |  | (2)布尔值-Boolean | False | False |
| caretPosition | 光标位置 | 0表示最前面，-1表示最后面，其它数字表示某个具体字符位置。 | (12)数字(整数)-Integer | 0 | True |
| advancedSettings | 高级设置 | 请参考模块文档。 | (0)字符串-Text |  | False |
| updateIfExists | 如果窗口存在，则直接更新窗口内容（而不是关闭后打开新窗口） |  | (2)布尔值-Boolean | False | False |
| stopIfFail | 失败后停止 | 失败后是否停止动作 | (2)布尔值-Boolean | True | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| isWindowExists | 窗口是否存在 |  | (2)布尔值-Boolean |
| selectedOperation | 选择的项 | 选择的后续操作项 | (0)字符串-Text |
| resultText | 结果文本 | 文本框内的所有文本 | (0)字符串-Text |
| selectedText | 选中的文本 | 文本框内选中的文本 | (0)字符串-Text |
| windowHandle | 窗口句柄 |  | (12)数字(整数)-Integer |
| windowPosition | 窗口位置 | 窗口的最终显示位置 | (0)字符串-Text |
| allWindows | 所有窗口 | 词典类型，key为窗口的句柄，value为窗口的标识。获取全部窗口时，为了安全，仅限自己开发的动作使用。 | (10)词典-Dict |

</details>
<details>
<summary>范例</summary>

```json
{
  "Variables": [
    {
      "Key": "context",
      "Type": 0,
      "Desc": "默认的文本变量",
      "DefaultValue": "aaaa\r\nbbbb",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "list",
      "Type": 4,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:form",
      "InputParams": {
        "title": {
          "VarKey": null,
          "Value": "填写表单"
        },
        "formDef": {
          "VarKey": null,
          "Value": "{\"Fields\":[{\"FieldKey\":\"context\",\"Label\":\"testt_t\",\"HelpText\":\"\",\"HelpLink\":null,\"InputMethod\":1,\"SelectionItems\":\"\",\"IsRequired\":false,\"MinValue\":\"\",\"MaxValue\":\"\",\"Pattern\":\"\",\"MaxLength\":0},{\"FieldKey\":\"list\",\"Label\":\"test_e\",\"HelpText\":\"test\",\"HelpLink\":null,\"InputMethod\":8,\"SelectionItems\":\"aaa\\r\\nbbb\\r\\nccc\\r\\nddd\",\"IsRequired\":false,\"MinValue\":\"\",\"MaxValue\":\"\",\"Pattern\":\"\",\"MaxLength\":0}]}"
        },
        "help": {
          "VarKey": null,
          "Value": ""
        },
        "restoreFocus": {
          "VarKey": null,
          "Value": "0"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:getSelectedText",
      "InputParams": {
        "format": {
          "VarKey": null,
          "Value": "UnicodeText"
        },
        "repeat": {
          "VarKey": null,
          "Value": "0"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "output": "context",
        "outputEncoded": null,
        "isSuccess": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:showText",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "WAIT"
        },
        "text": {
          "VarKey": "context",
          "Value": null
        },
        "title": {
          "VarKey": null,
          "Value": "结果内容"
        },
        "operations": {
          "VarKey": null,
          "Value": "[fa:Solid_Cog33:#339900]转大写(将选中的文字转换为大写)|call:s$rs$in$toUpper\r\n【*】|call:s$rs$sp$文本添加首尾内容?head=【&end=】\r\n[+][fa:Solid_Pen:#FF0000]菜单(这里是tooltip内容)\r\n[-][fa:Light_LaughBeam:#0000FF]添加[*](选中的内容包围在中括号中)|call:s$rs$sp$文本添加首尾内容?head=[&end=]\r\n[fa:Solid_Cog:#339900]转小写(将选中的文字转换为大写)|call:s$rs$in$toLower\r\nEcho服务|call:all$rs$cloud$echo\r\n[fa:Light_SignOut:#BB0000](关闭窗口)|Exit"
        },
        "winLocation": {
          "VarKey": null,
          "Value": "CenterScreen"
        },
        "fontsize": {
          "VarKey": null,
          "Value": "14"
        },
        "fontfamily": {
          "VarKey": null,
          "Value": ""
        },
        "highlight": {
          "VarKey": null,
          "Value": ""
        },
        "topMost": {
          "VarKey": null,
          "Value": "0"
        },
        "closeWhenLostFocus": {
          "VarKey": null,
          "Value": "0"
        },
        "showLineNum": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "selectedOperation": null,
        "resultText": null,
        "selectedText": "context"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 111.拆分文本为列表

**功能描述**
> 将文本拆分为列表

**官方文档**
> https://getquicker.net/KC/Help/Doc/splitstring

**内部名称**
> sys:splitString

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| data | 输入 | 要拆分为列表的文本 | (0)字符串-Text |  | True |
| separator | 分隔 | 拆分分隔符 | (0)字符串-Text | , | True |
| escapeSeparator | 转义分隔符 | 转义分隔符\r\n\t字符 | (2)布尔值-Boolean | False | False |
| multiSeparator | 使用多个分隔符拆分列表 | 每行指定一个。 | (2)布尔值-Boolean | False | False |
| removeEmpty | 滤除空值 | 滤除没有内容的文本 | (2)布尔值-Boolean | True | True |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| output | 结果 | 生成的文本内容 | (4)文本列表-List |

</details>
<details>
<summary>范例</summary>

**按字母顺序排序多行文本**
```json
{
  "Variables": [
    {
      "Key": "context",
      "Type": 0,
      "Desc": "默认的文本变量",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": null,
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "list",
      "Type": 4,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": null,
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:getSelectedText",
      "InputParams": {
        "format": {
          "VarKey": null,
          "Value": "UnicodeText"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "output": "context",
        "isSuccess": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:splitString",
      "InputParams": {
        "data": {
          "VarKey": "context",
          "Value": null
        },
        "separator": {
          "VarKey": null,
          "Value": "\\n"
        },
        "escapeSeparator": {
          "VarKey": null,
          "Value": "1"
        },
        "removeEmpty": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "output": "list"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:if",
      "InputParams": {
        "condition": {
          "VarKey": null,
          "Value": "$={quicker_in_param} == \"desc\""
        }
      },
      "OutputParams": {},
      "IfSteps": [
        {
          "StepRunnerKey": "sys:listOperations",
          "InputParams": {
            "list": {
              "VarKey": "list",
              "Value": null
            },
            "type": {
              "VarKey": null,
              "Value": "sortDesc"
            }
          },
          "OutputParams": {
            "value": "list",
            "isEmpty": null,
            "length": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": [
        {
          "StepRunnerKey": "sys:listOperations",
          "InputParams": {
            "list": {
              "VarKey": "list",
              "Value": null
            },
            "type": {
              "VarKey": null,
              "Value": "sortAsc"
            },
            "list2": {
              "VarKey": null,
              "Value": ""
            },
            "pos": {
              "VarKey": null,
              "Value": "0"
            },
            "length": {
              "VarKey": null,
              "Value": "1"
            },
            "item": {
              "VarKey": null,
              "Value": ""
            }
          },
          "OutputParams": {
            "isEmpty": null,
            "length": null,
            "value": "list"
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:outputText",
      "InputParams": {
        "content": {
          "VarKey": "list",
          "Value": null
        },
        "method": {
          "VarKey": null,
          "Value": "paste"
        },
        "appendReturn": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 112.替换文本

**功能描述**
> 替换文本中的指定内容

**官方文档**
> https://getquicker.net/KC/Help/Doc/strReplace

**内部名称**
> sys:strReplace

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| type | 操作类型 |  | (9)选项-Enum（single: 普通（替换一种内容）; batch: 批量（替换多种内容）） | single | True |
| input | 输入 | 要提取内容的文本 | (0)字符串-Text |  | True |
| batchReplaceData | 查找和替换内容 | 每行一对查找和替换内容，中间使用|||或|分隔。例如将a替换成A，写作:a|A 或 a|||A | (0)字符串-Text |  | True |
| old | 查找内容 | 要替换的内容 | (0)字符串-Text |  | True |
| new | 替换为 | 替换成的内容 | (0)字符串-Text |  | True |
| escapeOld | 转义“查找内容” | 替换“查找内容”中的转义字符（\r,\n,\t） | (2)布尔值-Boolean | False | False |
| replaceEscapes | 转义“替换为” | 替换“替换为”中的转义字符（\r,\n,\t） | (2)布尔值-Boolean | True | False |
| useRegex | 使用正则替换 |  | (2)布尔值-Boolean | False | False |
| ignoreCase | 忽略大小写 |  | (2)布尔值-Boolean | False | False |
| singleLine | 正则：单行 | 此模式下“.”能匹配任意字符，包括换行符。(否则匹配除了\n外的任意字符) | (2)布尔值-Boolean | True | False |
| multiLine | 正则：多行 | 此模式下^和$可以分别匹配行首和行尾。(否则匹配输入内容的开始和结束) | (2)布尔值-Boolean | False | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| output | 结果 | 替换后的文本 | (0)字符串-Text |

</details>
<details>
<summary>范例</summary>

**去除英文**
```json
{
  "Variables": [
    {
      "Key": "去除的变量",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "去除后",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:strReplace",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "single"
        },
        "input": {
          "VarKey": "去除的变量",
          "Value": null
        },
        "old": {
          "VarKey": null,
          "Value": "[a-zA-Z]"
        },
        "new": {
          "VarKey": null,
          "Value": ""
        },
        "escapeOld": {
          "VarKey": null,
          "Value": "0"
        },
        "replaceEscapes": {
          "VarKey": null,
          "Value": "1"
        },
        "useRegex": {
          "VarKey": null,
          "Value": "1"
        },
        "ignoreCase": {
          "VarKey": null,
          "Value": "0"
        },
        "singleLine": {
          "VarKey": null,
          "Value": "1"
        },
        "multiLine": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {
        "output": "去除后"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 113.字数统计

**功能描述**
> 统计文本行数、字符数等

**官方文档**
> https://getquicker.net/KC/Help/Doc/textcounter

**内部名称**
> sys:textCounter

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| content | 文本 | 要统计的内容 | (0)字符串-Text |  | True |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| line | 行数 |  | (12)数字(整数)-Integer |
| char | 字符数 |  | (12)数字(整数)-Integer |
| visableChar | 可见字符数 |  | (12)数字(整数)-Integer |
| cnChar | 汉字数 |  | (12)数字(整数)-Integer |

</details>

***

## 114.Office软件辅助

**功能描述**
> 辅助控制Office软件

**官方文档**
> https://getquicker.net/KC/Help/Doc/officehelper

**内部名称**
> sys:officehelper

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| operation | 操作类型 |  | (9)选项-Enum（execVBA: 执行VBA宏代码; setFormats: 设置格式/对象属性赋值; executeMsoCommand: 执行界面命令; getProgId: 获取ProgId） | execVBA | True |
| appType | 应用程序 |  | (9)选项-Enum（word_wps: Word或WPS文字（根据前台进程自动识别）; word; wps: wps文字; excel_et: EXCEL或WPS表格（根据前台进程自动识别）; excel; et: wps表格; powerpoint_wpp: PowerPoint或WPS幻灯片（根据前台进程自动识别）; powerpoint; wpp） | word_wps | True |
| code | 宏名称或VBA代码 | 宏的名称，或VBA代码（将执行第一个找到的Sub或Function） | (0)字符串-Text | Sub Hello() MsgBox "Hello World" End Sub | False |
| waitResp | 最长等待时间(ms) | 最长的等待返回结果的，毫秒数 | 数字(小数)-Number | 10000 | False |
| command | 命令ID | 界面按钮所对应的命令ID | (0)字符串-Text |  | False |
| formats | 格式设置/属性赋值代码 |  | (0)字符串-Text |  | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| progId | ProgId | 获取程序的Progld，可用于在C#里得到对应的Application对象。 | (0)字符串-Text |

</details>
<details>
<summary>范例</summary>

**获取选中文本到变量text，再到用户输入框，再以text变量内容为前台的word或wps添加批注**
```json
{
  "Variables": [
    {
      "Key": "text",
      "Type": 0,
      "Desc": "默认的文本变量",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": null,
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:getSelectedText",
      "InputParams": {
        "format": {
          "VarKey": null,
          "Value": "UnicodeText"
        },
        "waitMs": {
          "VarKey": null,
          "Value": "250"
        },
        "repeat": {
          "VarKey": null,
          "Value": "0"
        },
        "trim": {
          "VarKey": null,
          "Value": "0"
        },
        "tryNoClipboard": {
          "VarKey": null,
          "Value": "1"
        },
        "useActionParam": {
          "VarKey": null,
          "Value": "0"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "output": "text",
        "outputEncoded": null,
        "url": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:userInput",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "text"
        },
        "prompt": {
          "VarKey": null,
          "Value": "请输入批注内容"
        },
        "defaultValue": {
          "VarKey": "text",
          "Value": null
        },
        "pattern": {
          "VarKey": null,
          "Value": ""
        },
        "isRequired": {
          "VarKey": null,
          "Value": "0"
        },
        "restoreFocus": {
          "VarKey": null,
          "Value": "1"
        },
        "closeOnDeactivated": {
          "VarKey": null,
          "Value": "0"
        },
        "topMost": {
          "VarKey": null,
          "Value": "0"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        },
        "texttools": {
          "VarKey": null,
          "Value": ""
        },
        "extraSettings": {
          "VarKey": null,
          "Value": ""
        },
        "fontfamily": {
          "VarKey": null,
          "Value": ""
        },
        "fontsize": {
          "VarKey": null,
          "Value": "20"
        },
        "winLocation": {
          "VarKey": null,
          "Value": "CenterScreen"
        },
        "imeState": {
          "VarKey": null,
          "Value": "ON"
        },
        "help": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "textValue": "text",
        "isEmpty": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:officehelper",
      "InputParams": {
        "operation": {
          "VarKey": null,
          "Value": "execVBA"
        },
        "appType": {
          "VarKey": null,
          "Value": "word_wps"
        },
        "code": {
          "VarKey": null,
          "Value": "$$Sub CreateNewComment()\r\n    Dim MyRange As Range\r\n    Dim MyComment As Comment\r\n    Dim CommentText As String\r\n    \r\n    '设置批注内容为text\r\n    CommentText = \"{text}\"\r\n    \r\n    '设置选中的文本范围\r\n    Set MyRange = Selection.Range\r\n    \r\n    '在选中文本处添加新批注\r\n    Set MyComment = ActiveDocument.Comments.Add(MyRange, CommentText)\r\n    \r\nEnd Sub"
        },
        "waitResp": {
          "VarKey": null,
          "Value": "1"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        },
        "waitMs": {
          "VarKey": null,
          "Value": "10000"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "resp": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```

**冻结窗格**
```json
{
  "Variables": [],
  "Steps": [
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "下面步骤代码中的叹号表示对属性值取反。"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:officehelper",
      "InputParams": {
        "operation": {
          "VarKey": null,
          "Value": "setFormats"
        },
        "appType": {
          "VarKey": null,
          "Value": "excel_et"
        },
        "formats": {
          "VarKey": null,
          "Value": "application\r\n\t.ActiveWindow.FreezePanes = !"
        },
        "waitResp": {
          "VarKey": null,
          "Value": "1"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```

**配合C#冻结窗格**
```json
{
  "Variables": [
    {
      "Key": "progId",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "为兼容Excel和WPS，先根据前台进程获取ProgId（用于调用接口的程序对象标识）"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:officehelper",
      "InputParams": {
        "operation": {
          "VarKey": null,
          "Value": "getProgId"
        },
        "appType": {
          "VarKey": null,
          "Value": "excel_et"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "progId": "progId"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "使用c#代码获取程序对象并执行逻辑"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:csscript",
      "InputParams": {
        "mode": {
          "VarKey": null,
          "Value": "low_permission"
        },
        "scriptForLp": {
          "VarKey": null,
          "Value": "$$//.cs  文件类型，便于外部编辑时使用\r\n// 引用必要的命名空间\r\nusing System.Runtime.InteropServices;\r\n\r\n// Quicker将会调用的函数\r\npublic static string Exec(string paramValue)\r\n{\r\n   dynamic app = Marshal.GetActiveObject(\"{progId}\");\r\n    \r\n    app.ActiveWindow.FreezePanes = !app.ActiveWindow.FreezePanes;\r\n    \r\n    Marshal.ReleaseComObject(app);\r\n    return \"ok\";\r\n}\r\n"
        },
        "paramValue": {
          "VarKey": null,
          "Value": ""
        },
        "reference": {
          "VarKey": null,
          "Value": ""
        },
        "waitResp": {
          "VarKey": null,
          "Value": "1"
        },
        "enableCache": {
          "VarKey": null,
          "Value": "0"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "resp": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```

</details>

***

## 115.Excel文件读写

**功能描述**
> 读取Excel文件内容或写入Excel文件

**官方文档**
> https://getquicker.net/KC/Help/Doc/excelreadwrite

**内部名称**
> sys:excelreadwrite

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| operation | 操作类型 |  | (9)选项-Enum（load: 打开Workbook; newWorkbook: 创建Workbook; save: 保存Workbook; getSheet: 获取Sheet; createSheet: 创建Sheet; getRow: 获取行; getCellByValue: 查找单元格（根据值）; getCell: 读取单元格; setCell: 写入单元格; writeData: 写入多行数据; mergeCells: 合并单元格; freezePane: 冻结窗格; autoFilter: 自动筛选; setStyle: 设置区域单元格样式; readData: 批量提取数据; batchReplace: 批量模板替换） |  | True |
| filePath | 文件路径 | 要打开或写入的Excel文件路径 | (0)字符串-Text |  | False |
| fileType | 工作簿类型 |  | (9)选项-Enum（XSSF: .xlsx 2007版Excel; HSSF: xls 2003版Excel） |  | False |
| workbook | 工作簿对象 | 需要操作的工作簿对象 | (99)任意类型-Any |  | False |
| sheetIndex | 工作表序号或名称 | 以0开始计算的序号或名称 | (0)字符串-Text |  | False |
| sheetName | 工作表名称 | 要打开的工作表名称 | (0)字符串-Text |  | False |
| rowIndex | 行序号 | 以0开始计算的序号 | (12)数字(整数)-Integer | 0 | False |
| cellValue | 值 | 设置单元格的值 | (0)字符串-Text |  | False |
| worksheet | 工作表对象 | 需要操作的工作表对象 | (99)任意类型-Any |  | False |
| cellAddress | 单元格地址 | 类似于"D5"这样的单元格位置名称。或在下方使用行序号和单元格序号指定（两种二选一） | (0)字符串-Text |  | False |
| cellIndex | 列序号 | 单元格在所在行里的序号，从0开始 | (12)数字(整数)-Integer | 0 | False |
| cellType | 单元格类型 |  | (9)选项-Enum（"": 自动; String: 文本; Numeric: 数字或日期; Boolean: 布尔; Formula: 公式; Blank: 空白） |  | False |
| dataFormat | 数据格式 | 设置单元格的DataFormat | (0)字符串-Text |  | False |
| cellLink | 链接 | 可以为网址、邮件地址（mailto:who@domain.com)工作表名称、文件路径 | (0)字符串-Text |  | False |
| sourceData | 源数据 | 可以为工作表对象、表格变量或对象列表 | (99)任意类型-Any |  | False |
| columnMapping | 字段映射 | 复制哪些字段信息到目标工作表。请参考文档了解使用方法。 | (0)字符串-Text |  | False |
| writeTitleRow | 写入标题行 | 是否输出标题行 | (2)布尔值-Boolean | True | False |
| cellRange | 单元格范围 | 类似于"A1:B5"格式，或"开始行号,结束行号,开始列号,结束列号方式(从0开始的序号)。 | (0)字符串-Text |  | False |
| styleData | 样式 |  | (0)字符串-Text |  | False |
| readDataMap | 提取数据定义 | 每行一条规则：“字段:[工作表序号或名称]单元格地址” | (0)字符串-Text |  | False |
| replaceDict | 替换词典数据 | 词典格式数据。键为要查找的字段，值为要填充的内容。 | (10)词典-Dict |  | False |
| replacePrefixSuffix | 占位符前后缀 | 第一行写前缀，第二行写后缀。“前缀+字段名+后缀“组成要查找和替换的目标，如”{{姓名}}”。 | (0)字符串-Text | {{\r\n}} | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| workbook | 工作簿对象 | 用于在后续步骤中继续操作工作簿。 | (99)任意类型-Any |
| numberOfSheets | 工作表个数 | 工作簿中的工作表个数。 | (12)数字(整数)-Integer |
| worksheetNameList | 工作表名称列表 | 工作簿中的工作表名列表。 | (4)文本列表-List |
| sheet | 工作表对象 | 返回指定的工作表。加载文件时返回工作簿中的第一个工作表对象 | (99)任意类型-Any |
| firstRow | 首行序号 | 工作表首行序号。 | (12)数字(整数)-Integer |
| lastRow | 末行序号 | 工作表有内容的最后一行序号。 | (12)数字(整数)-Integer |
| names | 名称数据 | 工作簿中定义的名称数据，返回json格式 | (0)字符串-Text |
| firstCellNum | 首个单元格序号 | 工作表有内容的最后一行序号。 | (12)数字(整数)-Integer |
| lastCellNum | 末个单元格序号 | 一行的最后一个单元格的序号。 | (12)数字(整数)-Integer |
| cellAddress | 单元格地址 | 查找到的单元格地址 | (99)任意类型-Any |
| hasValue | 是否有值 | 单元格是否有值 | (2)布尔值-Boolean |
| cellValue | 值 | 单元格的值 | (0)字符串-Text |
| cellTextValue | 文本值 | 文本格式的单元格内容 | (0)字符串-Text |
| cellType | 类型 | 单元格的类型 | (0)字符串-Text |
| cellFormula | 公式 | 单元格的公式值 | (0)字符串-Text |
| cellDataFormatString | 数据格式字符串 | 数据格式的字符串表示 | (0)字符串-Text |
| dictData | 数据词典 | 从工作薄加载的数据 | (10)词典-Dict |

</details>
<details>
<summary>范例</summary>

**生成一个乘法口诀表**
```json
{
  "Variables": [
    {
      "Key": "isSuccess",
      "Type": 2,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "worksheet",
      "Type": 99,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "workbook",
      "Type": 99,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "x",
      "Type": 12,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "y",
      "Type": 12,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "filePath",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "创建新的excel工作簿"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:excelreadwrite",
      "InputParams": {
        "operation": {
          "VarKey": null,
          "Value": "newWorkbook"
        },
        "fileType": {
          "VarKey": null,
          "Value": "XSSF"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "workbook": "workbook"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "演示选中某个工作簿"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:excelreadwrite",
      "InputParams": {
        "operation": {
          "VarKey": null,
          "Value": "getSheetByName"
        },
        "workbook": {
          "VarKey": "workbook",
          "Value": null
        },
        "sheetName": {
          "VarKey": null,
          "Value": "Sheet1"
        },
        "createSheetIfNotExist": {
          "VarKey": null,
          "Value": "1"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "sheet": "worksheet",
        "firstRow": null,
        "lastRow": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "生成乘法口诀"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:repeat",
      "InputParams": {
        "count": {
          "VarKey": null,
          "Value": "9"
        },
        "stopCondition": {
          "VarKey": null,
          "Value": ""
        },
        "startIndex": {
          "VarKey": null,
          "Value": "1"
        },
        "repeatDelayMs": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "count": "x"
      },
      "IfSteps": [
        {
          "StepRunnerKey": "sys:repeat",
          "InputParams": {
            "count": {
              "VarKey": "x",
              "Value": null
            },
            "stopCondition": {
              "VarKey": null,
              "Value": ""
            },
            "startIndex": {
              "VarKey": null,
              "Value": "1"
            },
            "repeatDelayMs": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "count": "y"
          },
          "IfSteps": [
            {
              "StepRunnerKey": "sys:excelreadwrite",
              "InputParams": {
                "operation": {
                  "VarKey": null,
                  "Value": "setCell"
                },
                "worksheet": {
                  "VarKey": "worksheet",
                  "Value": null
                },
                "cellAddress": {
                  "VarKey": null,
                  "Value": ""
                },
                "rowIndex": {
                  "VarKey": null,
                  "Value": "$= {x}-1"
                },
                "cellIndex": {
                  "VarKey": null,
                  "Value": "$= {y}-1"
                },
                "cellType": {
                  "VarKey": null,
                  "Value": ""
                },
                "cellValue": {
                  "VarKey": null,
                  "Value": "$= {y}.ToString() + \" X \" + {x}.ToString() + \" = \" + ({x}*{y}).ToString()"
                },
                "dataFormat": {
                  "VarKey": null,
                  "Value": ""
                },
                "cellLink": {
                  "VarKey": null,
                  "Value": ""
                },
                "stopIfFail": {
                  "VarKey": null,
                  "Value": "1"
                }
              },
              "OutputParams": {
                "isSuccess": null
              },
              "IfSteps": null,
              "ElseSteps": null,
              "Note": "",
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            }
          ],
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "示例：调用NPOI方法"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:assign",
      "InputParams": {
        "input": {
          "VarKey": null,
          "Value": "$={worksheet}.SetColumnWidth(1, 50*256)"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "output": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "保存并关闭工作簿"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:GenTempFilePath",
      "InputParams": {
        "ext": {
          "VarKey": null,
          "Value": ".xlsx"
        }
      },
      "OutputParams": {
        "filePath": "filePath"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:excelreadwrite",
      "InputParams": {
        "operation": {
          "VarKey": null,
          "Value": "save"
        },
        "filePath": {
          "VarKey": "filePath",
          "Value": null
        },
        "workbook": {
          "VarKey": "workbook",
          "Value": null
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:run",
      "InputParams": {
        "path": {
          "VarKey": "filePath",
          "Value": null
        },
        "arg": {
          "VarKey": null,
          "Value": ""
        },
        "runas": {
          "VarKey": null,
          "Value": "false"
        },
        "alternativePath": {
          "VarKey": null,
          "Value": ""
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        },
        "setWorkingDir": {
          "VarKey": null,
          "Value": "1"
        },
        "windowStyle": {
          "VarKey": null,
          "Value": "0"
        },
        "waitInputIdle": {
          "VarKey": null,
          "Value": "false"
        },
        "waitExit": {
          "VarKey": null,
          "Value": "false"
        },
        "username": {
          "VarKey": null,
          "Value": ""
        },
        "password": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "pid": null,
        "mainWinHandle": null,
        "mainWinTitle": null,
        "stdout": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:excelObjects",
      "InputParams": {
        "operation": {
          "VarKey": null,
          "Value": "SaveWorkbook"
        },
        "path": {
          "VarKey": null,
          "Value": "d:\\test.xlsx"
        },
        "workbook": {
          "VarKey": "workbook",
          "Value": null
        },
        "params": {
          "VarKey": null,
          "Value": "CloseApplication=false"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": "isSuccess"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": true,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```

**从Excel表格中，根据某一列的特定值提取数据并显示。数据存放在Excel的第一个sheet中；第一行为标题行。标题前后不要有空格（最好中间也不要有）。首次使用时会弹窗进行动作设置（也可在动作右键菜单中选择设置）。未选中内容时，在弹出的输入框中输入值查询。查询内容中，可以使用%表示模糊匹配的通配符。 如果没有此符号，则使用精确匹配。**
```json
{
  "Variables": [
    {
      "Key": "filePath",
      "Type": 0,
      "Desc": "文件路径",
      "DefaultValue": "",
      "SaveState": true,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "checkField",
      "Type": 0,
      "Desc": "要判断的列名",
      "DefaultValue": "",
      "SaveState": true,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "checkValue",
      "Type": 0,
      "Desc": "搜索的字段值",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "table",
      "Type": 13,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "rows",
      "Type": 99,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "tableClone",
      "Type": 13,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "rowCount",
      "Type": 12,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "isSelected",
      "Type": 2,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "尝试获取选中的内容"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:getSelectedText",
      "InputParams": {
        "format": {
          "VarKey": null,
          "Value": "UnicodeText"
        },
        "waitMs": {
          "VarKey": null,
          "Value": "450"
        },
        "repeat": {
          "VarKey": null,
          "Value": "0"
        },
        "trim": {
          "VarKey": null,
          "Value": "1"
        },
        "useActionParam": {
          "VarKey": null,
          "Value": "0"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {
        "isSuccess": "isSelected",
        "output": "checkValue",
        "outputEncoded": null,
        "url": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "设置（右键菜单，或者文件不存在时）"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:simpleIf",
      "InputParams": {
        "condition": {
          "VarKey": null,
          "Value": "$= {quicker_in_param} == \"settings\" || File.Exists({filePath}) == false"
        }
      },
      "OutputParams": {},
      "IfSteps": [
        {
          "StepRunnerKey": "sys:form",
          "InputParams": {
            "title": {
              "VarKey": null,
              "Value": "动作设置"
            },
            "formDef": {
              "VarKey": null,
              "Value": "{\"Fields\":[{\"FieldKey\":\"filePath\",\"Label\":\"Excel文件路径\",\"HelpText\":\"文件需要是一个规范的表格，在第一个Sheet中第一行为表头，下面行为数据\",\"HelpLink\":null,\"InputMethod\":1,\"SelectionItems\":\"\",\"IsRequired\":true,\"MinValue\":\"\",\"MaxValue\":\"\",\"Pattern\":\"\",\"MaxLength\":0,\"ImeState\":null,\"TextTools\":\"SelectSingleFile\",\"VisibleExpression\":\"\"},{\"FieldKey\":\"checkField\",\"Label\":\"查找的字段\",\"HelpText\":\"根据哪个字段的值定位行数据\",\"HelpLink\":null,\"InputMethod\":1,\"SelectionItems\":\"\",\"IsRequired\":true,\"MinValue\":\"\",\"MaxValue\":\"\",\"Pattern\":\"\",\"MaxLength\":0,\"ImeState\":null,\"TextTools\":\"\",\"VisibleExpression\":\"\"}]}"
            },
            "help": {
              "VarKey": null,
              "Value": ""
            },
            "titleColumnWidth": {
              "VarKey": null,
              "Value": "100"
            },
            "windowWidth": {
              "VarKey": null,
              "Value": "500"
            },
            "restoreFocus": {
              "VarKey": null,
              "Value": "0"
            },
            "topMost": {
              "VarKey": null,
              "Value": "false"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            },
            "markdownhelp": {
              "VarKey": null,
              "Value": ""
            }
          },
          "OutputParams": {
            "isSuccess": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": [],
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "如果没有选中内容，则输入要搜索的值"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:simpleIf",
      "InputParams": {
        "condition": {
          "VarKey": null,
          "Value": "$={checkValue}.IsNullOrEmpty()"
        }
      },
      "OutputParams": {},
      "IfSteps": [
        {
          "StepRunnerKey": "sys:userInput",
          "InputParams": {
            "type": {
              "VarKey": null,
              "Value": "text"
            },
            "prompt": {
              "VarKey": null,
              "Value": "$$请输入查询的值({checkField} = ?)"
            },
            "defaultValue": {
              "VarKey": null,
              "Value": ""
            },
            "pattern": {
              "VarKey": null,
              "Value": ""
            },
            "isRequired": {
              "VarKey": null,
              "Value": "0"
            },
            "restoreFocus": {
              "VarKey": null,
              "Value": "1"
            },
            "closeOnDeactivated": {
              "VarKey": null,
              "Value": "0"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            },
            "texttools": {
              "VarKey": null,
              "Value": ""
            },
            "fontfamily": {
              "VarKey": null,
              "Value": ""
            },
            "fontsize": {
              "VarKey": null,
              "Value": "14"
            },
            "winLocation": {
              "VarKey": null,
              "Value": "CenterScreen"
            },
            "imeState": {
              "VarKey": null,
              "Value": "NO_CONTROL"
            },
            "help": {
              "VarKey": null,
              "Value": ""
            }
          },
          "OutputParams": {
            "isSuccess": null,
            "textValue": "checkValue",
            "isEmpty": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "从excel表中加载数据"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:tableoperation",
      "InputParams": {
        "table": {
          "VarKey": "table",
          "Value": null
        },
        "type": {
          "VarKey": null,
          "Value": "importExcel"
        },
        "excelFilePath": {
          "VarKey": "filePath",
          "Value": null
        },
        "sheetName": {
          "VarKey": null,
          "Value": ""
        },
        "startRowNum": {
          "VarKey": null,
          "Value": "1"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "rowCount": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "筛选结果"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:tableoperation",
      "InputParams": {
        "table": {
          "VarKey": "table",
          "Value": null
        },
        "type": {
          "VarKey": null,
          "Value": "select"
        },
        "filterExpression": {
          "VarKey": null,
          "Value": "$=\r\n// 如果包含%，进行模糊匹配。\r\nvar op = {checkValue}.Contains(\"%\") ? \" LIKE \" : \" = \";\r\n\r\nreturn \"[\" + {checkField} + \"]\" + op + \"'\" + {checkValue}.Trim() + \"'\";"
        },
        "sort": {
          "VarKey": null,
          "Value": ""
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "rows": "rows",
        "firstRow": null,
        "rowCount": "rowCount",
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "将筛选结果放入新表"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:assign",
      "InputParams": {
        "input": {
          "VarKey": null,
          "Value": "$=DataTable table = {table}.Clone();\r\n\r\nforeach(DataRow row in {rows}){\r\n\ttable.ImportRow(row);\r\n}\r\n\r\nreturn table;"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "output": "tableClone"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "显示结果"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:tableoperation",
      "InputParams": {
        "table": {
          "VarKey": "tableClone",
          "Value": null
        },
        "type": {
          "VarKey": null,
          "Value": "manage"
        },
        "gridSelectionMode": {
          "VarKey": null,
          "Value": "Cells"
        },
        "isReadOnly": {
          "VarKey": null,
          "Value": "1"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "selectedRows": null,
        "rowCount": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

## 116.Shell文件操作

**功能描述**
> 针对文件的Windows Shell相关操作

**官方文档**
> https://getquicker.net/KC/Help/Doc/shelloperation

**内部名称**
> sys:shelloperation

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| operation | 操作类型 |  | (9)选项-Enum（getverb: 获取文件的可用动词列表（verb）; ） | getverb: 获取文件的可用动词列表（verb）; execverb: 对文件执行动词（verb）; gettitles: 获取文件的可用菜单标题列表; execbytitle: 对文件执行菜单（指定菜单标题）; showmenu: 显示系统上下文菜单 | True |
| pathOrExt | 文件路径或扩展名 | 需要获取可用动词的文件类型，可使用扩展名如.txt或提供完整文件名。 | (0)字符串-Text | .txt | False |
| pathList | 文件路径列表 | 要操作文件的完整路径的列表。每个文件将会被依次调用 | (4)文本列表-List |  | False |
| verb | 动词 | Shell操作动词，需要在当前电脑上支持才能正常运行。 | (0)字符串-Text |  | False |
| title | 菜单标题 | 菜单上的标题文字，需要准确匹配。 | (0)字符串-Text |  | False |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| verbs | 动词列表 | 每项格式为：描述文字|动词 | (4)文本列表-List |
| titles | 菜单标题列表 |  | (4)文本列表-List |

</details>
<details>
<summary>范例</summary>

**批量打印文件**
```json
{
  "Variables": [
    {
      "Key": "filePaths",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:shelloperation",
      "InputParams": {
        "operation": {
          "VarKey": null,
          "Value": "execverb"
        },
        "pathList": {
          "VarKey": "filePaths",
          "Value": null
        },
        "verb": {
          "VarKey": null,
          "Value": "print"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```

**选择文件后，使用此动作，获得该文件所支持的Shell菜单信息。**
```json
{
  "Variables": [
    {
      "Key": "files",
      "Type": 4,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "verbs",
      "Type": 4,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "titles",
      "Type": 4,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:getSelectedFiles",
      "InputParams": {
        "operation": {
          "VarKey": null,
          "Value": "getSelection"
        },
        "waitMs": {
          "VarKey": null,
          "Value": "200"
        },
        "sortType": {
          "VarKey": null,
          "Value": "Default"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "files": "files",
        "firstFile": null,
        "fileNames": null,
        "firstFileName": null,
        "fileCount": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:shelloperation",
      "InputParams": {
        "operation": {
          "VarKey": null,
          "Value": "getverb"
        },
        "pathOrExt": {
          "VarKey": "files",
          "Value": null
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "verbs": "verbs"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:shelloperation",
      "InputParams": {
        "operation": {
          "VarKey": null,
          "Value": "gettitles"
        },
        "pathOrExt": {
          "VarKey": "files",
          "Value": null
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "titles": "titles"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:showText",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "NO_WAIT"
        },
        "text": {
          "VarKey": null,
          "Value": "$$动词：\r\n{verbs}\r\n\r\n\r\n标题：\r\n{titles}"
        },
        "title": {
          "VarKey": null,
          "Value": "结果内容"
        },
        "autoCloseKey": {
          "VarKey": null,
          "Value": "="
        },
        "topMost": {
          "VarKey": null,
          "Value": "false"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        },
        "operations": {
          "VarKey": null,
          "Value": ""
        },
        "winLocation": {
          "VarKey": null,
          "Value": "CenterScreen"
        },
        "winSize": {
          "VarKey": null,
          "Value": ""
        },
        "fontsize": {
          "VarKey": null,
          "Value": "14"
        },
        "fontfamily": {
          "VarKey": null,
          "Value": ""
        },
        "bgColor": {
          "VarKey": null,
          "Value": ""
        },
        "textColor": {
          "VarKey": null,
          "Value": ""
        },
        "highlight": {
          "VarKey": null,
          "Value": ""
        },
        "autoSaveToState": {
          "VarKey": null,
          "Value": ""
        },
        "closeWhenLostFocus": {
          "VarKey": null,
          "Value": "false"
        },
        "showLineNum": {
          "VarKey": null,
          "Value": "true"
        },
        "autoWrap": {
          "VarKey": null,
          "Value": "true"
        },
        "showBuildInToolbar": {
          "VarKey": null,
          "Value": "true"
        },
        "copyWholeLine": {
          "VarKey": null,
          "Value": "false"
        },
        "caretPosition": {
          "VarKey": null,
          "Value": "0"
        },
        "updateIfExists": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "windowHandle": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:shelloperation",
      "InputParams": {
        "operation": {
          "VarKey": null,
          "Value": "execbytitle"
        },
        "pathList": {
          "VarKey": "files",
          "Value": null
        },
        "title": {
          "VarKey": null,
          "Value": "邮件收件人"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```

</details>

***

## 117.表格数据操作

**功能描述**
> 表格变量的相关处理操作

**官方文档**
> https://getquicker.net/KC/Help/Doc/tableoperation

**内部名称**
> sys:tableoperation

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| table | 表格变量 | 要操作的表格变量 | (13)表格-Table |  | True |
| type | 操作类型 |  | (9)选项-Enum（info: 获取信息; addRow: 添加行; update: 更新行; manage: 查看或编辑数据; select: 查询或筛选行（Select）; clear: 清除所有行; deleteRows: 删除符合条件的行; deleteColumns: 删除列; importCsv: 从CSV文本加载数据; importJson: 从Json文本加载数据; importExcel: 从Excel工作表加载数据; export_text: 导出文本数据; exportExcel: 导出Excel文件） | True |
| rowData | 行数据 | 包含行数据的词典：更新行时，仅包含要更新的列的内容。 | (10)词典-Dict |  | false |
| filterExpression | 筛选表达式 |  | (0)字符串-Text |  | false |
| sort | 排序 |  | (0)字符串-Text |  | false |
| gridSelectionMode | 选择模式 | 注：单元格模式不支持返回选择的行。 | (9)选项-Enum（Cells: 单元格（类似Excel））; OneRow: 行：0行或1行; OneRowRequired: 行：1行（必选）; Rows: 行：0.1或多行; RowsRequired: 行：一行或多行（必选）） | Cells | false |
| isReadOnly | 只读模式 | 是否以只读模式打开 | (2)布尔值-Boolean |  | false |
| windowTitle | 窗口标题 |  | (0)字符串-Text | 表格数据 | false |
| helpText | 帮助文本 |  | (0)字符串-Text |  | false |
| winSize | 窗口尺寸/位置 | 设置选择窗口的最大尺寸，格式为：宽度，高度。。支持像素数值或屏幕宽高百分比，详情请参考模块文档。 | (0)字符串-Text |  | false |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| rows | 行列表 | 符合条件的行的数组 | | (99)任意类型-Any |
| columns | 列的列表 | 表格的列的信息列表（DataTable.Columns） | | (99)任意类型-Any |
| rowCount | 行数 | 表格内的数据行数 | (12)数字(整数)-Integer |
| firstRow | 第一行/结果行 | 第一个符合条件的行或新添加的行，可输出为词典对象 | (99)任意类型-Any |
| affectedRowCount | 影响行数 | 更新或删除、筛选的行数 | (0)字符串-Text |
| isConfirmed | 是否确认 | 是否点击了确认按钮 | (2)布尔值-Boolean |
| selectedRows | 选择的行列表 | 选择的所有行的列表 | (99)任意类型-Any |

</details>
<details>
<summary>范例</summary>

**根据汇总表和模板表将汇总表中的每行数据填充到模板中生成Excel文件。**
```json
{
  "Variables": [
    {
      "Key": "dataSourceFilePath",
      "Type": 0,
      "Desc": "汇总表路径",
      "DefaultValue": "E:\\CloudStation\\Drive\\Quicker\\_docs\\表格读写测试文件\\总表.xlsx",
      "SaveState": true,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "templateFilePath",
      "Type": 0,
      "Desc": "模板文件路径",
      "DefaultValue": "E:\\CloudStation\\Drive\\Quicker\\_docs\\表格读写测试文件\\模板.xlsx",
      "SaveState": true,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "outputFolder",
      "Type": 0,
      "Desc": "输出文件路径",
      "DefaultValue": "E:\\CloudStation\\Drive\\Quicker\\_docs\\表格读写测试文件\\输出",
      "SaveState": true,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "fileNameField",
      "Type": 0,
      "Desc": "文件名列",
      "DefaultValue": "%Index",
      "SaveState": true,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "autoDeleteOld",
      "Type": 2,
      "Desc": "是否删除旧文件",
      "DefaultValue": "1",
      "SaveState": true,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "table",
      "Type": 13,
      "Desc": "总表",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "rowCount",
      "Type": 12,
      "Desc": "行数",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "rowIndex",
      "Type": 12,
      "Desc": "行号",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "rowDict",
      "Type": 10,
      "Desc": "每一行数据的词典",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "rowFilePath",
      "Type": 0,
      "Desc": "对某一行数据生成的目标路径",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "workbook",
      "Type": 99,
      "Desc": "工作簿",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "sheet",
      "Type": 99,
      "Desc": "工作表",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "autoPrint",
      "Type": 2,
      "Desc": "",
      "DefaultValue": "0",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "每次启动时允许用户选择模板和总表文件。"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:form",
      "InputParams": {
        "title": {
          "VarKey": null,
          "Value": "填写表单"
        },
        "formDef": {
          "VarKey": null,
          "Value": "{\"Fields\":[{\"FieldKey\":\"dataSourceFilePath\",\"Label\":\"汇总表路径\",\"HelpText\":\"第一个工作表存储汇总数据。第一行为列名，列名单元格里面不要有空格。\",\"HelpLink\":null,\"InputMethod\":1,\"SelectionItems\":\"\",\"IsRequired\":true,\"MinValue\":\"\",\"MaxValue\":\"\",\"Pattern\":\"\",\"MaxLength\":0,\"ImeState\":null,\"TextTools\":\"SelectSingleFile\",\"VisibleExpression\":\"\"},{\"FieldKey\":\"templateFilePath\",\"Label\":\"模板文件路径\",\"HelpText\":\"模板文件中使用{{列名}}作为待替换的占位符。\",\"HelpLink\":null,\"InputMethod\":1,\"SelectionItems\":\"\",\"IsRequired\":true,\"MinValue\":\"\",\"MaxValue\":\"\",\"Pattern\":\"\",\"MaxLength\":0,\"ImeState\":null,\"TextTools\":\"SelectSingleFile\",\"VisibleExpression\":\"\"},{\"FieldKey\":\"outputFolder\",\"Label\":\"输出文件路径\",\"HelpText\":\"输出文件保存的目录，需清理里面的文件避免生成失败。\",\"HelpLink\":null,\"InputMethod\":1,\"SelectionItems\":\"\",\"IsRequired\":true,\"MinValue\":\"\",\"MaxValue\":\"\",\"Pattern\":\"\",\"MaxLength\":0,\"ImeState\":null,\"TextTools\":\"SelectSingleFolder\",\"VisibleExpression\":\"\"},{\"FieldKey\":\"fileNameField\",\"Label\":\"文件名列名\",\"HelpText\":\"指定作为文件名的列。%Index表示行序号。\",\"HelpLink\":null,\"InputMethod\":1,\"SelectionItems\":\"\",\"IsRequired\":true,\"MinValue\":\"\",\"MaxValue\":\"\",\"Pattern\":\"\",\"MaxLength\":0,\"ImeState\":null,\"TextTools\":\"\",\"VisibleExpression\":\"\"},{\"FieldKey\":\"autoDeleteOld\",\"Label\":\"自动删除旧文件\",\"HelpText\":\"如果输出位置已经存在旧文件会造成失败。\",\"HelpLink\":null,\"InputMethod\":6,\"SelectionItems\":\"\",\"IsRequired\":false,\"MinValue\":\"\",\"MaxValue\":\"\",\"Pattern\":\"\",\"MaxLength\":0,\"ImeState\":null,\"TextTools\":\"\",\"VisibleExpression\":\"\"},{\"FieldKey\":\"autoPrint\",\"Label\":\"自动打印\",\"HelpText\":\"自动打印生成的文件（本选项不保存）\",\"HelpLink\":null,\"InputMethod\":6,\"SelectionItems\":\"\",\"IsRequired\":false,\"MinValue\":\"\",\"MaxValue\":\"\",\"Pattern\":\"\",\"MaxLength\":0,\"ImeState\":null,\"TextTools\":\"\",\"VisibleExpression\":\"\"}]}"
        },
        "help": {
          "VarKey": null,
          "Value": "请设置好停止动作快捷键，以便于出现异常情况的时候停止动作。"
        },
        "titleColumnWidth": {
          "VarKey": null,
          "Value": "100"
        },
        "windowWidth": {
          "VarKey": null,
          "Value": "700"
        },
        "restoreFocus": {
          "VarKey": null,
          "Value": "0"
        },
        "topMost": {
          "VarKey": null,
          "Value": "false"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        },
        "markdownhelp": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {
        "isSuccess": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "将汇总表加载到表格中"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:tableoperation",
      "InputParams": {
        "table": {
          "VarKey": "table",
          "Value": null
        },
        "type": {
          "VarKey": null,
          "Value": "importExcel"
        },
        "excelFilePath": {
          "VarKey": "dataSourceFilePath",
          "Value": null
        },
        "sheetName": {
          "VarKey": null,
          "Value": ""
        },
        "startRowNum": {
          "VarKey": null,
          "Value": "1"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "rowCount": "rowCount"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "遍历表格的每一行，将数据写入rawDict中，并对该行数据进行处理"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:each",
      "InputParams": {
        "input": {
          "VarKey": null,
          "Value": "$={table}.Rows"
        },
        "useMultiThread": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {
        "item": "rowDict",
        "count": "rowIndex"
      },
      "IfSteps": [
        {
          "StepRunnerKey": "sys:comment",
          "InputParams": {
            "note": {
              "VarKey": null,
              "Value": "生成输出文件的完整路径"
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:assign",
          "InputParams": {
            "input": {
              "VarKey": null,
              "Value": "$= \r\nvar fileName = {fileNameField} == \"%Index\" \r\n\t? ({rowIndex} + 2).ToString()\r\n\t: {rowDict}[{fileNameField}];\r\n\t\r\nreturn Path.Combine({outputFolder}, fileName +\".xlsx\");\t"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "isSuccess": null,
            "output": "rowFilePath"
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:comment",
          "InputParams": {
            "note": {
              "VarKey": null,
              "Value": "根据设定，删除可能存在的旧文件"
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:simpleIf",
          "InputParams": {
            "condition": {
              "VarKey": "autoDeleteOld",
              "Value": null
            }
          },
          "OutputParams": {},
          "IfSteps": [
            {
              "StepRunnerKey": "sys:fileOperation",
              "InputParams": {
                "type": {
                  "VarKey": null,
                  "Value": "deleteFile"
                },
                "path": {
                  "VarKey": "rowFilePath",
                  "Value": null
                },
                "stopIfFail": {
                  "VarKey": null,
                  "Value": "0"
                }
              },
              "OutputParams": {
                "isSuccess": null
              },
              "IfSteps": null,
              "ElseSteps": null,
              "Note": "",
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            }
          ],
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:comment",
          "InputParams": {
            "note": {
              "VarKey": null,
              "Value": "将模板复制一份"
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:fileOperation",
          "InputParams": {
            "type": {
              "VarKey": null,
              "Value": "copyTo"
            },
            "path": {
              "VarKey": "templateFilePath",
              "Value": null
            },
            "dstPath": {
              "VarKey": "rowFilePath",
              "Value": null
            },
            "overwrite": {
              "VarKey": null,
              "Value": "0"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "isSuccess": null,
            "resultPath": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:comment",
          "InputParams": {
            "note": {
              "VarKey": null,
              "Value": "读取结果文件（模板复制出来的一个副本）"
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:excelreadwrite",
          "InputParams": {
            "operation": {
              "VarKey": null,
              "Value": "load"
            },
            "filePath": {
              "VarKey": "rowFilePath",
              "Value": null
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "isSuccess": null,
            "workbook": "workbook",
            "numberOfSheets": null,
            "worksheetNameList": null,
            "sheet": "sheet",
            "firstRow": null,
            "lastRow": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:comment",
          "InputParams": {
            "note": {
              "VarKey": null,
              "Value": "将行数据填充到文件中"
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:excelreadwrite",
          "InputParams": {
            "operation": {
              "VarKey": null,
              "Value": "batchReplace"
            },
            "worksheet": {
              "VarKey": "sheet",
              "Value": null
            },
            "replaceDict": {
              "VarKey": "rowDict",
              "Value": null
            },
            "replacePrefixSuffix": {
              "VarKey": null,
              "Value": "{{\r\n}}"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "isSuccess": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:comment",
          "InputParams": {
            "note": {
              "VarKey": null,
              "Value": "保存文件"
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:excelreadwrite",
          "InputParams": {
            "operation": {
              "VarKey": null,
              "Value": "save"
            },
            "filePath": {
              "VarKey": null,
              "Value": ""
            },
            "workbook": {
              "VarKey": "workbook",
              "Value": null
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "isSuccess": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:comment",
          "InputParams": {
            "note": {
              "VarKey": null,
              "Value": "根据设定打印文件"
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:simpleIf",
          "InputParams": {
            "condition": {
              "VarKey": "autoPrint",
              "Value": null
            }
          },
          "OutputParams": {},
          "IfSteps": [
            {
              "StepRunnerKey": "sys:shelloperation",
              "InputParams": {
                "operation": {
                  "VarKey": null,
                  "Value": "execverb"
                },
                "pathList": {
                  "VarKey": "rowFilePath",
                  "Value": null
                },
                "verb": {
                  "VarKey": null,
                  "Value": "print"
                },
                "stopIfFail": {
                  "VarKey": null,
                  "Value": "1"
                }
              },
              "OutputParams": {
                "isSuccess": null
              },
              "IfSteps": null,
              "ElseSteps": null,
              "Note": "",
              "Disabled": false,
              "Collapsed": false,
              "DelayMs": 0
            }
          ],
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        },
        {
          "StepRunnerKey": "sys:break",
          "InputParams": {},
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": null,
          "Disabled": true,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:notify",
      "InputParams": {
        "msg": {
          "VarKey": null,
          "Value": "完成"
        },
        "maxLines": {
          "VarKey": null,
          "Value": "0"
        },
        "type": {
          "VarKey": null,
          "Value": "Info"
        },
        "clickAction": {
          "VarKey": null,
          "Value": ""
        },
        "style": {
          "VarKey": null,
          "Value": "Default"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "打开输出文件所在的文件夹"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:run",
      "InputParams": {
        "path": {
          "VarKey": "outputFolder",
          "Value": null
        },
        "arg": {
          "VarKey": null,
          "Value": ""
        },
        "runas": {
          "VarKey": null,
          "Value": "false"
        },
        "alternativePath": {
          "VarKey": null,
          "Value": ""
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        },
        "setWorkingDir": {
          "VarKey": null,
          "Value": "1"
        },
        "windowStyle": {
          "VarKey": null,
          "Value": "0"
        },
        "waitInputIdle": {
          "VarKey": null,
          "Value": "false"
        },
        "waitExit": {
          "VarKey": null,
          "Value": "false"
        },
        "username": {
          "VarKey": null,
          "Value": ""
        },
        "password": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "pid": null,
        "mainWinHandle": null,
        "mainWinTitle": null,
        "stdout": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```

</details>

***

## 118.自定义窗口

**功能描述**
> 创建和显示自定义窗口

**官方文档**
> https://getquicker.net/KC/Help/Doc/customwindow

**内部名称**
> sys:customwindow

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| type | 操作类型 |  | (9)选项-Enum（ShowAndWaitClose: 显示窗口并等待关闭; Show: 显示窗口; Close: 关闭窗口; GetWindows: 获取窗口列表） | ShowAndWaitClose | true |
| windowMarkup | 窗口XAML代码 | 窗口定义XAML代码 | (0)字符串-Text | <Window xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"<br>        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"<br>        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"<br>        xmlns:hc="https://handyorg.github.io/handycontrol"<br>        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"<br>        xmlns:qk="https://getquicker.net"<br>        Width="637"<br>        Height="556"<br>        Title="Test Window"<br>        mc:Ignorable="d"><br>  <Grid Margin="10"><br>    <StackPanel><br>      <TextBlock Margin="10,50,10,50" Text="Hello World！" FontSize="20" /><br>     <br>      <Button Margin="10" qk:Att.Action="close:result" Style="{StaticResource ButtonPrimary}" Width="50"><br>        关闭<br>      </Button><br>    </StackPanel><br>  </Grid><br></Window> | false |
| dataMapping | 数据映射 | 将变量与窗口上下文数据进行映射。每行一个，格式为："窗口数据项名称：{动作变量名}”或“窗口数据项：=表达式” | (0)字符串-Text |  | false |
| windowId | 窗口标识 | 如需单独的步骤关闭窗口，需使用标识查找窗口。 | (0)字符串-Text |  | false |
| closeWhenDeactivate | 失去焦点后关闭窗口 |  | (9)选项-Enum | false | false |
| cscode | 辅助C#代码 | 辅助处理窗口事件的代码 | (0)字符串-Text |  | false |
| events | 事件 |  | (0)字符串-Text |  | false |
| autoCloseTime | 自动关闭时间（秒） | 自动关闭窗口的时间（秒数）。需大于0.5秒。 | (1)数字(小数)-Number | 0 | false |
| activateMode | 激活模式 |  | (9)选项-Enum（NotActivatable: 不支持激活（不占用焦点，仅能使用鼠标操作）; NotActivatableMouseThrough: 不支持激活，鼠标穿透; NotActivated: 支持激活，打开时不抢占焦点; AutoActivate: 支持激活，打开时抢占焦点） | AutoActivate | false |
| winLocation | 窗口位置 |  | (9)选项-Enum | CenterScreen | false |
| winSize | 窗口尺寸/位置 | 设置选择窗口的最大尺寸，格式为：宽度,高度。支持像素数值或屏幕宽高百分比例如30%,50%代表屏幕宽度的30%和屏幕高度的50%。“窗口位置”类型为“自定义位置”时用于指定显示位置，格式为：left,top,right,bottom | (0)字符串-Text |  | false |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| result | 窗口结果 | 通过close:result返回的结果 | (0)字符串-Text |
| windowLocation | 关闭时窗口位置 |  | (0)字符串-Text |
| windowHandle | 窗口句柄 |  | (12)数字(整数)-Integer |
| windowList | 窗口对象列表 | IList<Window>对象 | (99)任意类型-Any |

</details>

***

## 119.自定义操作窗

**功能描述**
> 自定义悬浮操作窗口，点击后直接执行操作，不隐藏。

**官方文档**
> https://getquicker.net/KC/Help/Doc/custompanel

**内部名称**
> sys:custompanel

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| operation | 操作类型 |  | (9)选项-Enum | show_fixed_panel（show_fixed_panel: 显示操作窗; show_fixed_panel_wait_close: 显示操作窗并等待关闭; close_fixed_panel: 关闭操作窗; toggle_collapse: 切换展开状态; get_panel_info: 获取操作窗状态） | true |
| operationData | 操作项定义 | 可以为Json/菜单文本格式/IList<CommonOperationltem>对象，详情请参考文档 | (0)字符串-Text |  | false |
| defaultOperation | 默认Operation | 默认的Operation值或参数组合。提供此值时，操作项可以直接通过“[图标]标题(提示)data”的形式定义。 | (0)字符串-Text |  | false |
| spacingStr | 按钮之间的间隔 | 可选格式1：5=>四个边都是5；格式2：10,5=>左右10，上下5； | (0)字符串-Text | 5 | false |
| buttonPadding | 按钮内边距 | 格式1：5=>四个边都是5；格式2：10,5=>左右10，上下5；格式3：7,8，9，10=>分别指定左上右下4边边距。 | (0)字符串-Text | 10,6 | false |
| columnCount | 列数 | 按钮排列方式为固定列数时，指定列数。0表示自动。 | (12)数字(整数)-Integer | 2 | false |
| columnWidth | 列宽 | 固定列宽时使用。0表示自动列宽，-1表示不对齐宽度，各子项根据内容自动调整宽度。 | (12)数字(整数)-Integer | 0 | false |
| groupMode | 分组方式 | 当包含子项时，第一级节点作为分组，第二级节点作为按钮。 | (9)选项-Enum（heading: 标题分组; expander: 可折叠的分组; tab-top: 标签页-顶部; tab-left: 标签页-左侧; tab-right: 标签页-右侧; tab-bottom: 标签页-底部; headingLeft: 多行; columns: 多列; none: 不分组） | heading | false |
| selectGroup | 选择标签分组 | 标签页分组时切换至设定的标签页标题，留空表示默认。 | (0)字符串-Text |  | false |
| title | 操作窗标题 | 标题文字，或"[图标]标题"格式。 | (0)字符串-Text |  | false |
| windowId | 窗口标识 | 如需单独的步骤关闭窗口，需使用标识查找窗口。可使用"="表示当前动作ID。 | (0)字符串-Text |  | false |
| buttonContextMenuData | 默认的按钮右键菜单 | 可以为Json/菜单文本格式/IList<CommonOperationltem>对象，详情请参考文档 | (0)字符串-Text |  | false |
| winLocation | 窗口位置 |  | (9)选项-Enum | CenterScreen | false |
| winSize | 窗口尺寸/位置 | 设置选择窗口的最大尺寸，格式为：宽度,高度。支持像素数值或屏幕宽高百分比例如30%,50%代表屏幕宽度的30%和屏幕高度的50%。“窗口位置”类型为“自定义位置”时用于指定显示位置，格式为：left,top,right,bottom | (0)字符串-Text |  | false |
| saveState | 记忆位置等状态 | 多次使用操作窗时，保持上一次所在位置和分组 | (2)布尔值-Boolean | 1 | false |
| horzAlign | 按钮内容对齐方式 |  | (9)选项-Enum（Center: 居中; Left: 左侧; Right: 右侧） | Center | false |
| bgColor | 背景颜色 |  | (0)字符串-Text |  | false |
| btnColor | 按钮颜色 |  | (0)字符串-Text |  | false |
| btnBorderColor | 按钮边框颜色 |  | (0)字符串-Text |  | false |
| fontColor | 字体颜色 |  | (0)字符串-Text |  | false |
| fontsize | 字体大小 |  | (12)数字(整数)-Integer | 12 | false |
| iconsize | 图标大小 | 图标的宽度/高度像素数 | (12)数字(整数)-Integer | 16 | false |
| contextMenuData | 窗口右键菜单 | 可以为Json/菜单文本格式/IList<CommonOperationltem>对象，详情请参考文档 | (0)字符串-Text |  | false |
| bindProc | 自动关联到进程 | 要关联的进程名称，输入”-“禁用此功能。当该进程为前台时显示操作窗，否则自动隐藏。 | (0)字符串-Text |  | false |
| autoCollapse | 自动折叠 |  | (9)选项-Enum（false: 关闭; 1: 开启） | 0 | false |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| winHandle | 窗口句柄 | 操作窗的窗口句柄 | (12)数字(整数)-Integer |
| selectedItemData | 选择的操作项数据 | 选择的操作项的data属性数据 | (0)字符串-Text |
| selectedItem | 选择的操作项 | 选择的操作项的CommonOperationltem对象 | (99)任意类型-Any |
| currentGroup | 当前标签分组 | 当使用标签分组显示时，关闭窗口时所停留的标签分组名称。 | (99)任意类型-Any |
| buttonItemData | 按钮操作项数据 | 点击的是按钮的菜单时，所对应按钮的操作项Data数据 | (0)字符串-Text |
| buttonItem | 按钮操作项 | 点击的是按钮的菜单时，所对应按钮的CommonOperationltem对象 | (99)任意类型-Any |
| isWindowVisible | 窗口是否可见 | 可能会因为关联进程而隐藏 | (2)布尔值-Boolean |
| isWindowExpanded | 窗口是否展开 |  | (2)布尔值-Boolean |

</details>
<details>
<summary>范例</summary>

**范例1**
```json

```

</details>

***

## 120.数据库查询

**功能描述**
> 对数据库执行SQL语句并返回结果

**官方文档**
> https://getquicker.net/KC/Help/Doc/dboperation

**内部名称**
> sys:dboperation

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| dbType | 数据库连接类型 |  | (9)选项-Enum（sqlserver: SQL Server; mysql: MySQL; sqlite: SQLite; oledb: OleDB; odbc: ODBC） |  | true |
| connectionString | 连接字符串 | Connection string | (0)字符串-Text |  | false |
| sql | SQL语句 | 要执行的SQL语句内容 | (0)字符串-Text |  | false |
| sqlParam | 参数 | 为SQL语句提供的参数 | (99)任意类型-Any |  | false |
| timeoutSeconds | 超时秒数 | 留空或0表示默认。 | (12)数字(整数)-Integer |  | false |
| operationType | 执行方式 |  | (9)选项-Enum（Query: Query：查询并返回结果数据; Execute: Execute：执行并返回影响的行数; ExecuteScalar: ExecuteScalar：执行并返回单个值（首行首列的值）） |  | false |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| dataTableResult | 查询结果(表格) | 获取表格类型的行结果 | (13)表格-Table |
| listResult | 查询结果(对象列表) | 获得动态对象列表类型的结果 | (99)任意类型-Any |
| firstItem | 首项结果 | 如果只需要返回结果的第一行，可以使用此项输出，支持词典或任意对象。没有结果时返回null。 | (99)任意类型-Any |
| rowCount | 结果行数 |  | (12)数字(整数)-Integer |
| rowsAffected | 影响行数 |  | (12)数字(整数)-Integer |
| scalarResult | 单值结果 |  | (0)字符串-Text |

</details>
<details>
<summary>范例</summary>

**使用SQLite，默认保存在d盘根目录**
```json
{
  "Variables": [
    {
      "Key": "firstItem",
      "Type": 10,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "item",
      "Type": 99,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "listResult",
      "Type": 99,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "path",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "d:\\quicker_test.db",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "rowCount",
      "Type": 12,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "rowsAffected",
      "Type": 12,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "scalarResult",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "table1",
      "Type": 13,
      "Desc": "表格测试",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": {
        "Fields": []
      },
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "tableRow",
      "Type": 99,
      "Desc": "DataTable的一行数据",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "temp",
      "Type": 2,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "创建数据库"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:fileOperation",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "deleteFile"
        },
        "path": {
          "VarKey": "path",
          "Value": null
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {
        "isSuccess": "temp"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:subprogram",
      "InputParams": {
        "subProgram": {
          "VarKey": null,
          "Value": "创建SQLite数据库文件"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        },
        "var:path": {
          "VarKey": "path",
          "Value": null
        },
        "summary": {
          "VarKey": null,
          "Value": "{path}"
        }
      },
      "OutputParams": {
        "isSuccess": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "创建表"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:dboperation",
      "InputParams": {
        "dbType": {
          "VarKey": null,
          "Value": "sqlite"
        },
        "connectionString": {
          "VarKey": "path",
          "Value": null
        },
        "sql": {
          "VarKey": null,
          "Value": "CREATE TABLE IF NOT EXISTS contacts (\r\n\tcontact_id INTEGER PRIMARY KEY,\r\n\tfirst_name TEXT NOT NULL,\r\n\tlast_name TEXT NOT NULL,\r\n\temail TEXT NOT NULL UNIQUE,\r\n\tphone TEXT NOT NULL UNIQUE\r\n);"
        },
        "sqlParam": {
          "VarKey": null,
          "Value": ""
        },
        "timeoutSeconds": {
          "VarKey": null,
          "Value": ""
        },
        "operationType": {
          "VarKey": null,
          "Value": "Execute"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "rowsAffected": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "插入一行数据，词典格式"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:dboperation",
      "InputParams": {
        "dbType": {
          "VarKey": null,
          "Value": "sqlite"
        },
        "connectionString": {
          "VarKey": "path",
          "Value": null
        },
        "sql": {
          "VarKey": null,
          "Value": "insert into contacts (first_name, last_name, email, phone) \r\nvalues(@FirstName, @LastName, @Email, @Phone)"
        },
        "sqlParam": {
          "VarKey": null,
          "Value": "FirstName:李\r\nLastName:四 \r\nEmail:lisi@getquicker.net\r\nPhone:13888889999"
        },
        "timeoutSeconds": {
          "VarKey": null,
          "Value": ""
        },
        "operationType": {
          "VarKey": null,
          "Value": "Execute"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "rowsAffected": "rowsAffected"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "插入一行数据，匿名对象"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:dboperation",
      "InputParams": {
        "dbType": {
          "VarKey": null,
          "Value": "sqlite"
        },
        "connectionString": {
          "VarKey": "path",
          "Value": null
        },
        "sql": {
          "VarKey": null,
          "Value": "insert into contacts (first_name, last_name, email, phone) \r\nvalues(@FirstName, @LastName, @Email, @Phone)"
        },
        "sqlParam": {
          "VarKey": null,
          "Value": "$= new {FirstName = \"王\", LastName=\"五\", Email=\"wangwu@getquicker.net\", Phone=\"13866666666\"}"
        },
        "timeoutSeconds": {
          "VarKey": null,
          "Value": ""
        },
        "operationType": {
          "VarKey": null,
          "Value": "Execute"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "rowsAffected": "rowsAffected"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "查询数据：全部。输出首项到一个词典变量。"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:dboperation",
      "InputParams": {
        "dbType": {
          "VarKey": null,
          "Value": "sqlite"
        },
        "connectionString": {
          "VarKey": "path",
          "Value": null
        },
        "sql": {
          "VarKey": null,
          "Value": "select * from contacts "
        },
        "sqlParam": {
          "VarKey": null,
          "Value": ""
        },
        "timeoutSeconds": {
          "VarKey": null,
          "Value": ""
        },
        "operationType": {
          "VarKey": null,
          "Value": "Query"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "dataTableResult": "table1",
        "listResult": "listResult",
        "firstItem": "firstItem",
        "rowCount": "rowCount"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:showText",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "WAIT"
        },
        "text": {
          "VarKey": null,
          "Value": "$=\r\n\"第一项结果的:\" + {firstItem}[\"first_name\"] + {firstItem}[\"last_name\"]"
        },
        "title": {
          "VarKey": null,
          "Value": "首项结果信息"
        },
        "topMost": {
          "VarKey": null,
          "Value": "false"
        },
        "operations": {
          "VarKey": null,
          "Value": ""
        },
        "autoCloseKey": {
          "VarKey": null,
          "Value": ""
        },
        "winLocation": {
          "VarKey": null,
          "Value": "CenterScreen"
        },
        "winSize": {
          "VarKey": null,
          "Value": ""
        },
        "fontsize": {
          "VarKey": null,
          "Value": "14"
        },
        "fontfamily": {
          "VarKey": null,
          "Value": ""
        },
        "bgColor": {
          "VarKey": null,
          "Value": ""
        },
        "textColor": {
          "VarKey": null,
          "Value": ""
        },
        "highlight": {
          "VarKey": null,
          "Value": ""
        },
        "autoSaveToState": {
          "VarKey": null,
          "Value": ""
        },
        "closeWhenLostFocus": {
          "VarKey": null,
          "Value": "false"
        },
        "showLineNum": {
          "VarKey": null,
          "Value": "true"
        },
        "autoWrap": {
          "VarKey": null,
          "Value": "true"
        },
        "showBuildInToolbar": {
          "VarKey": null,
          "Value": "true"
        },
        "copyWholeLine": {
          "VarKey": null,
          "Value": "false"
        }
      },
      "OutputParams": {
        "selectedOperation": null,
        "resultText": null,
        "selectedText": null,
        "windowPosition": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:showText",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "WAIT"
        },
        "text": {
          "VarKey": "table1",
          "Value": null
        },
        "title": {
          "VarKey": null,
          "Value": "表格赋值给文本"
        },
        "topMost": {
          "VarKey": null,
          "Value": "false"
        },
        "operations": {
          "VarKey": null,
          "Value": ""
        },
        "autoCloseKey": {
          "VarKey": null,
          "Value": ""
        },
        "winLocation": {
          "VarKey": null,
          "Value": "CenterScreen"
        },
        "winSize": {
          "VarKey": null,
          "Value": ""
        },
        "fontsize": {
          "VarKey": null,
          "Value": "14"
        },
        "fontfamily": {
          "VarKey": null,
          "Value": ""
        },
        "bgColor": {
          "VarKey": null,
          "Value": ""
        },
        "textColor": {
          "VarKey": null,
          "Value": ""
        },
        "highlight": {
          "VarKey": null,
          "Value": ""
        },
        "autoSaveToState": {
          "VarKey": null,
          "Value": ""
        },
        "closeWhenLostFocus": {
          "VarKey": null,
          "Value": "false"
        },
        "showLineNum": {
          "VarKey": null,
          "Value": "true"
        },
        "autoWrap": {
          "VarKey": null,
          "Value": "true"
        },
        "showBuildInToolbar": {
          "VarKey": null,
          "Value": "true"
        },
        "copyWholeLine": {
          "VarKey": null,
          "Value": "false"
        }
      },
      "OutputParams": {
        "selectedOperation": null,
        "resultText": null,
        "selectedText": null,
        "windowPosition": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:showText",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "WAIT"
        },
        "text": {
          "VarKey": "listResult",
          "Value": null
        },
        "title": {
          "VarKey": null,
          "Value": "动态对象列表赋值给文本"
        },
        "topMost": {
          "VarKey": null,
          "Value": "false"
        },
        "operations": {
          "VarKey": null,
          "Value": ""
        },
        "autoCloseKey": {
          "VarKey": null,
          "Value": ""
        },
        "winLocation": {
          "VarKey": null,
          "Value": "CenterScreen"
        },
        "winSize": {
          "VarKey": null,
          "Value": ""
        },
        "fontsize": {
          "VarKey": null,
          "Value": "14"
        },
        "fontfamily": {
          "VarKey": null,
          "Value": ""
        },
        "bgColor": {
          "VarKey": null,
          "Value": ""
        },
        "textColor": {
          "VarKey": null,
          "Value": ""
        },
        "highlight": {
          "VarKey": null,
          "Value": ""
        },
        "autoSaveToState": {
          "VarKey": null,
          "Value": ""
        },
        "closeWhenLostFocus": {
          "VarKey": null,
          "Value": "false"
        },
        "showLineNum": {
          "VarKey": null,
          "Value": "true"
        },
        "autoWrap": {
          "VarKey": null,
          "Value": "true"
        },
        "showBuildInToolbar": {
          "VarKey": null,
          "Value": "true"
        },
        "copyWholeLine": {
          "VarKey": null,
          "Value": "false"
        }
      },
      "OutputParams": {
        "selectedOperation": null,
        "resultText": null,
        "selectedText": null,
        "windowPosition": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:tableoperation",
      "InputParams": {
        "table": {
          "VarKey": "table1",
          "Value": null
        },
        "type": {
          "VarKey": null,
          "Value": "manage"
        },
        "isReadOnly": {
          "VarKey": null,
          "Value": "1"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "rowCount": "item"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "循环获取每一项的信息：方式一，对表格变量的行进行循环"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:each",
      "InputParams": {
        "input": {
          "VarKey": null,
          "Value": "$= {table1}.Rows"
        },
        "useMultiThread": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {
        "item": "tableRow",
        "count": null
      },
      "IfSteps": [
        {
          "StepRunnerKey": "sys:notify",
          "InputParams": {
            "msg": {
              "VarKey": null,
              "Value": "$= \"表格行：\"  + $\"({{tableRow}.GetType().Name}) \" + \r\n{tableRow}[\"first_name\"] + {tableRow}[\"last_name\"]"
            },
            "maxLines": {
              "VarKey": null,
              "Value": "0"
            },
            "type": {
              "VarKey": null,
              "Value": "Info"
            },
            "style": {
              "VarKey": null,
              "Value": "Default"
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "循环获取每一项的信息：方式二，对对象列表的每项进行循环"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:each",
      "InputParams": {
        "input": {
          "VarKey": "listResult",
          "Value": null
        },
        "useMultiThread": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {
        "item": "item",
        "count": null
      },
      "IfSteps": [
        {
          "StepRunnerKey": "sys:notify",
          "InputParams": {
            "msg": {
              "VarKey": null,
              "Value": "$= \"动态对象列表结果条目：\" +\r\n{item}.first_name + {item}.last_name"
            },
            "maxLines": {
              "VarKey": null,
              "Value": "0"
            },
            "type": {
              "VarKey": null,
              "Value": "Info"
            },
            "style": {
              "VarKey": null,
              "Value": "Default"
            }
          },
          "OutputParams": {},
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "查询数据：条件"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:dboperation",
      "InputParams": {
        "dbType": {
          "VarKey": null,
          "Value": "sqlite"
        },
        "connectionString": {
          "VarKey": "path",
          "Value": null
        },
        "sql": {
          "VarKey": null,
          "Value": "select * from contacts Where first_name = @FirstName"
        },
        "sqlParam": {
          "VarKey": null,
          "Value": "FirstName:李"
        },
        "timeoutSeconds": {
          "VarKey": null,
          "Value": ""
        },
        "operationType": {
          "VarKey": null,
          "Value": "Query"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "dataTableResult": "table1",
        "listResult": "listResult",
        "firstItem": "firstItem",
        "rowCount": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:showText",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "WAIT"
        },
        "text": {
          "VarKey": "table1",
          "Value": null
        },
        "title": {
          "VarKey": null,
          "Value": "条件查询结果内容"
        },
        "topMost": {
          "VarKey": null,
          "Value": "false"
        },
        "operations": {
          "VarKey": null,
          "Value": ""
        },
        "autoCloseKey": {
          "VarKey": null,
          "Value": ""
        },
        "winLocation": {
          "VarKey": null,
          "Value": "CenterScreen"
        },
        "winSize": {
          "VarKey": null,
          "Value": ""
        },
        "fontsize": {
          "VarKey": null,
          "Value": "14"
        },
        "fontfamily": {
          "VarKey": null,
          "Value": ""
        },
        "bgColor": {
          "VarKey": null,
          "Value": ""
        },
        "textColor": {
          "VarKey": null,
          "Value": ""
        },
        "highlight": {
          "VarKey": null,
          "Value": ""
        },
        "autoSaveToState": {
          "VarKey": null,
          "Value": ""
        },
        "closeWhenLostFocus": {
          "VarKey": null,
          "Value": "false"
        },
        "showLineNum": {
          "VarKey": null,
          "Value": "true"
        },
        "autoWrap": {
          "VarKey": null,
          "Value": "true"
        },
        "showBuildInToolbar": {
          "VarKey": null,
          "Value": "true"
        },
        "copyWholeLine": {
          "VarKey": null,
          "Value": "false"
        }
      },
      "OutputParams": {
        "selectedOperation": null,
        "resultText": null,
        "selectedText": null,
        "windowPosition": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "ExecuteScalar"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:dboperation",
      "InputParams": {
        "dbType": {
          "VarKey": null,
          "Value": "sqlite"
        },
        "connectionString": {
          "VarKey": "path",
          "Value": null
        },
        "sql": {
          "VarKey": null,
          "Value": "select COUNT(1) from contacts"
        },
        "sqlParam": {
          "VarKey": null,
          "Value": "FirstName:李"
        },
        "timeoutSeconds": {
          "VarKey": null,
          "Value": ""
        },
        "operationType": {
          "VarKey": null,
          "Value": "ExecuteScalar"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "scalarResult": "scalarResult"
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:notify",
      "InputParams": {
        "msg": {
          "VarKey": null,
          "Value": "$$ ExecuteScalar：共有 {scalarResult} 行数据。"
        },
        "maxLines": {
          "VarKey": null,
          "Value": "0"
        },
        "type": {
          "VarKey": null,
          "Value": "Info"
        },
        "style": {
          "VarKey": null,
          "Value": "Default"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:comment",
      "InputParams": {
        "note": {
          "VarKey": null,
          "Value": "删除数据库文件"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:fileOperation",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "deleteFile"
        },
        "path": {
          "VarKey": "path",
          "Value": null
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```

</details>

***

## 121.多步骤输入

**功能描述**
> 多步骤键盘组合输入
<details>
<summary>详细说明</summary>

```
每行一个步骤指令。
//开始的行作为注释。
指令的格式为：命令:参数。
特殊情况下无法分行填写时，也可以写在一行，并使用;;表示换行。


支持的命令类型如下：


键盘命令

input 模拟键入纯文本（不受输入法影响）。如：input:hello world，你好 世界。
input2 模拟键入纯文本，支持使用转义字符。 如\t内容\r\n换行中的\t表示tab，\r\n表示换行。
sendkeys 使用模拟按键B的语法键入内容。如： sendkeys:{LEFT 2} 发送2个向左的方向键用于移动光标位置。
delay 等待时间（毫秒数）如：delay:1000 等待1秒钟
paste 粘贴内容，如：paste:hello world 将hello world写入剪贴板后模拟Ctrl+V进行粘贴。
keydown 按下按键：如：keydown:F1 按下F1键，或keydown:#175按下音量增加键（#+键值数字）。 注意应该在后续步骤中使用keyup命令抬起按键。键名可参考：微软官方文档。
keyup 抬起按键，格式同上，如：keyup:F1。
keypress 点击（按下并抬起）按键，格式同上。
hotkey 发送组合快捷键。如：hotkey:Ctrl+S ，数字键请使用D+数字表示，如hotkey:Ctrl+Alt+D1。


鼠标命令

moveto 移动鼠标指针到一个绝对坐标。如：moveto:100,200 将鼠标指针移动到 (100,200)位置。1.30.0版本开始支持百分比数值，如：moveto:50%,50%将鼠标移动到主屏幕中心。
move 将鼠标指针移动一定距离（相对于当前位置），参数为“水平方向像素数,垂直方向像素数”。如：move:10,-10 将指针向右和向上分别移动10个像素。
click 点击鼠标某个按键。参数为鼠标按键名，可选：left/right/middle/x1/x2。如：click:left 点击左键。
dbclick 双击鼠标某个按键。参数格式同上。
down 按下某个鼠标按键。参数格式同上。需要特别注意：按下和抬起鼠标按键要完全配对。
up 抬起某个鼠标按键。参数格式同上。
wheel 垂直滚动，单位为clicks（可以理解为“行”）。正值表示向前（远离用户，滚动区域内容向下），负值表示向后（朝向用户，滚动区域内容向上）。
wheeldelta 垂直滚动。单位为1/120 click。更细微的滚动。
hwheel 水平滚动，单位为clicks（可以理解为“行”）。正值表示滚动区域内容向左，负值表示滚动区域内容向右。
hwheeldelta 水平滚动，单位为1/120 click。


组合命令

pastefile 粘贴文件（将文件写入剪贴板后模拟Ctrl+V）。参数为文件完整路径，多个文件使用英文半角分号隔开。如：pastefile:d:\test.png ， pastefile:d:\test1.png;d:\test2.txt
pasteimage 粘贴图片（将图片文件读取为图片后写入剪贴板，然后模拟Ctrl+V，注意写入剪贴板的是图片对象而非图片文件）。如：pasteimage:d:\test.png 只支持单个图片。
```

</details>

**官方文档**
> https://getquicker.net/KC/Help/Doc/inputscript

**内部名称**
> sys:inputScript

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| data | 步骤脚本 | 模拟输入的步骤列表详细格式请参考模块文档 | (0)字符串-Text |  | True |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |

</details>
<details>
<summary>范例</summary>

```json
{
  "Variables": [
    {
      "Key": "isDown",
      "Type": 2,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:keyoperation",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "get_key_state"
        },
        "key": {
          "VarKey": null,
          "Value": "LButton"
        },
        "getRealMouseState": {
          "VarKey": null,
          "Value": "0"
        }
      },
      "OutputParams": {
        "isDown": "isDown",
        "isToggled": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:if",
      "InputParams": {
        "condition": {
          "VarKey": null,
          "Value": "$= {isDown} == true"
        }
      },
      "OutputParams": {},
      "IfSteps": [
        {
          "StepRunnerKey": "sys:inputScript",
          "InputParams": {
            "data": {
              "VarKey": null,
              "Value": "up:left"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "isSuccess": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "ElseSteps": [
        {
          "StepRunnerKey": "sys:inputScript",
          "InputParams": {
            "data": {
              "VarKey": null,
              "Value": "down:left"
            },
            "stopIfFail": {
              "VarKey": null,
              "Value": "1"
            }
          },
          "OutputParams": {
            "isSuccess": null
          },
          "IfSteps": null,
          "ElseSteps": null,
          "Note": "",
          "Disabled": false,
          "Collapsed": false,
          "DelayMs": 0
        }
      ],
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```

</details>

***

## 122.显示菜单

**功能描述**
> 显示一个菜单

**官方文档**
> https://getquicker.net/KC/Help/Doc/showmenu

**内部名称**
> sys:showmenu

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| menuData | 菜单数据 | 可以为Json/菜单文本格式/IList<CommonOperationltem>对象，详情请参考文档 | (0)字符串-Text |  | true |
| fontsize | 字体大小 |  | (12)数字(整数)-Integer | 12 | true |
| iconsize | 图标大小 | 图标的宽度/高度像素数 | (1)数字(小数)-Number | 16 | true |
| maxHeight | 最大高度 | 可以为百分比（如：50%）或固定数值（如：500） | (0)字符串-Text |  | true |
| useFocus | 占用焦点 | 是否允许菜单占用焦点（从而可以键盘选择菜单项） | (2)布尔值-Boolean |  | false |
| waitMenuClose | 等待菜单关闭 | 是否等待菜单关闭后再运行后续步骤 | (2)布尔值-Boolean | True | false |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| selectedItemData | 选择的菜单项数据 | 选择的菜单项的data属性数据 | (0)字符串-Text |
| selectedItem | 选择的菜单项 | 选择的菜单项的CommonOperationltem对象 | (99)任意类型-Any |

</details>
<details>
<summary>范例</summary>

```json
{
  "Variables": [],
  "Steps": [
    {
      "StepRunnerKey": "sys:showmenu",
      "InputParams": {
        "menuData": {
          "VarKey": null,
          "Value": ""
        },
        "fontsize": {
          "VarKey": null,
          "Value": "12"
        },
        "iconsize": {
          "VarKey": null,
          "Value": "16"
        },
        "maxHeight": {
          "VarKey": null,
          "Value": "0"
        },
        "useFocus": {
          "VarKey": null,
          "Value": "0"
        },
        "waitMenuClose": {
          "VarKey": null,
          "Value": "1"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "selectedItemData": null,
        "selectedItem": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```

</details>

***


## 123.文件系统监控

**功能描述**
> 监控指定文件夹下文件或目录的变化（创建/删除/变更/重命名）。支持两种工作方式：1）等待事件发生后继续运行动作。2）持续监控，事件发生后调用设定好的子程序。

**官方文档**
> https://getquicker.net/KC/Help/Doc/filesystemwatch

**内部名称**
> sys:fileSystemWatch

<details>
<summary>传入参数</summary>

| Key | Name | Description | Type | Default | Required |
| :----: | :----: | :----: | :----: | :----: | :----: |
| operation | 操作类型 |  | (9)选项-Enum（wait: 等待事件发生; callback: 持续监控（事件发生后调用子程序）） | wait | true |
| path | 文件夹路径 | 要监控的文件夹路径 | (0)字符串-Text |  | false |
| includeSubdirectories | 包含子文件夹 |  | (2)布尔值-Boolean | True | false |
| filter | 文件筛选 | 筛选要监控的文件。可指定文件名（如foo.txt），或使用通配符（如*.txt） | (0)字符串-Text | *.* | false |
| notifyFilter | 通知筛选 | 可选，设定要监控的变更类型，对应于FileSystemWatcher.NotifyFilter属性（Attributes: 文件或文件夹的属性; CreationTime: 文件或文件夹的创建时间; DirectoryName: 文件夹的名称; FileName: 文件的名称; LastAccess: 文件或文件夹的最后打开时间; LastWrite: 文件或文件夹的最后写入时间; Security: 文件或文件夹的安全设置; Size: 文件或文件夹的大小），可以为使用英文半角逗号(,)连接的这些选项，留空表示默认设置（LastWrite,FileName,DirectoryName）。 | (0)字符串-Text |  | false |
| waitEvents | 等待的事件 | 多个事件可使用英文半角逗号(,)进行连接，支持created,deleted,changed,renamed | (0)字符串-Text | created | false |
| waitSeconds | 等待秒数 | 最长等待时间。0表示不限时间。 | (12)数字(整数)-Integer | 0 | false |
| createdCallback | [创建] 处理子程序 | 文件或文件创建时调用的子程序 | (0)字符串-Text |  | false |
| changedCallback | [变更]处理子程序 | 文件或文件夹变更时调用的子程序 | (0)字符串-Text |  | false |
| deletedCallback | [删除]处理子程序 | 文件或文件被删除时调用的子程序 | (0)字符串-Text |  | false |
| renamedCallback | [重命名]处理子程序 | 文件或文件重命名时调用的子程序 | (0)字符串-Text |  | false |

</details>
<details>
<summary>传出参数</summary>

| Key | Name | Description | Type |
| :----: | :----: | :----: | :----: |
| isSuccess | 是否成功 | 操作是否成功 | (2)布尔值-Boolean |
| fullPath | 变更的路径 | 发生变更的文件（夹）路径，或重命名后的新路径 | (0)字符串-Text |
| changedType | 变更类型 |  | (0)字符串-Text |
| oldFullPath | 旧路径 | 重命名时的原始路径 | (0)字符串-Text |


</details>
<details>
<summary>范例</summary>

**在资源管理器窗口上运行，自动监控当前路径60秒。发生文件创建或文件删除时显示提示消息。**
```json
{
  "Variables": [
    {
      "Key": "path",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": null
    },
    {
      "Key": "changedType",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    },
    {
      "Key": "fullPath",
      "Type": 0,
      "Desc": "",
      "DefaultValue": "",
      "SaveState": false,
      "IsInput": false,
      "IsOutput": false,
      "ParamName": "",
      "InputParamInfo": null,
      "OutputParamInfo": null,
      "TableDef": null,
      "CustomType": null,
      "Group": ""
    }
  ],
  "Steps": [
    {
      "StepRunnerKey": "sys:getExplorerPath",
      "InputParams": {
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "output": "path",
        "allPathList": null,
        "lastPath": null,
        "isSuccess": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:notify",
      "InputParams": {
        "msg": {
          "VarKey": null,
          "Value": "$$开始监控 {path}"
        },
        "maxLines": {
          "VarKey": null,
          "Value": "0"
        },
        "type": {
          "VarKey": null,
          "Value": "Info"
        },
        "clickAction": {
          "VarKey": null,
          "Value": ""
        },
        "style": {
          "VarKey": null,
          "Value": "Default"
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:fileSystemWatch",
      "InputParams": {
        "operation": {
          "VarKey": null,
          "Value": "wait"
        },
        "path": {
          "VarKey": "path",
          "Value": null
        },
        "includeSubdirectories": {
          "VarKey": null,
          "Value": "1"
        },
        "filter": {
          "VarKey": null,
          "Value": "*.*"
        },
        "notifyFilter": {
          "VarKey": null,
          "Value": ""
        },
        "waitEvents": {
          "VarKey": null,
          "Value": "created,deleted"
        },
        "waitSeconds": {
          "VarKey": null,
          "Value": "60"
        },
        "stopIfFail": {
          "VarKey": null,
          "Value": "1"
        }
      },
      "OutputParams": {
        "isSuccess": null,
        "fullPath": "fullPath",
        "changedType": "changedType",
        "oldFullPath": null,
        "errMessage": null
      },
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    },
    {
      "StepRunnerKey": "sys:notify",
      "InputParams": {
        "type": {
          "VarKey": null,
          "Value": "Info"
        },
        "msg": {
          "VarKey": null,
          "Value": "$${changedType}: {fullPath}"
        },
        "maxLines": {
          "VarKey": null,
          "Value": "0"
        },
        "style": {
          "VarKey": null,
          "Value": "Default"
        },
        "clickAction": {
          "VarKey": null,
          "Value": ""
        }
      },
      "OutputParams": {},
      "IfSteps": null,
      "ElseSteps": null,
      "Note": "",
      "Disabled": false,
      "Collapsed": false,
      "DelayMs": 0
    }
  ],
  "SubPrograms": []
}
```
</details>

***

