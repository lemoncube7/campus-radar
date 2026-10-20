# 캠퍼스레이더

충남대학교 사이버캠퍼스 과제·콘텐츠·공지를 기기에서 수집하고 해야 할 일과 일정을 확인하는 앱입니다.

- [Android 정식 0.4.14](https://github.com/lemoncube7/campus-radar/releases/tag/v0.4.14)
- [Android 개발 0.5.0 (36)](https://github.com/lemoncube7/campus-radar/releases/tag/v0.5.0-dev)

## 0.5.0 개발 버전

오늘 / 일정 / 과목 / 설정으로 구성했습니다. 일정에서 할 일·캘린더·시간표·확인 필요를 전환합니다.
공지에서 찾은 일정은 원문·오늘·캘린더에서 동일한 상태와 확정 기능으로 연결됩니다.

개인 계정·Gemini 키·Android 서명 파일은 소스에 포함하지 않습니다. 기존 앱 위에 업데이트합니다.

```sh
flutter pub get
flutter test
flutter analyze
flutter build apk --release --dart-define=RELEASE_CHANNEL=development
```
