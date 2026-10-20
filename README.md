# 캠퍼스레이더

충남대학교 사이버캠퍼스 과제·콘텐츠·공지를 기기에서 수집하고 마감과 새 항목을 알려 주는 앱입니다.

## Android 0.4.12 (33)

계정·동의 변경 보호, 로그아웃 정리, 공지 본문 재확인, 현재 과목 목록, 작업 잠금 소유권, 요청 전체 시간 제한, 첨부 캐시 용량 및 새 공지 알림을 보완했습니다.

개인 계정과 Gemini 키는 소스에 포함하지 않습니다. Android 서명 파일도 별도로 구성해야 합니다.

```sh
flutter pub get
flutter test
flutter analyze
flutter build apk --release --dart-define=RELEASE_CHANNEL=stable
```

[Android 릴리스](https://github.com/lemoncube7/campus-radar/releases/tag/v0.4.12)

