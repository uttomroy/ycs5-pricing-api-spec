This operation allows the user to setting up a price strategy based on length of stay.

## Use Cases
### Setting up a new length of stay price rule
![setting up](images/rendered/los-figure.svg)

Given you want a traveller to get a custom price on 1-4 if they stay more than 2 days

your request will look like this

```json
```

when you made a request, the api will store information in Agoda system, and you can retrived the current setup via

### Updating a lenght of stay rule

![setting up](images/rendered/los-figure.svg)
From the figure above, if you wanted to change your policy, you may made a request that look like this

```json
```

![update](images/rendered/los-update.svg)

when you made a request, any booking date that made in 4-6 will use rule B instead of A

### Overlapping rule

The last rule will take priority, please check the scenario below

![update with overlapped rule](images/rendered/los-update-overlapped.svg)