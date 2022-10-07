---
title: "[Git Blog] - Sidebar에 목차(Category List) 추가 "
excerpt: "Git 블로그(Git Page)에서 왼쪽 sidebar에 category list를 추가해보자."

categories: 
  - GitPage
tags: [Git, GitPage, jekyll]
toc: true
author_profile: true 
sidebar:
   nav: "docs"
---
# Sidebar에 Category List 생성하기
> 이 블로그는 jekyll의 minimal-mistake 테마를 적용했다.<br>
> 본 게시물은 <a href="https://ansohxxn.github.io/blog/category/" style="color:gray">**'공부하는 식빵맘'**</a> 님의 게시글에 큰 도움을 받았다.

## <span style="color:cornflowerblue"> **1. Category 구상하기**</span>
어떠한 Category를 설정하고, 어떻게 묶을 것인지를 미리 구상하는 것은 중요하다.
<figure class="half" style="margin-bottom:0px">
<img src="/assets/images/20221007/capture1.png" width="80%">
<img src="/assets/images/20221007/capture2.png" width="80%">
</figure>
<div style="text-align:center"><span style="color:darkgrey">[sidebar에 category list를 추가한 모습]</span></div><br>
나는 대목차 [Theory], [Project], [Git] 세 가지를, 그리고 그 아래에 [Javascript], [HTML], [CSS] 등 6가지 소목차를 구상하였다.<br>
<span style="color:darkgrey"><em> (부끄럽게도 아직 게시글이 2개뿐이라 게시글이 없는 소목차는 보이지 않는다... 부지런히 올려서 채워보자!!)</em></span>
<br>
또, 각 category에 몇개의 게시글이 있는지 표시하는 기능도 함께 추가해보겠다.

---
## <span style="color:cornflowerblue"> **2. Category별 Markdown 파일 만들기**</span>
가장 먼저, '_pages'란 폴더 안에 각 category별로 markdown문서를 작성해야한다. minimal-mistake에 보통 '_pages'라는 폴더가 있지만, 없다면 직접 생성하면 된다.<br>
**대목차**는 markdown파일을 만들지 않아도 된다. **소목차**에 해당하는 category만 파일을 생성하자.
<div style="text-align:center"><img src="/assets/images/20221007/markdown.png"></div><br>
이름은 구분할 수 있으면 된다. 단, <span style="color:cornflowerblue">markdown</span>으로 만들어야 함을 주의하자.<br>
파일을 만들었다면 안에 이러한 코드를 입력해야 한다.<br>

```markdown
---
title: "Javascript"  
layout: archive
permalink: categories/Javascript  
author_profile: true
sidebar_main: true
---

{% raw%}
{% assign posts = site.categories.Javascript %}  
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}
{% endraw %}
```

여기서 유저별, 그리고 카테고리별 변경해야 할 점은
- <span style="color:cornflowerblue">**title**</span>
- <span style="color:cornflowerblue">**permalink**</span> <br>
  ('categories'는 빼도 되지만 앞으로의 코드에서도 빼는걸 잊으면 안된다.)
- <span style="color:cornflowerblue">**{% raw%}{% assign posts = site.categories.Javascript %}{% endraw %}**</span> 에서 **categories.Javascript**

이 세 가지 이다.<br>
위 코드에서 각각 의미하는 것을 살펴보자
- **title**: category의 이름. 이 category는 'Javascript'이다. 
- **layout**: 이 category의 layout은 '**archive**'이다. 이는 minimal-mistake 테마에서 기본적으로 제공하는 레이아웃 방식이다.
- **permalink**: 상대주소. 이 category와 연결되는 링크이다.
- **author_profile**: 내 프로필에 나타낼건지 'true' 또는 'false'로 입력한다.
- **sidebar_main**: 별도로 지정한 변수값이다. 자세한 내용은 후술하겠다.

```
{% raw %}
{% assign posts = site.categories.Javascript %}  
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}
{% endraw %}
```
하단의 이 코드는 jekyll에서 사용되는 <span style="color:cornflowerblue">**Liquid**</span> 템플릿 언어로 이루어진 것이다.<br> Liquid와 관련 내용은 jekyll사이트에 있는 내용을 링크에 걸어둬야겠다.<br>
[[Liquid 알아보기 링크]](https://jekyllrb-ko.github.io/docs/liquid/)<br>
이 코드는 'archive-single.html'이라는 파일의 내용을 반영하는 것이고, 이 파일은 카테고리와 태그를 모아두는 역할을 한다. category list에 외적인 변화를 주고 싶다면 이 파일을 수정하면 되지만, 일단 수정하지 않고 진행하겠다.

> category 이름에 띄어쓰기가 들어간 경우 인식이 안될 수 있다. 이럴 땐 **site.categories.Git page**를 **site.categories.['Git Page']** 이런 식으로 입력해야 한다고 한다.

---
## <span style="color:cornflowerblue">**3. nav_list**</span>
'_include'폴더에 '**nav_list**'라는 파일을 연다. 만약 파일이 없다면 _include폴더 안에 새로 만들면 된다. 단, 이 파일은 markdown이나 HTML이 아니므로 확장자 없이 생성해야 한다.<br>
파일 안에 내가 작성한 코드는 이러하다.
```markdown
{% raw %}
{% assign sum = site.posts | size %}

<nav class="nav__list">
  <input id="ac-toc" name="accordion-toc" type="checkbox" />
  <label for="ac-toc">{{ site.data.ui-text[site.locale].menu_label | default: "Toggle Menu" }}</label>
  <nav class="nav__items" id="category_tag_menu">
    <li>
      전체 글 수 {{sum}} 개
    </li>
    <li>
      <span class="nav__sub-title">Theory</span>
      <ul>
        {% for category in site.categories %}
                    {% if category[0] == "Javascript" %}
                        <li><a href="/categories/Javascript" class="">Javascript ({{category[1].size}})</a></li>
                    {% endif %}
                {% endfor %}
      </ul>
      <ul>
        {% for category in site.categories %}
            {% if category[0] == "HTML" %}
                <li><a href="/categories/HTML" class="">HTML ({{category[1].size}})</a></li>
            {% endif %}
        {% endfor %}
      </ul>
      <ul>
        {% for category in site.categories %}
            {% if category[0] == "CSS" %}
                <li><a href="/categories/CSS" class="">CSS ({{category[1].size}})</a></li>
            {% endif %}
        {% endfor %}
      </ul>
      <span class="nav__sub-title">Project</span>
      <ul>
        {% for category in site.categories %}
                    {% if category[0] == "Project" %}
                        <li><a href="/categories/Project" class="">Project ({{category[1].size}})</a></li>
                    {% endif %}
                {% endfor %}
      </ul>
      <span class="nav__sub-title">Git</span>
      <ul>
        {% for category in site.categories %}
                    {% if category[0] == "GitPage" %}
                        <li><a href="/categories/GitPage" class="">GitPage ({{category[1].size}})</a></li>
                    {% endif %}
                {% endfor %}
      </ul>
      <ul>
        {% for category in site.categories %}
                    {% if category[0] == "Github" %}
                        <li><a href="/categories/Github" class="">Github ({{category[1].size}})</a></li>
                    {% endif %}
                {% endfor %}
      </ul>
    </li>
  </nav>
{% endraw %}
```
길다.....<br>
부분 부분 나눠서 코드를 살펴보자<br>
```markdown
{% raw %}
{% assign sum = site.posts | size %}

<nav class="nav__list">
  <input id="ac-toc" name="accordion-toc" type="checkbox" />
  <label for="ac-toc">{{ site.data.ui-text[site.locale].menu_label | default: "Toggle Menu" }}</label>
  <nav class="nav__items" id="category_tag_menu">
  {% endraw %}
  ```
  이 부분에서 다른건 아마 이미 파일 안에 있을 것이다. 중요한건 가장 윗 줄  <span style="color:cornflowerblue">{% raw %}
{% assign sum = site.posts | size %}{% endraw %}</span>. 이 부분은 이 코드 밑에 전체 글 수 와 관련된 코드이므로, 전체 게시물 수를 표시하고 싶다면 넣어주도록 하자.<br><br>

```markdown
{% raw %}
  <li>
      전체 글 수 {{sum}} 개
  </li>
{% endraw %}
```
코드 안에 {% raw %}{{sum}}{% endraw %} 이 게시글 수를 의미한다. 위 코드에서 'sum'이라는 변수에 값을 입력하고 이를 {% raw %}{{sum}}{% endraw %}라는 형태로 참조하는 것이다.<br><br>

```markdown
{% raw %}
<li>
      <span class="nav__sub-title">Theory</span>
      <ul>
        {% for category in site.categories %}
                    {% if category[0] == "Javascript" %}
                        <li><a href="/categories/Javascript" class="">Javascript ({{category[1].size}})</a></li>
                    {% endif %}
                {% endfor %}
      </ul>
{% endraw %}
```
이 부분부터는 계속 반복이니 한 구간만 살펴보자. 여기서 `<ul>`태그에 들어가지 않는 가장 윗줄은 **대목차**이다. 그리고 아래 `<ul>`태그에 들어가 있는 부분이 **소목차**이다.<br>
**대목차**는 윗 줄에 `<span>`태그 사이에 목차 이름을 넣어주면 되고, **소목차**는 `<ul>`태그 안에 들어있는 여러 코드에서 '**Javascript**'라고 적힌 부분을 모두 본인이 정한 category 이름으로 변경하면 된다. 중간에 Liquid로 이루어진 태그들은 게시글 <span style="color:cornflowerblue">2번</span>에서 만든 md파일과 링크를 거는 코드와 category별 게시글 수를 보여주는 코드이다.
<br>

---
## <span style="color:cornflowerblue">**4. sidebar.html**</span>
이제 거의 끝났다!<br>
'_include'폴더 안에 '**sidebar.html**'이라는 파일을 열어 다음과 같은 코드르 입력해보자.
```html
{% raw %}
{% if page.author_profile or layout.author_profile or page.sidebar %}
  <div class="sidebar sticky">
  {% if page.author_profile or layout.author_profile %}{% include author-profile.html %}{% endif %}
  {% if page.sidebar %}
    {% for s in page.sidebar %}
      {% if s.image %}
        <img src="{{ s.image | relative_url }}"
             alt="{% if s.image_alt %}{{ s.image_alt }}{% endif %}">
      {% endif %}
      {% if s.title %}<h3>{{ s.title }}</h3>{% endif %}
      {% if s.text %}{{ s.text | markdownify }}{% endif %}
      {% if s.nav %}{% include nav_list nav=s.nav %}{% endif %}
    {% endfor %}
  {% endif %}
  
  {% if page.sidebar_main %}   <!--추가-->
    {% include nav_list %}     <!--추가-->
  {% endif %}                  <!--추가-->
  
</div>
{% endif %}
{% endraw %}
```
이 코드들은 기존에 'sidebar.html'파일에 들어있는 코드들이고, 내가 추가한 것은 단 세 줄
```html
{% raw %}
  {% if page.sidebar_main %}   
    {% include nav_list %}     
  {% endif %}
{% endraw %}
```
게시글 <span style="color:cornflowerblue">3번</span>에서 작성한 'nav_list'파일을 <span style="color:cornflowerblue">2번</span>에서 후술한다고 했던 '**sidebar_main**'이라는 이름으로 반영하는 것이다. 그러나 한 가지 주의할 점이 있다.
```html
{% raw %}
  {% if page.sidebar.nav %}
    {% include nav_list nav=page.sidebar.nav %}
  {% endif %}
{% endraw %}
```
혹시 추가했던 코드 위에 이러한 코드가 있다면 sidebar에 category list가 중복으로 나타날 수 있다. 나의 경우 다른 파일명으로 위 코드를 백업해놓고 'sidebar.html'에서 지우니 중복이 해결되었다. <span style="color:crimson">다시 말하자면 위, 아래 코드 중 한가지만 'sidebar.html'안에 있어야 한다.</span>

---
## <span style="color:cornflowerblue">**5. _config.yml**</span>
마지막으로 **_config.yml**파일을 수정하면 된다.
```yml
# Defaults
defaults:
  # _posts
  - scope:
      path: ""
      type: posts
    values:
      layout: single
      author_profile: true
      read_time: true
      comments: true
      share: true
      related: true
      show_date: true
      sidebar_main: true  # 추가한 코드
```
제일 마지막 줄에 <span style="color:cornflowerblue">**sidebar.html**</span>에서 선언한 '**sidebar_main**'을 입력하고 'ture'를 입력한다.<br>
이렇게하면 왼쪽 sidebar에 category list가 생성되는 것을 확인할 수 있다.
> 나처럼 해당 category에 게시글이 없는 경우 **소목차**가 나타나지 않는다.

---
## <span style="color:cornflowerblue">**6. index.html(메인 페이지 오류)**</span>
게시글에서는 sidebar가 보이지만, 블로그 메인 페이지에서 보이지 않는다면 다음과 같은 코드를 'index.html'에 입력하면 된다.
```html
---
layout: home
sidebar_main: true  <!--추가한 코드-->
author_profile: true
---
```
`sidebar_main: true`를 이 파일에 추가하면 메인 페이지에서도 정상적으로 category list가 보이는 것을 확인할 수 있다.

---

<br><br>
<br>
>Git에 관한 첫 글인데 jekyll blog생성부터 순서대로 올리지 않은 이유는 내가 이 '블로그 구조'에 대해 정리가 하나도 안되었기 때문이다. 그래서 앞으로 추가할 것은 추가하는 김에 정리해서 이렇게 바로 올리겠지만, 이미 지나버린건 다시 해봐야할거 같으니 차근차근 정리해야겠다..  
