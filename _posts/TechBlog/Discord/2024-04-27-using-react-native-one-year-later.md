---
title: "[Discord - 테크 블로그 번역] using-react-native-one-year-later "

categories: javascript
toc: true
toc_sticky: true
date: 2024-01-05
last_modified_at: 2024-01-05
---

#

https://discord.com/blog/using-react-native-one-year-later

### REACT NATIVE 사용 일 년 후

작년 봄에 Discord의 iOS 개발자 면접을 볼때 테크 리드인 Stanislav가 React Native가 미래입니다. 출시되는 즉시 React Native를 사용하여 iOS앱을 처음부터 만들 것입니다.

As a native iOS developer, I strongly doubted using web technologies to build mobile apps because of my previous experiences with tools like PhoneGap. But after learning and using React Native for a while, I am glad we made that decision.

네이티브 iOS 개발자로서 저는 PhoneGap 같은 툴을 사용한 이전 경험때문에 모바일 앱을 만들때 웹 기술을 이용해서 만드는것에 매우 의혹스러웠습니다. 하지만 React Native를 학습하고 사용한 후에는 그 결정에 매우 만족스러웠습니다.

# 효율성

Although our iOS “team” is usually just me, the iOS app is still able to catch up with the lightning speed of our web and desktop development. Apple has recently allowed you to update the app over the air using JavaScriptCore without going through the App Store review process again. It is very helpful for a small startup without a fully dedicated iOS QA team doing thorough tests, since the iOS team is able to apply some hot fixes after shipping new features.

우리 iOS "팀"은 보통 저 혼자지만 iOS앱은 여전히 우리의 웹과 데스크톱 개발의 빠른 속도를 따라잡을수 있습니다. Apple은 최근 App Store 리뷰 프로세스를 거치지 않고 JavaScriptCore를 사용하여 무선으로 앱을 업데이트 할 수 있도록 허용했습니다.

After using React Native for over a year, our iOS development cycle has significantly accelerated because of its great effectiveness. For example:

React Native를 사용한지 일 년이 넘은 후 우리의 iOS 개발 사이클은 훌륭한 효율성 덕에 확실히 빨라졌습니다. 예를 들어:

v 1.0 was built within two weeks upon the existing front-end infrastructure.
Flexbox’s style code is about half as long and far easier to understand than the code of Auto Layout.
iOS app and web app share 98% of the code of store and action in the Flux design pattern.

- v 1.0은 기존 프론트엔드 인프라를 기반으로 2주안에 개발되었습니다.
- Flexbox의 스타일 코드는 Auto Layout의 코드보다 약 절반 정도 짧고 이해하기 쉽습니다.
- iOS 앱과 web 앱은 Flux 디자인 패턴에서 store와 action의 코드를 98% 공유합니다.

# 성능

React Native runs Javascript on a background thread and sends a minimal amount of code to main thread. It turns out there is little performance difference between this and native iOS apps which are written in Objective-C or Swift!

React Native는 자바스크립트를 백그라운드 스레드에서 실행하며 최소한의 코드를 메인 스레드로 보냅니다. 결과적으로 Objective-C나 Swift로 쓰여진 네이티브 iOS 앱과 성능차이가 거의 없는것으로 밝혀졌습니다.

However, when we started building the iOS app, the performance of the chat’s scroll view wasn’t satisfactory, especially for some active chat groups. We decided to use ComponentKit for chat and write the necessary bridges instead. The Animated library also cannot deliver the animations as smooth as the native while doing heavy duty works on the JS thread, so we keep using PopAnimation for our drawers.

하지만 iOS 앱을 만들기 시작했을때 특히 일부 활발한 채팅 그룹들에서 채팅 스크롤 뷰의 성능이 매우 만족스럽지 못했습니다. 그래서 채팅을 위해 ComponentKit를 사용하고 필요한 브릿지를 작성하기로 했습니다. 또 Animated 라이브러리도 JS 스레드에서 헤비한 작업을 하는동안에는 네이티브처럼 부드러운 애니메이션을 제공하지 못했습니다, 그래서 우리 drawers에는 PopAnimation을 계속 사용하고 있습니다.

We tried to run the app on Android too when React Native for Android came out, but unfortunately encountered some performance issues and decided to hold off. According to our lead Android dev Miguel:

React Native for Android가 출시되었을때 안드로이드에도 적용해보려했지만 불행하게도 성능 문제를 겪어 보류하기로 했습니다. 우리의 리드 안드로이드 개발자 Miguel에 따르면:

Unfortunately Android devices have much greater variance in performance and tend to trail significantly behind iOS. We were able to get our app running fairly quickly, but the performance — specifically on touch events was not at an acceptable level even on higher end devices. In addition at that early stage there was still a lot missing in the React Native Android feature-set that would have made getting our prototype to production level more time consuming than our iOS effort.

불행하게도 안드로이드 디바이스는 성능 차이가 크고 iOS에 상당히 뒤쳐져 있습니다. 우리 앱을 빠르게 실행할수 있었지만 성능이 터치 이벤트가 하이엔드 디바이스에서 조차 합격점을 줄수 없었습니다. 또한 초기 단계에서는 React Native Android의 기능이 여전히 많이 부족했기때문에 프로토타입을 프로덕션으로 만들기까지 iOS보다 더 많은 시간과 노력이 필요했습니다.

# 유용성

The React Native project keeps making the development work easier and allowing the developers to focus on the core app features in every new release. I just can’t calculate how many hours it saves via the handy tools from its in-app developer menu.

React Native 프로젝트는 새로운 릴리즈마다 개발자가 일하기 쉽고 앱의 중요 기능에 집중할수있게 해줍니다. 인앱 개발자 메뉴의 편리한 도구들을 통해 얼마나 많은 시간을 아꼈는지 계산할수도 없네요.

One of my favorite features is Show Inspector. It immediately displays the interactive view hierarchies and all the necessary style info of the selected component and simply beats any other iOS inspector tools I’ve ever used.

제가 좋아하는 기능중 하나는 Show Inspector입니다. 이건 선택된 컴포넌트의 인터랙티브 뷰 계층과 필요한 모든 스타일 정보를 즉시 보여줍니다 그리고 제가 사용한 모든 다른 iOS inspector 툴을 능가합니다.

# 커뮤니티

The React Native project pushes a new release biweekly with tens of new features and bug fixes. It is a double edge sword. Compared to the stable release of iOS every few months, the evolving code base costs extra time to upgrade especially for the app in production. So that’s why we only did four major upgrades of our forked React Native repo so far.

React Native 프로젝트는 격주로 새로운 릴리즈를 출시하며 수십개의 새로운 기능과 버그 픽스를 제공합니다. iOS의 안정적인 릴리즈가 몇달마다 이루어지는 것과 비교하면, 지속적으로 진화하는 코드 베이스는 특히 프로덕션 환경의 앱에서 추가적인 시간이 소요됩니다. 이건 양날의 검이 될수있습니다. 그래서 우린 포크된 React Native 저장소를 오직 4번의 메이저 업그레이드만 진행했습니다.

Since React Native is fairly new, the resources are limited and incomplete but will catch up with the other mature technologies in the near future given its increasing popularity. Below are some useful channels besides its repo that I use to ask question and get latest info:

React Native는 아직 새로운 기술이기 때문에 리소스가 제한적이고 불완전하지만 인기가 높아짐에 따라 다른 성숙한 기술들을 가까운 미래에 따라잡을것입니다. 아래는 저장소 외에 제가 질문을 하거나 최신 정보를 가져올때 쓰는 유용한 채널들입니다.

#react-native on Reactiflux.
js.coach — a catalog of open source component of React Native.
awesome-react-native — a list of React Native articles, tutorials and examples.

- #react-native[https://discord.com/invite/0ZcbPKXt5bWVQmld] on Reactiflux.
- js.coach[https://js.coach/react-native] — React Native의 오픈 소스 컴퍼넌트의 카탈로그.
- awesome-react-native[https://github.com/jondot/awesome-react-native] — React Native에 대한 기사, 튜토리얼, 예시 리스트.

Overall, React Native looks very promising and brings the mobile app development to a new level within our team. The transition from a native iOS developer like me is smoother than I originally thought. It also helps me to escape the pigeonhole at work as I am able to contribute to our web app which is written in React very easily.

React Native는 매우 유망한것으로 보이며 우리 팀의 모바일 앱 개발을 새로운 레벨로 끌어올립니다. 저와 같은 네이티브 iOS개발자로부터 전환은 제가 생각했던거보다 훨씬 쉬웠습니다. 또한 우리의 React로 쓰여진 웹 앱에 매우 쉽게 기여할수있어서 직업에서 한가지 역할만 할수있는것에서 탈출하는데 도움이 됐습니다.

Lastly, we’re always looking for talented engineers, designers, and other roles to join our team! Check out our Jobs page for openings (especially product designers plz come halp).

마지막으로, 우리는 항상 우리 팀에 합류할 재능 있는 엔지니어, 디자이너 및 기타 직군을 찾고 있습니다! 채용 공고를 확인해보세요 (특히 제품 디자이너분들 환영합니다!).
