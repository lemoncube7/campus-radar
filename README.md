# 캠퍼스레이더

충남대학교 사이버캠퍼스 과제·콘텐츠·공지를 기기에서 수집하고 마감과 새 항목을 알려 주는 앱입니다.

## Android 0.4.14 정식 버전 (35)

Gemini 재검토 기반 AI 일정 자동 승인(선택 기능), 수업 전 잠금화면 카운트다운, 내부 구조 개선을 포함합니다.
AI 설정에서 ‘명확한 AI 일정 자동 승인’을 켜면 해당 공지와 후보를 추가 전송해 검토합니다. 캘린더 전송은 일정 추가 기본 위치 설정을 따릅니다.

개인 계정·Gemini 키·Android 서명 파일은 소스에 포함하지 않습니다.

```sh
flutter pub get
flutter test
flutter analyze
flutter build apk --release --dart-define=RELEASE_CHANNEL=stable
```

[Android 정식 릴리스](https://github.com/lemoncube7/campus-radar/releases/tag/v0.4.14)
