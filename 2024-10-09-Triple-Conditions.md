# Fastest triple condition

Keyboard апп хөгжүүлэх явцад гарсан код болон судалгаа шинжилгээний товчлолоо бичиж байгаа билээ. Энэ удаа код дээр тулгарсан нэг асуудлаа хуваалцъя. 

Хэрэглэгч хоёр үсэг дараалан эсвэл зэрэг дарах үед товч эхний үсгийг эгшиг эсэхийг шалгана, том болон жижиг үсэг байж болно, хоёр дахь үсэг `й/ы` дээр дарагдсан эсэхийг шалгана, ингээд хэрвээ эхний үсэг Эгшиг байгаад хоёр дахь үсэг `й/ы` дээр дарагдсан бол `Й` үсэг шивэгдэж бусад тохиолдолд `Ы` үсэг шивэгдэх шаардлага тавигдсан. 

```swift
// version 0 - Хэтэрхий удаан O(20) 
let vowels = Array("аоөүэияеюАОӨҮЭИЯЕЮ")
let ys = Array("иы")
func isVowels(_ letter: Character) -> Bool {
  return vowels.contains(letter.lowercased())
}
func isY(_ letter: Character) -> Bool {
  return ys.contains(letter.lowercased())
}
```

Уг 3 шалгалтыг асар богино хугацаанд гүйцэтгэх шаардлагатай болж байгаа. Эхний хувилбар нь цуваанаас хайлтыг гүйцэтгэх бөгөөд зөвхөн жижиг үсгээр тулгана. 

```swift
// version 1 - Хэтэрхий удаан O(10)
let vowels = Array("аоөүэияею")
let ys = Array("иы")
func isVowels(_ letter: Character) -> Bool {
  return vowels.contains(letter.lowercased())
}
func isY(_ letter: Character) -> Bool {
  return ys.contains(letter.lowercased())
}
```

Өмнөхийг бага зэрэг хурдасгах арга бол, `ЙЫ` тэй ойрхон эгшгийг эрэмбийн хойш, хол эгшгийг эрэмбийн урагш байрлуулах юм. Учир нь үои үсгүүд баруун эрхий хуруу, бусад нь зүүн эрхий хуруунд оногдож байгаа нь `үои` болон `йы` товчны зэрэг дарагдах магадлалыг өсгөж байгаа юм. 

```swift
// version 2 - Өмнөхийг бодвол хол эгшгийг хурдан илрүүлнэ, гэхдээ үнэтэй шийдэл O(10)
let vowels = Array("оүиюеаөэя")
let ys = Array("иы")
func isVowels(_ letter: Character) -> Bool {
  return vowels.contains(letter.lowercased())
}
func isY(_ letter: Character) -> Bool {
  return ys.contains(letter.lowercased())
}
```

Үүнийг O(1)-д багтаах арга байна. 

```swift
// final version - Ганц үйлдлээр өмнөх 3 үйдлийг шалгаж, гүйцэтгэж дуусгана O(1)
let vowels: [String: String] = [
  "а": "й",
  "о": "й",
  "у": "й",
  "ү": "й",
  "э": "й",
  "ө": "й",
  "и": "й",
  "е": "й",
  "я": "й",
  "ю": "й",
  "А": "Й",
  "О": "Й",
  "У": "Й",
  "Ү": "Й",
  "Э": "Й",
  "Ө": "Й",
  "И": "Й",
  "Е": "Й",
  "Я": "Й",
  "Ю": "Й",
]
func writeY(_ letter: String) -> String {
    let otherY: String = letter.allSatisfy(\.isUppercase) ? "Ы" : "ы"
    return vowels[letter] ?? otherY
}
```
