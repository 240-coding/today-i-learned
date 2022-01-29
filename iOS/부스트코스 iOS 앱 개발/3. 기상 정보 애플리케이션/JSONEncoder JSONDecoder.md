# JSONEncoder / JSONDecoder

스위프트 4 버전 이전에는 `JSONSerialization` 을 사용해 JSON 타입의 데이터를 생성했다. 그러나 스위프트 4 버전부터 JSONEncoder / JSONDecoder가 `Codable` 프로토콜을 지원하기 때문에 JSONEncoder / JSONDecoder 와 `Codable` 프로토콜을 사용해 손쉽게 JSON 형식으로 인코딩 및 디코딩할 수 있다. 즉, JSONEncoder 및 JSONDecoder를 사용해 스위프트 타입의 인스턴스를 JSON 데이터로 인코딩, JSON 데이터에서 스위프트 타입의 인스턴스로 디코딩할 수 있다.

# JSONEncoder

Codable 프로토콜을 준수하는 `GroceryProduct` 구조체의 인스턴스를 JSON 데이터로 인코딩하는 방법

```swift
struct GroceryProduct: Codable {
	var name: String
	var points: Int
	var description: String?
}

let pear = GroceryProduct(name: "Pear", points: 250, description: "A ripe pear.")

let encoder = JSONEncoder()
encoder.outputFormatting = .prettyPrinted // 들여쓰기를 통해 가독성이 좋게 출력해준다

do {
	let data = try encoder.encode(pear)
	print(String(data: data, encoding: .utf8)!)
} catch {
	print(error)
}

// -----출력
{
	"name": "Pear",
	"points": 250,
	"description": "A ripe pear."
}
```

# JSONDecoder

JSON 데이터를 `Codable` 프로토콜을 준수하는 `GroceryProduct` 구조체의 인스턴스로 디코딩하는 방법

```swift
struct GroceryProduct: Codable {
    var name: String
    var points: Int
    var description: String?
}

// 스위프트 4 버전부터 """를 통해 여러 줄 문자열을 사용할 수 있다.
let json = """
{
	"name": "Durian",
	"points": 600,
	"description": "A fruit with a distinctive scent."
}
""".data(using: .utf8)!

let decoder = JSONDecoder()

do {
	let product = try decoder.decode(GroceryProduct.self, from: json)
	print(product.name)
} catch {
	print(error)
}
// ----- 출력
"Durian"
```

### 💡 T.Type이 뭘까?

```swift
func decode<T>(_ type: T.Type, from: Self.Input) throws -> T where T : Decodable
```

`decode()` 의 원형은 다음과 같다. 여기서 `T.Type` 은 인스턴스가 아닌 타입 자체를 가리킨다.

자세한 내용 참조: [https://stackoverflow.com/questions/47836341/what-is-t-type-in-swift](https://stackoverflow.com/questions/47836341/what-is-t-type-in-swift)