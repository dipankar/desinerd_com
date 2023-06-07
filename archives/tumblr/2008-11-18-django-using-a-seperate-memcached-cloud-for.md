---
layout: post
title: 'Django : using a seperate memcached cloud for sessions'
date: '2008-11-18T10:43:22+05:30'
tags:
- code
- django
- help
- media
- memcached
- multiple
- tutorial
tumblr_url: http://www.desinerd.com/post/150535098473/django-using-a-seperate-memcached-cloud-for
---
When you are using a platform like django you realise how slow sessions can get when you are using the database as a backend. The problem of using a memory cache like memcached is the fact that when you restart the server to refresh the cache or remove stale objects, the problem is that you lose your sessions data and a lot of people using your site get logged out. The only solution to this problem is to use 2 memcached instances , one for your regular python objects and another for your sessions objects … this is not a default feature in Django. So here is the solution to this particular problem.


In your project directory create the following files, the first file is basically a copy of a core django file (contrib/sessions/backends/cache.py) and the second is a file where the class gets initialized (its not necessary , but a good example).

/session_backend.py

from django.contrib.sessions.backends.base import SessionBase, CreateError
from kwippyproject.session_cache import cache

class SessionStore(SessionBase):
    """
    A cache-based session store.
    """
    def __init__(self, session_key=None):
        self._cache = cache
        super(SessionStore, self).__init__(session_key)

    def load(self):
        session_data = self._cache.get(self.session_key)
        if session_data is not None:
            return session_data
        self.create()
        return {}

    def create(self):
        # Because a cache can fail silently (e.g. memcache), we don''t know if
        # we are failing to create a new session because of a key collision or
        # because the cache is missing. So we try for a (large) number of times
        # and then raise an exception. That''s the risk you shoulder if using
        # cache backing.
        for i in xrange(10000):
            self.session_key = self._get_new_session_key()
            try:
                self.save(must_create=True)
            except CreateError:
                continue
            self.modified = True
            return
        raise RuntimeError("Unable to create a new session key.")

    def save(self, must_create=False):
        if must_create:
            func = self._cache.add
        else:
            func = self._cache.set
        result = func(self.session_key, self._get_session(no_load=must_create),
                self.get_expiry_age())
        if must_create and not result:
            raise CreateError

    def exists(self, session_key):
        if self._cache.get(session_key):
            return True
        return False

    def delete(self, session_key=None):
        if session_key is None:
            if self._session_key is None:
                return
            session_key = self._session_key
        self._cache.delete(session_key)


/session_cache.py

from django.core.cache.backends.memcached import CacheClass
from django.conf import settings

scheme, rest = settings.SESSION_CACHE.split('':'', 1)
host = rest[2:-1]
cache = CacheClass(host,{})


In your settings file you need to make the following changes
/settings.py


SESSION_ENGINE = "kwippyproject.session_backend"
SESSION_CACHE = ''memcached://127.0.0.1:11200/''


Restart, start a memcached server on port 11200 and see your site becoming that much more faster :). Keep coding and in any problems with this approach feel free to mail me on me@dipankar.name.
