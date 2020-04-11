---
title: Jira, Bitbucket을 활용한 업무 공유 및 프로젝트 관리
date: 2020-04-11 13:00:00
category: development
thumbnail: './images/Jira-Bitbucket-Integration.png'
draft: false
---

## 개발 프로젝트를 관리 도구, Jira
[Jira 홈페이지](https://www.atlassian.com/ko/software/jira)

프로젝트 범위와 산출물은 초기에 개괄적으로만 정의되었다가 진행하면서 구체화될 수밖에 없으며 이로 인해 초기의 계획이 어긋나게 된다. 설계 완료되었어도 개발/테스트 단계에서 설계를 수정해야 하는 경우가 자주 발생한다.

고객의 요구가 변경될 수 있는 환경에서 개발팀은 민첩하게 업무를 관리하고 추적해야 한다. 나는 지금 일하고 있는 회사에서 프로젝트 관리 툴로 Atlassian 회사의 '지라(Jira)' 서비스를 도입하자고 주장했고 해당 서비스로 프로젝트를 관리 및 이끌고 있다.

Jira는 깔끔한 UI와 강력한 프로젝트 관리 기능을 제공하며 애자일, 스프린트 기능 등이 있어 변화에 빠르게 반응하고 업무에 집중할 수 있도록 도와준다.

자세한 내용은 구글 슬라이드로 정리해보았다.

<iframe src="https://docs.google.com/presentation/d/e/2PACX-1vRExz7fv0zOOwPBnRRkjYnx0YXvwMxK_eMycpyhAGkuPxHQvnzj23x_l5_WCffiZCjIQzieHHMzLjSw/embed?start=false&loop=false&delayms=10000" frameborder="0" width="960" height="569" allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>


## Git 코드 관리 도구, Bitbucket
[Bitbucket 홈페이지](https://bitbucket.org/product/ko/)

Jira는 업무 생산성 향상 및 프로젝트 관리라고 한다면, 소스 코드를 위한 방법론과 이를 도와주는 서비스도 필요하다.  프로젝트 관리와 코드 관리가 통합이 되면 개발 및 릴리즈 속도를 단축할 수 있고 빠르고 편한 협업을 만들 수 있다.

이를 위해 기존에 Github를 사용해왔고, 하나의 대표 계정으로 여러 비공개 저장소를 만들어 사람들을 초대하는 방식으로 소스 코드와 저장소를 관리했다. JIRA에 Github을 연동하기 위해서는 Github의 Enterprise 서비스를 사용해야 한다. 해당 서비스를 사용하려면 한 사람당 매월 21달러라는 큰돈을 지불해야 하는 부담이 있고, 관리 측면에서도 서로 다른 회사의 서비스를 사용해야 하니 비효율적이다.

Bitbucket는 Jira 서비스를 제공하는 Atlassian의 Git 코드 관리 서비스로 기본적으로 Jira와 연동 기능을 제공한다. 업무와 소스 코드 관리가 통합이 가능하니 협업과 수정/배포가 편리하고 추적이 가능하다. 비용은 5명 이하 US$15, 6-100명은 한 사람당 매월 3달러라는 금액을 지불해야 합니다. 금액에 대한 자세한 내용은 Bitbucket 가격 정책 사이트를 보면 자세한 금액을 계산할 수 있다.

[Bitbucket 가격 정책](https://bitbucket.org/product/ko/pricing)


## 함께 노력하고 배움의 자세를 가져야 한다

Jira와 Bitbucket이 정답이라고 생각하지 않는다. 팀에 맞는 효과적이고 효율적인 프로젝트 관리 방법론과 프로세스를 늘 고민하게 되며, 툴을 구축하는 것보다 단순한 프로세스로 먼저 팀 전체가 움직일 수 있도록 적용하는 것이 중요하다고 생각한다. 툴 적용과 프로세스의 정의가 끝나고 최소한 2~3개월은 지속적인 노력해야 팀에 적용이 될 수 있을 것이다. 앞으로 더욱 툴 외에 프로세스 관련해서도 학습, 정리해나가야겠다.
