# 다수의 액션 발생 시 최적화하는 방법

이벤트 오버클럭(overclock-과도한 이벤트 발생)은 리소스 사용량을 증가시키기 때문에 성능문제를 야기하고, 사용자 경험을 떨어뜨린다.<br />
예를 들어 스크롤 이벤트의 경우, 스크롤을 빨리 내리게 되면
3초 간격 내에 몇 천번 이상의 이벤트가 발생하게 되기 때문에
성능에 문제가 생기게 된다.

과도한 이벤트나 함수들의 빈도수를 줄여서 성능을 향상시키는 프로그래밍 기법 중,
자주 언급되는 두가지에 대해 정리해보려 한다.

## Debounce

> 계속 호출되는 함수들 중 제일 마지막 함수만 호출되게 하는 것<br />
> = **가장 최신으로 실행된 이벤트**를 실행되게 하는 것

<div align="center">
<img width="367" alt="스크린샷 2022-06-27 오후 1 52 46" src="https://velog.velcdn.com/images%2Feassy%2Fpost%2F49fbc19a-8df2-4e6d-a653-b3ee2ee07ae9%2Fimage.png">
</div>

8번의 이벤트 중 1️⃣,7️⃣,8️⃣ 이벤트만이 실행된 것을 볼 수 있는데, 정해둔 delay time 보다 짧은 시간 내에 이벤트가 발생된 경우에는 실행되지 않고 delay time을 지나면 실행이 되는 기법이 `debounce`이다.

## Throttle

> 마지막 함수가 호출된 후 일정시간이 지나기 전에 다시 호출되지 않게 하는 것<br />
> = 여러번 실행되는 이벤트를 **일정시간 동안 한번만** 실행되게 하는 것

<div align="center">
<img width="367" alt="스크린샷 2022-06-27 오후 1 52 46" src="https://velog.velcdn.com/images%2Feassy%2Fpost%2F364cc2a4-46f7-4b3e-b74a-0071b3e73866%2Fimage.png">
</div>

점선으로 된 박스 안에 이벤트가 발생한 순서대로 묶여있고
8번의 이벤트 중에 실제 실행된 것은 1️⃣, 4️⃣, 7️⃣, 8️⃣ 뿐이다.<br />
점선으로 표시된 박스는 정해둔 시간의 간격을 표시하고,
그 정해둔 시간의 가장 마지막에 호출된 이벤트를 발생시키는 기법이 `throttle`이다.<br />
실행 횟수에 제한을 걸어두는 것이 특징이다.
