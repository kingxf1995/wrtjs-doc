# API 参考文档

---
# 目录
1. [Base Fcuntion](#base-function)
2. [GPIO](#gpio)
3. [Pinmux](#pinmux) 
4. [External Interrupt](#external-interrupt) 

# Base function

## **print**

### 说明
> 将信息打印到终端上

### 参数
|   参数名  |     类型    | 可选/必须 |
|-----------|-------------|-----------|
| 打印数据  | 所有类型    | 必须      |
### 返回值
Undefined

# GPIO

## 首先需要使用requre导入GPIO库
    var gpio = require('gpio');

## **gpio.open**
### 说明
> 打开一个引脚，获得`pinobj`，通过该`pinobj`控制引脚读写

### 参数
|   参数名  |     类型    | 可选/必须 |
|-----------|-------------|-----------|
| 引脚号    | number      | 必须      |

### 返回值
如果成功返回引脚对象`pinobj`，否则返回false

## **pinobj.pinnum**
### 说明
> 获取该pinobj对象的引脚号

### 参数
无

### 返回值
该pinobj对象的引脚号

## **pinobj.read**
### 说明
> 从引脚上读电平信号，在此之前请注意用[pinobj.direction('in')](#pinobjdirection)设置引脚为输入模式

### 参数
无

### 返回值
如果引脚为高电平返回true，如果为低电平返回false，如果读取失败返回Undefined

## **pinobj.write**
### 说明
> 通过引脚写电平信号，在此之前请注意用[pinobj.direction('out')](#pinobjdirection)设置引脚为输出模式

### 参数
|   参数名  |     类型    | 可选/必须 |                 说明                 |
|-----------|-------------|-----------|--------------------------------------|
| 电平值    | boolean     | 必须      | 高电平使用true，低电平使用false      |

### 返回值
成功返回true，失败返回false

## **pinobj.pull**
### 说明
> 设置内部上拉/下拉

### 参数
|   参数名  |     类型    | 可选/必须 |                 说明                 |
|-----------|-------------|-----------|--------------------------------------|
| 模式      | string      | 必须      | 'up'、'down' 或者 'none'             |

### 返回值
成功返回true, 失败返回false

## **pinobj.direction**
### 说明
> 设置I/O方向

### 参数
|   参数名  |     类型    | 可选/必须 |                 说明                 |
|-----------|-------------|-----------|--------------------------------------|
| 方向      | string      | 必须      | 'in' 或者 'out'                      |

### 返回值
成功返回true, 失败返回false

# Pinmux
## 首先需要使用requre导入Pinmux库
    var pinmux = require('pinmux');

## **pinmux.set**
### 说明
> 设置引脚复用

### 参数
|   参数名  |     类型    | 可选/必须 |                 说明                 |
|-----------|-------------|-----------|--------------------------------------|
| 引脚号    | number      | 必须      |                                      |
| 功能号    | number      | 必须      | 详情查阅芯片手册                     |

# External Interrupt
## 首先需要使用requre导入External Interrupt库
    var extint = require('extint');

## extint.pin2eint
### 说明
> 传入引脚号，返回该引脚上的外部中断号

### 参数
|   参数名  |     类型    | 可选/必须 |                 说明                 |
|-----------|-------------|-----------|--------------------------------------|
| 引脚号    | number      | 必须      |                                      |

### 返回值
成功，返回引脚对应的外部中断号；失败，返回false


## **extint.init**
### 说明
> 初始化外部中断

### 参数
|   参数名  |     类型    | 可选/必须 |                 说明                        |
|-----------|-------------|-----------|---------------------------------------------|
| 外部中断号| number      | 必须      | 可使用[extint.pin2eint](#extintpin2eint)获取|
| 触发模式  | string      | 必须      | 见下方表格                                  |
| 消抖时间  | number      | 必须      | 若禁用消抖，该参数填0                       |

触发模式

|  触发模式  |    参数值    |
|------------|--------------|
| 低电平触发 | "low_level"  |
| 高电平触发 | "high_level" |
| 下降沿触发 | "fall_edge"  |
| 上升沿触发 | "rise_edge"  |
| 双边沿触发 | "both_edge"  |

### 返回值
成功返回true，失败返回false

## **extint.register**
### 说明
> 注册回调函数

### 参数
|   参数名  |     类型    | 可选/必须 |                 说明                        |
|-----------|-------------|-----------|---------------------------------------------|
| 外部中断号| number      | 必须      | 可使用[extint.pin2eint](#extintpin2eint)获取|
| 回调函数  | function    | 必须      | 该回调函数不传参数                          |

### 返回值
成功返回 extint_callback_handler，失败返回false

## **extint_callback_handler.kill**
### 说明
> 删除这个回调

### 参数
无

### 返回值
成功返回true，失败返回false
