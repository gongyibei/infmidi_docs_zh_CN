Viewer
======

使用 ``Viewer`` 来实时显示 ``Clip`` 里的音符。

使用
----

.. code:: python

    >>> from infmidi.devices import Viewer
    
    # 创建Clip
    >>> clip = Clip()

    # 创建 Viewer
    >>> viewer = Viewer(clip, port=7777) 
    Open this link in your browser: http://1.0.0.127.in-addr.arpa:7777

    # 在浏览器中打开上述生成的链接。然后再对clip进行修改, 就可以实时预览了.
    
