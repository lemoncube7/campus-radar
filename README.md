# 캠퍼스레이더

충남대학교 사이버캠퍼스 과제·콘텐츠 알림 프로토타입입니다. Android APK를 배포하며 iPhone용 AltStore 테스트 배포를 준비했습니다.

iPhone 빌드·설치·검증 절차는 [IOS-DISTRIBUTION.md](IOS-DISTRIBUTION.md)를 확인하세요. iOS 백그라운드 수집은 고정된 주기를 보장하지 않습니다.

## 설치

Releases에서 campus-radar.apk를 내려받아 설치하세요. Android 8.0 이상을 대상으로 합니다.
앱에서 충남대 포털 계정으로 연결하고 알림 권한을 허용하세요.
계정은 기기에 암호화해 저장하며, 과제 수집은 기기에서 사이버캠퍼스로 직접 요청합니다.

## 기능

- 약 1시간마다 새로 로그인해 과제와 콘텐츠를 수집합니다. 실행 시각은 Android 절전 정책에 따라 지연될 수 있습니다.
- 첫 연결은 기존 과제를 기준 목록으로 저장하고, 이후 새로 발견한 과제를 알립니다.
- 미제출 과제와 미완료 콘텐츠의 마감 24시간 전 알림을 예약합니다. 이미 하루 이내라면 한 번 알립니다.
- 알림을 누르면 앱 상세를 열고, 사이버캠퍼스 바로가기로 연결합니다.
- 제출 완료·마감 변경이 확인되면 알림 예약을 갱신합니다.
- 업데이트 확인 → APK 다운로드·해시·서명 검증 → Android 설치 화면을 제공합니다.

- 상세 화면의 목록에서 제외로 항목과 알림을 숨깁니다. 제외 항목 보기에서 복구할 수 있고, 다음 수집에도 제외 상태를 유지합니다.

## 검증 상태

실제 계정에서 포털 로그인과 수강 과목·과제·콘텐츠 수집을 확인했습니다.
과제는 실제 제출 기록의 apply_yn 및 임시 저장 여부를 사용하고, 콘텐츠는 complete_yn을 사용합니다.
0.1.1은 실제 Android 16 삼성 기기에서 시작 화면 표시를 확인했습니다. 백그라운드 수집, 실제 알림, 웹뷰 바로가기, APK 업데이트 설치는 추가 확인이 필요합니다.

## 개발

Flutter 3.35.7 / Dart 3.9.2, Java 17, Android SDK 36을 사용합니다.
소스 패키지 campus-radar-source.zip을 풀고 flutter pub get을 실행하세요.
릴리스 빌드에는 기존 배포와 같은 Android 서명 키가 필요합니다. 서명 키·계정 파일은 공개하지 않습니다.
빌드 설정의 signingConfigs를 자신의 안전한 로컬 서명 설정으로 연결하세요.
flutter analyze 및 flutter test 후 flutter build apk --release로 빌드합니다.

## 업데이트 게시

같은 서명 키로 만들고 versionCode를 증가시킨 APK와 latest.json을 새 GitHub Release에 함께 올립니다.
latest.json에는 versionCode, versionName, apkUrl, sha256, notes가 필요합니다.
앱의 기본 확인 주소는 https://github.com/lemoncube7/campus-radar/releases/latest/download/latest.json 입니다.
SHA-256, 패키지명, 버전, 서명 인증서가 맞는 APK만 설치 화면으로 전달합니다.

학교 공식 앱이 아닌 개인 프로토타입입니다. 실패 시 마지막 성공 데이터를 유지하고 화면에 오류를 표시합니다.


