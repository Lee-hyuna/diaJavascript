---
title: Web font
date: 2018-01-02
tags: ['web', 'webfont', 'font']
categories: ['Web']
layout: default 
---

회사 세미나에서 웹폰트 관련으로 발표를 진행했는데, 그 때의 발표자료를 올리도록합니다 :^)
(절대 문서정리가 귀찮아서 그런 것 아님..)

![](/images/WEBFONT.001.jpeg)
![](/images/WEBFONT.002.jpeg)
![](/images/WEBFONT.003.jpeg)
웹사이트는 대부분 텍스트로 이루어져있습니다. 
사진이나 영상 이외에 정보 전달은 글을 눈으로 읽는 과정에서 이루어지죠.
<br>


![](/images/WEBFONT.004.jpeg)
이 과정에서 시스템 폰트 외 상당 부분의 폰트를 아름다운 폰트로 사용하기 위해 웹사이트에 폰트를 심어주고 
그 폰트를 사이트에 불러오는 것을 웹폰트라고 합니다.  

페이지의 가독성을 높혀주어 사용자에게 정보가 잘 전달될 수 있도록 하는 것이 목적입니다.
<br>


![](/images/WEBFONT.005.jpeg)
![](/images/WEBFONT.006.jpeg)
 앞의 이미지를 보면 브라우저마다 지원하는 파일의 종류가 다른 것을 알 수 있습니다 
 EOT는 IE브라우저만 지원하고 WOFF는 모든 브라우저를 지원합니다. 
 <br>
 
 
![](/images/WEBFONT.007.jpeg)
![](/images/WEBFONT.008.jpeg)
앞의 이미지에서 처럼 카카오서체를 웹폰트로 사용하기 위해 폰트페이스를 적용합니다. 
폰트페이스에는 font-family , src , font-style , font-weight 등 속성을 사용할 수 있습니다.
 <br>
 
 
![](/images/WEBFONT.009.jpeg)
내가 사용할 웹폰트 family명은 카카오폰트로 하겠다 라고 선언한 것입니다. 
font-family에서 선언한 웹폰트 family명과 웹폰트명은 반드시 같아야하는 것은 아닙니다.
 <br>
 
 
![](/images/WEBFONT.010.jpeg)
로컬에 이미 설치된 폰트의 경로를 적는 local 다운로드할 웹폰트 주소를 적는 url속성이 있습니다. 
브라우저가 적용하는 순서는 선언한 순서대로 이동합니다. 
만약 카카오폰트가 설치되어 있지 않은 PC사용자가 크롬브라우저를 웹사이트에 접속하면 
위부터 아래로 읽어오는데 마지막엔 적용가능한 카카오.woff파일이 적용되게되고
이 때 적용가능한 폰트가 나올때 까지 읽기 때문에 불필요한 다운로드가 일어나게됩니다.
 <br>
![](/images/WEBFONT.011.jpeg)
이러한 불필요한 다운로드를 막기위해 포멧 속성을 사용합니다. 
포멧속성을 사용하게되면 브라우저에서 지원가능한 파일만 다운로드 받을 수 있습니다 
해당코드로 변경하면 지원이 불가능한 파일은 건너뛰고 적용가능한 파일이 적용이됩니다.
앞서 브라우저별 지원범위에서 말씀드렸다시피, 브라우저가 지원하지 않는 포멧이라면 지원가능한 포멧을 찾아서 다운로드를 하게 되는 것이죠.
<br>

eot 형식을 따로 분리하고 ?iefix를 붙이는 이유
 • IE8 이하 브라우저의 경우
  1. src에 둘 이상의 글꼴 형식을 포함하면 로드하지 못하고 404 오류를 보고함 > IE가 {} 사이에 있는 모든 파일을 로드하려고 시도하기 때문
  2. format() 값을 해석하지 못함 > format() 부분을 하나의 문자열로 인식 > url(/fonts/xxx.eot)%format('embedded-opentype')라고 읽어줌
    • 이것을 방지하기 위해 eot를 먼저 선언하고 ?iefix를 붙임 (물음표만 붙여줘도 됨)
    • IE가 물음표 뒤의 문자열을 쿼리 문자열로 생각하도록 만들어 이후 문자들을 읽는 것을 멈추게 함
<br>


![](/images/WEBFONT.012.jpeg)
![](/images/WEBFONT.013.jpeg)
서버에 직접 업로드 하는 경우는 CSS에 방금 말씀 드린 font-face를 직접 선언해주어야 합니다.
폰트의 종류가 많을 수록 font-face를 많이 선언해야해서 좀 복잡하지만
다른 CDN을 이용하는 것 보다 속도가 빠르고 안전합니다 

무료배포 웹폰트 CDN을 이용하는 경우  
font-face를 정의하지 않아도 되기에 편리하지만, 서버에 직접 업로드하는 것 보다 
속도가 느리고 해당 CDN서버가 제대로 동작하지 않을 경우 웹폰트를 제대로 제공받지 못할 수 있으므로 
서버가 있으면 직접 업로드하는 것이 좋습니다
<br>


![](/images/WEBFONT.014.jpeg)
웹폰트가 렌더링 되는 구조에 대해 잠시 설명드리겠습니다
처음 사용자가 브라우저를 접속하면 브라우저가 html 문서를 요청 파싱 후 dom생성 작업을 시작합니다
브라우저가 CSS, JS 및 기타 리소스를 발견하고 요청을 발송하고
렌더를 하면서 CSS를 검사하고 CSSOM을 빌드합니다.
그 후 DOM과 CSSOM을 결합하여 렌더링 트리를 만들고 웹페이지가 로드됩니다.

그 과정에서 렌더링 트리가 페이지의 렌더링에 필요한 글꼴이 무엇인지 확인하고 확인되다면 해당글꼴을 요청합니다.
페인팅을 진행할 때 글꼴을 사용할 수 없다면 브라우저가 텍스트를 렌더링 하지 않고 
사용할 수 있게 된다면 브라우저가 그때 텍스트를 그리게 됩니다. 
<br>


![](/images/WEBFONT.015.jpeg)
![](/images/fout.gif)
웹폰트의 대표적인 이슈인데요,
FOUT는 웹폰트파일이 완전히 로드되기 전 기본 서체가 보였다가 로드가 완료되면 웹폰트로 교체되는 현상이고
<br>
 
 
![](/images/foit.gif)
FOIT는 웹폰트파일이 다운로드 전 텍스트 렌더링이 지연되면서 텍스트영역이 비어있다 로드 완료되면 보여지는 현상입니다
<br>
 
 
![](/images/WEBFONT.018.jpeg)
![](/images/WEBFONT.019.jpeg)
폰트가 로드되어있는지 체크해주는 폰트페이스 옵저버 라이브러리를 추가합니다. (FontFaceObserver)
웹폰트가 로드되고 사용자에게 알려지도록 모니터 합니다, 스크롤이벤트를 사용하여 최소한의 오버헤드로 효율적으로 로드를 감지하는 라이브러리입니다.
폰트옵저버 콜백은  글꼴이 로드가 된 후 상위 부모에게 클래스를 부여하여 폰트를 입히는 건데요, 해당 로직을 사용하면 폰트들이 깜박거리는 현상을 막을 수 있습니다.
<br>


![](/images/WEBFONT.020.jpeg)
앞의 이미지에서 파란막대가 HTML이고 보라색이 CSS 회색이 글꼴파일입니다. 
앞서 말씀 드린 구조와 같이 브라우저가 HTML을 파싱할 때 CSS파일에 대한 참조를 발견하고 다운로드를 합니다 
CSS를 완전히 다운로드하면 브라우저에서 글꼴이 필요하다는 걸 인식하고 다운로드를 시작합니다. 

맨위에 보이는 한줄의 코드를 추가하고 폰트를 빠르게 다운로드할 수 있는 방법이 있는데요, 
프리로드 혹은 프리팻치를 통해 
아래의 이미지 처럼 CSS파일을 정의하기 전에 폰트를 다운로드합니다. 

브라우저 에이전트가 "as"속성(및 이 대상과 관련된 우선 순위)에 따라 현재 탐색할 대상 리소스를 미리 가져와 캐시하도록 지정합니다.
<br>


![](/images/WEBFONT.021.jpeg)
세번째 해결방안은 WebFont Loader를 사용하는 방법입니다 
웹폰트를 로드할 때 구글에서 제공하는 웹폰트로더를 사용하여 FOUT현상을 막을 수 있습니다. 

앞에 보여드렸던 프리로드와는 다르게, 이 웹폰트로더는 사이트의 나머지가 로드되기 전에 로드하고
비동기스크립트도 사용할 수 있지만, 폰트가 먼저 로드되는 것을 확실하게 하기위해 동기스크립트를 사용하는 것이 좋습니다.
<br>


![](/images/WEBFONT.023.jpeg)
웹폰트로더를 적용하면 해당 폰트에 관련한 이슈들이 클래스로 붙게됩니다.
이를 통해서 구글 웹폰트로더를 사용하면 로드되는 시간동안 변화를 체크하여 6가지 이벤트를 제공하여 해당 클래스를 html에 부여를 해주게 됩니다

그리고, 요 라이브러리는 구글에서 제공하는 폰트만 가능합니다. 이 부분 참고해주세요.
요 로직에 관해 궁금하신 분들은 해당 API 레퍼런스 확인하시면 디테일한 정보를 알 수 있습니다
<br>
 
 
![](/images/WEBFONT.024.jpeg)
이외에도 합리적인 방법으론 font.css파일을 ajax로 가져와 head에 뿌리고 그걸 로컬스토리지에 저장하면 
FOUT이 한번일어나고 이후 방문부터는 로컬스토리지에 저장된 CSS내용을 꺼내 head에 박는 방법도 있습니다. 

즉,

처음 웹 폰트를 로딩할 때 한 번만 기본 글꼴 깜빡임 현상이 있게 하고 두 번째 페이지부터는 없게 하는 방법이구요
그럼으로써 인터넷 속도가 느린 경우에도 웹 폰트를 안정적으로 사용할 수 있게 합니다.
<br>


![](/images/WEBFONT.025.jpeg)
마지막으로 크로스도메인에 관련된 내용입니다. 
웹폰트를 호출했지만 웹폰트를 못불러오는 이슈가 발생할 경우 오류메세지가 뜨는데요, 
요청받은 웹서버에서 크로스 도메인 통신을 가능하도록 허용해야합니다. 

웹폰트를 올린 CDN도메인과 현재 웹폰트를 가져와서 써야하는 페이지간의 통신이 제한되는 것으로 
웹폰트가 올려진 CDN서버의 담당자가 허용을 해줘야합니다. 
<br>


![](/images/WEBFONT.027.jpeg)