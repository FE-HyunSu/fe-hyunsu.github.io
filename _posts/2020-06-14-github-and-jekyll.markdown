---
layout: post
title:  "Github Pages와 jekyll, 로컬 환경 이슈"
date:   2020-06-14
tags: [ruby, jekyll, github]
---
깃헙에서 개인 페이지를 호스팅할 수 있도록 해주는 서비스를 [Github Pages](https://pages.github.com){:target="_blank"}라고 한다. Github Pages는 jekyll을 지원한다. 이것이 무슨 말인고 하면, 우리가 깃헙 저장소에 jekyll 파일 구조를 따르는 소스 코드를 push하면 깃헙이 그걸 인식하고 자체적으로 `jekyll build`를 실행해서 페이지를 배포한다는 뜻이다. 덕분에 우리는 따로 서버를 가지고 있지 않아도 깃헙을 통해 커스터마이즈 가능한 블로그를 만들고 배포할 수 있다.

그런데 직접 홈페이지를 배포하지 않는다는 상황이 가끔은 혼란을 일으키는 원인이 된다. 웹 프레임워크를 통해 웹 앱을 개발해본 사람은 알겠지만 보통 애플리케이션의 코드를 수정하고 나면 바로 원격 저장소에 push하는 게 아니라 로컬 환경에 띄워보고 의도한 대로 잘 작동하는지 확인하는 단계를 먼저 거친다. Django를 예로 들면 `python manage.py runserver`를 실행해 로컬의 8000번 포트에 앱을 띄울 수 있다. 그래서 jekyll을 사용할 때도 언제나처럼 로컬 환경을 갖추려고 시도하는데, 이게 잘 안 될 때가 있다. 로컬에서는 잘 되는데 원격에선 잘 안 되고, 혹은 그 반대로 원격에선 되는데 로컬에선 안 되고... 그 이유는 바로 깃헙의 배포 환경이 내 로컬과 완전히 동일하지 않기 때문이다. 구체적으로 말하자면, 깃헙은 내가 만든 `Gemfile`을 읽지 않는다. 깃헙은 자기만의 `Gemfile`이 있어서 그것만 사용한다. 이 때문에 다음과 같은 이슈들이 생긴다.

# `theme`과 `remote_theme`
`_config.yml`의 `theme` 옵션은 프로젝트에 설치된 gem으로부터 jekyll 테마를 불러올 수 있게 한다. 그래서 내 로컬 환경에 원하는 테마의 gem을 깔고 `theme` 옵션을 통해 테마를 적용할 수 있지만 그걸 Github Pages에서 쓸 수 있다는 보장은 없다. Github Pages에서 사용 가능한 `theme` 옵션 값은 [이 페이지](https://pages.github.com/themes/){:target="_blank"}에 있는 것에만 한정되며, 여기 없는 값을 입력했을 경우 깃헙으로부터 page build warning 메일을 받게 된다.

이를 보완하기 위해 깃헙은 `remote_theme` 옵션을 제공한다. `remote_theme` 옵션은 다른 사람의 깃헙 저장소에 올라와 있는 테마를 사용할 수 있도록 한다. 옵션 값은 { 계정 이름 }/{ 저장소 이름 }으로 주면 된다. 예를 들어 해당 저장소 주소가 https://github.com/thelehhman/plainwhite-jekyll 이라면 옵션 값을 `thelehman/plainwhite-jekyll`로 주면 된다. 문제는 로컬 jekyll은 `remote_theme` 옵션을 인식하지 못한다는 것인데, 이는 [github-pages](https://github.com/github/pages-gem){:target="_blank"} gem을 설치하여 해결할 수 있다.

# 플러그인 사용

원래 jekyll 플러그인은 gem을 설치해서 사용할 수 있다. 그러니 위의 `theme`과 마찬가지로 깃헙에서는 그걸 알아먹지 못한다. 일단 [github-pages](https://github.com/github/pages-gem){:target="_blank"} gem이 설치되어 있으면 `_config.yml`에서 `plugins` 옵션을 설정해서 깃헙에서 플러그인들을 사용할 수 있긴 하다. 다만 [여기](https://pages.github.com/versions/){:target="_blank"} 등록되어 있는 플러그인만 사용할 수 있다. 

# `baseurl` 문제

Github Pages에서 개인이 생성할 수 있는 페이지는 User/Organization Page와 Project Page로 나뉜다. User/Organization Page는 계정당 단 하나만 생성할 수 있으며 저장소 이름이 반드시 `{ 계정 이름 }.github.io`이어야 하고 언제나 해당 저장소 이름과 같은 주소에 배포된다. Project Page는 한 계정이 여러 개를 생성할 수 있으며 프로젝트 이름도 자유이고 배포는 `{ 계정 이름 }.github.io/{ 저장소 이름 }`의 주소에 된다. 단 소스 코드를 `gh-pages` 브랜치에 push하거나 `master` 브랜치의 `/docs` 디렉토리에 push해야 깃헙이 Project Page로 인식하고 배포한다. `baseurl` 문제는 User/Organization Page를 빌드할 때 생긴다.

`baseurl`은 `_config.yml`의 옵션 중의 하나로 원래 용도는 jekyll 페이지를 서브도메인에 배포하고 싶을 때 그 서브도메인 값을 정의하기 위함이다. 그래서 단순하게 생각하면 User/Organization Page를 서브도메인에 배포하고 싶을 때 `baseurl` 값을 설정하면 될 것 같다. 예를 들어 내 블로그를 `fuzzysound.github.io/blog/`에 배포하고 싶으면 `fuzzysound.github.io` 저장소에 있는 내 `_config.yml` 파일에 `baseurl: /blog` 한 줄을 추가하면 만사 오케이라고 생각하게 된다. 그런데 실제로 해보면 안 된다. 로컬에서는 `localhost:4000/blog/`에 페이지가 잘 뜨지만, 원격에서는 CSS 파일을 불러오지 못해 화면 양식이 깨지고 하이퍼링크는 여기저기 날라다닌다. 왜냐면 깃헙은 내 User/Organization Page를 무조건 고정된 주소 (`fuzzysound.github.io`)에 배포하기 때문이다. 이걸 레이아웃을 오버라이딩하는 식으로 고쳐볼라다간 오류가 꼬리에 꼬리를 물고 발생해 정신이 나가버린다. 

Github Pages를 사용할 때 `baseurl`의 올바른 용도는 Project Page를 빌드할 때 서브도메인을 명시함으로써 로컬과 원격에서 동일한 환경을 갖추기 위함이다. 예를 들어 Project Page 저장소 이름이 `myproject`이면, `baseurl` 값을 저장소 이름과 동일하게 `myproject`로 둠으로써 로컬에서는 `localhost:4000/myproject/`에, 원격에서는 `fuzzysound.github.io/myproject/`에 페이지가 배포되고 두 환경이 동일해진다... 라고 구글링해서 찾은 소스들에서는 설명하고 있다. 그 이상의 자세한 설명을 해주는 곳은 없고 jekyll이나 Github Page 공식 홈페이지에서도 이 내용을 자세히 언급하고 있지 않다. 내 생각엔 아무도 `baseurl`의 Github Page에서의 작동 방식을 확실하게 알지 못하는 것 같다. 일단 나는 Project Page에서 `baseurl`을 명기하지 않았을 때 문제가 생기는지는 아직 발견하지 못했다.

### 참고한 페이지
[Adding a theme to your GitHub Pages site using Jekyll](https://help.github.com/en/github/working-with-github-pages/adding-a-theme-to-your-github-pages-site-using-jekyll){:target="_blank"}

[About GitHub Pages and Jekyll #Plugins](https://help.github.com/en/github/working-with-github-pages/about-github-pages-and-jekyll#plugins){:target="_blank"}

[Clearing Up Confusion Around baseurl -- Again](https://byparker.com/blog/2014/clearing-up-confusion-around-baseurl/){:target="_blank"}