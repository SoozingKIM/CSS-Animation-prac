# CSS-Animation-prac

## CSS 동적으로 적용

```js
// <ChallengeItem> 컴포넌트
<div className="challenge-item-details">
```

`isExpanded` 속성이 true면 스타일 요소에 `.expanded` 클래스 추가, false면 공백처리

```js
// <ChallengeItem> 컴포넌트
// isExpanded 속성이 있다.
<div className={`challenge-item-details ${isExpanded ? "expanded" : ""}`} >
```

## CSS로 애니메이션 추가

### transition

어느 프로퍼티의 어떤 변경 사항에 적용할지 알려주어야 한다.

```css
.challenge-item-details-icon {
  display: inline-block;
  font-size: 0.85rem;
  margin-left: 0.25rem;

  /* 없다가 생길때 애니메이션 효과 */
  transition: transform 0.3s ease-out;
}

.challenge-item-details.expanded .challenge-item-details-icon {
  transform: rotate(180deg);
}
```

## @keyframes

모달창처럼 DOM에 있다가 없어지는 요소는 CSS 트랜지션을 쓸 수 없다.  
이걸 사용하면 된다.

```css
@keyframes 이름 {
    상태 {
        적용할 css
    }
}
```

이렇게 정의한 뒤, 이 애니메이션을 적용하려는 요소의 CSS 속성에 `animation: 이름 시간 ...` 을 적어넣으면 된다.  
값에 `forwards`를 추가하면 애니메이션이 끝나도 최종상태를 유지하라는 뜻이다.

```css
.modal {
  top: 10%;
  border-radius: 6px;
  padding: 1.5rem;
  width: 30rem;
  max-width: 90%;
  z-index: 10;

  /* 애니메이션 적용 */
  animation: slide-up-fade-in 0.6s ease-out forwards;
}

/* 애니메이션 정의 */
@keyframes slide-up-fade-in {
  0% {
    transform: translateY(30px);
    opacity: 0;
  }
  100% {
    transform: translateY(0);
    opacity: 1;
  }
}
```

이것의 한계:

1. DOM요소를 나타나게 할 수는 있지만 사라지게 할 수는 없다.

DOM에서 사라지면 즉시 사라지기때문에 효과르 적용할 수 없음.

2. 현실감있거나 복잡한 애니메이션을 넣을 수 없다.

ex) 메뉴같은 데에서 탭을 전환할 때 -> 가능은 하지만 너무 복잡하고 어렵다.

## Framer Motion 라이브러리 이용하기

리액트 라이브러리이다.

### 기본 사용법

패키지를 import 한 후,
이걸 입히려는 요소 이름을 바꾸고 속성을 추가한다.

```js
// <div> 에 입히려면
<motion.div animate={{ 스타일들 }} transition={{ 효과들 }}>

// 조건에 따라 입히기
<motion.div animate={{ rotate: isExpanded ? 180 : 0 }} transition={{ 효과들 }}>
```
