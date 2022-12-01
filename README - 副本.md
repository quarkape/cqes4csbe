# CQES4CS V1.0.0 Front End

![banner](https://user-images.githubusercontent.com/43498577/202853353-1f9b97ee-b7ac-4a55-9fc8-f5c2d2319953.png)

---

💼  一个基于规则配置的综合素质评价系统，助力高校更方便、更高效的开展学生综合素质评价工作。

:raised_hands: 如果需要帮助请联系Q244627905

---

## :notebook:环境要求

- JDK，[你可以参照这篇文章安装与配置JDK](https://www.runoob.com/java/java-environment-setup.html)

- MySQL，[你可以参照这篇文章安装与配置mysql](https://www.runoob.com/mysql/mysql-install.html)

- Redis，[你可以参照这篇文章安装与配置Redis](https://juejin.cn/post/7043684887773052965)

- Node.js，[你可以参照这篇文章安装与配置Node.js](https://www.runoob.com/nodejs/nodejs-install-setup.html)

- Maven，[你可以参照这篇文章安装与配置Maven并了解如何在IDEA中使用](https://blog.csdn.net/pan_junbiao/article/details/104264644)

  **:herb: 安装完成后，redis和mysql需要进行配置，具体配置参数请点击[mysql配置](#mysqlconf)和[redis配置](#redisconf)，保证配置与项目一致**

---

## :baguette_bread: 项目技术框架与主要组件

- 前端：Vue，ElementUI，echarts，axios，nprogress，qs
- 后端：springboot，redis，shiro，poi，mybatis
- 数据库：mysql

## :taco: 详细安装、运行以及部署流程

### 1、前端项目安装、运行与部署

1. 下载项目压缩包至本地解压，或者使用`git clone https://github.com/quarkape/cqes4cs.git`克隆项目
2. 进入项目目录，打开命令窗口，执行`npm install`，会开始下载前端项目所需要的所有依赖，等待所有依赖下载完成
3. 进入项目目录，打开命令窗口，执行`npm run serve`，会开始运行前端项目
4. 如果需要部署该项目，你需要对前端项目进行构建：进入项目目录，打开命令窗口，执行`npm run build`，执行完后，项目目录下会生成一个`dist`文件夹，这个文件夹就是构建之后的文件，可以直接部署

---

### <span id="mysqlconf">2、MySQL数据导入与配置说明</span>

1. 使用`mysql -u root -p`进入mysql

2. 依次执行下面的四条命令：

   ```mysql
   # 创建名为cqes4cs的数据库
   create database cqes4cs;
   # 使用数据库cqes4cs
   use cqes4cs;
   # 设置数据库编码方式
   set name utf8;
   # 下面的source后面是sql文件的位置，例如是G:\Projects\IDEA\cqes4cs\cqes4cs.sql的话就是：
   source "G:\Projects\IDEA\cqes4cs\cqes4cs.sql"
   ```

3. 导入数据后，切换到数据库cqes4cs中，查询users表，看是否有数据，如果有的话说明导入成功

4. 你可以借助MySQL WorkBench或者Navicat对数据库进行管理

5. 项目要求的mysql配置可以在：`cqes4cs\src\main\resources\application.yml`配置文件中找到：

   ```yaml
   datasource:
   	# 用户名为root
       username: root
       # 密码为root
       password: root
       # 端口为3306，数据库为cqes4cs
       url: jdbc:mysql://127.0.0.1:3306/cqes4cs?serverTimezone=UTC&useUnicode=true&characterEncoding=utf-8
       driver-class-name: com.mysql.jdbc.Driver
   ```

   请确保电脑上面的相关配置与项目中的配置保持一致（可以改电脑上的配置，也可以改配置文件）

---

### <span id="mysqlconf">3、Redis配置说明</span>

1. 项目要求的redis配置可以在：`cqes4cs\src\main\resources\application.yml`配置文件中找到：

   ```yaml
   redis:
   	# 端口6379
       port: 6379
       # 密码kkty
       password: kkty
       host: 127.0.0.1
   ```

   请确保电脑上面的相关配置与项目中的配置保持一致（可以改电脑上的配置，也可以改配置文件）

### 4、后端项目安装、运行与部署

1. 下载项目压缩包至本地解压，或者使用`git clone https://github.com/quarkape/cqes4csbe.git`克隆项目
2. 进入项目目录，打开命令窗口，执行`mvn dependency:copy-dependencies`，会开始下载后端项目所需要的所有依赖，等待所有依赖下载完成
3. 进入项目目录，打开命令窗口，执行`mvn spring-boot:run`，开始运行后端项目
4. 如果需要部署该项目，你需要对后端项目进行打包，进入项目目录，打开命令窗口，执行`mvn package`对项目进行打包。默认打包为jar包，如果需要更换为war包，请自行搜索相关流程。

### 5、静态资源的部署

1. 找到`src\main\java\club\hue\config\`下的`MvcConfig.java`文件并打开，在这个文件下，找到这一行代码:

   ```java
   registry.addResourceHandler("/files/**").addResourceLocations("file:G:/Projects/Materials/cqes4cs/files/");
   ```

   上述代码用于指定静态资源的位置，必须配置正确。你需要将你后端项目中的files文件夹的路径复制，并替换上面代码中的路径。例如，在你的电脑上，你的后端项目中的files文件夹的路径是：`G:\Projects\IDEA\cqes4cs\files`，那么你需要修改上述代码的后半部分：

   ```Java
   // 你需要注意两点：一是使用正斜杠/，二是路径后面一定要加一个/
   registry.addResourceHandler("/files/**").addResourceLocations("file:G:/Projects/IDEA/cqes4cs/files/");
   ```

---

### 6、进入系统与初步配置使用

1. 浏览器地址栏输入`http://localhost:8080`回车进入系统登录页面
2. 登录管理员账号，用户名和密码均为`admin`
3. 登陆后新建一个教师账号，建议新建一个管理年级为2021的账号，这有助于后续与项目提供的测试数据关联
4. 点击右上角头像，退出管理员账号，登录上一步创建的教师账号
5. 在教师端，点击学生管理，点击上传学生名单，选择后端项目中`files\students\test_students_data.xlsx`文件上传，用于生成学生数据
6. 在教师端，点击学分评价，点击上传学生成绩，选择后端项目中`files\grades\test_grades_data.xlsx`文件上传，用于生成学生成绩数据
7. 退出教师账号，登录学生账号，学生账号是可以选择纲刚上传的学生名单文件中的任一学号，初始密码也为学号。一个可用的学号和密码为“51214108037”
8. 在学生端，可以提交学分申请等。至此，基本工作已经差不多完成

---

## :chart_with_downwards_trend:  系统演示

[安装配置演示视频](https://www.bilibili.com/video/BV1KG4y1Z7Pd?share_source=copy_web)​

---

## :pushpin: ​前端项目地址

[前端项目](https://github.com/quarkape/CQES4CS.git)

---

## ✂️  静态资源结构说明

```

├─files
    ├─configs  (导出的配置文件的存储位置)
    │      2bb65d3b-11c0-4073-8a68-99f18dcab1c3.xls
    │      
    ├─exports  （导出的综评结果文件的存储位置）
    │      06c4156c-9939-4d11-b93b-2af496c27d43.xls
    │      
    ├─grades  （上传的学生成绩名单的存储位置）
    │      1660235470069.xlsx
    │      
    ├─material  （学分申请的图片存储位置）
    │      166884104794251214108037.png
    │      
    ├─source
    │      efile.pdf  （综合素质评价文件位置）
    │      grade_example.xlsx  （学生成绩模板文件）
    │      student_list_example.xlsx  （学生名单模板文件）
    │      
    └─students
            1660232101630.xls  （上传的学生名单文件存储位置）
```

---

## :bow_and_arrow: 特色功能

- 提前配置加分规则，减少繁琐的计分过程，提高科学性和效率
- 支持文件导入导出，覆盖常见功能
- 灵活构建评价指标体系，适合不同高校不同专业的培养目标
