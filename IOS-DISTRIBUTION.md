# iPhone 배포 준비

## 배포 방식

- Flutter iOS Release 빌드를 macOS GitHub Actions에서 만들고, 서명 없는 IPA를 생성합니다.
- AltStore Classic 2.3에서 사용자의 Apple 계정으로 재서명해 설치합니다. Remote AltServer는 AltStore 설정에서 연결합니다.
- Apple 계정, 기기 페어링 파일, 사이버캠퍼스 계정은 GitHub 빌드에 넣지 않습니다.
- 최소 iOS 14.0, 앱 식별자 `kr.campusradar.campusradar`입니다.

## 설치

빌드 성공 후 `ios-preview` 테스트 Release에서 `campus-radar.ipa`를 제공합니다.
Safari에서 IPA 다운로드 → 파일 앱에 저장 → AltStore Classic의 My Apps에서 + → IPA 선택 → 서명·설치 순서입니다.
이미 사용하는 Remote AltServer 연결을 AltStore에서 선택합니다. 연결이나 서명 갱신은 AltStore에서 처리합니다.

AltStore Source 주소는 다음과 같습니다. **Release 생성 전에는 유효한 설치 주소가 아닙니다.**

`https://github.com/lemoncube7/campus-radar/releases/download/ios-preview/altstore-source.json`

AltStore의 Sources에 이 주소를 등록하면 캠퍼스레이더를 찾아 설치하고 새 버전도 확인할 수 있습니다.
앱의 iPhone 업데이트 화면에서는 GitHub 배포 페이지로 연결합니다. 실제 업데이트 설치는 AltStore에서 진행합니다.

## iOS 동작

- 계정은 iOS Keychain에 저장합니다. 재부팅 후 처음 잠금을 해제한 다음 백그라운드 접근을 허용하고, 다른 기기로 이전하지 않는 설정입니다.
- 알림 권한을 요청하고 로컬 알림을 예약합니다. iOS 예약 한도에 맞춰 마감이 가까운 항목부터 최대 60개를 예약합니다.
- 새 과제는 수집에 성공해 발견한 시점에 알립니다. 실시간 서버 푸시가 아닙니다.
- iOS 백그라운드 확인은 BGAppRefreshTask를 사용합니다. 1시간을 요청하지만 실행 여부와 시각은 iOS가 결정합니다.
- 앱 실행·복귀 시에도 수집합니다. 사용자가 강제 종료하거나 백그라운드 앱 새로 고침을 끄면 자동 수집이 제한됩니다.
- 미완료 항목의 마감 24시간 전 알림은 마지막 수집 정보를 기준으로 예약합니다. 이후 제출·마감 변경은 다음 성공 수집에 반영됩니다.
- 목록 제외·복구, 상세 보기, 세션 쿠키를 전달한 WKWebView 바로가기를 제공합니다.

## 빌드

GitHub 저장소에는 소스 ZIP과 `.github/workflows/ios.yml`을 올립니다.
ZIP이 바뀌거나 Actions에서 수동 실행하면 macOS에서 analyze → test → iOS build → IPA 패키징 → 메타데이터 생성 → 테스트 Release 게시를 진행합니다.
Android의 최신 정식 Release는 iOS 테스트 Release와 별도로 유지합니다.

Mac에서 직접 빌드할 때는 Flutter 3.35.7, Xcode, CocoaPods를 설치하고 프로젝트 루트에서 실행합니다.

```sh
bash scripts/build-ios.sh
```

결과: `build/ios/altstore/campus-radar.ipa`.
AltStore 메타데이터는 실제 IPA의 Info.plist, 파일 크기, SHA-256을 읽어서 생성합니다.

## 실제 iPhone에서 남은 검증

1. AltStore로 설치하고 첫 실행 화면을 확인합니다.
2. 포털 계정 연결, 과제·콘텐츠 수집, 재실행 후 계정 유지 여부를 확인합니다.
3. 알림 테스트 → 알림 클릭 → 앱 상세 이동을 확인합니다.
4. 과제·콘텐츠의 사이버캠퍼스 바로가기와 세션 유지 여부를 확인합니다.
5. 잠금 상태의 백그라운드 수집 기록과 예약 알림을 관찰합니다. 실행 간격은 보장값으로 판단하지 않습니다.
6. 항목 제외·복구 후 목록과 알림 예약이 바뀌는지 확인합니다.
7. 다음 IPA에서 AltStore 업데이트 후 계정·목록 유지 여부를 확인합니다.

참고: [AltStore Source 형식](https://faq.altstore.io/developers/make-a-source), [Remote AltServers](https://faq.altstore.io/altstore-classic/remote-altservers), [Flutter iOS 배포](https://docs.flutter.dev/deployment/ios).
