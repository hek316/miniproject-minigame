# miniproject-minigame
메가 IT 아카데미 미니 JAVA 프로젝트





# 1.프로젝트 주제

본 프로젝트는 **' HappyFarm '**은  농장게임으로  씨앗을 심고 농작물을 키워서 수확하는 게임이다.

다음과 같은 요구사항을 만족할 수 있도록 구현하는 것을 목표로 진행하였다.  

### [ 요구 사항 ]

- 로그인과 회원가입

- 씨앗을 선택 후 밭 클릭시 씨앗이 심어지는 그래픽

- 씨앗마다 각각의 시간흐름을 가지고 그래픽 변화 

- 다 자란 농작물을 수확 시 경험치 증가를 표시 
- 일정 시간동안에만 씨앗 생성 시간 감소 
- 수확시기까지의 남은 시간을 표시
- 마우스 이벤트 구현
- 밭 확장 버튼
- 알림 메세지

- 사용자의 게임을 저장하고 불러오기 
- 효과음 추가   



# 2. 사용된 프로그램 정보

- JDK 11.0.9
- IDE : 이클립스





# 3.게임 소개

Happy Farm 게임은 초보농부인 당신을 위한 농촌체험 가이드를 해주는 게임으로 
씨앗을 심고 물을 주고 밭을 확장하는 게임입니다
상세기능은 아래에 적혀있습니다 

### [ Happy Farm 기본적인 진행 방법 ]

- 회원가입을 하고 로그인을 한다.
- 메뉴 버튼 중 씨앗 심기 버튼을 클릭하여 씨앗의 종류 중 하나를 선택한다.
- 선택한 뒤 밭을 클릭하여 씨앗을 심는다.
- 씨앗이 성장하여 농작물로 수확이 가능할 때 수확한다.



### [ 경험치와 코인 얻는 방법 ]

- 수확 시 해당 씨앗마다 정해진 경험치를 얻을 수 있다.
- 수확 시 해당 씨앗마다 정해진 코인을 얻을 수 있다.
- 씨앗이 일정시간마다 코인을 자동으로 얻는다.
  이때, 씨앗의 레벨이 높을수록 얻을 수 있는 코인은 증가한다.



### [ 메뉴 버튼 설명 ]



![menu](https://user-images.githubusercontent.com/81146596/119937477-cfc21e00-bfc5-11eb-8672-1b0151a21990.png)




#### 씨앗 심기 

- 씨앗의 종류로는 토마토, 벼, 가지 3가지가 존재한다.
- 씨앗의 레벨(Lv), 가격(Price), 소요되는 시간, 수확시 얻는 경험치와 코인(Earned Exp / Coin), 현재 수확량(Current yield),
  업그레이드 조건 수확량(Next yield) 정보를 보여주며 실시간으로 갱신해준다.  
- Buy 버튼을 통해 씨앗 중 한가지를 선택할 수 있다.
- Upgrade 버튼을 통해 씨앗 레벨을 올린다.



#### 물 주기

- 성장시간을 일정 시간동안 빠르게 단축시켜주는 기능을 한다.
- Buy 버튼을 통해 구매하면 영구적으로 사용할 수 있다.
- Use 버튼을 통해 사용할 수 있다.
- 한 번 사용하면 해당 시간 동안 모든 밭에 시간 단축 효과를 부여한다.



#### 밭 확장

- 씨앗을 심을 수 있는 밭의 개수를 확장한다.
- 유저의 레벨과 30,000 coin을 만족하면 확장시킬 수 있다.
- 밭을 구매하면 다음 밭 확장 구매 버튼이 나타난다.



# 4.시연영상

<div>
   <a href="https://www.youtube.com/watch?v=WVEriE9FcNM" target="_blank"><image src = "https://img.youtube.com/vi/WVEriE9FcNM/mqdefault.jpg"></a>   

</div>


# 5. 프로젝트의 특장점 



### 1.더블 버퍼링 기술 구현 

-  비디오 메모리만을 사용한 싱글 버퍼링으로 그래픽을 그릴 경우 데이터를 저장하는 동안에는 다음 그림의 데이터를 전송할 수 없기 때문에 지우고 그리고 지우고 그리고 할 경우 필연적으로 발생하는 깜빡임, 찢어짐 등의 상황을 막기 위해서 사용되는 기법

```JAVA
// 더블 버퍼링으로 한번에 그려주기 
public void paint(Graphics g) {
    menuImage = createImage(400, main.SCREEN_WIDTH);
    screenGraphic = menuImage.getGraphics();
    screenDraw(screenGraphic);// 이미지 그려주기
    g.drawImage(menuImage, 0, 0, null);

}

// 배경 색 설정
public void screenDraw(Graphics g) {
    if (isMainScreen) {
        g.setColor(new Color(0xfd, 0xff, 0xc2));// 배경이미지 노랑색으로 설정
        g.fillRoundRect(0, 0, 400, 720, 5, 5);// 둥근네모 그리기
    } else {
        g.setColor(new Color(242, 242, 194));// 배경이미지 노랑색으로 설정
        g.fillRoundRect(0, 0, 400, 720, 5, 5);// 둥근네모 그리기
    }
    paintComponents(g);// 하위 구성요소에 대해 페인트 호출
    this.repaint();// update() 메소드 자동호출

}
```



### 2.콜백 함수 구현

- 물 주기의 Use 버튼을 한 번 눌렀을 때 실행되도록 하여, 이미 시간 단축이 진행되고 있을 때를 막기 위해 사용했다.
- 

```java
// FarmingPanel 부분
private SkillTimer th; 

void runWaterSkill(int skillLevel) {
		if (th == null) {
			SoundsClip.play(SoundsClip.SUCCESS_SOUND);
			th = new SkillTimer(seeds, skillLevel, this);
			new Thread(th).start();
	         FarmerMessage.getSkillUseMsg(skillLevel);
		}
}

public void callback() {
    th = null;
}
```

```java
// SkillTimer 부분

private FarmingPanel farmingPanel;

public SkillTimer(FarmingPanel farmingPanel, Seeds[][] seeds, int level) {
		this.seeds = seeds;
		this.farmingPanel = farmingPanel;
		setWaterLevel(level);
		setBuff(level);
}

@Override
public void run() {

    try {
        for(int i = 0; i < buffTime/1000; ++i) {
            changeTimeReduction(timeReduction);
            Thread.sleep(1000);
        }
    } catch (InterruptedException e) {
        e.printStackTrace();
    } finally {
        changeTimeReduction(1000); // 1초로 다시 바꾼다.

    }
    farmingPanel.callback();

}
```



### 3. 멀티 스레드 구현

- 각 밭에 심는 씨앗의 성장을 나타내기위한 위한 스레드
  : 씨앗마다 요구되는 성장 시간이 다르고  언제 씨앗을 심었는지에 따라 시간이 달라야하기 때문에 사용했다.

- 일정 시간 동안만 성장 시간을 빠르게 단축시키기 위한 스레드
  :  일정 시간만 효과를 주기위한 제한을 걸기위해 사용했다.
- 배경 음악을 반복시키기 위한 스레드 
  : main문이 종료되면 같이 종료되도록 하기위해 데몬 스레드를 사용했다.

```java
// StartFrame의 일부분

private Thread bgm;

StartFrame() {	
	bgm = new Thread(this);
    bgm.setDaemon(true);
    bgm.start();
}

@Override
	public void run() {
		while(true) {
			try {
				SoundsClip.play(SoundsClip.BACKGROUND_MUSIC);
				Thread.sleep(112000);
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
		}
}
```



씨앗을 심을 수 있는 조건을 확인한 뒤 심을 수 있는 조건일 때  `Seeds`형 변수를 생성하여 쓰레드를 `start()` 한다.

씨앗의 시간 감소를 위해 TimerSkill 

```java
// Seeds 의 run() 일부분
@Override
public void run() {

    try {

        System.out.println(row+"/"+col);
        farmingPanel.fields[row][col].setVisible(false); // 밭 표시 x
        harvestCheck = false; // 수확 불가능

        while(leftTimeInMillis > 0) {

            remainingTimeLabel.setText(getRemainingTime(leftTimeInMillis));
            path = String.format("image\\%s_0%d.png", seedName,(((timeGrow-leftTimeInMillis)/ timeGrowInterval)+1));

            repaint();
            if(leftTimeInMillis % timeAuto == 0 && leftTimeInMillis != timeGrow) { // timeAuto마다 코인 증가 
                farmingPanel.calculateCoin(coinAuto);
            }
            Thread.sleep(1000); 
            leftTimeInMillis -= 1000;

    }
}
```



### 4. HashMap을 이용한 게임 데이터 저장 구현





# 6.어려웠던 점 및 극복 방법



1.  게임 구현중 마우스클릭시 **비동기 처리**가 필요하였는데 스레드를 돌리기에는 너무 비효율적이라서 어려움을 겪고 있었습니다. 그러다 **콜백함수**를 알게되었고 다른 클래스의 함수를 마우스 클릭시 비동기 방식으로 실현할수 있게 되었습니다. 전달된 콜백함수는 콜백함수를 포함한  함수 내부인자에 접근이 가능하고 심지어 전역변수에도 접근이 가능한 상태가 되어서 덕분에 마우스 리스너 기능 및  다른 비동기 처리도 수월히 처리하였습니다. mainFrame 을 기준으로  인자값을 주고 받았다.
2.  **유저의 게임 정보를 저장하기 위해  보조스트림을 통해 `HashMap<String, Object> ` 에 `put()`하여 데이터를 넣었다.**
    어떤 밭에 어떤 씨앗이 자라고 있는지, 얼마나 자랐는지를 저장하는 과정에서 처음에는 씨앗의 현재 정보를 가진 Seeds형의 **이차배열을 그대로 넣으려고 했다.**
    그런데  **`NotSerializableException` 이 발생하는 문제가 발생했다.** 문제를 해결하기위해 처음에는 클래스가 직렬화 되어있지 않아서라 판단하여 오류가 발생하는 클래스에 `implements Serializable` 을 추가했다. 하지만 계속해서  `NotSerializableException` 가 발생하여  해당 씨앗의 이름은 **`String[]**`으로 시간과 밭의 위치는 `int[][]`, 마지막 저장시간은 `long`  으**로 저장하는 방법을 사용하여 문제를 해결**했다. 정확한 원인을 파악하지는 못했지만 Serializable 구현이 누락된  것으로 생각된다.
3.  코인과 유저레벨이 공통으로 사용된다고 판단하여 **static으로 선언**했다가  **main 의 콜백 함수로 인자값을 전달** 해 주었다.
4.  버튼 객체를 생성자에 생성해주고 함수를 만들어 마우스 리스너를 붙여주었는데 클릭 할때마다 한 객체의 여러개의 리스너가 붙는 오류가  발견되었다. if button.getMouseListeners().length == 1) 의 조건문을 이용하여 오류를 해결해 주었고 앞으로는 관련된 객체와 기능을 잘 분류하여 정리하였야겠다는 다짐을 하였다





# 7. 앞으로 개선할 것들 

- 시간상의 여유로 DB연동을 하지 못하여 현재는 버퍼 입출력과 파일 입출력을 통해 `.dat` 확장자로 저장하며 회원 가입 기능만 존재한다.
  회원가입과 로그인을 할 때, DB를 연동하여 DTO와 DAO를 통해 회원에 대한 정보를 저장/삭제하는 기능을 추가하면 회원관리를 원활하게 할 수 있을 것이다.
- 현재 코인을 얻을 수 있는 방법에는 시간제약이 많기 때문에 추가로 미니게임을 넣어 코인을 얻을 기회를 추가하면 좋을 것 같다.
- 시간 단축 기능을 하는 물주기의 효과 시간이 어느정도 남았는지 표시해주면 유저가 따로 씨앗의 시간 감소를 확인하거나 Use버튼을 계속 누를 필요가 없어져 편할 것이다.
- 콜백함수에 인터페이스를 선언하여 실행 시점과 구현 시점을 다르게 하여  코드의 종속성을 줄이고 유지보수성을 높혀준다
- mvc 모델 구현@ 수정



# 8. Javadoc

