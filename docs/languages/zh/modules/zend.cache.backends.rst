.. _zend.cache.backends:

Zend_Cache后端
============

.. _zend.cache.backends.file:

Zend_Cache_Backend_File
-----------------------

此后端把缓存纪录存储到文件中去(在一个选定的目录中).

可用的选项有 :

.. _zend.cache.backends.file.table:

.. table:: 文件后端选项

   +--------------------------+-------+------------+-----------------------------------------------------------------------------------------------------------------------------------+
   |选项                        |数据类型   |默认值         |描述                                                                                                                                 |
   +==========================+=======+============+===================================================================================================================================+
   |cache_dir                 |string |'/tmp/'     |存放缓存文件的目录                                                                                                                          |
   +--------------------------+-------+------------+-----------------------------------------------------------------------------------------------------------------------------------+
   |file_locking              |boolean|true        |启用/禁用文件锁定 : 在比较坏的情况下,能够避免缓存中断,但在多线程Web服务器或者NFS文件系统中没有任何帮助.                                                                         |
   +--------------------------+-------+------------+-----------------------------------------------------------------------------------------------------------------------------------+
   |read_control              |boolean|true        |启用/禁用读控制: 如果启用,控制键被嵌入到缓存文件中,并且这个键将与读取后计算出的值进行比较.                                                                                   |
   +--------------------------+-------+------------+-----------------------------------------------------------------------------------------------------------------------------------+
   |read_control_type         |string |'crc32'     |读控制类型 (仅在读控制启用时). 可用的值有: 'md5' (最好但最慢), 'crc32' (安全性稍差,但更快,更好的选择), 'adler32' (新选择，比 crc32 快), 'strlen' for a length only test (最快).|
   +--------------------------+-------+------------+-----------------------------------------------------------------------------------------------------------------------------------+
   |hashed_directory_level    |int    |0           |Hash目录结构层次: 0 表示"不使用hash的目录结构", 1 表示"一级目录结构" , 2表示"二级目录"... 次选项在你有成千上万的缓存文件是能够加速缓存.只有相关的基准测试才能帮助你选择合适的值.也许1或2是一个好的开始.              |
   +--------------------------+-------+------------+-----------------------------------------------------------------------------------------------------------------------------------+
   |hashed_directory_umask    |int    |0700        |目录结构的Unix 掩码                                                                                                                       |
   +--------------------------+-------+------------+-----------------------------------------------------------------------------------------------------------------------------------+
   |file_name_prefix          |string |'zend_cache'|缓存文件前缀;小心使用此选项,因为当清除缓存时,在系统缓存目录(像 /tmp)中一个太generic的值将导致灾难.                                                                         |
   +--------------------------+-------+------------+-----------------------------------------------------------------------------------------------------------------------------------+
   |cache_file_umask          |int    |0700        |缓存文件掩码                                                                                                                             |
   +--------------------------+-------+------------+-----------------------------------------------------------------------------------------------------------------------------------+
   |metatadatas_array_max_size|int    |100         |metadatas 数组的内部最大尺寸（除非你知道你在做什么，不要更改这个值）                                                                                            |
   +--------------------------+-------+------------+-----------------------------------------------------------------------------------------------------------------------------------+

.. _zend.cache.backends.sqlite:

Zend_Cache_Backend_Sqlite
-------------------------

此后端把缓存纪录存储到SQLite数据库中.

可用的选项有:

.. _zend.cache.backends.sqlite.table:

.. table:: Sqlite 后端选项

   +----------------------------------+------+----+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |选项                                |数据类型  |默认值 |描述                                                                                                                                                                                       |
   +==================================+======+====+=========================================================================================================================================================================================+
   |cache_db_complete_path (mandatory)|string|null|SQLite数据库的完整和路径(包括文件名)                                                                                                                                                                   |
   +----------------------------------+------+----+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |automatic_vacuum_factor           |int   |10  |禁用 / 调整自动清理过程. 自动清理过程将对数据库文件进行碎片整理(and make it smaller) 当clean() 或则 delete() 被调用时 : 0 表示不自动清理; 1 表示自动清理(当调用 delete() 或者 clean() 方法时) ; x (整数) > 1 => 当调用 delete() 或者 clean() 方法时随机清理1到x次.|
   +----------------------------------+------+----+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _zend.cache.backends.memcached:

Zend_Cache_Backend_Memcached
----------------------------

本后端把缓存纪录存储到memcached服务器. `memcached`_
是一个高性能的,分布式内存对象缓存系统.要使用此后端,你需要一个memecached守护进程(daemon)和
`memcache PECL 扩展`_.

注意 : 使用此后端当设置"doNotTestCacheValidity=true"参数时,不支持"tags"

可用的选项有:

.. _zend.cache.backends.memcached.table:

.. table:: Memcached 后端选项

   +-----------+-------+-------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |选项         |数据类型   |默认值                                                                      |描述                                                                                                                                                                 |
   +===========+=======+=========================================================================+===================================================================================================================================================================+
   |servers    |array  |array(array('host' => 'localhost','port' => 11211, 'persistent' => true))|一个memcached服务器数组;其中每个memcached服务器描述为一个关联数组: 'host' => (string) : memcached服务器的名称, 'port' => (int) : memcached服务器端口, 'persistent' => (bool) : 是否使用到memcached服务器的持久连接|
   +-----------+-------+-------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |compression|boolean|false                                                                    |如果你想使用数据压缩,设置为true                                                                                                                                                 |
   +-----------+-------+-------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _zend.cache.backends.apc:

Zend_Cache_Backend_Apc
----------------------

此后端通过 `APC`_ (Alternative PHP Cache) 扩展把缓存纪录存储于共享内存中
(当然为使用此后端,APC是需要的).

注意 : 使用此后端当设置"doNotTestCacheValidity=true"参数时,不支持"tags"

此后端没有选项.

.. _zend.cache.backends.xcache:

Zend_Cache_Backend_Xcache
-------------------------

整个后端通过 `XCache`_ 扩展（它当然需要使用这个后端）
在共享内存里存储了缓存记录。

小心：用这个后端，目前不支持 ”tags“，因为 "doNotTestCacheValidity=true" 参数。

可用的选项如下：

.. _zend.cache.backends.xcache.table:

.. table:: Xcache backend 选项

   +--------+------+----+----------------------------------------------------------------------------+
   |选项      |数据类型  |缺省值 |描述                                                                          |
   +========+======+====+============================================================================+
   |user    |string|null|xcache.admin.user, necessary for the clean() method                         |
   +--------+------+----+----------------------------------------------------------------------------+
   |password|string|null|xcache.admin.pass (in clear form, not MD5), necessary for the clean() method|
   +--------+------+----+----------------------------------------------------------------------------+

.. _zend.cache.backends.platform:

Zend_Cache_Backend_ZendPlatform
-------------------------------

本后端使用 `Zend Platform`_\ 产品的内容缓存API. 要使用此后端必须安装Zend Platform.

本后端支持标记(tags),但不支持 *CLEANING_MODE_NOT_MATCHING_TAG*\ 清除模式.

当使用 *Zend_Cache::factory()*\ 方法时,在字 'Zend' 和 'Platform'之间使用字分隔符-- '-', '.', ' ',
or '\_'指定此后端:

.. code-block:: php
   :linenos:

   $cache = Zend_Cache::factory('Core', 'Zend Platform');


此后端没有选项.



.. _`memcached`: http://www.danga.com/memcached/
.. _`memcache PECL 扩展`: http://pecl.php.net/package/memcache
.. _`APC`: http://pecl.php.net/package/APC
.. _`XCache`: http://xcache.lighttpd.net/
.. _`Zend Platform`: http://www.zend.com/products/platform
