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
	* noGreenfees: 'Keine Startzeiten für den ausgewählten Zeitraum verfügbar.'

* **render**

  A custom render function. Uses returned server data to render tee times into any DOM element.
  
  While this method gives the highest degree of flexibility is also exposes internal data representations that might change in the future.
  The return data currently uses the following schema:
  
  ```
  {
    issuerId?:string
    golfCourse: {
      courseName:string
      teeTimes:TeeTime[]  // array of tee times
    }
  }
  ```

  `TeeTime` currently uses the following schema:

  ```
  {
    courseName:string
    teeTimes:TeeTimeSlot[] // array of tee time slots
  }
  ```  

  `TeeTimeSlot` currently uses the following schema:

  ```
  {
    tt:number
    ttTime:string
    ttDate:DateTime
    countAvail:number facet:Seq[TeeTimeSlotFacet]
  }
  ```

  Finally `TeeTimeSlotFacet` currently uses this schema:
  
  ```
  {
    facetName:String
    facetId:Long
    price?: { amount: number, currency: { code:string, symbol:string  } }
  }
  ```

* **date** 	(dd.mm.yyyy)
* **hour**
* **minutes**

### Helpers

The widget has one public function "reload" which accepts the following parameters

The widget also provides the ```createBookingButtonLink(issuerId:string,teeTimeSlot:TeeTimeSlot,facet:Facet)``` methoed to render the booking button link.

### Styling
Size, color, etc. can be adjusted individually using standard CSS

### Examples

<img src="https://github.com/xtradesoft/nexxchange-teetime-widget/blob/master/example/img/Example-Image-using-widget.png?raw=true" alt="Website Screenshot" width="800">

<img src="https://github.com/xtradesoft/nexxchange-teetime-widget/blob/master/example/img/Example-Image-using-widget-2.png?raw=true" alt="Website Screenshot" width="800">

### Selection of Live Implementations

[Golf & Seen] (http://www.golfundseen.at/startseite.html)

[Tourismusverband Attersee - Salzkammergut] (http://attersee.salzkammergut.at/sommer/golfen.html)

[AlpeAdria Golf Tarvisio] (http://www.teetimealpeadriagolf.com/de/golfplatz-buchen/tarvis.html)

[GC Salzburg] (https://www.golfclub-salzburg.at/courses/tee-online/)

[GC Velden] (http://www.golfvelden.at/en/book-tee-time.html)

[GC Drautal] (http://www.drautalgolf.at/index.php/article?id=37)

### License

Apache




