!SLIDE

# APIs, some thoughts

(btw: Stop SOPA!, Stop PIPA!)

!SLIDE

## About me (before you run away)

Joaquin Rivera Padron (a.k.a joahking)

* working: Rails since 2006
* tests addict since 2007 (do you remember peepcodes on tests back in 2007?)
* since 2010 working for [3scale](http://www.3scale.net) an SaaS startup "API Management Platform"
* I love paragliding

!SLIDE

## APIs from inside and outside

!SLIDE

## outside

* who's using your api?
* design
* change responsability

!SLIDE

## inside

* code Maintainability/Organization/Beauty
* team developing speed
* cheap

!SLIDE

## main concerns

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
* resources design: xml, json (should be the same throughout the API)

!SLIDE

* versions, they aid you at changing
* pagination (speed)
* light responses (speed)

!SLIDE

## urls

they are important in web app, but in APIs lots more

* main way of referring to your end, RESTful

!SLIDE

* subdomain. e.g. http://api.pent.es/flying_sites.json
* namespaces. e.g. http://para.pent.es/api/flying_sites.json

* direct. e.g. http://para.pent.es/flying_sites.json (but really not a choice)

!SLIDE

## resources

should be the same throughout the API

!SLIDE

* do not expose your objects directly

why expose your db?

!SLIDE

(and make your clients cry seeing your object model)

!SLIDE

## resources

* nest object inside objects?

!SLIDE

bad for speed and design:

:user => { :plans => { :plan => { :name => "bad" }}}

!SLIDE

good:

:user => { :plans => [1,6] }

!SLIDE

sexy:

:user => { :plans => ["api.pent.es/plans/1.json", "api.pent.es/plans/6.json"]}

(but keep an eye on speed)

!SLIDE

## versioning

lots of controversy around. Main ways are:

!SLIDE

* as a param

http://para.pent.es/flying_sites.json?version=1

!SLIDE

* in the path (version 1)


http://para.pent.es/1/flying_sites.json


twitter does it!, but "cool urls don't change"

!SLIDE

* in the headers

Accept: your/media-type; version=X

Content-Type: your/media-type; version=X


allows the client to say which range of versions it can handle, and the server to decide which one to respond with

!SLIDE

wanz moar? e.g. http://freelancing-gods.com/posts/versioning\_your\_ap\_is

!SLIDE

## versions? yes, but...

they do not solve everything, because:

* you need to have your clients to change their end
* maintenance cost of different versions (but there are some good solutions around)

!SLIDE

## pagination

speed is your main concern here

!SLIDE

* as attr in collection root element

<users page="1" per_page="20" pages="20">

!SLIDE

* as elements itself

:users => { :page => .., :per_page => .., :pages => .., :username => ..}

!SLIDE code

## Coding decision points

 # first decision point

class UsersController < ApplicationController

  # second decision point

  before\_filter :login\_required

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

!SLIDE

avoid overriding login_required

  before_filter :api\_login\_required

!SLIDE

## 3 Decision Point: to_xml vs builder views

to_xml

* way faster (no view handling involved)
* simplicity

!SLIDE

## builder views

* lots of people prefers them
* cache may be easier to set in Rails

!SLIDE code

class Api::UsersController < Api::BaseController
  before\_filter :api\_login_required

  def index
    respond_to do |format|
      format.js
      format.xml
    end
  end
end

!SLIDE

## coding insides

* rails XmlBuilder is a pain, beware of using instruct on him

!SLIDE

* nokogiri builder fast but no skip_instruct (easy to patch)

!SLIDE

## test the API

* (idea) lint tests every response

!SLIDE

## profile your API

* ab

!SLIDE

## documentation to play with

* swagger http://swagger.wordnik.com/

!SLIDE

# gracias

!SLIDE

# Questions?

(btw: Stop SOPA!, Stop PIPA!)
