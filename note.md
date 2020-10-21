### 数据删除与过滤

一般处理删除事件时，如数组常用
`this.arr = this.arr.filter(item => item!==xxx )`

至于同一个数据但需要在不同状态下呈现：（过滤）
使用一个默认值然后过滤给新数组
`this.newArr = this.arr.filter(item => ...)`

### typescript环境配置

1. `ts`环境安装
   `npm install -g typescript` 
2. 运行ts文件
   `tsc Hello.ts` 

### 代码规范

1.  `html`多个属性要换行、避免多个空格
2.  `css`样式：每个样式之间空行
3.  `ts：import`下面空行，属性与方法的注释用/** */ 内部用//

### 模块引用

每个组件都是一个模块，然后在多个组件外面一层定义一个`index.ts`文件导出多个组件

```
export * from './stb-capsule-label';
export * from './stb-pie-chart';
export * from './stb-status-circle';
```

同时`index.ts`同层定义一个`module.ts`引入这些组件模块   **#用‘.’即表示所有组件文件**

```
import {  StbCapsuleLabelModule,  StbCapsuleLabelComponent,  StbPieChartComponent} from '.';    
```

同时要注意的是要把一个组件做成公共组件，需要在其模块下exports出去

```
@NgModule({  
imports: [CmtDashboardPageModule, CmtCollaborationPageModule  ],
// 在以下导出
exports: [CmtDashboardPageComponent, CmtCollaborationPageComponent  ]
}) 
```

### 远程桌面连接

1.`cmd` 运行`mstsc`，输入一下配置

​	01. `host：10.37.36.112`

​	02.`user：local\avatar`

​	03.`pwd: Jo3Tj;4@2019`

2.`cmd` 运行`gpedit.msc` 打开配置项：计算机配置>管理模板>系统>凭据分配>加密oracle修正 选择启用并选择易受攻击 保存

### Angular中监听窗口变化

```
import { Observable } from 'rxjs/Observable';
```

```
Observable.fromEvent(window, 'resize')
.distinctUntilChanged()
.debounceTime(500)
.throttle(() => Observable.interval(500))
.subscribe(_ => {
// 窗口变化时执行以下内容
this.orderSearchPageHeight= document.body.clientHeight;
});
```

### 对数组中的元素做`JSON.stringify()`的简便写法

`[123, [1, 2, 3], [1, "2", 3], [1, 2, 3], "meili"].map(JSON.stringify)`

对于多维数组或数组中有引用类型，可使用`JSON.stringify()`转换后，通过new Set()去重(有缺陷，如果对象中的属性位置不一样，则去不了重)

### Git拉取远程分支

1.在本地新建一文件夹用来存放项目代码 

2.进入该文件，右键选择 git bush here，打开命令窗后，输入初始化命令：git init

3.命令行：git remote add origin 后面是项目所在远程仓库地址（不是远程分支名称，而是仓库地址）

4.拉取远程分支到本地：git fetch origin dev(dev是你要拉取的远程分支名称)

5.在本地创建dev分支并且切换到该分支：git checkout -b dev(本地分支名称)

6.拉取分支到本地：git pull origin dev(远程分支名称)
原文链接：https://blog.csdn.net/Gomeer/java/article/details/102947291

### 解决UI上未能更新view（）

```
import { Component, OnInit, Input, EventEmitter, Output, ChangeDetectorRef} from '@angular/core';

constructor( 
	private detRef: ChangeDetectorRef
) {}

this.detRef.detectChanges();// 常用于comp显示时异常
```

