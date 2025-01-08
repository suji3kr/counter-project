<br><br>
---------------------------------------
## ***. Counter Project***

<br><br>
### 카운터 앱 만들기 프로젝트 시작 ( React )

<br>

#### Vite + React 사용할 때  <br>
-프로젝트 실행 순서 <br><br>

![화면 캡처 2024-12-20 144741](https://github.com/user-attachments/assets/c55c36bc-29ed-47b0-a574-ccbb59116be6)  <br/>
<br/>
![화면 캡처 2024-12-20 144927](https://github.com/user-attachments/assets/20392df3-296c-4506-9b81-5f8236992557)    <br/>

<br>
      
#### - npm run dev  +  O enter <br>
실행 단축키 기억안날때 h <br>

![화면 캡처 2024-12-20 144927](https://github.com/user-attachments/assets/69e81ba0-fd0c-484d-9d67-e84cf2eb3495)<br>

---------------------------------
<br>

![화면 캡처 2024-12-20 151643](https://github.com/user-attachments/assets/a09cc881-d1f0-474e-949a-e35fb48bfb30)
<br>

![화면 캡처 2024-12-20 151755](https://github.com/user-attachments/assets/bb2fba90-f905-4d85-b489-f7574e129a46)
<br>

      App.jsx 
      
      import './App.css'
      import Controller from './component/Controller';
      import Viewer from './component/viewer';
      
      function App() {
      
        return(
          <>
            <h1>Simple Counter</h1>
            <section>
              <Viewer/>
            </section>
            <section>
              <Controller />
            </section>
          </>
        );
      }
      
      export default App;

<br>

![화면 캡처 2024-12-20 152958](https://github.com/user-attachments/assets/e223df2c-daf6-4f6e-b42e-8ff280650587)

<br>

App.css 적용하려면...? index.css 에 body를 주석처리 하고,

      
      App.css에서 
      
      body {
        padding: 20px;
      }
      
      .App {
        margin: 0 auto;
        width: 500px;
      }
      .App >section {
        padding: 20px;
        background-color: bisque;
        border: 3px solid rgb(60, 124, 167);
        border-radius: 5px;
        margin-bottom: 10px;
      }
      
<br>



<br>

      
App.jsx
<br>

      import { useEffect, useState } from 'react';
      import './App.css'
      import Controller from './component/Controller';
      import Viewer from './component/viewer';
      
      function App() {
      
        const [count, setCount] = useState(0);
        const handleSetCount =(value) => {
          setCount(count + value);
        };
        useEffect(() => {
          console.log("count 업데이트: ", count);
        }, [count]);
      
        return(
          <div className="App">
            <h1>Simple Counter</h1>
            <section>
              <Viewer count = {count}/>
            </section>
            <section>
              <Controller handleSetCount={handleSetCount}/>
            </section>
          </div>
        );
      }
      
      export default App;

<br>      
Controller
<br>

      const Controller =({ handleSetCount }) =>{
          return(
              <>
                  <button onClick={() => handleSetCount(-1)}>-1</button>
                  <button onClick={() => handleSetCount(-10)}>-10</button>
                  <button onClick={() => handleSetCount(-100)}>-100</button>
                  <button onClick={() => handleSetCount(+100)}>+100</button>
                  <button onClick={() => handleSetCount(+10)}>+10</button>
                  <button onClick={() => handleSetCount(+1)}>+1</button>
              </>
          );
      };
      export default Controller;
      
<br>


Viewer
<br>

      const Viewer =({count}) =>{
          return(
              <>
                  <div>현재 카운트: </div>
                  <h1>{count}</h1>
              </>
          );
      };


      
![화면 캡처 2024-12-20 154615](https://github.com/user-attachments/assets/d40c435a-55a7-4f83-b127-ad43255c6b62)

<br>
<br>

App 에 Ref 적용
<br>
      import {useRef,  useEffect, useState } from 'react';
      import './App.css'
      import Controller from "./component/Controller";
      import Viewer from "./component/viewer";
      import Even from "./component/Even";
      
      function App() {
      
        const [count, setCount] = useState(0);
        const [text, setText] = useState("");
        const handleSetCount =(value) => {
          setCount(count + value);
        };
        const handleChangeText = (e) => {
          setText(e.target.value);
        };
      
        const didMountRef = useRef(false);
        useEffect(() => {
          if (!didMountRef.current) {
            didMountRef.current = true;
            return;
          }else {
          console.log("컴포넌트 업데이트!");
          }
        });
      
        useEffect(() => {
          console.log("컴포넌트 마운트");
        }, []);
      
        useEffect(() => {
          const intervalID = setInterval(() => {
          console.log("깜빡");
          }, 1000);
      
          return () => {
            clearInterval("클린업");
            clearInterval(intervalID);
          };
        });
      
        return(
          <div className="App">
            <h1>Simple Counter</h1>
            <section>
              <input value={text} onChange={handleChangeText} />
            </section>
            <section>
              <Viewer count={count}/>
              {count % 2 === 0 && <Even />}
            </section>
            <section>
              <Controller handleSetCount={handleSetCount}/>
            </section>
          </div>
        );
      }
      
      export default App;
      
<br>

Even.jsx
<br>
      
      import { useEffect } from "react";
      
      
      function Even() {
          useEffect(() => {
              return () => {
                  console.log("Even 컴포넌트 언마운트");
              };
          }, []);
          
          return <div> 현재 카운트는 짝수 입니다</div>;
      }
      export default Even;

<br>

![화면 캡처 2024-12-20 163440](https://github.com/user-attachments/assets/aad171c4-b404-4273-9758-41754adbad86)

<br>
