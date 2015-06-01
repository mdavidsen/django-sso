django-sso will allow your django application to accept single sign on links from other applications and authenticate users. It is also capable of creating links to other applications that use SSO links.

Add sso to your python path, INSTALLED\_APPS, and middleware. The middleware needs to be **after Session Middleware**
```
    'sso.middleware.SingleSignOnMiddleware',
```

SSO\_SECRET is a required setting. You can use it like the following or set your own.
```
SSO_SECRET = SECRET_KEY
```


If you will be creating sso links with your django app, this is required.
```
    url(r'^sso/$', 'sso.views.sso', name="sso"),
```

With that you can create links with the following in your templates
```
{% url sso %}?next=http://ivylees.com
```
That will create a url like
```
http://ivylees.com/?id=123&timestamp=1234&token=12345
```

If you want to automatically replace all links to another domain, add them to this tuple. All of the following types of urls will work.
```
SSO_DOMAINS = (
    'ivylees.com/user/',
    'presskitn.com',
    'http://codespatter.com',
)
```