django-redis-sessions
=======================

fork of ``martinrusev/django-redis-sessions``

Redis database backend for your sessions and sharing with expressjs

------------
Installation
------------

1. Get ``redis_sessions`` into ``site-packages`` or otherwise into ``PYTHON_PATH``

2. Set ``redis_sessions.session`` as your session engine, like so::

       SESSION_ENGINE = 'redis_sessions.session'

3. Replace ``django.contrib.sessions.middleware.SessionMiddleware`` with ``redis_sessions.middleware.SessionMiddleware``
		
4. Optional settings::

       SESSION_REDIS_HOST = 'localhost'
       SESSION_REDIS_PORT = 6379
       SESSION_REDIS_DB = 0
       SESSION_REDIS_PASSWORD = 'password'
		
5. Configure your expressjs app::

  var RedisStore = require('connect-redis')(express);
  app.use(express.cookieParser());
  app.use(express.session({
    key: 'sessionid',
    secret: 'lulcats are uber sekrit', // This should be SECRET_KEY from settings.py
    store: new RedisStore({
      prefix: '',
    }),
    cookie: {
      maxAge: 1209600 * 1000,
    },
    fingerprint: function (s) { return ''; },
  }));


I haven't done much testing beyond making sure sessions aren't immediately
invalidated
