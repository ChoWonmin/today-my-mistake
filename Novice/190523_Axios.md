# Axios

[A**** B***]

axios를 이용해서 api function을 만들고 있었다.

```ts
async upLike(groupId: string) {
    return new Promise(async (resolve, rejects) => {
      const header = util.createHeader(ContentType.JSON);
      console.warn('header', header);

      const result = await util.makeAxiosDefaultPromise(
        axios.post(`${util.HOST}/안알랴줌/${groupId}/안알랴줌`, header)
      );
      resolve(result);
    });
  }
```

### 문제 상황

위와 같이 post로 쿼리를 날리는데 response code로 401 unauthorization이 발생

postman으로 같은 쿼리를 날리면 정상작동했다.

```ts
async upLike(groupId: string) {
    return new Promise(async (resolve, rejects) => {
      const header = util.createHeader(ContentType.JSON);
      console.warn('header', header);

      const result = await util.makeAxiosDefaultPromise(
        axios.post(`${util.HOST}/안알랴줌/${groupId}/안알랴줌`, {}, header)
      );
      resolve(result);
    });
  }
```

### 실수/착각

401 unauthorization이 발생해서 Bearer 보안 문제일거라고 생각했다.

### 해결방안

하지만...
post는 당연히 body가 존재한다. axios.post() 2번째 parameter로 body를 안 적었네.... 실수하지말자
