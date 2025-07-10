# 1. TEST 코드 작성 시 충돌

## 1.1 핵심 에러 내용

- JPA metamodel must not be empty

- 실제 스프링 부트


```kotlin

CLASS NAME 1. Test 클래스에서 사용하는 @WebMvcTest

        @WebMvcTest(
            controllers = [TodoController::class]
        )

// SPRING BOOT RUN 되는 클래스

@SpringBootApplication
@EnableJpaAuditing
class KtTodoApplication

fun main(args: Array<String>) {
    runApplication<KtTodoApplication>(*args)
}

```

@EnableJpaAuditing 어노테이션이 등록되면 스프링 테스트에서 해당 BEAN을 읽지만,
@WebMvcTest에 JPA가 포함되어 있지 않기 때문에 에러가 발생함. <br>
이런 케이스가 많다보니 스프링 자체에서는 Application 스타트 클래스에는
환경 설정을 넣지 않는 것을 권장함. <br>
대신 @Configuration 어노테이션을 사용해서 따로 JpaConfiguration 클래스를 만드는 것을 권장. 

2. 참고

[JPA EnableJpaAuditing](https://giron.tistory.com/127)
