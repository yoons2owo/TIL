# 비동기

## promise vs async/await

### Promise를 이용한 비동기 요청 처리 방법
* getUsers() 메소드는 promise 객체를 리턴하고, JSON 객체가 resolve 됨
* 콜백 지옥을 벗어날 수 있음

```js
const users = () => {
    getUsers()
        .then(users => {
            // TODO: logic
            console.log(users);
            return users;
        })
        .catch(error => {
            // TODO: error handling
        });
}
```

### async / await 를 이용한 비동기 요청 처리 방법
* 함수를 선언할때 async라는 단어를 붙임
* await이라는 단어는 async로 정의된 함수에서만 사용되며, 비동기 함수를 call할때 앞에 붙여 사용
* await getUsers()는 getUsers()의 promise가 resolve된 후에 응답 데이터가 전달
* 동기적 코딩을 위함(순차 진행)
```js
const users = async() => {
    // TODO: logic
    console.log(await getUsers());
    return await getUsers();
}
```