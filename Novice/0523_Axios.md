# Axios

[As*** Ba*k]

axios를 이용해서 api function을 만들고 있었다.

```js
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

위와 같이 post로 쿼리를 날리는데 response code로 401 unauthorization이 발생

```js
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

post는 당연히 body가 존재한다. axios.post() 2번째 parameter에 {}를 안 적었네.... 실수하지말자
