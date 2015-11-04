.. _model_problem:

***********************
some model problems
***********************

在开发过程中遇到的一些 `model` 相关的问题


.. _django-debug-toolbar:

django-debug-toolbar的jquery.js访问问题
======================================

由于 `django-debug-toolbar` 的 `jquery` 原路径为 https//ajax.googleapis.com/ajax/libs/jquery/2.1.0/jquery.min.js,
访问速度很慢，或因 GFW 根本无法访问，所以会出现 `django-debug-toolbar` 无法正常使用的问题。

在 `django-debug-toolbar` 安装目录下 site-packages/debug_toolbar/settings.py 中的原配置为::

    ......
    CONFIG_DEFAULTS = { # Toolbar options
    'DISABLE_PANELS': set(['debug_toolbar.panels.redirects.RedirectsPanel']),
    'INSERT_BEFORE': '</body>',
    'JQUERY_URL': '//ajax.googleapis.com/ajax/libs/jquery/2.1.0/jquery.min.js',
    'RENDER_PANELS': None,
    'RESULTS_STORE_SIZE': 10,
    'ROOT_TAG_EXTRA_ATTRS': '',
    'SHOW_COLLAPSED': False,
    'SHOW_TOOLBAR_CALLBACK': 'debug_toolbar.middleware.show_toolbar', # Panel options
    'EXTRA_SIGNALS': [],
    'ENABLE_STACKTRACES': True,
    'HIDE_IN_STACKTRACES': ( 'socketserver' if six.PY3 else 'SocketServer',
    'threading', 'wsgiref', 'debug_toolbar', 'django', ),
    'PROFILER_MAX_DEPTH': 10,
    'SHOW_TEMPLATE_CONTEXT': True,
    'SQL_WARNING_THRESHOLD': 500, # milliseconds}
    USER_CONFIG = getattr(settings, 'DEBUG_TOOLBAR_CONFIG', {})
    ......

在 `django` 项目文件的主配置文件 settings.py 中添加如下项::

    DEBUG_TOOLBAR_CONFIG = { ##'JQUERY_URL': '//ajax.googleapis.com/ajax/libs/jquery/2.1.0/jquery.min.js',
    'JQUERY_URL': '/static/admin/js/jquery.js', }

即让 `jquery.js` 访问至 APP admin 下的对应文件 django/contrib/admin/static/admin/js/jquery.js
本机访问，不需要联网，更不怕 GFW 的阻止了
