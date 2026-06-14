DeepfakeDetect — AI-Powered Deepfake Detection Platform
A compelete cybersecurity platform for detecting synthetic media (deepfakes) in images, video, and audio using a multi-model AI forensic pipeline.

Overview
DeepfakeDetect is a production-ready web application that provides forensic-grade deepfake detection across image, video, and audio media. It combines six parallel detection models — including GAN artifact analysis, facial biometric coherence checks, frequency-domain inspection, and audio-visual synchronization — into a single confidence score with per-indicator breakdowns.

Built for security teams, digital investigators, legal professionals, and enterprise compliance programs.

Features
Multi-Modal Detection — Analyze images (JPG, PNG, WebP), video (MP4, MOV), and audio (WAV, MP3)
6-Model Ensemble Pipeline — Parallel AI inference with confidence-weighted voting
Forensic Dashboard — Radar chart and per-indicator score breakdown for every analysis
Live Statistics — Real-time platform stats and weekly detection activity charts
Research Blog — Categorized security intelligence articles with full article view
Contact System — Organization inquiry form with database-persisted messages
REST API — Fully documented OpenAPI 3.0 spec with code-generated TypeScript hooks
Secure by Design — Ephemeral processing, no persistent media storage, SOC 2 aligned
Tech Stack
Layer	Technology
Frontend	React 19, Vite 7, Tailwind CSS v4, Wouter (routing)
UI Components	shadcn/ui, Recharts, Lucide Icons
Backend	Node.js 24, Express 5
Database	PostgreSQL + Drizzle ORM
Validation	Zod v4, drizzle-zod
API Contract	OpenAPI 3.0 → Orval (React Query hooks + Zod schemas)
Build	esbuild (API), Vite (frontend)
Package Manager	pnpm workspaces (monorepo)
Fonts	Montserrat (headings), Poppins (body)
Project Structure
.
├── artifacts/
│   ├── api-server/          # Express 5 REST API (port 8080)
│   │   └── src/
│   │       ├── routes/      # detection, articles, contact, stats
│   │       └── index.ts
│   └── deepfake-detection/  # React + Vite frontend
│       └── src/
│           ├── pages/       # Home, About, Services, Demo, Blog, BlogPost, Contact
│           ├── components/  # Navbar, Footer, MainLayout, shadcn/ui
│           └── index.css    # Theme variables (navy + cyan)
├── lib/
│   ├── api-client-react/    # Orval-generated React Query hooks
│   ├── api-spec/            # OpenAPI 3.0 specification + codegen config
│   ├── api-zod/             # Orval-generated Zod validation schemas
│   └── db/                  # Drizzle ORM schema + migrations
├── scripts/                 # Utility scripts
├── pnpm-workspace.yaml
└── tsconfig.base.json

Pages
Route	Description
/	Hero, platform stats, detection activity chart, how-it-works walkthrough
/about	Deepfake explainer, cybersecurity threat vectors, detection methods
/services	8 service capability cards (image, video, audio, API, biometrics, etc.)
/demo	Interactive drag-and-drop analyzer with radar chart result dashboard
/blog	Categorized research articles with filtering
/blog/:id	Full article view with tags
/contact	Inquiry form with subject routing and organization field
Getting Started
Prerequisites
Node.js 20+
pnpm — npm install -g pnpm
PostgreSQL database (Neon free tier recommended for quick setup)
Installation
# 1. Clone the repository
git clone https://github.com/your-username/deepfake-detect.git
cd deepfake-detect
# 2. Install all workspace dependencies
pnpm install

Environment Variables
Create artifacts/api-server/.env:

DATABASE_URL=postgresql://user:password@host:5432/deepfake_db
SESSION_SECRET=your-random-secret-string
PORT=8080

Database Setup
# Push schema to your database
pnpm --filter @workspace/db run push

Run Locally
Open two terminals:

# Terminal 1 — API Server (http://localhost:8080)
pnpm --filter @workspace/api-server run dev
# Terminal 2 — Frontend (http://localhost:5173)
pnpm --filter @workspace/deepfake-detection run dev

Open http://localhost:5173 in your browser.

API Endpoints
Method	Endpoint	Description
POST	/api/detection/analyze	Submit media for deepfake analysis
GET	/api/detection/results	List all past detection results
GET	/api/detection/results/:id	Get a specific detection result
GET	/api/articles	List articles (optional ?category= filter)
GET	/api/articles/:id	Get a single article
POST	/api/contact	Submit a contact inquiry
GET	/api/stats	Get platform-wide statistics
Full OpenAPI spec: lib/api-spec/openapi.yaml

Available Scripts
# Typecheck all packages
pnpm run typecheck
# Build all packages
pnpm run build
# Regenerate API hooks from OpenAPI spec
pnpm --filter @workspace/api-spec run codegen
# Push DB schema changes (development only)
pnpm --filter @workspace/db run push

Design System
Token	Value
Background	#1A2A40 (dark navy)
Primary Accent	#00CFA0 (cyan)
Heading Font	Montserrat (600–900 weight)
Body Font	Poppins (300–600 weight)
Border Radius	4px
Detection Pipeline
Each media submission is processed through a 4-stage pipeline:

Media Ingestion — Format normalization, metadata stripping, content segmentation
AI Model Ensemble — Six parallel models: GAN fingerprint detection, facial landmark analysis, frequency domain inspection, biometric coherence, temporal consistency, compression forensics
Confidence Scoring — Weighted ensemble voting produces a 0–100 confidence score with individual indicator values
Verdict & Report — Final verdict of Authentic, Suspicious, or Deepfake with supporting forensic evidence
Database Schema
Table	Description
detection_results	All analysis results with indicators (JSONB), verdict, confidence score
articles	Blog/research articles with category, tags, content, author
contact_messages	Submitted contact form entries
Contributing
Fork the repository
Create a feature branch: git checkout -b feature/your-feature
Commit your changes: git commit -m 'feat: add your feature'
Push to the branch: git push origin feature/your-feature
Open a Pull Request
Please follow the existing TypeScript conventions and run pnpm run typecheck before submitting.

License
MIT License — see LICENSE for details.

Acknowledgements
Detection models inspired by research from FaceForensics++, DeepFakeLab, and published work on GAN fingerprint detection
UI components by shadcn/ui
Charts by Recharts
Icons by Lucide
