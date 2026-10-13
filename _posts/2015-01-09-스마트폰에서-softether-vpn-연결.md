---
title: "스마트폰에서 SoftEther VPN 연결"
date: "2015-01-09T22:50:23+09:00"
categories:
  - Posts
tags:
  - gotocloud
source: "https://gotocloud.co.kr/?p=1459"
---

(참고) 이 글을 읽기 전에 SoftEther VPN을 이용한 원격 접속 구현이라는 글과 원격 접속 VPN에서 IP 주소 자동 할당을 참고하기 바란다.

이 글에서는 이미 구성되어 있는 SoftEther VPN 서버에 스마트폰에서 VPN 연결을 하는 방법을 설명하고자 한다. 먼저 SoftEther VPN 서버 설정에 관한 글과 원격 접속 VPN에 IP 주소를 자동으로 할당하는 방법에 관한 글에서 설명한 대로 SoftEther VPN 서버가 설정이 되어 있는 상태에서 스마트폰에서 L2TP/IPsec 프로토콜을 이용하여 VPN 접속을 하도록 설정해 보도록 한다. L2TP/IPsec 프로토콜은 안드로이드 및 iOS 뿐만 아니라 Windows에 자체적으로 내장된 VPN 클라이언트에서도 지원하고 있는데, 이 프로토콜에 대한 설명은 VPN 터널링 프로토콜에 대한 예전 글을 참조하기 바란다.

### 1. SoftEther VPN 서버의 L2TP 설정

스마트폰의 L2TP/IPsec VPN 접속을 위해서 SoftEther VPN 서버에서 L2TP 기능을 활성화한다.

![](/posts/post-1459/images/윈도우-1-300x224.png)

SoftEther VPN 관리 툴을 사용하여 VPN 서버에 접속한 다음 IPsec / L2TP Setting을 선택한다.

![](/posts/post-1459/images/윈도우-2-300x228.png)

IPsec / L2TP Setting 화면에서 그림과 같이 L2TP Server Function을 체크하여 기능을 활성화한다. 암호화를 지원하지 않는 L2TP 클라이언트에서 접속을 허용하고자 할 경우에는 아래의 체크 박스도 활성화한다.

다음으로 L2TP 클라이언트가 접속할 Virtual Hub를 지정해준다. SoftEther VPN의 L2TP 계정은 “사용자 계정이름@Virtual Hub” 와 같이 사용되는데, 여기에서 지정된 Virtual Hub에 속한 사용자는 “@Virtual Hub” 부분을 생략하고 사용자 계정 이름만으로 접속하게 된다. 만일 여러 개의 Virtual Hub가 생성되어 있고, 해당 Virtual Hub에 L2TP로 접속하기를 원할 때는 “사용자 계정@Virtual Hub”와 같이 풀네임을 사용해야 한다. 여기에서는 DEFAULT 라는 이름의 Virtual Hub를 기본으로 정하였다.

다음으로 IPsec의 암호화를 위한 사전공유키(Pre-Shared Key)를 입력한다. SoftEther VPN에서는 사전 공유키를 8자 이내로 입력하도록 제한하고 있으니 8자를 넘기게 되면 접속이 되지 않을 수 있다. 사전공유키는 클라이언트에서 PSK 또는 Secret 라는 이름의 필드명으로 사용되곤 한다. 이 사전 공유키를 L2TP 클라이언트에서 입력해야 접속이 가능하다.

### 2. VPN 서버 방화벽 개방

L2TP/IPsec 에서는 IPSec NAT-T (Network Address Translator Traversal)을 위해 UDP 4500번 포트와 IPSec ISAKMP (Internet Security Association and Key Management Protocol)로 UDP 500번 포트를 사용하므로 SoftEther VPN 서버의 UDP 500 포트와 UDP 4500 포트를 개방한다. 이 두 포트가 개방되지 않으면 L2TP/IPsec으로 VPN 연결이 불가능하다.

### 3. 스마트폰 VPN 클라이언트 설정

서버 설정이 완료되면 스마트폰에서 VPN 접속이 가능하도록 설정한다. 이 글에서는 안드로이드 4.x 버전을 사용하였는데, 대부분의 안드로이드 전화기에서는 유사한 방식으로 설정이 가능하다.

[![](/posts/post-1459/images/1-1-168x300.png)](https://gotocloud.co.kr/wp-content/uploads/2015/01/1-1.png)삼성 갤럭시S3 VPN 설정
[![](/posts/post-1459/images/1-180x300.png)](https://gotocloud.co.kr/wp-content/uploads/2015/01/1.png)LG 옵티머스G VPN 설정
안드로이드 폰의  시스템 설정에 들어가서 VPN(가상 네트워크)라는 항목을 찾아서 선택한다. 삼성 갤럭시 S3의 경우 “시스템설정 -> 네트워크 더보기”에 있고, LG 옵티머스 G의 경우는 “시스템설정 -> 인터넷 함께 쓰기(테더링) 및 네트워크” 항목 아래에서 찾을 수 있다. 이 글에서는 옵티머스 G를 기준으로 설명하고자 한다. 삼성 갤럭시S3의 경우는 VPN을 사용할 경우 자격증명 저장소를 활성화해야 하는데, 이 때는 비밀번호나 PIN 암호를 설정해야만 하니 참고하기 바란다.

![](/posts/post-1459/images/2-180x300.png)

VPN 설정 화면에 처음 들어가면 VPN 네트워크 추가를 눌러서 접속하고자 하는 VPN 설정을 추가한다.

![](/posts/post-1459/images/3-180x300.png)

추가하고자 하는 VPN의 이름과 타입, SoftEther VPN 서버 주소를 입력한다. 타입은 L2TP/IPsec PSK로 지정하는데, 이는 사전 공유키(Pre-Shared Key, PSK)를 사용하는 L2TP/IPsec 프로토콜을 의미한다.

![](/posts/post-1459/images/4-180x300.png)

나머지 항목은 비워두고 아래로 내려 IPSec 사전 공유 키에 SoftEther VPN 서버에서 지정한 사전 공유키인 password를 입력한다. 이 사전 공유키는 L2TP/IPsec으로 접속하고자 하는 모든 사용자들에게 공유되어야 한다.

![](/posts/post-1459/images/5-180x300.png)

L2TP VPN 접속을 위한 설정이 완료되었다. 방금 설정한 GotoCloud VPN을 선택하여 접속을 시도한다.

![](/posts/post-1459/images/6-180x300.png)

VPN 접속 화면이 나타나면 사용자 이름에 SoftEther VPN 서버에서 생성한 계정이름을 입력한다. 서버 설정해서 설명한 바와 같이 “사용자 계정@Virtual Hub” 형태로 입력해야 하므로 gotocloud@DEFAULT와 같이 입력해야하지만 DEFAULT라는 이름의 Virtual Hub를 기본으로 지정했으므로 gotocloud만 입력하면 된다. 그리고 gotocloud 계정의 비밀번호를 입력한 다음에 “연결”을 시도한다.

![](/posts/post-1459/images/8-180x300.png)

접속에 성공하면 그림과 같이 “연결됨”이라는 메시지를 볼 수 있다. 설정에 문제가 있거나 암호가 다르거나, 여러가지 이유로 접속에 실패하면 “연결 끊김”이라고 나오니 설정을 확인하기 바란다.

![](/posts/post-1459/images/9-180x300.png)

VPN이 연결되면 스마트폰의 상단의 알림바에 열쇠 모양의 아이콘이 나타나며, 이를 선택하면 VPN 연결 정보와 송수신 패킷, 접속 시간 등을 확인할 수 있다. 접속을 종료하고할 경우는 “연결 끊기”를 선택하면 된다.

![](/posts/post-1459/images/윈도우-3-300x214.png)

SoftEther VPN의 세션 정보를 확인하면 그림과 같이 L2TP 프로토콜을 사용하여 접속한 사용자 정보를 확인할 수 있다.

이상으로 SoftEther VPN 서버에 스마트폰을 사용하여 VPN으로 접속하기 위한 서버 설정 및 클라이언트 설정 방법을 설명하였다.
