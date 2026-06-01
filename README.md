# Study Smart

[![CI](https://github.com/lidge-jun/study-smart-app/actions/workflows/ci.yml/badge.svg)](https://github.com/lidge-jun/study-smart-app/actions/workflows/ci.yml)
[![Pages](https://github.com/lidge-jun/study-smart-app/actions/workflows/pages.yml/badge.svg)](https://github.com/lidge-jun/study-smart-app/actions/workflows/pages.yml)
![Next.js](https://img.shields.io/badge/next-15.5.18-111827)
![React](https://img.shields.io/badge/react-19-111827)
![License pending](https://img.shields.io/badge/license-pending-6b7280)

포모도로 기법과 학습 데이터 시각화 기반 학습 시간 관리 웹 애플리케이션입니다. Supabase 인증/DB, Next.js App Router, 주간/월간 분석, AI chat, 파일 파서, 프로필 게임화 기능을 포함합니다.

## Public Surface

| Area | Current status |
| --- | --- |
| Repository | Public repo, GitHub reports 0 stars / 0 forks |
| Production URL | https://study-smart-app-two.vercel.app |
| Framework | Next.js 15.5.18, React 19, TypeScript, Tailwind CSS |
| Backend | Supabase Auth + PostgreSQL + storage migrations |
| Core app | Pomodoro timer, dashboard, weekly view, calendar, profile, settings |
| AI surface | Local browser API key manager, chat sessions, file parsing for study context |
| GitHub Pages | Prepared docs surface from `/docs` after an authorized push |
| CI | Prepared in `.github/workflows/ci.yml`; no remote GitHub Actions runs yet |
| License | No root `LICENSE` file is declared in this repository |

## Features

- Pomodoro timer with custom session settings and auto-start options.
- Real-time dashboard metrics and chart visualizations.
- Weekly study pattern view with heatmaps and insight cards.
- Calendar view with monthly heatmap, journal editor, and session detail modal.
- Profile and gamification: level, badges, goals, study analysis.
- Supabase authentication and user settings.
- AI chat surface with API key manager, chat sessions, file upload, and parsers for PDF, DOCX, CSV, code, image, and text.
- Responsive app shell for desktop and mobile use.

## Quickstart

```bash
npm ci
cp .env.example .env.local
npm run dev
```

Fill `.env.local` with Supabase values:

```env
NEXT_PUBLIC_SUPABASE_URL=your_supabase_project_url
NEXT_PUBLIC_SUPABASE_ANON_KEY=your_supabase_anon_key
NEXT_PUBLIC_BASE_URL=http://localhost:3000
NEXT_PUBLIC_ENV=development
SUPABASE_SERVICE_ROLE_KEY=your_supabase_service_role_key
```

## Verification

```bash
npm ci
NEXT_PUBLIC_SUPABASE_URL=https://example.supabase.co \
NEXT_PUBLIC_SUPABASE_ANON_KEY=dummy-anon-key \
SUPABASE_SERVICE_ROLE_KEY=dummy-service-key \
NEXT_PUBLIC_BASE_URL=http://localhost:3000 \
npm run build
npm audit --audit-level=high
```

`npm run build` needs Supabase-looking environment values because App Router API routes instantiate Supabase clients during build-time page collection. The dummy values above are only for static verification; they are not valid app credentials.

Current audit state after package updates: `npm audit --audit-level=high` passes. `npm audit` still reports two moderate advisories through the current Next/PostCSS chain; do not claim a zero-vulnerability tree until those are resolved by a compatible upstream update.

## Architecture

```text
Next.js App Router
  -> Supabase auth/client/server helpers
  -> dashboard/calendar/weekly/profile/pomodoro routes
  -> Zustand stores for timer, goals, AI chat
  -> Supabase migrations under supabase/migrations
```

Key directories:

| Path | Purpose |
| --- | --- |
| `app/` | App Router pages, layouts, API routes, auth callback |
| `components/` | UI, dashboard, charts, calendar, weekly, pomodoro, AI chat |
| `lib/` | Analytics, AI provider adapters, Supabase clients, parsers, utilities |
| `store/` | Zustand state for timer, goals, and AI chat |
| `supabase/migrations/` | Database schema and RPC migrations |
| `docs/` | Prepared GitHub Pages public documentation |

## Security & Privacy

- Do not commit `.env.local`, Supabase service role keys, user exports, or chat/session data.
- `SUPABASE_SERVICE_ROLE_KEY` is server-only and must never be exposed in client code.
- AI chat API keys are managed in the browser-side app surface; treat browser storage and exports as sensitive.
- File parsers may process private study documents. Avoid logging raw file content.
- GitHub Pages hosts documentation only; the live app remains on Vercel/Supabase.

## License

This repository currently has no root `LICENSE` file. Add an explicit license before redistributing or depending on the project externally.
