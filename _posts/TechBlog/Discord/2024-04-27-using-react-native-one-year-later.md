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

However, when we started building the iOS app, the performance of the chat’s scroll view wasn’t satisfactory, especially for some active chat groups. We decided to use ComponentKit for chat and write the necessary bridges instead. The Animated library also cannot deliver the animations as smooth as the native while doing heavy duty works on the JS thread, so we keep using PopAnimation for our drawers.

We tried to run the app on Android too when React Native for Android came out, but unfortunately encountered some performance issues and decided to hold off. According to our lead Android dev Miguel:
