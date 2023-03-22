# daum_topnews_scrapping


# 2020-2 Term-Project : Mid-term Report
#### 컴퓨터공학과 2017104015 이재호, 컴퓨터공학과 2017104038 한봉훈
#### 1) 프로젝트 목표 및 내용
- 주제 : 유사도 검사를 통한 문서 추천 프로그램
- 최종 목표 : 사용자에 의해 선택된 문서의 내용과 유사도가 높은 문서 및 사용자가 요구하는 키워드와 관련 있는 문서들을 추천해 주고, 선택된 문서의 간단한 요약문을 제공해 정보 습득, 접근 시간을 단축시킨다. 문서의 단어 빈도수 순위를 제공해 사용자가 예상 못 한 키워드를 접하게 하여 사용자의 문서 선택 폭을 넓혀준다.

-역할 분담 <br>



프로그램 개발에 필요한 전반적인 지식 (웹 스크래핑과 flask를 이용한 웹 구현)은 서적 및 인터넷 자료를 통해 각자 학습하였다.
개발 초기에 웹 스크래핑 및 유사도 분석과 flask를 활용한 웹 페이지 구현, 이렇게 두 파트로 나누어 작업하는 방식으로 진행하다가 기능의 구현과 이를 웹으로 띄우는 데 있어 여러 문제점이 발생하였다.  ex) 기능 구현에는 문제가 없으나 웹으로 띄우면 복잡하고 시간이 오래걸리는 코드
<br>
그래서 이후 코드에 문제점이 있거나 개선점이 있으면 맡은 파트와 관계없이 코드를 수정하고 새로 짜는 식으로 진행하여 프로젝트를 마무리 하였고 각자 중점을 두고 개발한 부분은 다음과 같다.  <br>

이재호 : 웹 스크래핑 및 유사도 분석 <br>
한봉훈 : 웹 스크래핑 및 flask를 활용한 웹 구현 <br>

#### 2) 주제 선정 이유 또는 이 프로젝트의 필요성
&nbsp;&nbsp;인터넷 기반 콘텐츠의 규모가 커져감에 따라 정보와 지식의 습득 기회가 증가했고, 과거보다 습득에 필요한 노력, 시간 등은 감소했다. 현재의 정보는 규모 성장에 따른 빨라진 생성 속도로 인해 다양한 형태와 방대한 양을 가지게 되었다. 디지털 분석 전문 회사 Esri UK가 성인 1000명을 대상으로 진행한 연구에서 위의 현대 정보의 특징으로 인하여 개인이 필요로 하는 특정 정보에 대해 오히려 접근성이 떨어지게 되었으며, 무분별한 정보의 유입은 사용자에게 필요성, 이용 가치, 신뢰도에 대한 고민으로 스트레스를 유발함을 보였다. 따라서 수많은 데이터 중 사용자의 요구 사항과 맞는 데이터를 선별하고 제공하는 기술이 필요해졌다. <br>
&nbsp;&nbsp;실제로 인터넷 포털사이트의 뉴스 페이지에 들어가 보면 ‘분야별 주요 기사’, ‘많이 본 기사’,‘ 많이 검색된 단어’에 대한 정보는 제공하고 있다. 하지만 이것들은 여러 사용자에 의해 누적된 데이터일 뿐 특정 정보를 요구하는 개인에게는 의미 있다고 볼 수 없는 정보이다. 또한 사용자가 원하는 정보를 포함하는 기사에 접근을 했다고 해도 주변에 나타나는 것은 사용자의 요구와는 전혀 상관없는 기사들이다. 직접 실험해본 결과 작성일 기준 ‘코로나’에 대한 약 500만 건의 기사가 검색 옵션을 관련도 순으로 주었음에도 불구하고 키워드의 빈도 수 순으로 나타나는 것이 아닌 키워드의 포함 여부와 최신 순으로 보였다. 이를 생각해보면 키워드를 통한 기사 접근 또한 개인이 원하는 특정 정보에 접근하는 게 어려워 보인다. <br>
&nbsp;&nbsp;따라서 사용자가 선택한 문서의 내용과 유사도가 높은 문서 및 사용자가 요구하는 키워드와 관련 있는 문서들에 대한 정보와 문서의 단어 빈도수 순위를 제공해 준다면 위의 문제점들을 어느 정도 보완할 수 있을 것이다. <br>
&nbsp;&nbsp;위 기능들을 잘 활용하면 유사한 문서 정보를 통해 사용자가 원하는 것과 관련된 정보에 접근하는 시간을 단축시킬 수 있을 것이며 단어 빈도수 순위를 통해 사용자가 예상 못 한 키워드를 접하게 하여 사용자의 문서 선택 폭을 넓혀줄 것이 기대된다.<br><br>
#### 3) 데이터 획득
&nbsp;&nbsp;인터넷 포털사이트가 제공하는 뉴스 페이지에서 뉴스기사 제목과 원문 데이터를 웹 크롤링을 통해 획득한다.<br><br>
**crawling.py**<br>
https://news.daum.net/ranking/popular?regDate= 의 랭킹 뉴스들을 크롤링한다. 

![daumnews](https://user-images.githubusercontent.com/33712528/102899985-0e036080-44af-11eb-9b26-49b8344d4a99.png)


csv파일에 저장된 기사의 제목과 내용은 프로그램이 실행되면 기사 제목과 내용을 저장하는 각각의 배열에 저장되어 양이 많더라도 빠르게 원하는 기사의 내용을 얻을 수 있게 하였다.

![csv](https://user-images.githubusercontent.com/33712528/102899982-0cd23380-44af-11eb-8642-d67d7adea954.png)


csv 파일에 저장된 기사의 제목과 내용은 프로그램이 실행되면 기사 제목과 내용을 저장하는 각각의 배열에 저장되어 양이 많더라도 빠르게 원하는 기사의 내용을 얻을 수 있게 하였다.
#### 4) 구현 내용 설명
1. 구현방향
    * 인터넷 포털사이트가 제공하는 뉴스 페이지에서 뉴스 기사 제목과 원문 데이터를 **Beautiful Soup**, **Requests**라이브러리를 활용해 크롤링 한다.
        - Beautiful Soup : HTML과 XML 문서를 파싱 하기 위한 파이썬 패키지. 웹 스크래핑에 유용한 HTML에서 데이터를 추출하는 데 사용할 수 있는 구문 분석된 페이지에 대한 구문 분석 트리를 생성한다.
        - Requests : 파이썬에서 HTTP 요청을 보낼 수 있게 해준다.
    * **Beautiful Soup** 라이브러리를 활용해 획득한 데이터 중 원문을 분석하기 위해 기사 제목과 원문을 분리시킨다.
    * **Konlpy** 라이브러리를 활용하여 기사 내용을 형태소 단위로 분석하고, 각 문서별 등장 단어의 빈도수를 벡터화해 전체 문서에 대한 단어 빈도수를 행렬로 나타내어 문서의 유사도 분석에 사용한다.
        - Konlpy : 한국어 정보처리를 위한 파이썬 패키지로 한국어 데이터를 처리할 때 주로 사용하는 라이브러리
    * **Scikit-learn** 라이브러리를 이용해 유사도 측정을 위한 TF-IDF 모델을 생성한다.
        - Scikit-learn : 파이썬의 대표적인 머신러닝 라이브러리 중 하나로 TF-IDF 모델을 생성하는데 사용한다.
    * **TextRank**알고리즘을 이용해 문서를 이루는 각 문장의 키워드를 추출하고, 키워드 score가 높은 문장을 뽑아서 간단한 요약문을 만든다.
        - TextRank : Google의 PageRank를 활용한 텍스트에 관한 그래프 기반의 Ranking 모델이다.
    * **Flask** 프레임 워크를 사용하여 기능을 웹 애플리케이션으로 구현함으로써 사용자에게 인터페이스를 제공한다.
        - Flask : 파이썬 웹 애플리케이션을 만드는 프레임 워크로 가볍고 단순하게 웹 애플리케이션 구현 가능
<br><br>
2. 실제 구현
    * **crawling.py** <br>
    https://news.daum.net/ranking/popular?regDate= 의 랭킹 뉴스들을 크롤링한다. 
    ![daumnews](https://user-images.githubusercontent.com/33712528/102899985-0e036080-44af-11eb-9b26-49b8344d4a99.png)
    기사는 위 사진과 같이 특정 날짜에 많이 본 기사들이 날짜별로 50개씩 올라와 있다. 
    제안서에 기술하였듯 Beutifulsoup 라이브러리를 활용하여 원하는 데이터 (기사 제목, 내용, 각 기사의 URL)을 파싱하였고 이를 제목과 내용을 구분지어 저장하기 위해 articles.csv파일에 저장하였다. <br>
    ![csv](https://user-images.githubusercontent.com/33712528/102899982-0cd23380-44af-11eb-8642-d67d7adea954.png)
    csv파일에 저장된 기사의 제목과 내용은 프로그램이 실행되면 기사 제목과 내용을 저장하는 각각의 배열에 저장되어 양이 많더라도 빠르게 원하는 기사의 내용을 얻을 수 있게 하였다.
    
    * **make_summary.py** <br>
    textrank 알고리즘을 활용해 각 기사의 내용을 5문장으로 요약하여 이를 summaries.csv파일에 저장한다. 한 행에 5줄로 요약된 하나의 기사 내용이 저장된다. 
    ![main](https://user-images.githubusercontent.com/33712528/102899993-0f348d80-44af-11eb-8331-7e128ab4139d.png)
    * **readCsv.py** <br>
    crawling.py실행을 통해 csv파일에 저장된 제목과 내용, 그리고 기사의 요약본을 불러와 리스트로 반환하는 역할을한다. 각각은 getTitles, getContents, getSummaries 함수에 의해 실행된다.
    
    * **make_matrix_voca.py** <br>
    기사에서 어떤 단어가 자주 등장하는지, 본문에서 특정 단어를 많이 포함하고 있는 기사는 어떤 기사인지를 알려주는 기능에 사용할 데이터를 가공한다. Scikit-learn 라이브러리의 Countvectorizer를 이용해 전체 기사에 등장하는 단어를 토큰화, 기사별 단어의 출현 빈도를 벡터화한다. CountVectorizer.vocabulary() 메소드를 이용해 토큰화된 단어를 추출 후 voca.txt에 저장해 단어장을 만든다. CountVectorizer.fit_transform() 메소드를 이용해 기사별 단어의 빈도수를 벡터화하고 벡터들의 집합 즉 행렬로 표현해 matrix.txt에 저장한다.<br>
    * **Frequency.py** <br>
    make_matrix_voca.py의 함수로 만들어진 matrix.txt와 voca.txt를 읽어와 특정 단어가 많이 등장한 기사들의 제목과 특정 기사에서 빈도가 높은 단어들을 얻는 함수를 구현한다.
    get_FrequencyWord 함수는 matrix.txt를 통해 각 행의 값 즉, 기사별 단어의 등장 횟수를 리스트로 만들고 등장 횟수를 기준으로 정렬해 해당 기사에서 많이 등장한 단어 TOP 5 리스트를 반환한다. 
    get_FrequencyTitle 함수를 통해 특정 단어가 많이 등장한 기사를 알기 위해 matrix.txt의 값중 특정 단어에 해당하는 열의 값을 리스트를 만들고 등장 빈도를 기준으로 정렬해 해당 단어가 많이 등장한 순으로 저장된 제목 리스트를 반환한다. <br>
    * **Cosine_Similarity.py** <br>
    get_similar 함수는 사용자가 선택한 기사의 제목, 전체 제목 리스트, 전체 내용 리스트를 인자로 받는다. Scikit-learn의 TfidfVectorizer를 이용해 문서 내에서 특정 단어의 등장 횟수를 특정 단어가 등장한 문서의 수로 나눈 값을 가중치로 하는 TF-IDF 행렬을 생성한다. Scikit-learn의 linear_kernel을 이용해 행렬 곱을 구하고, 이를 이용해 코사인 유사도 기법을 구현한다. 구해진 유사도 값을 정렬해 사용자가 선택한 기사와 내용이 유사한 기사들의 제목 리스트를 반환해 준다.<br>
    * **main.py** <br>
    위 파일들을 통해 저장된 데이터들을 활용하여 다양한 기능을 제공한다 
   ![main](https://user-images.githubusercontent.com/33712528/102899993-0f348d80-44af-11eb-8331-7e128ab4139d.png)
    첫 화면에서 기사들의 목록을 확인할 수 있고 ‘>’, ‘<’ 키를 통해 페이지를 이동할 수 있다. 입력 부분에 기사의 제목을 입력하면 해당 기사를 조회하고, 특정 키워드를 입력하는 경우에는 키워드를 포함하는 기사를 확인할 수 있다. 기사를 조회하면 Frequency.py, Cosine_Similarity.py의 함수를 통해 최다빈도 단어와, 유사도가 높은 기사를 출력하게끔 구현한다. <br>    
    * **web.py** <br>
    main.py 를 통해 실행할 수 있는 여러 기능을 flask 웹프레임워크를 통해 웹으로 구현하였다. cmd 창에서 실행될 때보다 쉽게 사용할 수 있고 명확한 인터페이스를 제공한다. 
    
    ![flask1](https://user-images.githubusercontent.com/33712528/102899986-0e036080-44af-11eb-90e7-e6fb6c9e338f.PNG)
    ![flask2](https://user-images.githubusercontent.com/33712528/102899989-0e9bf700-44af-11eb-99d6-29e65fb4ec19.PNG)
    ![flask3](https://user-images.githubusercontent.com/33712528/102899992-0e9bf700-44af-11eb-91a0-4ab99e8f73b2.PNG)   <br>
    
3. 주요기능
    * 기능1. 메인화면에 가공을 통해 얻은 기사의 제목들의 리스트를 출력한다.
    * 기능2. 사용자가 기사의 제목을 입력할 시 선택한 기사의 제목과 원문 출력
    * 기능3. 사용자가 선택한 문서의 간단한 요약문을 만들어 출력
    * 기능4. 사용자가 선택한 문서와 유사한 기사의 제목 출력
    * 기능5. 사용자가 선택한 문서 중 가장 많이 등장한 단어 순위 출력
    * 기능6. 사용자가 단어를 입력할 시 입력된 단어가 많이 등장한 기사의 제목 출력 <br>      
    
#### 5) 구현 결과

1. crawling.py 를 실행하여 뉴스기사에서 내가 원하는 데이터(기사 제목 및 내용)만을 스크래핑하여 하나의 파일(articles.csv)에 저장
 ![articles](https://user-images.githubusercontent.com/33712528/102899968-0774e900-44af-11eb-8135-777644d828a2.PNG) <br>

2. summary.py 를 실행하여 articles.csv 파일의 기사 내용을 요약하여 새로운 파일에 저장(summaries.csv).
![summary](https://user-images.githubusercontent.com/33712528/102900003-10fe5100-44af-11eb-8560-04725cdb4e40.PNG) <br>

3.make_matrix_voca 를 실행하여 기사 간 유사도 분석에 필요한 데이터를 matrix.txt에 저장하고, 기사에 등장한 단어를 voca.txt에 저장<br>
matrix.txt <br>
![matrix](https://user-images.githubusercontent.com/33712528/102900001-10fe5100-44af-11eb-954b-1504f5ab6272.PNG) <br>

vaca.txt <br>
![voca](https://user-images.githubusercontent.com/33712528/102900004-1196e780-44af-11eb-827c-38c6cea0bf33.PNG)
 <br>

4.main.py 를 실행하여 1~3 의 과정을 통해 가공한 데이터를 활용한 다양한 기능을 실행할 수 있다. <br>
초기화면 <br>
![main1](https://user-images.githubusercontent.com/33712528/102899994-0fcd2400-44af-11eb-809d-b8f41ca46344.PNG) <br>
페이지 전환<br>
![main2](https://user-images.githubusercontent.com/33712528/102899995-0fcd2400-44af-11eb-85d8-f26fc6a69503.PNG) <br>
기사 제목 입력을 통한 기사 조회 <br>
![main3](https://user-images.githubusercontent.com/33712528/102899996-1065ba80-44af-11eb-9bb1-8d0109b0bded.PNG) <br>
단어(keyword)로 기사를 조회했을 때
![main4](https://user-images.githubusercontent.com/33712528/102899997-1065ba80-44af-11eb-896e-7225a575d84f.PNG) <br>

5.web.py 를 실행하면 cmd에서 사용하던 기능을 단순하고 사용자 친화적이게 사용할 수 있다. 
메인화면 <br>
![flask1](https://user-images.githubusercontent.com/33712528/102899986-0e036080-44af-11eb-90e7-e6fb6c9e338f.PNG) <br>
 클릭한 기사 조회 <br>
![flask2](https://user-images.githubusercontent.com/33712528/102899989-0e9bf700-44af-11eb-99d6-29e65fb4ec19.PNG) <br>
단어(keyword)로 기사를 조회했을 때
![flask3](https://user-images.githubusercontent.com/33712528/102899992-0e9bf700-44af-11eb-91a0-4ab99e8f73b2.PNG) <br>

 
#### 6) 결론
원본 데이터의 경우 단순히 여러 사용자로 인해 누적된 데이터를 나열한 것에 불과하지만 사용자는 이 프로그램을 통해 특정 키워드를 입력하면 그에 해당하는 기사를 빠르게 접근 및 조회할 수 있다. 
또한 문서내용을 분석하여 유사도가 높은, 즉 사용자가 관심을 가질만한 가능성이 큰 기사들을 제공하고 빈도수가 높은 단어를 함께 제시하여 사용자가 관심가질만한 범위 내에서 선택의 폭을 넓혀주었다. 
마지막으로 이러한 기능을 단순 구현하는데 그치지 않고 사용자로 하여금 단순하고 쉽게 이용할 수 있도록 웹으로 구현하였다. 
따라서 요구 사항과 맞는 데이터를 선별하고 제공하는 프로그램을 개발함으로써 초반부에주제선정 이유로 언급한 '개인이 필요로 하는 특정 정보에 대한 접근성의 저하' 문제를 개선하였다고 말할 수 있다. 

#### 7) 오픈소스 활용한 부분 명시: 활용한 오픈소스의 출처와 본인 코드에서 활용한 부분 명시. 본인이 직접 구현한 부분 명시.

#### 8) 참고문헌: 프로젝트를 위해 획득한 자료, 인터넷 정보, 논문, 도서 등의 출처를 나열.

flask 튜토리얼 : https://flask.palletsprojects.com/en/1.1.x/tutorial/   
html 및 css 학습 : https://www.w3schools.com/
beautifulsoup 사용법 : https://www.crummy.com/software/BeautifulSoup/bs4/doc/

#### 9) 별첨: 3)의 획득한 데이터 원본 (너무 큰 경우 링크)
https://news.daum.net/ranking/popular?regDate= <br>
#### 10) 별첨: 4)의 가공한 데이터 원본
articles.csv, summaries.csv 파일<br>
#### 11) 별첨: 프로젝트를 위해 본인이 직접 개발한 python 소스코드 원본
