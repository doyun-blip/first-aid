# 응급처치 길잡이 – Vercel 배포

## 구조
- `public/index.html` : 화면 (검색, 사진 촬영·분석)
- `api/analyze.js`    : 사진 분석 프록시 (API 키는 서버에서만 사용)

## 배포 순서
1. Anthropic 콘솔에서 **새 API 키 발급** (이전에 채팅에 붙여넣은 키는 폐기).
   콘솔에서 월 사용 한도(Spend limit)도 꼭 설정하세요.
2. 이 폴더를 GitHub에 올리거나, 터미널에서 `npm i -g vercel` 후 폴더에서 `vercel` 실행.
3. Vercel 프로젝트 > Settings > Environment Variables 에 추가
   - `ANTHROPIC_API_KEY` = 새 키 (Production/Preview 모두)
   - (선택) `ALLOWED_ORIGIN` = https://내도메인
   - (선택) `CLAUDE_MODEL` = 사용할 모델명 (기본: claude-sonnet-5-5)
4. 환경변수 저장 후 **Redeploy**.

## 비용·악용 방지
- `api/analyze.js`의 IP당 시간당 10회 제한은 서버리스 인스턴스별 임시 제한입니다.
  공개 운영 시 Vercel > Firewall > Rate Limiting 규칙으로 `/api/analyze`에 제한을 거세요.
- 이미지는 JPEG만, 약 3MB 이하만 받습니다.

## 주의
- 의료 진단 서비스가 아닙니다. 화면과 결과에 면책 문구를 유지하세요.
- 사진은 분석을 위해 Anthropic API로 전송됩니다. 개인정보 처리 안내를 사이트에 게시하세요.
