
## 내용 정리

- 모듈 문제  
ES 모듈을 사용할 때, __dirname을 사용하면 ReferenceError가 생긴다.  
CommonJS에서 사용하던 __dirname 변수가 ES 모듈에서는 없기 때문에 발생하는 에러.  
```javascript
// 대체 코드
const __dirname = path.resolve();
```

- storage API  
웹 스토리지를 사용할 때 주의해야 할 점: 오직 문자형(string) 데이터 타입만 지원  
해결: JSON 형태로 데이터를 읽고 쓰기  
[ 로컬 스토리지에 쓸 데이터를 JSON 형태로 직렬화(serialization) / 읽은 데이터를 JSON 형태로 역직렬화(deserialization) ]
```javascript
// 값을 가져올 때,
const repoLists = JSON.parse(window.localStorage.getItem("lists")) || []
// 값을 설정할 때,
const _lists = writable(repoLists)
_lists.subscribe($lists => {
    window.localStorage.setItem("lists", JSON.stringify($lists))
})
```

- 특정 모듈 사용 시 생기는 롤업 번들러 문제  
rollup-plugin-node-builtins: Node 내장 API를 사용할 수 있게 해줌. (builtins)  
rollup-plugin-node-globals: 일부 Node 모듈이 필요로 하는 전역 API를 사용할 수 있게 해줌. (globals)  
rollup-plugin-replace: 번들 파일의 문자를 대체. 문제가 발생하는 코드를 다른 코드로 대체 실행하기 위해 사용한다. (replace)  
```javascript
// resolve(), 위에
replace({
    values: {
        'crypto.randomBytes': 'require("randombytes")'
    }
}),
// commonjs(), 밑에
globals(),
builtins(),
```

- 수정 모드


## 참고
https://www.inflearn.com/course/%EC%8A%A4%EB%B2%A8%ED%8A%B8-%EC%99%84%EB%B2%BD-%EA%B0%80%EC%9D%B4%EB%93%9C