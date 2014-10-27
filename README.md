[Alina Recommendation](http://alinapi.com/) — Javascript-based  Recommendation Engine (Hosted in the Alina Inteliigence Cloud)
==================================================

Contribution Guides
--------------------------------------

In the spirit of open source software development, we always encourages community code contribution. To help you get started and before you jump into writing code, please check out this demo with sample code.

1. [Demo](http://alinapi.com/demos/recommend)



Environments in which to use Alina Recommendation
--------------------------------------

-You can run ALINA from your localhost for testing; however, sites and associated products/recommendations are segmented by domain. Therefore, everyone using recommendation from your localhost server without a special namespace locally will be mixing with other users training their recommendation engine. We would love to hear your ideas around this topic!

- jQuery is a dependency of Alina front-end's implementation. When you deploy the Alina plugin into your web application, you can specifiy which "hotspots" (or user interactions) mean what kind of rating in the database. All of the data is stored in the Alinapi.com cloud, so there is no need to configure a database or write any back-end code. The benefit of this is not just ease-of-implementation, but the fact that everyone's training data can benefit everyone else's training data. If you are a book e-tailer, your users are training the Alina Cloud, and another book recommendation service can opt-in to get access to overall book data. 
This feature will be available soon. As currently, all training data is split between domain implimentation of the Alina Recommendation service. 

What you need to build your own Recommendation Engine with Alina
--------------------------------------

Clone a copy of the main Alina Recommendation git repo by running:

```bash
git clone git://github.com/codecloudme/alina-recommend-js.git
```

Enter the alina-recommend-js directory and open your index.html file:

Firstly, import the Alina Recommendation library after including jQuery.

```
<script src="js/alina-beta-0.1.js"></script>
```

Secondly, create your Alina instance after the page has loaded.
```
window.load(function(){
	var myAlina = new alina('recommendation');

})

```
Specify your settings for your alina instance.

```
	rec.recommend({
		
		productDetection:'selectors', //options are selectors or pre-suff (pre-suff example appears two lines below)
		productIds:'.productId', // where the product ID is stored

		//productDetection:'pre-suff', //this vs pre-suff
		//productIds:'product=...&', //vs products/.../.html

		callback:showThem,
		hotspots:{
			//you can specifiy product ID here if there are several products/items on the page you would like to attach to hotspots.
			"button":[{"action":"click", "rating":4, "productId":'455'},
					{"action":"hover", "rating":4}],
			".selector":[{"action":"click", "rating":4},
					{"action":"hover", "rating":5}]		
			

		}
	});
```

Create a hidden div where you will include the ID of your product on the page.
```
<div class="productId" style="display:none">377GHA9KLW1</div>
```

That's it. When a user visits a product page an automatic call is made added that view with a rating of 3. If the user clicks a hotspot, then whatever rating you associated with that hotspot is added for that user's session. 

In the example above, we have the example callback parameter in the settings of "showThem". This callback is executed with a single parameter containing the products that are recommended and their cooresponding recommendation level. The most highly recommended product based on similar users' interaction appears at the top. 

Example output passed to your callback will look as follows:
```
{'status':'sucess', data:{domainId:4, data:['productId', 4.3333], ['productId2', 3.555]}}
```


Questions?
----------

If you have any questions, please feel free to ask!
[m@alinapi.com](mailto:m@alinapi.com) or in #alinapi on irc.freenode.net or twitter.
