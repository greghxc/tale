---
layout: post
title:  "Better Errors Using the Google My Business API Java Client"
author: "Greg"
comments: true
---
![placeholder](https://farm5.staticflickr.com/4215/34664199694_abf41b2606_c.jpg "Large example image")

I wanted to do a thing, and maybe you do to! It goes something like this.
<!--more-->
{% highlight scala %}
object GooglePlacesQuoteService extends App with Directives {
  implicit val system = ActorSystem()
  val config = ConfigFactory.load()
  implicit val executor = system.dispatcher
  implicit val materializer = ActorMaterializer()
  val logger = Logging(system, getClass)

  val placesService: PlacesService = new PlacesService
  val quotesService: QuotesService = new QuotesService
  val profilesService: ProfilesService = new ProfilesService
  val swaggerDocService: SwaggerDocsService = new SwaggerDocsService(system)
  val swaggerUIService: SwaggerUIService = new SwaggerUIService
  val healthService: HealthService = new HealthService

  val routes = placesService.routes ~ quotesService.routes ~
    profilesService.routes ~ swaggerDocService.routes ~
    swaggerUIService.routes ~ healthService.routes

  Http().bindAndHandle(
    routes, config.getString("http.interface"), config.getInt("http.port")
  )
}
{% endhighlight %}
