# APIs
```
POST "/api/batting/createBatting"       베팅 생성
GET "/api/batting/getBattings"          베팅 읽기 (복수)
GET "/api/batting/getBatting"           베팅 읽기 (단일)
PUT "/api/batting/editBatting"          베팅 수정
DELETE "/api/batting/deleteBatting"     베팅 삭제
```
<br>

# Batting Model Schema
```js
var BattingSchema = mongoose.Schema({
    user: {
        type: mongoose.Schema.Types.ObjectId,
        required: true
    },
    userNickname: {  // 논의 필요.
        type: String,
        required: true
    },
    match: {
        type: mongoose.Schema.Types.ObjectId,
        required: true
    },
    chooseHomeAwayDraw: {
        type: String,
        enum: [Home, Away, Draw], 
        required: true
    },
    battingPoint: {
        type: Number,
        required: true
    },
    createdAt: {
        type: Date,
        default: Date.now
    },
    description: {
        type: String,
    },
});
```
<br>

# API spec

## __베팅 생성__ POST "/api/batting/createBatting" 
__Requset__
```
method: POST
url: "/api/batting/createBatting"
header: { 
    "Content-type": "application/json", 
    "x-access-token": "token value" 
}
body: {
    "user": req.user._id  // inputed automatically
    "batting": req.params.matchId,  // inputed automatically
    "chooseHomeAwayDraw": "Home",
    "battingPoint": "10",
    "description": "cause I feel good"
}
```

__Response__
```
{
    "success": true,
    "data": {
        "_id": "shdflkewjklrjklhlk325sdhflk24sdlkfj",
        "user": req.user._id,  // inputed automatically
        "batting": req.params.matchId,  // inputed automatically
        "chooseHomeAwayDraw": "Home",
        "battingPoint": "10",
        "description": "cause I feel good"
    }
}
```
<br>

## __베팅 읽기 (복수)__ GET "/api/batting/getBattings"
- Need query conditions                 /////!!

__Requset__
```
method: GET
url: "/api/batting/getBattings"
header: { 
    "Content-type": "application/json" 
}
```

__Response__
```
{
    "success": true,
    "data": [{
        "user": "sdqwehlk23lksjfklds",
        "batting": "dhflkj3234hkldjfksldjf",
        "chooseHomeAwayDraw": "Home",
        "battingPoint": "10",
        "description": "cause I feel good"
    }, {
        "user": "dhsfklj3hslkjklds5sdlfhekl"
        "batting": "dfhelkjfdsfh343kdfhsdlk"
        "chooseHomeAwayDraw": "Home",
        "battingPoint": "40",
        "description": "I feel bad"
    }]
}
```
<br>

## __베팅 읽기 (단일)__ GET "/api/batting/getBatting/:battingId"
__Requset__
```
method: GET
url: "/api/batting/getBatting/:battingId"
header: { 
    "Content-type": "application/json" 
}
```

__Response__
```
{
    "success": true,
    "data": {
        "user": "sdfedkflj343dflkjdk"
        "batting": "dhgklj3kl33klj2lkjklsdjf3" 
        "chooseHomeAwayDraw": "Home",
        "battingPoint": "10",
        "description": "cause I feel good"
    }
}
```
<br>


## __베팅 수정__ PUT "/api/batting/editBatting/:battingId"
- Batting onwer can do

__Requset__
```
method: PUT
url: "/api/batting/editBatting/:battingId"
header: { 
    "Content-type": "application/json", 
    "x-access-token": "token value" 
}
body: {
    "chooseHomeAwayDraw": "Away"
}
```

__Response__
```
{
    "success": true,
    "data": {
        "user": "sdfedkflj343dflkjdk"
        "batting": "dhgklj3kl33klj2lkjklsdjf3" 
        "chooseHomeAwayDraw": "Away",
        "battingPoint": "10",
        "description": "cause I feel good"
    }
}
```
<br>

## __베팅 삭제__ DELETE "/api/batting/deleteBatting/:battingId"
- Batting onwer can do

__Requset__
```
method: DELETE
url: "/api/batting/deleteBatting/:battingId"
header: {
    "Content-type": "application/json",
    "x-access-token": "token value"
}
```

__Response__
```
{
    "success": true,
    "data": ""
}
```