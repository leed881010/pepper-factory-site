# N x N Screenshots

App Store Connect 에 업로드한 스크린샷을 그대로 다운로드해서 locale 별 폴더에 넣어주세요.

## 명명 규칙 (사이트 다른 앱과 동일)

```
ko/0_APP_IPHONE_65_0.jpg   ← 첫 번째 스크린샷 (한국어 UI)
ko/1_APP_IPHONE_65_1.jpg
ko/2_APP_IPHONE_65_2.jpg
ko/3_APP_IPHONE_65_3.jpg
ko/4_APP_IPHONE_65_4.jpg

en/0_APP_IPHONE_65_0.jpg   ← 첫 번째 (영문 UI)
...

ja/0_APP_IPHONE_65_0.jpg   ← 첫 번째 (일문 UI)
...
```

## 다운로드 위치

App Store Connect → 앱 → iOS App → 1.8.0 → "iPhone 6.5\" Display" 섹션에서 각 스크린샷의 "Download" 우클릭

## 페이지에 자동 반영

`nxn.html` 의 스크린샷 갤러리는 위 파일들을 직접 참조합니다. 파일을 떨구고 `git push` 만 하면 Vercel 이 배포.

## 권장 5장 구성 (피처링 어필용)

1. **빈 보드 + 레이아웃 선택 UI** — "단순함" 메시지
2. **채워진 3×3 보드 + 이모지 캡션** — 핵심 결과물
3. **텍스트 오버레이 + 스티커 편집 화면** — 표현력
4. **레이아웃 다양성 (1×2, 9:16 등)** — 유연성
5. **추출된 결과 영상 미리보기** — 최종 산출물
