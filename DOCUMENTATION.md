# Documentation Technique Complète - Créalia

## Table des Matières

1. [Vue d'ensemble du projet](#1-vue-densemble-du-projet)
2. [Architecture système](#2-architecture-système)
3. [Stack technique](#3-stack-technique)
4. [Schéma de base de données](#4-schéma-de-base-de-données)
5. [Modules et fonctionnalités](#5-modules-et-fonctionnalités)
6. [API et intégrations](#6-api-et-intégrations)
7. [Intelligence artificielle](#7-intelligence-artificielle)
8. [Traitement vidéo](#8-traitement-vidéo)
9. [Système de publication](#9-système-de-publication)
10. [Analytics et tracking](#10-analytics-et-tracking)
11. [Interface utilisateur](#11-interface-utilisateur)
12. [Sécurité et authentification](#12-sécurité-et-authentification)
13. [Performance et optimisation](#13-performance-et-optimisation)
14. [Tests et qualité](#14-tests-et-qualité)
15. [Déploiement](#15-déploiement)

---

## 1. Vue d'ensemble du projet

### 1.1 Mission et objectifs

**Créalia** est une plateforme de création de contenu vidéo automatisée alimentée par l'IA, conçue pour transformer des vidéos longues en contenus courts optimisés (Reels, Shorts, Stories) avec une direction artistique personnalisée et une publication multi-plateforme.

**Objectifs principaux:**
- Automatiser la création de contenu court à partir de vidéos sources
- Optimiser le contenu selon les plateformes (Instagram, TikTok, YouTube, Facebook)
- Fournir des analytics avancés pour améliorer les performances
- Guider les créateurs avec des suggestions basées sur l'IA
- Permettre une publication multi-plateforme centralisée

### 1.2 Proposition de valeur

- **Gain de temps:** Réduction de 90% du temps de production de contenu court
- **Optimisation IA:** Direction artistique et montage automatisés
- **Analytics prédictifs:** Insights pour maximiser l'engagement
- **Multi-plateforme:** Gestion centralisée de tous les réseaux sociaux
- **Personnalisation:** Respect du branding et de l'identité visuelle

### 1.3 Utilisateurs cibles

- Créateurs de contenu individuels (YouTubers, influenceurs)
- Agences de marketing digital
- Entreprises B2C avec présence sociale
- Community managers
- Équipes de production de contenu

---

## 2. Architecture système

### 2.1 Architecture globale

```
┌─────────────────────────────────────────────────────────────┐
│                     FRONTEND (React/Next.js)                 │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐     │
│  │   Dashboard  │  │   Editor     │  │   Analytics  │     │
│  └──────────────┘  └──────────────┘  └──────────────┘     │
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│                  API GATEWAY (Kong/AWS API Gateway)          │
│                    Authentication & Rate Limiting             │
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│                    BACKEND SERVICES (Node.js/Python)         │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐     │
│  │   User API   │  │   Video API  │  │   Social API │     │
│  └──────────────┘  └──────────────┘  └──────────────┘     │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐     │
│  │   AI Engine  │  │Analytics API │  │  Content API │     │
│  └──────────────┘  └──────────────┘  └──────────────┘     │
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│                    MESSAGE QUEUE (RabbitMQ/Kafka)            │
│          Job Scheduling & Async Processing                   │
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│                    WORKER SERVICES                           │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐     │
│  │Video Processor│ │  AI Worker   │  │ Publisher     │     │
│  └──────────────┘  └──────────────┘  └──────────────┘     │
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│                    DATA LAYER                                │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐     │
│  │  PostgreSQL  │  │    Redis     │  │  MongoDB     │     │
│  │  (Relations) │  │   (Cache)    │  │  (Analytics) │     │
│  └──────────────┘  └──────────────┘  └──────────────┘     │
│  ┌──────────────┐  ┌──────────────┐                        │
│  │  S3/Storage  │  │ Elasticsearch│                        │
│  │   (Media)    │  │   (Search)   │                        │
│  └──────────────┘  └──────────────┘                        │
└─────────────────────────────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────┐
│              EXTERNAL SERVICES & APIs                        │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐     │
│  │   OpenAI     │  │   Instagram  │  │   YouTube    │     │
│  └──────────────┘  └──────────────┘  └──────────────┘     │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐     │
│  │   TikTok     │  │   Facebook   │  │   FFmpeg     │     │
│  └──────────────┘  └──────────────┘  └──────────────┘     │
└─────────────────────────────────────────────────────────────┘
```

### 2.2 Principes architecturaux

**Microservices:**
- Découplage des fonctionnalités en services indépendants
- Scalabilité horizontale par service
- Déploiement indépendant et releases continues

**Event-Driven:**
- Communication asynchrone via message queue
- Resilience et retry automatique
- Traceabilité complète des événements

**API-First:**
- Conception API avant implémentation
- Documentation OpenAPI/Swagger
- Versioning d'API strict

**Cloud-Native:**
- Conteneurisation Docker
- Orchestration Kubernetes
- Infrastructure as Code (Terraform)

### 2.3 Patterns de conception

**Backend:**
- Repository Pattern (abstraction de la couche données)
- Service Layer Pattern (logique métier)
- Factory Pattern (création d'objets complexes)
- Strategy Pattern (algorithmes interchangeables pour l'IA)
- Observer Pattern (notifications et événements)
- Command Pattern (opérations de traitement vidéo)

**Frontend:**
- Container/Presenter Pattern
- Higher-Order Components (HOC)
- Render Props
- Custom Hooks
- Context API pour état global

---

## 3. Stack technique

### 3.1 Frontend

**Framework principal:**
```json
{
  "framework": "Next.js 14+",
  "language": "TypeScript 5.x",
  "ui_library": "React 18+",
  "styling": "Tailwind CSS 3.x + Styled Components",
  "state_management": "Zustand + React Query",
  "forms": "React Hook Form + Zod",
  "animation": "Framer Motion",
  "charts": "Recharts + D3.js",
  "video_player": "Video.js + HLS.js",
  "drag_drop": "dnd-kit",
  "notifications": "React Hot Toast"
}
```

**Dépendances critiques:**
```bash
# Core
next@14.2.0
react@18.3.0
typescript@5.4.0

# State & Data
zustand@4.5.0
@tanstack/react-query@5.28.0
axios@1.6.8

# UI Components
@radix-ui/react-*@latest
tailwindcss@3.4.0
framer-motion@11.0.0

# Forms & Validation
react-hook-form@7.51.0
zod@3.22.4

# Video
video.js@8.10.0
hls.js@1.5.7

# Utils
date-fns@3.6.0
lodash-es@4.17.21
uuid@9.0.1
```

### 3.2 Backend

**Services API (Node.js):**
```json
{
  "runtime": "Node.js 20 LTS",
  "framework": "Express.js 4.x / Fastify 4.x",
  "language": "TypeScript 5.x",
  "orm": "Prisma 5.x",
  "validation": "Zod",
  "auth": "Passport.js + JWT",
  "testing": "Jest + Supertest",
  "documentation": "Swagger/OpenAPI 3.0"
}
```

**Services de traitement (Python):**
```json
{
  "version": "Python 3.11+",
  "framework": "FastAPI 0.110+",
  "ml_framework": "PyTorch 2.2 / TensorFlow 2.15",
  "video_processing": "FFmpeg-python",
  "computer_vision": "OpenCV 4.x",
  "nlp": "Transformers (HuggingFace)",
  "async": "Celery + Redis",
  "testing": "pytest"
}
```

**Dépendances Node.js:**
```json
{
  "dependencies": {
    "express": "^4.19.0",
    "fastify": "^4.26.0",
    "@prisma/client": "^5.11.0",
    "passport": "^0.7.0",
    "passport-jwt": "^4.0.1",
    "jsonwebtoken": "^9.0.2",
    "bcrypt": "^5.1.1",
    "zod": "^3.22.4",
    "bull": "^4.12.0",
    "ioredis": "^5.3.2",
    "aws-sdk": "^2.1585.0",
    "sharp": "^0.33.3",
    "winston": "^3.12.0",
    "helmet": "^7.1.0",
    "cors": "^2.8.5",
    "compression": "^1.7.4",
    "express-rate-limit": "^7.2.0"
  }
}
```

**Dépendances Python:**
```txt
fastapi==0.110.0
uvicorn[standard]==0.28.0
sqlalchemy==2.0.28
alembic==1.13.1
pydantic==2.6.4
python-multipart==0.0.9
python-jose[cryptography]==3.3.0
passlib[bcrypt]==1.7.4
celery==5.3.6
redis==5.0.3
opencv-python==4.9.0.80
ffmpeg-python==0.2.0
torch==2.2.1
transformers==4.38.2
openai==1.14.0
anthropic==0.21.3
pillow==10.2.0
numpy==1.26.4
pandas==2.2.1
scikit-learn==1.4.1
moviepy==1.0.3
```

### 3.3 Base de données

**PostgreSQL (données relationnelles):**
```
Version: 16+
Use cases:
- Utilisateurs et authentification
- Projets et vidéos
- Configurations de comptes sociaux
- Relations entre entités
- Transactions critiques
```

**MongoDB (analytics et logs):**
```
Version: 7.0+
Use cases:
- Métriques de performance
- Logs d'activité
- Historique de modifications
- Données non structurées
- Time-series data
```

**Redis (cache et sessions):**
```
Version: 7.2+
Use cases:
- Sessions utilisateur
- Cache API responses
- Rate limiting
- Queue de jobs (Bull)
- Real-time features
```

**Elasticsearch (recherche):**
```
Version: 8.12+
Use cases:
- Recherche full-text
- Recherche de contenus
- Agrégations analytics
- Logs centralisés
```

### 3.4 Infrastructure

**Conteneurisation:**
```yaml
# Docker 24+
# Kubernetes 1.29+
# Helm 3.14+

services:
  - frontend: nginx + Next.js static
  - api-gateway: Kong/Traefik
  - user-service: Node.js
  - video-service: Node.js + FFmpeg
  - ai-service: Python + GPU support
  - analytics-service: Node.js
  - worker-video: Python + FFmpeg
  - worker-ai: Python + PyTorch
  - worker-publisher: Node.js
```

**Cloud Provider (AWS recommandé):**
```
- EC2/ECS/EKS: Compute
- S3: Stockage média
- CloudFront: CDN
- RDS: PostgreSQL managé
- DocumentDB: MongoDB compatible
- ElastiCache: Redis managé
- SQS/SNS: Message queue
- Lambda: Serverless functions
- CloudWatch: Monitoring
- Route53: DNS
```

**Alternative Cloud:**
```
- Google Cloud Platform:
  - GKE, Cloud Storage, Cloud SQL, Memorystore
- Azure:
  - AKS, Blob Storage, Azure Database, Redis Cache
- Hybrid/On-premise:
  - K8s self-hosted, MinIO, PostgreSQL, Redis
```

### 3.5 Outils de développement

```json
{
  "version_control": "Git + GitHub/GitLab",
  "ci_cd": "GitHub Actions / GitLab CI / Jenkins",
  "code_quality": "ESLint, Prettier, Pylint, Black",
  "testing": "Jest, Pytest, Cypress, Playwright",
  "monitoring": "Prometheus + Grafana",
  "logging": "ELK Stack (Elasticsearch, Logstash, Kibana)",
  "apm": "New Relic / Datadog / Elastic APM",
  "error_tracking": "Sentry",
  "documentation": "Swagger, TypeDoc, Sphinx"
}
```

---

## 4. Schéma de base de données

### 4.1 PostgreSQL - Schéma relationnel

```sql
-- =============================================
-- TABLE: users
-- Description: Stockage des utilisateurs
-- =============================================
CREATE TABLE users (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    email VARCHAR(255) UNIQUE NOT NULL,
    username VARCHAR(100) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    first_name VARCHAR(100),
    last_name VARCHAR(100),
    profile_picture_url TEXT,
    phone VARCHAR(20),
    timezone VARCHAR(50) DEFAULT 'UTC',
    language VARCHAR(10) DEFAULT 'fr',
    
    -- Subscription
    subscription_tier VARCHAR(50) DEFAULT 'free', -- free, pro, enterprise
    subscription_status VARCHAR(50) DEFAULT 'active',
    subscription_start_date TIMESTAMP,
    subscription_end_date TIMESTAMP,
    
    -- Limits
    monthly_video_quota INTEGER DEFAULT 10,
    monthly_videos_used INTEGER DEFAULT 0,
    storage_quota_gb INTEGER DEFAULT 5,
    storage_used_gb DECIMAL(10,2) DEFAULT 0,
    
    -- Metadata
    email_verified BOOLEAN DEFAULT FALSE,
    onboarding_completed BOOLEAN DEFAULT FALSE,
    last_login_at TIMESTAMP,
    last_active_at TIMESTAMP,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    deleted_at TIMESTAMP,
    
    -- Indexes
    CONSTRAINT chk_email CHECK (email ~* '^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}$')
);

CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_users_username ON users(username);
CREATE INDEX idx_users_subscription ON users(subscription_tier, subscription_status);
CREATE INDEX idx_users_created_at ON users(created_at);

-- =============================================
-- TABLE: social_accounts
-- Description: Comptes de réseaux sociaux connectés
-- =============================================
CREATE TABLE social_accounts (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
    
    platform VARCHAR(50) NOT NULL, -- instagram, tiktok, youtube, facebook, twitter, linkedin
    platform_user_id VARCHAR(255) NOT NULL,
    platform_username VARCHAR(255),
    platform_name VARCHAR(255),
    profile_picture_url TEXT,
    
    -- OAuth tokens
    access_token TEXT NOT NULL,
    refresh_token TEXT,
    token_expires_at TIMESTAMP,
    scope TEXT,
    
    -- Platform specific data (JSON)
    platform_data JSONB DEFAULT '{}',
    
    -- Status
    is_active BOOLEAN DEFAULT TRUE,
    is_primary BOOLEAN DEFAULT FALSE, -- compte principal par plateforme
    last_sync_at TIMESTAMP,
    
    -- Metadata
    connected_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    
    UNIQUE(user_id, platform, platform_user_id),
    CONSTRAINT chk_platform CHECK (platform IN ('instagram', 'tiktok', 'youtube', 'facebook', 'twitter', 'linkedin'))
);

CREATE INDEX idx_social_accounts_user ON social_accounts(user_id);
CREATE INDEX idx_social_accounts_platform ON social_accounts(platform);
CREATE INDEX idx_social_accounts_active ON social_accounts(is_active);

-- =============================================
-- TABLE: projects
-- Description: Projets de création de contenu
-- =============================================
CREATE TABLE projects (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
    
    name VARCHAR(255) NOT NULL,
    description TEXT,
    color VARCHAR(20) DEFAULT '#6366f1', -- pour l'UI
    
    -- Settings
    default_style_preset_id UUID, -- référence vers style_presets
    default_platforms JSONB DEFAULT '[]', -- ["instagram", "tiktok"]
    
    -- Organization
    is_archived BOOLEAN DEFAULT FALSE,
    folder VARCHAR(255),
    tags JSONB DEFAULT '[]',
    
    -- Metadata
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    deleted_at TIMESTAMP
);

CREATE INDEX idx_projects_user ON projects(user_id);
CREATE INDEX idx_projects_archived ON projects(is_archived);
CREATE INDEX idx_projects_created_at ON projects(created_at DESC);

-- =============================================
-- TABLE: source_videos
-- Description: Vidéos sources uploadées
-- =============================================
CREATE TABLE source_videos (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
    project_id UUID REFERENCES projects(id) ON DELETE SET NULL,
    
    -- File info
    title VARCHAR(255) NOT NULL,
    description TEXT,
    file_name VARCHAR(255) NOT NULL,
    file_path TEXT NOT NULL, -- S3 path
    file_size_bytes BIGINT NOT NULL,
    mime_type VARCHAR(100),
    
    -- Video properties
    duration_seconds DECIMAL(10,2),
    width INTEGER,
    height INTEGER,
    fps DECIMAL(10,2),
    bitrate INTEGER,
    codec VARCHAR(50),
    
    -- Processing status
    processing_status VARCHAR(50) DEFAULT 'pending', -- pending, processing, completed, failed
    processing_progress INTEGER DEFAULT 0, -- 0-100
    processing_error TEXT,
    
    -- AI Analysis (stored after processing)
    ai_transcript JSONB, -- transcription complète avec timestamps
    ai_scenes JSONB, -- détection de scènes
    ai_speakers JSONB, -- détection de locuteurs
    ai_topics JSONB, -- sujets identifiés
    ai_emotions JSONB, -- analyse émotionnelle
    ai_key_moments JSONB, -- moments clés identifiés
    
    -- Thumbnail
    thumbnail_url TEXT,
    
    -- Metadata
    uploaded_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    processed_at TIMESTAMP,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    deleted_at TIMESTAMP
);

CREATE INDEX idx_source_videos_user ON source_videos(user_id);
CREATE INDEX idx_source_videos_project ON source_videos(project_id);
CREATE INDEX idx_source_videos_status ON source_videos(processing_status);
CREATE INDEX idx_source_videos_uploaded_at ON source_videos(uploaded_at DESC);

-- =============================================
-- TABLE: style_presets
-- Description: Présets de direction artistique
-- =============================================
CREATE TABLE style_presets (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID REFERENCES users(id) ON DELETE CASCADE,
    
    name VARCHAR(255) NOT NULL,
    description TEXT,
    is_global BOOLEAN DEFAULT FALSE, -- preset système vs utilisateur
    
    -- Visual settings
    color_palette JSONB, -- {"primary": "#ff0000", "secondary": "#00ff00"}
    font_family VARCHAR(100),
    font_size_body INTEGER DEFAULT 16,
    font_size_title INTEGER DEFAULT 24,
    text_color VARCHAR(20) DEFAULT '#ffffff',
    text_background_color VARCHAR(20),
    text_position VARCHAR(50) DEFAULT 'bottom', -- top, center, bottom, custom
    
    -- Video effects
    filter_preset VARCHAR(100), -- vintage, vibrant, cinematic, etc.
    brightness DECIMAL(5,2) DEFAULT 1.0,
    contrast DECIMAL(5,2) DEFAULT 1.0,
    saturation DECIMAL(5,2) DEFAULT 1.0,
    
    -- Transitions
    transition_style VARCHAR(50) DEFAULT 'cut', -- cut, fade, slide, zoom
    transition_duration_ms INTEGER DEFAULT 300,
    
    -- Branding
    logo_url TEXT,
    logo_position VARCHAR(50), -- top-left, top-right, bottom-left, bottom-right
    logo_size INTEGER DEFAULT 100, -- pixels
    watermark_opacity DECIMAL(3,2) DEFAULT 0.8,
    
    -- Audio
    default_music_genre VARCHAR(100),
    music_volume DECIMAL(3,2) DEFAULT 0.3,
    voice_volume DECIMAL(3,2) DEFAULT 1.0,
    
    -- Advanced
    custom_css TEXT, -- pour overlays HTML personnalisés
    custom_effects JSONB DEFAULT '{}',
    
    -- Metadata
    usage_count INTEGER DEFAULT 0,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_style_presets_user ON style_presets(user_id);
CREATE INDEX idx_style_presets_global ON style_presets(is_global);

-- =============================================
-- TABLE: generated_contents
-- Description: Contenus courts générés
-- =============================================
CREATE TABLE generated_contents (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
    project_id UUID REFERENCES projects(id) ON DELETE SET NULL,
    source_video_id UUID REFERENCES source_videos(id) ON DELETE CASCADE,
    style_preset_id UUID REFERENCES style_presets(id) ON DELETE SET NULL,
    
    -- Basic info
    title VARCHAR(255) NOT NULL,
    description TEXT,
    
    -- Generation parameters
    generation_prompt TEXT, -- prompt fourni par l'utilisateur
    target_platforms JSONB NOT NULL, -- ["instagram", "tiktok"]
    target_duration_seconds INTEGER, -- durée souhaitée
    
    -- Video segments (from source)
    start_time_seconds DECIMAL(10,2),
    end_time_seconds DECIMAL(10,2),
    
    -- Output file
    output_file_path TEXT, -- S3 path
    output_file_size_bytes BIGINT,
    output_duration_seconds DECIMAL(10,2),
    output_width INTEGER,
    output_height INTEGER,
    output_format VARCHAR(20), -- mp4, mov, etc.
    
    -- Thumbnail
    thumbnail_url TEXT,
    
    -- Applied effects
    has_subtitles BOOLEAN DEFAULT FALSE,
    subtitle_style JSONB,
    applied_filters JSONB DEFAULT '[]',
    music_track_id UUID, -- référence vers music_library
    
    -- Generation status
    status VARCHAR(50) DEFAULT 'queued', -- queued, processing, completed, failed
    generation_progress INTEGER DEFAULT 0,
    generation_error TEXT,
    processing_time_seconds INTEGER,
    
    -- AI analysis
    ai_score DECIMAL(3,2), -- score de qualité prédit par l'IA (0-1)
    ai_predicted_engagement JSONB, -- prédictions d'engagement
    ai_suggestions JSONB, -- suggestions d'amélioration
    
    -- Publishing
    is_published BOOLEAN DEFAULT FALSE,
    scheduled_publish_at TIMESTAMP,
    
    -- Metadata
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    completed_at TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    deleted_at TIMESTAMP
);

CREATE INDEX idx_generated_contents_user ON generated_contents(user_id);
CREATE INDEX idx_generated_contents_project ON generated_contents(project_id);
CREATE INDEX idx_generated_contents_source ON generated_contents(source_video_id);
CREATE INDEX idx_generated_contents_status ON generated_contents(status);
CREATE INDEX idx_generated_contents_created_at ON generated_contents(created_at DESC);

-- =============================================
-- TABLE: published_posts
-- Description: Posts publiés sur les réseaux sociaux
-- =============================================
CREATE TABLE published_posts (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
    generated_content_id UUID REFERENCES generated_contents(id) ON DELETE SET NULL,
    social_account_id UUID NOT NULL REFERENCES social_accounts(id) ON DELETE CASCADE,
    
    -- Platform data
    platform VARCHAR(50) NOT NULL,
    platform_post_id VARCHAR(255), -- ID du post sur la plateforme
    platform_post_url TEXT,
    
    -- Content
    caption TEXT,
    hashtags JSONB DEFAULT '[]',
    mentions JSONB DEFAULT '[]',
    
    -- Publishing
    published_at TIMESTAMP,
    scheduled_for TIMESTAMP,
    publishing_status VARCHAR(50) DEFAULT 'draft', -- draft, scheduled, publishing, published, failed
    publishing_error TEXT,
    
    -- Performance snapshot (updated periodically)
    views_count INTEGER DEFAULT 0,
    likes_count INTEGER DEFAULT 0,
    comments_count INTEGER DEFAULT 0,
    shares_count INTEGER DEFAULT 0,
    saves_count INTEGER DEFAULT 0,
    engagement_rate DECIMAL(5,4), -- calculated
    
    last_metrics_update_at TIMESTAMP,
    
    -- Metadata
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_published_posts_user ON published_posts(user_id);
CREATE INDEX idx_published_posts_content ON published_posts(generated_content_id);
CREATE INDEX idx_published_posts_account ON published_posts(social_account_id);
CREATE INDEX idx_published_posts_platform ON published_posts(platform);
CREATE INDEX idx_published_posts_status ON published_posts(publishing_status);
CREATE INDEX idx_published_posts_published_at ON published_posts(published_at DESC);

-- =============================================
-- TABLE: music_library
-- Description: Bibliothèque de musiques libres de droits
-- =============================================
CREATE TABLE music_library (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    
    title VARCHAR(255) NOT NULL,
    artist VARCHAR(255),
    album VARCHAR(255),
    
    -- File info
    file_path TEXT NOT NULL,
    file_size_bytes BIGINT,
    duration_seconds DECIMAL(10,2),
    
    -- Metadata
    genre VARCHAR(100),
    mood VARCHAR(100), -- energetic, calm, upbeat, dramatic, etc.
    tempo_bpm INTEGER,
    
    -- Licensing
    license_type VARCHAR(100), -- creative_commons, royalty_free, etc.
    attribution_required BOOLEAN DEFAULT FALSE,
    attribution_text TEXT,
    
    -- Usage
    is_active BOOLEAN DEFAULT TRUE,
    usage_count INTEGER DEFAULT 0,
    
    -- Metadata
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_music_library_genre ON music_library(genre);
CREATE INDEX idx_music_library_mood ON music_library(mood);
CREATE INDEX idx_music_library_active ON music_library(is_active);

-- =============================================
-- TABLE: ai_prompts
-- Description: Templates de prompts IA
-- =============================================
CREATE TABLE ai_prompts (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID REFERENCES users(id) ON DELETE CASCADE,
    
    name VARCHAR(255) NOT NULL,
    description TEXT,
    category VARCHAR(100), -- content_creation, analysis, optimization, etc.
    
    prompt_template TEXT NOT NULL,
    variables JSONB DEFAULT '[]', -- variables dans le template
    
    is_global BOOLEAN DEFAULT FALSE,
    is_favorite BOOLEAN DEFAULT FALSE,
    
    usage_count INTEGER DEFAULT 0,
    
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_ai_prompts_user ON ai_prompts(user_id);
CREATE INDEX idx_ai_prompts_category ON ai_prompts(category);
CREATE INDEX idx_ai_prompts
## 7. Intégrations avec les API sociales

Pour offrir une expérience fluide, Créalia intègre directement les API des principales plateformes sociales.

### Plateformes supportées
- **YouTube Data API** → publication sur YouTube Shorts
- **TikTok API** → upload direct et gestion de métadonnées
- **Instagram Graph API** → publication de Reels
- **Facebook Graph API** → publication croisée
- **Twitter/X API** → publication de clips courts
- **LinkedIn API** → publication B2B (teasers, webinars)

### Fonctionnalités
- Authentification OAuth2 par utilisateur
- Planification de posts (scheduler interne)
- Suivi des statistiques (likes, vues, partages) récupérées depuis les APIs
- Multi-compte (un utilisateur peut connecter plusieurs chaînes/pages)

### Flux de données
1. L’utilisateur connecte son compte social via OAuth
2. La vidéo générée est stockée sur S3
3. L’API Créalia envoie la vidéo + métadonnées à la plateforme choisie
4. Les métriques (vues, engagement) sont synchronisées dans le dashboard

### Schéma d’intégration
```mermaid
flowchart LR
    A[Créalia] -->|OAuth2| B((YouTube))
    A -->|OAuth2| C((TikTok))
    A -->|OAuth2| D((Instagram))
    A -->|OAuth2| E((Twitter/X))
    A -->|OAuth2| F((LinkedIn))
