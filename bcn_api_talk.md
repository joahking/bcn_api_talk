!SLIDE

# APIs, some thoughts

(btw: Stop SOPA!, Stop PIPA!)

!SLIDE

## About me :-)

* working with Rails since 2006
* tests addict since 2007 (do you remember 2007 tests' peepcodes?)
* since 2010 working for [3scale](http://www.3scale.net) an SaaS startup "API Management Platform"
* I love paragliding http://para.pent.es

!SLIDE

## main points of this talk

it all depends, see your choices, choose wisely

!SLIDE

## APIs from inside and outside

outside
* who's using your api?
* design
* change responsability

inside
* code Maintainability/Organization/Beauty
* team developing speed
* cheap

!SLIDE

## main points on APIs

* APIs are hard to change, design them carefully
* speed is a major concern
* test them, test them and test them!
* live documentation (bonus)

!SLIDE

## APIs changed? omg!?!?

if your API is for clients consumption:

* very problematic
* you are **out of control** of how your users parse your data 

(they can even be using regexps!)

!SLIDE

## colors of change

* adding a new node/attr to object => red
* even bug fixing is a problem!    => red

* adding a new url => green

!SLIDE

## being ready for change

* clients communication!
* versioning

!SLIDE

## so... API design

outside
* URLs, they are the API, REST
* resources design: xml, json (should be the same throughtout the API)
* versions, they aid you at changing
* pagination (speed)
* light responses (speed)

!SLIDE

## urls

they are important in web app, but in APIs lots more

* main way of referring to your end, RESTful

* subdomain. e.g. http://api.pent.es/flying_sites.json
* namespaces. e.g. http://para.pent.es/api/flying_sites.json

* direct. e.g. http://para.pent.es/flying_sites.json (but really not a choice)

!SLIDE

## resources

should be the same throughtout the API

* do not expose your objects directly

you can be exposing your db

(and making your clients cry seeing your object model)

!SLIDE

## resources

* nest object inside objects?

(bad for speed and design)

bad:

<user>
  <plans>
    <plan>
      <name>...</name>
    </plan>
  </plans>
</user>

good:

<user>
  <plan_ids>1,6</plan_ids>
</user>

sexy (but keep an eye on speed):

<user>
  <plans>
    <plan>api.pent.es/plans/1</plan>
    <plan>api.pent.es/plans/6</plan>
  </plans>
</user>

!SLIDE

## versioning

lots of controversy around. Main ways are:

* as a param, http://para.pent.es/flying_sites.json?version=1

* in the path, (twitter does it!)
e.g. 
(version 1) http://para.pent.es/1/flying_sites.json

but "cool urls don't change"

* in the headers
Accept: your/media-type; version=X
Content-Type: your/media-type; version=X

allows the client to say which range of versions it can handle, and the server to decide which one to respond with

wanz moar? e.g. http://freelancing-gods.com/posts/versioning\_your\_ap\_is

!SLIDE

## versions? yes, but...

they do not solve everything, because:

* you need to have your clients to change their end
* maintenance cost of different versions

!SLIDE

## pagination

speed is your main concern here

main ways are:
* as attr in collection root element

<users page=".." per_page => ".." pages => "..">


* as elements itself

{ :page => .., :per_page => .., :pages => .. }

!SLIDE

## Coding decision points

let's see some Rails

!SLIDE code

# first decision point
class UsersController < ApplicationController
  # second decision point
  before_filter :login_required

  def index
    respond_to do |format|
      format.html
      format.xml # third decision point
    end
  end
end

!SLIDE

## 1 Decision Point: prefer separated controllers

class Api::UsersController < Api::BaseController

* you save loading lots of support the full app needs
* speed
* code separated, good for team speed

!SLIDE

## or a leaner stack

* sinatra + sequel
* padrino
* rack

speed, less memory footprint

!SLIDE

## 2 Decision Point: api login

http://para.pent.es/api/flying_sites.json?key=SHA1

avoid overriding login_required

  before_filter :api_login_required

!SLIDE

## 3 Decision Point: to_xml vs builders in views

to_xml
* way faster (no view handling involved)
* simplicity

(at 3scale we are implementing a lego-like api cache on redis, should be trailing fast)

builders
* lots of people prefers them
* cache may be easier to set in Rails

!SLIDE code

class Api::UsersController < Api::BaseController
  before_filter :api_login_required

  def index
    respond_to do |format|
      format.js
      format.xml
    end
  end

end

!SLIDE

## coding insides

* rails builder is a pain, beware of using instruct on him
* nokogiri fast but no skip_instruct

!SLIDE

## test the API

* lint tests every request

!SLIDE

## profile your API

* ab

!SLIDE

## documentation to play with

* swagger http://swagger.wordnik.com/

will 3scale be providing here?

!SLIDE

# gracias

# Questions?

(btw: Stop SOPA!, Stop PIPA!)
