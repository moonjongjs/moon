# JSON 데이터 fetch() &  axios() API 구현하기
아파치톰켓서버 => ORACLE + JAVA + JSP & SERVLET(서블릿) => JSON => 웹페이지에전송
아파치톰켓서버 => MYSQL + JAVA + JSP & SERVLET(서블릿) => JSON => 웹페이지에전송
윈도우NT서버 => MSSQL + ASP & 닷넷 => JSON => 웹페이지에전송
아파치웹서버 => MYSQL + PHP => JSON => 웹페이지에전송

# JSON 데이터 분석 설계 제작
- [pulic]
     [json]
        {}notice.json
        {}slide.json

1. 공지사항(notice) [{},{},{},{}]
    - 글제목
    - 글내용
    - 작성날짜
```JSON
    // notice.json
    {
        "공지사항": [
            {"글번호":1,"글제목":"모든 스타벅스 카드의 자동 충전 서비스가 종료되는 것이 아닌 일부 결제 대행사를 통한 결제 서비스의 제공이 종료되는 것으로, 스타벅스 앱을 통하여 자동 충전을 다시 설정하시면 서비스 종료일 이후에도 자동 충전 기능 사용이 가능합니다. 즐거운(스마일콘) 시스템 점검 안내 페이스북 공유하기 새창","글내용":"모든 스타벅스 카드의 자동 충전 서비스가 종료되는 것이 아닌 일부 결제 대행사를 통한 결제 서비스의 제공이 종료되는 것으로, 스타벅스 앱을 통하여 자동 충전을 다시 설정하시면 서비스 종료일 이후에도 자동 충전 기능 사용이 가능합니다. 즐거운(스마일콘) 시스템 점검 안내 페이스북 공유하기 새창 온라인 전자결제대행사(스마트로)와의 계약 종료로 인하여, 일부 스타벅스 카드 자동 충전 서비스가 2024년 12월 15일까지만 제공될 예정임을 안내 드립니다.","작성날짜":"2024-12-23"},
            {"글번호":2,"글제목":"즐거운의 시스템 점검으로 인해 스마일콘에서 발행된 스타벅스 모바일 상품권 사용이 일시적으로 제한됩니다.","글내용":"즐거운의 시스템 점검으로 인해 스마일콘에서 발행된 스타벅스 모바일 상품권 사용이 일시적으로 제한됩니다. 즐거운의 시스템 점검으로 인해 스마일콘에서 발행된 스타벅스 모바일 상품권 사용이 일시적으로 제한됩니다.","작성날짜":"2024-12-21"},
            {"글번호":3,"글제목":"스마트로 PG(전자결제대행사)를 통한 일부 자동 충전 서비스 종료 사전 안내 페이스북 공유하기 새창","글내용":"스마트로 PG(전자결제대행사)를 통한 일부 자동 충전 서비스 종료 사전 안내 페이스북 공유하기 새창 사이렌 오더/딜리버스 음료 기본 설정 변경 안내 (ICED → HOT) 페이스북 공유하기 새창 스마트로 PG(전자결제대행사)를 통한 일부 자동 충전 서비스 종료 사전 안내 페이스북 공유하기 새창 사이렌 오더/딜리버스 음료 기본 설정 변경 안내 (ICED → HOT) 페이스북 공유하기 새창","작성날짜":"2024-12-19"},
            {"글번호":4,"글제목":"온라인 전자결제대행사(스마트로)와의 계약 종료로 인하여, 일부 스타벅스 카드 자동 충전 서비스가 2024년 12월 15일까지만 제공될 예정임을 안내 드립니다.","글내용":"온라인 전자결제대행사(스마트로)와의 계약 종료로 인하여, 일부 스타벅스 카드 자동 충전 서비스가 2024년 12월 15일까지만 제공될 예정임을 안내 드립니다. 온라인 전자결제대행사(스마트로)와의 계약 종료로 인하여, 일부 스타벅스 카드 자동 충전 서비스가 2024년 12월 15일까지만 제공될 예정임을 안내 드립니다.","작성날짜":"2024-12-17"}
        ]
    }
```


# Section3Component.jsx
1-1 공지글 전체 객체로 생성해서 보내기

  
  ```JS
    // 모달창 열기 클릭 이벤트 
    const onClickModalOpen=(e, 공지글)=>{
        e.preventDefault();
        // 5. 모달창열기 구현 => 데이터 전송
        // 공지글 => 글번호, 글제목, 글내용, 작성날짜, 모달 true
        // 리덕스 => modal 리듀서 전송 객체
        const notice = {
            글번호: 공지글.글번호,
            글제목: 공지글.글제목,
            글내용: 공지글.글내용,
            작성날짜: 공지글.작성날짜,
            모달: true
        }
        dispatch(mainModalAction(notice));
    }
```


# [store]  modal.js
1-2 리듀서 확인 console.log();
```JS
    mainModalAction(state, action){ 
        state.mainModal = action.payload.모달;
        state.글번호 = action.payload.글번호;
        state.글제목 = action.payload.글제목;
        state.글내용 = action.payload.글내용;
        state.작성날짜 = action.payload.작성날짜;

        console.log(  'action.payload' )
        console.log(  action.payload )
        console.log(  action.payload.글번호 )
        console.log(  action.payload.글제목 )
        console.log(  action.payload.글내용 )
        console.log(  action.payload.작성날짜 )
        console.log(  state )
    },

```

#  ModalComponent.jsx
1-3. 모달창에 글제목, 직상날짜, 글내용 바인딩 하기





2. 갤러리(Gallery) [{},{},{}]
    - 글번호
    - 이미지
    - 이미지설명
```JSON
    // gallery.json
    {
        "갤러리": [
            {"글번호":1,"이미지":"./images/gallery1.jpg","이미지설명":"마을과 전경 이미지"},
            {"글번호":2,"이미지":"./images/gallery2.jpg","이미지설명":"마을과 뒷산 이미지"},
            {"글번호":3,"이미지":"./images/gallery3.jpg","이미지설명":"마을과 호수 이미지"}
        ]
    }
```

2-1 갤러리 JSON 데이터 fetch()  API로 가져오기 => 상태관리에 저장

2-2 상태관리 갤러리 데이터 JSX 바인딩하기




# Section1Component.jsx
3. 섹션1 슬라이드 
```JSON
    // main_slide.json
    {
        "메인슬라이드": [
            {"글번호":1,"클래스":"slide3 last", "이미지":"./images/slide3.jpg", "타이틀":"푸른마을 이미지 슬라이드3"},
            {"글번호":2,"클래스":"slide1",      "이미지":"./images/slide1.jpg", "타이틀":"푸른마을 이미지 슬라이드1"},
            {"글번호":3,"클래스":"slide2",      "이미지":"./images/slide2.jpg", "타이틀":"푸른마을 이미지 슬라이드2"},
            {"글번호":4,"클래스":"slide3",      "이미지":"./images/slide3.jpg", "타이틀":"푸른마을 이미지 슬라이드3"},
            {"글번호":5,"클래스":"slide1 first","이미지":"./images/slide1.jpg", "타이틀":"푸른마을 이미지 슬라이드1"}
        ]
    }
```


# Section2Component.jsx
4. 섹션2 배너
```JSON
    // section2.json
    {
        "section2": {
            "글번호":1,
            "타이틀":"Lorem ipsum dolor sit amet consectetur adipisicing elit.", 
            "내용":"Illum placeat ipsa eos neque illo, voluptates excepturi modi molestiae nostrum accusamus cum corporis? Dolorem praesentium facilis enim reiciendis aut tempora provident corporis, voluptatibus quidem minima ea fuga, quam distinctio!", 
            "이미지":"./images/banner.jpg"
        }
    }
```

# Section1Component.jsx
5. 섹션1 링크 바로가기
```JSON
    // section1.json
    {
        "section1": [
            {"글번호":1, "타이틀":"link1", "이미지":"./images/link1.jpg"}
            {"글번호":2, "타이틀":"", "이미지":""}
            {"글번호":3, "타이틀":"link2", "이미지":"./images/link1.jpg"}
            {"글번호":4, "타이틀":"", "이미지":""}
            {"글번호":5, "타이틀":"link3", "이미지":"./images/link1.jpg"}
        ]
    }
```

```JS
 useEffect(()=>{
        // 0 1 2 3 4
        // 0  2  4 => 나머지 0
        // 1 3  => 나머지 1
        // idx % 2 연산 JSX 출력시 버블링 발생
        // link.바로가기.map((item, idx)=>
        //     idx % 2 === 1 ?  console.log("2행, 4행 " + idx )  : console.log( "1행 3행 5행" + idx )  
        // );

        
        // 중괄호 있는 리턴문 사용 형식은
        // if 문사용 가능
        // 그러나 반드시 리턴문 사용
        link.바로가기.map((item, idx)=>{
            if(item.타이틀!==""){
                return console.log("idx = 0, 2, 4"  + idx + " " + item.이미지 ) // 0 2 4
            }
            else {
                return console.log("idx = 1, 3"  + idx + " " + item.이미지 ) // 1, 3
            }
        })            


        // 중괄호 없는 즉시리턴 형식은
        // 3항연산자 사용
        // if 문사용 안된다.
        link.바로가기.map((item, idx)=>
            item.타이틀!=="" ?
                console.log("idx = 0, 2, 4"  + idx + " " + item.이미지 ) // 0 2 4
            :            
                console.log("idx = 1, 3"  + idx + " " + item.이미지 ) // 1, 3            
        )
            
        


    }, [link.바로가기]);

```


# HeaderComponent.jsx
6. 헤더 네비게이션(Navigation) 메인메뉴 & 서브메뉴
네비게이션 => 메인메뉴 => 서브메뉴[4]

```JSON
    // nav.json
    {        
        "네비게이션": {
            "메인메뉴": {
                "OnSale": [
                    ["메인1서브","OnSale","할인행사"],
                    ["봄 먹거리","여름 먹거리","가을 먹거리","겨울 먹거리"],
                    ["메인요리","밑반찬","간식","브런치"],
                    ["신규매장","추천매장","공지사항"]
                ],
                "기획전": [
                    ["메인2서브", "기획전", "신상품"],
                    ["아동복", "자켓", "팬츠","장남감"],
                    ["신규매장", "추천매장", "공지사항"]
                ], 
                "푸른마을 레시피": [
                    ["메인3서브","푸른마을 레시피","베스트"],
                    ["남성의류","자켓","팬츠","운동복"],
                    ["메인요리","밑반찬","간식","브런치"]
                ],
                "매장안내": [
                    ["메인4서브","매장안내","알뜰상품"],
                    ["여성의류","상의","팬츠","레깅스"]
                ]
            }
        }
    }
```


```JS
  // 메인메뉴 바인딩 테스트
    useEffect(()=>{        
        console.log( state.메인메뉴 )
        // 메인메뉴 만 출력
        // 반복문 for of 배열

        // 1. 메인메뉴만 출력 방법
        //    JSX 에서 적하지 않다.
        // 반복문 for in 객체
        for (let item in  state.메인메뉴) {
            console.log( item);
        }
        // 출력
        /*
          OnSale
          기획전
          푸른마을 레시피
          매장안내
        */

        // 객체를 지정하는 방식
        // . 점표기법 => 공백이 포함안된상태만 가능
        // [''] 대괄호 표기법 => 공백이 포함된 상태도 가능
        console.log( state.메인메뉴.OnSale ); // 자식요소 배열 모두 점표기
        console.log( state.메인메뉴.기획전 ); // 자식요소 배열 모두  점표기
        console.log( state.메인메뉴['푸른마을 레시피']); // 자식요소 배열 모두  [] 표기
        console.log( state.메인메뉴['매장안내'] ); // 자식요소 배열 모두 

        // 2. 객체(Object)의 키(keys), 밸류(values), 엔트리(entries)
        console.log(  Object.keys(state.메인메뉴) ); // => 키 배열로 출력
        // (4) ['OnSale', '기획전', '푸른마을 레시피', '매장안내']

        console.log(  Object.values(state.메인메뉴) ); // => 값 배열로 출력        
        // (4) [Array(4), Array(3), Array(3), Array(2)]

        console.log(  Object.entries(state.메인메뉴) ); // => 키: 밸류 한쌍 출력 []
        // Array(2), Array(2), Array(2), Array(2)]

        // 2. 객체를 배열로 생성해서 map() 함수 사용
        //  Object.keys(state.메인메뉴) 결과가 배열로 출력 
        Object.keys(state.메인메뉴).map((item, idx)=>{
            return console.log( idx,  item); // 인덱스번호, 메인메뉴
        });

        // 3. 각 메인메뉴에 서브메뉴를 출력하라
        //    최종 JSX 데이터 바인가능한 형태가 만들어 졌다
        //    인덱스번호, 메인메뉴, 서브메뉴[], 서브메뉴[] 배열 길이
        Object.keys(state.메인메뉴).map((item, idx)=>{
            return console.log( idx,  item,  state.메인메뉴[item], state.메인메뉴[item].length );
        });


    },[state.메인메뉴])

```


```JSX

<ul onMouseLeave={onMouseLeaveMainBtn}>
{ 
// ['메인메뉴1', '메인메뉴2', '메인메뉴3', '메인메뉴4'].map()
    Object.keys(state.메인메뉴).map((item, idx)=>                                                            
        <li key={item}>
            <a href="!#" className="main-btn" title="OnSale"  onMouseEnter={(e)=>onMouseEnterMainBtn(e, idx)} >{item}</a>
            {
                sub[idx] &&     
                <div className="sub sub1">
                    <ul>
                        {
                        state.메인메뉴[item].map((item2, idx2)=>
                            <li key={idx2}> {/*  줄 */}
                            {               
                                item2.map((item3, idx3)=>
                                    <span key={idx3}> {/*  칸 */}
                                        <a href="!#">{item3}</a>
                                    </span>   
                                )
                            }
                            </li>
                        )     
                        }
                    </ul>
                </div>
            }
        </li>            
    )    
}
</ul>

```