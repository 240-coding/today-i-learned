# 싱글턴(SingleTon)

싱글턴은 ‘특정 클래스의 인스턴스가 오직 하나임을 보장하는 객체’를 의미한다. 싱글턴은 애플리케이션이 요청한 횟수와 관계없이 이미 생성된 같은 인스턴스를 반환한다. 애플리케이션 내에서 특정 클래스의 인스턴스가 딱 하나만 있기 때문에 다른 인스턴스들이 공유해서 사용할 수 있다.

# Cocoa 프레임워크에서의 싱글턴 디자인 패턴

싱글턴 인스턴스를 반환하는 팩토리 메서드나 프로퍼티는 일반적으로 `shared` 라는 이름을 사용한다.

### 🤔 팩토리 메서드?

팩토리 메서드 패턴은 객체지향 디자인 패턴이다. Factory method는 부모 클래스에 알려지지 않은 구체 클래스를 생성하는 패턴이며, 자식 클래스가 어떤 객체를 생성할지 결정하는 패턴이기도 하다. 부모 클래스 코드에 구체 클래스 이름을 감추기 위한 방법으로도 사용한다. (위키백과)

이름 그대로 무언가를 생산하는 공장을 떠올리자.

참고자료: [https://gdtbgl93.tistory.com/19](https://gdtbgl93.tistory.com/19)

### 싱글턴 디자인 패턴을 활용하는 대표적인 클래스

- FileManager
    - 애플리케이션 파일 시스템을 관리하는 클래스
    - `FileManager.default`
- URLSession
    - URL 세션을 관리하는 클래스
    - `URLSession.shared`
- NotificationCenter
    - 등록된 알림의 정보를 사용할 수 있게 해주는 클래스
    - `NotificationCenter.default`
- UserDefaults
    - Key-Value 형태로 간단한 데이터를 저장하고 관리할 수 있는 인터페이스를 제공하는 데이터베이스 클래스
    - `UserDefaults.standard`
- UIApplication
    - iOS에서 실행디는 중앙제어 애플리케이션 객체
    - `UIApplication.shared`

# 주의할 점

싱글턴 디자인 패턴은 객체가 불필요하게 여러 개 만들어질 필요가 없는 경우에 많이 사용한다. (예: 환경설정, 네트워크 연결처리, 데이터 관리 등) 하지만 멀티 스레드 환경에서 동시에 싱글턴 객체를 참조하는 경우 원치 않은 결과를 가져올 수 있다. 디자인 패턴을 사용할 때는 항상 긍정적인 면과 위험성을 함께 고려해서 사용할 것!

---

# StackView

## UIStackView

스택뷰는 여러 뷰들의 수평 또는 수직 방향의 선형적인 레이아웃의 인터페이스를 사용할 수 있도록 해준다. 스택뷰와 오토레이아웃 기능을 활용하여 디바이스의 방향과 화며크기에 따라 동적으로 적응할 수 있는 사용자 인터페이스를 만들 수 있다. 

스택뷰의 레이아웃은 스택뷰의 `axis` , `distribution` , `alignment` , `spacing` 과 같은 프로퍼티로 조정한다.

스택뷰는 `arrangedSubviews` 프로퍼티에 스택뷰에 포함된 뷰들을 관리한다. 이 프로퍼티는 순서가 있는 배열과도 같다. 스택뷰에 포함된 뷰의 순서가 레이아웃에 영향을 미친다.

스토리보드에서 스택뷰에 뷰를 추가하는 것은 코드상에서 `func addArangedSubview(UIView)` 메서드를 호출하는 것과 같다.

## UIStackView 클래스의 주요 프로퍼티

- var arrangedSubviews: [UIView]: 스택뷰의 정렬된 뷰의 배열. 스택뷰에 포함된 뷰들을 이 프로퍼티에 저장하고 관리한다.
- var axis: UILayoutConstraintAxis: 레이아웃의 방향을 결정한다.(vertical, horizontal)
- var distribution: UIStackViewDistribution: 스택뷰에 포함된 뷰가 스택뷰 내에서 어떻게 배치될지 결정한다.
- var spacing: CGFloat: 스택뷰에 정렬된 뷰들 사이의 간격을 결정한다.

## UIStackView 클래스의 주요 메서드

- func addArrangeSubview(UIView): arrangedSubviews 배열의 마지막 요소에 뷰를 추가한다.
- func insertArrangedSubview(UIView, at: Int): arrangedSubview 배열의 특정 인덱스에 뷰를 추가한다.
- func removeArrangedSubview(UIView): 스택뷰의 arrangedSubviews 배열로부터 뷰를 제거한다.
