# 一、Linux常用命令

## 1.文件处理命令

### (1)命令格式与目录处理命令ls

linux命令大部分没有顺序
#### a.文件类型 
- -：二进制文件
- d：目录
- l：软链接文件

#### b.文件用户
- u：所有者（创建文件的人）
- g：所属组（创建者的缺省组）
- o：其他人

#### c.文件权限
- r：读
- w：写
- x：执行
1. 所有者只有r，w权限，re--；所属组r--；其他人r--
2. x权限只有需要操作的文件如脚本需要，一般只用读和写

#### d.命令
- ls（list）：命令用于显示指定工作目录下之内容
- -a（all）： 显示所有文件及目录 (. 开头的隐藏文件也会列出)
- -l（long）： 除文件名称外，亦将文件型态、权限、拥有者、文件大小等资讯详细列出
- -d（directive）：查询指定目录的详细信息
- -h（human）：人性化展示文件
- -i（）：查看i结点（索引）

### (2)目录处理命令

目录做好规划，见名知意。
- mkdir（make directories）目录名称：创新目录，不能在没创建的目录下创建子目录（父/子）

- mkdir -p （父/子）：递归创建，允许（父/子）创建

  ![QQ图片20210131170457](F:\Learning materials\Linux\一、Linux常用命令\QQ图片20210131170457.png)

- cd（change directory） 目录名称：切换目录、
- cd ..：回到上级目录（cd和..有空格）
- pwd（print working directory）：显示当前目录  

- .：当前目录

- ..：上级目录

  ![QQ图片20210131172625](F:\Learning materials\Linux\一、Linux常用命令\QQ图片20210131172625.png)
  
- rmdir（remove empty directories） 目录名：删除空目录
- cp（copy） 源文件 目标目录：复制
- cp -r：复制目录
- cp -p：可以保存源文件的属性
- mv（move）源文件 目标文件：剪切、改名
- rm （remove） -rf 文件或目录：删除
- rm -r：删除目录
- rm -f：强制删除
1. 删除文件前要备份
2. 误删情况确定后，对硬盘停止读写操作（读写越多越难恢复）
3. 数据恢复很贵
- Ctrl c ：终止命令

### （3）文件处理命令

- touch： 创建空文件，windows不能用的字符Linux没限制，文件名有空格要加引号，否则是创建了两个文件，最好别用

  ![微信图片_20210201134308](F:\Learning materials\Linux\一、Linux常用命令\微信图片_20210201134308.png)

- cat：显示文件内容
- tac：倒序显示文件内容
- cat -n：显示行号
- more 文件名：分页展示文件内容， 空格下一页 回车下一行 q退出
- less 文件名：功能和more一样，可以向上翻页pgup 上箭头上一行 /关键词是搜索，按n（next）显示下一个
- head -n 行号 文件名：显示一个文件的前几行，没有-n 行号，默认显示前10行
- tail -n 行号 文件名：显示一个文件的后行，没有-n 行号，默认显示后10行
- tail -f：动态显示文件尾的内容

### （4）链接命令ln

- ln -s 源文件 目标文件：创建软链接
> 软链接相当于windows的快捷方式 ，快捷方式还要找到源文件打开。软链接文件的所有用户权限是rwx

- ln 源文件 目标文件：创建硬链接
> 硬链接相比cp -p可以同步更新；源文件丢失，硬链接仍然可以使用，就像一个实时备份；硬链接和源文件的i结点一样，也正是因为i结点一样所以可以同步更新；不能跨分区；不能对目录使用

## 2. 权限管理命令

### （1）权限管理命令chmod（change the permissions mode of a file）

1. chmod：[{ugoa} {+-=} {rwx}] 文件名或目录，a是所有人

  ![微信图片_20210202092408](F:\Learning materials\Linux\一、Linux常用命令\微信图片_20210202092408.png)

  ![QQ图片20210202094610](F:\Learning materials\Linux\一、Linux常用命令\QQ图片20210202094610.png)

2. 权限的数字表示
	r==4（100），w==2（010），x==1（001），rwx==4+2+1=7
	
	![QQ图片20210202095704](F:\Learning materials\Linux\一、Linux常用命令\QQ图片20210202095704.png)
	
3. chmod -R：递归修改

4. file  r:cat/more/head/tail/less
	      v:vim

   ​      x: command/script
   
   directory  r:ls
   
   ​                w:touch/mkdir/rmdir/rm	
   
   ​                x:cd
   
   ![QQ图片20210202160908](F:\Learning materials\Linux\一、Linux常用命令\QQ图片20210202160908.png)
   
### (2)其他权限管理命令

 - chown（change file ownership）用户 文件或目录：改变文件或目录的所有者

 - chgrp(change file group ownership) 用户组 文件或目录：改变文件或目录的所属组

 - umask（the user file-creation mask） -S：显示设置文件的缺省权限（缺省创建的文件没有可执行权限）
   
   ![QQ图片20210203074108](F:\Learning materials\Linux\一、Linux常用命令\QQ图片20210203074108.png)
   
## 3.文件搜索命令

### （1）文件搜索命令find

- find 搜索范围 匹配条件：文件搜索
- find /目录 -name 文件名：根据文件名在目录搜索（不是模糊查询）；文件名* ：模糊查询以文件名开头的文件；文件名？？？文件名后有三个字符；大小写不能混淆
- find /目录 -iname 文件名：不区分大小写
- find /  size +数据块：在目录下查找大于数据块的文件；一个数据块0.5k 100MB =102400KB=204800个数据块
- find /  -user 文件名：在目录下查找所有者为文件名的文件，user可以变成group所属组
- find / -cmin -时间：查找在目录下时间内（+时间为超过时间）被修改过属性的文件和目录
- find / -size +数据块1  -a  -数据块2：在目录下查找大于数据块1小于数据块2的文件 （-a与，-o或）；-type ，根据文件类型查找：f文件，d目录，l软链接；-inum，根据i结点查找

### （2）其他搜索命令
- locate 文件名：在文件资料库中查找文件，先更新文件资料库updatedb，暂时文件资料库不更新；-i不区分大小写
- which 命令 ：搜索命令所在目录及别名信息
 一般放在bin，usr/bin下的是所有用户都能使用的命令，sbin，usr/sbin下的是只有root能使用的命令
- whereis 命令：搜索命令所在路径和帮助文档的路径
- grep 指定字串 文件：在文件中搜索子串匹配的行并输出；-i不区分大小写；-v排除指定字符串

## 4.帮助命令

- man 命令或配置文件：获得帮助信息
   命令：看name，选项用处用/搜索，直接输入/字符检索，按n下一个
   配置文件：看name，看手册的格式查找，#为注释
   帮助文档：1命令的帮助，5配置文件的帮助 man 5 passwd
- whatis 命令：只读取命令的name
- apropos 配置文件：只读取配置文件的name
- 命令 --help：列出常见选项
- help 命令：获得shell内置命令的帮助信息，内置命令没有路径