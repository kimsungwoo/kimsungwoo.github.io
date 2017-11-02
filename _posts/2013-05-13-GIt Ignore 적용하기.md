---
layout: post
title: "Git Ignore적용하기"
date: "2013-05-13"
slug: "example_content"
description: "gitignore`파일은 비 추적 파일을 지정합니다. Git이 이미 추적 한 파일은 영향을받지 않습니다. gitignore파일의 각 행은 패턴을 지정합니다."
category: 
  - 개발
  - 안드로이드
# tags will also be used as html meta keywords.
tags:
  - gitignore
  - git
show_meta: true
comments: true
mathjax: true
gistembed: true
published: true
noindex: false
nofollow: false
# hide QR code, permalink block while printing.
hide_printmsg: false
# show post summary or full post in RSS feed.
summaryfeed: false
## for twitter summary card with squared image and page description or page excerpt:
# imagesummary: foo.png
## for twitter card with large image:
# imagefeature: "http://img.youtube.com/vi/VEIrQUXm_hY/0.jpg"
## for twitter video card: (active for this page)
videofeature: ""
imagefeature: ""
videocredit: 
---

Howdy! This is an example blog post that shows features supported in **lanyon-plus** theme. See [raw post](https://raw.githubusercontent.com/dyndna/lanyon-plus/master/_posts/2013-01-01-example-content.md) for required YAML header and liquid tag specifications.

<!--more-->

* TOC
{:toc}

# Git Ignore란
`gitignore`파일은 비 추적 파일을 지정합니다. Git이 이미 추적 한 파일은 영향을받지 않습니다.
gitignore파일의 각 행은 패턴을 지정합니다.
>Git은 경로를 무시할지 여부를 결정할 때 일반적으로 gitignore다음 우선 순위와 함께 여러 소스의 패턴을 가장 높은 순서에서 가장 낮은 순서로 검사합니다 (한 수준의 우선 순위 내에서 마지막 일치하는 패턴이 결과를 결정합니다).

.gitignore경로와 같은 디렉토리 또는 상위 디렉토리 의 파일에서 읽은 패턴은 상위 레벨 파일 (작업 트리의 최상위 레벨까지)의 패턴이 하위 레벨 파일의 패턴에 의해 덮어 쓰여지고 파일. 이 패턴은 .gitignore파일 의 위치에 상대적으로 일치 합니다. 프로젝트는 일반적으로 프로젝트 .gitignore저장소의 일부로 생성 된 파일 패턴을 포함하는 해당 파일을 저장소에 포함합니다.


## 사용법


{% highlight js %}

.gitignore Command
git rm -r --cached
git add .
git commit -m "fixed untracked files”

{% endhighlight %}


### Git Ignore For Android

<code data-gist-id="00e5729d1f5dbd492f55baf3c83c4daf" data-gist-file=".gitignore_android" ></code>


### Git Ignore For Python

<code data-gist-id="6bcba188755a5f3a563733dffb6bea37" data-gist-file=".gitignore_python" ></code>

