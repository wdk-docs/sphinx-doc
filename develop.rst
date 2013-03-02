:orphan:

Sphinx开发
==================

Sphinx是一组志愿者维护的。我们珍惜每个贡献！

* 可以在 `Mercurial <http://bitbucket.org/birkenfeld/sphinx/>`_ 仓库中找到代码.
* 在 `追踪系统 <http://bitbucket.org/birkenfeld/sphinx/issues/>`_ 中提问和功能申请
* 开发邮件列表 `Google 组 <http://groups.google.com/group/sphinx-dev/>`_.

欲了解更多关于我们的开发过程和方法, 查看 :doc:`devguide`.


扩展
==========

`sphinx-contrib <http://bitbucket.org/birkenfeld/sphinx-contrib/>`_ 
库包含了许多贡献的扩展.  它们中的一些在PyPI上有发布版本, 其它你可以检出再安装.

下面是仓库中当前贡献的扩展列表:

- aafig: 使用 aafigure_ 把嵌入式的ASCII艺术渲染为一个好图.
- actdiag: 使用 actdiag_ 嵌入活动图
- adadomain: 支持Ada扩展 (需要Sphinx 1.0)
- ansi: 解析文档中ANSI颜色序列.
- autorun: 在runblock指令中执行代码.
- blockdiag: 使用 blockdiag_ 嵌入框图
- cheeseshop: 很容易地连接到PyPI包
- clearquest: 从 ClearQuest_ 查询创建表。
- coffeedomain: （自动）记录CoffeeScript的源代码的域。
- context: ConTeXt创建器.
- doxylink: 连接到 Doxygen-generated HTML 文档
- email: 混淆的电子邮件地址
- erlangdomain: 支持Erlang的扩展 (需要Sphinx 1.0)
- exceltable: 在文档中使用 exceltable_ 嵌入Excel电子表格
- feed: 建立联合供稿和来自你网站内容的基于时间的概述的扩展
- gnuplot: 使用 gnuplot_ 语言产生的图像。
- googleanalytics: 跟踪HTML访客统计
- googlechart: 通过使用 `Google Chart`_ 嵌入图表
- googlemaps: 通过使用 `Google Maps`_ 嵌入地图
- httpdomain: 记录的RESTful HTTP的API域。
- hyphenator: 使用 hyphenator_ 的HTML的客户端连字符
- lilypond: 在PNG格式里插入 Lilypond_ 的音乐脚本的扩展.
- mscgen: embed mscgen-formatted MSC (Message Sequence Chart)s.
- nicoviceo: 从nicovideo嵌入视频
- nwdiag: 使用 nwdiag_ 内嵌网络图表
- omegat: 和 OmegaT_ 合作支持工具 (需要Sphinx 1.1)
- osaka: 转换标准的日本DOC为大阪方言 (它是笑话扩展)
- paverutils: Sphinx 和 Paver_的备用集成.
- phpdomain: 支持PHP的扩展
- plantuml: 使用 PlantUML_ 嵌入UML图表
- rawfiles: 复制原始文件，就像一个CNAME。
- requirements: 在你需要的地方声明需求（例如，在测试文档字符串），标记状态并收集他们到一个列表中
- rubydomain: 支持Ruby的扩展 (需要Sphinx 1.0)
- sadisplay: 显示SQLAlchemy的模型 sadisplay_
- sdedit: 使用快速序列插入序列图的扩展。图编辑器 (sdedit_)
- seqdiag: 使用 seqdiag_ 嵌入序列图
- slide: 嵌入 slideshare_ 和 其他网站 的演示幻灯片。
- swf: 内嵌flash文件
- sword: 插入来自 Sword_ 圣经经文的扩展。
- tikz: 使用 `TikZ/PGF LaTeX package`_ 画画.
- traclinks: 在Sphinx里创建 TracLinks_ 到 a Trac_ 实例
- whooshindex: whoosh indexer 扩展
- youtube: 内嵌来之 YouTube_ 的视频
- zopeext: 提供一个使用 `Zope interfaces`_ 的 ``autointerface`` 指令。

在入门指南中查看 :ref:`扩展文档 <exttut>`，和撰写自己的扩展。

.. _aafigure: https://launchpad.net/aafigure
.. _gnuplot: http://www.gnuplot.info/
.. _paver: http://www.blueskyonmars.com/projects/paver/
.. _Sword: http://www.crosswire.org/sword/
.. _Lilypond: http://lilypond.org/web/
.. _sdedit: http://sdedit.sourceforge.net/
.. _Trac: http://trac.edgewall.org
.. _TracLinks: http://trac.edgewall.org/wiki/TracLinks
.. _OmegaT: http://www.omegat.org/
.. _PlantUML: http://plantuml.sourceforge.net/
.. _PyEnchant: http://www.rfk.id.au/software/pyenchant/
.. _sadisplay: http://bitbucket.org/estin/sadisplay/wiki/Home
.. _blockdiag: http://blockdiag.com/
.. _seqdiag: http://blockdiag.com/
.. _actdiag: http://blockdiag.com/
.. _nwdiag: http://blockdiag.com/
.. _Google Chart: http://code.google.com/intl/ja/apis/chart/
.. _Google Maps: http://maps.google.com/
.. _hyphenator: http://code.google.com/p/hyphenator/
.. _exceltable: http://packages.python.org/sphinxcontrib-exceltable/
.. _YouTube: http://www.youtube.com/
.. _ClearQuest: http://www-01.ibm.com/software/awdtools/clearquest/
.. _Zope interfaces: http://docs.zope.org/zope.interface/README.html
.. _slideshare: http://www.slideshare.net/
.. _TikZ/PGF LaTeX package: http://sourceforge.net/projects/pgf/
