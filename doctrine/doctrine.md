Doctrine 简介与实例

Doctrine是一个ORM（Object-relational mapper），提供php数据库和PHP对象的映射。他和其他的ORM一样都是为了保证持久层和逻辑层的分类而存在的。

什么是Entity?
An：
	Entity是PHP的一个对象

	Entity对应的表需要有主键

	Entity中不能含有final属性或者final方法

代码生成表结构命令 ：php vendor/bin/doctrine orm:schema-tool:create
更新数据表命令     ：php vendor/bin/doctrine orm:schema-tool:update --force --dump-sql

实例（使用EntityManager能对Entity进行增删改查的操作）：
		增加：
		$product = new Product();
		$product->setName($newProductName);
		 
		$entityManager->persist($product);
		$entityManager->flush();
		 
		查询：
		$entityManager->find('Product', $id)
		 
		更新：
		$product = $entityManager->find('Product', $id);
		$product->setName($newName);
		$entityManager->flush();
		 
		删除：
		$product = $entityManager->find('Product', $id);
		$product->remove();
		$entityManager->flush();


教程地址       ：http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/tutorials/getting-started.html
教程github地址 ：https://github.com/doctrine/doctrine2-orm-tutorial
blog地址	   ：http://www.cnblogs.com/yjf512/p/3375614.html

======================
