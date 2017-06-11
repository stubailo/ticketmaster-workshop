# Ticketmaster workshop

I recently flew down to LA and did a GraphQL workshop at Ticketmaster where everyone built a JavaScript GraphQL API together using [Launchpad](https://launchpad.graphql.com/), a tool that lets you experiment with GraphQL servers in your browser. Thankfully, the workshop was recorded, so you can try it too! The video references a Quip document I prepared, but all of that content is reproduced here in this README.

I hope to re-record a version of this more optimized for internet consumption soon, but who knows how long it will be before I have time, so I thought I'd put this up first. Go ahead and watch it!

[![Video screenshot](http://i.imgur.com/undefined.png)](https://www.youtube.com/watch?v=j0Ot84L5n04)

Here are some things you'll need to do right away:

- Get an API key here: http://developer.ticketmaster.com/
- Open Launchpad and log in! https://launchpad.graphql.com/new

### My favorite artists

And their Ticketmaster API attraction IDs:

* Kansas: `K8vZ9171C-f`
* Lil Yachty: `K8vZ9174v57`
* Jason Mraz: `K8vZ9171CVV`

### Desired query

This is the query we want to be able to fetch from our new GraphQL API:

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

### Desired schema

This is a schema that will fulfill the above query:

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

### The answer key

Click on these links to see the finished APIs in Launchpad:

- Mocked: https://launchpad.graphql.com/z4lnp9j37
- Mocked with list of artists: https://launchpad.graphql.com/p380l5rx0
- Fetch artist details from API: https://launchpad.graphql.com/831vp05qq
- Fetch upcoming events from API: https://launchpad.graphql.com/9pw9nnkjr
- UI with Expo Snack: https://snack.expo.io/BJpiF0SfW

### Endpoints

These are the REST endpoints in the Ticketmaster API we want to fetch from.

URLs

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

Details docs from the Ticketmaster API: http://developer.ticketmaster.com/products-and-docs/apis/discovery-api/v2/#attraction-details-v2

### Workshops

If you are interested in getting a GraphQL workshop like this at your company, don't hesitate to email me at `sashko@apollodata.com`!
