# Throwable

Throwable 클래스는 예외처리를 할 수 있는 최상위 클래스이다. Exception과 Error는 Throwable의 상속을 받는다.

> 에러: 시스템 레벨에서 발생하여, 개발자가 어떻게 조치할 수 없는 수준을 의미 ex: JVM OOM

> 예외: 개발자가 구현한 로직에서 발생하며, 개발자가 미리 조치를 치할 수 있다.

![img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F99E8073E5A41F0C80C)

# Exception

![img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F99C85A375A41F0FF31)

예외의 2가지 종류

1. Checked Exception: 컴파일 오류
    1. 반드시 코드에서 처리해야 하는 예외
2. Unchcked Exception: 런타임 오류, 실행 후 알 수 있는 예외
    1. Runtime Exception → NullPinterException, IndexOutOfBound Exception
