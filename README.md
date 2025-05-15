# 워드프레스 콘텐츠 편집 실전 기록: TheGem 테마, WPBakery, SA Sliders 정복기

웹사이트의 핵심 콘텐츠, 페이지와 슬라이더를 내 마음대로 주무르기 위한 실전 편집 기록이다. TheGem 테마, WPBakery 페이지 빌더, "SA Sliders" 플러그인과의 씨름 과정을 담았다.

## 목차

1.  [제품 소개 페이지 구조 분석 (Portfolio 기능 활용 전략)](#1-제품-소개-페이지-구조-분석-portfolio-기능-활용-전략)
2.  [기존 형식 복제: 새 제품 등록 효율 극대화](#2-기존-형식-복제-새-제품-등록-효율-극대화)
3.  [슬라이더 이미지 변경 불가 현상 돌파 (캐시와의 정면승부)](#3-슬라이더-이미지-변경-불가-현상-돌파-캐시와의-정면승부)
4.  [슬라이드 콘텐츠 강화: HTML/CSS 직접 제어](#4-슬라이드-콘텐츠-강화-htmlcss-직접-제어)
5.  [참고 스크린샷 위치](#5-참고-스크린샷-위치)

---

## 1. 제품 소개 페이지 구조 분석 (Portfolio 기능 활용 전략) 🎯

"페이지 편집"에 들어갔으나, 보이는 건 레이아웃 편집 기능 또는 정체불명의 "PORTFOLIO" 요소뿐. 실제 제품 정보 추가 및 업데이트는 어디서 하는가?

* **상황:** "제품 소개" 페이지 내용 직접 수정 불가.
  (제품 페이지 예시):* ![image](https://github.com/user-attachments/assets/0e7a1fef-f50d-48a5-a6c3-16b5ebf0dbf3)

    (WPBakery 편집 - PORTFOLIO 요소):* ![image](https://github.com/user-attachments/assets/d9999175-2f3f-4167-b79a-2c2375842daf)

* **분석 및 대응:**
    * 상단 관리자 바 "Edit with WPBakery Page Builder" 확인 -> WPBakery 사용 확정.
    * TheGem 테마의 경우 "Portfolio" 커스텀 포스트 타입을 제품 관리에 활용하는 경우가 많음을 인지.
    * **조치:**
        1.  워드프레스 관리자 메뉴에서 "Portfolio" (또는 "TheGem Portfolio") 확인.
        2.  "Portfolio" > "Add New" 또는 기존 아이템 "Edit"을 통해 제품명, 설명, **특성 이미지(Featured Image)**, 카테고리 등 핵심 정보 입력/수정.
        3.  WPBakery 페이지 빌더로 돌아와, 페이지 내 "Portfolio" 요소 설정 (Source/Query, 레이아웃, 표시 항목 등)을 조정하여 원하는 제품 목록 표시. 또는 "Portfolio Grid" 등 신규 요소 추가 검토.

---

## 2. 기존 형식 복제: 새 제품 등록 효율 극대화 ⏱️

신규 제품 등록 시마다 레이아웃을 새로 짜는 건 시간 낭비다. 기존 "Export Transformer" 아이템의 구조를 그대로 복제하여 생산성을 높인다.
![image](https://github.com/user-attachments/assets/961129ed-996d-40e8-8212-0479d291963d)

* **상황:** "Portfolio" > "Add New" 방식은 비효율적. "Export Transformer" 레이아웃 재사용 필요.
    
* **문제점:** "Export Transformer" 항목에 마우스오버 시 "Duplicate" 또는 "Clone" 기능 부재.
    
* **대응책: WPBakery 페이지 빌더 템플릿 기능 활용**
    1.  **원본("Export Transformer") 편집:** WPBakery 편집 모드 진입.
    2.  **템플릿 저장:** WPBakery 편집기 도구 모음 > "Templates" > "Save current layout as a template" 실행. (예: "제품_기본_레이아웃"으로 저장)
    3.  **새 아이템 생성:** "Portfolio" > "Add New"로 새 아이템 생성.
    4.  **템플릿 적용:** WPBakery 편집 모드에서 "Templates" > 저장한 "제품_기본_레이아웃" 불러오기.
    5.  **내용 수정 및 발행:** 불러온 레이아웃에 새 제품 정보(텍스트, 이미지, 특성 이미지, 카테고리 등) 입력 후 "Publish".

---

## 3. 슬라이더 이미지 변경 불가 현상 돌파 (캐시와의 정면승부) 😤

"SA Sliders"에서 슬라이드 배경 이미지를 분명히 바꿨는데, 웹사이트는 요지부동. 편집 화면 미리보기조차 말을 듣지 않는 상황. 원인은 무엇인가?
![image](https://github.com/user-attachments/assets/bbab69da-723c-406f-91d5-bd12eb66c8ed)

* **상황:** "SA Sliders" 편집 화면에서 "Set image"로 새 배경 이미지 선택 후 저장/업데이트했으나 변경사항 미반영.
* ![image](https://github.com/user-attachments/assets/60665287-184d-430a-ad5f-bf6df8e75d31)
 ![image](https://github.com/user-attachments/assets/82b89a16-b9bc-4d86-9787-21728939552e)
* **핵심 점검 및 조치:**
    1.  **저장 절차 재확인:**
        * **개별 슬라이드 저장:** 각 슬라이드(SLIDE 1 등) 편집 후, 해당 슬라이드 설정 영역 내 "Save Slide"(또는 유사 명칭) 버튼 클릭 여부 확인. (이 버튼이 UI상 명확하지 않아 혼선)
        * **슬라이더 전체 저장/업데이트:** 개별 슬라이드 저장 후, 슬라이더 전체 설정 페이지(** 화면 기준, 오른쪽 상단 파란색 "업데이트" 버튼**) 클릭.
    2.  **캐시(Cache) 완전 소탕:** 이것이 주범일 확률이 매우 높다.
        * **브라우저:** 강력 새로고침 (Ctrl+Shift+R 또는 Cmd+Shift+R), 시크릿 모드 사용.
        * **워드프레스 캐시 플러그인:** (LiteSpeed Cache 등) 관리자 메뉴에서 "모든 캐시 비우기".
        * **테마 캐시 (TheGem):** Theme Options > Performance 등에서 캐시 초기화.
        * **서버 캐시 (Cafe24):** 호스팅 제어판에서 제공하는 모든 서버 측 캐시 비우기.
    3.  **플러그인 충돌 검토:** "SA Sliders", 테마 코어, WPBakery를 제외한 플러그인 일시 비활성화 후 테스트.
    4.  **브라우저 개발자 도구(F12) Console 탭:** JavaScript 오류 등 추가 단서 확인.

---

## 4. 슬라이드 콘텐츠 강화: HTML/CSS 직접 제어 ⌨️

단순 배경 이미지를 넘어, 이미지와 텍스트를 결합하여 슬라이드 콘텐츠의 전달력을 높인다. HTML과 약간의 CSS 직접 편집으로 원하는 결과물을 만든다.

* **목표:** 슬라이드 배경 이미지 대신, 콘텐츠 영역에 이미지와 제품명(예: "콜게이트 유입변압기", "(Oil-Filled transformer)")을 함께 표시.
 ![image](https://github.com/user-attachments/assets/2f6eb7b2-e729-4878-9481-f28cf5c2def0)
![image](https://github.com/user-attachments/assets/ec2a0910-0740-4b1a-bce4-e17c77e24af5)

* **실행 방안 (HTML/CSS):**
    1.  **편집 모드 전환:** 슬라이드 콘텐츠 편집 영역의 툴바에서 "텍스트(Text)" 또는 "HTML" 모드로 진입.
    2.  **HTML 구조 설계:**
        * 전체를 감싸는 `<div>`와 클릭 가능한 `<a>` 태그 사용.
        * `<a>` 태그 내부에 `<img>` 태그와 텍스트용 `<span>` 태그 (또는 단순 텍스트와 `<br />`) 배치.
    3.  **CSS 인라인 스타일 적용:**
        * 이미지: `max-width`, `height: auto;`, `display: block;`, `margin` 등으로 크기 및 정렬 제어.
        * 텍스트: `font-size`, `color`, `display: block;` 등으로 스타일 및 줄 바꿈 처리.
        * 전체 컨테이너: `text-align: center;` 등으로 내부 요소 정렬.
    4.  **이미지 URL 확보:** 워드프레스 "미디어 > 라이브러리"에서 사용할 이미지의 "파일 URL"을 복사하여 `<img>` 태그의 `src` 속성에 적용.
    5.  **저장 및 최종 확인:** 개별 슬라이드 저장 -> 슬라이더 전체 "업데이트" -> 캐시 삭제 후 웹사이트에서 최종 결과물 확인.

---

**한마디:** 웹사이트 관리는 때로 예상치 못한 난관의 연속이다. 그러나 문제의 본질을 파악하고 끈기 있게 대응하면 결국 원하는 결과를 얻을 수 있다. 
