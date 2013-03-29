# The TicketMaster API
## Contents
* [General Response Format](#general-response-format)
  * [Request](#request)
  * [Response](#response)
  	  * [Response JSON](#response-json)
      * [Response Fields](#response-fields)
* [Endpoints](#endpoints)
    * [Events Endpoint](#events-endpoint)
        * [Event Query Parameters](#event-query-parameters)
        * [Event Response](#event-response)
            * [Event JSON](#event-json)
            * [Event Fields](#event-fields)
            * [Event Notes](#event-notes)

## General Response Format
Here we will look at a general request to the TicketMaster API, and the response we get back.

## Request
Requests to TicketMaster are simply GET queries to a particular endpoint.

No special headers, cookies, or even a user agent are needed.

**Note:** TicketMaster appears to have recently started blocking the IPs of major data centers (AWS, Softlayer, etc.), so be aware that requests may simply fail from your IP.

## Response
The response from TicketMaster's API is a JSON object with the following structure.

### Response JSON
```php
{  
	"spellcheck": null,  
	"responseHeader": {  
		"status": 0,
		"QTime": 0
	},
	"response": {
		"facet_counts": { },
		"numFound": 100,
		"docs": [ 
			...
		],
		"start": 0
	},
	"fromJetson": 1
}
```

### Response Fields
* **unknown** `spellcheck`  Not sure, only seen `null`
* **object** `responseHeader` 
	* **int** `status` - `0` means "success", also seen `404` (obviously page not found)
	* **int** `QTime` - Probably the time to execute the query (I think `0` means cached)
* **object** `response` 
	* **obj** `facet_counts` - Not sure
	* **int** `numFound` - Number of docs in response
	* **array** `docs` - Response documents (events, etc)
	* **int** `start` - Probably the starting document for pagination, only seen `0`
* **int** `fromJetson` - Not sure, usually `1`  

## Endpoints
*Note: Certain endpoints appear to accept multiple IDs per parameter, but I have only ever seen  
endpoints accept a single query parameter (ex. you can't specify a venue AND artist to search)*

## Events Endpoint
`http://www.ticketmaster.com/json/search/event`  

### Event Query Parameters
* **vid** - Appending `?vid=<Venue ID>` returns events which are located at the given venue.
* **aid** - Appending `?aid=<Artist ID>` returns events which contain the given artist.  
*(Note: Events returned for an `aid` search could contain other artists as well - the search is not exclusive)*

### Event Response 
*Note: This structure describes an item (`doc`) in the `docs` array [above](#general-response-format).*  
*Other Note: I've reorganized the response in order to better group the returned fields.*

This event actually happens to make an excellent example of "typical" TicketMaster data. Pay attention 
to things like `null` `AttractionIds`, empty `AttractionNames` and `AttractionImages`, etc.

#### Event JSON
```php
{
    "Currency":"CAD",
    "LangCode":"en-us",
    "Id":"1100497D79FA5606",
    "DocumentId":"Event+1100497D79FA5606+en-us+1",
    "Type":[
       "Event"
    ],
    "EventId":"1100497D79FA5606",
    "EventName":"WINNIPEG FOLK FESTIVAL - RV PASS FOR FESTIVAL CAMPGROUND",
    "EventInfo":"Only one (1) RV pass need per vehicle.",
    "EventNotes":"Only one (1) RV pass need per vehicle.  Tickets will not be sent out until mid May.<br><br>No more RV passes available through Ticketmaster.  Limited number at the Folk Festival Music Store.<br><br>\n\nFor more information on the Winnipeg Folk Festival\n<A HREF=&#34;http://www.winnipegfolkfestival.ca&#34; target=&#34;_new&#34;> \n<b><i>Click Here</i></b></A><br><br>\nThere is no in store pickup available for this event - all tickets must be mailed, couriered or picked up at will call (at the venue day of show).\n",
    "EventType":0,
    "EventStatus":"2",
    "StarReviewCount":20,
    "Stars":4.6,
    "Timezone":"America/Chicago",
    "LocalEventDateDisplay":"Wed, 07/10/13<br>09:00 AM",
    "LocalEventMonthYear":"July 2013",
    "LocalEventWeekdayString":"Wednesday",
    "LocalEventShortWeekday":"Wed",
    "LocalEventShortMonth":"Jul",
    "LocalEventMonth":7,
    "LocalEventDay":10,
    "LocalEventYear":2013,
    "VenueId":"139409",
    "VenueName":"Winnipeg Folk Festival - Birds Hill Park",
    "VenueAddress":"Hwy #59",
    "VenueCity":"Winnipeg",
    "VenueState":"MB",
    "VenueCityState":"Winnipeg, MB",
    "VenuePostalCode":"R3J 3W3",
    "VenueCountry":"CA",
    "VenueLatLong":"49.898145000,-97.257242000",
    "VenueImage":"/dbimages/14034v.gif",
    "VenueSEOLink":"/Winnipeg-Folk-Festival-Birds-Hill-Park-tickets-Winnipeg/venue/139409",
    "timestamp":"2013-03-28T09:58:09.039Z",
    "EventRangeStart":"2013-07-10T05:00:00Z",
    "EventInternetRelease":"1997-03-26T06:00:00Z",
    "EventRangeEnd":"2013-07-14T05:00:00Z",
    "SearchableUntil":"2013-07-11T04:59:59Z",
    "OnsaleOn":"2012-12-01T16:00:00Z",
    "OnsaleOff":null,
    "EventDate":"2013-07-10T14:00:00Z",
    "ExpirationDate":null,
    "ActOverride":true,
    "SuppressBestAvailAll":true,
    "SingleEPDate":true,
    "Host":"VAN",
    "PurchaseDomain":"1",
    "MajorGenre":[
       "Music"
    ],
    "MajorGenreId":[
       10001
    ],
    "MinorGenre":[
       "Country and Folk"
    ],
    "MinorGenreId":[
       2
    ],
    "Genre":[
       "Country and Folk"
    ],
    "MusicBrowseGenre":[
       "All Music",
       "Country and Folk"
    ],
    "PresaleName":[
       "Early Bird Presale",
       "Early Bird Presale"
    ],
    "PresaleOff":[
       "2012-12-28T02:00:00Z",
       "2013-05-01T02:59:00Z"
    ],
    "PresaleOn":[
       "2012-12-01T17:00:00Z",
       "2013-03-16T16:00:00Z"
    ],
    "PromoterId":[
       "320"
    ],
    "MarketId":[
       106
    ],
    "DMAId":[
       530
    ],
    "AttractionId":[
       "874376",
       "1784064",
       null,
       "1548463",
       "1153444",
       "1577943",
       "1009255",
       "1638381",
       "753510",
       "907821",
       "898743",
       "735515",
       "1479990",
       "1012831",
       "1511324",
       "791766",
       "971857",
       "735326",
       "910513",
       "1411318",
       "960162",
       "1584613",
       "734084",
       "1594491",
       "991994",
       "781743",
       "1113003",
       "1618457",
       "1537986",
       "753213",
       "1109940",
       "1482259",
       "1499210",
       "1487711",
       "1309100",
       "1532840",
       "972411",
       "1746245",
       "1731816",
       "1108947",
       "1116121",
       "983767",
       "1682784",
       "732762",
       "732779",
       "735007",
       "733261",
       "1823433",
       "1832723",
       "1665132",
       "1501968",
       "1672789",
       "880598",
       "1627530",
       "882091",
       "1668736"
    ],
    "AttractionName":[
       "Winnipeg Folk Festival",
       "A Tribe Called Red",
       "",
       "Aidan Knight",
       "Bhi Bhiman",
       "Bombino",
       "City and Colour",
       "Cold Specks",
       "Dan Bern",
       "Danny Michel",
       "David Francey",
       "David Lindley",
       "Del Barber",
       "Dr. Dog",
       "Frank Fairfield",
       "Galactic",
       "Hayes Carll",
       "Indigo Girls",
       "Jason Collett",
       "Josh Ritter and the Royal City Band",
       "Kaki King",
       "Lake Street Dive",
       "Leon Redbone",
       "Lindi Ortega",
       "Locos Por Juana",
       "Martin Sexton",
       "Matt the Electrician",
       "Nathan Rogers",
       "Oh My Darling",
       "Over the Rhine",
       "Patrick Watson",
       "Rich Aucoin",
       "Robert Ellis",
       "Rose Cousins",
       "Sara Watkins",
       "Sean Rowe",
       "Serena Ryder",
       "Shelley Bean and the Duckety Muds",
       "Alan Kelly Gang",
       "The Avett Brothers",
       "The Blind Boys of Alabama",
       "The Cat Empire",
       "The Dunwells",
       "The Flatlanders",
       "Jimmie Dale Gilmore",
       "Joe Ely",
       "Butch Hancock",
       "The Harpoonist and the Axe Murderer",
       "The Howlin&#39; Brothers",
       "The Milk Carton Kids",
       "The Okee Dokee Brothers",
       "Tinpan Orange",
       "Tony Furtado",
       "Whitehorse",
       "Xavier Rudd",
       "WINNIPEG FOLK FESTIVAL - RV PASS FOR FESTIVAL CAMPGROUND"
    ],
    "AttractionImage":[
       "/dbimages/77294a",
       "",
       "",
       "",
       "",
       "/dbimages/119575a.jpg",
       "/dbimages/137651a.jpg",
       "",
       "/dbimages/37481a.jpg",
       "/dbimages/32729a.jpg",
       "",
       "/dbimages/38870a.jpg",
       "/dbimages/131116a.jpg",
       "/dbimages/121686a.jpg",
       "",
       "/dbimages/96685a.jpg",
       "/dbimages/76695a.jpg",
       "/dbimages/105173a.jpg",
       "",
       "/dbimages/129954a.jpg",
       "/dbimages/121407a.jpg",
       "",
       "/dbimages/30343a.jpg",
       "",
       "",
       "/dbimages/103554a.jpg",
       "",
       "",
       "",
       "/dbimages/OvertheRhine_753213_EMI_3Z.jpg",
       "/dbimages/103877a.jpg",
       "/dbimages/101372a.jpg",
       "",
       "",
       "",
       "",
       "/dbimages/127292a.jpg",
       "",
       "",
       "/dbimages/122594a.jpg",
       "/dbimages/83887a.jpg",
       "/dbimages/96861a.jpg",
       "/dbimages/109794a.jpg",
       "/dbimages/32200a.jpg",
       "/dbimages/38535a.jpg",
       "/dbimages/13579a.jpg",
       "",
       "",
       "",
       "/dbimages/134774a.jpg",
       "",
       "",
       "",
       "/dbimages/97343a.jpg",
       "/dbimages/134435a.jpg"
    ],
    "PostProcessedData":{
       "LocalEventRangeStart":"2013-07-10T00:00:00-05:00",
       "LocalEventDate":"2013-07-10T09:00:00-05:00",
       "MEV":3,
       "SuppressWireless":true,
       "onsale_status":"1",
       "Onsales":{
          "unmodified_epdate":null,
          "expire":"Tue, 04/30/13<br>09:59 PM",
          "onsales":[
             {
                "suppress":0,
                "onsale_type":"1",
                "interval":{
                   "end":"Sun, 07/14/13<br>12:00 AM",
                   "start":"Sat, 12/01/12<br>10:00 AM"
                }
             },
             {
                "suppress":0,
                "onsale_type":"2",
                "interval":{
                   "end":"Tue, 04/30/13<br>09:59 PM",
                   "start":"Sat, 03/16/13<br>11:00 AM"
                }
             }
          ],
          "event_date":{
             "event_date_type":6,
             "date":"Wed, 07/10/13<br>09:00 AM",
             "date_range":{
                "end":"Sun, 07/14/13<br>12:00 AM",
                "start":"Wed, 07/10/13<br>12:00 AM"
             },
             "suppress_time":0
          }
       }
    },
    "AttractionSEOLink":[
       "/Winnipeg-Folk-Festival-tickets/artist/874376",
       "/A-Tribe-Called-Red-tickets/artist/1784064",
       "",
       "/Aidan-Knight-tickets/artist/1548463",
       "/Bhi-Bhiman-tickets/artist/1153444",
       "/Bombino-tickets/artist/1577943",
       "/City-and-Colour-tickets/artist/1009255",
       "/Cold-Specks-tickets/artist/1638381",
       "/Dan-Bern-tickets/artist/753510",
       "/Danny-Michel-tickets/artist/907821",
       "/David-Francey-tickets/artist/898743",
       "/David-Lindley-tickets/artist/735515",
       "/Del-Barber-tickets/artist/1479990",
       "/Dr-Dog-tickets/artist/1012831",
       "/Frank-Fairfield-tickets/artist/1511324",
       "/Galactic-tickets/artist/791766",
       "/Hayes-Carll-tickets/artist/971857",
       "/Indigo-Girls-tickets/artist/735326",
       "/Jason-Collett-tickets/artist/910513",
       "/Josh-Ritter-and-the-Royal-City-Band-tickets/artist/1411318",
       "/Kaki-King-tickets/artist/960162",
       "/Lake-Street-Dive-tickets/artist/1584613",
       "/Leon-Redbone-tickets/artist/734084",
       "/Lindi-Ortega-tickets/artist/1594491",
       "/Locos-Por-Juana-tickets/artist/991994",
       "/Martin-Sexton-tickets/artist/781743",
       "/Matt-the-Electrician-tickets/artist/1113003",
       "/Nathan-Rogers-tickets/artist/1618457",
       "/Oh-My-Darling-tickets/artist/1537986",
       "/Over-the-Rhine-tickets/artist/753213",
       "/Patrick-Watson-tickets/artist/1109940",
       "/Rich-Aucoin-tickets/artist/1482259",
       "/Robert-Ellis-tickets/artist/1499210",
       "/Rose-Cousins-tickets/artist/1487711",
       "/Sara-Watkins-tickets/artist/1309100",
       "/Sean-Rowe-tickets/artist/1532840",
       "/Serena-Ryder-tickets/artist/972411",
       "/Shelley-Bean-and-the-Duckety-Muds-tickets/artist/1746245",
       "/Alan-Kelly-Gang-tickets/artist/1731816",
       "/The-Avett-Brothers-tickets/artist/1108947",
       "/The-Blind-Boys-of-Alabama-tickets/artist/1116121",
       "/The-Cat-Empire-tickets/artist/983767",
       "/The-Dunwells-tickets/artist/1682784",
       "/The-Flatlanders-tickets/artist/732762",
       "/Jimmie-Dale-Gilmore-tickets/artist/732779",
       "/Joe-Ely-tickets/artist/735007",
       "/Butch-Hancock-tickets/artist/733261",
       "/The-Harpoonist-and-the-Axe-Murderer-tickets/artist/1823433",
       "/The-Howlin-Brothers-tickets/artist/1832723",
       "/The-Milk-Carton-Kids-tickets/artist/1665132",
       "/The-Okee-Dokee-Brothers-tickets/artist/1501968",
       "/Tinpan-Orange-tickets/artist/1672789",
       "/Tony-Furtado-tickets/artist/880598",
       "/Whitehorse-tickets/artist/1627530",

       "/Xavier-Rudd-tickets/artist/882091"
    ],
    "search-en":"WINNIPEG FOLK FESTIVAL - RV PASS FOR FESTIVAL CAMPGROUND Winnipeg MB  Manitoba Winnipeg Folk Festival A Tribe Called Red Aidan Knight Bhi Bhiman Bombino City and Colour Cold Specks Dan Bern Danny Michel David Francey David Lindley Del Barber Dr. Dog Frank Fairfield Galactic Hayes Carll Indigo Girls Jason Collett Josh Ritter and the Royal City Band Kaki King Lake Street Dive Leon Redbone Lindi Ortega Locos Por Juana Martin Sexton Matt the Electrician Nathan Rogers Oh My Darling Over the Rhine Patrick Watson Rich Aucoin Robert Ellis Rose Cousins Sara Watkins Sean Rowe Serena Ryder Shelley Bean and the Duckety Muds Alan Kelly Gang The Avett Brothers The Blind Boys of Alabama The Cat Empire The Dunwells The Flatlanders Jimmie Dale Gilmore Joe Ely Butch Hancock The Harpoonist and the Axe Murderer The Howlin&#39; Brothers The Milk Carton Kids The Okee Dokee Brothers Tinpan Orange Tony Furtado Whitehorse Xavier Rudd Winnipeg Folk Festival - Birds Hill Park July 2013 Wednesday R3J 3W3 Country and Folk winnipegfolkfestival-rvpassforfestivalcampground winnipegfolkfestival atribecalledred aidanknight bhibhiman cityandcolour coldspecks danbern dannymichel davidfrancey davidlindley delbarber dr.dog frankfairfield hayescarll indigogirls jasoncollett joshritterandtheroyalcityband kakiking lakestreetdive leonredbone lindiortega locosporjuana martinsexton matttheelectrician nathanrogers ohmydarling overtherhine patrickwatson richaucoin robertellis rosecousins sarawatkins seanrowe serenaryder shelleybeanandtheducketymuds alankellygang theavettbrothers theblindboysofalabama thecatempire thedunwells theflatlanders jimmiedalegilmore joeely butchhancock theharpoonistandtheaxemurderer thehowlin&#39;brothers themilkcartonkids theokeedokeebrothers tinpanorange tonyfurtado xavierrudd"
}
```

#### Event Fields
* `Currency` 
* `LangCode`
* `Id`
* `DocumentId`
* `Type`
* `Event<...>` - A collection of fields describing the event
    * `EventId`
    * `EventName`
    * `EventInfo`
    * `EventNotes`
    * `EventType`
    * `EventStatus`
* `StarReviewCount`
* `Stars`
* `Timezone`
* `LocalEvent<...>` - A collection of fields describing the date of the event
    * `LocalEventDateDisplay`
    * `LocalEventMonthYear`
    * `LocalEventWeekdayString`
    * `LocalEventShortWeekday`
    * `LocalEventShortMonth`
    * `LocalEventMonth`
    * `LocalEventDay`
    * `LocalEventYear`
* `Venue<...>` - A collection of fields describing the venue
    * `VenueId`
    * `VenueName`
    * `VenueAddress`
    * `VenueCity`
    * `VenueState`
    * `VenueCityState`
* ``

#### Event Notes
* Quite a few fields seem extraneous and unnecessary (`LocalEventWeekdayString`, `LocalEventShortWeekday`, `LocalEventDay`, etc.), but are probably included so that some display
logic somewhere can just use the data directly.
* TicketMaster has started being very kind lately by providing `VenueLatLong` for us! No need to (sometimes unreliably) geocode venue addresses any more.
* Nearly any field can be `null`/empty/missing - there is very little consistency in TicketMaster's
data - so plan your code accordingly