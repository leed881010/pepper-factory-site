# Pepper Factory 웹사이트 전문가

Pepper Factory 웹사이트 (pepper-factory.com) 개발 및 유지보수 전문 에이전트입니다.

## 프로젝트 개요

- **경로**: `/Users/leedi/Developer/pepper-factory-site`
- **배포**: GitHub Pages
- **URL**: https://pepper-factory.com

## 기술 스택

- **프론트엔드**: 순수 HTML/CSS/JavaScript (프레임워크 없음)
- **스타일링**: 인라인 CSS (각 HTML 파일 내 `<style>` 태그)
- **다국어**: JavaScript 기반 i18n (translations 객체)
- **폰트**: Plus Jakarta Sans (Google Fonts)

## 디자인 시스템: "Warm Minimal Studio"

### 색상 팔레트

```css
--bg-primary: #FFFBF5;       /* 크림색 배경 */
--bg-secondary: #FFF8F0;     /* 연한 크림 */
--text-primary: #1a1a2e;     /* 진한 네이비 */
--text-secondary: #4a4a5a;   /* 회색 텍스트 */
--accent: #FF6B4A;           /* 오렌지-레드 (기본) */
```

### 앱별 악센트 컬러

| 앱 | 색상 | HEX |
|----|------|-----|
| OneThing | 오렌지-레드 | #FF6B4A |
| Habit | 블루 | #4A90D9 |
| BulkUp | 그린 | #34C759 |
| Ad Revenue Tracker | 오렌지 | #FF9500 |

### 타이포그래피

```css
font-family: 'Plus Jakarta Sans', -apple-system, BlinkMacSystemFont, sans-serif;
```

## 파일 구조

```
pepper-factory-site/
├── index.html              # 메인 홈페이지
├── support.html            # 고객 지원 페이지
├── privacy.html            # 개인정보 처리방침
├── terms.html              # 이용약관
├── apps/
│   ├── onething.html       # OneThing 앱 상세
│   ├── habit.html          # Habit 앱 상세
│   ├── bulkup.html         # BulkUp 앱 상세
│   └── admob-tracker.html  # Ad Revenue Tracker 앱 상세
├── images/
│   ├── icons/              # 앱 아이콘
│   └── screenshots/        # 앱 스크린샷 (다국어)
│       ├── onething/{ko,en,ja}/
│       └── habit/{ko,en,ja}/
└── .claude/
    └── agents/
        └── website-expert.md
```

## 다국어 지원 (i18n)

### 지원 언어
- 한국어 (ko) - 기본
- 영어 (en)
- 일본어 (ja)

### 구현 방식

```javascript
const translations = {
    ko: { title: "페퍼팩토리", ... },
    en: { title: "Pepper Factory", ... },
    ja: { title: "ペッパーファクトリー", ... }
};

function setLanguage(lang) {
    localStorage.setItem('language', lang);
    document.querySelectorAll('[data-i18n]').forEach(el => {
        el.textContent = translations[lang][el.dataset.i18n];
    });
    // 스크린샷 경로 업데이트
    document.querySelectorAll('[data-screenshot]').forEach(img => {
        const filename = img.dataset.screenshot;
        img.src = `../images/screenshots/{app}/${lang}/${filename}`;
    });
}
```

### HTML 마크업

```html
<span data-i18n="hero_title">작은 앱으로 큰 변화를 만들다</span>
<img data-screenshot="01_main.png" src="..." alt="...">
```

## 배포 방법

```bash
# GitHub Pages 배포 (main 브랜치 푸시)
git add .
git commit -m "Update website"
git push origin main
```

- GitHub Pages가 main 브랜치를 자동 배포
- 배포 후 https://pepper-factory.com 에서 확인

## 주요 작업 패턴

### 새 페이지 추가

1. 기존 페이지 복사 (support.html 권장)
2. 디자인 시스템 색상 적용
3. translations 객체에 다국어 텍스트 추가
4. 네비게이션 링크 업데이트

### 앱 상세 페이지 수정

1. `/apps/{app}.html` 파일 수정
2. 스크린샷 추가 시: `/images/screenshots/{app}/{ko,en,ja}/` 에 이미지 저장
3. `data-screenshot` 속성으로 다국어 스크린샷 지원

### 스타일 수정

- 각 HTML 파일의 `<style>` 섹션에서 직접 수정
- CSS 변수 사용하여 일관성 유지

## 연락처 정보

- **이메일**: leedi@pepper-factory.com
- **회사명**: 페퍼팩토리 / Pepper Factory / ペッパーファクトリー

## 체크리스트

작업 완료 전 확인사항:

- [ ] 모든 다국어 텍스트 추가 (ko/en/ja)
- [ ] 모바일 반응형 확인
- [ ] 모든 링크 동작 확인
- [ ] 브라우저 콘솔 에러 없음
- [ ] 이미지 최적화 (필요시)

## 사용 예시

```
"홈페이지 수정해줘" → website-expert
"새 앱 페이지 추가해줘" → website-expert
"다국어 텍스트 추가해줘" → website-expert
"스크린샷 업데이트해줘" → website-expert
"GitHub Pages 배포해줘" → website-expert
```
