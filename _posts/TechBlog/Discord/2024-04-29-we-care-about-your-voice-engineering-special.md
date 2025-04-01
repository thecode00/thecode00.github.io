---
title: "[Discord - 테크 블로그 번역] we-care-about-your-voice-engineering-special"

toc: true
toc_sticky: true
date: 2024-04-29
last_modified_at: 2024-04-29
---

### 여러분의 소리에 귀 기울입니다 (엔지니어링 스페셜)

Over the last four months, a couple of our engineers tucked themselves into a cave and coded some incredible backend voice chat infrastructure improvements. These are the kind of fixes that just make Discord work better. You’ll never notice them because… well, that’s the point. Your voice experience should just be smoother than ever.

지난 4개월 동안, 저희 엔지니어 몇 명은 마치 동굴 속에 있는 듯 깊이 몰입하여 백엔드 음성 채팅 인프라를 놀랍게 개선하는 작업에 매진했습니다. 이런 개선들은 디스코드를 더욱 원활하게 만듭니다. 여러분은 아마 이런 개선을 눈치채지 못할 것입니다. 왜냐하면 그게 바로 저희가 목표로 하는 바이기 때문입니다. 여러분의 음성 채팅 경험은 그 어느 때보다 부드럽고 자연스러워야 합니다.

We want to provide some insight into what we actually did so you can understand how much we care about making sure your voice chat experience is as painless as possible. This kind of work isn’t the sexiest stuff but it’s some of the most important work we do here.
저희가 실제로 어떤 작업을 했는지 간단히 설명드리고자 합니다. 이를 통해 저희가 여러분의 음성 채팅 경험을 가능한 한 매끄럽게 만들기 위해 얼마나 많은 노력을 기울이고 있는지 아실 수 있을 것입니다. 이런 종류의 작업이 가장 화려한 일은 아니지만, 저희가 여기서 하는 가장 중요한 작업 중 하나입니다.

With an expert three-pronged approach, two of our engineers, Jesse and Andrei, were able to greatly reduce voice issues and improve performance across the board. This was done by creating a curator, leveling up our infrastructure, and improving our client technology.
두 명의 엔지니어 Jesse와 Andrei는 전문가다운 3단계 접근법을 통해 음성 관련 문제를 크게 줄이고 성능을 전반적으로 개선했습니다. 이 작업은 curator를 만들고, 인프라를 업그레이드하고, 클라이언트 기술을 개선함으로써 가능했습니다.

Watch the video for a basic breakdown from our engineers Jesse and Andrei. Then, read below for further details.
아래의 영상에서 엔지니어 Jesse와 Andrei가 직접 간단한 설명을 해주니 한 번 시청해 보세요. 더 자세한 내용은 아래를 계속 읽어주시기 바랍니다.

<iframe width="519" height="292" src="https://www.youtube.com/embed/TZiOUel0IZ0" title="Discord Engineering - Voice Improvements" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

# curator 만들기

Server health is important. If you’re connected to a server that’s experiencing issues for whatever reason, you might encounter things like robo voice or even disconnects (which is, clearly, the last thing we want our users to experience). Maintaining connection in the middle of a gank can be the defining factor between success and failure.

서버 상태는 매우 중요합니다. 만약 여러분이 어떤 이유에서든 문제가 있는 서버에 연결되어 있다면, 로봇처럼 들리는 음성이나 연결 끊김과 같은 문제를 경험할 수 있습니다(당연히 우리는 사용자들이 이런 상황을 겪는 걸 절대 원하지 않습니다). 특히 게임에서 치열한 전투 중에 안정적인 연결 상태를 유지하는 것은 승패를 가르는 결정적인 요소가 될 수 있습니다.

The curator detects and removes bad servers. It does this by sending all servers some network data similar to the voice data that users send. The curator then inspects the return traffic. If it’s not healthy, it alerts the clients that the server is bad and the server is removed.
curator는 문제가 있는 서버를 감지하고 제거합니다. 이를 위해 curator는 사용자가 보내는 음성 데이터와 비슷한 네트워크 데이터를 모든 서버에 전송하고 반환된 데이터를 검사합니다. 만약 데이터가 정상이 아니라면 클라이언트에게 서버에 문제가 있다고 알리고 그 서버를 제거합니다.

Discord engineers can also manually blacklist bad servers, providers, and regions when issues arise.
디스코드 엔지니어는 문제가 발생했을 때 문제가 있는 서버, 서비스 공급자 그리고 지역을 수동으로 블랙리스트에 추가할 수 있습니다.

Another sweet feature of the curator is that it improves our ability to roll out updates without disturbing our users.
curator의 또 하나 멋진 기능은 사용자 경험을 방해하지 않고 업데이트를 배포할 수 있도록 도와준다는 점입니다.

Most of the time we can update our voice servers while users are on them. Sometimes though, an update requires us to take the server offline. The curator can mark a server as “draining”, allowing currently connected users to finish up their voice session on the server. However, new sessions will be started on non-draining servers. Once all the sessions on the server have finished, we take the server offline and do the update.
대부분의 경우 우리는 사용자가 음성 서버에 연결된 상태에서도 업데이트를 진행할 수 있습니다. 하지만 일부 업데이트의 경우 서버를 오프라인으로 전환해야 할 수도 있는데, 이때 curator가 서버를 "점진적 종료(draining)" 상태로 표시할 수 있습니다. 이렇게 하면 이미 연결된 사용자는 음성 세션을 중단 없이 마칠 수 있고, 새로운 세션이 "점진적 종료" 상태가 아닌 서버에서 시작됩니다. 서버에 있는 모든 세션이 끝나면 서버를 오프라인으로 전환하고 업데이트를 진행합니다.

Leveling Up the Infrastructure

# 인프라 업그레이드하기

One of the key things that Discord provides over self-hosted alternatives is something called “failover.”
디스코드가 자체 호스팅 방식의 다른 솔루션과 비교해 제공하는 가장 중요한 기능 중 하나는 바로 "failover"입니다.

When issues arise with one particular provider or data center, Discord will move users connected to these servers to healthier servers.
만약 특정 서비스 공급자나 데이터 센터에 문제가 생기면, 디스코드는 해당 서버에 연결된 사용자들을 즉시 더 건강한 서버로 이동시킵니다.

This happens seamlessly on our end — as a user, you’ll never notice this occurs (unless you’re staring mindlessly at your voice connection information for some reason).
이 과정은 완벽하게 자동으로 이뤄지므로, 사용자 입장에선 이런 일이 일어난다는 것을 알아차릴 수도 없습니다. (물론 아무 이유 없이 연결 상태 창만 빤히 쳐다보고 있다면 모를까 말이죠.)

Get off your mom’s computer Jimmy.
We improved this process in a few ways.
우리는 이 failover 과정을 여러 가지 방식으로 개선했습니다.

First up, we added multiple providers and data centers to almost all of our regions so we can have more options.
첫째, 거의 모든 지역에 여러 서비스 공급자와 데이터 센터를 추가해 선택지를 넓혔습니다.

Second up, we increased the number of servers in each region. Increased capacity means more, more, and more options.
둘째, 각 지역의 서버 개수를 늘려서 더 많은 옵션과 용량을 확보했습니다. 더 많은 서버는 곧 더 나은 옵션을 의미합니다.

Finally, we consolidated servers in some regions to provide cleaner and less confusing server options.
마지막으로, 몇몇 지역의 서버들을 통합하여 더 간결하고 명확한 서버 옵션을 제공하게 되었습니다.

Overall, this means our backend has a lot more flexibility to maintain connection for our users.
전체적으로 이러한 개선 덕분에 우리 백엔드 시스템은 사용자들이 더욱 안정적으로 연결을 유지할 수 있도록 높은 유연성을 확보하게 되었습니다.

This image is like a metaphor.
Improving the Client Technology

# 클라이언트 기술 개선하기

The last bastion of these improvements is our client itself.
이러한 개선의 마지막 관문은 바로 디스코드 클라이언트 그 자체입니다.

The client is now much more resilient to spotty internet and will resume connections without losing any voice traffic.
디스코드 클라이언트는 이제 불안정한 인터넷 환경에도 훨씬 더 잘 대응하며, 음성 데이터를 잃지 않고 연결을 빠르게 다시 복구할 수 있게 되었습니다.

Network changes, Wi-Fi blips, IP changes, and short internet outages are now recognized quickly and our voice reconnection responds just as fast. In practice, you’ll notice far less connection issues when experiencing these things.
네트워크 환경이 바뀌거나 Wi-Fi가 잠깐 끊기거나, IP 주소가 변경되거나, 짧은 시간 동안 인터넷이 끊어지더라도 즉시 인식하여 빠르게 재연결을 수행합니다. 실제 사용 환경에서도 연결 문제가 훨씬 줄어든 것을 체감할 수 있을 겁니다.

You’ll Never Know What Hit Ya

# 무슨 일이 있었는지도 모를겁니다

As we said in the beginning, the key with these improvements is that you will never notice them taking effect. We do all the heavy lifting behind the scenes and we do it all seamlessly so you can do the thing you’re trying to do — play games with a stable, high quality voice connection.
처음에도 말했듯이, 개선의 핵심은 사용자들이 개선된 사항을 알아차릴 수조차 없도록 매끄럽게 적용하는 것입니다. 우리는 무대 뒤에서 모든 어려운 작업들을 수행하고, 사용자들은 그저 원하는 대로 게임을 하며 안정적이고 고품질의 음성 연결을 즐기기만 하면 됩니다.

If you have a friend who may have had an issue connecting with Discord in the past, now would be a great time to have them give Discord another shot.
만약 여러분의 친구가 과거에 디스코드 연결 문제로 어려움을 겪었다면, 지금 다시 한 번 디스코드를 사용해 보라고 권해보세요.

May your connections be strong and your ganks successful.
언제나 여러분의 연결이 안정적이고 갱이 성공하길 바랍니다,

Wanna be a part of our next engineering endeavor? Check out our job listings here.
우리의 다음 엔지니어링 프로젝트에 함께하고 싶으신가요? 채용 공고를 여기에서 확인해보세요.
