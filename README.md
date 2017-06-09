# Ticketmaster workshop

Get an API key here: http://developer.ticketmaster.com/
Open Launchpad and log in! https://launchpad.graphql.com/new

## My favorite artists

* Kansas: K8vZ9171C-f
* Lil Yachty: K8vZ9174v57
* Jason Mraz: K8vZ9171CVV

## My desired query

```graphql
{
  myFavoriteArtists {
    id,
    name
    image
    twitterUrl
    events {
      name
      image
      startDateTime
    }
  }
}
```

Desired schema

```graphql
  type Query {
    myFavoriteArtists: [Artist]
  }

  type Artist {
    id: ID
    name: String
    image: String
    twitterUrl: String
    events: [Event]
  }

  type Event {
    name: String
    image: String
    startDateTime: String
  }
```

The answer key

Mocked: https://launchpad.graphql.com/z4lnp9j37
Mocked with list: https://launchpad.graphql.com/p380l5rx0
Fetch from API: https://launchpad.graphql.com/831vp05qq
Events: https://launchpad.graphql.com/9pw9nnkjr
UI: https://snack.expo.io/BJpiF0SfW

Endpoint fetching

URLs:

```js
// Look up artist details
https://app.ticketmaster.com/discovery/v2/attractions/${id}.json?apikey=${context.secrets.TM_API_KEY}

// Look up events for an artist
https://app.ticketmaster.com/discovery/v2/events.json?size=10&apikey=${context.secrets.TM_API_KEY}&attractionId=${id}
```

Code

```js
// Artist details
return fetch(`https://app.ticketmaster.com/discovery/v2/attractions/${id}.json?apikey=${context.secrets.TM_API_KEY}`)
  .then(res => res.json())

// Events
return fetch(`https://app.ticketmaster.com/discovery/v2/events.json?size=10&apikey=${context.secrets.TM_API_KEY}&attractionId=${id}`)
  .then(res => res.json())
```

Details docs: http://developer.ticketmaster.com/products-and-docs/apis/discovery-api/v2/#attraction-details-v2
