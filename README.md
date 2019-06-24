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

<img src="https://github.com/xtradesoft/nexxchange-teetime-widget/blob/master/example/img/Example-Image-using-widget-3.png?raw=true" alt="Website Screenshot" width="800">

### Selection of Live Implementations

[Golf & Seen] (http://www.golfundseen.at/startseite.html)

[Tourismusverband Attersee - Salzkammergut] (http://attersee.salzkammergut.at/sommer/golfen.html)

[AlpeAdria Golf Tarvisio] (http://www.teetimealpeadriagolf.com/de/golfplatz-buchen/tarvis.html)

[GC Salzburg] (https://www.golfclub-salzburg.at/courses/tee-online/)

[GC Velden] (http://www.golfvelden.at/en/book-tee-time.html)

[GC Drautal] (http://www.drautalgolf.at/index.php/article?id=37)

[Mehr Grün] (https://www.mehr-gruen.at/buchung/)

# Tournament Widget

The tournament widget allows integration of a tournament table on external website.

* Minimal configuration: Include javascript and invoke `renderTournamentWidget` to load the tournament widget into a DOM element.
* Self contained: CSS is non-intrusively (namespaced) injected by the tournament widget. Note that most of the injected CSS is need by [react-datepicker](https://github.com/Hacker0x01/react-datepicker).
* Responsive by default: Uses some basic (namespaced) [Bootstrap 4](https://getbootstrap.com/) CSS styles to properly flow on mobile devices.
* No iframes required.
* Configurable: See [widget parameter section](#widget-parameter-section).

## Integration

Load the tournament widget Javascript from https://portal.nexxchange.com to import the `renderTournamentWidget` function into the global namespace. 
Invoke `renderTournamentWidget` for a given DOM element ID and pass the desired `issuerId` in the [parameter section](#widget-parameter-section).

```
<div id="tournament-widget-container"></div>
...
<script src="https://portal.nexxchange.com/assets/widgets/js/tournament-widget.js"></script>
<script>
  renderTournamentWidget(
    "tournament-widget-container",   // First argument sets the ID of the target DOM element  
    {  // Second argument is used for configuration parameters
      issuerId : "<issuerId>"  // set correct issuer ID for your golf club here
    }
  );
</script>
```

## Widget Parameter Section

| Name         | Type        | Description           |
| -------------|-------------|-----------------------|
| issuerId     | string      | The ID of the golfclub (see [How to find the issuer ID?](#how-to-find-the-issuer-id?)) |
| fromDate     | Date        | Lower bound for tounament date, the upper bound is fixed to `fromDate` + 1 year |
| lang         | string      | Language used to render tournament widget: `en`, `da`, `de`, `es`, `fr`, `it`, `no`, `sv`. Date picker will show names of month and weekdays in the selected language.
| spinner      | string      | `donat` or `donat multi` or `ripple` |
| hideFromDatePicker | boolean | If set to `true` the date picker will be hidden, you can use the [Widget API](#widget-api) to update the from date programatically. |
| maxResults   | integer     | maximum number of displayed tournaments, maxResults is capped to 10 entries. |
| i18nDictionary | Map<string,string> | Overwrite translation keys for selected language, see the [I18n](#i18n) section. |

## Widget API

Methods can be called on the widget instance returned by `renderTournamentWidget`.

### Update From Date (`setFromDate`)

Example:
```
<div id="tournament-widget-container"></div>
...
<script src="https://portal.nexxchange.com/assets/widgets/js/tournament-widget.js"></script>
<script>
  var widget = renderTournamentWidget(
    "tournament-widget-container",
    { issuerId : "<issuerId>" }
  );
  const date = new Date(2019, 1, 1)
  widget.setFromDate(date);
</script>
```

A change in the `fromDate` will automatically trigger a reload.

### I18n

The `i18n` property can be used to override the default translations provided by the widget or to define translations for unsupported languages.
The following translation keys are available: 

`registrationDeadline`,`remainingTickets`,`availableTickets`,`registerButtonLabel`,`round`

### Custom Styling

Most of the elements in the widget have proper class names assigned to them to allow customization of the CSS styles.
E.g. by default the tournament date is left aligned while the name/type of the tournament is right aligned.
To move the date to the right side and the title to the left side you can use the following custom CSS:
```
.tournament-date {
  float: right !important;
}
.tournament-name {
  float: left !important;
}
.tournament-type {
  float: left !important;
}
```

### Debugging

In case of load errors (reload icon is shown) please check the browser console for more details.

## Tournament Widget FAQ

### How to find the correct issuer ID?

1. Go to https://www.nexxchange.com
2. Select an golf club/issuer using the search field
3. Inspect the page source and look for the meta tag with the `name` attribute set to `issuerId`. The `content` attribute of this meta tag contains the issuer ID. 

Example:
```
...
<meta name="issuerId" content="112233445566778899001122">`
...
```
### Can I use my own date picker instead of the one that ships with the widget?

Yes, you can use the `setFromDate` method described in the [Widget API](#widget-api) section to control the from date used by the widget.
Also use the `hideFromDatePicker` property to hide the built-in date picker.

### What happens in case the widget cannot load the tournament data for some reason?

The spinner will be replaced by a reload icon. Clicking on the icon will trigger a reload request.

### License

Apache




