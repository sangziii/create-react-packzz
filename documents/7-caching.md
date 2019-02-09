# 5. Caching

브라우저가 static 자원을 요청할 때, 불필요한 traffic을 줄이기 위해 캐싱 기법을 이용한다. 근데 이 캐싱 기법 이용시에 새로운 코드가 배포됐을 시에는 서버의 응답값으로 캐싱된 자원을 주면 안된다. 기존에는(그냥 내가 알기에 기존에는..) 자원 요청 url에 쿼리스트링에 timestamp를 이용하여 캐시기법을 이용했다. 근데 이 기법은 코드 변경 유무와 관계없이 빌드될 때마다 timestamp가 변경되었다. 이것의 문제점은 코드가 변경되지 않았어도 timestamp가 변경되어 불필요한 트래픽을 유발한다.

이것을 웹팩은 contents가 바뀌지 않은 경우에는 cached 된채로 남겨두는 컴파일 방법을 통하여 쉽게 해결할 수 있다.

## output filename

`output.filename` [대체](https://webpack.js.org/configuration/output/#output-filename) 기법을 이용하여 output file 이름을 정의할 수 있다. 

이 중 `[contenthash]` 대체 기법을 이용하여 unique hash를 filename에 추가할 것이다.

> [contenthash]
> asset content가 변경될 때만 [contenthash]가 변경됨.

webpack의 output.filename을 다음과 같이 변경하자.

```js
output: {
  filename: "[name].[contenthash].js",
}
```

npm run build 해보자. 2번 반복해서 hash값이 그대로인지 확인하고, 코드 한 줄 변경 후 hash값이 변경됐는지 확인하자.