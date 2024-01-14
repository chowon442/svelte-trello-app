
## 내용 정리

- 모듈 문제  
ES 모듈을 사용할 때, __dirname을 사용하면 ReferenceError가 생긴다.  
CommonJS에서 사용하던 __dirname 변수가 ES 모듈에서는 없기 떄문에 발생하는 에러.  
```javascript
// 대체 코드
const __dirname = path.resolve();
```

- storage API


## 참고
https://www.inflearn.com/course/%EC%8A%A4%EB%B2%A8%ED%8A%B8-%EC%99%84%EB%B2%BD-%EA%B0%80%EC%9D%B4%EB%93%9C