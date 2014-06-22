---
layout: post
title: "Google Maps v3 Custom HTML Map Marker"
date: 2013-07-29 14:23
comments: true
categories: [JavaScript,Google Maps]
---
I'm currently building a small rails app that will display where all of the breweries located in Portland Oregon are. So far the most complicated thing about it is interfacing with the Google Maps v3 API. Many of the problems I face, Google has examples for in their documentation. However, some examples seem to be buried deep down in the recesses of the documentation and are a little bit harder to come by. 
<!-- more --> After two or so hours of searching for a way to make custom HTML map markers, I finally found an example in a forum. 

 Here is the basic code I found for creating a custom HTML map marker.
``` javascript
   function CustomMarker(latlng,  map) {
     this.latlng_ = latlng;

     // Once the LatLng and text are set, add the overlay to the map.  This will
     // trigger a call to panes_changed which should in turn call draw.
     this.setMap(map);
   }

   CustomMarker.prototype = new google.maps.OverlayView();

   CustomMarker.prototype.draw = function() {
     var me = this;

     // Check if the div has been created.
     var div = this.div_;
     if (!div) {
       // Create a overlay text DIV
       div = this.div_ = document.createElement('DIV');
       // Create the DIV representing our CustomMarker
       div.style.border = '2px solid blue';
       div.style.position = 'absolute';
       div.style.paddingLeft = '0px';
       div.style.cursor = 'pointer';
       div.style.width = '10px';
       div.style.height = '10px';

       google.maps.event.addDomListener(div, "click", function(event) {
         google.maps.event.trigger(me, "click");
       });

       // Then add the overlay to the DOM
       var panes = this.getPanes();
       panes.overlayImage.appendChild(div);
     }

     // Position the overlay 
     var point = this.getProjection().fromLatLngToDivPixel(this.latlng_);
     if (point) {
       div.style.left = point.x + 'px';
       div.style.top = point.y + 'px';
     }
   };

   CustomMarker.prototype.remove = function() {
     // Check if the overlay was on the map and needs to be removed.
     if (this.div_) {
       this.div_.parentNode.removeChild(this.div_);
       this.div_ = null;
     }
   };

   CustomMarker.prototype.getPosition = function() {
    return this.latlng_;
   };
```

After finding this it was rather easy to replace my normal map markers with the custom ones. I just changed my code from
``` javascript
  var marker = new google.maps.Marker({
    position: myLatlng,
    id: myid,
    map: map,
    title: name,
  });
```
to
``` javascript
  overlay = new CustomMarker(myLatlng, map, className);
```
Now, you'll notice I have a couple of extra parameters in my CustomMarker function call. Luckily with a couple of modifications it is very easy to pass parameters to your custom marker. 

All you have to do is add a couple of attributes to the main function, and they are accessible in the marker creation. Here is a basic example
``` javascript
function CustomMarker(latlng,  map, PARAM1, PARAM2) {
  this.latlng_ = latlng;
  this.CustomParam1 = PARAM1;
  this.CustomParam2 = PARAM2;
  this.setMap(map);
}
CustomMarker.prototype.draw = function() {
  var me = this;
  var div = this.div_;
  if (!div) {
    div = this.div_ = document.createElement('DIV');

    // Maybe Custom Param 1 is a class name
    div.className = this.CustomParam1;
    // And Param 2 is some content for the marker
    div.contentText = this.CustomParam2;

    div.style.border = '2px solid blue';
    div.style.position = 'absolute';
    div.style.paddingLeft = '0px';
    div.style.cursor = 'pointer';
    div.style.width = '10px';
    div.style.height = '10px';

    var panes = this.getPanes();
    panes.overlayImage.appendChild(div);
  }
  var point = this.getProjection().fromLatLngToDivPixel(this.latlng_);
  if (point) {
    div.style.left = point.x + 'px';
    div.style.top = point.y + 'px';
  }
};
```

I personally find that using custom HTML map markers in Google maps is much easier than using their map markers. It allows me to do things like CSS hover states and styling, as well as have better event listeners for buttons/links inside of the info windows.

Here is the [demo from Google](http://gmaps-samples-v3.googlecode.com/svn/trunk/overlayview/custommarker.html) I was linked to. 

Enjoy your custom map markers, and make something cool.
