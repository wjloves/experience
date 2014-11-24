记录学习经验和知识的沉淀
Swool 安装步骤：
1.1  wget https://github.com/swoole/swoole-src/archive/swoole-1.7.7-stable.tar.gz

1.2  解压  tar -zxvf swoole-1.7.7-stable.tar.gz
     修改目录名称   mv  swoole-1.7.7-stable    swoole

1.3  进入swoole 
	 cd   swoole

1.4	 编译
	 phpize    //或者使用绝对路径  /usr/local/php/bin/phpize

	 如果你系统没有安装phpize的话，执行命令安装就可以了，指令为：
	 yum install php-devel

1.5  然后再进行配置，指令为：
	./configure --with-php-config=/usr/local/php/bin/php-config

1.6   安装   make & make install

1.7  安装好之后会输出一个路径，那个就是生成swoole.so的文件路径，然后配置php.ini，把该路径配置进去：
	 /usr/local/php/lib/php/extensions/no-debug-non-zts-20121212/

	 php.ini
	 extension="swoole.so"
1.8  检查
 	 php  -m   &  phpinfo()

==========
