.. PM2.5 documentation master file, created by
   sphinx-quickstart on Mon Jul  6 21:16:59 2015.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

进阶指南
========

Contents:

.. code-block:: python
   :emphasize-lines: 3,5

   def some_function():
       interesting = False
       print 'This line is highlighted.'
       print 'This one is not...'
       print '...but this one is.'

内部实现
--------

PM2.5的内部实现

当Node进程通过PM2.5启动时，PM2.5 CLI会同云端服务进行握手，握手成功后才会源源不断的进行数据的上报。上报时首先会将数据进行AES256加密，然后使用TCP通信将数据上报到服务器，这里用到了开源的Axon，云端服务器收到数据后会将数据入库存储到MongoDB中，同时会进行监控报警的扫描，如果当前数据符合用户订阅的监控报警条件，则会通过云端的Push服务向iOS客户端推送报警信息。云端同时运行WebSocket服务，为多个终端（Web平台、iOS应用）提供实时数据的推送。

这里值得一提的是，PM2.5的客户端是基于React-Native开发，目前已经提交Apple Store正在审核，审核通过后就可以从Apple Store中下载到了，客户端提供了服务和进程基本指标的查看，同时可以配合Web平台的监控报警设置实现7x24小时对服务的监控。
