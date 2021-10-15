## FE 지식

- **브라우저 렌더링 과정**
    1. 서버로부터 `HTML` , `CSS` 를 받는다.
        1. 단순한 텍스트 파일이다.
    2. `HTML` 은 `DOM` 으로, `CSS` 는 `CSSOM` 으로.
        1. `DOM` : HTML 문서의 프로그래밍 interface.
            - 프로그래밍 언어가 DOM구조에 접근할 수 있는 방법을 제공.
            - 단순 텍스트로 구성된 HTML 문서의 내용과 구조가 **객체 모델**로 변환되어 다양한 프로그램에서 사용될 수 있다.
    3. `Rendering Tree` 생성. - 브라우저에 표시될 요소들만 가지고 있는.
    4. Layout 계산. - 노드들이 뷰포트 내에서 어디에 위치할 건지 계산.
    5. 그리기.
- **웹 프로토콜**
    1. 웹 프로토콜
        - 웹 프로토콜은 웹에서 쓰이는 통신규약입니다. 통신규약이라는 것은 쉽게 설명하면, 통신을 할때 내가 이렇게 할게 너는 이렇게 해줘 라고 약속하는 것입니다.
    2. HTTP?
        - 웹 프로토콜중 하나로 HTTP가 가장 많이 쓰이는데 Hyper text Transfer Protocol의 약자입니다.
        - 쉽게말하면, 인터넷에서 **데이터를 주고 받을 수 있는 통신규약** 정도로 보시면됩니다. 요청과 응답으로 이루어져있어 어떤 데이터 주세요하고 요청하면, 이 데이터 줄게요 라고 응답합니다.
    3. HTTP vs HTTPS?
        - 결정적 차이는 **보안**이다.
        - http방식은 네트워크상에서 정보를 누군가가 마음대로 열람, 수정이 가능 / https는 누가 볼수없도록 막음.
        - http방식이 https방식보다 빠르다.
        - Http방식은 민감한정보를 다룰 때 항상 변조, 해킹 가능성을 생각해야한다. Https는 설치 및 인증서를 유지하는데 추가적인 비용이 발생. -> 따라서, 민감한 정보가 있는 페이지의 경우 Https 그럴필요가없으면 http로 만들면 된다.
    
    ---
    
- 세션과 토큰 사용이유
    
    HTTP의 특징이자 약점을 보안하기 위해서 사용된다. 특징이자 약점은 바로 Connectionless(비연결지향), Statelss(상태 정보 유지 안함)이다. 이때 Session과 Cookie가 없다면 로그인이 되었을때 글 작성이 가능한 사이트를 이용하고자 한다면 글을 작성 할 때마다 매번 아이디와 비밀번호를 작성해야 될것이다.
    
- `Javascript`
    - **Event** 흐름
        
        이벤트는 **캡쳐링** → **버블링** 순서로 발생한다. 
        
        ![%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%20%E1%84%8C%E1%85%AE%E1%86%AB%E1%84%87%E1%85%B5%2003ec0f3145fb40099032bc2c96728326/Untitled.png](%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%20%E1%84%8C%E1%85%AE%E1%86%AB%E1%84%87%E1%85%B5%2003ec0f3145fb40099032bc2c96728326/Untitled.png)
        
        1. 캡처링 단계 – 이벤트가 하위 요소로 전파되는 단계
        2. 타깃 단계 – 이벤트가 실제 타깃 요소에 전달되는 단계
        3. 버블링 단계 – 이벤트가 상위 요소로 전파되는 단계
        
        **Event Bubbling**
        
        한 요소에 이벤트가 발생하면, 이 요소에 할당된 핸들러가 동작하고, 이어서 **부모 요소의 핸들러가 동작**합니다. 가장 최상단의 조상 요소를 만날 때까지 이 과정이 반복되면서 요소 각각에 할당된 핸들러가 동작합니다.
        
        - 중단하는 법
            
            → `event.stopPropagation` 함수 사용.
            
        
        **Event Capturing**
        
        ```jsx
        elem.addEventListener(..., true)
        ```
        
        이런식으로 `true` 값을 주면 캡쳐링 함.
        
        **Event Delegation**
        
        1. 컨테이너에 하나의 핸들러를 할당합니다. / 상위요소에 추가함.
        2. 핸들러의 `event.target`을 사용해 이벤트가 발생한 요소가 어디인지 알아냅니다.
        3. 원하는 요소에서 이벤트가 발생했다고 확인되면 이벤트를 핸들링합니다.
    - 클로저
        - 정의
            - **반환된 내부함수**가 자신이 **선언됐을 때의 환경(Lexical environment)인 스코프**를 기억하여 자신이 선언됐을 때의 환경(스코프) 밖에서 호출되어도 **그 환경(스코프)에 접근할 수 있는 함수**
            - 자신이 생성될 때의 환경(Lexical environment)을 기억하는 함수.
            - 외부 변수를 기억하고 이 외부 변수에 접근할 수 있는 함수를 의미
        - 작동 방식
            - 숨김 프로퍼티인 `[[Environment]]` 를 이용해 자신이 어디서 만들어졌는지를 기억. 함수 내부의 코드는 `[[Environment]]` 를 사용해 외부 변수에 접근합니다.
        - 사용 이유
            
            1) 현재 상태를 기억하고 변경된 최신 상태를 유지하기 위해
            
            2) 전역 변수의 사용을 억제 하기위해
            
            3) 정보를 은닉하기 위해
            
    - **this**
        
        [JS 지식_1. this란?](https://velog.io/@ghdtjrrl94/JS-%EC%A7%80%EC%8B%9D1.-this%EB%9E%80)
        
    - **prototype**
        - 정의
            - 상속을 구현하여 불필요한 중복을 제거
        - 생성자 함수가 생성할 모든 인스턴스가 공통적으로 사용할 프로퍼티나 메소드를 프로토타입에 미리 구현해 놓음으로써 위(부모) 객체인 프로토타입의 자산을 공유하여 사용
    - **var**, **let**, **const** 정리
        
        ### 가장 먼저 기본적인 특징
        
        - `var`는 이미 선언되어있는 이름과 같은 이름으로 변수를 또 선언해도 에러가 나지 않지만 `let`, `const`는 이미 존재하는 변수와 같은 이름의 변수를 또 선언하면 에러.
        - `var`, `let`은 변수 선언시 초기 값을 주지 않아도 되지만 `const`는 반드시 초기값 할당해야함.
        - `var`, `let`은 값을 다시 할당할 수 있지만 `const`는 한번 할당한 값은 변경불가
            
            (단, 객체 안에 프로퍼티가 변경되는 것까지 막지는 못함.)
            
        
        ### 중요 특징
        
        - `var`는 **함수 레벨 스코프**이고 `let`, `const`는 **블록 레벨 스코프**임.
            - **함수 레벨 스코프**란?
                - 함수 내에서 선언된 변수는 함수 내에서만 유효하며 함수 외부에서는 참조할 수 없다.
                    
                    → 함수 내부에서 선언한 변수는 지역 변수이며 함수 외부에서 선언한 변수는 모두 전역 변수이다.
                    
                    ![%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%20%E1%84%8C%E1%85%AE%E1%86%AB%E1%84%87%E1%85%B5%2003ec0f3145fb40099032bc2c96728326/Untitled%201.png](%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%20%E1%84%8C%E1%85%AE%E1%86%AB%E1%84%87%E1%85%B5%2003ec0f3145fb40099032bc2c96728326/Untitled%201.png)
                    
                    **블록 레벨 스코프를 따르지 않는** `var` 키워드의 특성 상, 코드 블록 내의 변수 `foo`는 전역 변수이다. 
                    
                    그런데 이미 전역 변수 foo가 선언되어 있다. 
                    
                    var 키워드를 사용하여 선언한 변수는 중복 선언이 허용되므로 위의 코드는 문법적으로 아무런 문제가 없다. 
                    
                    단, 코드 블록 내의 변수 foo는 전역 변수이기 때문에 전역에서 선언된 전역 변수 foo의 값 123을 새로운 값 456으로 재할당하여 덮어쓴다.
                    
        - `var`로 선언한 변수는 선언 전에 사용해도 에러가 나지 않지만 `let`, `const`는 에러 발생.
            - `var` 는 호이스팅이 되어 할당 전에 접근하면 `undefined` 가 뜬다. (실행가능.)
            - `let` , `const` 도 호이스팅이 된다.
                - 쓰기전까지 **TDZ**에 있어서 `not defined` 에러가 뜬다.
                - 할당되기 전까지는 **TDZ**에 있다.
    - **호이스팅**
        - 정의
            - 사전적) 밧줄이나 장비를 이용하여 끌어올리다.
            - 코드를 실행하기 전에 **실행 컨텍스트를 위해** 함수와 변수를 **메모리에 저장**
            
            or **쉽게는 함수 안에 있는 선언들을 모두 끌어올려서 해당 함수 유효 범위의 최상단에 선언하는 것**
            
        - 함수는 전체 함수에 대한 참조와 함께 저장되고, var 키워드가 있는 변수는 undefined, let 및 const 키워드가 있는 변수 는 초기화되지 않은 상태로 메모리에 저장.
        - 함수 선언식은 호이스팅 되지만 함수 표현식은 ㄴㄴ
    - `undefined` 와 `null`
        
        두개 모두 원시값이다. - string, number, boolean, undefined, null, bigint, symbol
        
        원시값이란 - 객체가 아니면서도, 메서드도 가지지 않는 타입, 쉽게 말해 기본타입.
        
        - `undefined` : 변수가 선언되었으나 현재 아무런 값도 할당되지 않은 상태
        - `null` : 선언 후 빈 값을 할당한 상태. / 의도적으로 비어있음을 표현. → 타입을 확인해 보면 'object' 이다.
    - `==` 와 `===`
        - `==` : 동등 연산자. 다른 타입이여도 강제로 변환해서 비교.
            - ex) `0 == '0'` : `true` / `false == '0'` : `true`
        - `===` : 일치 연산자. 타입까지 비교.
    - `call`, `apply` , `bind`
        
        → 모두 `this` 를 조작하기 위해서 쓰이는 친구들. 
        
        → 어떤 함수의 메소드로써 쓰이며 그 함수의 `this` 를 바꿔준다.
        
        [https://beomy.tistory.com/4](https://beomy.tistory.com/4)
        
        - `call` : 첫번째 인수: `this` , 이어지는 것들은 arguments. comma로
        - `apply` : 첫번째 인자: `this`, 이어지는 것들은 arguments 배열형태로.
        - `bind` : `this` 를 수정하는 방법.
    - **Debounce, Throttle**
        
        두 개념 모두 자주 사용되는 이벤트나 함수들의 실행되는 빈도를 줄여 성능의 유리함을 추구
        
        > 키보드로 한자씩 입력할 때마다 입력이 끝난 후나 입력되는 중간 중간 200ms마다 api를 가져오려고 한다.
        > 
        
        ### Debounce
        
        입력이 끝난 후 api값을 가져온다.
        
        Debounce 는 여러번 발생하는 이벤트에서, 가장 마지막 이벤트 만을 실행 되도록 만드는 개념이다.
        
        예) 검색 기능
        
        ### Throttle
        
        입력주기를 방해하지 않고, 일정시간 동안의 입력을 모아 한번에 처리.
        
        Throttle 는 여러번 발생하는 이벤트를 일정 시간 동안, 한번만 실행 되도록 만드는 개념이다.
        
        예) 무한 스크롤
        
- `Typescript`
    - **Typescript** 란?
        - 컴파일 언어, 정적 타입 언어이다.
        - 코드 수준에서 미리 타입을 체크하고 오류를 발견한다.
        - 비교
            - `Javascript` 는 동적 언어 / 런타임에 타입이 결정된다.
    - **Type Aliases** ( 타입 별칭)
        - 정의
            - 특정 타입이나 인터페이스를 참조할 수 있는 타입 변수를 의미
            - 새로운 타입 값을 하나 생성하는 것이 **아니라** 정의한 타입에 대해 **나중에 쉽게 참고할 수 있게 이름을 부여**하는 것
        - `interface` 와 다른점
            - 원래는 `extends` 의 지원 유무였는데 바뀜.
                
                → `interface` 는 `extends` 로 확장이 가능.
                
                → `type` 은 `&` 로 확장.
                
    - **interface**
        - 정의
            - 일종의 새로운 시스템 규약.
            - 쉽게 말하면 여러가지 타입을 갖는 새로운 타입을 정의하는 것.
        - 옵션 속성
            - 아래와 같이 `?` 를 통해 선택적으로 적용할 수 있음.
            
            ![%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%20%E1%84%8C%E1%85%AE%E1%86%AB%E1%84%87%E1%85%B5%2003ec0f3145fb40099032bc2c96728326/Untitled%202.png](%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%20%E1%84%8C%E1%85%AE%E1%86%AB%E1%84%87%E1%85%B5%2003ec0f3145fb40099032bc2c96728326/Untitled%202.png)
            
        - 읽기 전용 속성
            - 처음 생성할때만 할당하고 변경 불가.
            
            ![%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%20%E1%84%8C%E1%85%AE%E1%86%AB%E1%84%87%E1%85%B5%2003ec0f3145fb40099032bc2c96728326/Untitled%203.png](%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%20%E1%84%8C%E1%85%AE%E1%86%AB%E1%84%87%E1%85%B5%2003ec0f3145fb40099032bc2c96728326/Untitled%203.png)
            
        - 상속 가능
            - `extends` 를 통해 확장이 가능.
            
            ![%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%20%E1%84%8C%E1%85%AE%E1%86%AB%E1%84%87%E1%85%B5%2003ec0f3145fb40099032bc2c96728326/Untitled%204.png](%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%20%E1%84%8C%E1%85%AE%E1%86%AB%E1%84%87%E1%85%B5%2003ec0f3145fb40099032bc2c96728326/Untitled%204.png)
            
            - `interface` 를 다시 선언함으로 상속을 구현할 수 있다.
            
            ```jsx
            interface IStudent {
            id: number;
            name: string;
            }
            
            interface IStudent {
            age: number;
            }
            
            const student: Istudent // id, name, age 속성 모두 가지고 있다.
            ```
            
    - **Enum**
        - 정의
            - 특정 값들의 집합.
        - 숫자형 **Enum**
            - 아래 처럼 초기값 설정해주면 1씩 늘어나서 배정받음.
            
            ![%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%20%E1%84%8C%E1%85%AE%E1%86%AB%E1%84%87%E1%85%B5%2003ec0f3145fb40099032bc2c96728326/Untitled%205.png](%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%20%E1%84%8C%E1%85%AE%E1%86%AB%E1%84%87%E1%85%B5%2003ec0f3145fb40099032bc2c96728326/Untitled%205.png)
            
            - 기본은 0부터 시작.
            - 실제 사용은 아래처럼 할 수 있다.
            
            ![%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%20%E1%84%8C%E1%85%AE%E1%86%AB%E1%84%87%E1%85%B5%2003ec0f3145fb40099032bc2c96728326/Untitled%206.png](%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%20%E1%84%8C%E1%85%AE%E1%86%AB%E1%84%87%E1%85%B5%2003ec0f3145fb40099032bc2c96728326/Untitled%206.png)
            
        - 문자형 **Enum**
            - 문자형 이넘은 이넘 값 전부 다 특정 문자 또는 다른 이넘 값으로 초기화 해줘야 함.
                
                ![%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%20%E1%84%8C%E1%85%AE%E1%86%AB%E1%84%87%E1%85%B5%2003ec0f3145fb40099032bc2c96728326/Untitled%207.png](%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%20%E1%84%8C%E1%85%AE%E1%86%AB%E1%84%87%E1%85%B5%2003ec0f3145fb40099032bc2c96728326/Untitled%207.png)
                
                숫자형 처럼 자동적으로 늘어나는게 없음.
                
    - **Type 추론**
        - 정의
            - 타입스크립트가 코드를 해석해 나가는 동작.
            - 아래와 같이 선언만 하고 따로 타입을 지정하지 않아도 `x` 는 `number` 로 간주됨.
            
            ![%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%20%E1%84%8C%E1%85%AE%E1%86%AB%E1%84%87%E1%85%B5%2003ec0f3145fb40099032bc2c96728326/Untitled%208.png](%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%20%E1%84%8C%E1%85%AE%E1%86%AB%E1%84%87%E1%85%B5%2003ec0f3145fb40099032bc2c96728326/Untitled%208.png)
            
    - **Generic**
        - 정의
            - 제네릭이란 **타입을 마치 함수의 파라미터처럼 사용하는 것**
            
    - **Utility Types**
        
        정의) 이미 정의해 놓은 타입을 변환할 때 사용하기 좋은 타입 문법
        
        참고) 
        
        [Typescript 유틸리티 클래스 파헤치기](https://medium.com/harrythegreat/typescript-%EC%9C%A0%ED%8B%B8%EB%A6%AC%ED%8B%B0-%ED%81%B4%EB%9E%98%EC%8A%A4-%ED%8C%8C%ED%97%A4%EC%B9%98%EA%B8%B0-7ae8a786fb20)
        
        ### Partial Type
        
        Partial<T>
        
        **타입 T의 모든 프로퍼티를 Optional 형태로 바꾸어줍니다.**
        
        예시1)
        
        ```tsx
        interface User {
            name: string;
            age: number;
        }
        
        let user1: User = {name: 'harry', age: 23} //OK
        let user2: User = {age: 23} // 에러발생
        
        let user2: Partial<User> = {age: 23} // OK
        ```
        
        예시 2)
        
        ```tsx
        interface Address {
          email: string;
          address: string;
        }
        
        type MayHaveEmail = Partial<Address>;
        const me: MayHaveEmail = {}; // 가능
        const you: MayHaveEmail = { email: 'test@abc.com' }; // 가능
        const all: MayHaveEmail = { email: 'capt@hero.com', address: 'Pangyo' }; // 가능
        ```
        
        ### Require Type
        
        Require<T>
        
        **모든 Optional 타입들을 언랩핑합니다.**
        
        예시1)
        
        ```tsx
        interface Props {
            a?: number;
            b?: string;
        };
        
        const obj: Props = { a: 5 }; // OK
        
        const obj2: Required<Props> = { a: 5 }; //에러발생
        ```
        
        ### ReadOnly Type
        
        Readonly<T>
        
        **모든 프로퍼티를 값을 참조만 할 수 있도록 바꿉니다.**
        
        예시)
        
        ```tsx
        interface Todo {
          title: string;
        }
        
        const todo: Readonly<Todo> = {
          title: "Delete inactive users",
        };
        
        todo.title = "Hello";
        // Cannot assign to 'title' because it is a read-only property.
        ```
        
        ### Record Type
        
        Record<K,T>
        
        **K타입을 Key값 타입으로, T타입을 밸류 값 타입으로 갖는 타입을 리턴합니다.**
        
        → 주로 K에 유니온 문자열 값을 주어 map 형식의 타입을 만들 수 있고 여러 값들을 원하는 키값에 따라 분류할 때 유용합니다.
        
        예시1)
        
        ```tsx
        export interface Car {
            name: string,
            price: number
        }
        
        const productList: Record<"SONATA" | "AVANTE", Car> = {
            SONATA: {name: "SONATA", price: 10000},
            AVANTE: {name: "SONATA", price: 10000}
        }
        
        const nextProductList: Record<string, Car> = {
            SONATA: {name: "SONATA", price: 10000},
            AVANTE1: {name: "SONATA", price: 10000},
            AVANTE2: {name: "SONATA", price: 10000},
            AVANTE3: {name: "SONATA", price: 10000},
        }
        ```
        
        예시2)
        
        ```tsx
        interface CatInfo {
          age: number;
          breed: string;
        }
        
        type CatName = "miffy" | "boris" | "mordred";
        
        const cats: Record<CatName, CatInfo> = {
          miffy: { age: 10, breed: "Persian" },
          boris: { age: 5, breed: "Maine Coon" },
          mordred: { age: 16, breed: "British Shorthair" },
        };
        ```
        
        ### Pick Type
        
        Pick<T,K>
        
        **T 타입으로부터 K 프로퍼티만 추출합니다.**
        
        예시1)
        
        ```tsx
        interface Todo {
            title: string;
            description: string;
            completed: boolean;
        }
        
        type TodoPreview = Pick<Todo, 'title' | 'completed'>;
        
        const todo: TodoPreview = {
            title: 'Clean room',
            completed: false,
        };
        ```
        
        예시2)
        
        ```tsx
        interface Hero {
          name: string;
          skill: string;
        }
        const human: Pick<Hero, 'name'> = {
          name: '스킬이 없는 사람',
        };
        ```
        
        ### Omit Type
        
        Omit<T,K>
        
        **Pick과는 정반대로 T타입으로부터 K프토퍼티를 제거합니다.**
        
        예시1)
        
        ```tsx
        interface Hero {
          name: string;
          skill: string;
        }
        const human: Pick<Hero, 'name'> = {
          name: '스킬이 없는 사람',
        };
        ```
        
        예시2)
        
        ```tsx
        interface AddressBook {
          name: string;
          phone: number;
          address: string;
          company: string;
        }
        
        const phoneBook: Omit<AddressBook, 'address'> = {
          name: '재택근무',
          phone: 12342223333,
          company: '내 방'
        }
        
        const chingtao: Omit<AddressBook, 'address'|'company'> = {
          name: '중국집',
          phone: 44455557777
        }
        ```
        
    - **Mapped Types**

---

- `React`
    - 정의 / react란 무엇인가?
        - facebook에서 개발한 UI 라이브러리
        - ui 기능만을 제공한다.
    - 특징
        - 전역상태 / 라우팅 등 → 개발자가 직접 설정해야한다.
            - 자유도가 높지만
            - 직접 개발환경을 구축해야한다. → cra로 어느정도 지원해줌.
        - 모든것이 컴포넌트이다.
        - 부모에서 자식으로만 데이터가 전달된다.
    - 왜 사용할까?
        - 자동으로 UI를 업데이트해준다.
            - API 결과 값이나 사용자 이벤트로 프로그램 상태값이 변경된다.
                - 그떄마다 자동으로 업데이트해줌.
    - 장단점
        
        ![%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%20%E1%84%8C%E1%85%AE%E1%86%AB%E1%84%87%E1%85%B5%2003ec0f3145fb40099032bc2c96728326/Untitled%209.png](%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%20%E1%84%8C%E1%85%AE%E1%86%AB%E1%84%87%E1%85%B5%2003ec0f3145fb40099032bc2c96728326/Untitled%209.png)
        
    - 선택이유
        - 팀원들 모두 사용하고 싶어하는 기술
        - 레퍼런스가 많기 때문에 문제 발생 시 해결하기에 보다 용이
        - TypeScript와의 호환성이 좋아 프로젝트 기술 스택에 적합
        - 많은 기업에서 요구하는 기술이라 추후 이직, 취직 시 도움
        - `JSX` , `TSX` 문법이 `HTML` 과 유사하여 편리성 도모.
    
    - **Virtual DOM**
        
        def) 애플리케이션의 `UI`를 구성하는 `HTML` 엘리먼트 를 메모리 내에서 구현한 것
        
        → `DOM` 의 상태를 로컬 메모리에 저장하고 변경 전과 변경 후의 상태를 비교한 뒤 최소한의 내용만 반영하는 기능.
        
        ![%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%20%E1%84%8C%E1%85%AE%E1%86%AB%E1%84%87%E1%85%B5%2003ec0f3145fb40099032bc2c96728326/Untitled%2010.png](%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%20%E1%84%8C%E1%85%AE%E1%86%AB%E1%84%87%E1%85%B5%2003ec0f3145fb40099032bc2c96728326/Untitled%2010.png)
        
        - React는 **실제로 DOM을 제어하는 방식이 아니라** 중간에 가상의 DOM인 Virtual DOM을 두어 개발의 편의성을 높임.
            - 개발자는 직접 DOM을 제어하지 않고 Virtual DOM을 제어하고, React에서 적절하게 Virtual DOM을 DOM에 반영하는 작업을 한다.
            - 비교할때 → `Reconciliation` 작업을 함. (`virtual DOM` 이랑 `DOM` 비교)
            
    - Hooks
        - 훅이란?
            - 함수형 컴포넌트에서 라이프사이클과 state를 관리하기 위한 메소드들
        - `useState`
            - 넘겨주는 인자: `state` 의 초기 값
            - 반환되는 인자: `state` 변수와 이 변수를 갱신할 수 있는 함수.
        - `useEffect`
            - 하는 일: 컴포넌트 렌더링 후에 어떤 일 수행하라고 말함.
            - 첫번째 렌더링하고 나서는 무조건 수행되고, dependency 배열 값에 따라 그 항목이 바뀌면 수행.
            
            ![%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%20%E1%84%8C%E1%85%AE%E1%86%AB%E1%84%87%E1%85%B5%2003ec0f3145fb40099032bc2c96728326/Untitled%2011.png](%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%20%E1%84%8C%E1%85%AE%E1%86%AB%E1%84%87%E1%85%B5%2003ec0f3145fb40099032bc2c96728326/Untitled%2011.png)
            
        - `useCallback`
            - 정의
                
                2번은 `useCallback` , 3번은 `useMemo` 로 예시.
                
                - `useMemo` 와 비슷.
                - 상위컴포에서 하위컴포로 `callback` 함수를 넘겨줄때 그 콜백함수를 `useCallback`  함수로 선언하는게 좋다.
                    
                    → 매번 재선언되면 하위는 그 콜백함수가 달라졌다고 인식하기 때문에.
                    
        - `useMemo`
            - 정의
                - 메모리제이션된 값을 반환한다.
                    
                    ![%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%20%E1%84%8C%E1%85%AE%E1%86%AB%E1%84%87%E1%85%B5%2003ec0f3145fb40099032bc2c96728326/Untitled%2012.png](%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%20%E1%84%8C%E1%85%AE%E1%86%AB%E1%84%87%E1%85%B5%2003ec0f3145fb40099032bc2c96728326/Untitled%2012.png)
                    
                    nested 한 값도 메모이제이션이 되는지?
                    
                    # 구글링할것!
                    
        - `useCallback` 이랑 `useMemo` 는 아래 링크 참고.
            
            @[https://velog.io/@ashnamuh/React의-useReducer-useCallback-useMemo-제대로-알고-사용하기](https://velog.io/@ashnamuh/React%EC%9D%98-useReducer-useCallback-useMemo-%EC%A0%9C%EB%8C%80%EB%A1%9C-%EC%95%8C%EA%B3%A0-%EC%82%AC%EC%9A%A9%ED%95%98%EA%B8%B0)
            
            [https://juicyjerry.tistory.com/148](https://juicyjerry.tistory.com/148)
            
            둘다 최적화할때 쓰인다.
            
            `useCallback` 은 함수를, `useMemo` 는 함수가 반환한 값을 저장시켜 메모리제이션한다.
            
            전자 - 상위컴포가 가지고 있는 콜백함수...
            
            후자 - 상위 컴포가 복잡한 계산 후 props로 A, B 를 내려주면...
            
        
    - `context api`
        
        
    - **Key**
        - react가 어떤 항목을 추가, 변경, 삭제할때 식별할 수 있도록 도움.
        - 고유한 문자열 id를 주는게 좋다.
        - index를 주면 부작용.
            - 추가 / 삭제할때 원치않는 결과 작동 가능.
        
    - `react` 는 언제 렌더링 되냐?
        
        ![%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%20%E1%84%8C%E1%85%AE%E1%86%AB%E1%84%87%E1%85%B5%2003ec0f3145fb40099032bc2c96728326/Untitled%2013.png](%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%20%E1%84%8C%E1%85%AE%E1%86%AB%E1%84%87%E1%85%B5%2003ec0f3145fb40099032bc2c96728326/Untitled%2013.png)
        
    - `react` 라이프 사이클
        - 마운트
            
            ![%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%20%E1%84%8C%E1%85%AE%E1%86%AB%E1%84%87%E1%85%B5%2003ec0f3145fb40099032bc2c96728326/Untitled%2014.png](%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%20%E1%84%8C%E1%85%AE%E1%86%AB%E1%84%87%E1%85%B5%2003ec0f3145fb40099032bc2c96728326/Untitled%2014.png)
            
        - 업데이트
            
            ![%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%20%E1%84%8C%E1%85%AE%E1%86%AB%E1%84%87%E1%85%B5%2003ec0f3145fb40099032bc2c96728326/Untitled%2015.png](%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%20%E1%84%8C%E1%85%AE%E1%86%AB%E1%84%87%E1%85%B5%2003ec0f3145fb40099032bc2c96728326/Untitled%2015.png)
            
        - 언마운트
            - `componentWillUnmount`
        
    
- `SPA`
    - 정의
        - `Single Page Application` 의 약어.
        - 말 그대로 페이지가 1개인 어플리케이션. / 어떤 행동(클릭) 하면 전체 페이지가 로딩되지 **않고** 현재 페이지에서 데이터만 바뀌는 것.
        - 기존의 방법은 다음과 같았음.
            
            ### MPA
            
            - 웹 페이지가 **여러 페이지**로 구성되어 있었음.
            - 유저가 요청할 때 마다 페이지가 새로고침 되며, 서버로부터 리소스를 받음.
                
                → 웹에서 제공하는 정보가 너무 많아 속도적인 문제가 있었음.
                
                → 렌더링을 서버쪽에서 담당한다는 뜻은 그만큼 렌더링 시 서버 자원이 많이 사용되고 불필요한 트래픽 낭비가 된다는 것.
                
        - 이를 해결하려면 하나의 웹 페이지가 여러개의 페이지를 보여줘야 함.→ `Routing` 필요.
        - `react` 에는 이 기능이 내장되어 있지 않아 서드파티 라이브러리인 `react-router` 사용.
    - 단점
        - 앱 규모가 커지만 JS 파일 사이즈가 너무 커짐. (첫 로딩이 느림)
            
            → 페이지 로딩 시 사용자가 실제로 방문하지 않을 수도 있는 페이지의 스크립트도 불러옴.
            
            → `Code Splitting` 를 사용하면 해결하지만, 아직 써본적은 없음.
            
        - SEO 에 불리함.  Search Engine Optimization
            - CSR는 server가 비어있는 `HTML` 를 응답하고 client가 화면을 그리는데, 검색엔진은 `HTML` 을 기반으로 검색이 되므로.
    - `NEXT.js` ?
        - 사용자가 처음 페이지 들어왔을때 → 서버에서 리소스 받아 렌더링. (SSR)
        - 그 다음 라우팅은 CSR 방식.
        - CSR 가 가지고 있는 SEO 문제 → SSR 제공으로 향상
    
    - `useHistory` 로 페이지 이동.
        
        ![%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%20%E1%84%8C%E1%85%AE%E1%86%AB%E1%84%87%E1%85%B5%2003ec0f3145fb40099032bc2c96728326/Untitled%2016.png](%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%20%E1%84%8C%E1%85%AE%E1%86%AB%E1%84%87%E1%85%B5%2003ec0f3145fb40099032bc2c96728326/Untitled%2016.png)
        
    - `useLocation` 으로 `history.push` 로 받은 인자 관리.
    - `useParams` 으로 URL `:~` ~부분 추출.
    
    - `URL 파라미터` : 특정 아이디나 이름으로 조회시 사용
- Babel
    
    ### Babel 이란 무엇인가?
    
    - 초기 ES6 문법을 ES5로 변환해주는 용도로 쓰임.
    - or 코드에서 주석을 제거하거나 압축하는 용도로 쓰이기도 함.
- **CSS**
    
    ### display: inline
    
    예시) span
    
    text 크기 만큼 공간 점유, 줄바꿈 하지 않음.
    
    width, height 적용 불가.
    
    margin, padding 적용 불가.
    
    ### display: block
    
    예시) div
    
    무조건 한줄 점유.
    
    ### display: inline-block
    
    inline 처엄 줄바꿈하지 않고 가로로 길게 배치 가능.
    
    하지만 width, height 적용 가능.
    
    ### 요소를 렌더링 되지 않게 되고 싶다. 방법과 그 차이들은?
    
    ![Untitled](%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%20%E1%84%8C%E1%85%AE%E1%86%AB%E1%84%87%E1%85%B5%2003ec0f3145fb40099032bc2c96728326/Untitled%2017.png)
    
    ### box-sizing 속성에 대해서 아는것이 있나?
    
    content-box: 
    
    border-box: 
    

---

### 포트폴리오 기반 질문

- **간단하게 자기 소개 부탁드려요**

- **C++을 하다가 프론트로 전향하게 된 계기가 있으신가요?**
    
    4년 컴공을 다니며 다뤘던 언어는 C++. 정해진 커리큘럼만을 따라갔고 / 덜컥 취직을 했었다.
    
    회사를 다니다보니까 내가 정말 만들어보고 싶거나 / 서비스 하고 싶었던 부분을 한번도 생각하지 못했어서, 과감히 퇴사. 
    
    - **궁금한 점은 그럼 어떻게 해결하시나요?**
        
        구글링을 통해서 해결. / 정리하고 싶은 내용은 블로그에 적는다.
        
        +) 코어 자바스크립트 스터디 진행중.
        

- **Atomic Design Pattern에 대해 소개해주세요.**
    
    정의) 컴포넌트 관리(디자인 시스템) 방법론이다.
    
    디자인 요소들을 나누어 파악하고 이 요소들이 조합되는 과정을 통해서 디자인을 구성하는 방식.
    
    **컴포넌트 중심의 디자인 패턴**
    
    - **아토믹 디자인 패턴을 사용하면 재활용성이 높아지나요?**
        
        장점
        
        간단 명료하다.
        
        Atom, molecules, organism, Template, pages 로 컴포넌트들을 분류하고, 하위 컴포넌트들이 합쳐져 상위 컴포넌트로 완성되는 구조.
        
        중복되는 컴포넌트를 줄일 수 있다.
        
    - **아토믹 디자인 패턴의 단점은 무엇인가요?'**
        - 컴포넌트에 대한 이해도가 필요하다.
        - 각자 개인마다 컴포넌트 단위를 나누는 기준이 달라 모호하다.
        - 초기 설정 및 러닝 커브가 높다.
    - **느슨한 결합이 되면 뭐가 좋나요?**
        
        정의) 컴포넌트들끼리 서로 의존성이 줄어든 상태.
        
        장점) 유연성과 재사용성을 높일 수 있다. 변경사항을 강한 결합보다 쉽게 적용할 수 있다.
        
        - **컴포넌트 간 통신이 필요하게 될 수도 있을텐데 이 경우 컴포넌트 간에 통신은 어떻게 진행할 수 있을까요?**
            
            간단할때는 콜백함수로 통신 가능.
            
            Context API
            

- **가장 자신있는 프로젝트 하나 소개해주세요.**
    
    게임 플릭스
    
    - **왜 그 기술 스택을 사용하셨나요?**
        1. **typescript**
            1. 사전 에러 핸들링이 편하다.
            2. undefined 오류를 방지할 수 있다.
            3. 원래 타입 지정 언어를 선호.
        2. **react**
            1. tsx 문법이 html과 비슷해 알아보기 쉽다.
            2. atomic design 을 적용하기 최적화된 라이브러리.
        3. **Nextjs**
            1. SSR를 위해. / SEO 를 위해.
        4. **SWR**
            1. 프로젝트 특성상 Get 메소드가 많은데, 거기에 최적화 됨.
            2. 전역 상태 관리를 딱히 할

- **웹 소켓에 대해서 설명해주세요.**
    - 참고문헌
        
        [https://velog.io/@wldus9503/네트워크-Network3.-WebSocket-웹-소켓에-대해서](https://velog.io/@wldus9503/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-Network3.-WebSocket-%EC%9B%B9-%EC%86%8C%EC%BC%93%EC%97%90-%EB%8C%80%ED%95%B4%EC%84%9C)
        
    
    정의) **서버와 클라이언트 간에 Socket Connection을 유지해서 언제든 양방향 통신 또는 데이터 전송이 가능하도록 하는 기술**
    
    Websocket 은 웹 상에서 HTTP환경에서 양방향 통신을 지원하는 프로토콜.
    
    HTTP 기반으로 handshake 가 일어나지만 HTTP와는 다른 방식.
    
     **HTTP는 접속 유지하지 않고, 한방향으로만 통신이 가능.**
    
    서버 - 클라이언트 웹소켓 연결을 HTTP 프로토콜을 통해 이루어짐.
    
    서버에 소켓 연결되면 3way handshake통해 TCP 세션 생성.
    
    handshake 하고 연결 유지함.
    
    - **소켓은 어떤식으로 동작하나요?**
        - TCP와 UDP의 차이가 무엇인가요?
            - 참고문헌
                
                [https://velog.io/@hidaehyunlee/TCP-와-UDP-의-차이](https://velog.io/@hidaehyunlee/TCP-%EC%99%80-UDP-%EC%9D%98-%EC%B0%A8%EC%9D%B4)
                
            
            두 개념은 TCP/IP 의 전송계층에서 사용되는 프로토콜이다.
            
            전송계층이란) IP에 의해 전달되는 패킷의 오류를 검사하고 재전송 요구등 제어담당.
            
            ### TCP
            
            Transmission Control Protocol
            
            - 신뢰성이 요구되는 애플리케이션에서 사용.
            - 신뢰성 보장 / 안정적 / 순서대로 / 에러 없이.
            
            **TCP Connection (3-way handshake)**
            
            1. 먼저 open()을 실행한 클라이언트가 `SYN`을 보내고 `SYN_SENT` 상태로 대기한다.
            2. 서버는 `SYN_RCVD` 상태로 바꾸고 `SYN`과 응답 `ACK`를 보낸다.
            3. `SYN`과 응답 `ACK`을 받은 클라이언트는 `ESTABLISHED` 상태로 변경하고 서버에게 응답 `ACK`를 보낸다.
            4. 응답 `ACK`를 받은 서버는 `ESTABLISHED` 상태로 변경한다.
            
            **TCP Disconnection (4-way handshake)**
            
            1. 먼저 close()를 실행한 클라이언트가 FIN을 보내고 `FIN_WAIT1` 상태로 대기한다.
            2. 서버는 `CLOSE_WAIT`으로 바꾸고 응답 ACK를 전달한다. 동시에 해당 포트에 연결되어 있는 어플리케이션에게 close()를 요청한다.
            3. ACK를 받은 클라이언트는 상태를 `FIN_WAIT2`로 변경한다.
            4. close() 요청을 받은 서버 어플리케이션은 종료 프로세스를 진행하고 `FIN`을 클라이언트에 보내 `LAST_ACK` 상태로 바꾼다.
            5. FIN을 받은 클라이언트는 ACK를 서버에 다시 전송하고 `TIME_WAIT`으로 상태를 바꾼다. `TIME_WAIT`에서 일정 시간이 지나면 `CLOSED`된다. ACK를 받은 서버도 포트를 `CLOSED`로 닫는다.
            
            ### UDP
            
            User Datagram Protocol
            
            - 간단한 데이터를 빠른 속도로 전송하고자 하는 애플리케이션에서 사용.
            - 비 연결형 프로토콜
            - BroadCast, Multicast.

- **git rebase와 git merge에 차이는 무엇인가요?**
    
    git rebase
    
    어떤 특정 브랜치를 base로 커밋 이력을 재정렬하겠다.
    
    사용이유) 히스토리 깔끔하게 유지하기 위해.
    
    git merge
    
    말 그대로 합치는 명령어. 보통 master / develop 에서 sub branch를 merge한다.
    

- **SWR, Context API에 대해 소개해주세요.**
    
    ### SWR
    
    정의) 원격데이터 fetch를 위한 커스텀 훅 npm 모듈
    
    **기본 골격**
    
    ```tsx
    const {data, error, revalidate, mutate} = useSWR(주소, fetcher)
    ```
    
    > fetcher 함수: 주소를 어떻게 처리할건지. 주소를 fetcher로 넘겨준다.
    > 
    
    > loading 상태 알 수 있다: data가 존재하지 않으면 loading 중.
    > 
    - 특징
        - 자동으로 다시 요청. 일정 시간 지나면 자동 재요청. (deduping Interval 인자주면 그 숫자 내에서는 캐시 사용.)
        - revalidate
            - 서버에 다시 요청 보내서 data 가져오는것.
        - mutate
            - 요청 안보내고 데이터를 수정. useState 의 set처럼.
    
    ### Context api
    
    정의) 전역적으로 데이터를 공유할 수 있도록 고안된 방법
    
    ```tsx
    const MessageContext = React.createContext('hello')
    ```
    
    위처럼 context 선언.
    
    provider / consumer
    
    provider / useContext
    

- **NextJS를 활용하면 어떻게 SEO에 최적화가 되나요?**
    
    첫 화면은 SSR를 활용하기 때문에 웹 크롤러가 빈 HTML가 아닌 내용이 이미 있어서 크롤링 됨.
    
    - **SEO 최적화 방법은 뭐가 있나요?**
        1. 문법에 맞는 HTML 작성.
            1. `title` 태그에 사이트 제목
            2. 구체적으로 간결하게 구성 - `사이트 이름 - 나머지 제목`
        2. 메타 태그 활용.
            
            ```html
            <meta name=”keywords” content = “키워드 1, 키워드 2″>
            <meta name = “description” content = “페이지 내용을 정리한 소개 글(검색 결과 프리뷰로 나타나는 영역)”>
            ```
            
        3. `img` 태그에 `alt` 속성 사용.
            1. 검색 엔진이 이미지 발견하면 `alt` 속성값 읽어서 인덱싱 작업함.

- **OAuth가 무엇인가요?**
    
    정의) 특정 애플리케이션이 다른 애플리케이션의 정보에 접근할 수 있는 권한을 관리하는 프로토콜.
    
    - 참고 문헌은 여기.
        
        [https://velog.io/@panther222128/OAuth-2.0-생활코딩-강의-필기](https://velog.io/@panther222128/OAuth-2.0-%EC%83%9D%ED%99%9C%EC%BD%94%EB%94%A9-%EA%B0%95%EC%9D%98-%ED%95%84%EA%B8%B0)
        

- **HongIT 프로젝트에서 생산성을 높이기 위한 아키텍처로 어떤 아키텍처를 사용했나요?**

- **SPA가 무엇인가요?**
    - **MPA와 비교했을 때 장단점은 무인가요?**
        
        

- **JWT는 무엇인가요?**
    
    Json Web Token 약자로 모바일이나 웹의 사용자 인증을 위해 사용하는 암호화된 토큰
    
    - header: token의 타입과 signature에서 사용한 해싱 알고리즘
    - payload: 토큰 data
    - signature: 토큰을 인코딩하거나 / 유효성 검증에 필요한 암호화 코드.
    - **JWT은 어떻게 동작하나요?**

- **5년뒤, 10년뒤 개발자로서 계획이 있나요?**
    
    

- **팀에 불화가 생겼을 때 어떻게 대처하시나요?**
    
    갈등
    

### CS 지식

- 데드락
    
    정의) 한정된 자원을 여러 프로세스가 사용하고자 할 때 발생하는 상황
    
    `Deadlock` 를 일으키는데에는 **4가지 필요조건**이 있다.
    
    1. `Mutual Exclusion` - 상호배제.
        - 프로세서들이 자원을 배타적으로 점유한다.
        - 즉, **남 안주고 나만 쓴다.**
    2. `Hold and wait` - 점유와 대기.
        - 이미 어떤 자원을 점유하고 있으며, 다른 자원을 요구함.
    3. `No preemption` - 비선점.
        - 프로세스가 자원을 점유하는 동안 뺏을 수 없음
    4. `Circular Wait` - 환형대기.
        - 프로세스와 자원이 원형을 이루며, 각 프로세스는 내 자원을 가지고 있는 상태에서 상대방 프로세스의 자원을 요구.
    
    해결 방법
    
    - 예방
    - 회피
    - 탐지
    - 무시
    
- RESTful API
    
    `REST` 란, `REpresentational State Transfer` 의 약자이다. 
    
    정의) HTTP 통신에서 어떤 자원에 대한 `CRUD` 요청을 `Resource` 와 `Method` 로 표현하여 특정한 형태로 전달하는 방식.
    
    ![%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%20%E1%84%8C%E1%85%AE%E1%86%AB%E1%84%87%E1%85%B5%2003ec0f3145fb40099032bc2c96728326/Untitled%2018.png](%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%20%E1%84%8C%E1%85%AE%E1%86%AB%E1%84%87%E1%85%B5%2003ec0f3145fb40099032bc2c96728326/Untitled%2018.png)
    
    → **API 설계의 중심에 자원(Resource)이 있고 HTTP Method 를 통해 자원을 처리하도록 설계.**
    
- 라이브러리와 프레임워크 차이점
    
    ![%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%20%E1%84%8C%E1%85%AE%E1%86%AB%E1%84%87%E1%85%B5%2003ec0f3145fb40099032bc2c96728326/Untitled%2019.png](%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%20%E1%84%8C%E1%85%AE%E1%86%AB%E1%84%87%E1%85%B5%2003ec0f3145fb40099032bc2c96728326/Untitled%2019.png)
    
- 자료구조
    - 스택: 세로로 된 바구니와 같은 구조로 먼저 넣게 되는 자료가 마지막으로 나오게 되는 First-In Last-Out(FILO) 구조이다. → **DFS**
    - 큐: 가로로 된 통과 같은 구조로 먼저 넣게 되는 자료가 가장 먼저 나오는 First-In First-Out(FIFO) 구조이다. → **BFS**
    - 트리: 정점과 간선을 이용해 사이클을 이루지 않도록 구성한 Graph의 특수한 형태로, 계층이 있는 데이터를 표현하기에 적합하다.
    - 힙: 최댓값 또는 최솟값을 찾아내는 연산을 쉽게 하기 위해 고안된 구조로, 각 노드의 키값이 자식의 키값보다 작지 않거나(최대힙) 그 자식의 키값보다 크지 않은(최소힙) 완전이진트리이다.
    - 해시: 해시 테이블은 (Key, Value)로 데이터를 저장하는 자료구조 중 하나로 빠른 데이터 검색이 필요할 때 유용합니다. 해시 테이블은 Key값에 해시함수를 적용해 고유한 index를 생성하여 그 index에 저장된 값을 꺼내오는 구조입니다.
- 알고리즘
    - Arraylist vs LinkedList
        
        **ArrayList**
        
        - get, set : O(1) → **Random Access**가 가능하다.
        - add, remove
            - 맨 뒤: O(1)
            - 맨 앞, 그 외: O(n)
        
        **LinkedList**
        
        - get, set: O(n) - 하나하나 접근해야하기 때문.
        - add, remove - O(1)
    - DFS
        
        깊이 우선 탐색. → 그래프 탐색 알고리즘 중의 하나.
        
        - 정점의 자식들을 먼저 탐색하는 방식
        
        **시간복잡도**
        
        인접 행렬 - O(n^2)
        
        인접 리스트 - O(V+E)
        
    - BFS
        
        너비 우선 탐색. → 그래프 탐색 알고리즘 중의 하나.
        
        - 형제 노드들을 먼저 탐색하는 방식
        
        **시간복잡도**
        
        인접 행렬 - O(n^2)
        
        인접 리스트 - O(V+E)
        
    - Sorting
        - Bubble Sort
            
            하나하나 비교해서 자리 바꾸는것.
            
            **시간복잡도**
            
            O(n^2)
            
        - Quick sort
            
            Divide and conquer. 
            
            pivot을 정하고, pivot 보다 작은 애들은 왼쪽으로, 큰애들은 오른쪽으로, 그리고 그 피봇의 위치는 확정.
            
            divide 해서 recursion.
            
            [https://www.youtube.com/watch?v=cWH49IKDIiI](https://www.youtube.com/watch?v=cWH49IKDIiI)
            
            **시간복잡도**
            
            피벗을 선정하는 방법에 따라 속도가 달라짐. nlogn
            
        - Merge sort
            
            가장 작은 단위로 쪼갠 다음, 소팅하며 병합한다. 
            
            **시간복잡도**
            
            1개짜리로 자르는건 //2 가 계속되므로 log2n 이고
            
            합병하는 건 모든 원소를 비교해야하므로 n.
            
            → **nlog2n**.
            
        
- 메모리 구조
    
    
    ![%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%20%E1%84%8C%E1%85%AE%E1%86%AB%E1%84%87%E1%85%B5%2003ec0f3145fb40099032bc2c96728326/Untitled%2020.png](%E1%84%86%E1%85%A7%E1%86%AB%E1%84%8C%E1%85%A5%E1%86%B8%20%E1%84%8C%E1%85%AE%E1%86%AB%E1%84%87%E1%85%B5%2003ec0f3145fb40099032bc2c96728326/Untitled%2020.png)
    
    - 코드 영역
        
        코드 자체를 구성하는 메모리 영역으로 Hex파일이나 BIN파일 메모리.
        
    - 데이터 영역
        
        프로그램의 전역 변수(global)와 정적 변수(static)가 저장되는 영역
        
        초기화 된 데이터는 data 영역에 저장됨.
        
    - bss 영역
        
        초기화 되지 않은 데이터는 BSS (Block Stated Symbol) 영역에 저장된다
        
    - 힙 영역
        
        프로그래머가 직접 관리할 수 있는 메모리 영역으로 이 공간에 메모리를 할당하는 것을 동적 할당이라고 함.
        
    - 스택 영역
        
        함수의 호출과 함께 할당되며 지역 변수와 매개 변수가 저장되는 영역
        
        지역(local) 변수, 매개변수(parameter), 리턴 값 등 잠시 사용되었다가 사라지는 데이터를 저장하는 영역
        
    - `Call by Value` vs `Call by Reference`
        
        > 함수가 호출될때, **매개변수를 어떻게 넣어줄건지**에 대한 개념.
        > 
        - **Call by Value**
            
            인자로 받은 값을 **복사하여** 처리를 한다.
            
            장점) 복사하여 처리하기 때문에 안전하다. 원래의 값이 보존이 된다.
            
            단점) 복사를 하기 때문에 메모리가 사용량이 늘어난다.
            
        - **Call by Reference**
            
            인자로 받은 값의 **주소를 참조하여 직접 값에 영향**을 준다.
            
            장점) 복사하지 않고 직접 참조를 하기에 빠르다.
            
            단점) 직접 참조를 하기에 원래 값이 영향을 받는다.(리스크)
            
    
    - `parameter` 와 `argument` 의 차이
        - Parameter: 함수를 선언할 때 사용된 변수
        - Argument: 함수가 호출되었을 때 함수의 파라미터로 전달된 실제 값
    
