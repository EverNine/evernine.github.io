Rally
========================

Rally是一个OpenStack基准测试工具，可以用于功能验证，基准测试和性能分析。

其主要功能有：

1. 部署：通过devstack、fuel、anvil等工具部署一套新的OpenStack，或是直接使用已有的OpenStack环境；
2. 验证：通过tempest等第三方测试框架进行功能验证；
3. 基准测试：通过参数化的测试用例对OpenStack加压，并统计api响应时长。


.. image:: https://wiki.openstack.org/w/images/thumb/e/ee/Rally-Actions.png/1700px-Rally-Actions.png

Rally的整体架构十分清晰，所有功能组件都是以插件的形式进行集成，十分易于扩展。

.. image:: http://rally.readthedocs.io/en/latest/_images/Rally-Plugins.png

上图左侧的四类插件负责了实际的用例执行过程。

一个yaml文件或json文件中的用例，在执行前由Context Plugin为其生成所需的资源，如租户、网络、虚机等。

完成资源创建后，Runner Plugin会根据用例执行方式启动对应数量的子进程来执行用例，在Context Plugin中创建的资源由Runner进行分配并通过self.context传入子进程中。

Scenario Plugin负责了子进程中的用例执行，每一个用例从一个或多个Scenario Plugin继承。

用例执行结束后，由SLA Plugin对用例结果进行统计与分析。
