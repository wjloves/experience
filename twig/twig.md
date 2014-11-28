安装配置  
		    新建一个目录 libs  
		    在该目录下新建文件 composer.json，往该文件写入以下内容：  
		    {  
		       "require": { 
		           "twig/twig": "1.*" 
		       } 
		    }  
		    在 libs 目录上执行 composer install 安装 Twig（前提是已安装 Composer 包管理器） 
		    在 libs 上级目录新建三个文件夹：templates、templates_c、web，其中 templates 用来存放 模板文件，templates_c 用来存放编译缓存文件，web 用来存放 PHP 源文件  
		    在 libs 上级目录新建文件 MyTwig.php 公共文件，内容如下：  
		    // 引用 Composer 自动加载文件  
		    require_once dirname(__FILE__).'/libs/vendor/autoload.php'; 
		    
		    // 注册 Twig 加载器 
		  	Twig_Autoloader::register(); 
		    
		  	// 设置基本的配置项 
		  	$loader = new Twig_Loader_Filesystem(dirname(__FILE__).'/templates'); 
		  	$twig   = new Twig_Environment($loader, array(  
		      'cache'       => dirname(__FILE__).'/templates_c', 
		      'auto_reload' => true 
		  	));  
		  	后续使用时，只需让 web 目录下的 PHP 文件引用该公共文件，且在 templates 目录下放置好 对应的模板即可，引用公共文件的语句为：require_once dirname(dirname(__FILE__)).'/MyTwig.php';  
		  	基本的模板渲染语句：
					echo $twig->render('abc.html.twig', array('name' => 'Ruchee'));



twig英文学习文档 : http://twig.sensiolabs.org/documentation
=============
