# NestJs Study

1. hello world
2. express + ts 활용
3. dataMocking 이용한 express 이해하기

- express의 middleware 구현

  - middleware? 서버와 클라이언트 사이에 위치해 두 end point가 데이터를 주고받도록 중간에서 매개 역할을 하는것
  - express의 use 키워드 사용
  - 코드는 위에서 아래로 차례로 실행되므로 use키워드의 위치가 중요
    - middleware역할: api 함수 가장 위에 위치
    - 존재하지 않는 api 요청시 error handling 역할: api 함수를 모두 지난 맨 끝에 위치

  ```
  app.use((req, res, next) =>{
      console.log('logging middleware');
       next();
  });

  app.get('/', (req: express.Request, res: express.Response) => {
      console.log(req.rawHeaders[1]);
      res.send({ animals: Animal });
  });

  app.get('/cat', (req, res) => {
      console.log('cat data');
      res.send({ cat: Animal[2] });
  });

  app.use((req, res, next) =>{
      res.send({ error: '404 not found error' });
  });
  ```

- CRUD 구현하기

1.  Read : 특정 id값 get

```
route.get('/animal/:id', (req, res) => {
    const id = req.params.id;
    const cat = Animal.find((cat) => {
      return cat.id === id;
    });
});
```

2. Create : post메소드로 json으로 입력되어 들어오는 데이터 저장

```
// json middleware: post로 입력받는 데이터(json)를 식별하기 위한 미들웨어
app.use(express.json());

...

route.post('/animal', (req, res) => {
    const id = req.params.id;
    const cat = Animal.find((cat) => {
      return cat.id === id;
    });
});
```

- route (API end-point) 모듈 분리하기
  - 분리 전
    ![모듈분리전](https://user-images.githubusercontent.com/24540759/149896292-f60fbf3d-5ba9-479e-b459-3ba41d46555e.PNG)
  - 분리 후
    ![모듈분리후](https://user-images.githubusercontent.com/24540759/149896308-8d416815-6bb7-4ba6-928d-03b5aaa3ee6c.PNG)
