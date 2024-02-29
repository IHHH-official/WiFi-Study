# Wifi-Study
# project

### Installing Kali Linux as a VM on Apple Mac OS

프로젝트 진행에 맞게 사용자화된 칼리 리눅스이미지를 다운받자. 아래 링크로 접속하여 link2라고 되어있는 걸 설치한다. 다운로드하면 kali를 가상머신으로 사용가능하다.

[Download Custom Kali - zSecurity](https://zsecurity.org/download-custom-kali/)

아래부터 kali 리눅스를 vmware에 설치하는 과정을 보여주겠다.

![Untitled](project%201a10e99f9a2144feb77ac6ee80e3d377/Untitled.png)

z는 아카이브다. 더블클릭해서 압축 해제 

![Untitled](project%201a10e99f9a2144feb77ac6ee80e3d377/Untitled%201.png)

upgrade

![Untitled](project%201a10e99f9a2144feb77ac6ee80e3d377/Untitled%202.png)

I copied it 클릭

![Untitled](project%201a10e99f9a2144feb77ac6ee80e3d377/Untitled%203.png)

enter하면 리눅스 자동 실행되며 로그인 요청이 된다.

![Untitled](project%201a10e99f9a2144feb77ac6ee80e3d377/Untitled%204.png)

기본적으로 `username : root`, `password : toor` 이다.

![Untitled](project%201a10e99f9a2144feb77ac6ee80e3d377/Untitled%205.png)

칼리 리눅스 배경화면이 떴다. 이 환경에는 해킹에 사용되는 도구들이 이미 준비되어있게 설정된 세팅이다. 

vmware에서 설정에 들어가자.

![Untitled](project%201a10e99f9a2144feb77ac6ee80e3d377/Untitled%206.png)

network adapter에 들어가면

![Untitled](project%201a10e99f9a2144feb77ac6ee80e3d377/Untitled%207.png)

네트워크 사용하지 않게 되어있다.

이 설정은 **내 호스트 컴퓨터**가 **라우터**가 될 가상 네트워크를 생성한다. 

모든 가상 머신은 이 네트워크(호스트 컴퓨터)에 연결된 클라이언트가 된다. 동시에 모든 가상 머신은 동일한 가상 네트워크에 연결된다. 가상머신끼리 통신할 수 있고 우리는 칼리 머신을 통해 다른 머신을 해킹할 수 있다.

가상머신은 이더넷 네트워크에 연결되어있지만 실제로는 호스트 시스템에 연결됨

칼리 리눅스 사용 방법

1) ctrl+alt+위 아래로 멀티 데스크 쓸 수 있음

2) wired connected : NAT 네트워크를 사용하기 때문에 유선 네트워크 연결되어있다고 봄

![Untitled](project%201a10e99f9a2144feb77ac6ee80e3d377/Untitled%208.png)

### 10. Connecting a Wireless Adapter To Kali

무선 어댑터 : USB ⇒ wifi 네트워크와 통신 가능

컴퓨터에는 대부분 무선 카드가 내장되어있으나 wifi나 무선 어댑터를 해킹하는데 적합하지 않다. 

무선카드에는 없지만 우리가 해킹하는데 필요한 무선어댑터 mode들

- monitor mode
- packet injection
- AP mode

위의 도구들을 사용하는 chipset을 가진 무선 어댑터를 사용해야한다. 그 chipset의 종류에는 `RealTek RTL8812AU`, `Atheros AR971` 이있다.

![Untitled](project%201a10e99f9a2144feb77ac6ee80e3d377/Untitled%209.png)

우리는 실습을 위해 위 상품을 구매했다.

칼리 리눅스를 실행시킨 다음 USB 연결하면 아래와 같이 뜨고, 파란 버튼을 클릭해주면된다.

![Untitled](project%201a10e99f9a2144feb77ac6ee80e3d377/Untitled%2010.png)

ifconfig : 이 컴퓨터에 연결된 모든 네트워크 인터페이스를 나열한다.

![Untitled](project%201a10e99f9a2144feb77ac6ee80e3d377/Untitled%2011.png)

- eth0는 vmware에서 생성한 가상 이더넷 인터페이스이고
- lo는 가상 NAT 네트워크를 통해 머신 연결하기 위해 Linux에서 사용되는 가상 루프백 인터페이스다.
- 나머지 wlan0는 위의 명령어를 사용하면 우리가 연결한 usb 무선 어댑터다. 내가 연결한 무선 어댑터의 이름은 wlan0인걸 확인할 수 있다.

### 11. What is MAC Address & How To Change It

- 네트워크 카드는 고유한 주소인 Mac 주소를 갖는다. 동일한 맥 주소를 가지는 두 개의 장치는 없다.
- mac 주소는 네트워크 내에서 장치를 식별하고 장치 간에 데이터 전송하는데 사용한다.

<aside>
💡 mac 주소 바꾸는 이유

1) 익명성

2) impersonate other devices

3) bypass filter : 장치 연결을 방지하거나 허용하기 위해 필터에 많이 사용됨

</aside>

네트워크 인터페이스 : 우리가 네트워크에 연결할 수 있게 해주는 모든 장치 ex. wifi 카드 or 이더넷 카드

[mac 주소 바꾸는 방법]

1) `ifconfig wlan down` : 인터페이스 비활성화

2) `ifconfig wlan0 hw ether 00:11:22:22:44:55` : 하드웨어 주소 정해서 변경

3) `ifconfig wlan0 up` : 인터페이스 활성화

4) `ifconfig` 로 변경된 mac 주소 확인. 메모리 주소만 변경하는거라 컴퓨터 껐다키면 다시 돌아옴

### 12. Wireless Modes - Managed & Monitor Mode Explained

무선에서는 패킷이 공중에서 전달되니 dest mac 주소 없이 캡처 가능하다. 

- `iwconfig` : 무선 인터페이스를 볼 수 있는 모든 인터페이스를 나열하는 ifconfig 확인
- `mode: managed` 로 되어있으면 이 장치가 대상 Mac을 Mac 주소로 갖는 패킷만 캡쳐하는 것. 기본적으로 managed로 세팅되어있다. 아래 사진과같이 iwconfig를 했을 때 확인 가능하다.
    
    ![Untitled](project%201a10e99f9a2144feb77ac6ee80e3d377/Untitled%2012.png)
    
    Managed를→ monitor mode 로 바꿔 범위 내에만 있으면 캡처할 수 있다.
    

[monitor 모드로 바꾸는 방법]

1) `iwconfig`

2) `ifconfig wlan0 down`

3) `airmon-ng check kill`

4) `iwconfig wlan0 mode monitor`

5) `ifconfig wlan0 up`

![Untitled](project%201a10e99f9a2144feb77ac6ee80e3d377/Untitled%2013.png)

방법대로 실행하면 monitor mode로 바꾼걸 확인할 수 있다.

### 13. Sniffing Basics - Using Airodump-ng

`airodump-ng` 은 패킷 캡처하는 프로그램이다.

- 모니터 모드여야하고, 우리 주변의 모든 무선 네트워크를 볼 수 있다.
- mac 주소, 채널, 암호화, 클라이언트 알려준다.

[사용 방법]

1) `iwconfig`

2) `airodump-ng wlan0`

명령어를 사용하면 아래와 같이 계속 뭐가 뜨게된다. ctrl+c 로 중지할 수 있다.

![Untitled](project%201a10e99f9a2144feb77ac6ee80e3d377/Untitled%2014.png)

한 줄마다 캡처되는 패킷들이고, 한 줄 안에서는 차례대로 아래의 내용을 우리에게 알려주는 것이다.

- BSSID: mac주소
- PWR: 신호 강도
- Beacons: 비콘으로 네트워크 존재를 보로드캐스트하기 위해 네트워크에서 보낸 프레임이다. 숨겨져있어도 기본적으로 브로드캐스트한다는 특징이 있다.
- #Data: 데이터수
- #/s: 과거 수집한 데이터 패킷 수
- CH: 네트워크 작동 채널
- MB: 네트워크가 지원하는 최대 속도
- ENC CIPTHER AUTH: 암호화
- ESSID: 네트워크이름이다.

우리 집에서는 iptime06 이름을 가진 wifi를 사용하는데 맨 아래 줄에 잡힌 게 보인다.

### 14. WiFi Bands - 2.4Ghz & 5Ghz Frequencies

네트워크 대역은 신호를 브로드캐스트하는데 사용할 수 있는 주파수를 정의한다.

airodump 도구를 사용했을 때 네트워크의 모든 클라이언트가 표시되지 않는 경우 라우터가 브로드캐스트 중일 수 있다. 그래도 안 보이면 5기가헤르츠 이상을 방송하고 있을 수 있다.

[주파수 정해서 패킷 캡처하는 방법]

1) `airodump-ng --band a wlan0`

![Untitled](project%201a10e99f9a2144feb77ac6ee80e3d377/Untitled%2015.png)

필터링해서 얼마 안 보인다.

band는 여러 개 설정도 가능하다. abg로 해서 2.4 및 5GHz 주파수 모두에서 데이터를 캡처하도록 지시하려면 `airodump-ng -—band abg mon0` 이렇게 사용한다.

### 15. Targeted Sniffing Using Airodump-ng

패킷 캡처본을 저장하고싶다면 저장하고싶은 패킷의 bssid와 channel을 기억해서 아래의 명령어에 적어준다.

1) `airodum-ng —bssid F8:23:B2:B9:50:A8 —channel 2 —write test wlan0`

⇒ test-01.cap 파일에 저장됨

2) `wireshark`

wireshark로 패킷 분석 할 수 있따.

### 16.Deauthentication Attack (Disconnecting Any Device From The Network) D 인증 공격

이 공격을 통해 네트워크에 연결하기 전에 모든 네트워크에서 모든 장치의 연결을 끊을 수 있으며, 네트워크의 비밀번호 모른채로 airplay 도구를 사용해서 router인 척 연결이 끊겨졌다고 어댑터에게 전달하자

1) `airodump-ng` 로 데이터 찾기

2) 1번째 터미널 창 보면서 mac 주소 참고하며 새로운 터미널창 열어서 `aireplay-ng —deauth 10000000 -a [Mac주소 BSSID] -c [클라이언트 Mac 주소 STATION] (-D : 5Ghz 이상일 때) mon0` (아직 enter x)

10000000 : 인증 패킷의 개수. 많이 보내서 두 라우터 모두에게 계속 보낼 수 있게함

3) 1번째 터미널 창에서 `airodump -ng —bssid F8:23:B2:B9:50:A8 —channel 2 mon0` 으로 검색 

4) 2번째 터미널 창에서 이제 enter

그러면 원래 내 컴퓨터가 연결되던 네트워크가 끊긴 것을 확인할 수 있다. 인터넷 들어가도 연결이 안된다.

이 부분에서 해커들이 할 수있는 행동이 있다.

⇒ 제조업체인척 client한테 전화해서 고쳐주겠다고하며 백도어를 제공해줄 수 있거나 가짜 엑세스 포인트를 연결해서 감시가능하다.

### 17. Discovering Hidden Networks

숨겨진 네트워크는 이름과 ESSID를 숨기지만, channel과 BSSID는 그대로 브로드캐스팅함

- 문제점 : 패스워드 크랙 시도를 못한다.
- 해결 : Airodump-ng는 네트워크가 활성화되면 Essid는 찾아낼 수 있다.

네트워크가 숨겨져있으면 host com에서 wifi로 Hidden Network에 연결하려할 때 이름을 적으라한다. 하지만 우리는 이름을 모르니 연결이 안되는 것이다.

숨겨진 네트워크는 이름을 가지고있지만 공중에 broadcast하지는 않아 우리가 볼 수 없는 것이다.

1) `airodump-ng wlan0`

![Untitled](project%201a10e99f9a2144feb77ac6ee80e3d377/Untitled%2016.png)

<length:   0> 이 숨겨진 네트워크다. 이 네트워크의 BSSID와 CH를 사용해서 이름을 알아내자.

2) `airodump-ng --bssid B4:A9:4F:05:F8:9D --channel 6 wlan0`

enter 하니

![Untitled](project%201a10e99f9a2144feb77ac6ee80e3d377/Untitled%2017.png)

오 난 숨겨진 이름이 떴다. 복사해서 notion에 붙여넣기하니까 “국민바이오2_2G” 라고한다.

나는 네트워크에 연결되어있는 wifi라 이름이 바로나왔는데 만약 연결이 되어있지 않으면 아래 그 네트워크에 연결하는 client와의 연결을 잠깐 끊어서 공중으로 이름을 던진 걸 우리가 캡처해오면된다.

그 방법은 아까 d-auth와 유사하다. 아래 적겠다.

3) 새 터미널 창을 연다

4) `aireplay-ng —deauth 4 -a B4:A9:4F:05:F8:9D -c FE:54:37:01:49:11 wlan0`

우리는 잠깐 연결을 끊을거니까 보내는 패킷수를 임의의 작은 숫자 4로 보낸다.

### 18. Connecting To Hidden Networks

1) 다시 wlan0를 네트워크에 연결하기위해 managed모드로 바꾼다.

2) kali linux applications에 들어가 settings>network에 들어간다.

안되면 터미널에 `service network-manager start`

그래도 안되면 reboot

![Untitled](project%201a10e99f9a2144feb77ac6ee80e3d377/Untitled%2018.png)

kali linux 안에서의 설정에서 Network 설정에 들어갔을 때 이 창이 뜨면 된다.

![Untitled](project%201a10e99f9a2144feb77ac6ee80e3d377/Untitled%2019.png)

오른쪽 맨 위 …을 눌러 숨겨진 네트워크에 연결하자.

![Untitled](project%201a10e99f9a2144feb77ac6ee80e3d377/Untitled%2020.png)

우리가 찾아낸 숨겨진 네트워크 이름을 입력하여 연결한다.

![Untitled](project%201a10e99f9a2144feb77ac6ee80e3d377/Untitled%2021.png)

근데 난 연결 실패했다. 숨겨진 네트워크를 내가 설정한 게 아니라 정말 외부의 것을 연결하려해서 이 네트워크가 무슨 wifi-security를 사용하고있는지 모르고 비번도 있는지 몰라서 그런거 같다.

---

### 19. Bypassing Mac Filtering (Blacklists & Whitelists)

개방형 네트워크가 연결하지 못하게 하는 것 중 하나는 mac filtering하는 것이다.

라우터가 mac filtering을 써서 allow/deny devices한다.

mac filtering 방법

1) blacklist : blacklist에 나열된 모든 네트워크 장치 차단 ⇒ mac 주소 바꾸면 우회 가능

2) whitelist : 리스트에 있는 특정 장치만 연결 가능

아래는 whitelist 우회하는 방법을 알려주겠다

1) `airodump-ng wlan0`

2) `airodump-ng —bssid [mac주소] —channel 6 wlan0`

### 20. Cracking Sections Introduction

지금까지는 네트워크 연결없이 진행했던 것이다. 연결 가로채서 보내는 모든것을 알 수 있었다.

이제는 암호화를 사용하는 경우 암호화 해제하고 wifi 네트워크에 액세스 하는 방법을 공부할거다. + WEP, WPA, WPA2 키를 얻는 것까지

### 21. Theory Behind Cracking WEP

RC4 의 알고리즘을 사용하여 데이터를 보낸다.

client → router 에게 보내는 패킷은 key로 암호화한다. 

라우터는 key가 있으니까 암호화된걸 해석할 수 있다. 

공중으로 전송되는 각 패킷은 새로운 고유 키를 생성 ⇒ 임의의 24비트 초기화 벡터 생성(실제 키에 대한 네트워크 비밀번호에 추가)

키 스트림을 생성한 다음 이 키 스트림을 사용하여 패킷을 암호화

패킷에 초기화 벡터(IV)를 추가하는 이유

- 패킷 해독하기 위해 키와 IV가 필요.
- 근데 이미 라우터는 키가 있음
- IV만 보내면됨

근데 알고리즘이 문제가 있다. IV는 24bit라서 보안 취약

### 22. WEP Cracking - Basic Case

WEP는 많은 수의 IV를 캡처하면 24bit라 알 수 있다.

1) `airodump-ng` 도구 사용하여 여러 packets/IVs를 캡처

2) IV들을 `aircrack-ng` 도구를 사용하여 분석하고 key를 크랙

방법

우린 많은 수의 패킷을 캡처해야하기 때문에 WEP 암호화를 사용하며 패킷을 많이 보내는 바쁜 네트워크를 골라

1) airodump-ng —bssid F8:23:00:00:00:00 —channel 1 —write basic_wep wlan0

2) 다른 터미널을 열어 `ls`로 cap 파일 확인

3) aircrack-ng basic_wep-01.cap

하면 Opening basic_wep-01.cap 

Read 32093 packets

라면서 마지막에 KEY FOUND! [ **41:73:32:33:70** ] (ASCII: As23p) 

로 열쇠를 찾아준다.

우리는 [] 대괄호 안에 있는 key를 : 을 제거한 4173323370이 비밀번호인 걸 확인할 수있다. 실제로 Host에서 wep로 암호화된 네트워크 wifi를 연결할 때 4173323370를 password로 입력하면 연결된다.

### 23. Associating With Target Network Using Fake Authentication Attack

그 전에는 WEP의 암호를 알아낼 때 패킷을 많이 전달하는 바쁜 네트워크를 기준으로 비밀번호를 알아냈으나, 이번에는 네트워크가 바쁘지 않은 경우 어떻게 할 지 알아보자. 

바쁘지 않은 경우 데이터의 수가 늦게 증가하며 키를 해독할 수 있는 충분한 데이터가 확보되기 전까지는 기다려야한다. 

⇒ 해결방법 : AP(Access Point)가 새로운 IVs를 사용하여 새로운 패킷을 생성하도록 강제하는 것이다. 

근데 AP는 연결된 클라이언트랑만 통신하니까 우리는 우선 AP와 연결해야한다. 여기서 타겟 네트워크와 연결하고 다음에 연결된 네트워크에 패킷을 주입하는 것을 함께 해보자.

세 개의 cmd창을 연다.

1) 1번째 창에서 `airodump-ng —bssid 64:16:F0:EC:7B:F3 —channel 6 —write arplreplay wlan0` enter

2) 2번째 창에서 `ifconfig` 하여 내 무선 어댑터 wlan0의 unspec 뒤의 mac 주소를 가져온다. 48-5D-60-2A-45-25-… 으로 되어있을텐데 12개만 가져오고 중간에 -대신 :을붙여줘야한다.

3) 3번째 창에서 `aireplay-ng —fakeauth 0 -a 64:16:F0:EC:7B:F3 -h 48:5D:60:2A:45:25 wlan0`  enter. 우린 가짜인증 공격을 할 거고, 한 번만 실행하기위해 0 사용, -a로 대상 네트워크의 mac 주소 지정 -h 로 무선 어댑터의 mac 주소를 지정하고 mac주소를 가져옴

4) 그럼 1번째 창에서 우리가 접근하려한 대상 네트워크 AUTH가 OPN으로 공개된게 확인된다. 그리고 아래에 나의 무선 어댑터가 연결된게 보인다. 이제 이 네트워크와 통신할 수 있다.

새로운 IV를 사용하여 새로운 패킷을 생성하도록 강제하여 키를 해독하게하자.

### 24. ARP Request Reply Attack

트래픽에 패킷을 주입하여 액세스 포인트가 생성되도록 한다. 새로운 IV가 포함된 새 패킷이 있고 데이터 수가 빠르게 증가하여 WEP 네트워크를 크랙할 수 있다.

- ARP 패킷을 기다린다
- 캡처하고 replay하여 AP가 새로운 IV를 생성해 다른 패킷에게 주게한다.
- 우리가 key를 crack할만큼 충분한 IVs를 가질 때까지 반복한다.

1) 아까 그대로 2번째 창에서 `aireplay-ng --arpreplay -b 64:16:F0:EC:7B:F3 -h 48:5D:60:2A:45:25 wlan0` enter

2) 3번째 창에서 `aircrack-ng arpreplay-01.cap` enter

또 KEY FOUND! 해서 대괄호 안에 있는 것을 사용하면된다.

와이파이 비밀번호를 탈취하는 방법까지 프로젝트에서 공부할 수 있었다. 외부 와이파이를 연결하면 해커들이 수행할 수 있는 사항들에 대해 정리해보자.

1. **데이터 가로채기 (Man-in-the-Middle 공격)**: 해커가 와이파이 네트워크를 도청하여 사용자가 송수신하는 데이터를 가로챌 수 있다. 이를 통해 로그인 정보, 금융 정보, 개인 메시지 등을 탈취할 수 있다.
2. **피싱 공격**: 해커가 가짜 웹 페이지나 이메일을 통해 사용자의 개인 정보를 훔치려고 시도할 수 있다. 이를 통해 사용자는 암호나 금융 정보를 노출시킬 수 있다.
3. **악성 코드 삽입**: 해커가 와이파이 트래픽을 이용하여 악성 코드를 주입할 수 있다. 사용자의 장치에 악성 소프트웨어가 설치되면 해커가 해당 장치를 제어하거나 사용자의 개인 정보를 탈취할 수 있다.
4. **네트워크 리소스 남용**: 해커가 와이파이에 연결된 모든 장치의 대역폭을 사용하여 네트워크 성능을 저하시킬 수 있다. 이는 사용자들에게 불편을 주고 시스템을 마비시킬 수 있다.
5. **액세스 포인트 위장 (Evil Twin 공격)**: 해커가 실제와 유사한 외관을 가진 가짜 액세스 포인트를 생성하여 사용자를 유인하고 개인 정보를 탈취할 수 있다.
6. **DoS/DDoS 공격**: 해커가 와이파이 네트워크에 대량의 트래픽을 보내거나 장치를 공격하여 네트워크를 마비시킬 수 있다.

이러한 위협으로부터 보호하기 위해서는 안티바이러스 및 방화벽 소프트웨어를 설치하고 업데이트하는 등의 조치를 취해야한다. 또한, 공개 와이파이 네트워크를 사용할 때는 주의해야 하며, 가능하면 가상 사설 네트워크(VPN)를 사용하여 데이터를 암호화하는 것이 좋다.
