1. 반복문 (forEach)

```javascript
const colors = ["red","green","yellow"]
for(const color of colors) {
    console.log(color)
}
------------------------------------------
colors.forEach(function(color) {
    console.log(color)
})
```



2. callback은 세가지 인수를 받음

```javascript
function handlePosts(){
    const posts = [
        {id:1, title:"hihi"},
        {id:13, title:"hello"},
        {id:17, title:"123456"},
    ]
    // for(let i=0; i < posts.length; i++){
    //     console.log(posts[i].title)
    
    // posts.forEach(post => {
    //     console.log(post.title)
    // })

    posts.forEach((post,index,original) => {
        console.log(original)
        // post : 요소값
        // index : 요소 인덱스
        // original : 순회 중인 배열
    })
}
handlePosts()
```



3. map

```javascript
const numbers = [1,2,3]

const double = [1,2,3].map(function(number){
    return number *= 2
})

console.log(double)

---------------------------------------------------
const images = [
    {h:"30px",w:"30px"},
    {h:"50px",w:"500px"},
    {h:"100px",w:"1000px"},
]

const res = images.map(image =>{
    return image.h
})
console.log(res)
>>> [ '30px', '50px', '100px' ]

const trips = [
    {distance:30,time:10},
    {distance:90,time:50},
    {distance:59,time:25},
]

// 속도값이 들어있는 배열을 반환

const speed = trips.map(trip =>{
    return trip.distance/trip.time
})

console.log(speed)
>>> [ 3, 1.8, 2.36 ]
```



4. filter

```javascript
const products = [
    {name : 'phone', value:100},
    {name : 'notebook', value:200},
    {name : 'desktop', value:200},
    {name : 'mouse', value:1},
]

const twoH = products.filter(function(product) {
    return product.value === 200
})

console.log(twoH)
>>>[ { name: 'notebook', value: 200 },
  { name: 'desktop', value: 200 } ]


---------------------------------------------
const numbers = [10,20,30]

function reject(array, callback){
    return array.filter(callback)
}

const lessThan15 = reject(numbers, function(number){
    return number < 15
})

console.log(lessThan15)
>>> [10]

------------------------------------------------
const numbers = [10,20,30]

function reject(array, callback){
    return array.filter(callback)
}

const lessThan15 = reject(numbers, function(number){
    return number < 15
})

console.log(lessThan15)
>>> [10]
```



5. 동기 // 비동기

- `blocking` - `python`
  - 다른 함수가 실행이 되지 않도록 막고있음
- `non-blocking` - `javascript`
  - 안 막음
  - 순서대로 실행되는걸 보장하지 않음
  - `single thread `이기 때문 그래서 `call back`을 사용해 blocking할수 있도록 함
    - 많은 `call back`은 안좋아서 ES6에서 `promise` 라는걸로..?



6. then, catch

```javascript
// function makeOrdeR(){}
const makeOrder = function(order){
    let coffee

    setTimeout(function(){
        coffee = order
    },3000)

    return coffee
}

const coffee = makeOrder("Americano")
console.log(커피)

>>> undefined
3초후
>>> 

// nonblocking으로 돌아가니까 안되는 것
```

- `call back`을 이용한 해결

```javascript
const makeOrder = function(order, serve){
    let coffee

    setTimeout( function(){
        coffee = order
        serve(커피)
    }, 3000)
    return coffee
}
// 두번째에는 다음에 실행시킬 함수를 넣어줌
const coffee = makeOrder("Americano", console.log)
>>> 3초 후에 
>>> Americano
```

- `Promise`를 이용한 해결

```javascript
// 1 . 오더를 받는다.
// 2 . 종업원이 약속을 한다.(잘 됐는지 안됐는지를)
// 2-1. 다 만들면 resolve로 커피를 주고
// 2-2. 문제가 있으면 reject로 알려준다.

const makeOrder = (order) => /* Promise 객체 생성*/ new Promise(function(resolve, reject){
        let coffee

        setTimeout(function() {
            // 실패한 경우
            if(order === undefined){
                reject("주문 잘못하셨어요")
            } else{
                // 성공한 경우
                coffee = order
                resolve(커피)
            }
        }, 3000)
    })

makeOrder()
// then이 실행되려면 항상 앞의 함수가 성공해야 함.
.then((커피) => {console.log(커피)}) // 성공
.catch((error) => {console.log(error)}) // 실패

>>> 3초후
>>> Americano

makeOrder()
.then((커피) => {console.log(커피)})
.catch((error) => {console.log(error)})

>>> 3초후
>>> 주문 잘못하셨어요

makeOrder()
.then((커피) => {console.log(커피)}) // 성공
.catch((error) => {console.log(error)}) // 실패
.then((커피) => {console.log(커피)}) // 성공을하던 실패를하던 출력 : then과 catch의 순서가 중요한 이유

// makeOrder에 undefined가 넘어가기 때문에 "주문 잘못하셨어요"가 출력되고
// .then과 .catch를 건너 뛰고 2번째 .then을 출력
>>> 3초후
>>> 주문 잘못하셨어요
>>> undefined
```

