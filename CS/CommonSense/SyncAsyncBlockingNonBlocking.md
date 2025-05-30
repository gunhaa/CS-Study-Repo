# Synchronized, Asynchronized, Blocking, Non-Blocking

![images1](images/sync1.png)

## Synchronized & Asynchronized

- Synchronous의 Syn는 그리스어로 '함께'이란 뜻이고 chrono는 '시간'이라는 뜻이다
- 즉, Synchronous는 작업 시간을 함께 맞춰서 실행한다
- Asynchronous(!함께 시간)는 요청한 작업에 대해 완료 여부를 따지지 않기 때문에 자신의 다음 작업을 그대로 수행한다.
- 동기 작업은 요청한 작업에 대해 순서가 지켜지는 것을 말하는 것이고, 비동기 작업은 순서가 지켜지지 않는 것을 말한다.
- 동기(sync) 방식은 실행의 주도권이 하나의 스레드에 고정되어 있고, 해당 작업이 완전히 끝날 때까지 다음 작업은 절대 실행되지 않는다.
- 비동기(Async) 방식은 실행 주도권을 잠시 반납하고, 이벤트 루프나 백그라운드가 처리한 후, 나중에 다시 이어받아 실행되는 구조이다.

## js의 await

-  JavaScript와 같은 싱글스레드 환경에서는 async와 await가 블로킹처럼 보일 수 있지만, 실제로는 블로킹되지 않는다. await이 있으면 해당 스레드(js는 싱글스레드)의 작업은 멈추고 비동기 작업이 이벤트 루프에서 처리된다
- await으로 멈춘 async함수는 백그라운드 스레드가 처리하고, 콜스택이나 이벤트큐에 아무것도 없다면 사실상 멈춘것과 같다

## Blocking / Non-Blocking
- Blocking/Non-Blocking은 단어에서 알 수 있듯이 다른 요청의 작업을 처리하기 위해 현재 작업을 block(차단, 대기) 하냐 안하냐의 유무를 나타내는 프로세스의 실행 방식이다.
- 동기/비동기가 전체적인 작업에 대한 순차적인 흐름 유무라면, 블로킹/논블로킹은 전체적인 작업의 흐름 자체를 막냐 안 막냐로 볼 수 있다. 
- 파일을 읽는 작업이 있을 때, 블로킹 방식으로 읽으면 파일을 다 읽을 때까지 대기하고, 논블로킹 방식으로 읽으면 파일을 다 읽지 않아도 다른 작업을 할 수 있다. 

## Recap
- sync/async : 순차적인 흐름 유무
- blocking/nonblocking : 작업의 흐름 blocking 유무