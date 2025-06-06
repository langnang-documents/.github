---
created: 2023-03-07T19:42:44 (UTC +08:00)
tags: []
source: https://overapi.com/express
author: OverAPI
---

# ExpressJS v 4x Cheat Sheet | OverAPI.com

> ## Excerpt
> OverAPI.com is a site collecting all the cheatsheets,all!

---
## Application

-   [express()](http://expressjs.com/4x/api.html#express)
-   [application settings](http://expressjs.com/4x/api.html#app-settings)
-   [app.set()](http://expressjs.com/4x/api.html#app.set)
-   [app.get()](http://expressjs.com/4x/api.html#app.get)
-   [app.enable()](http://expressjs.com/4x/api.html#app.enable)
-   [app.disable()](http://expressjs.com/4x/api.html#app.disable)
-   [app.enabled()](http://expressjs.com/4x/api.html#app.enabled)
-   [app.disabled()](http://expressjs.com/4x/api.html#app.disabled)
-   [app.use()](http://expressjs.com/4x/api.html#app.use)
-   [app.engine()](http://expressjs.com/4x/api.html#app.engine)
-   [app.param()](http://expressjs.com/4x/api.html#app.param)
-   [application routing](http://expressjs.com/4x/api.html#app.VERB)
-   [app.all()](http://expressjs.com/4x/api.html#app.all)
-   [app.route()](http://expressjs.com/4x/api.html#app.route)
-   [app.locals](http://expressjs.com/4x/api.html#app.locals)
-   [app.render()](http://expressjs.com/4x/api.html#app.render)
-   [app.listen()](http://expressjs.com/4x/api.html#app.listen)

Request

-   [req.params](http://expressjs.com/4x/api.html#req.params)
-   [req.query](http://expressjs.com/4x/api.html#req.query)
-   [req.param()](http://expressjs.com/4x/api.html#req.param)
-   [req.route](http://expressjs.com/4x/api.html#req.route)
-   [req.cookies](http://expressjs.com/4x/api.html#req.cookies)
-   [req.signedCookies](http://expressjs.com/4x/api.html#req.signedCookies)
-   [req.get()](http://expressjs.com/4x/api.html#req.get)
-   [req.accepts()](http://expressjs.com/4x/api.html#req.accepts)
-   [req.acceptsCharset()](http://expressjs.com/4x/api.html#req.acceptsCharset)
-   [req.acceptsLanguage()](http://expressjs.com/4x/api.html#req.acceptsLanguage)
-   [req.is()](http://expressjs.com/4x/api.html#req.is)
-   [req.ip](http://expressjs.com/4x/api.html#req.ip)
-   [req.ips](http://expressjs.com/4x/api.html#req.ips)
-   [req.path](http://expressjs.com/4x/api.html#req.path)
-   [req.host](http://expressjs.com/4x/api.html#req.host)
-   [req.fresh](http://expressjs.com/4x/api.html#req.fresh)
-   [req.stale](http://expressjs.com/4x/api.html#req.stale)
-   [req.xhr](http://expressjs.com/4x/api.html#req.xhr)
-   [req.protocol](http://expressjs.com/4x/api.html#req.protocol)
-   [req.secure](http://expressjs.com/4x/api.html#req.secure)
-   [req.subdomains](http://expressjs.com/4x/api.html#req.subdomains)
-   [req.originalUrl](http://expressjs.com/4x/api.html#req.originalUrl)

Response

-   [res.status()](http://expressjs.com/4x/api.html#res.status)
-   [res.set()](http://expressjs.com/4x/api.html#res.set)
-   [res.get()](http://expressjs.com/4x/api.html#res.get)
-   [res.cookie()](http://expressjs.com/4x/api.html#res.cookie)
-   [res.clearCookie()](http://expressjs.com/4x/api.html#res.clearCookie)
-   [res.redirect()](http://expressjs.com/4x/api.html#res.redirect)
-   [res.location()](http://expressjs.com/4x/api.html#res.location)
-   [res.send()](http://expressjs.com/4x/api.html#res.send)
-   [res.json()](http://expressjs.com/4x/api.html#res.json)
-   [res.jsonp()](http://expressjs.com/4x/api.html#res.jsonp)
-   [res.type()](http://expressjs.com/4x/api.html#res.type)
-   [res.format()](http://expressjs.com/4x/api.html#res.format)
-   [res.attachment()](http://expressjs.com/4x/api.html#res.attachment)
-   [res.sendfile()](http://expressjs.com/4x/api.html#res.sendfile)
-   [res.download()](http://expressjs.com/4x/api.html#res.download)
-   [res.links()](http://expressjs.com/4x/api.html#res.links)
-   [res.locals](http://expressjs.com/4x/api.html#res.locals)
-   [res.render()](http://expressjs.com/4x/api.html#res.render)

Router

-   [Router()](http://expressjs.com/4x/api.html#router)
-   [router.use()](http://expressjs.com/4x/api.html#router.use)
-   [router.param()](http://expressjs.com/4x/api.html#router.param)
-   [router.route()](http://expressjs.com/4x/api.html#router.route)
-   [router.VERB()](http://expressjs.com/4x/api.html#router.VERB)

Middleware

-   [bodyParser()](https://github.com/expressjs/body-parser)
-   [compress()](https://github.com/expressjs/compression)
-   [cookieParser()](https://github.com/expressjs/cookie-parser)
-   [cookieSession()](https://github.com/expressjs/cookie-session)
-   [csrf()](https://github.com/expressjs/csurf)
-   [errorhandler()](https://github.com/expressjs/errorhandler)
-   [methodOverride()](https://github.com/expressjs/method-override)
-   [morgan()](https://github.com/expressjs/morgan)
-   [responseTime()](https://github.com/expressjs/response-time)
-   [favicon()](https://github.com/expressjs/serve-favicon)
-   [directory()](https://github.com/expressjs/serve-index)
-   [serveStatic()](https://github.com/expressjs/serve-static)
-   [timeout()](https://github.com/expressjs/timeout)
-   [vhost()](https://github.com/expressjs/vhost)
-   [session()](https://github.com/expressjs/session)
