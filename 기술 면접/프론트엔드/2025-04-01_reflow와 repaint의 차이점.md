---
tags:
  - TI_front
  - reflow
  - repaint
---
## reflow와 repaint의 차이점에 대해서 설명해주세요.

---

>브라우저가 화면을 그리는 과정에서 일어나는 두 가지 단계인 reflow(레이아웃) 와 repaint(페인트) 는 동작 방식도 다르고, 비용도 다르고, 최적화 방법도 다르다.

---

### 브라우저 렌더링 흐름 간단 정리

1. HTML 파싱 → DOM 트리 생성
2. CSS 파싱 → CSSOM 생성
3. DOM + CSSOM → Render Tree 생성
4. **Layout (Reflow)** → 요소 위치와 크기 계산
5. **Paint (Repaint)** → 픽셀에 색상, 스타일 칠함
6. Compositing → 레이어 합쳐서 화면에 표시

---

### Reflow (Layout, Layout Thrashing)

> 요소의 **위치나 크기**가 변경될 때, 브라우저가 전체 또는 일부 레이아웃을 다시 계산하는 과정

#### 예시 상황:

- `width`, `height`, `margin`, `padding`, `display`, `position`, `top` 등 **레이아웃에 영향을 주는 속성** 변경
- DOM 구조 변경 (노드 추가/삭제)
- 폰트 크기 변경
- 창 크기 변경 (`resize` 이벤트)

#### 비용: 매우 크다

- 부모 요소부터 자식 요소까지 **연쇄적으로 계산**됨
- 복잡한 레이아웃일수록 큰 영향

---

### Repaint (Re-render, Paint)

> 요소의 **시각적 속성(스타일)이 바뀌었을 때**, 다시 **색상, 테두리, 그림자 등 시각 요소를 그리는 작업**

#### 예시 상황:

- `background-color`, `color`, `box-shadow`, `border-color`, `visibility` 등의 **스타일만 변경**

#### 비용: 비교적 작음

- 레이아웃은 그대로지만 픽셀만 다시 칠하는 것

---

### 핵심 차이 요약

| 항목      | Reflow                         | Repaint              |
| ------- | ------------------------------ | -------------------- |
| 의미      | 레이아웃 재계산                       | 스타일만 다시 그림           |
| 발생 시점   | 구조/위치/크기 변화                    | 색상/폰트/그림자 등 시각 요소 변화 |
| 비용      | 높음 (성능 이슈 큼)                   | 낮음 (덜 위험함)           |
| 최적화 포인트 | DOM 조작 최소화, `class`로 묶어서 일괄 변경 | GPU 가속 사용, 스타일 통합 변경 |

---

### 최적화 팁

- **DOM 변경은 한 번에, 배치해서 처리**
- `display: none` 후 DOM 수정 → `display: block` → Reflow 최소화
- `requestAnimationFrame`을 활용해 렌더 타이밍 제어
- 가급적 **transform/opacity** 이용 (레이아웃 영향 X, GPU 가속됨)

---

### 🔍 실제 코드 예시

```js
// 안 좋은 예 - 매번 Reflow 발생
for (let i = 0; i < 1000; i++) {
  element.style.marginTop = i + 'px'; // 1000번 layout 발생
}

// 좋은 예 - DOM 일괄 변경
element.style.cssText = 'margin-top: 100px; margin-left: 50px;';

```