# swift-style-guide
코딩 컨벤션을 작성하는 목적은  코드를 일관되게 작성하여 개발자 간에 서로의 코드를 더 잘 이해하기 위함입니다. [애플의 디자인 가이드 라인](https://swift.org/documentation/api-design-guidelines/)를 기본적으로 따르며, 이 문서는 현 프로젝트에 맞도록 개선하거나 보충한 것입니다. 새롭게 작성하는 코드는 컨벤션을 따라야 하지만, 이전에 작성한 코드는 시간 날 때 수시로 리팩토링을 하여 컨벤션을 준수할 수 있도록 합니다.

## 순서
[1. 코드 포맷팅](#코드-포맷팅)   
  1. 줄바꿈
  2. 띄어쓰기  
    
[2. 네이밍과 스타일](#네이밍과-스타일)   
  1. 공통
  2. 프로퍼티
  3. 메소드
  4. 약어
  5. 배열
  6. 클로저
  7. 프로토콜과 확장
  8. 열거형   
    
[3. 주석](#주석)   
   1. // MARK:-
   2. // MARK:
   3. ///
   4. //   
     
[4. 로그](#로그)


## 코드 포맷팅
### 1. 줄바꿈
-   코드가 길어질 경우 argument 단위로 줄바꿈을 해줍니다.
-   argument 단위로 줄바꿈을 할 때는 여는 괄호 이후 줄바꿈을 하되, 닫는 괄호 이전에는 줄바꿈을 하지 않습니다.
```swift
applyTypography(
	name: "default",
	isSubtitle: false,
	textMode: .edit,
	backgroundColor: .red)
```
- 단, 함수 정의부에서는 줄바꿈을 하지 않습니다.
```swift
func collectionView(_ collectionView: UICollectionView, numberOfItemsInSection section: Int) -> Int
```
- `if-let` 과 `guard-let` 구문에서 콤마(,)를 여러 번 두 번 이상 사용하는 경우 줄바꿈을 해주어야 합니다.
- `guard-let` 구문에서 줄바꿈을 해주었다면 `else` 이전에도 줄바꿈을 해주어야 합니다.
```swift
// Right
guard let video = video,
	let videoURL = video.remoteURL
	else { return }

// Wrong
guard let video = video, let videoURL = video.remoteURL else { return }
guard let video = video, let videoURL = video.remoteURL
	else { return }
```
- 가독성을 위한 함수 내 두 줄 이상 하지 않습니다.
- `//MARK:-`, `//MARK:` 이후에는 줄바꿈을 해야 합니다. 
- `MARK`로 구별된 코드블럭들 사이에는 빈 두 줄을 띄어야 합니다.
- 파일의 끝은 항상 빈 한 줄을 남깁니다.

### 2. 띄어쓰기
- 1개의 탭(tap)은 4개의 스페이스(space)이며, 들여쓰기는 항상 1탭을 기준으로 합니다.
- 콜론(:)을 사용할 때는 왼쪽은 붙여 사용하며 오른쪽엔 1개의 스페이스를 둡니다.
```swift
// Right
let size = CGSize(width: 10, height: 10)

// Wrong
let size = CGSize(width:10, height:10)
```
- 콤마(,) 를 사용할 때는 왼쪽은 붙이되 오른쪽엔 1개의 스페이스를 둡니다.
```swift
// Right
let result = [3, 1, 4, 2]

// Wrong
let result = [3,1,4,2]
```
- 여는 괄호는 줄바꿈을 하지 않습니다.
- 필요없는 공백은 제거합니다.
- 연산자의 전후로 1개의 스페이스를 두되, 여는 괄호 뒤와 닫는 괄호 전에는 스페이스를 두지 않습니다.
```swift
let width = viewWidth - (itemsPerRow -1) * 30
```

##  네이밍과 스타일
### 1. 공통
- 타입에는 PascalCase, 이외에는 CamelCase를 사용합니다.
```swift
class Music {
  /* ... */
}

let music = Music()
```
- `import`를 할 때는 애플에서 제공하는 프레임워크를 먼저 쓰고 한 줄을 띄운 다음 서드파티를 추가합니다. 알파벳 순서대로 추가해줍니다.
```swift
import UIKit

import Alamofire
import SwiftyJSON
```
- 객체를 생성할 때는 implicit member expression을 사용하지 않습니다.
```swift
// Right 
let size = CGSize(width: 10, height: 10)

// Wrong 
let size = CGSize.init(width: 10, height: 10) 
```
<br> 

### 2. 프로퍼티
- propertyObserver에 코드가 길어질 경우 함수로 분리합니다.
- boolean 값에 대해서는 is, should 로 시작합니다.
- 타입이 명확한 경우에는 명시하지 않습니다.
```swift
// Right
let music = Music()

// Wrong
let music: Music = Music()
```
- 프로퍼티 명으로 타입을 유추하기 어려운 경우 명시해줍니다.
```swift
// Right
let titleLabel: UILabel
let closeButton: UIButton
  
// Wrong 
let title: UILabel 
let close: UIButton 
```
<br>  

### 3. 메소드
- 함수명은 동사로 시작합니다.
- boolean 값에 대해서는 is, should 로 시작합니다.
- 리턴타입이 함수명에 포함되는 경우 get은 피하도록 합니다.
```swift
// Right
func user() -> User
  
// Wrong 
func getUser() -> User
```
- Action에 관한 함수는 주어 + 조동사 + 동사 + (목적어/보어) 형태로 작성합니다.
```swift
// Right
func cancelButtonDidTap()

// Wrong
func cancel()
func cancelTapped()
func cancelButtonTapped()
```
<br>  

### 4. 약어
- 약어는 대문자로 적되, 단어의 시작으로 사용될 때는 소문자를 사용합니다.
```swift
// Right
let urlString = URL(string: "...") 
let musicURL = URL(string: "...")
 
// Wrong 
let URLString = URL(string: "...")
let UrlString = URL(string: "...")
let musicUrl = URL(string: "...")
```

- 합의되지 않은 약어는 사용하지 않습니다.
```swift
// Right 
let view = UIView(frame: .zero) 
homeViewController.view.backgroundColor = .red

// Wrong 
let v = UIView(frame: .zero) 
homeVC.view.backgroundColor = .red 
```

<br>  

### 5. 배열
- index를  통해 배열에 접근 시, 배열의 범위를 벗어날 위험이 있는 경우 subscript을 이용하여 옵셔널 언래핑을 합니다.
```swift
if let music = musics[safe: 2] {
  // do something
}
```

<br>  

### 6. 클로저
- closure 내의 코드가 길어질 경우 함수로 분리합니다.

<br>  

### 7. 프로토콜과 확장
- 메소드의 첫 번째 argument의 네임 라벨은 작성하지 않습니다.
```swift
protocol MusicPickerDelegate {
  func selectMusic(_ music: Music)
}
```
- Foundation 프레임워크를 extension을 사용할 경우 Extensions 폴더에 파일을 추가해서 사용합니다.
- 클래스에서 프로토콜을 사용할 경우, 클래스 정의 부에 extension을 추가하지 않고 프로토콜 별로 분리해야 합니다.
```swift
// Right
// MARK: - HomeViewController
extension HomeViewController: UICollectionViewDataSource { /* ... */ }


// MARK: - HomeViewController
extension HomeViewController: UICollectionViewDelegate { /* ... */ }

// Wrong
extension HomeViewController: UICollectionViewDataSource, UICollectionViewDelegate { /* ... */ }
```
- 단, 프로토콜을 확장해서 이미 구현되어 있어 프로토콜을 채택한 클래스에서 별도로 구현할 사항이 없는 경우 분리하지 않습니다.
```swift
protocol PrintingDelegate: class {
  func print()
}

extension PrintingDelegate {
  func print() {
    // do something
  }
}

// Right
class HomeViewController: UIViewController, PrintingDelegate {
  /* ... */
}

// Wrong
class HomeViewController: UIViewController {
  /* ... */
}

extension HomeViewController: PrintingDelegate { }
```
- 채택한 프로토콜의 구현부가 100줄 이상인 경우 파일로 분리합니다. 파일명은 `클래스명+프로토콜명`으로 정합니다.

<br>  

### 8. 열거형
- 타입이 열거형으로 명확한 경우에는 타입을 명시하지 않습니다.
```swift
// Right
let direction: Direction = .left
view.backgroundColor = .red

// Wrong
let direction: Direction = Direction.left
view.backgroundColor = UIColor.red
```
- swift문에서는 모든 case를 작성하여 default는 사용하지 않습니다.
```swift
switch direction {
  case .left:
    // do something
  case .right:
    // do something
  case .up, down:
    // do something
}

// Wrong
switch direction {
  case .left:
    // do something
  case .right:
    // do something
  case default:
    // do something
}
```
<br>  

## 주석
- 개발을 위해 작성했거나 placeHolder로 존재하는 주석, 더 이상 사용되지 않는 코드는 주석 처리 하지 않고 반드시 삭제해야 합니다.
- 의미없는 코드로 인해 가독성이 떨어짐을 막기 위함입니다.
- C 스타일의 /* ... */는 사용하지 않습니다.
<br>  

### 1. //MARK:-
- 한 파일 내에서 프로토콜 여러 개를 채택하는 경우 `//MARK:-` 로 코드 분리해줍니다.
```swift
// Right
// MARK: - UICollectionViewDataSource
extension HomeViewController: UICollectionViewDataSource { /* ... */ }


// MARK: - UICollectionViewDelegate
extension HomeViewController: UICollectionViewDelegate { /* ... */ }

// Wrong
extension HomeViewController: UICollectionViewDataSource { /* ... */ }
extension HomeViewController: UICollectionViewDelegate { /* ... */ }
```

<br>  

### 2. //MARK: 
- life cycle, init, deinit, 이외 메소드들을 구분하기 위해 사용합니다.
- 이외 함수에서도 연관된 코드끼리 묶기 위해 사용합니다.
- 접근 레벨에 따라 property 분리를 위해 사용합니다.
```swift
class Music() {
  // MARK: public property
  let title: String
  let duration: Float

  // MARK: private property
  private var playCount: Int = 0

  // MARK: init
  init(title: String, duration: float) { /* ... */ }
  init(title: String) { /* ... */ }
}
```

<br>  

### 3. ///
- 문서 작성을 위한 주석처리를 합니다. 주로 함수나 변수 설명을 위해 사용합니다.
- 설명하고자 하는 코드의 윗줄에 작성합니다.
<br>  

### 4. //
- 코드를 위한 설명에 사용합니다.

<br>  

## 로그
- print(_)는 사용하지 않습니다. 대신에 `swift-log`를 사용합니다.
