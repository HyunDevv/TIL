# typora 이전버전 사용하기

## Beta 지속 방법

아직 Typora를 충분히 사용하지 않아서 비용을 지불할지 결정 하지 못한 분들을 위해 Typora에서는 무료 평가를 제공 하고 있지만, 그래도 베타버전을 조금 더 오래 써보고 싶은 분들은 아래와 같이 최신 beta 버전을 설치 하고, hold 시키는 방법이 있습니다.

하지만 Typora가 충분히 본인스타일에 맞다는 확신이 있다면 비용을 지불하고 사용하는게 좋겠죠.

### Ubuntu

```zsh
sudo apt remove typora
sudo apt install typora=0.11.18-1
sudo apt-mark hold typora
# typora set on hold.
```

나중에 유료 구입 후 hold를 취소 할 때는 아래와 같이 입력 해 주세요.

```zsh
sudo apt-mark unhold typora
```

### MacOS

맥북에서는 마지막 Beta버전의 dmg 파일을 받아 설치 한 후에

> ![image-20220111150018623](https://raw.githubusercontent.com/Shane-Park/mdblog/main/news/typora-release.assets/image-20220111150018623.png)
>
> mac: https://typora.io/dev_release.html
>
> windows/Linux: https://typora.io/windows/dev_release.html

![image-20211208214912647](https://raw.githubusercontent.com/Shane-Park/mdblog/main/news/typora-release.assets/image-20211208214912647.png)

-  Check updates automatically 체크 박스를 해지하고

![image-20211208215037282](https://raw.githubusercontent.com/Shane-Park/mdblog/main/news/typora-release.assets/image-20211208215037282.png)

Software Upgrade 에서도 Automatically download and install updates in the future 체크를 해지하면 됩니다.

물론 비싼 가격이 아니니 계속 사용 할 예정이라면 구매하는게 좋습니다. 기능도 다양하게 추가 되고 있거든요.