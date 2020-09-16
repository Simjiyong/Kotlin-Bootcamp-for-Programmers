# 2. Kotlin basics

## Introduction

여기서는 Kotlin 프로그래밍 언어의 기본인 data type, operator, variable, control structure 그리고 nullable과 non-nullable 변수에 대해 알아본다.



## Learn about operators and types

### Step 1: Explore numeric operators

다른 언어와 마찬가지로 Kotlin은 +, -, *, / 연산자를 사용한다. Kotlin은 Int, Long, Double, Float과 같은 다양한 숫자 type도 지원한다.

```kotlin
1+1
res8: kotlin.Int = 2

53-3
res9: kotlin.Int = 50

50/10
res10: kotlin.Int = 5

1.0/2.0
res11: kotlin.Double = 0.5

2.0*3.5
res12: kotlin.Double = 7.0

1/2
res15: kotlin.Int = 0

1.0/2.0
res16: kotlin.Double = 0.5
```

연산 결과는 operands의 type을 유지한다.



Kotlin은 number를 primitive type으로 갖지만, object인 것처럼 숫자에 대한 메소드를 호출할 수 있다.

```kotlin
2.times(3)
res18: kotlin.Int = 6

3.5.plus(4)
res19: kotlin.Double = 7.5

2.4.div(2)
res20: kotlin.Double = 1.2
```

Boxing이라고 하는 wrapper 객체를 만들 수 있다. Boxing은 자동으로 이루어지며, 필요에 따라서 boxed and unboxed될 수 있다.



주의 : wrapper 객체는 primitive type보다 더 많은 메모리가 필요하다. 그래서 collection과 같이 꼭 wrapper 객체가 필요한 경우가 아니면 Boxing을 사용하지 않는 것이 좋다.



### Step 2: Practice using types

Kotlind은 숫자 type간에 암시적 변환을 하지 않는다.

short 값을 long 변수에 할당하거나 Byte를 Int에 할당할 수 없다.(auto casting이 안된다?) 

-> 암시적 숫자 변환은 프로그램 오류의 일반적인  원인이기 때문이다.

캐스팅을 통해 다른 type의 값을 할당할 수 있다.

```kotlin
val i: Int = 6
val b1 = i.toByte()
println(b1)
=> 6
```



```kotlin
val b2: Byte = 1
 println(b2)
1

val i1: Int = b2
error: type mismatch: inferred type is Byte but Int was expected
```

다음과 같이 auto casting이 되지 않아 error가 발생한다.

```kotlin
val i4: Int = b2.toInt()
println(i4)
1
```

이렇게 명시적으로 casting을 해야 값이 할당된다.

Kotlin은 긴 숫자 상수의 값을 더 읽기 쉽게 읽을 수 있도록 숫자에 밑줄을 표시할 수 있다.

```kotlin
val oneMillion = 1_000_000
val socialSecurityNumber = 999_99_9999L
val hexBytes = 0xFF_EC_DE_5E
val bytes = 0b11010010_01101001_10010100_10010010
```



### Step 3: Learn the value of variable types

Kotlin은 두 가지 타입의 변수를 지원한다. (val, var)

val을 사용하면 값을 한 번 할당할 수 있다. 다시 할당하려고 하면 error가 발생한다. 

var을 사용하면 값을 할당한 다음 나중에 프로그램에서 값을 변경할 수 있다.

```kotlin
var fish = 1
fish = 2
val aquarium = 1
aquarium = 2
error: val cannot be reassigned
```

변수에 저장하는 type은 컴파일러가 context로 부터 type을 알아낼 수 있을 때 지정된다. 원하는 경우에는 `:` notation을 사용해서 변수 type을 명시적으로 지정할 수 있다.

사용자나 컴파일러에 의해  type이 지정되면 type을  변경할 수 없다.



### Step 4: Learn about strings

Kotlin에서 String은 다른 프로그래밍 언의 stirng과 유사하게 `"`을 문자열에 `' ` 단일 character에 사용하고 `+`연산자로 문자열을 연결할 수 있다. `$variable` name은 변수에 들어있는 값을 나타내는 텍스트로 대체된다. 이를 variable interpolation이라고 한다.

```kotlin
val numberOfFish = 5
val numberOfPlants = 12
"I have $numberOfFish fish" + " and $numberOfPlants plants"
res10: kotlin.String = I have 5 fish and 12 plants
```

expression을 정의하려면 중괄호 `{}`을 사용한다.

```kotlin
"I have ${numberOfFish + numberOfPlants} fish and plants"
res11: kotlin.String = I have 17 fish and plants
```



## Compare conditions and booleans

Kotlin 프로그래밍 언어의 boolean과 checking condition에 대해서 알아본다.

다른 언어와 마찬가지로 Kotlin에서는 `<`, `==`, `>`, `!=`, `<=`, `>=`과 같은 boolean operator 및 boolean을 가지고 있다.

```kotlin
val numberOfFish = 50
 val numberOfPlants = 23
 if (numberOfFish > numberOfPlants) {
     println("Good ratio!")
 } else {
     println("Unhealthy ratio")
 }
Good ratio!
```

`if`문에서 range를 사용할 수 있다.

```kotlin
val fish = 50
if (fish in 1..100) {
    println(fish)
}
50
```

더 복잡한 조건의 경우 논리 연산자 `&&`와 `||`를 사용한다. 또 다른 언어와 마찬가지로 `else if`문을 사용할 수 있다.

```kotlin
if (numberOfFish == 0) {
     println("Empty tank")
 } else if (numberOfFish < 40) {
     println("Got fish!")
 } else {
     println("That's a lot of fish!")
 }
That's a lot of fish!
```

`when` 문을 사용할 수 있다. 다른 언어의 `switch`문과 같은 `when`문을 사용해서 Kotlin에서 `if`/`else if`/`else`문 을 대신해서 작성할 수 있다. `when`문의 조건도 range를 사용할 수 있다.

```kotlin
when(numberOfFish){
     0 -> println("Empty tank")
     in 1..39 -> println("Got fish!")
     else -> println("That's a lot of fish")
 }
That's a lot of fish
```



## Learn about nullability

nullable 변수와 non-nullable 변수에 대해 알아본다. null과 관련된 프로그래밍 error는 수많은 버그의 원인이 된다. Kotlin은 nullable이 아닌 변수를 도입해서 버그를 줄인다.

### Step 1: Learn about nullability

default로 변수는`null`이 될 수 없다.

```kotlin
var rocks: Int = null
error: null can not be a value of a non-null type Int
```

변수가 `null` 일 수 있음을 나타내려면 type 뒤에 `?` 연산자를 사용한다. 

```kotlin
var marbles: Int? = null
```



list와 같은 복잡한 데이터 type이 있을 때

- list의 element가 null이 되도록 허용할 수 있다.
- list가 null이 되도록 허용할 수 있지만, null이 아닌 경우 elements는 null이 될 수 없다.
- list나 element 모두 null이 되도록 허용할 수 있다.

### Step 2: Learn about the ? and ?: operators

 `if/else`문의 사용을 줄이기 위해 `?` 연산자를 사용해서 `null`을 테스트 할 수 있다. 

`fishFoodTreats` 변수가 `null`이 아님을 체크하는 방법

```kotlin
var fishFoodTreats = 6
if (fishFoodTreats != null) {
    fishFoodTreats = fishFoodTreats.dec()
}
```

`?` 연산자를 사용해 작성한 Kotlin 의 `null` 체크 방법

```kotlin
var fishFoodTreats = 6
fishFoodTreats = fishFoodTreats?.dec()
```

`?:` 연산자를 사용해서 `null` 테스트를 chain할 수도 있다.

```kotlin
fishFoodTreats = fishFoodTreats?.dec() ?: 0
```

위의 코드는 `fishFoodTreats`가 `null`이 아니면 decrement를 한 후 사용하고, `null`인 경우엔 `?:` 뒤의 value인 0을 사용한다는 의미다. 만약 `fishFoodTreats`가 `null`이면 `dec()` 메소드는 호출되지 않는다.

#### A point about null pointers

만약 `NullPointerException`을 정말 좋아한다면, Kotlin에서 사용할 수 있다. 

not-null assertion 연산자인 `!!` 연산자는 모든 값을 `null`이 아닌 type으로 변환하고 값이 `null`인 경우엔 exception을 throw 한다.

```kotlin
val len = s!!.length   // throws NullPointerException if s is null
```

일반적으로 `!!`연산자를 사용하는 것은 좋지 않다. 그러나 때로는 레거시 Java 코드를 다룰 때 `!!`연산자가 필요하다.



## Explore arrays, lists, and loops

array와 list에 대해 배우고 Kotlin 프로그래밍 언어로 loop를 만드는 다양한 방법을 배운다.



### Step 1: Make lists

list는 Kotlin의 기본 type이며 다른 언어의 lists와 유사하다.

```kotlin
val school = listOf("mackerel", "trout", "halibut")
 println(school)
[mackerel, trout, halibut]
```

`mutableListof`를 사용해서 변경할 수 있는 list를 만들 수 있다.

```kotlin
val myList = mutableListOf("tuna", "salmon", "shark")
 myList.remove("shark")
res19: kotlin.Boolean = true
```

item이 성공적으로 지워지면 `remove()`메소드는 `true`를 return 한다. 



_`val`로 정의된 list를 사용하면 변수가 참조하는 list을 변경할 수 없지만 list의 내용은 변경할 수 있다._



### Step 2: Create arrays

다른 언어와 마찬가지로 Kotlin에는 array가 있다. Kotiln의 list와는 다르게 Array는 `mutable`한 버전의 Array는 없다. Array를 생성하면 크기가 고정된다. 새로운 Array로 복사하는 경우를 제외하고는 element를 추가하거나 제거할 수 없다.

`arrayOf`를 사용해서 array를 생성할 수 있다.

```kotlin
val school = arrayOf("shark", "salmon", "minnow")
 println(java.util.Arrays.toString(school))
[shark, salmon, minnow]
```

`arrayOf`로 선언된 array에는 type association이 없기 때문에 type을 섞을 수있어서 유용하다. 

```kotlin
val mix = arrayOf("fish", 2)
```

모든 element에 대해 하나의 type으로 array를 선언할 수도 있다. 예를 들어, `intArrayOf()`를 사용해 정수 배열을 생성할 수 있다. 

```kotlin
val numbers = intArrayOf(1,2,3)
```

`+` 연산자를 사용해 array를 결합할 수 있다.

```kotlin
val numbers = intArrayOf(1,2,3)
val numbers3 = intArrayOf(4,5,6)
val foo2 = numbers3 + numbers
println(foo2[5])
3
```

Nested array와 list를 가질 수 있다. list의 element로 array가 올 수 도 있고 그 반대가 될 수도 있다.

```kotlin
val numbers = intArrayOf(1, 2, 3)
val oceans = listOf("Atlantic", "Pacific")
val oddList = listOf(numbers, oceans, "salmon")
println(oddList)
[[I@6cf58989, [Atlantic, Pacific], salmon]
```

Kotlin의 좋은 기능 중 하나는 array를 0으로 초기화하는 대신 코드로 초기화할 수 있다는 점이다.

```kotlin
val array = Array (5) {it * 2}
 print(java.util.Arrays.toString(array))
[0, 2, 4, 6, 8]
```

초기화 코드는 `{}`에서 정의한다. 코드에서 `it`는 0부터 시작하는 array의 index를 나타낸다.



### Step 3: Make loops

`for` loop를 사용해 array를 돌면서 element 를 print한다.

```kotlin
val school = arrayOf("shark", "salmon", "minnow")
 for (element in school) {
     print(element + " ")
 }
shark salmon minnow 
```

Kotlin에서는 element와 index를 동시에 사용할 수 있다. `.withIndex()`

```kotlin
for( (index, element) in school.withIndex()) {
     println("Item at $index is $element\n")
 }
Item at 0 is shark
Item at 1 is salmon
Item at 2 is minnow
```

step과 특정 range를 지정할 수 있다.  `downTo`를 사용해서 뒤로 이동할 수 있다.

```kotlin
for(i in 1..5) print(i)
12345

for(i in 5 downTo 1) print(i)
54321

for(i in 3..6 step 2) print(i)
35

for(i in 'd'..'g') print(i)
defg
```

다른 언어와 마찬가지로 Kotlin에는 `while`, `do...while` loop, `++`, `--`연산자가 있다. 또 Kotlin에는 `repeat` loop가 있다.

```kotlin
var bubbles = 0
 while (bubbles < 50) {
     bubbles++
 }
 println("$bubbles bubbles in the water\n")
 
 do {
     bubbles--
 } while (bubbles > 50)
 println("$bubbles bubbles in the water\n")
 
 repeat(2) {
     println("A fish is swimming")
 }
50 bubbles in the water
49 bubbles in the water
A fish is swimmingA fish is swimming
```

