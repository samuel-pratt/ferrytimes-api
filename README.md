## FerryTimes API - [ferrytimes.ca](https://ferrytimes.ca)

The only public API for retrieving current data on BC Ferries sailings.

## How It's Made

FerryTimes is a flask api connected to a python web scraper. The scraper is made with BeautifulSoup4 and Pandas. It runs every 3 minutes and saves the relevant, formatted data to a json 'database' made with flata. When flask recieves a request, it checks the validity of the request, then returns the specified data.

The frontend is made with HTML, Bootstrap, and Javascript. When the user hits the request button, it runs a small script that calls the api with the user's request, and displays the info on the page.

<b>Built with</b>

- [Flask](https://github.com/pallets/flask)
- [BeautifulSoup4](https://github.com/wention/BeautifulSoup4)
- [Pandas](https://github.com/pandas-dev/pandashttps://github.com/pandas-dev/pandas)
- [Bootstrap](https://github.com/twbs/bootstrap)
- [Flata](https://github.com/harryho/flata)

## API Reference

The api runs on the format:

`https://www.ferrytimes.ca/api/<departure-terminal>/<destination-terminal>`

You can be as specific as needed, the fewer arguments there are, the more data you will recieve.

For example, `https://www.ferrytimes.ca/api/tsawwassen` will return all data for all sailings leaving from Tsawwassen.

If the response is empty and shows no errors, it just means there may not be any more sailings for that terminal, this usually happens later at night.

Options for each are as follows:

#### departure-terminal

```
"tsawwassen"
"swartz-bay"
"nanaimo-(duke-pt)"
"nanaimo-(dep.bay)"
"horseshoe-bay"
"langdale"
"snug-cove-(bowen-is.)"
```

#### destination-terminal

Note: destination terminal must correspond with departure terminal, for example you can't put tsawwassen to langdale, it will return an error.

```
"tsawwassen": [
    "swartz-bay"
    "southern-gulf-islands"
    "duke-point"
]
"swartz-bay": [
    "tsawwassen"
    "fulford-harbour"
]
"nanaimo-(duke-pt)": [
    "tsawwassen"
]
"nanaimo-(dep.bay)": [
    "horseshoe-bay"
]
"horseshoe-bay": [
    "departure-bay"
    "langdale"
    "snug-cove-(bowen-is.)"
]
"langdale": [
    "horseshoe-bay"
]
"snug-cove-(bowen-is.)": [
    "horseshoe-bay"
]
```

#### Errors

If any of the parameters are not from the above, you will see one of the following errors:

```
"Error: Not a valid departure terminal."
"Error: Not a valid destination terminal."
```

If you see an error not included in this list, there may be an issue with the API, please [submit an issue](https://github.com/samuel-pratt/ferry-times-api/issues/new)
