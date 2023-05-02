# Actor - Zoopla Scraper

## Zoopla scraper

Since Zoopla doesn't provide a good and free API, this actor should help you to retrieve data from it.

The Zoopla data scraper supports the following features:

-   Get anything, filter by your needs - Retrieving any result is as easy as clicking a button. Filter your needs, create filters, ranges or pick locations and immediately harvest properties which are for sale, for rent or already sold.

-   Scrape listings of agents - You can get properties directly from agents. Use agent's profile URL and get everything with ease.

-   Property data right away - Baths, amenities, tax history, price, beds, features and many other information are ready at your consumption. Get rental, for sale or sold properties blazingly fast!

## Bugs, fixes, updates and changelog

This scraper is under active development. If you have any feature requests you can create an issue from [here](https://github.com/epctex/zoopla-scraper/issues).

## Input Parameters

The input of this scraper should be JSON containing the list of pages on Zoopla that should be visited. Possible fields are:

- `startUrls`: (Required) (Array) URLs to start with. It should be agent, search, list or property detail URL.

- `endPage`: (Optional) (Number) Final number of page that you want to scrape. Default is `Infinite`. This is applies to all `search` request and `startUrls` individually.

- `maxItems`: (Optional) (Number) You can limit scraped items. This should be useful when you search through the big lists or search results.

- `proxy`: (Required) (Proxy Object) Proxy configuration.

- `extendOutputFunction`: (Optional) (String) Function that takes a JQuery handle ($) as argument and returns object with data.

- `customMapFunction`: (Optional) (String) Function that takes each objects handle as argument and returns object with executing the function.


This solution requires the use of **Proxy servers**, either your own proxy servers or you can use [Apify Proxy](https://www.apify.com/docs/proxy).

### Tip

When you want to have a scrape over a specific list URL, just copy and paste the link as one of the **startUrl**.

If you would like to scrape only the first page of a list then put the link for the page and have the `endPage` as 1.

With the last approach that explained above you can also fetch any interval of pages. If you provide the 5th page of a list and define the `endPage` parameter as 6 then you'll have the 5th and 6th pages only.

### Compute Unit Consumption

The actor optimized to run blazing fast and scrape as many items as possible. Therefore, it forefronts all the detail requests. If actor doesn't block very often it'll scrape 100 listings in 1 minute with ~0.06-0.75 compute units.

### Zoopla Scraper Input example

```json
{
  "startUrls":[
    "https://www.zoopla.co.uk/overseas/details/64410387/",
    "https://www.zoopla.co.uk/new-homes/details/64410305/",
    "https://www.zoopla.co.uk/to-rent/details/64411515/",
    "https://www.zoopla.co.uk/for-sale/details/62414617/",
    "https://www.zoopla.co.uk/for-sale/branch/chancellors-east-oxford-oxford-13801/",
    "https://www.zoopla.co.uk/to-rent/branch/residential-land-london-19482/",
    "https://www.zoopla.co.uk/for-sale/property/oxford/?q=oxford&results_sort=newest_listings&search_source=for-sale",
    "https://www.zoopla.co.uk/to-rent/property/oxford/",
    "https://www.zoopla.co.uk/new-homes/property/oxfordshire"
  ],
  "endPage":4,
  "maxItems":100,
  "proxy":{
    "useApifyProxy":true
  }
}
```

## During the Run

During the run, the actor will output messages letting you know what is going on. Each message always contains a short label specifying which page from the provided list is currently specified.
When items are loaded from the page, you should see a message about this event with a loaded item count and total item count for each page.

If you provide incorrect input to the actor, it will immediately stop with failure state and output an explanation of what is wrong.

## Zoopla Export

During the run, the actor stores results into a dataset. Each item is a separate item in the dataset.

You can manage the results in any languague (Python, PHP, Node JS/NPM). See the FAQ or <a href="https://www.apify.com/docs/api" target="blank">our API reference</a> to learn more about getting results from this Zoopla actor.

## Scraped Zoopla Properties

The structure of each property in Zoopla.co.uk looks like this:

### Property Detail

```json
{
	"url": "https://www.zoopla.co.uk/to-rent/details/42244429/",
	"uuid": "daaeeb87-5ade-44ae-8229-05069c491498",
	"propertyType": "flat",
	"publishedOn": "2023-03-31T04:34:52",
	"title": "2 bed flat to rent",
	"images": [
		"https://lid.zoocdn.com/u/2400/1800/d5512046adffd7816f82af30f5f6d243602bc6fd.jpg",
		"https://lid.zoocdn.com/u/2400/1800/8ed9c3c2eb584576d129a214c52a2124369e860b.jpg",
		"https://lid.zoocdn.com/u/2400/1800/17b0ed64963f7fb589df6669ebda44587e075497.jpg",
		"https://lid.zoocdn.com/u/2400/1800/7f73dec2dee4cc63f36095a7b382d761fb48c076.jpg",
		"https://lid.zoocdn.com/u/2400/1800/5bb32c4f99af5de61b91c6d3cab95ec71d412eca.jpg",
		"https://lid.zoocdn.com/u/2400/1800/06b4352ca431a7074246b3a85fc57c777b7af116.jpg",
		"https://lid.zoocdn.com/u/2400/1800/f17aeba815231722612584f0a91a99ecd334b5fb.jpg"
	],
	"poi": [],
	"latitude": 51.493675,
	"longitude": -0.239744,
	"postalCode": "W6 0SP",
	"id": "42244429",
	"features": [
		"2 Bedrooms",
		"2 Bathrooms",
		"Furnished",
		"785 square foot",
		"Parking",
		"Digital TV",
		"CCTV",
		"Shops",
		"Recycling Facilities"
	],
	"availableFrom": null,
	"isFurnished": "Furnished",
	"studentFriendly": false,
	"description": "A stunning two bedroom apartment situated in a Victorian red brick building in the Ravenscourt Park conservation area.<br><br>This second floor apartment comprises two double bedrooms with the master benefiting from an en-suite bathroom, modern second bathroom, and an open plan spacious kitchen/reception room allowing great space for entertaining.<br><br>The apartment has recently been renovated to the highest specification and is set over 633 sq. Ft. It benefits from wood flooring throughout, along with pre cabled Sky TV as well as Cat 4 cables for internet connections.<br><br>Residential Land is the owner and managing agent of this property. All of our tenants benefit from a dedicated on-site or building manager who is on hand to assist with any property related issues. We also employ a dedicated team of maintenance experts and provide a 24-hour emergency helpline.<br><br>Financial Summary:<br><br>• Holding Deposit= £800 (1 week’s rent- this is taken off the total security deposit)<br>• Security Deposit= £2,666.67 (1 calendar month’s rent, less holding deposit)<br>• 1 calendar months rent= £3,466.67<br><br>Total amount payable= £6,933.33<br><br>Council Tax band- E<br>EPC rating- C<br><br>* Spacious and bright<br><br>* Period features<br><br>* Key entry phone<br><br>* 24 hour maintenance service<br><br>* Dedicated building manager<br><br>* Available furnished or unfurnished",
	"address": "King Street, London W6",
	"leaseExpiry": null,
	"groundRent": null,
	"councilTaxBand": null,
	"administrationFees": "<strong>No admin fees</strong>",
	"deposit": null,
	"tags": [],
	"floorPlan": [
		"https://lc.zoocdn.com/85e3a5dbc5bbc39dc611bd3332ec9556e1f302af.jpg"
	],
	"livingRooms": 0,
	"beds": 2,
	"bedsMax": 2,
	"bedsMin": 2,
	"baths": null,
	"isRetirementHome": false,
	"isSharedOwnership": false,
	"listingCondition": "pre-owned",
	"listingStatus": "to_rent",
	"price": 3467,
	"priceActual": 3467,
	"priceMax": 3500,
	"priceMin": 3250,
	"sqft": "",
	"additionalLinks": [],
	"category": "residential",
	"agent": {
		"address": "59-60 Grosvenor Street, Mayfair, London",
		"name": "Residential Land",
		"phone": "020 3463 6976"
	}
}
```
