## Session
### Open session
`GET https://freefeed.net/v1/session?username=myusername&password=mypassword`

**Params**

*username*, *password* : text

#### CURL example
`curl -d "username=myusername" -d "password=mypassword" https://freefeed.net/v1/session
`
#### Returns
json (with *authToken*)

## Users
### Whoami
`GET https://freefeed.net/v1/users/whoami`
`X-Authentication-Token: authToken`

**Params**

*authToken* : token (see "Open Session")

#### CURL example
`curl -H "X-Authentication-Token:authToken" https://freefeed.net/v1/users/whoami`
#### Returns
json (with user profile)
or `{"err":"Not found"}` if authToken invalid

## Attachments
### Upload attachments
```
POST https://freefeed.net/v1/attachments
X-Authentication-Token: authToken
Content-type: multipart/form-data
(files data)
```
**Params**

*authToken* : token (see "Open Session")

#### CURL example
`curl -H "X-Authentication-Token:mytoken" -F "file=@x5.png" https://freefeed.net/v1/attachments`
#### Returns
json (with *attachments.id*)

## Timeline
### Home timeline
```
GET https://freefeed.net/v1/timelines/home?offset=NN
X-Authentication-Token: authToken
```
**Params**

*authToken* : token (see "Open Session")

*NN*: offset in timeline (may be 0,30,60...)

#### CURL example
`curl -H "X-Authentication-Token:authToken" https://freefeed.net/v1/timelines/home?offset=NN`
#### Returns
json (with timeline)
or `{"err":"Not found"}` if authToken invalid

### User timeline
```
GET https://freefeed.net/v1/timelines/username?offset=NN
X-Authentication-Token: authToken
```
**Params**

*authToken* : token (see "Open Session")

*username* : username

*NN* : offset in timeline (may be 0,30,60...)

### 'My Discussions' timeline
```
GET https://freefeed.net/v1/timelines/filter/discussions?offset=NN
X-Authentication-Token: authToken
```
## Posts
### Get post
```
GET https://freefeed.net/v1/posts/postid?maxComments=all&maxLikes=all
X-Authentication-Token: authToken
```
**Params**

*authToken* : token (see "Open Session")

*postid*: post id

#### CURL example
`curl -H "X-Authentication-Token:authToken" https://freefeed.net/v1/posts/postid?maxComments=all&maxLikes=all`
#### Returns
json (with post content)
or `{"err":"Not found"}` if authToken or postid invalid

### Add new post
```
POST https://freefeed.net/v1/posts
Content-type: application/json; charset=utf-8
X-Authentication-Token: authToken
{"post":{"body":"ptext","createdAt":null,"updatedAt":null,"isHidden":false,"createdBy":null,"attachments":[attachid],"likes":[],"groups":[],"timeline":null},"meta":{"feeds":"feedname"}}';
```
**Params**

*authToken* : token (see "Open Session")

*ptext*: post text

*attachid* : attachid (see "Upload attachments") 

`"attachments":[]` if no attachment

`"attachments":["id1","id2"]` if two (or more) attachment

#### CURL example
```
curl -i -X POST -H "Content-type:application/json; charset=utf-8" -H "X-Authentication-Token:mytoken" -d '{"post":{"body":"Это текст вашей записи","createdAt":null,"updatedAt":null,"isHidden":false,"createdBy":null,"attachments":["50d520f9-a953-421a-bc8d-ccbed5cbcd38"],"likes":[],"groups":[],"timeline":null},"meta":{"feeds":"myusername"}}' https://freefeed.net/v1/posts
```
#### Returns
json (with postid)
### Edit post
```
PUT /v1/posts/postid
X-Authentication-Token: authToken
{"post":{"body":"ptext"}}
```
**Params**

*authToken* : token (see "Open Session")

*postid* : post id

*ptext*: post text

#### CURL example
```
curl -i -X PUT -H "Content-type:application/json; charset=utf-8" -H "X-Authentication-Token:mytoken" -d '{"post":{"body":"Это новый текст вашей записи"}}' https://freefeed.net/v1/posts/30d520f9-a953-421a-bc8d-ccbed5cbcd38
```
### Delete post
```
DELETE /v1/posts/postid
X-Authentication-Token: authToken
```
**Params**

*authToken* : token (see "Open Session")

*postid* : post id

#### CURL example
```
curl -i -X DELETE -H "X-Authentication-Token:mytoken"  https://freefeed.net/v1/posts/30d520f9-a953-421a-bc8d-ccbed5cbcd38
```
### Like post
```
POST /v1/posts/postid/like
X-Authentication-Token: authToken
```
**Params**

*authToken* : token (see "Open Session")

*postid* : post id

#### CURL example
```
curl -i -X POST -H "X-Authentication-Token:mytoken"  https://freefeed.net/v1/posts/30d520f9-a953-421a-bc8d-ccbed5cbcd38/like
```
### Hide post
```
POST /v1/posts/postid/hide
X-Authentication-Token: authToken
```
**Params**

*authToken* : token (see "Open Session")

*postid* : post id

#### CURL example
```
curl -i -X POST -H "X-Authentication-Token:mytoken"  https://freefeed.net/v1/posts/30d520f9-a953-421a-bc8d-ccbed5cbcd38/hide
```
### Unlike post
```
POST /v1/posts/postid/unlike
X-Authentication-Token: authToken
```
**Params**

*authToken* : token (see "Open Session")

*postid* : post id

#### CURL example
```
curl -i -X POST -H "X-Authentication-Token:mytoken"  https://freefeed.net/v1/posts/30d520f9-a953-421a-bc8d-ccbed5cbcd38/unlike
```
## Comments
### Add new comment
```
POST /v1/comments
Content-type: application/json; charset=utf-8
X-Authentication-Token: authToken
{"comment":{"body":"ctext","createdAt":null,"updatedAt":null,"postId":"postid","createdBy":null,"post":null}}
```
**Params**

*authToken* : token (see "Open Session")

*ctext* : comment text

*postid* : post id

#### CURL example
```
curl -i -X POST -H "Content-type:application/json; charset=utf-8" -H "X-Authentication-Token:mytoken" -d '{"comment":{"body":"Текст комментария","createdAt":null,"updatedAt":null,"postId":"30d520f9-a953-421a-bc8d-ccbed5cbcd38","createdBy":null,"post":null}}' https://freefeed.net/v1/comments
```
### Edit comment
```
PUT /v1/comments/commentid
X-Authentication-Token: authToken
{"comment":{"body":"ctext"}}
```
**Params**

*authToken* : token (see "Open Session")

*commentid* : comment id

*ctext*: comment text

#### CURL example
```
curl -i -X PUT -H "Content-type:application/json; charset=utf-8" -H "X-Authentication-Token:mytoken" -d '{"comment":{"body":"Это новый комментария"}}' https://freefeed.net/v1/comments/90d520f9-a953-421a-bc8d-ccbed5cbcd38
```
### Delete comment
```
DELETE /v1/comments/commentid
X-Authentication-Token: authToken
```
**Params**

*authToken* : token (see "Open Session")

*commentid* : comment id

#### CURL example
```
curl -i -X DELETE -H "X-Authentication-Token:mytoken"  https://freefeed.net/v1/comments/90d520f9-a953-421a-bc8d-ccbed5cbcd38
```
