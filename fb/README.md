#### ie - iframe cookie f..

When facebook app is loading iframed url, internet explorer will not store the cookie given inside this iframe, unless you specify P3P header.

> [http://stackoverflow.com/questions/389456/cookie-blocked-not-saved-in-iframe-in-internet-explorer](http://stackoverflow.com/questions/389456/cookie-blocked-not-saved-in-iframe-in-internet-explorer) [http://adamyoung.net/IE-Blocking-iFrame-Cookies](http://adamyoung.net/IE-Blocking-iFrame-Cookies)

```ruby
class App < Sinatra::Base
  enable :sessions
  after do
    response.headers["X-Frame-Options"]='GOFORIT'
    response.headers["P3P"] = 'CP="CAO DSP COR CURa ADMa DEVa OUR IND PHY ONL UNI COM NAV INT DEM PRE"'
  end
end
```

#### oauth redirect stops in the middle

Sometimes if you do not have oauth dialog displayed @ top.location.href, the oauth redirect might stop at blank page with facebook logo, using ```<script type='text/javascript'>top.location.href = 'oauth-url';</script>``` and adding ```&type=user_agent&display=page``` to the oauth url fixes the problem (THANKS @matthewphiong).

> [http://matthewphiong.com/facebook-oauth-2-0-for-canvas-app-explained](http://matthewphiong.com/facebook-oauth-2-0-for-canvas-app-explained) [http://stackoverflow.com/questions/3942260/how-to-use-facebook-oauth-2-0-authentication-like-zynga-and-other-use-it](http://stackoverflow.com/questions/3942260/how-to-use-facebook-oauth-2-0-authentication-like-zynga-and-other-use-it)

```ruby
class App < Sinatra::Base
  get '/fb-oauth-redirect-top'
    url = 'https://graph.facebook.com/oauth/authorize?client_id=.........&scope=email%2Coffline_access%2Cuser_birthday&response_type=code&type=user_agent&display=page'
    "<script type='text/javascript'>top.location.href = '#{url}';</script>"
  end
end
```

