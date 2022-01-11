# Target-Action 디자인 패턴

iOS 환경에서 많이 사용하는 디자인 패턴 중 하나. Target-Action 디자인 패턴에서 객체는 이벤트가 발생할 때 다른 객체에 메시지를 보내는 데 필요한 정보를 포함한다. **액션**은 특정 이벤트가 발생했을 때 호출할 메서드를 의미하고, **타겟**은 액션이 호출될 객체를 의미한다. 이벤트 발생 시 전송된 메시지를 **액션 메시지**라고 하고, 타겟은 프레임워크 객체를 포함된 모든 객체가 될 수 있으나, 보통 컨트롤러가 되는 경우가 일반적이다.

### 왜 Target과 Action을 지정하고 디자인 패턴으로 활용하는 걸까?

같은 메서드가 여러 클래스에 정의되어 있는 경우도 있고, 그런 클래스의 인스턴스가 여러 개인 상황도 있다. 이런 여러 가지 상황에서 우리가 원하는 객체를 Target으로 지정하면 액션을 실행할 객체를 상황에 따라 선택할 수 있다.

### 액션 메서드

액션 메서드는 특정한 양식이 필요하다. IBAction은 인터페이스 빌더가 메서드를 인지할 수 있도록 해준다. 스위프트 언어를 활용한 프로그래밍 방식에서 `@objc` 는 Swift 클래스를 사용하는 Objective-C 코드가 있거나 Objective-C 유형의 메서드를 사용하는 경우 필요하다.

# 컨트롤 이벤트

## 컨트롤 이벤트와 액션과의 관계

UIKit에는 UIButton, UISwitch 등 UIControl을 상속받은 다양한 컨트롤 클래스가 있다. 그런 컨트롤 객체에 발생한 다양한 이벤트 종류를 특정 액션 메서드에 연결할 수 있다. 즉, 컨트롤 객체에서 특정 이벤트가 발생하면 미리 지정해둔 타겟의 액션을 호출하게 된다.

## 컨트롤 이벤트의 종류

컨트롤 이벤트는 `UIControlEvents` 라는 타입으로 정의되어 있다.

- touchDown
- touchDownRepeat
- touchDragInside
- touchDragOutside
- touchDragEnter
- touchDragExit
- touchUpInside
- touchUpOutside
- touchCancel
- valueChanged
- primaryActionTriggered
- editingDidBegin
- editingChanged
- editingDidEnd
- editingDidEndOnExit
- allTouchEvents
- allEditingEvents
- applicationReserved
- systemReserved
- allEvents
