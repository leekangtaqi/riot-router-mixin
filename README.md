# riot-router-mixin

###Hello, router

a micro router mixin based riotjs

a componentized router, koa or express like.
    
you can define router in any tag easily ( nesting define router and middleware support).

###Demo

https://github.com/leekangtaqi/riot-router-mixin-example

###Install

    npm install riot-router-mixin
  
###Usage

```js

<parent>
  <child></child>
  this.mixin('router');
  this.use(function(next){
    console.log(this); //'this' is context object, contains path_to string and request object
    //filter...
    console.log('middleware1')
    next();
  })
  this.use(function(next){
    //filter...
    console.log('middleware2')
    next();
  })
  this.routeConfig = [{
    path: '/children/_:id',
    name: 'child'
  }]
</parent>

<child>
  <nest></nest>
  this.on('open', ctx={
    assert.equal(ctx.request.query.id, 111)  //when route to /children/_111
    //...do some sync or async action
    this.trigger('ready');
  })
  //define nest-route
  //...this.routeConfig
</child>

```

###API

####tag.routeConfig(options: Object)

#####options#path: String

the sub-tag corresponding URL

the pattern is similar to koa or express

eg: 

1. /user/_:id
2. /user?id=xxx

#####options#name: String

sub-tag name.

#####options#before(done: Function)

a hook fn, trigger when the parent tag route to sub-tag.

the route will be continue only apply done function.

#####options#defaultRoute: Boolean

set the current url to a default router.

####tag.use: Function

koa and express like middleware, route filter

use#next: Function

call next to continue

####tag.on('open', fn: Function)

fn will apply when route to current tag.

####tag.ready()

the tag will be presented when invocate ready,

and then trigger sub-child's open event.


    
