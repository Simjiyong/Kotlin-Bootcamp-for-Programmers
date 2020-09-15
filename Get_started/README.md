# 1. Get started

## Benefits of Kotlin

**Kotlin**은 프로그래머가 프로그래머를 위해 만든 새롭고 현대적인 프로그래밍 언어이다. 

명확성, 간결성 및 코드 안정성에 중점을 둔다.

- Robust code
- Mature platform
- Cocise, readable code
- Interoperable with Java

### Robust code

**Kotlin** 제작자는 프로그래머가 robust code를 만들 수 있도록 언어에 대한 다양한 디자인 결정을 내렸다. 예를 들어, 소프트웨어에서 *Null Pointer Exception*은 재정적 손실과 엄청난 컴퓨터 충돌을 일으키며 수많은 디버깅 시간을 초래했다. 그래서 Koltin은 nullable과 non-nullable 데이터 유형을 구분해서 컴파일 타임에 더 많은 오류를 잡아낼 수 있다. 

**Kotlin**은 strongly type이며 코드에서 type을 유추하는데 많은 역할을 한다. lambda, coroutine, property가 있어서 더 적은 버그와 코드를 더 짧게(less code with fewer bugs) 작성할 수 있다.



### Mature platform

**Kotlin**은 2011년부터 시작되었으며 2012년에 오픈 소스로 출시되었다. 2016년 버전 1.0을 출시하고 2017년부터 Kotlin은 Android 앱 빌드를 위한 공식적으로 지원하는 언어가 되었다. 



### Concise, readable code

Kotlin으로 작성된 코드는 매우 간결하고 언어는 getter, setter와 같은 boilerplate code를 제거하도록 설계되었다. 

예를 들어, 다음과 같은 Java 코드는

```java
public class Aquarium {

   private int mTemperature;

   public Aquarium() { }

   public int getTemperature() {
       return mTemperature;
   }

   public void setTemperature(int mTemperature) {
       this.mTemperature = mTemperature;
   }

   @Override
   public String toString() {
       return "Aquarium{" +
               "mTemperature=" + mTemperature +
               '}';
   }
}
```

Kotlin에서는 이렇게 간결하게 작성될 수 있다.

```kotlin
data class Aquarium (var temperature: Int = 0)
```

Kotlin은 적당한 boilerplate code를 사용해 간결하게 유지하면서 가독성을 보장하도록 설계되었다.



### Interoperable with Java

Kotlin 코드는 Java와 Kotlin 코드를 함께 사용하고 즐겨찾는 Java 라이브러리를 계속 사용할 수 있도록 컴파일된다. 기존 Java 프로그램에 Kotlin 코드를 추가하거나 프로그램을 완전히 migration하려는 경우 IntelliJ IDEA와 Android Studio 모두 기존 Java 코드를 Kotlin 코드로 migration하는 도구를 포함한다.

