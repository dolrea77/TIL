# 코틀린 기초 



## 오버로딩 조건

- 같은 스코프 내에서 같은 이름의 함수를 쓸 수 있는 것이 오버로딩 
- 함수의 이름이 같더라도 함수의 패러미터 수가 달라지거나 패러미터의 자료형이 달라져도 다른 함수처럼 사용 가능하다 
- 패러미터의 이름이 다르고 자료형과 패러미터의 수가 같다면 오버로딩이 되지 않음 



```kotlin
fun main(){
    read(7)
    read("Hi")
}

fun read(x: Int){
    println("숫자 $x 입니다")
}

fun read(x: String){
    println(x)
}
```





## 기본값 함수

* 패러미터가 없을 때 기본값으로 동작하려고 할 때는 default arguments를 사용한다
* 파라이터 중간값을 기본값으로 지정하고 나머지는 원하는 파라미터를 쓴다고 하면 named arguments를 사용한다



```kotlin
fun main(){
    
    deliveryItem("짬뽕")
    deliveryItem("책", 3)
    deliveryItem("노트북", 30, "학교")
    //중간 파라미터인 개수는 기본값, 마지막 파라미터인 도착지를 원하는 값으로 넣을시 도착지에 값을 넣는다는 것을 지정함
    deliveryItem("선물", destination = "친구집") 
    
}
fun deliveryItem(name: String, count: Int = 1, destination: String = "집"){
    println("${name}, ${count}개를 ${destination}에 배달하였습니다")
}
```



## vararg

* 같은 자료형을 개수에 상관없이 패러미터로 받고 싶을 때 variable number of arguments를 사용 
* vararg는 개수가 지정되지 않은 패러미터라는 특징이 있으므로 다른 패러미터와 사용시 제일 뒤에 나와야 한다 



```kotlin
fun main(){
    sum(1,2,3,4)
}

//vararg 로 선언된 변수는 배열처럼 for로 꺼내쓸 수 있다 
fun sum(vararg numbers: Int){  
    var sum = 0
    
    for(n in numbers){
        sum += n
    }
    print(sum) 
}
```



## infix 함수

- 연산자처럼 사용할 수 있음 
- 함수 이름 형식 : infix함수가 적용될 자료형.이름 



```kotlin
fun main(){
    //6 : infix 함수가 적용되는 객체 자신 
    //4 : 패러미터 x  
    println(6 multiply 4)
    println(6.multyply(4))
}
infix fun Int.multiply(x: Int):Int = this * x
```





