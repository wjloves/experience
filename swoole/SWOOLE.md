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


基本实例：
	服务端（源码执行）
	class Server{
	    private $serv;

	    public function __construct() {
	        $this->serv = new swoole_server("0.0.0.0", 9501);
	        $this->serv->set(array(
	            'worker_num' => 8,
	            'daemonize' => false,
	            'max_request' => 10000,
	            'dispatch_mode' => 2,
	            'debug_mode'=> 1
	        ));

	        $this->serv->on('Start', array($this, 'onStart'));
	        $this->serv->on('Connect', array($this, 'onConnect'));
	        $this->serv->on('Receive', array($this, 'onReceive'));
	        $this->serv->on('Close', array($this, 'onClose'));

	        $this->serv->start();
	    }

	    public function onStart( $serv ) {
	        echo "Start\n";
	    }

	    public function onConnect( $serv, $fd, $from_id ) {
	        $serv->send( $fd, "Hello {$fd}!" );
	    }

	    public function onReceive( swoole_server $serv, $fd, $from_id, $data ) {
	        echo "Get Message From Client {$fd}:{$data}\n";
	    }

	    public function onClose( $serv, $fd, $from_id ) {
	        echo "Client {$fd} close connection\n";
	    }
	}
	// 启动服务器
	$server = new Server();

   客户端
   class Client{
	    private $client;

	    public function __construct() {
	        $this->client = new swoole_client(SWOOLE_SOCK_TCP);
	    }

	    public function connect() {
	        if( !$this->client->connect("127.0.0.1", 9501 , 1) ) {
	            echo "Error: {$fp->errMsg}[{$fp->errCode}]\n";
	        }
	        $message = $this->client->recv();
	        echo "Get Message From Server:{$message}\n";
	    }
	}

	$client = new Client();
	$client->connect();



入门资料链接地址：https://github.com/LinkedDestiny/swoole-doc
官网地址    	：http://wiki.swoole.com/
==========
