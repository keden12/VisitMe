# VisitMe
# Assignment 1 - Agile Software Practice.

Kamil Bigos

20075688

Software Systems Development

## Overview.

This API is made for a tourism web app which will store Listings of places that are in a specific area. These listings will be populated on the site depending on their variables such as category or featured.

## API endpoints.

app.get("/listings", listings.findListings) //Get All Listings

app.get("/listings/total", listings.findTotalListings) //Get the total number of listings
app.get("/listings/:category/total", listings.findTotalListingsByCategory) //Get the total number of listings in a specific category

app.get("/listings/:id", listings.findByID) //Get listing by ID
app.get("/listings/title/:title", listings.findByTitle) //Get listing by title
app.get("/listings/category/:category", listings.findByCategory) //Get all listings in category


app.put("/listings/:id/love", listings.incrementHeart) //Like a listing

app.put("/listings/:id/changetitle", listings.changeTitle) //Change the listing title
app.put("/listings/:id/changedesc", listings.changeDescription) //Change the listing description
app.put("/listings/:id/changefeatured", listings.changeFeatured) //Change the featured state of a listing

app.post("/listings",listings.addListing) //Add a new listing
app.post("/listings/search", listings.searchListings) //Fuzzy search that searches for listings

app.delete("/listings/:id", listings.deleteListingByID) //Delete the listing by ID
app.delete("/listings/title/:title", listings.deleteListingByTitle) //Delete the listing by title

## Data model.

Listing Model

    {
    title: String,
    description: String,
    category: String,
    website:  {type: String, default: null},
    mobile:  {type: String, default: null},
    location: String,
    featuredimage: String,
    gallery:[{
        type: String, default: null
    }],
    featured:{type: Boolean, default: false},
    facebook: {type: String, default: ""},
    instagram: {type: String, default: ""},
    twitter: {type: String, default: ""},
    hearts: {type: Number, default: 0},
    reviews:[{
        type: String, default: null
    }]
}

Sample Data

     {
          "website": "http://witsu.ie/locations/the-dome-bar/",
          "mobile": "0858558793",
          "gallery": [
               "./images/dome02.jpg",
               "./images/dome03.jpg"
          ],
          "featured": false,
          "facebook": "https://www.facebook.com/WITdomebar/",
          "instagram": "",
          "twitter": "",
          "hearts": 0,
          "reviews": [],
          "_id": "5dc06477ee07d62ee0e80a8a",
          "title": "The Dome",
          "description": "The Dome Bar is located in the WIT Main Campus. It is mainly used by students since it is a great place to socialise! Why not check it out yourself!",
          "category": "Pubs",
          "location": "WIT Main Campus, Waterford",
          "featuredimage": "./images/dome01.jpg",
          "__v": 0
     }



## Sample Test execution.
~~~
  Listings
    GET /listings/category/:category
Successfully Connected to [ admin ]
GET /listings/category/Nightclubs 200 46.105 ms - 1543
      √ should return all listings from that category (137ms)
    GET /listings/:category/total
GET /listings/Nightclubs/total 200 9.429 ms - 11
      √ should return the total number of listings in the category
    GET /listings/:id
GET /listings/5dc191d6f245e233b086be8b 200 12.139 ms - 804
      √ should return the matching listing
    GET /listings/title/:title
GET /listings/title/Project 200 8.470 ms - 804
      √ should return the matching listing
    GET /listings/total
GET /listings/total 200 12.776 ms - 11
      √ should return the total number of listings
    GET /listings
GET /listings 200 13.942 ms - 3426
      √ should GET all the listings
    PUT /listings/:id/changetitle
PUT /listings/5dc191d7f245e233b086be9b/changetitle 200 75.732 ms - 889
      √ should return a 200 and change the listing title (86ms)
GET /listings/5dc191d7f245e233b086be9b 200 8.218 ms - 809
    PUT /listings/:id/love
PUT /listings/5dc191d7f245e233b086be9f/love 200 13.633 ms - 888
      √ should return a 200 and hearts increment by 1
GET /listings/5dc191d7f245e233b086be9f 200 6.573 ms - 804
    PUT /listings/:id/changedesc
PUT /listings/5dc191d7f245e233b086bea3/changedesc 200 21.575 ms - 778
      √ should return a 200 and change the description
GET /listings/5dc191d7f245e233b086bea3 200 8.796 ms - 692
    PUT /listings/:id/changefeatured
PUT /listings/5dc191d7f245e233b086bea7/changefeatured 200 14.999 ms - 884
      √ should return a 200 and change the featured status to true
GET /listings/5dc191d7f245e233b086bea7 200 5.872 ms - 803
    POST /listings
POST /listings 200 7.753 ms - 869
      √ should return confirmation message and update datastore
GET /listings/title/Test 200 6.038 ms - 680
    POST /listings/search
POST /listings/search 200 19.890 ms - 520
      √ should work like a fuzzy search so should return listings without full title
    DELETE /listings/:id
      when id is valid
(node:13232) DeprecationWarning: Mongoose: `findOneAndUpdate()` and `findOneAndDelete()` without the `useFindAndModify` option set to false are deprecated. See: https://mongoosejs.com/docs/deprecations.html#-findandmodify-
DELETE /listings/$%7BprojectID%7D 200 17.269 ms - 43
        √ should return a confirmation message and delete the listing
GET /listings 200 12.884 ms - 3426
      when id is invalid
DELETE /listings/142013 200 4.218 ms - 34
        √ should return an error message
    DELETE /listings/title/:title
      when title is valid
(node:13232) DeprecationWarning: collection.remove is deprecated. Use deleteOne, deleteMany, or bulkWrite instead.
DELETE /listings/title/Project 200 7.976 ms - 43
        √ should return a confirmation message and delete the listing
GET /listings 200 11.065 ms - 2624


  15 passing (5s)

