# Backend Coding Challenge

## Requirements

Design an API endpoint that provides auto-complete suggestions for large cities in the US and Canada. _See data folder for a CSV file containing cities. The original data comes from Geonames. See link below in references._ 

- The endpoint is exposed at `/suggestions`
- The partial (or complete) search term is passed as a querystring parameter `q`
- The endpoint returns a JSON response with an array of scored suggested matches
    - The suggestions are sorted by descending score
    - Each suggestion has a score between 0 and 1 (inclusive) indicating confidence in the suggestion (1 is most confident)
    - Each suggestion has a name which can be used to disambiguate between similarly named locations
    - Each suggestion has a latitude and longitude
- Create Database Model(s)
- Generate script to seed initial data (cities in the US and Canada):
    - Read CSV file using csvtojson or fast-csv module
    - Import CSV data to MongoDB Database using mongodb module
- Use Node.js
- Use MongoBD

## Bonus Requirements

- The caller's location can optionally be supplied via querystring parameters `latitude` and `longitude` to help improve relative scores

## The Rules / Advice

- **Try to design and implement your solution as you would do for real production code**. Show us how you create clean, maintainable code.
- You should demonstrate your coding style and approach to problem solving.
- _Don't worry if you don't finish everything in that time, as long as it effectively demonstrates your approach and style._ Stub out functionality and use comments to describe the changes/improvements you were intending to make.
- Try to include at least one test to demonstrate the tools you use, and how your approach to writing tests.
- Stub out or describe what other tests you would include with more time.
- Use infrastructure products (eg: databases) to solve the problem.
- Documentation and maintainability is a plus. If short on time, describe how you would document the service/API in a README.md. How would you make the documentation available? What tools would you use?
- Publish your solution to Github or another source control system you can share with us.

## Sample responses

These responses are meant to provide guidance. The exact values can vary based on the data source and scoring algorithm

**Near match**

    GET /suggestions?q=Londo&latitude=43.70011&longitude=-79.4163

```json
{
  "suggestions": [
    {
      "name": "London, ON, Canada",
      "latitude": "42.98339",
      "longitude": "-81.23304",
      "score": 0.9
    },
    {
      "name": "London, OH, USA",
      "latitude": "39.88645",
      "longitude": "-83.44825",
      "score": 0.5
    },
    {
      "name": "London, KY, USA",
      "latitude": "37.12898",
      "longitude": "-84.08326",
      "score": 0.5
    },
    {
      "name": "Londontowne, MD, USA",
      "latitude": "38.93345",
      "longitude": "-76.54941",
      "score": 0.3
    }
  ]
}
```

**No match**

    GET /suggestions?q=SomeRandomCityInTheMiddleOfNowhere

```json
{
  "suggestions": []
}
```

## References

- Geonames provides city lists Canada and the USA http://download.geonames.org/export/dump/readme.txt
