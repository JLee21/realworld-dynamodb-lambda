```
DELETE /__TESTUTILS__/purge
```
```
200 OK

"Purged all data!"
```
# Article
```
POST /users

{
  "user": {
    "email": "author-19lce6@email.com",
    "username": "author-19lce6",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "author-19lce6@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvci0xOWxjZTYiLCJpYXQiOjE1NDQ5ODcxMjEsImV4cCI6MTU0NTE1OTkyMX0.GFzIi4xiVx3eq6mHwMgPzc-uegn39r3JViIbTUk2gBA",
    "username": "author-19lce6",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "authoress-wyc6is@email.com",
    "username": "authoress-wyc6is",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "authoress-wyc6is@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvcmVzcy13eWM2aXMiLCJpYXQiOjE1NDQ5ODcxMjEsImV4cCI6MTU0NTE1OTkyMX0.lcsR_soiAT6PM3oV-1SDzs9gu_BlL8II7cZsrV1z7Uc",
    "username": "authoress-wyc6is",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "non-author-omblz5@email.com",
    "username": "non-author-omblz5",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "non-author-omblz5@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6Im5vbi1hdXRob3Itb21ibHo1IiwiaWF0IjoxNTQ0OTg3MTIxLCJleHAiOjE1NDUxNTk5MjF9.2XXxBMmljlJSXhK7Nftj_MHDD8wrFIGoDrg_E8YqufY",
    "username": "non-author-omblz5",
    "bio": "",
    "image": ""
  }
}
```
## Create
### should create article
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body"
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-7mue75",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1544987121533,
    "updatedAt": 1544987121533,
    "author": {
      "username": "author-19lce6",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should create article with tags
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "tag_a",
      "tag_b"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-mrl9vu",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1544987121581,
    "updatedAt": 1544987121581,
    "author": {
      "username": "author-19lce6",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should disallow unauthenticated user
```
POST /articles

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should enforce required fields
```
POST /articles

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "title must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "description must be specified."
    ]
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "body must be specified."
    ]
  }
}
```
## Get
### should get article by slug
```
GET /articles/title-7mue75
```
```
200 OK

{
  "article": {
    "createdAt": 1544987121533,
    "author": {
      "username": "author-19lce6",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-7mue75",
    "updatedAt": 1544987121533,
    "tagList": [],
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should get article with tags by slug
```
GET /articles/title-mrl9vu
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1544987121581,
    "author": {
      "username": "author-19lce6",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-mrl9vu",
    "updatedAt": 1544987121581,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should disallow unknown slug
```
GET /articles/xh1kmp
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [xh1kmp]"
    ]
  }
}
```
## Update
### should update article
```
PUT /articles/title-mrl9vu

{
  "article": {
    "title": "newtitle"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1544987121581,
    "author": {
      "username": "author-19lce6",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "newtitle",
    "body": "body",
    "slug": "title-mrl9vu",
    "updatedAt": 1544987121581,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
```
PUT /articles/title-mrl9vu

{
  "article": {
    "description": "newdescription"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1544987121581,
    "author": {
      "username": "author-19lce6",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "newdescription",
    "title": "newtitle",
    "body": "body",
    "slug": "title-mrl9vu",
    "updatedAt": 1544987121581,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
```
PUT /articles/title-mrl9vu

{
  "article": {
    "body": "newbody"
  }
}
```
```
200 OK

{
  "article": {
    "tagList": [
      "tag_a",
      "tag_b"
    ],
    "createdAt": 1544987121581,
    "author": {
      "username": "author-19lce6",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "newdescription",
    "title": "newtitle",
    "body": "newbody",
    "slug": "title-mrl9vu",
    "updatedAt": 1544987121581,
    "favoritesCount": 0,
    "favorited": false
  }
}
```
### should disallow missing mutation
```
PUT /articles/title-mrl9vu

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article mutation must be specified."
    ]
  }
}
```
### should disallow empty mutation
```
PUT /articles/title-mrl9vu

{
  "article": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "At least one field must be specified: [title, description, article]."
    ]
  }
}
```
### should disallow unauthenticated update
```
PUT /articles/title-mrl9vu

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow updating non-existent article
```
PUT /articles/foo-title-mrl9vu

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foo-title-mrl9vu]"
    ]
  }
}
```
### should disallow non-author from updating
```
PUT /articles/title-mrl9vu

{
  "article": {
    "title": "newtitle"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article can only be updated by author: [author-19lce6]"
    ]
  }
}
```
## Favorite
### should favorite article
```
POST /articles/title-7mue75/favorite

{}
```
```
200 OK

{
  "article": {
    "createdAt": 1544987121533,
    "author": {
      "username": "author-19lce6",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "slug": "title-7mue75",
    "updatedAt": 1544987121533,
    "favoritedBy": [
      "non-author-omblz5"
    ],
    "favoritesCount": 1,
    "tagList": [],
    "favorited": true
  }
}
```
```
GET /articles/title-7mue75
```
```
200 OK

{
  "article": {
    "createdAt": 1544987121533,
    "author": {
      "username": "author-19lce6",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "favoritesCount": 1,
    "slug": "title-7mue75",
    "updatedAt": 1544987121533,
    "tagList": [],
    "favorited": true
  }
}
```
### should disallow favoriting by unauthenticated user
```
POST /articles/title-7mue75/favorite

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow favoriting unknown article
```
POST /articles/title-7mue75_foo/favorite

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [title-7mue75_foo]"
    ]
  }
}
```
### should unfavorite article
```
DELETE /articles/title-7mue75/favorite
```
```
200 OK

{
  "article": {
    "createdAt": 1544987121533,
    "author": {
      "username": "author-19lce6",
      "bio": "",
      "image": "",
      "following": false
    },
    "description": "description",
    "title": "title",
    "body": "body",
    "favoritesCount": 0,
    "slug": "title-7mue75",
    "updatedAt": 1544987121533,
    "tagList": [],
    "favorited": false
  }
}
```
## Delete
### should delete article
```
DELETE /articles/title-7mue75
```
```
200 OK

{}
```
```
GET /articles/title-7mue75
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [title-7mue75]"
    ]
  }
}
```
### should disallow deleting by unauthenticated user
```
DELETE /articles/foo
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow deleting unknown article
```
DELETE /articles/foobar
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foobar]"
    ]
  }
}
```
### should disallow deleting article by non-author
```
DELETE /articles/title-mrl9vu
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article can only be deleted by author: [author-19lce6]"
    ]
  }
}
```
## List
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "n9p9zh",
      "tag_0",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-fo6kau",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1544987122597,
    "updatedAt": 1544987122597,
    "author": {
      "username": "authoress-wyc6is",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "n9p9zh",
      "tag_0",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "9rgbo",
      "tag_1",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-y9f3u",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1544987122622,
    "updatedAt": 1544987122622,
    "author": {
      "username": "author-19lce6",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "9rgbo",
      "tag_1",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "4m2x7p",
      "tag_2",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-7eigyq",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1544987122643,
    "updatedAt": 1544987122643,
    "author": {
      "username": "authoress-wyc6is",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "4m2x7p",
      "tag_2",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "dyzuso",
      "tag_3",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-4mypiq",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1544987122673,
    "updatedAt": 1544987122673,
    "author": {
      "username": "author-19lce6",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "dyzuso",
      "tag_3",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "v2afyu",
      "tag_4",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-epzz97",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1544987122697,
    "updatedAt": 1544987122697,
    "author": {
      "username": "authoress-wyc6is",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "v2afyu",
      "tag_4",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "4qbhw4",
      "tag_5",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-yj1hi4",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1544987122725,
    "updatedAt": 1544987122725,
    "author": {
      "username": "author-19lce6",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "4qbhw4",
      "tag_5",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "f4rqiv",
      "tag_6",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-fsb8zu",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1544987122753,
    "updatedAt": 1544987122753,
    "author": {
      "username": "authoress-wyc6is",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "f4rqiv",
      "tag_6",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "5yxky4",
      "tag_7",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-qnog5x",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1544987122774,
    "updatedAt": 1544987122774,
    "author": {
      "username": "author-19lce6",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "5yxky4",
      "tag_7",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "wolf3v",
      "tag_8",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-g79ico",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1544987122800,
    "updatedAt": 1544987122800,
    "author": {
      "username": "authoress-wyc6is",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "wolf3v",
      "tag_8",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "kxmkka",
      "tag_9",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-lfz17y",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1544987122824,
    "updatedAt": 1544987122824,
    "author": {
      "username": "author-19lce6",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "kxmkka",
      "tag_9",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "3fmyuw",
      "tag_10",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-bfh3ps",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1544987122850,
    "updatedAt": 1544987122850,
    "author": {
      "username": "authoress-wyc6is",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "3fmyuw",
      "tag_10",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "f6am5y",
      "tag_11",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-ws2bir",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1544987122880,
    "updatedAt": 1544987122880,
    "author": {
      "username": "author-19lce6",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "f6am5y",
      "tag_11",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "dbbzun",
      "tag_12",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-ra6rcy",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1544987122907,
    "updatedAt": 1544987122907,
    "author": {
      "username": "authoress-wyc6is",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "dbbzun",
      "tag_12",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "c6881k",
      "tag_13",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-islu31",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1544987122934,
    "updatedAt": 1544987122934,
    "author": {
      "username": "author-19lce6",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "c6881k",
      "tag_13",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "uuingk",
      "tag_14",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-dr8utj",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1544987122956,
    "updatedAt": 1544987122956,
    "author": {
      "username": "authoress-wyc6is",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "uuingk",
      "tag_14",
      "tag_mod_2_0",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "r66l3c",
      "tag_15",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-8uvdr7",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1544987122980,
    "updatedAt": 1544987122980,
    "author": {
      "username": "author-19lce6",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "r66l3c",
      "tag_15",
      "tag_mod_2_1",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "gvz2kk",
      "tag_16",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-va2bhc",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1544987123002,
    "updatedAt": 1544987123002,
    "author": {
      "username": "authoress-wyc6is",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "gvz2kk",
      "tag_16",
      "tag_mod_2_0",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "79zv2f",
      "tag_17",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-mn1rsc",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1544987123039,
    "updatedAt": 1544987123039,
    "author": {
      "username": "author-19lce6",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "79zv2f",
      "tag_17",
      "tag_mod_2_1",
      "tag_mod_3_2"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "t9ot9t",
      "tag_18",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-xk6yap",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1544987123066,
    "updatedAt": 1544987123066,
    "author": {
      "username": "authoress-wyc6is",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "t9ot9t",
      "tag_18",
      "tag_mod_2_0",
      "tag_mod_3_0"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body",
    "tagList": [
      "pizpiv",
      "tag_19",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ]
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-c847zl",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1544987123110,
    "updatedAt": 1544987123110,
    "author": {
      "username": "author-19lce6",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [
      "pizpiv",
      "tag_19",
      "tag_mod_2_1",
      "tag_mod_3_1"
    ],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
### should list articles
```
GET /articles
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "pizpiv",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1544987123110,
      "author": {
        "username": "author-19lce6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-c847zl",
      "updatedAt": 1544987123110,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "t9ot9t",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1544987123066,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-xk6yap",
      "updatedAt": 1544987123066,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "79zv2f",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1544987123039,
      "author": {
        "username": "author-19lce6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mn1rsc",
      "updatedAt": 1544987123039,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "gvz2kk",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1544987123002,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-va2bhc",
      "updatedAt": 1544987123002,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "r66l3c",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1544987122980,
      "author": {
        "username": "author-19lce6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-8uvdr7",
      "updatedAt": 1544987122980,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "uuingk"
      ],
      "createdAt": 1544987122956,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-dr8utj",
      "updatedAt": 1544987122956,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "c6881k",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1544987122934,
      "author": {
        "username": "author-19lce6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-islu31",
      "updatedAt": 1544987122934,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dbbzun",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1544987122907,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ra6rcy",
      "updatedAt": 1544987122907,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "f6am5y",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1544987122880,
      "author": {
        "username": "author-19lce6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ws2bir",
      "updatedAt": 1544987122880,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "3fmyuw",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1544987122850,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-bfh3ps",
      "updatedAt": 1544987122850,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "kxmkka",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1544987122824,
      "author": {
        "username": "author-19lce6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-lfz17y",
      "updatedAt": 1544987122824,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "wolf3v"
      ],
      "createdAt": 1544987122800,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-g79ico",
      "updatedAt": 1544987122800,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "5yxky4",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1544987122774,
      "author": {
        "username": "author-19lce6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-qnog5x",
      "updatedAt": 1544987122774,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "f4rqiv",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1544987122753,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fsb8zu",
      "updatedAt": 1544987122753,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4qbhw4",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1544987122725,
      "author": {
        "username": "author-19lce6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-yj1hi4",
      "updatedAt": 1544987122725,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "v2afyu"
      ],
      "createdAt": 1544987122697,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-epzz97",
      "updatedAt": 1544987122697,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dyzuso",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1544987122673,
      "author": {
        "username": "author-19lce6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-4mypiq",
      "updatedAt": 1544987122673,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4m2x7p",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1544987122643,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7eigyq",
      "updatedAt": 1544987122643,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "9rgbo",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1544987122622,
      "author": {
        "username": "author-19lce6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-y9f3u",
      "updatedAt": 1544987122622,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "n9p9zh",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1544987122597,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fo6kau",
      "updatedAt": 1544987122597,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles with tag
```
GET /articles?tag=tag_7
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "5yxky4",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1544987122774,
      "author": {
        "username": "author-19lce6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-qnog5x",
      "updatedAt": 1544987122774,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
GET /articles?tag=tag_mod_3_2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "79zv2f",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1544987123039,
      "author": {
        "username": "author-19lce6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mn1rsc",
      "updatedAt": 1544987123039,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "uuingk"
      ],
      "createdAt": 1544987122956,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-dr8utj",
      "updatedAt": 1544987122956,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "f6am5y",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1544987122880,
      "author": {
        "username": "author-19lce6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ws2bir",
      "updatedAt": 1544987122880,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "wolf3v"
      ],
      "createdAt": 1544987122800,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-g79ico",
      "updatedAt": 1544987122800,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4qbhw4",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1544987122725,
      "author": {
        "username": "author-19lce6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-yj1hi4",
      "updatedAt": 1544987122725,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4m2x7p",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1544987122643,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7eigyq",
      "updatedAt": 1544987122643,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles by author
```
GET /articles?author=authoress-wyc6is
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "t9ot9t",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1544987123066,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-xk6yap",
      "updatedAt": 1544987123066,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "gvz2kk",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1544987123002,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-va2bhc",
      "updatedAt": 1544987123002,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "uuingk"
      ],
      "createdAt": 1544987122956,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-dr8utj",
      "updatedAt": 1544987122956,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dbbzun",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1544987122907,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ra6rcy",
      "updatedAt": 1544987122907,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "3fmyuw",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1544987122850,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-bfh3ps",
      "updatedAt": 1544987122850,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "wolf3v"
      ],
      "createdAt": 1544987122800,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-g79ico",
      "updatedAt": 1544987122800,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "f4rqiv",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1544987122753,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fsb8zu",
      "updatedAt": 1544987122753,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "v2afyu"
      ],
      "createdAt": 1544987122697,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-epzz97",
      "updatedAt": 1544987122697,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4m2x7p",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1544987122643,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7eigyq",
      "updatedAt": 1544987122643,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "n9p9zh",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1544987122597,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fo6kau",
      "updatedAt": 1544987122597,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles favorited by user
```
GET /articles?favorited=non-author-omblz5
```
```
200 OK

{
  "articles": []
}
```
### should list articles by limit/offset
```
GET /articles?author=author-19lce6&limit=2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "pizpiv",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1544987123110,
      "author": {
        "username": "author-19lce6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-c847zl",
      "updatedAt": 1544987123110,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "79zv2f",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1544987123039,
      "author": {
        "username": "author-19lce6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mn1rsc",
      "updatedAt": 1544987123039,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
GET /articles?author=author-19lce6&limit=2&offset=2
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "r66l3c",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1544987122980,
      "author": {
        "username": "author-19lce6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-8uvdr7",
      "updatedAt": 1544987122980,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "c6881k",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1544987122934,
      "author": {
        "username": "author-19lce6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-islu31",
      "updatedAt": 1544987122934,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should list articles when authenticated
```
GET /articles
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "pizpiv",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1544987123110,
      "author": {
        "username": "author-19lce6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-c847zl",
      "updatedAt": 1544987123110,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "t9ot9t",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1544987123066,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-xk6yap",
      "updatedAt": 1544987123066,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "79zv2f",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1544987123039,
      "author": {
        "username": "author-19lce6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mn1rsc",
      "updatedAt": 1544987123039,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "gvz2kk",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1544987123002,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-va2bhc",
      "updatedAt": 1544987123002,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "r66l3c",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1544987122980,
      "author": {
        "username": "author-19lce6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-8uvdr7",
      "updatedAt": 1544987122980,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "uuingk"
      ],
      "createdAt": 1544987122956,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-dr8utj",
      "updatedAt": 1544987122956,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "c6881k",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1544987122934,
      "author": {
        "username": "author-19lce6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-islu31",
      "updatedAt": 1544987122934,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dbbzun",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1544987122907,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ra6rcy",
      "updatedAt": 1544987122907,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "f6am5y",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1544987122880,
      "author": {
        "username": "author-19lce6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ws2bir",
      "updatedAt": 1544987122880,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "3fmyuw",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1544987122850,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-bfh3ps",
      "updatedAt": 1544987122850,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "kxmkka",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1544987122824,
      "author": {
        "username": "author-19lce6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-lfz17y",
      "updatedAt": 1544987122824,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "wolf3v"
      ],
      "createdAt": 1544987122800,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-g79ico",
      "updatedAt": 1544987122800,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "5yxky4",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1544987122774,
      "author": {
        "username": "author-19lce6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-qnog5x",
      "updatedAt": 1544987122774,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "f4rqiv",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1544987122753,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fsb8zu",
      "updatedAt": 1544987122753,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4qbhw4",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1544987122725,
      "author": {
        "username": "author-19lce6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-yj1hi4",
      "updatedAt": 1544987122725,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "v2afyu"
      ],
      "createdAt": 1544987122697,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-epzz97",
      "updatedAt": 1544987122697,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dyzuso",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1544987122673,
      "author": {
        "username": "author-19lce6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-4mypiq",
      "updatedAt": 1544987122673,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4m2x7p",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1544987122643,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7eigyq",
      "updatedAt": 1544987122643,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "9rgbo",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1544987122622,
      "author": {
        "username": "author-19lce6",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-y9f3u",
      "updatedAt": 1544987122622,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "n9p9zh",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1544987122597,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": false
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fo6kau",
      "updatedAt": 1544987122597,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should disallow multiple of author/tag/favorited
```
GET /articles?tag=foo&author=bar
```
```
GET /articles?author=foo&favorited=bar
```
```
GET /articles?favorited=foo&tag=bar
```
## Feed
### should get feed
```
GET /articles/feed
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only one of these can be specified: [tag, author, favorited]"
    ]
  }
}
```
```
200 OK

{
  "articles": []
}
```
```
POST /profiles/authoress-wyc6is/follow

{}
```
```
200 OK

{
  "profile": {
    "username": "authoress-wyc6is",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /articles/feed
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "t9ot9t",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1544987123066,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-xk6yap",
      "updatedAt": 1544987123066,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "gvz2kk",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1544987123002,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-va2bhc",
      "updatedAt": 1544987123002,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "uuingk"
      ],
      "createdAt": 1544987122956,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-dr8utj",
      "updatedAt": 1544987122956,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dbbzun",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1544987122907,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ra6rcy",
      "updatedAt": 1544987122907,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "3fmyuw",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1544987122850,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-bfh3ps",
      "updatedAt": 1544987122850,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "wolf3v"
      ],
      "createdAt": 1544987122800,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-g79ico",
      "updatedAt": 1544987122800,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "f4rqiv",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1544987122753,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fsb8zu",
      "updatedAt": 1544987122753,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "v2afyu"
      ],
      "createdAt": 1544987122697,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-epzz97",
      "updatedAt": 1544987122697,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4m2x7p",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1544987122643,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7eigyq",
      "updatedAt": 1544987122643,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "n9p9zh",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1544987122597,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fo6kau",
      "updatedAt": 1544987122597,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
```
POST /profiles/author-19lce6/follow

{}
```
```
200 OK

{
  "profile": {
    "username": "author-19lce6",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /articles/feed
```
```
200 OK

{
  "articles": [
    {
      "tagList": [
        "pizpiv",
        "tag_19",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1544987123110,
      "author": {
        "username": "author-19lce6",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-c847zl",
      "updatedAt": 1544987123110,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "t9ot9t",
        "tag_18",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1544987123066,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-xk6yap",
      "updatedAt": 1544987123066,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "79zv2f",
        "tag_17",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1544987123039,
      "author": {
        "username": "author-19lce6",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-mn1rsc",
      "updatedAt": 1544987123039,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "gvz2kk",
        "tag_16",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1544987123002,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-va2bhc",
      "updatedAt": 1544987123002,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "r66l3c",
        "tag_15",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1544987122980,
      "author": {
        "username": "author-19lce6",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-8uvdr7",
      "updatedAt": 1544987122980,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_14",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "uuingk"
      ],
      "createdAt": 1544987122956,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-dr8utj",
      "updatedAt": 1544987122956,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "c6881k",
        "tag_13",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1544987122934,
      "author": {
        "username": "author-19lce6",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-islu31",
      "updatedAt": 1544987122934,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dbbzun",
        "tag_12",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1544987122907,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ra6rcy",
      "updatedAt": 1544987122907,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "f6am5y",
        "tag_11",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1544987122880,
      "author": {
        "username": "author-19lce6",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-ws2bir",
      "updatedAt": 1544987122880,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "3fmyuw",
        "tag_10",
        "tag_mod_2_0",
        "tag_mod_3_1"
      ],
      "createdAt": 1544987122850,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-bfh3ps",
      "updatedAt": 1544987122850,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "kxmkka",
        "tag_9",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1544987122824,
      "author": {
        "username": "author-19lce6",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-lfz17y",
      "updatedAt": 1544987122824,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_8",
        "tag_mod_2_0",
        "tag_mod_3_2",
        "wolf3v"
      ],
      "createdAt": 1544987122800,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-g79ico",
      "updatedAt": 1544987122800,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "5yxky4",
        "tag_7",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1544987122774,
      "author": {
        "username": "author-19lce6",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-qnog5x",
      "updatedAt": 1544987122774,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "f4rqiv",
        "tag_6",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1544987122753,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fsb8zu",
      "updatedAt": 1544987122753,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4qbhw4",
        "tag_5",
        "tag_mod_2_1",
        "tag_mod_3_2"
      ],
      "createdAt": 1544987122725,
      "author": {
        "username": "author-19lce6",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-yj1hi4",
      "updatedAt": 1544987122725,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "tag_4",
        "tag_mod_2_0",
        "tag_mod_3_1",
        "v2afyu"
      ],
      "createdAt": 1544987122697,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-epzz97",
      "updatedAt": 1544987122697,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "dyzuso",
        "tag_3",
        "tag_mod_2_1",
        "tag_mod_3_0"
      ],
      "createdAt": 1544987122673,
      "author": {
        "username": "author-19lce6",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-4mypiq",
      "updatedAt": 1544987122673,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "4m2x7p",
        "tag_2",
        "tag_mod_2_0",
        "tag_mod_3_2"
      ],
      "createdAt": 1544987122643,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-7eigyq",
      "updatedAt": 1544987122643,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "9rgbo",
        "tag_1",
        "tag_mod_2_1",
        "tag_mod_3_1"
      ],
      "createdAt": 1544987122622,
      "author": {
        "username": "author-19lce6",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-y9f3u",
      "updatedAt": 1544987122622,
      "favoritesCount": 0,
      "favorited": false
    },
    {
      "tagList": [
        "n9p9zh",
        "tag_0",
        "tag_mod_2_0",
        "tag_mod_3_0"
      ],
      "createdAt": 1544987122597,
      "author": {
        "username": "authoress-wyc6is",
        "bio": "",
        "image": "",
        "following": true
      },
      "description": "description",
      "title": "title",
      "body": "body",
      "slug": "title-fo6kau",
      "updatedAt": 1544987122597,
      "favoritesCount": 0,
      "favorited": false
    }
  ]
}
```
### should disallow unauthenticated feed
```
GET /articles/feed
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
## Tags
### should get tags
```
GET /tags
```
```
200 OK

{
  "tags": [
    "tag_14",
    "tag_mod_2_0",
    "tag_mod_3_2",
    "uuingk",
    "4m2x7p",
    "tag_2",
    "kxmkka",
    "tag_9",
    "tag_mod_2_1",
    "tag_mod_3_0",
    "dyzuso",
    "tag_3",
    "t9ot9t",
    "tag_18",
    "5yxky4",
    "tag_7",
    "tag_mod_3_1",
    "4qbhw4",
    "tag_5",
    "f6am5y",
    "tag_11",
    "r66l3c",
    "tag_15",
    "f4rqiv",
    "tag_6",
    "3fmyuw",
    "tag_10",
    "gvz2kk",
    "tag_16",
    "9rgbo",
    "tag_1",
    "tag_a",
    "tag_b",
    "pizpiv",
    "tag_19",
    "dbbzun",
    "tag_12",
    "tag_4",
    "v2afyu",
    "n9p9zh",
    "tag_0",
    "tag_8",
    "wolf3v",
    "79zv2f",
    "tag_17",
    "c6881k",
    "tag_13"
  ]
}
```
# Comment
```
POST /users

{
  "user": {
    "email": "author-rynwhv@email.com",
    "username": "author-rynwhv",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "author-rynwhv@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImF1dGhvci1yeW53aHYiLCJpYXQiOjE1NDQ5ODcxMjQsImV4cCI6MTU0NTE1OTkyNH0.8xDeAZx6nQLHvEMpk2dOWIR1fekL9UsIlKfLJpkZ5A0",
    "username": "author-rynwhv",
    "bio": "",
    "image": ""
  }
}
```
```
POST /users

{
  "user": {
    "email": "commenter-lkwem3@email.com",
    "username": "commenter-lkwem3",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "commenter-lkwem3@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImNvbW1lbnRlci1sa3dlbTMiLCJpYXQiOjE1NDQ5ODcxMjQsImV4cCI6MTU0NTE1OTkyNH0.wgduWKJVuDymWc2gR-LgLX2N4HAevIRhWG-U5R_-50w",
    "username": "commenter-lkwem3",
    "bio": "",
    "image": ""
  }
}
```
```
POST /articles

{
  "article": {
    "title": "title",
    "description": "description",
    "body": "body"
  }
}
```
```
200 OK

{
  "article": {
    "slug": "title-bfq1ec",
    "title": "title",
    "description": "description",
    "body": "body",
    "createdAt": 1544987124363,
    "updatedAt": 1544987124363,
    "author": {
      "username": "author-rynwhv",
      "bio": "",
      "image": "",
      "following": false
    },
    "tagList": [],
    "favorited": false,
    "favoritesCount": 0
  }
}
```
## Create
### should create comment
```
POST /articles/title-bfq1ec/comments

{
  "comment": {
    "body": "test comment 7u397s"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "bf4573d0-0093-46cd-b348-d0fcd34e7997",
    "slug": "title-bfq1ec",
    "body": "test comment 7u397s",
    "createdAt": 1544987124400,
    "updatedAt": 1544987124400,
    "author": {
      "username": "commenter-lkwem3",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-bfq1ec/comments

{
  "comment": {
    "body": "test comment 333mw8"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "ce102c7d-9416-4869-991c-aef02f5f7610",
    "slug": "title-bfq1ec",
    "body": "test comment 333mw8",
    "createdAt": 1544987124428,
    "updatedAt": 1544987124428,
    "author": {
      "username": "commenter-lkwem3",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-bfq1ec/comments

{
  "comment": {
    "body": "test comment ikzbiw"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "06feec8f-c231-460f-809b-0dfefd2de978",
    "slug": "title-bfq1ec",
    "body": "test comment ikzbiw",
    "createdAt": 1544987124456,
    "updatedAt": 1544987124456,
    "author": {
      "username": "commenter-lkwem3",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-bfq1ec/comments

{
  "comment": {
    "body": "test comment 8okh5k"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "9e14ecbc-96dd-479b-ad64-79382aa2d9a2",
    "slug": "title-bfq1ec",
    "body": "test comment 8okh5k",
    "createdAt": 1544987124504,
    "updatedAt": 1544987124504,
    "author": {
      "username": "commenter-lkwem3",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-bfq1ec/comments

{
  "comment": {
    "body": "test comment ydvcvw"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "2771f061-3e9a-48da-99be-40fff3890113",
    "slug": "title-bfq1ec",
    "body": "test comment ydvcvw",
    "createdAt": 1544987124549,
    "updatedAt": 1544987124549,
    "author": {
      "username": "commenter-lkwem3",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-bfq1ec/comments

{
  "comment": {
    "body": "test comment kb9ekn"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "a7acccf4-fcbb-4712-b3c3-005f93ad8936",
    "slug": "title-bfq1ec",
    "body": "test comment kb9ekn",
    "createdAt": 1544987124580,
    "updatedAt": 1544987124580,
    "author": {
      "username": "commenter-lkwem3",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-bfq1ec/comments

{
  "comment": {
    "body": "test comment gkdgl5"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "03f40388-2a1e-4d04-8936-f0cd43d8f32b",
    "slug": "title-bfq1ec",
    "body": "test comment gkdgl5",
    "createdAt": 1544987124608,
    "updatedAt": 1544987124608,
    "author": {
      "username": "commenter-lkwem3",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-bfq1ec/comments

{
  "comment": {
    "body": "test comment gghf5r"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "6e27ff00-f289-4cde-86a6-f1fa7e8d3547",
    "slug": "title-bfq1ec",
    "body": "test comment gghf5r",
    "createdAt": 1544987124645,
    "updatedAt": 1544987124645,
    "author": {
      "username": "commenter-lkwem3",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-bfq1ec/comments

{
  "comment": {
    "body": "test comment g83n30"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "1fe1b435-0adb-48d9-ade2-5e7393f0c374",
    "slug": "title-bfq1ec",
    "body": "test comment g83n30",
    "createdAt": 1544987124674,
    "updatedAt": 1544987124674,
    "author": {
      "username": "commenter-lkwem3",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
```
POST /articles/title-bfq1ec/comments

{
  "comment": {
    "body": "test comment isgv40"
  }
}
```
```
200 OK

{
  "comment": {
    "id": "ca3b3bb4-5b4f-4647-9b4c-61cd021b6cd0",
    "slug": "title-bfq1ec",
    "body": "test comment isgv40",
    "createdAt": 1544987124701,
    "updatedAt": 1544987124701,
    "author": {
      "username": "commenter-lkwem3",
      "bio": "",
      "image": "",
      "following": false
    }
  }
}
```
### should disallow unauthenticated user
```
POST /articles/title-bfq1ec/comments

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should enforce comment body
```
POST /articles/title-bfq1ec/comments

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Comment must be specified."
    ]
  }
}
```
### should disallow non-existent article
```
POST /articles/foobar/comments

{
  "comment": {
    "body": "test comment lvucwo"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Article not found: [foobar]"
    ]
  }
}
```
## Get
### should get all comments for article
```
GET /articles/title-bfq1ec/comments
```
```
200 OK

{
  "comments": [
    {
      "createdAt": 1544987124608,
      "id": "03f40388-2a1e-4d04-8936-f0cd43d8f32b",
      "body": "test comment gkdgl5",
      "slug": "title-bfq1ec",
      "author": {
        "username": "commenter-lkwem3",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1544987124608
    },
    {
      "createdAt": 1544987124456,
      "id": "06feec8f-c231-460f-809b-0dfefd2de978",
      "body": "test comment ikzbiw",
      "slug": "title-bfq1ec",
      "author": {
        "username": "commenter-lkwem3",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1544987124456
    },
    {
      "createdAt": 1544987124504,
      "id": "9e14ecbc-96dd-479b-ad64-79382aa2d9a2",
      "body": "test comment 8okh5k",
      "slug": "title-bfq1ec",
      "author": {
        "username": "commenter-lkwem3",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1544987124504
    },
    {
      "createdAt": 1544987124674,
      "id": "1fe1b435-0adb-48d9-ade2-5e7393f0c374",
      "body": "test comment g83n30",
      "slug": "title-bfq1ec",
      "author": {
        "username": "commenter-lkwem3",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1544987124674
    },
    {
      "createdAt": 1544987124549,
      "id": "2771f061-3e9a-48da-99be-40fff3890113",
      "body": "test comment ydvcvw",
      "slug": "title-bfq1ec",
      "author": {
        "username": "commenter-lkwem3",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1544987124549
    },
    {
      "createdAt": 1544987124400,
      "id": "bf4573d0-0093-46cd-b348-d0fcd34e7997",
      "body": "test comment 7u397s",
      "slug": "title-bfq1ec",
      "author": {
        "username": "commenter-lkwem3",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1544987124400
    },
    {
      "createdAt": 1544987124645,
      "id": "6e27ff00-f289-4cde-86a6-f1fa7e8d3547",
      "body": "test comment gghf5r",
      "slug": "title-bfq1ec",
      "author": {
        "username": "commenter-lkwem3",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1544987124645
    },
    {
      "createdAt": 1544987124580,
      "id": "a7acccf4-fcbb-4712-b3c3-005f93ad8936",
      "body": "test comment kb9ekn",
      "slug": "title-bfq1ec",
      "author": {
        "username": "commenter-lkwem3",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1544987124580
    },
    {
      "createdAt": 1544987124428,
      "id": "ce102c7d-9416-4869-991c-aef02f5f7610",
      "body": "test comment 333mw8",
      "slug": "title-bfq1ec",
      "author": {
        "username": "commenter-lkwem3",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1544987124428
    },
    {
      "createdAt": 1544987124701,
      "id": "ca3b3bb4-5b4f-4647-9b4c-61cd021b6cd0",
      "body": "test comment isgv40",
      "slug": "title-bfq1ec",
      "author": {
        "username": "commenter-lkwem3",
        "bio": "",
        "image": "",
        "following": false
      },
      "updatedAt": 1544987124701
    }
  ]
}
```
## Delete
### should delete comment
```
DELETE /articles/title-bfq1ec/comments/bf4573d0-0093-46cd-b348-d0fcd34e7997
```
```
200 OK

{}
```
### only comment author should be able to delete comment
```
DELETE /articles/title-bfq1ec/comments/ce102c7d-9416-4869-991c-aef02f5f7610
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Only comment author can delete: [commenter-lkwem3]"
    ]
  }
}
```
### should disallow unauthenticated user
```
DELETE /articles/title-bfq1ec/comments/ce102c7d-9416-4869-991c-aef02f5f7610
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Must be logged in."
    ]
  }
}
```
### should disallow deleting unknown comment
```
DELETE /articles/title-bfq1ec/comments/foobar_id
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Comment ID not found: [foobar_id]"
    ]
  }
}
```
# User
## Create
### should create user
```
POST /users

{
  "user": {
    "email": "user1-0.7kmnspwg7lx@email.com",
    "username": "user1-0.7kmnspwg7lx",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user1-0.7kmnspwg7lx@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuN2ttbnNwd2c3bHgiLCJpYXQiOjE1NDQ5ODcxMjQsImV4cCI6MTU0NTE1OTkyNH0.GvAXC-Zqo2DeThahTN6E94xn0wca7BDcUFHJE1TeKZo",
    "username": "user1-0.7kmnspwg7lx",
    "bio": "",
    "image": ""
  }
}
```
### should disallow same username
```
POST /users

{
  "user": {
    "email": "user1-0.7kmnspwg7lx@email.com",
    "username": "user1-0.7kmnspwg7lx",
    "password": "password"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Username already taken: [user1-0.7kmnspwg7lx]"
    ]
  }
}
```
### should disallow same email
```
POST /users

{
  "user": {
    "username": "user2",
    "email": "user1-0.7kmnspwg7lx@email.com",
    "password": "password"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email already taken: [user1-0.7kmnspwg7lx@email.com]"
    ]
  }
}
```
### should enforce required fields
```
POST /users

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "foo": 1
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Username must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "username": 1
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email must be specified."
    ]
  }
}
```
```
POST /users

{
  "user": {
    "username": 1,
    "email": 2
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Password must be specified."
    ]
  }
}
```
## Login
### should login
```
POST /users/login

{
  "user": {
    "email": "user1-0.7kmnspwg7lx@email.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user1-0.7kmnspwg7lx@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuN2ttbnNwd2c3bHgiLCJpYXQiOjE1NDQ5ODcxMjUsImV4cCI6MTU0NTE1OTkyNX0.QxE8PjmIwrYWVoV-dSNIyQcru2cjSL-mFO0ezkI-oos",
    "username": "user1-0.7kmnspwg7lx",
    "bio": "",
    "image": ""
  }
}
```
### should disallow unknown email
```
POST /users/login

{
  "user": {
    "email": "0.b15mr6n2omh",
    "password": "somepassword"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email not found: [0.b15mr6n2omh]"
    ]
  }
}
```
### should disallow wrong password
```
POST /users/login

{
  "user": {
    "email": "user1-0.7kmnspwg7lx@email.com",
    "password": "0.fhky6pjvyma"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Wrong password."
    ]
  }
}
```
### should enforce required fields
```
POST /users/login

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
```
POST /users/login

{
  "user": {}
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email must be specified."
    ]
  }
}
```
```
POST /users/login

{
  "user": {
    "email": "someemail"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Password must be specified."
    ]
  }
}
```
## Get
### should get current user
```
GET /user
```
```
200 OK

{
  "user": {
    "email": "user1-0.7kmnspwg7lx@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuN2ttbnNwd2c3bHgiLCJpYXQiOjE1NDQ5ODcxMjUsImV4cCI6MTU0NTE1OTkyNX0.QxE8PjmIwrYWVoV-dSNIyQcru2cjSL-mFO0ezkI-oos",
    "username": "user1-0.7kmnspwg7lx",
    "bio": "",
    "image": ""
  }
}
```
### should disallow bad tokens
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
GET /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
## Profile
### should get profile
```
GET /profiles/user1-0.7kmnspwg7lx
```
```
200 OK

{
  "profile": {
    "username": "user1-0.7kmnspwg7lx",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
### should disallow unknown username
```
GET /profiles/foo_0.2ul9yo2hl1k
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User not found: [foo_0.2ul9yo2hl1k]"
    ]
  }
}
```
### should follow/unfollow user
```
POST /users

{
  "user": {
    "username": "followed_user",
    "email": "followed_user@mail.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "followed_user@mail.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6ImZvbGxvd2VkX3VzZXIiLCJpYXQiOjE1NDQ5ODcxMjUsImV4cCI6MTU0NTE1OTkyNX0.3AY5aB11A27jQFJCN9PO11vnd7U-gt2mCpEEHmqZOKg",
    "username": "followed_user",
    "bio": "",
    "image": ""
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /profiles/followed_user
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
GET /profiles/followed_user
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
POST /users

{
  "user": {
    "username": "user2-0.nfjkfhacjqc",
    "email": "user2-0.nfjkfhacjqc@mail.com",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user2-0.nfjkfhacjqc@mail.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIyLTAubmZqa2ZoYWNqcWMiLCJpYXQiOjE1NDQ5ODcxMjUsImV4cCI6MTU0NTE1OTkyNX0.RoHaootUUpD21YcK1yWVEuD84O3tnlwfzC6W0nYD_1Q",
    "username": "user2-0.nfjkfhacjqc",
    "bio": "",
    "image": ""
  }
}
```
```
POST /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": true
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
```
DELETE /profiles/followed_user/follow
```
```
200 OK

{
  "profile": {
    "username": "followed_user",
    "bio": "",
    "image": "",
    "following": false
  }
}
```
### should disallow following with bad token
```
POST /profiles/followed_user/follow
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
## Update
### should update user
```
PUT /user

{
  "user": {
    "email": "updated-user1-0.7kmnspwg7lx@email.com"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.7kmnspwg7lx",
    "email": "updated-user1-0.7kmnspwg7lx@email.com",
    "image": "",
    "bio": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuN2ttbnNwd2c3bHgiLCJpYXQiOjE1NDQ5ODcxMjUsImV4cCI6MTU0NTE1OTkyNX0.QxE8PjmIwrYWVoV-dSNIyQcru2cjSL-mFO0ezkI-oos"
  }
}
```
```
PUT /user

{
  "user": {
    "password": "newpassword"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.7kmnspwg7lx",
    "email": "updated-user1-0.7kmnspwg7lx@email.com",
    "image": "",
    "bio": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuN2ttbnNwd2c3bHgiLCJpYXQiOjE1NDQ5ODcxMjUsImV4cCI6MTU0NTE1OTkyNX0.QxE8PjmIwrYWVoV-dSNIyQcru2cjSL-mFO0ezkI-oos"
  }
}
```
```
PUT /user

{
  "user": {
    "bio": "newbio"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.7kmnspwg7lx",
    "bio": "newbio",
    "image": "",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuN2ttbnNwd2c3bHgiLCJpYXQiOjE1NDQ5ODcxMjUsImV4cCI6MTU0NTE1OTkyNX0.QxE8PjmIwrYWVoV-dSNIyQcru2cjSL-mFO0ezkI-oos"
  }
}
```
```
PUT /user

{
  "user": {
    "image": "newimage"
  }
}
```
```
200 OK

{
  "user": {
    "username": "user1-0.7kmnspwg7lx",
    "image": "newimage",
    "bio": "newbio",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIxLTAuN2ttbnNwd2c3bHgiLCJpYXQiOjE1NDQ5ODcxMjUsImV4cCI6MTU0NTE1OTkyNX0.QxE8PjmIwrYWVoV-dSNIyQcru2cjSL-mFO0ezkI-oos"
  }
}
```
### should disallow missing token/email in update
```
PUT /user
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Token not present or invalid."
    ]
  }
}
```
```
PUT /user

{}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "User must be specified."
    ]
  }
}
```
### should disallow reusing email
```
POST /users

{
  "user": {
    "email": "user2-0.j9mui155u6n@email.com",
    "username": "user2-0.j9mui155u6n",
    "password": "password"
  }
}
```
```
200 OK

{
  "user": {
    "email": "user2-0.j9mui155u6n@email.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VybmFtZSI6InVzZXIyLTAuajltdWkxNTV1Nm4iLCJpYXQiOjE1NDQ5ODcxMjUsImV4cCI6MTU0NTE1OTkyNX0.7baaLovrvEmZ5dieyOHrFXrj8nzyOIibAwQzXEa38p0",
    "username": "user2-0.j9mui155u6n",
    "bio": "",
    "image": ""
  }
}
```
```
PUT /user

{
  "user": {
    "email": "user2-0.j9mui155u6n@email.com"
  }
}
```
```
422 Unprocessable Entity

{
  "errors": {
    "body": [
      "Email already taken: [user2-0.j9mui155u6n@email.com]"
    ]
  }
}
```
# Util
## Ping
### should ping
```
GET /ping
```
```
200 OK

{
  "pong": "2018-12-16T19:05:25.671Z",
  "AWS_REGION": "us-east-1",
  "DYNAMODB_NAMESPACE": "dev"
}
```
