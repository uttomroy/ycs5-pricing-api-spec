This operation allows the user to setting up a price strategy based on length of stay.

## Use Cases
### Setting up a new length of stay price rule
![setting up](images/rendered/los-figure.svg)

Given you want a traveller to get a custom price on 1-4 if they stay more than 2 days

your request will look like this

```json
{
  "propertyId": 5,
  "currency": "USD",
  "offers": [
    {
      "roomId": 5,
      "ratePlanId": 5,
      "rates": [
        {
          "checkIn": {
            "start": "2022-01-01",
            "end": "2022-01-04"
          },
          "occupancyPrices": [
            {
              "occupancy": {
                "min": 1,
                "max": 1
              },
              "prices": [
                {
                  "los": 1,
                  "value": 6200.00
                },
                {
                  "los": 2,
                  "value": 6000.00
                },
                {
                  "los": 3,
                  "value": 5500.00
                },
                {
                  "los": 4,
                  "value": 5000.00
                }
              ]
            }
          ]
      }
      ]
    }
  ]
}
```

when you made a request, the api will store information in Agoda system, and you can retrived the current setup via https://supply.agoda.com/api/price/fplos/search
you will get the price setup like this

### Updating a lenght of stay rule

![setting up](images/rendered/los-figure.svg)
From the figure above, if you wanted to change your policy, you may made a request that look like this

```json
{
  "propertyId": 5,
  "currency": "USD",
  "offers": [
    {
      "roomId": 5,
      "ratePlanId": 5,
      "rates": [
        {
          "checkIn": {
            "start": "2022-01-05",
            "end": "2022-01-07"
          },
          "occupancyPrices": [
            {
              "occupancy": {
                "min": 1,
                "max": 1
              },
              "prices": [
                {
                  "los": 1,
                  "value": 10200.00
                },
                {
                  "los": 2,
                  "value": 10000.00
                },
                {
                  "los": 3,
                  "value": 9000.00
                }
              ]
            }
          ]
      }
      ]
    }
  ]
}
```

![update](images/rendered/los-update.svg)

when you made a request, any booking date that made in 4-6 will use rule B instead of A ( for instance,. if traveller book for a property with 1 date lenght of stay, they will get a rate of USD 10200.00 )

### Overlapping rule

The last rule will take priority, please check the scenario below

![update with overlapped rule](images/rendered/los-update-overlapped.svg)

```json
{
  "propertyId": 5,
  "currency": "USD",
  "offers": [
    {
      "roomId": 5,
      "ratePlanId": 5,
      "rates": [
        {
          "checkIn": {
            "start": "2022-01-04",
            "end": "2022-01-07"
          },
          "occupancyPrices": [
            {
              "occupancy": {
                "min": 1,
                "max": 1
              },
              "prices": [
                {
                  "los": 1,
                  "value": 10200.00
                },
                {
                  "los": 2,
                  "value": 10000.00
                },
                {
                  "los": 3,
                  "value": 9000.00
                }
              ]
            }
          ]
      }
      ]
    }
  ]
}
```

then the booking that happened after 4 January 2022 to 6 January 2022 will use 10200, 10000, 9000 as a rate depends on length of stay, instead of 6200, 6000, 5500, 5000