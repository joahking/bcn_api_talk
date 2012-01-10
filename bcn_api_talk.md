!SLIDE

# APIs

!SLIDE

## concerns

* start simple (kiss her)
* design
* speed
* change ratio
* test, test and test
* do not expose whole objects

* api typical login via param
* versions strategies
* pagination

* nested object inside objects (try to avoid, better _counters)

* separated controllers (speed by leaving out views support inclusion)
* to_xml vs builders (speed!) cache may be better in the second
* rails builder is a pain, beware
* nokogiri fast but no skip_instruct
* lint tests every request (suggestion?)

!SLIDE

## APIs changes?

* problematic
* you are of control of how your users parse your data
* even bug fixing is a problem!

!SLIDE

## versions?

yes, but you need to talk upfront to clients, to have them change their end

maintenance cost

!SLIDE

## design

* urls: are very important, RESTfull a.s.o
* resource representation should be the same

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

Google is [here](http://google.com)

!SLIDE

# Questions?
