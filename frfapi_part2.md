## Posts
### Unhide post
```
POST /v1/posts/postid/unhide
X-Authentication-Token: authToken
```

**Params**

*authToken* : token (see "Open Session")

*postid* : post id

#### CURL example
`curl -H "X-Authentication-Token:authToken" -X POST https://freefeed.net/v1/posts/30d520f9-a953-421a-bc8d-ccbed5cbcd38/unhide
`
#### Returns
json 

### Disable comments
```
POST /v1/posts/postid/disableComments
X-Authentication-Token: authToken
```

**Params**

*authToken* : token (see "Open Session")

*postid* : post id

#### CURL example
`curl -H "X-Authentication-Token:authToken" -X POST https://freefeed.net/v1/posts/30d520f9-a953-421a-bc8d-ccbed5cbcd38/disableComments
`
#### Returns
json 

### Enable comments
```
POST /v1/posts/postid/enableComments
X-Authentication-Token: authToken
```

**Params**

*authToken* : token (see "Open Session")

*postid* : post id

#### CURL example
`curl -H "X-Authentication-Token:authToken" -X POST https://freefeed.net/v1/posts/30d520f9-a953-421a-bc8d-ccbed5cbcd38/enableComments
`
#### Returns
json 

## Users
### Ban user
```
POST /v1/users/username/ban
X-Authentication-Token: authToken
```

**Params**

*authToken* : token (see "Open Session")

*username* : username to be banned

#### CURL example
`curl -H "X-Authentication-Token:authToken" -X POST https://freefeed.net/v1/users/dumbbob/ban
`
#### Returns
json 

### Unban user
```
POST /v1/users/username/unban
X-Authentication-Token: authToken
```

**Params**

*authToken* : token (see "Open Session")

*username* : username to be unbanned

#### CURL example
`curl -H "X-Authentication-Token:authToken" -X POST https://freefeed.net/v1/users/dumbbob/unban
`
#### Returns
json 

### Subscribe to user feed
```
POST /v1/users/username/subscribe
X-Authentication-Token: authToken
```

**Params**

*authToken* : token (see "Open Session")

*username* : username to be subscribed

#### CURL example
`curl -H "X-Authentication-Token:authToken" -X POST https://freefeed.net/v1/users/alice22/subscribe
`
#### Returns
json 

### Unsubscribe from user feed
```
POST /v1/users/username/unsubscribe
X-Authentication-Token: authToken
```

**Params**

*authToken* : token (see "Open Session")

*username* : username to be unsubscribed

#### CURL example
`curl -H "X-Authentication-Token:authToken" -X POST https://freefeed.net/v1/users/alice22/unsubscribe
`
#### Returns
json 

### Get user subscriptions
```
GET /v1/users/username/subscriptions
X-Authentication-Token: authToken
```

**Params**

*authToken* : token (see "Open Session")

*username* : username 

#### CURL example
`curl -H "X-Authentication-Token:authToken"  https://freefeed.net/v1/users/alice22/subscriptions
`
#### Returns
json 

### Get user subscribers
```
GET /v1/users/username/subscribers
X-Authentication-Token: authToken
```

**Params**

*authToken* : token (see "Open Session")

*username* : username 

#### CURL example
`curl -H "X-Authentication-Token:authToken"  https://freefeed.net/v1/users/alice22/subscribers
`
#### Returns
json 

## Timelines
### Direct timeline
```
GET https://freefeed.net/v1/timelines/filter/directs
X-Authentication-Token: authToken
```
**Params**

*authToken* : token (see "Open Session")

#### CURL example
`curl -H "X-Authentication-Token:authToken" https://freefeed.net/v1/timelines/filter/directs
#### Returns
json (with directs)
or `{"err":"Not found"}` if authToken invalid

### User likes timeline
```
GET https://freefeed.net/v1/timelines/username/likes?offset=NN
X-Authentication-Token: authToken
```
**Params**

*authToken* : token (see "Open Session")

*username* : username

*NN* : offset in timeline (may be 0,30,60...)

### User comments timeline
```
GET https://freefeed.net/v1/timelines/username/comments?offset=NN
X-Authentication-Token: authToken
```
**Params**

*authToken* : token (see "Open Session")

*username* : username

*NN* : offset in timeline (may be 0,30,60...)
