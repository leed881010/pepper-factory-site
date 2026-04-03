---
name: download-screenshots
description: App Store Connect에서 fastlane으로 스크린샷 다운로드하여 웹사이트에 배치
user_invocable: true
---

# App Store Connect 스크린샷 다운로드

각 iOS 프로젝트 디렉토리에서 `bundle exec fastlane deliver download_screenshots`를 실행하여
App Store Connect에서 최신 스크린샷을 다운로드하고 웹사이트 이미지 디렉토리에 배치합니다.

## 앱 정보

| 앱 | 프로젝트 경로 | 웹사이트 스크린샷 경로 |
|----|-------------|---------------------|
| OneThing | ~/Developer/one_thing | images/screenshots/onething/{lang}/ |
| Weekly (Habit) | ~/Developer/habit | images/screenshots/habit/{lang}/ |
| Workout Timy (BulkUp) | ~/Developer/bulkUp | images/screenshots/bulkup/{lang}/ |
| Ad Revenue Tracker | ~/Developer/admob-tracker-ios | images/screenshots/admob-tracker/{lang}/ |

## 인자

- 인자 없음: 전체 4개 앱
- 앱 이름 지정: `onething`, `habit`, `bulkup`, `admob-tracker` 중 선택

## 실행 절차

### 1. API Key로 각 프로젝트에서 다운로드

API Key 파일은 OneThing Fastfile에서 추출 가능 (key_id: JWVC2UU6Y7).

```bash
# API Key JSON 생성 (one_thing/fastlane/Fastfile에서 추출)
# /tmp/asc_api_key.json

# 각 프로젝트에서 실행
cd ~/Developer/{PROJECT_DIR} && bundle exec fastlane deliver download_screenshots \
  --screenshots_path "/tmp/screenshots/{APP_NAME}" \
  --skip_metadata true \
  --use_live_version true \
  --api_key_path "/tmp/asc_api_key.json"
```

4개 앱을 병렬로 실행 가능.

### 2. 웹사이트 이미지 디렉토리에 복사

fastlane은 `en-US/`, `ko/`, `ja/` 폴더로 다운로드.
6.5인치 또는 6.7인치 iPhone 스크린샷만 (`*IPHONE_6[57]*`) 복사:

```bash
SITE=~/Developer/pepper-factory-site
for src_lang in ko en-US ja; do
    dst_lang=${src_lang/en-US/en}
    mkdir -p "$SITE/images/screenshots/$APP/$dst_lang"
    rm -f "$SITE/images/screenshots/$APP/$dst_lang/"*
    cp /tmp/screenshots/$APP/$src_lang/*IPHONE_6[57]* "$SITE/images/screenshots/$APP/$dst_lang/"
done
```

### 3. HTML data-screenshot 속성 확인

다운로드된 파일 수가 HTML의 `data-screenshot` 항목 수와 다르면 HTML 업데이트.
파일명 패턴: `{N}_APP_IPHONE_65_{N}.jpg`

### 4. 커밋 & 배포

변경된 이미지와 HTML을 git add & commit, push 여부는 사용자에게 확인.
