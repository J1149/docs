# Catena Art 

Catena Art can largely be seen as a light wrapper around PAI Pass. It wraps PAI Pass' OAuth2, PAI Messages, and Yggdrasil. Effectively, the only thing the backend of Catena stores itself is the user's profile data.  

## Users

### User Creation

User creation occurs after a user hits signup (or login), goes to PAI Pass and accepts the OAuth request. When the OAuth credentials are sent from PAI Pass to Catena Art, the user is created (or logged in).



## Assets 

### Process

So the user initiates 

 

### Catena/Yggdrasil Interface
As mentioned in the above, Catena is largely a wrapper around PAI Pass; that is, the assets portion of Catena is a wrapper around PAI Pass' [Yggdrasil](/paipass/yggdrasil/). The structure of the schema is as follows:

| Field              | Data Type | Description                                                                                                                                                       |
|--------------------|-----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Name               | TEXT      | The name of the asset.                                                                                                                                            |
| Asset Owner        | TEXT      | The owner of the asset.                                                                                                                                           |
| Asset Poster       | TEXT      | Effectively the same as the Asset Owner. There was this differentiation initially to distinguish between the owner and the person posting on behalf of the owner. |
| Artist             | TEXT      | The creator of the Asset                                                                                                                                          |
| Description        | TEXT      | A description of the asset                                                                                                                                        |
| Price              | TEXT      | The price of the asset                                                                                                                                            |
| Price Units        | TEXT      | The price in units of the asset. This existed initially in order to peg the asset price to a less volatile currency.                                              |
| Main Thumbnail     | IMAGE     | An image reduced in quality and size in order to make a consistent and quick browsing experience for the main page.                                               |
| Images             | LIST      | A structure to hold the images of the asset                                                                                                                       |
| Image              | IMAGE     | An image of the asset                                                                                                                                             |
| Timeline Events    | LIST      | A structure to hold the timeline events as the asset changes provenance or is updated.                                                                            |
| Timeline Event     | OBJECT    | A structure to hold details of the event                                                                                                                          |
| Event Name         | TEXT      | The name of the event                                                                                                                                             |
| Blockchain Address | TEXT      | The address to which this asset is pegged to when the event occurred.                                                                                             |
| Timestamp          | DATE      | The timestamp corresponding to the event.                                                                                                                         |


When an asset is submitted

## PAI Messages

Catena wraps around PAI Pass' PAI Messages. 


