### Todo-任务管理
#### 一、作品描述
**主要学习express与mysql搭配使用构建后端数据api，无非就是CRUD哈哈**
先看看渣渣的效果嘻嘻
![](./Vue%2BNodeJs实战%2BMySQL-Todo_md_files/image_20200531155304.png)
#### 二、技术栈

 1. 前端
	 Vue
	 axios
	 ElementUI
 2. 后端
	 express
	 cors
	 body-parser
	 sequelize、sequelize-cli
	 mysql2

#### 三、后端实现
（附上思维导出，就不再写了嘻嘻，实现步骤应该很清晰了）
[点我点我](http://naotu.baidu.com/file/3205c5a0def25ae3f4e89a2ad85f8a99?token=c006e1313fbe4c2f)
![](./Vue+NodeJs实战+MySQL-Todo_md_files/image_20200531155127.png?v=1&type=image&token=V1:F_jZVWOPOqWimqQovCFXYwU6CNVC-vu9XueAnVl3NqU)
#### 四、前端实现

 ##### 1. 前端项目搭建
		 

 1. Vue脚手架创建项目
			 ``` vue create todo```
			 选择 vue-router、vuex、css-proceer
 ---
 2. 安装element-ui-UI库
			```vue add element-ui```安装ElementUI库
 	               (vue脚手架会自动引入UI库不用自己引用，但全局引入的，如果按需引入的话，可以自主引入)
---
 3. 安装axios-网络请求库
			(这里我选择yarn 安装axios 为了二次封装axios而已，当然你可以选择  "vue add axios " vue脚手架会自动引入)
![](./Vue+NodeJs实战+MySQL-Todo_md_files/image_20200531150805.png?v=1&type=image&token=V1:vxCOlQJrmHNwkNMzdDvs9h7p63LIJJqNtYouqbzMBTk)
---
  #####   基本框架搭建
  
 1. 目录结构
		 ![](./Vue+NodeJs实战+MySQL-Todo_md_files/image_20200531152223.png?v=1&type=image&token=V1:buuMfle0U4m3K5JcSbupwg7MafFlMUYuGOFGCbTlISw)
 2. 设计页面框架
	 App.vue
				                  ![]./(Vue+NodeJs实战+MySQL-Todo_md_files/image_20200531152424.png?v=1&type=image&token=V1:2ByY843DFUJ6JXK2VUZjtPDLRp6t9nhzazLdJ-hBwvQ)	
			 Main.vue
			          * ![]./(Vue+NodeJs实战+MySQL-Todo_md_files/image_20200531152558.png?v=1&type=image&token=V1:57-8bpmxOCRMigEnf1hnk-hR6OtR0hfxxHzdWv-jYtQ)
			          * ![]./(Vue+NodeJs实战+MySQL-Todo_md_files/image_20200531152618.png?v=1&type=image&token=V1:VVyFdZGah1ts36bPMpFkVQSBfOoDm09sulxGv4iSo2A)
 4. 设计路由
        router/index.js
            ![](./Vue+NodeJs实战+MySQL-Todo_md_files/image_20200531152711.png?v=1&type=image&token=V1:GGx4Ky6MoESATtuVKqe0yqA7bscG51dK1I8ub151fjM)
            页面效果
                 ![](./Vue+NodeJs实战+MySQL-Todo_md_files/image_20200531152859.png?v=1&type=image&token=V1:cBTU5d1jrCXn5qjx-3bj8aFpJaZjTbimQiGwcvudn-8)
  #####  前后端数据联调-封装axios
  1. 在src目录下新建http.js
      ![](./Vue+NodeJs实战+MySQL-Todo_md_files/image_20200531153225.png?v=1&type=image&token=V1:WNkDNUa_j4HvajWUtbRZn9Ztl145E64yL-CEoFVV4qo)
  3. 挂载实例 -在mian.js
	           ![](./Vue+NodeJs实战+MySQL-Todo_md_files/image_20200531153247.png?v=1&type=image&token=V1:8fW1TDTJChh8-m4rZWlWJ65q75mpV00_CgRtKQ_zdLo)
3. 使用方法
     异步
	    ``` this.$http.get(''/list).then((res)=>{ }).catch((err)=>{})```
	同步
	```async-await方法: const result=await this.$http.get('/list')```
  #####  功能模块实现
  1. 设计任务列表页面
       （这里需要消耗你艺术细胞了哈哈）
        大概页面是这样的
          ![](./Vue+NodeJs实战+MySQL-Todo_md_files/image_20200531153750.png?v=1&type=image&token=V1:NK3KRXYW2gk_yvAuJju3ytOTCN-PNrfl5iYbsVc7lNU)
          还有其他一些细节![]./(Vue+NodeJs实战+MySQL-Todo_md_files/image_20200531153912.png?v=1&type=image&token=V1:-2mEZXZTmDL-r2_pnBun7m4OwQFBr9CK1MDbONLFUDw)
          ![](./Vue+NodeJs实战+MySQL-Todo_md_files/image_20200531154417.png?v=1&type=image&token=V1:qhaJ2glJg2XYlMDNtTXvLRdDeLm9OZpVJ6v1Q60V8-U)
          过滤数据
          ![](./Vue+NodeJs实战+MySQL-Todo_md_files/image_20200531154515.png?v=1&type=image&token=V1:dOu29QG7TqYfYbv7sTaIp3_X53vvWC5V8OwHvO3QuGU)
          当页面加载时 获取全部数据
          ![](./Vue+NodeJs实战+MySQL-Todo_md_files/image_20200531154555.png?v=1&type=image&token=V1:4xFJE8XYb5I_-l6x-_f71Zw7mUo91TMzgcnTKiOBiGI)
  2. 增删改查逻辑实现
       用到的变量
![](./Vue+NodeJs实战+MySQL-Todo_md_files/image_20200531154146.png?v=1&type=image&token=V1:HJdYed_mcyBiWCRF-u6PkcbL0RF39-b1yzcf_KAtU7c)
       新建任务
![](./Vue+NodeJs实战+MySQL-Todo_md_files/image_20200531154000.png?v=1&type=image&token=V1:AMHvT_t8ku5ufpM_lTY1vNk9AroxxxJyA7vCW0ePN3o)
           逻辑方法
![](./Vue+NodeJs实战+MySQL-Todo_md_files/image_20200531154056.png?v=1&type=image&token=V1:e0GelOgDhGM9v11t5skTM8haeu_PVxSqs-mAy185W-Q)
           编辑任务
![](./Vue+NodeJs实战+MySQL-Todo_md_files/image_20200531154017.png?v=1&type=image&token=V1:z883N_bmrWelE-NCSwV7TnHxlC50L8zkxrVBm5HvqHw)
         逻辑方法
![](./Vue+NodeJs实战+MySQL-Todo_md_files/image_20200531154232.png?v=1&type=image&token=V1:RjBtl4f0lHBJ9HX4KtSAlQVWoGNC6CjhE9R5FfTvRy4)	
		修改状态
		![](./Vue+NodeJs实战+MySQL-Todo_md_files/image_20200531154306.png?v=1&type=image&token=V1:SwEiQUgWzibgxDdrou4OE_jVf0rYqwKkW5e_5aG4jWs)
		删除任务
		![](./Vue+NodeJs实战+MySQL-Todo_md_files/image_20200531154323.png?v=1&type=image&token=V1:pjl8gCa_KcLhfJxwhUfQZz4pemEMAlifijdHJgTY1z0)
		获取全部任务
		![](./Vue+NodeJs实战+MySQL-Todo_md_files/image_20200531154344.png?v=1&type=image&token=V1:VX3Fsl0-KlCgJv120iC3WD-E1Uc-5_f7paNp9qutXO0)



#### 最后
**前后端分离开发模式，确定很方便开发，两者工作不会相互影响，这是它们的好处之一；（作为渣渣，不太会用专业的术语去表达呜呜呜）；有兴趣的伙伴，我们一起学习吧，冲冲冲！！！目标就是做个特别的程序员（code搬运工）（哈哈哈）**

