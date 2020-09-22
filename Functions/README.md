# 3. Functions

## Introduction

여기서는 Kotlin의 function에 대해서 배운다. 

내용은 default values for parmeters, filters, lambdas and compact functions이 있다.



## Explore the main() function

Kotlin 프로그램을 만들고 main() function에 대해서 알아본다. 또 command line에서 프로그램에 인수를 전달하는 방법에 대해 알아본다.

`fun` 키워드와 함수 name을 사용해서 함수를 정의한다. 

다른 프로그래밍 언어와 마찬가지로 `()`는 argument를 위한 것이다. `{}`는 함수의 코드를 구성한다. 

### Step 1: Create a Kotlin file

### Step 2: Add code and run yout program

다른 프로그래밍 언어와 마찬가지로, Kotlin의 `main()`함수는 실행을 위한 entry point다. command line의 argument는 string 배열로 전달된다.

```kotlin
fun main(args: Array<String>) {
    println("Hello, world!")
}
```

_Kotlin 1.3부터 `main()`함수에 parameter를 사용하지 않으면, args를 정의하지 않아도된다._

이 함수는 return문이 없다. Kotlin의 모든 함수는 명시적으로 나타내지 않은 경우에도 무언가를 return한다. `main()`함수와 같은 함수는 `kotlin.Unit` type을 return한다. 이는 Kotlin에서 값이 없다고 말하는 것이다.

_함수가 `kotlin.Unit` return하면 명시적으로 나타낼 필요가 없다._



## Learn why (almost) everything has a value

Kotlin의 거의 모든 것이 값을 가지고 있는 이유와, 이것이 유용한 이유를 알아본다.

Kotlin에서는 거의 모든 것이 expression이고 값이 있다. 값이 `kotlin.Unit`인 경우에도 마찬가지다.

`println()`을 `isUnit` 변수에 할당하고 print 해본다. 

```kotlin
val isUnit = println("This is an expression")
println(isUnit)
```

처음 `println()`은 `"This is an expression"`을 print한다. 그리고 두 번째 `println()`은 첫 번째 println() 무의 값, 즉 `kotlin.Unit`을 출력한다.

```kotlin
This is an expression
kotlin.Unit
```



`isHot`변수에 `if`/`else`문의 결과 값을 할당한다. expression이므로 `if`문의 값을 바로 사용할 수 있다.

```kotlin
val temperature = 10
val isHot = if (temperature > 50) true else false
println(isHot)
```

```
false
```

 _Loop문은 예외다. `for`문과 `while`문은 값이 없다. Loop문의 값을 무언가에 할당하려고하면 컴파일에러가 발생한다._



## Learn more about functions

Kotline의 더 많은 함수와  `when`조건식에 대해 알아본다.

### Step 1: Create some functions

### Step 2: Use a when expression

`when` 문은 다른 프로그래밍 언어의 `switch`와 비슷하지만 각 분기의 끝에서 자동으로 break된다. 또 enum을 확인하는 경우 코드가 모든 분기를 포함하는지 확인한다.

```kotlin
fun fishFood (day : String) : String {
    var food = ""
    when (day) {
        "Monday" -> food = "flakes"
        "Tuesday" -> food = "pellets"
        "Wednesday" -> food = "redworms"
        "Thursday" -> food = "granules"
        "Friday" -> food = "mosquitoes"
        "Saturday" -> food = "lettuce"
        "Sunday" -> food = "plankton"
    }
    return food
}

fun feedTheFish() {
    val day = randomDay()
    val food = fishFood(day)

    println ("Today is $day and the fish eat $food")
}
```

`else` 를 사용해서 `when` 조건식에 default branch를 추가할 수 있다. 

default branch가 있으면 `food`가 return 되기 전에 값이 할당되므로 초기화 할 필요가 없다. 그래서 `food`에 문자열을 한 번만 할당하므로 `var` 대신 `val`을 사용해서 `food`를 선언 할 수 있다.

또, `when` 식의 값을 직접 return하도록 `food` 변수를 제거할 수 있다.

```kotlin
fun fishFood (day : String) : String {
    return when (day) {
        "Monday" -> "flakes"
        "Wednesday" -> "redworms"
        "Thursday" -> "granules"
        "Friday" -> "mosquitoes"
        "Sunday" -> "plankton"
        else -> "nothing"
    }
}
```



## Explore default values and compact functions

function과 method의 기본값에 대해서 알아본다. 또 코드를 더 간결하고 읽기 쉽게 만들고 테스트를 위한 code path의 수를 줄일 수 있는 compact function에 대해서도 알아본다. compact function은 single-expression 함수라고도 한다.

### Step 1: Create a default value for a parameter

Kotlin에서는 parameter 이름으로 argument를 전달할 수 있다. parameter에 기본 값을 지정할 수도 있다. caller가 argument를 제공하지 않으면 기본 값이 사용된다. 나중에 메소드(멤버 함수)를 작성할 때 동일한 메소드의 많은 오버로딩을 하지 않아도 된다.



`speed`라는 문자열 매개변수를 갖는 `swim()`함수이다. speed 매개변수의 기본값은 `"fast"` 이다.

```kotlin
fun swim(speed: String = "fast") {
   println("swimming $speed")
}
```

첫 번째는 기본값을 이용한 호출, 다음으론 name없이, 마지막으론 `speed`매개변수 이름을 사용한 호출이다.

```kotlin
swim()   // uses default speed
swim("slow")   // positional argument
swim(speed="turtle-like")   // named parameter

swimming fast
swimming slow
swimming turtle-like
```

_Argument는 매개변수 이름을 사용할 필요가 없다. 정의된 순서대로 인수를 전달할 수 있다. 그러나 기본값을 사용하면 조금 혼란스러울 수 있다. 그래서 기본 값이 없는 매개변수를 먼저 배치하고 기본 값이 있는 매개변수를 뒤에 배치하는 것이 좋다._

### 

### Step 2: Add required parameter

만약 매개변수에 기본 값이 지정되지 않은 경우 해당 인수는 항상 전달되어야한다.

```kotlin
fun shouldChangeWater (day: String, temperature: Int = 22, dirty: Int = 20): Boolean {
    return when {
        temperature > 30 -> true
        dirty > 30 -> true
        day == "Sunday" ->  true
        else -> false
    }
}
```

다음과 같이 `shouldChangeWater()`라는 함수가 있으면 `day` parameter는 기본 값이 없기 때문에 항상 argument가 전달 되어야한다.



### Step 3: Make compact functions

Compact function 또는 single-expression 함수는 Kotlin의 일반적인 패턴이다. 함수가 single-expression의 결과를 return할 때, `=` 기호 뒤에 함수 본문을 지정하고 `{}`를 생략하고 return 을 생략할 수 있다.

```kotlin
fun isTooHot(temperature: Int) = temperature > 30

fun isDirty(dirty: Int) = dirty > 30

fun isSunday(day: String) = day == "Sunday"
```

```kotlin
fun shouldChangeWater (day: String, temperature: Int = 22, dirty: Int = 20): Boolean {
    return when {
        isTooHot(temperature) -> true
        isDirty(dirty) -> true
        isSunday(day) -> true
        else  -> false
    }
}
```



### Defalut values

parameter의 기본 값은 값이 아니어도 된다. 다른 함수 일 수도 있다.

```kotlin
fun shouldChangeWater (day: String, temperature: Int = 22, dirty: Int = getDirtySensorReading()): Boolean {
	...
}
```

_기본 값으로 사용되는 함수는 런타님에 평가되므로 file read나 대용량 메모리 할당과 같은 비용이 많이 드는 작업을 함수에 넣으면 안된다. 이 작업은 함수가 호출될 때마다 실행되므로 프로그램 속도가 느려질 수 있다._



## Get started with filters

Kotlin의 filter에 대해서 알아본다. 필터는 특정 조건에 따라 list의 일부를 가져오는 편리한 방법이다.

### Step 1: Create a filter

```kotlin
val decorations = listOf ("rock", "pagoda", "plastic plant", "alligator", "flowerpot")
```

다음 decoration 에서 문자 'p'로 시작하는 decoration만 print해본다. 필터 조건에 대한 code는 `{}`안에 있으며 필터가 반복 될 때 `it`는 각 item을 나타낸다. 식이 true를 return하면, item이 포함된다.

```kotlin
fun main() {
    println( decorations.filter {it[0] == 'p'})
}
```

```
⇒ [pagoda, plastic plant]
```



### Step 2: Compare eager and lazy filters

결과 list는 즉시 생성될까? 아니면 list에 access할 때 생성될까?

Kotlin에서는 필요한 방식으로 정할 수 있다.(In Kotlin, it happens whichever way you need it to)?? 기본적으로 필터는 eager이며 필터를 사용할 때마다 list가 생성된다.

필터를 lazy로 만들려면 `Sequence`를 사용할 수 있다. `Sequence`를 사용하면 연산에 대해 lazy evaluation으로 처리하기 때문에 중간 과정에서 새로운 collection을 return하지 않으며, 결과값이 필요한 시점에 연산을 수행해서 최종 결과만을 return한다. 



```kotlin
fun main() {
    val decorations = listOf("rock", "pagoda", "plastic plant", "alligator", "flowerpot")
    
    val eager = decorations.filter { it[0] == 'p' }
    println("eager : $eager")

    // lazy, will wait until asked to evaluate
    val filtered = decorations.asSequence().filter { it[0] == 'p' }
    println("filtered: $filtered")
    
    // force evaluation of the lazy list
    val newList = filtered.toList()
    println("new list: $newList")
}
```



```
eager : [pagoda, plastic plant]
filtered: kotlin.sequences.FilteringSequence@34b7bfc0
new list: [pagoda, plastic plant]
```

`eager`에는 filter된 list가 생성되어 할당된다.

`Sequence`의 `asSequence()`를 사용해서 필터를 계산한다. 그리고 `filtered` 변수에 sequence를 할당한다. 

filter 결과를 `Sequence`로 return할 때, `filtered`변수는 새 list를 갖지 않는다. `filtered`변수는 list element의 `Sequence`와 해당 element에 적용할 filter의 대한 정보를 갖고있는다. 이후에, `Sequence`의 element에 접근할 때, filter가 적용되고 결과가 return된다.

`toList()`를 사용해서 sqeunce를 List로 변환해서 force evaluation을 한다.



Sequence와 lazy evaluation에서 진행되는 작업을 시각화하려면 `map()`을 사용한다. `map()`함수는 sequence의 각 element에 대해 간단한 변환을 수행한다.

```kotlin
    val lazyMap = decorations.asSequence().map {
        println("access: $it")
        it
    }

    println("lazy: $lazyMap")
    println("-----")
    println("first: ${lazyMap.first()}")
    println("-----")
    println("all: ${lazyMap.toList()}")
```

```
lazy: kotlin.sequences.TransformingSequence@52af6cff
-----
access: rock
first: rock
-----
access: rock
access: pagoda
access: plastic plant
access: alligator
access: flowerpot
all: [rock, pagoda, plastic plant, alligator, flowerpot]
```

element에 접근하면 `println()`을 호출하는 `map()`을 적용한 sequence를 `lazyMap`변수에 할당한다.

`lazyMap`을 print하면 sequence에 대한 reference만 print된다.

first element를 print하면 첫 번째 element에만 access한다.

sequence를 list로 변환하면 모든 element에 접근한다.



```kotlin
    val lazyMap2 = decorations.asSequence().filter {it[0] == 'p'}.map {
        println("access: $it")
        it
    }
    println("-----")
    println("filtered: ${lazyMap2.toList()}")
```

```
-----
access: pagoda
access: plastic plant
filtered: [pagoda, plastic plant]
```

`map()`을 적용하기 전에 원래 `filter()`를 적용해 새로운 sequence를 만들어 print하면 `println()`은 access되는 element에 대해서만 호출된다.



## Get started with lambdas and higher-order functions

Kotlin의 lambda와 higher-order function에 대해서 알아본다.



### Lambdas

기존 named function외에 Kotlin은 lambda를 지원한다. lambda는 함수를 만드는 식(expression)이다. 그러나 named function대신 이름이 없는 함수를 선언한다. 이 것이 유용한 이유 중 하나는 lambda식을 데이터로 전달할 수 있다는 점이다. 다른 언어에서 lambda는 익명 함수, 함수 리터럴 등으로 알려져있다.



### Higher-order functions

lambda를 다른 함수에 전달해서 고차 함수(higher-order function)을 만들 수 있다. 이 전에 썼던 `filter`도 고차 함수 중 하나이다. 조건으로  `filter`하기 위해서 lambda 식을 사용했다. `{ it[0] == 'p' }`

또, `map`도 고차 함수이며 전달한 lambda식은 적용할 변환이었다.



### Step 1: Learn about lambdas

named function과 마찬가지로, lambda는 매개변수를 가질 수 있다. lambda의 경우 매개 변수(와 type)는 `->` 왼쪽에 있다.  실행할 코드는 `->` 오른쪽에 위치한다.  lambda가 변수에 할당되면 함수처럼 호출 할 수 있다.

```kotlin
var dirtyLevel = 20
 val waterFilter = {dirty : Int -> dirty / 2}
 println(waterFilter(dirtyLevel))
10
```

여기서 lambda는 `dirty`라는 `Int` 매개변수를 받아서 `dirty / 2`를 return 한다.



함수 type에 대한 Kotlin 문법은 lambda에 대한 문법과 관련이 있다. 

```kotlin
val waterFilter: (Int) -> Int = { dirty -> dirty / 2 }
```

`waterFilter`변수는 `Int`를 parameter로 갖고 `Int`를 반환하는 모든 함수가 될 수 있다.

lambda는 dirty 인자를 2로 나눈 값을 반환한다.`

lambda의 type 추론에 의해 계산되므로 더이상 람다의 argument type을 지정할 필요가 없다.



### Step 2: Create a higher-order function

lambda의 진정한 힘은 lambda를 사용해서 한 함수에 대한 인수가 다른 함수인 고차 함수를 만드는 것이다.

다음은  두 개의 argument를 사용하는 함수의 예다. 첫 번째 argument는 integer이다. 두 번째 인수는 integer를 매개변수로 하고 integer를 return 하는 함수이다.

```kotlin
fun updateDirty(dirty: Int, operation: (Int) -> Int): Int {
   return operation(dirty)
}
```

`updateDirty()`함수는 두 번째 인수로 전달된 함수를 호출하고 첫 번째 인수를 함께 전달한 값을 return한다.

```kotlin
val waterFilter: (Int) -> Int = { dirty -> dirty / 2 }
println(updateDirty(30, waterFilter))

15
```

전달하는 함수가 lambda일 필요는 없다. 대신 named function일 수 있다. 인수를 일반 함수로 지정하려면 `::` 연산자를 사용한다. 이렇게 하면 Kotlin은 함수 호출을 하지 않고, argument로 함수의 reference를 전달한다. 

```kotlin
fun increaseDirty( start: Int ) = start + 1

println(updateDirty(15, ::increaseDirty))
⇒ 16
```



Kotlin은 함수를 사용하는 모든 매개 변수가 마지막 매개 변수인 것을 선호한다. 고차 함수로 작업 할 때 Kotlin에는 **last parameter call syntax**라는 특수한 구문이 있다. 이 경우, lambda를 괄호안에 넣지 않고 함수의 매개변수로 전달할 수 있다. 

```kotlin
var dirtyLevel = 19;
dirtyLevel = updateDirty(dirtyLevel) { dirtyLevel -> dirtyLevel + 23}
println(dirtyLevel)
⇒ 42
```

