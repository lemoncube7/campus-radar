# 현재 iPhone 배포: 0.5.2 (38) 개발 버전

AltStore 소스의 실제 버전·빌드를 확인하세요. 기존 앱을 삭제하지 않고 같은 Apple 계정으로 업데이트합니다. 위젯을 사용하려면 확장을 유지하세요. App Group·위젯·원격 업데이트·서명 갱신은 실제 기기 체크리스트로 확인해야 합니다.

검증 항목: [TEST-CHECKLIST-0.5.2.md](TEST-CHECKLIST-0.5.2.md)

아래는 이전 설치 안내와 검증 이력입니다. 과거 버전 결과를 현재 기기 검증으로 보지 마세요.

# iPhone 배포 준비

## 0.2.1 업데이트

화면 개편·공지 AI 일정함·선택형 AI 요약·EventKit 캘린더 전송을 포함합니다. 자세한 범위와 iOS 차이는 [IOS-RELEASE-NOTES.md](IOS-RELEASE-NOTES.md)를 확인하세요. AltStore 소스 주소와 번들 ID는 유지합니다. 실제 iPhone 검증은 별도로 필요합니다.

## 이전 0.1.5 확인 기록

- 최신 0.1.5 (빌드 6) IPA는 GitHub macOS 빌드에서 정적 분석·테스트·컴파일·패키징을 통과했고, ios-preview 테스트 Release에 게시했습니다.
- 게시된 IPA를 내려받아 번들 ID·버전·최소 iOS 14.0·SHA-256과 AltStore 메타데이터의 파일 크기를 확인했습니다.
- GitHub 연결 권한을 다시 설정한 뒤 소스 쓰기와 IPA 자동 게시가 정상 동작했습니다.
- 로그·공지·마감 색상과 AltStore 업데이트 연결, 전체 할 일 API 시간 초과를 피하는 강의별 수집 수정이 최신 IPA에 들어 있습니다. 실제 iPhone 설치·알림·백그라운드 검증은 남아 있습니다.
- 0.1.5 IPA는 7,606,975바이트이며 SHA-256은 `3594031bfc36004609e95d83a67ffe57df0c55f988086700aba6717163ae5a6d`입니다. 공개 파일을 다시 다운로드해 버전·번들 ID·파일 크기·AltStore 소스 메타데이터와 대조했습니다.
- [빌드 성공 기록](https://github.com/lemoncube7/campus-radar/actions/runs/38668376157), [iPhone 테스트 Release](https://github.com/lemoncube7/campus-radar/releases/tag/ios-preview).

## 배포 방식

- Flutter iOS Release 빌드를 macOS GitHub Actions에서 만들고, 서명 없는 IPA를 생성합니다.
- AltStore Classic 2.3에서 사용자의 Apple 계정으로 재서명해 설치합니다. Remote AltServer는 AltStore 설정에서 연결합니다.
- Apple 계정, 기기 페어링 파일, 사이버캠퍼스 계정은 GitHub 빌드에 넣지 않습니다.
- 최소 iOS 14.0, 앱 식별자 `kr.campusradar.campusradar`입니다.

## 설치

### 먼저 준비할 것

- AltStore Classic 2.3을 사용하는 이번 배포 방식은 iOS 17.4 이상이 필요합니다. IPA 자체의 최소 iOS 설정 14.0과 설치 도구의 요구 버전은 서로 다릅니다. [AltStore 공식 릴리스 노트](https://github.com/altstoreio/FAQ/blob/main/release-notes/altstore.md)를 확인하세요.
- iPhone, 데이터 통신이 되는 USB 케이블, Windows PC, Apple 계정, Wi-Fi를 준비합니다. Apple 계정은 AltStore/AltServer의 인증 화면에 직접 입력합니다.
- AltStore가 아직 없다면 [Windows 공식 설치 안내](https://faq.altstore.io/altstore-classic/how-to-install-altstore-windows)에 따라 Apple 직접 배포판 iTunes·iCloud와 AltServer를 설치하고, iPhone USB 연결·컴퓨터 신뢰·Wi-Fi 동기화를 설정한 다음 AltServer에서 Install AltStore를 선택합니다.
- iPhone의 설정 → 일반 → VPN 및 기기 관리에서 개발자 앱을 신뢰하고, 설정 → 개인정보 보호 및 보안 → 개발자 모드를 켭니다. 표시되는 재시작·확인 절차를 완료합니다.
- AltStore가 이미 설치돼 있다면 위 초기 설치 단계를 반복할 필요 없이 아래 Remote AltServer 및 소스 등록으로 진행합니다.

### Remote AltServer와 앱 설치

[`ios-preview` 테스트 Release](https://github.com/lemoncube7/campus-radar/releases/tag/ios-preview)에서 `campus-radar.ipa`를 내려받습니다.
Safari에서 IPA 다운로드 → 파일 앱에 저장 → AltStore Classic의 My Apps에서 + → IPA 선택 → 서명·설치 순서입니다.
AltStore 설정의 Set up Remote AltServer로 기기 페어링과 LocalDevVPN 설정을 진행합니다. 사용 시 Wi-Fi와 LocalDevVPN 연결이 필요합니다. 이미 설정했다면 기존 연결을 사용합니다. 서명 갱신은 AltStore에서 처리합니다.

AltStore Source 주소는 다음과 같습니다. 게시된 최신 테스트 IPA를 가리킵니다.

`https://github.com/lemoncube7/campus-radar/releases/download/ios-preview/altstore-source.json`

AltStore의 Sources에 이 주소를 등록하면 캠퍼스레이더를 찾아 설치하고 새 버전도 확인할 수 있습니다.
앱의 iPhone 업데이트 화면에서는 업데이트 확인으로 `ios-latest.json`의 버전 정보를 읽습니다. 새 버전에서 업데이트를 누르면 AltStore Classic의 소스 화면을 엽니다. 실제 서명·설치는 AltStore에서 확인합니다.

일반 무료 Apple 계정으로 설치한 앱은 7일 안에 서명을 갱신해야 합니다. AltStore의 My Apps → Refresh All로 만료 전에 갱신하고, Remote AltServer를 사용할 때는 Wi-Fi와 LocalDevVPN을 연결합니다. 무료 계정의 동시 활성 앱 제한도 확인하세요. [AltStore 시작 안내](https://faq.altstore.io/altstore-classic/your-altstore).

### 캠퍼스레이더 첫 실행

1. 포털 계정을 연결하고 과제·콘텐츠·공지 목록이 수집되는지 확인합니다.
2. 알림 권한을 허용하고 앱의 알림 테스트로 실제 표시를 확인합니다.
3. 설정 → 일반 → 백그라운드 앱 새로 고침을 켜고 캠퍼스레이더를 허용합니다.
4. 자동 수집을 확인하는 동안 저전력 모드는 끄고, 앱 전환 화면에서 앱을 위로 밀어 강제 종료하지 않습니다. 고정된 1시간 실행을 보장하는 설정은 아닙니다.

## iOS 동작

- 계정은 iOS Keychain에 저장합니다. 재부팅 후 처음 잠금을 해제한 다음 백그라운드 접근을 허용하고, 다른 기기로 이전하지 않는 설정입니다.
- 알림 권한을 요청하고 로컬 알림을 예약합니다. iOS 예약 한도에 맞춰 마감이 가까운 항목부터 데일리 요약 7회 공간을 남겨 최대 56개를 예약합니다.
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

