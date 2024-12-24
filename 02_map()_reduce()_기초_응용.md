# map() reduce() 기초 응용

```JS
    // 리듀스    map(     item, idx, arr) 함수 사용하기
    // 리듀스 reduce(acc, item, idx, arr) 함수 사용하기
    // 리듀스 reduce(누산기 acc 어큐믈레이터 연산결과저장, item, idx, arr) 함수 사용하기
    let arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
    let sum = arr.reduce((acc, item)=> acc + item, 0);
    // 0 + 1 = 1 acc
    // 1 + 2 = 3 acc
    // 3 + 3 = 6 acc
    // 6 + 4 = 10 acc
    // :
    // 45 + 10 = 55 acc

    console.log( ' 리듀스 reduce(acc, item, idx, arr) 함수 사용하기' );
    console.log(  sum );

    // reduce() 사용 배열을 객체로 변환하기
    console.log( cookieArr );
    // [ 'MAIN_MODAL1 = green_1234_close' ]
    /*
        [ 
            {
                이름: 'MAIN_MODAL1',
                값 : 'green_1234_close'
            }
        ]
    */
    // 리턴문 없으면 소괄호로 감싼다.
    let result = cookieArr.reduce((acc, item)=> ([...acc, {이름: item.split('=')[0],값: item.split('=')[1]}]), []);
    console.log( 'reduce => 배열을 객체로 변환 ' );
    console.log( result );

    // map() 반복문, 계산,...배열처리
    // filter() 일치 불일치 필터링
    // reduce() 누산기 연산결과기억, 반복문, 계산,...배열처리


    const result2 = cookieArr.reduce((acc, item, idx, arr)=> (
        [
            ...acc, 
            {
                이름: item.split('=')[0],
                값: item.split('=')[1]
            }
        ]
    ), []);
    console.log( 'reduce => 배열을 객체로 변환 ' );
    console.log( result2 );



    // 리턴문 사용
    const result3 = cookieArr.reduce((acc, item)=> {
        return [
            ...acc, 
            {
                이름: item.split('=')[0],
                값: item.split('=')[1]
            }
        ]
    }, []);

    console.log( 'result3 => 배열을 객체로 변환 ' );
    console.log( result3 );

    // reduce() 응용
    const job = [
        {이름: '조지현', 나이: 39, 급여: 3500000, 직업: '프론트앤드'},
        {이름: '홍지문', 나이: 49, 급여: 4500000, 직업: '백앤드'},
        {이름: '김수현', 나이: 26, 급여: 2500000, 직업: '웹디자이너'},
        {이름: '이수정', 나이: 25, 급여: 2700000, 직업: '웹퍼블리셔'},
        {이름: '김시연', 나이: 29, 급여: 5000000, 직업: '프론트앤드'},
        {이름: '김시연', 나이: 29, 급여: 6000000, 직업: '웹디자이너'},
        {이름: '김시연', 나이: 29, 급여: 6000000, 직업: '풀스택'}
    ]

    // 1. 급여 합계 계산 리듀스
    // 리턴문 사용
    let hap = job.reduce((acc, item, idx, arr)=> {
        return acc + item.급여;
    }, 0);
    console.log( hap.toLocaleString('ko-KR') );
    // 19,200,000

    // 즉시 리턴
    hap = job.reduce((acc, item, idx, arr)=> acc + item.급여 , 0 );
    console.log( hap.toLocaleString('ko-KR')  );

    // 2. 급여 300만원 이상인 인원수 카운트
    // 리턴문 사용
    let cnt = job.reduce((acc, item)=>{
        if(item.급여>=3000000){
            return acc + 1;
        }
        else {
            return acc
        }
    }, 0);

    console.log( '급여 300만원 이상인 인원수 카운트' );
    console.log( cnt + '명');

    // 즉시리턴
    // 조건문 3항연산자
    cnt = job.reduce((acc, item)=> item.급여 >= 3000000 ? acc + 1 : acc, 0);

    console.log( '급여 300만원 이상인 인원수 카운트' );
    console.log( cnt + '명');

    // 문제 예시] 직업이 프론트앤드 인 사람의 급여의 합계 출력
    // 즉시리턴
    // 조건문 3항연산자
    sum = job.reduce((acc, item)=> item.직업==='프론트앤드' ? acc + item.급여 : acc, 0);

    console.log( '문제 예시] 직업이 프론트앤드 인 사람의 급여의 합계 출력' );
    console.log( sum.toLocaleString('ko-KR') + '원');


    // map() 함수이용 
    // 1. 급여 300만원이상인 인원수
    // map()
    let acc = 0;  // 누적연산 변수
    job.map((item, idx, arr) => {       
        return item.급여>=3000000 ? acc += 1 : acc += 0  
    } );        
    console.log( acc );

    // reduce()         
    cnt = job.reduce((acc, item, idx, arr)=> item.급여 >=3000000 ? acc+1 : acc+0 , 0 );
    console.log( cnt );

    // 2. 직업이 프론트앤드인 급여 합계        
    // map()
    acc = 0; // 누적 연산 변수
    job.map((item, idx, arr) => {
        return item.직업==='프론트앤드' ? acc += item.급여 : acc += 0;
    });
    console.log(  acc );

    // reduce()
    sum = job.reduce((acc, item, idx, arr)=> {
        return item.직업==='프론트앤드' ? acc + item.급여  : acc + 0;
    }, 0);
    console.log(  sum );

    // 3. 나이가 30세 이상 급여 합계
    // map()
    // reduce()
    acc = 0; // 누적 연산 변수
    job.map((item, idx, arr) => {
        return item.나이>=30 ? acc += item.급여 : acc += 0;
    });
    console.log(  acc );

    // reduce()
    sum = job.reduce((acc, item, idx, arr)=> {
        return item.나이>=30 ? acc + item.급여  : acc + 0;
    }, 0);
    console.log(  sum );

    
    // reduce() 응용
    // 이름, 나이, 급여, 직업
    const jobArr = [
        "조지현, 39, 3500000, 프론트앤드",
        "홍지문, 49, 4500000, 백앤드",
        "김수현, 26, 2500000, 웹디자이너",
        "이수정, 25, 2700000, 웹퍼블리셔",
        "김시연, 29, 5000000, 프론트앤드",
        "김수영, 29, 6000000, 웹디자이너",
        "문영수, 29, 7000000, 풀스택"
    ]

    // 배열(Array) => 객체(Object)        
    // map() 1;
    acc = [];
    jobArr.map((item)=> {
        return acc = [
                ...acc,
                {
                    이름: item.split(',')[0],
                    나이: item.split(',')[1],
                    급여: item.split(',')[2],
                    직업: item.split(',')[3]
                }
        ]
    });
    console.log( acc );
    
    // map() 2;
    // 맵함수는 리턴하면 결과 값 배열
    acc = jobArr.map((item)=> (
            {
                이름: item.split(',')[0],
                나이: item.split(',')[1],
                급여: item.split(',')[2],
                직업: item.split(',')[3]
            }
    ));
    console.log( acc );


    // reduce();
    // 배열 = []
    let 직장인 = jobArr.reduce((acc, item)=> [
        ...acc,
        {
            이름: item.split(',')[0],
            나이: item.split(',')[1],
            급여: item.split(',')[2],
            직업: item.split(',')[3]
        }
    ], [] );
    console.log( 직장인 );


    let txt = "조지현, 39, 3500000, 프론트앤드;  홍지문, 49, 4500000, 백앤드;  김수현, 26, 2500000, 웹디자이너;이수정, 25, 2700000, 웹퍼블리셔;  김시연, 29, 5000000, 프론트앤드; 김수영, 29, 6000000, 웹디자이너; 문영수, 29, 7000000, 풀스택";

    // 0. 단계 " "  공백제거 정규표현식  \s  => replace(정규표현식, "")
    // 0. 단계 " "  공백제거 " "  => replaceAll(" ", "")

    // 1. 단계 ";"  배열 만들기
    // let txtArr = txt.replaceAll(' ','').split(';');  // 행단위 배열처리
    // Global 글로발 전체(All)
    let txtArr = txt.replace(/\s/g,'').split(';');  // 행단위 배열처리

    console.log( txtArr );
    /* 
        [
            "조지현, 39, 3500000, 프론트앤드",
            "홍지문, 49, 4500000, 백앤드",
            "김수현, 26, 2500000, 웹디자이너",
            "이수정, 25, 2700000, 웹퍼블리셔",
            "김시연, 29, 5000000, 프론트앤드",
            "김수영, 29, 6000000, 웹디자이너",
            "문영수, 29, 7000000, 풀스택"
        ]
    */
    // 2. 단계 ","  객체 만들기 이름, 나이, 급여, 직업
    let res = txtArr.map((item)=> (
        {
            이름: item.split(',')[0],
            나이: item.split(',')[1],
            급여: item.split(',')[2],
            직업: item.split(',')[3]
        }
    ));
    console.log( res );

    // reduce()
    res = txtArr.reduce((acc, item)=> [
        ...acc, 
        {
            이름: item.split(',')[0],
            나이: item.split(',')[1],
            급여: item.split(',')[2],
            직업: item.split(',')[3]
        }
    ], []);
    console.log( res );
```