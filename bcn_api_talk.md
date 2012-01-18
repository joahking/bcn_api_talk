!SLIDE

# APIs, some thoughts

!SLIDE

## About me :-)

* working with Rails since 2006
* tests addict since 2007 (do you remember tests peepcodes?)
* I work for [3scale](http://www.3scale.net) an SaaS startup "API Management Platform" since 2010
* I love paragliding http://para.pent.es

!SLIDE

## main points of this talk

it all depends, see your choices, choose wisely

* inside and outside point of view

inside means
* code organization/beauty
* team developing speed

outside means
* who's using your api?

!SLIDE

## main points on APIs

* APIs are hard to change, design them carefully
* speed is a major concern
* test them, test them and test them!
* documentation

!SLIDE

## APIs changed? omg!?!?

if your API is for clients consumption:

* very problematic
* you are **out of control** of how your users parse your data (they can even be using regexps!)

so...
* adding a new node/attr to object => bad
* even bug fixing is a problem!    => bad
* adding a new url => fine

that being said try be strict with testing and return same resource representation always

!SLIDE

## so... design

outside
* URLs, they are the API, REST
* versions, they aid you at changing
* pagination (speed)
* light responses (speed)

!SLIDE

## versioning

lots of controversy around. Main ways are:

* as a param, http://para.pent.es/flying_sites.json?version=1

* in the path, (twitter does it!)
e.g. (version 1) http://para.pent.es/1/flying_sites.json
but "cool urls don't change"

* in the headers
Accept: your/media-type; version=X
Content-Type: your/media-type; version=X

this last way allows the client to say which range of versions it can handle, and server to decide which one to respond with

wanz moar? e.g. http://freelancing-gods.com/posts/versioning\_your\_ap\_is

!SLIDE

## versions? yes, but...

they do not solve everything, because:

* you need to have your clients to change their end
* maintenance cost if some of the clients remain behind in versions

!SLIDE

## pagination

speed is your main concern here

main ways are:
* as attr in collection root element, e.g.

* as elements itself, e.g.

!SLIDE

## urls

they are important in web app, but in APIs lots more

* main way of referring to are very important, RESTfull a.s.o
* namespaces. e.g. http://api.pent.es/flying_sites.json

!SLIDE

## resources

* do not expose your objects directly, think carefully, you can be exposing your db (object modeling)
* nested object inside objects (try to avoid, better use _counters or so and then another call to fetch nested ones)

!SLIDE

## implementation

you chose a subdomain (api.pent.es) or a namespace (para.pent.es/api/...)

* separated controllers (speed by leaving out views support inclusion)

!SLIDE

## url parameters:

* nesting, try to keep it

!SLIDE code

see rails typical params

@@@ ruby
{"action"=>"...", "controller"=>"users", "format" => "xml", "id" => "unnested", "name" => "BANG!" }
@@@

!SLIDE

## url params suggestion?

come up with a convention, e.g. first underscore separate resource

!SLIDE

## miscellaneous

* api typical login via param

!SLIDE

##
* separated controllers (speed by leaving out views support inclusion)
* to_xml vs builders (speed!) cache may be better in the second
* rails builder is a pain, beware
* nokogiri fast but no skip_instruct

!SLIDE

## test
* lint tests every request (suggestion?)

!SLIDE

## documentation

* swagger http://swagger.wordnik.com/

!SLIDE

# gracias

# Questions?
