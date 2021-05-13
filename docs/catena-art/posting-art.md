# Posting Artwork

Catena has a REST API that allows you to post artwork from your user account.

You can make a POST to

```
catenaart.com/api/v1/asset/
```

The parameters it accepts in the Request Body are:

| Parameter                | Description                                   |
|--------------------------|-----------------------------------------------|
| Name                     | The name of the asset                         |
| Artist                   | The name of the artist                        |
| Price                    | The price of the asset in PAI                 |
| Asset Public Key Address | The public key of the asset                   |
| Description              | The description of the asset                  |
| Images                   | Images of the asset                           |
| Public                   | Whether or not the asset is publicly viewable |


## Accepted file type and sizes:

We currently only support PNG and JPG file types with a file size less than 50 MB.


