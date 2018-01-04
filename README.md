# Nexxchange TeeTime Widget
TeeTime widget to book within the Nexxchange Marketplace <https://www.nexxchange.com>

## Overview
The example HTML code <https://github.com/xtradesoft/nexxchange-teetime-widget/blob/master/example/index.html> shows exactly how to implement the **Nexxchange** tee time widget. 

It is only a simple copy and paste.

`Pull Requests` are welcome.

### Widget parameters

* **issuer**

	This is to define for which `golfclub` the tee times should be displayed.

* **showBookingButton**

	(default: true) Optional, allows to en/disable the booking button
	
* **onlyShowAvailable**

	(default: false) Optional, allows to show only available tee time
	
* **course**

    Optional, integer value, server only sends tee times for the selected golf course.
	
* **i18n**

	Optional, defines the used translation in the widget.

	* booking: "Buchen"
	* available: "verfügbar"
	* noGreenfees: 'Greenfees konnten nicht geladen werden!'


The widget has one public function "reload" which accepts the following parameters

* **date** 	(dd.mm.yyyy)
* **hour**
* **minutes**

### Styling
Size, color, etc. can be adjusted individually using standard CSS

### Examples

<img src="https://github.com/xtradesoft/nexxchange-teetime-widget/blob/master/example/img/Example-Image-using-widget.png?raw=true" alt="Website Screenshot" width="800">

<img src="https://github.com/xtradesoft/nexxchange-teetime-widget/blob/master/example/img/Example-Image-using-widget-2.png?raw=true" alt="Website Screenshot" width="800">

### Live Implementations

[GC Drautal] (http://www.drautalgolf.at/index.php/article?id=37)

[GC Velden] (http://www.golfvelden.at/en/book-tee-time.html)

[AlpeAdria Golf Tarvisio] (http://www.teetimealpeadriagolf.com/de/golfplatz-buchen/tarvis.html)

[Golf & Seen] (http://attersee.salzkammergut.at/sommer/golfen.html)

### License

Apache




