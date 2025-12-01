markdown_content = """# 🏥 Mesai Dışı Denetim Uygulaması - Detaylı Proje Planı

## 📋 İçindekiler
1. [Proje Özeti](#proje-özeti)
2. [Teknik Mimari](#teknik-mimari)
3. [Database Schema](#database-schema)
4. [Rol Yetkilendirme Sistemi](#rol-yetkilendirme-sistemi)
5. [Denetim İş Akışı](#denetim-iş-akışı)
6. [Raporlama ve Analiz Sistemi](#raporlama-ve-analiz-sistemi)
7. [Bildirim Sistemi](#bildirim-sistemi)
8. [Platform Özellikleri](#platform-özellikleri)
9. [Geliştirme Fazları](#geliştirme-fazları)
10. [Ek Öneriler](#ek-öneriler)
11. [UI/UX Önerileri](#uiux-önerileri)
12. [Proje Yönetimi](#proje-yönetimi)
13. [Riskler ve Çözümler](#riskler-ve-çözümler)
14. [Başarı Metrikleri](#başarı-metrikleri)

---

## 📊 Proje Özeti

### Genel Bakış
Sağlık tesisleri için çoklu platform (iOS, Android, Web) mesai dışı denetim yönetim sistemi. Dinamik denetim yapısı ile esnek ve ölçeklenebilir çözüm.

### Kapsam
- **Platform**: iOS (iPhone/iPad), Android (Mobil/Tablet), Web App
- **Dağıtım**: App Store, Google Play, Web (self-hosted)
- **Denetim Yapısı**: 18 bölüm, 218 soru, 16 kategori
- **Kullanıcı Rolleri**: 5 farklı rol seviyesi
- **Dil Desteği**: Türkçe (başlangıç), İngilizce (gelecek)

### Temel Özellikler
- ✅ Dinamik denetim şablonu oluşturma
- ✅ Akıllı denetim planlama ve ekip yönetimi
- ✅ Offline denetim yapabilme
- ✅ Önceki denetimlerle karşılaştırma
- ✅ Düzeltici faaliyet yönetimi
- ✅ Gelişmiş raporlama ve analiz
- ✅ Çoklu bildirim kanalları
- ✅ Rol bazlı erişim kontrolü

---

## 🎯 Teknik Mimari

### Backend Stack

#### Core Technologies
- **Database**: PostgreSQL 15+
  - ACID uyumluluğu
  - JSON/JSONB desteği (esnek veri yapıları için)
  - Full-text search
  - Partitioning (büyük veri setleri için)
  
- **Backend Framework**: Node.js 20+ LTS + Express.js + TypeScript
  - Type-safety
  - Modern async/await
  - Middleware ekosistemi
  
- **ORM**: Prisma 5+
  - Type-safe database client
  - Otomatik migration
  - Introspection
  - Prisma Studio (database GUI)

- **API Architecture**: 
  - **RESTful API**: CRUD operasyonları için
  - **GraphQL**: Karmaşık sorgular ve ilişkisel veri için
  - **API Versioning**: /api/v1, /api/v2
  - **Rate Limiting**: DDoS koruması

#### Authentication & Security
- **Authentication**: JWT (Access Token) + Refresh Token
  - Access Token: 15 dakika
  - Refresh Token: 7 gün
  - HttpOnly cookies
  
- **Authorization**: RBAC (Role-Based Access Control)
  - Granular permissions
  - Resource-level access control
  
- **Password**: bcrypt (salt rounds: 12)
- **2FA**: TOTP (Time-based One-Time Password)
- **API Security**: 
  - Helmet.js (HTTP headers)
  - CORS configuration
  - Input validation (Joi/Zod)
  - SQL injection prevention
  - XSS protection

#### File Management
- **Primary**: AWS S3
  - Scalable storage
  - CDN integration (CloudFront)
  - Lifecycle policies
  - Versioning
  
- **Alternative**: MinIO (self-hosted)
  - S3-compatible
  - On-premise deployment
  - Cost-effective
  
- **Image Processing**: Sharp
  - Resize, compress
  - Format conversion
  - Thumbnail generation
  - WebP support

#### Real-time & Communication
- **Real-time**: Socket.io
  - Bildirimler
  - Live denetim durumu
  - Collaborative editing (gelecek)
  
- **Email**: NodeMailer + SMTP
  - Template engine (Handlebars)
  - Queue system (Bull)
  - Retry mechanism
  - Bounce handling
  
- **SMS** (Opsiyonel): Twilio / Netgsm
  - Kritik bildirimler
  - 2FA verification

#### Background Jobs
- **Queue**: Bull (Redis-based)
  - Email sending
  - Report generation
  - Notification dispatch
  - Data cleanup
  - Scheduled reminders

#### Admin Panel
- **AdminJS** (PostgreSQL için)
  - Auto-generated CRUD
  - Custom actions
  - Dashboard widgets
  - Export/Import
  - Audit logs

#### Caching & Performance
- **Redis**: 
  - Session storage
  - API response caching
  - Rate limiting
  - Queue management
  
- **Database Optimization**:
  - Connection pooling
  - Query optimization
  - Indexing strategy
  - Materialized views

---

### Frontend Stack

#### Web Application
- **Framework**: React 18+ + TypeScript
- **Build Tool**: Vite
  - Fast HMR
  - Optimized builds
  - Plugin ecosystem
  
- **State Management**: 
  - **Zustand**: Lightweight, simple API
  - **Alternative**: Redux Toolkit (complex state için)
  - **React Query**: Server state management
  
- **Routing**: React Router v6
  - Nested routes
  - Protected routes
  - Lazy loading
  
- **UI Framework**: 
  - **Option 1**: Material-UI (MUI)
    - Comprehensive components
    - Theming system
    - Accessibility
  - **Option 2**: Ant Design
    - Enterprise-grade
    - Rich components
    - Form handling
  
- **Form Management**: 
  - React Hook Form
  - Zod validation
  - Type-safe schemas
  
- **Charts & Visualization**: 
  - Recharts (React-native)
  - Chart.js (feature-rich)
  - D3.js (custom visualizations)
  
- **File Upload**: 
  - React Dropzone
  - Progress tracking
  - Drag & drop
  - Multiple files
  
- **Date/Time**: 
  - date-fns (lightweight)
  - Day.js (Moment.js alternative)
  
- **Rich Text Editor** (Opsiyonel):
  - Lexical (Facebook)
  - Tiptap
  
- **PDF Generation**: 
  - jsPDF
  - pdfmake
  - React-PDF

#### Mobile Application
- **Framework**: React Native + Expo
  - Single codebase
  - OTA updates
  - Managed workflow
  - EAS Build
  
- **Navigation**: React Navigation
  - Stack, Tab, Drawer
  - Deep linking
  - Authentication flow
  
- **UI Library**: 
  - **Option 1**: React Native Paper (Material Design)
  - **Option 2**: NativeBase (Customizable)
  - **Option 3**: Tamagui (Performance-focused)
  
- **State Management**: Zustand (web ile aynı)
  
- **Local Storage**: 
  - AsyncStorage
  - MMKV (faster alternative)
  - Encrypted storage (sensitive data)
  
- **Offline Support**: 
  - Redux Persist / Zustand Persist
  - NetInfo (connectivity detection)
  - Queue system (offline actions)
  
- **Camera**: 
  - expo-camera
  - expo-image-picker
  - Image compression
  
- **Notifications**: 
  - expo-notifications
  - Push notification tokens
  - Background notifications
  
- **Biometrics**: 
  - expo-local-authentication
  - Face ID, Touch ID, Fingerprint

#### Shared Libraries
- **API Client**: Axios
  - Interceptors
  - Request/response transformation
  - Timeout handling
  
- **Validation**: Zod
  - Type inference
  - Schema composition
  - Error messages
  
- **Date**: date-fns
  - Tree-shakeable
  - Immutable
  - i18n support
  
- **Utilities**: Lodash-es (tree-shakeable)

---

### DevOps & Infrastructure

#### Containerization
- **Docker**: 
  - Multi-stage builds
  - Docker Compose (local development)
  - Health checks
  
- **Services**:
  - Backend API
  - PostgreSQL
  - Redis
  - MinIO (optional)
  - Nginx (reverse proxy)

#### CI/CD
- **GitHub Actions**:
  - Automated testing
  - Linting & formatting
  - Build & deploy
  - Mobile app builds (EAS)
  
- **Pipeline Stages**:
  1. Lint & Format check
  2. Unit tests
  3. Integration tests
  4. Build
  5. Deploy to staging
  6. E2E tests
  7. Deploy to production

#### Hosting & Deployment

**Backend & Database**:
- **Option 1**: AWS
  - EC2 (backend)
  - RDS PostgreSQL (managed)
  - ElastiCache Redis
  - S3 + CloudFront
  - Load Balancer
  
- **Option 2**: DigitalOcean
  - Droplets (backend)
  - Managed PostgreSQL
  - Managed Redis
  - Spaces (S3-compatible)
  - Load Balancer
  
- **Option 3**: Self-hosted
  - VPS (Hetzner, OVH)
  - Docker Swarm / Kubernetes
  - Backup strategy

**Web Application**:
- **Option 1**: Vercel
  - Zero-config
  - Edge network
  - Preview deployments
  
- **Option 2**: Netlify
  - Similar to Vercel
  - Form handling
  
- **Option 3**: Self-hosted
  - Nginx
  - SSL (Let's Encrypt)

**Mobile Applications**:
- **iOS**: App Store Connect
  - TestFlight (beta testing)
  - App Review process
  
- **Android**: Google Play Console
  - Internal/Closed/Open testing
  - Staged rollout

#### Monitoring & Logging
- **Error Tracking**: Sentry
  - Real-time alerts
  - Stack traces
  - User context
  - Performance monitoring
  
- **Logging**: 
  - Winston (Node.js)
  - Log levels
  - Log rotation
  - Centralized logging (optional: ELK stack)
  
- **APM** (Application Performance Monitoring):
  - New Relic / DataDog (paid)
  - Prometheus + Grafana (open-source)
  
- **Uptime Monitoring**: 
  - UptimeRobot
  - Pingdom
  - StatusPage.io

#### Backup & Disaster Recovery
- **Database Backup**:
  - Daily automated backups
  - Point-in-time recovery
  - Off-site backup storage
  - Backup testing (monthly)
  
- **File Backup**:
  - S3 versioning
  - Cross-region replication
  
- **Disaster Recovery Plan**:
  - RTO (Recovery Time Objective): 4 hours
  - RPO (Recovery Point Objective): 1 hour
  - Documented procedures
  - Regular drills

---

## 🗄️ Database Schema (PostgreSQL)

### Core Tables

#### Users & Authentication

```
sql
-- Kullanıcılar
CREATE TABLE users (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    email VARCHAR(255) UNIQUE NOT NULL,
    password_hash VARCHAR(255) NOT NULL,
    full_name VARCHAR(255) NOT NULL,
    phone VARCHAR(20),
    avatar_url TEXT,
    role_id INTEGER NOT NULL REFERENCES roles(id),
    is_active BOOLEAN DEFAULT true,
    is_email_verified BOOLEAN DEFAULT false,
    email_verification_token VARCHAR(255),
    password_reset_token VARCHAR(255),
    password_reset_expires TIMESTAMP,
    last_login_at TIMESTAMP,
    two_factor_secret VARCHAR(255),
    two_factor_enabled BOOLEAN DEFAULT false,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    deleted_at TIMESTAMP -- Soft delete
);

CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_users_role_id ON users(role_id);
CREATE INDEX idx_users_is_active ON users(is_active);

-- Refresh Token'lar
CREATE TABLE refresh_tokens (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
    token VARCHAR(500) UNIQUE NOT NULL,
    expires_at TIMESTAMP NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    revoked_at TIMESTAMP
);

CREATE INDEX idx_refresh_tokens_user_id ON refresh_tokens(user_id);
CREATE INDEX idx_refresh_tokens_token ON refresh_tokens(token);
```

#### Roles & Permissions

```
sql
-- Roller
CREATE TABLE roles (
    id SERIAL PRIMARY KEY,
    name VARCHAR(50) UNIQUE NOT NULL,
    display_name VARCHAR(100) NOT NULL,
    description TEXT,
    permissions JSONB NOT NULL DEFAULT '{}',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Varsayılan roller
INSERT INTO roles (name, display_name, description, permissions) VALUES
('admin', 'Sistem Yöneticisi', 'Tüm sistem erişimi', 
 '{"all": true}'::jsonb),
('group_admin', 'Grup Yöneticisi', 'Tesis grubu yönetimi', 
 '{"facilities": ["create", "read", "update", "delete"], "audits": ["create", "read", "update"], "users": ["create", "read", "update"], "reports": ["read", "export"]}'::jsonb),
('auditor', 'Denetmen', 'Denetim gerçekleştirme', 
 '{"audits": ["read", "update"], "reports": ["read"]}'::jsonb),
('controller', 'Kontrolcü', 'Denetim sonuçları yönetimi', 
 '{"audits": ["read"], "reports": ["read", "export"], "corrective_actions": ["create", "read", "update"]}'::jsonb),
('hospital_manager', 'Hastane Yöneticisi', 'Düzeltici faaliyet yönetimi', 
 '{"corrective_actions": ["read", "update"]}'::jsonb);
```

#### Facilities & Groups

```
sql
-- Tesis Grupları
CREATE TABLE facility_groups (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    name VARCHAR(255) NOT NULL,
    description TEXT,
    logo_url TEXT,
    contact_email VARCHAR(255),
    contact_phone VARCHAR(20),
    address TEXT,
    is_active BOOLEAN DEFAULT true,
    created_by UUID REFERENCES users(id),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    deleted_at TIMESTAMP
);

CREATE INDEX idx_facility_groups_is_active ON facility_groups(is_active);

-- Tesisler (Hastaneler)
CREATE TABLE facilities (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    group_id UUID NOT NULL REFERENCES facility_groups(id) ON DELETE CASCADE,
    name VARCHAR(255) NOT NULL,
    code VARCHAR(50) UNIQUE, -- Hastane kodu (örn: MPP-01)
    type VARCHAR(50), -- hospital, clinic, medical_center
    address TEXT,
    city VARCHAR(100),
    district VARCHAR(100),
    postal_code VARCHAR(10),
    phone VARCHAR(20),
    email VARCHAR(255),
    contact_person VARCHAR(255),
    contact_person_phone VARCHAR(20),
    latitude DECIMAL(10, 8),
    longitude DECIMAL(11, 8),
    metadata JSONB DEFAULT '{}', -- Ek bilgiler (yatak sayısı, bölümler vs.)
    is_active BOOLEAN DEFAULT true,
    created_by UUID REFERENCES users(id),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    deleted_at TIMESTAMP
);

CREATE INDEX idx_facilities_group_id ON facilities(group_id);
CREATE INDEX idx_facilities_code ON facilities(code);
CREATE INDEX idx_facilities_is_active ON facilities(is_active);
CREATE INDEX idx_facilities_city ON facilities(city);

-- Kullanıcı-Tesis Atamaları
CREATE TABLE user_facility_assignments (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
    facility_id UUID NOT NULL REFERENCES facilities(id) ON DELETE CASCADE,
    role_id INTEGER NOT NULL REFERENCES roles(id),
    assigned_by UUID REFERENCES users(id),
    assigned_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    expires_at TIMESTAMP, -- Geçici atamalar için
    is_active BOOLEAN DEFAULT true,
    UNIQUE(user_id, facility_id, role_id)
);

CREATE INDEX idx_user_facility_user_id ON user_facility_assignments(user_id);
CREATE INDEX idx_user_facility_facility_id ON user_facility_assignments(facility_id);
CREATE INDEX idx_user_facility_role_id ON user_facility_assignments(role_id);
```

#### Question Pool

```
sql
-- Kategoriler
CREATE TABLE question_categories (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) UNIQUE NOT NULL,
    description TEXT,
    color VARCHAR(7), -- Hex color code
    icon VARCHAR(50), -- Icon name
    order_index INTEGER,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- 16 kategori
INSERT INTO question_categories (name, color, order_index) VALUES
('Acil Durum Yönetimi', '#FF5252', 1),
('Atık Yönetimi', '#8D6E63', 2),
('Bilgi Güvenliği', '#2196F3', 3),
('Cihaz Yönetimi', '#9C27B0', 4),
('Emniyet', '#FF9800', 5),
('Enerji Yönetimi', '#4CAF50', 6),
('Erişim Kolaylığı', '#00BCD4', 7),
('Güvenlik', '#F44336', 8),
('Hasta Mahremiyeti', '#E91E63', 9),
('Malzeme Yönetimi', '#795548', 10),
('Personel', '#3F51B5', 11),
('Teh. Mad. Yönetimi', '#FF5722', 12),
('Temizlik ve Düzen', '#009688', 13),
('Tesis Yönetimi', '#607D8B', 14),
('Yangın Güvenliği', '#D32F2F', 15),
('İlaç Yönetimi', '#1976D2', 16);

-- Bölümler
CREATE TABLE question_sections (
    id SERIAL PRIMARY KEY,
    section_number INTEGER UNIQUE NOT NULL,
    name VARCHAR(255) NOT NULL,
    description TEXT,
    order_index INTEGER,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- 18 bölüm
INSERT INTO question_sections (section_number, name, order_index) VALUES
(1, 'Hastane Bahçesi / Dış Alan', 1),
(2, 'Hastane Girişi / Lobi', 2),
(3, 'Acil Servis', 3),
(4, 'Poliklinikler', 4),
(5, 'Yatan Hasta Servisleri', 5),
(6, 'Yoğun Bakım Üniteleri', 6),
(7, 'Ameliyathaneler', 7),
(8, 'Doğumhane', 8),
(9, 'Yenidoğan Ünitesi', 9),
(10, 'Görüntüleme Birimleri (Radyoloji)', 10),
(11, 'Laboratuvar', 11),
(12, 'Eczane', 12),
(13, 'Sterilizasyon Ünitesi', 13),
(14, 'Mutfak ve Yemekhane', 14),
(15, 'Çamaşırhane', 15),
(16, 'Teknik Alanlar (Kazan Dairesi, Jeneratör)', 16),
(17, 'Atık Toplama ve Saklama Alanları', 17),
(18, 'Personel Alanları', 18);

-- Soru Havuzu
CREATE TABLE question_pool (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    section_id INTEGER NOT NULL REFERENCES question_sections(id),
    category_id INTEGER NOT NULL REFERENCES question_categories(id),
    question_number INTEGER NOT NULL, -- Global soru numarası
    local_number INTEGER NOT NULL, -- Bölüm içi sıra numarası
    text TEXT NOT NULL,
    weight INTEGER NOT NULL CHECK (weight BETWEEN 1 AND 5), -- Soru ağırlığı
    description TEXT, -- Ek açıklama
    reference TEXT, -- Referans doküman/yönetmelik
    is_active BOOLEAN DEFAULT true,
    version INTEGER DEFAULT 1, -- Soru versiyonu
    parent_question_id UUID REFERENCES question_pool(id), -- Versiyon takibi için
    created_by UUID REFERENCES users(id),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    deleted_at TIMESTAMP
);

CREATE INDEX idx_question_pool_section_id ON question_pool(section_id);
CREATE INDEX idx_question_pool_category_id ON question_pool(category_id);
CREATE INDEX idx_question_pool_question_number ON question_pool(question_number);
CREATE INDEX idx_question_pool_is_active ON question_pool(is_active);

-- Soru etiketleri (arama ve filtreleme için)
CREATE TABLE question_tags (
    id SERIAL PRIMARY KEY,
    name VARCHAR(50) UNIQUE NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE question_pool_tags (
    question_id UUID REFERENCES question_pool(id) ON DELETE CASCADE,
    tag_id INTEGER REFERENCES question_tags(id) ON DELETE CASCADE,
    PRIMARY KEY (question_id, tag_id)
);
```

#### Audit Templates

```
sql
-- Denetim Şablonları
CREATE TABLE audit_templates (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    group_id UUID NOT NULL REFERENCES facility_groups(id) ON DELETE CASCADE,
    name VARCHAR(255) NOT NULL,
    description TEXT,
    version VARCHAR(20), -- v1.0, v2.1 gibi
    is_active BOOLEAN DEFAULT true,
    is_default BOOLEAN DEFAULT false, -- Varsayılan şablon
    total_questions INTEGER DEFAULT 0,
    total_weight INTEGER DEFAULT 0,
    metadata JSONB DEFAULT '{}', -- Ek bilgiler
    created_by UUID REFERENCES users(id),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    deleted_at TIMESTAMP
);

CREATE INDEX idx_audit_templates_group_id ON audit_templates(group_id);
CREATE INDEX idx_audit_templates_is_active ON audit_templates(is_active);

-- Şablon-Soru İlişkisi
CREATE TABLE audit_template_questions (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    template_id UUID NOT NULL REFERENCES audit_templates(id) ON DELETE CASCADE,
    question_id UUID NOT NULL REFERENCES question_pool(id),
    order_index INTEGER NOT NULL,
    is_required BOOLEAN DEFAULT true, -- Zorunlu soru mu?
    custom_weight INTEGER, -- Şablona özel ağırlık (null ise soru ağırlığı kullanılır)
    added_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(template_id, question_id)
);

CREATE INDEX idx_template_questions_template_id ON audit_template_questions(template_id);
CREATE INDEX idx_template_questions_question_id ON audit_template_questions(question_id);

-- Şablon geçmişi (versiyonlama)
CREATE TABLE audit_template_history (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    template_id UUID NOT NULL REFERENCES audit_templates(id) ON DELETE CASCADE,
    version VARCHAR(20) NOT NULL,
    changes JSONB NOT NULL, -- Yapılan değişiklikler
    changed_by UUID REFERENCES users(id),
    changed_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

#### Audits

```
sql
-- Denetimler
CREATE TABLE audits (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    template_id UUID NOT NULL REFERENCES audit_templates(id),
    facility_id UUID NOT NULL REFERENCES facilities(id),
    audit_code VARCHAR(50) UNIQUE, -- DEN-2024-001 gibi
    scheduled_date DATE NOT NULL,
    scheduled_time TIME NOT NULL,
    scheduled_end_time TIME,
    actual_start_time TIMESTAMP,
    actual_end_time TIMESTAMP,
    status VARCHAR(50) NOT NULL DEFAULT 'scheduled', 
    -- scheduled, notified, in_progress, completed, approved, cancelled
    questions_visible_at TIMESTAMP, -- Sorular ne zaman görünür olacak
    notes TEXT,
    metadata JSONB DEFAULT '{}',
    created_by UUID REFERENCES users(id),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    cancelled_at TIMESTAMP,
    cancelled_by UUID REFERENCES users(id),
    cancellation_reason TEXT
);

CREATE INDEX idx_audits_template_id ON audits(template_id);
CREATE INDEX idx_audits_facility_id ON audits(facility_id);
CREATE INDEX idx_audits_status ON audits(status);
CREATE INDEX idx_audits_scheduled_date ON audits(scheduled_date);
CREATE INDEX idx_audits_audit_code ON audits(audit_code);

-- Denetim Ekibi
CREATE TABLE audit_team_members (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    audit_id UUID NOT NULL REFERENCES audits(id) ON DELETE CASCADE,
    user_id UUID NOT NULL REFERENCES users(id),
    role VARCHAR(50) DEFAULT 'auditor', -- lead_auditor, auditor
    has_approved BOOLEAN DEFAULT false,
    approved_at TIMESTAMP,
    approval_notes TEXT,
    notified_at TIMESTAMP,
    notification_read_at TIMESTAMP,
    UNIQUE(audit_id, user_id)
);

CREATE INDEX idx_audit_team_audit_id ON audit_team_members(audit_id);
CREATE INDEX idx_audit_team_user_id ON audit_team_members(user_id);

-- Denetim Cevapları
CREATE TABLE audit_responses (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    audit_id UUID NOT NULL REFERENCES audits(id) ON DELETE CASCADE,
    question_id UUID NOT NULL REFERENCES question_pool(id),
    response_type VARCHAR(50) NOT NULL, 
    -- meets (Karşılıyor), partially_meets (Kısmen), does_not_meet (Karşılamıyor), out_of_scope (Kapsam Dışı)
    score INTEGER, -- Hesaplanan puan
    max_score INTEGER, -- Maksimum puan
    description TEXT,
    photos JSONB DEFAULT '[]', -- [{url, filename, size, uploaded_at}]
    attachments JSONB DEFAULT '[]', -- PDF ve diğer dosyalar
    answered_by UUID REFERENCES users(id),
    answered_at TIMESTAMP,
    is_draft BOOLEAN DEFAULT false, -- Taslak mı?
    previous_response_id UUID REFERENCES audit_responses(id), -- Önceki denetim cevabı
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(audit_id, question_id)
);

CREATE INDEX idx_audit_responses_audit_id ON audit_responses(audit_id);
CREATE INDEX idx_audit_responses_question_id ON audit_responses(question_id);
CREATE INDEX idx_audit_responses_response_type ON audit_responses(response_type);
CREATE INDEX idx_audit_responses_answered_by ON audit_responses(answered_by);

-- Cevap geçmişi (düzenleme takibi)
CREATE TABLE audit_response_history (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    response_id UUID NOT NULL REFERENCES audit_responses(id) ON DELETE CASCADE,
    previous_response_type VARCHAR(50),
    previous_description TEXT,
    previous_photos JSONB,
    changed_by UUID REFERENCES users(id),
    changed_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    change_reason TEXT
);
```

#### Reports

```
sql
-- Denetim Raporları
CREATE TABLE audit_reports (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    audit_id UUID NOT NULL REFERENCES audits(id) ON DELETE CASCADE,
    report_code VARCHAR(50) UNIQUE, -- RAP-2024-001
    total_score INTEGER NOT NULL,
    max_score INTEGER NOT NULL,
    percentage DECIMAL(5, 2) NOT NULL,
    grade VARCHAR(2), -- A, B, C, D, F
    section_scores JSONB NOT NULL DEFAULT '{}', 
    -- {section_id: {score, max_score, percentage}}
    category_scores JSONB NOT NULL DEFAULT '{}',
    -- {category_id: {score, max_score, percentage}}
    findings JSONB DEFAULT '[]', -- Bulgular listesi
    recommendations TEXT, -- Öneriler
    summary TEXT, -- Özet
    pdf_url TEXT,
    excel_url TEXT,
    generated_by UUID REFERENCES users(id),
    generated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    sent_at TIMESTAMP,
    metadata JSONB DEFAULT '{}'
);

CREATE INDEX idx_audit_reports_audit_id ON audit_reports(audit_id);
CREATE INDEX idx_audit_reports_report_code ON audit_reports(report_code);
CREATE INDEX idx_audit_reports_percentage ON audit_reports(percentage);
CREATE INDEX idx_audit_reports_grade ON audit_reports(grade);

-- Rapor alıcıları
CREATE TABLE audit_report_recipients (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    report_id UUID NOT NULL REFERENCES audit_reports(id) ON DELETE CASCADE,
    user_id UUID NOT NULL REFERENCES users(id),
    sent_at TIMESTAMP,
    viewed_at TIMESTAMP,
    downloaded_at TIMESTAMP,
    UNIQUE(report_id, user_id)
);

CREATE INDEX idx_report_recipients_report_id ON audit_report_recipients(report_id);
CREATE INDEX idx_report_recipients_user_id ON audit_report_recipients(user_id);
```

#### Corrective Actions

```
sql
-- Düzeltici Faaliyetler
CREATE TABLE corrective_actions (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    audit_response_id UUID NOT NULL REFERENCES audit_responses(id),
    action_code VARCHAR(50) UNIQUE, -- AKS-2024-001
    title VARCHAR(255) NOT NULL,
    description TEXT NOT NULL,
    priority VARCHAR(20) DEFAULT 'medium', -- low, medium, high, critical
    assigned_to UUID NOT NULL REFERENCES users(id),
    assigned_by UUID NOT NULL REFERENCES users(id),
    due_date DATE NOT NULL,
    status VARCHAR(50) DEFAULT 'pending',
    -- pending, in_progress, completed, approved, rejected, overdue
    estimated_cost DECIMAL(10, 2),
    actual_cost DECIMAL(10, 2),
    tags JSONB DEFAULT '[]',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    started_at TIMESTAMP,
    completed_at TIMESTAMP,
    approved_at TIMESTAMP,
    approved_by UUID REFERENCES users(id),
    rejected_at TIMESTAMP,
    rejection_reason TEXT
);

CREATE INDEX idx_corrective_actions_response_id ON corrective_actions(audit_response_id);
CREATE INDEX idx_corrective_actions_assigned_to ON corrective_actions(assigned_to);
CREATE INDEX idx_corrective_actions_assigned_by ON corrective_actions(assigned_by);
CREATE INDEX idx_corrective_actions_status ON corrective_actions(status);
CREATE INDEX idx_corrective_actions_due_date ON corrective_actions(due_date);
CREATE INDEX idx_corrective_actions_priority ON corrective_actions(priority);

-- Düzeltici Faaliyet Güncellemeleri
CREATE TABLE corrective_action_updates (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    action_id UUID NOT NULL REFERENCES corrective_actions(id) ON DELETE CASCADE,
    update_text TEXT NOT NULL,
    attachments JSONB DEFAULT '[]', -- Fotoğraf, belge
    progress_percentage INTEGER CHECK (progress_percentage BETWEEN 0 AND 100),
    updated_by UUID NOT NULL REFERENCES users(id),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_action_updates_action_id ON corrective_action_updates(action_id);
CREATE INDEX idx_action_updates_updated_by ON corrective_action_updates(updated_by);

-- Düzeltici Faaliyet Yorumları
CREATE TABLE corrective_action_comments (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    action_id UUID NOT NULL REFERENCES corrective_actions(id) ON DELETE CASCADE,
    user_id UUID NOT NULL REFERENCES users(id),
    comment TEXT NOT NULL,
    is_internal BOOLEAN DEFAULT false, -- Sadece yöneticiler görsün mü?
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    deleted_at TIMESTAMP
);

CREATE INDEX idx_action_comments_action_id ON corrective_action_comments(action_id);
```

#### Notifications

```
sql
-- Bildirimler
CREATE TABLE notifications (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
    type VARCHAR(50) NOT NULL,
    -- audit_scheduled, audit_reminder, audit_starting, report_ready, 
    -- action_assigned, action_due_soon, action_overdue, action_completed, 
    -- action_approved, action_rejected
    title VARCHAR(255) NOT NULL,
    message TEXT NOT NULL,
    related_entity_type VARCHAR(50), -- audit, report, corrective_action
    related_entity_id UUID,
    priority VARCHAR(20) DEFAULT 'normal', -- low, normal, high, urgent
    channels JSONB DEFAULT '["app"]', -- ["app", "email", "sms"]
    is_read BOOLEAN DEFAULT false,
    read_at TIMESTAMP,
    sent_at TIMESTAMP,
    email_sent BOOLEAN DEFAULT false,
    sms_sent BOOLEAN DEFAULT false,
    push_sent BOOLEAN DEFAULT false,
    metadata JSONB DEFAULT '{}',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    expires_at TIMESTAMP -- Bildirim süresi dolunca silinebilir
);

CREATE INDEX idx_notifications_user_id ON notifications(user_id);
CREATE INDEX idx_notifications_type ON notifications(type);
CREATE INDEX idx_notifications_is_read ON notifications(is_read);
CREATE INDEX idx_notifications_created_at ON notifications(created_at);
CREATE INDEX idx_notifications_related_entity ON notifications(related_entity_type, related_entity_id);

-- Bildirim tercihleri
CREATE TABLE notification_preferences (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
    notification_type VARCHAR(50) NOT NULL,
    enabled BOOLEAN DEFAULT true,
    channels JSONB DEFAULT '["app", "email"]', -- Hangi kanallardan alsın
    quiet_hours_start TIME, -- Sessiz saat başlangıcı (örn: 22:00)
    quiet_hours_end TIME, -- Sessiz saat bitişi (örn: 08:00)
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(user_id, notification_type)
);

CREATE INDEX idx_notification_prefs_user_id ON notification_preferences(user_id);
```

#### Audit Logs

```
sql
-- Sistem Audit Logları (güvenlik ve izlenebilirlik)
CREATE TABLE audit_logs (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id UUID REFERENCES users(id),
    action VARCHAR(100) NOT NULL, -- login, logout, create, update, delete, export
    entity_type VARCHAR(50), -- user, facility, audit, report
    entity_id UUID,
    ip_address INET,
    user_agent TEXT,
    changes JSONB, -- Yapılan değişiklikler (before/after)
    status VARCHAR(20), -- success, failure
    error_message TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_audit_logs_user_id ON audit_logs(user_id);
CREATE INDEX idx_audit_logs_action ON audit_logs(action);
CREATE INDEX idx_audit_logs_entity ON audit_logs(entity_type, entity_id);
CREATE INDEX idx_audit_logs_created_at ON audit_logs(created_at);

-- Partition by month for performance
-- ALTER TABLE audit_logs PARTITION BY RANGE (created_at);
```

#### Settings & Configuration

```
sql
-- Sistem ayarları
CREATE TABLE system_settings (
    id SERIAL PRIMARY KEY,
    key VARCHAR(100) UNIQUE NOT NULL,
    value JSONB NOT NULL,
    description TEXT,
    is_public BOOLEAN DEFAULT false, -- Frontend'e açık mı?
    updated_by UUID REFERENCES users(id),
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Varsayılan ayarlar
INSERT INTO system_settings (key, value, description, is_public) VALUES
('audit.questions_visible_before_minutes', '30', 'Denetim sorularının kaç dakika önce görüneceği', false),
('audit.reminder_days', '[7, 3, 1]', 'Denetim hatırlatma günleri', false),
('action.reminder_days', '[7, 3, 1, 0]', 'Aksiyon hatırlatma günleri', false),
('action.overdue_notification_frequency', '1', 'Gecikmiş aksiyon bildirimi sıklığı (gün)', false),
('report.grade_thresholds', '{"A": 90, "B": 80, "C": 70, "D": 60, "F": 0}', 'Rapor not eşikleri', false),
('file.max_upload_size_mb', '10', 'Maksimum dosya yükleme boyutu (MB)', false),
('file.allowed_image_types', '["jpg", "jpeg", "png", "webp"]', 'İzin verilen resim formatları', false),
('file.allowed_document_types', '["pdf", "doc", "docx"]', 'İzin verilen doküman formatları', false);
```

### Database Optimization

#### Indexes
- Tüm foreign key'lerde index
- Sık sorgulanan alanlarda composite index
- Full-text search için GIN index (soru metinleri)

#### Partitioning
- `audit_logs`: Aylık partition (performans)
- `notifications`: Aylık partition + otomatik temizleme

#### Views (Materialized)
```
sql
-- Tesis performans özeti (hızlı raporlama için)
CREATE MATERIALIZED VIEW facility_performance_summary AS
SELECT 
    f.id as facility_id,
    f.name as facility_name,
    f.group_id,
    COUNT(DISTINCT a.id) as total_audits,
    AVG(ar.percentage) as avg_score,
    COUNT(DISTINCT CASE WHEN ca.status = 'overdue' THEN ca.id END) as overdue_actions,
    MAX(a.scheduled_date) as last_audit_date
FROM facilities f
LEFT JOIN audits a ON f.id = a.facility_id AND a.status = 'approved'
LEFT JOIN audit_reports ar ON a.id = ar.audit_id
LEFT JOIN audit_responses resp ON a.id = resp.audit_id
LEFT JOIN corrective_actions ca ON resp.id = ca.audit_response_id
GROUP BY f.id, f.name, f.group_id;

CREATE UNIQUE INDEX ON facility_performance_summary (facility_id);

-- Günlük refresh (cron job ile)
-- REFRESH MATERIALIZED VIEW CONCURRENTLY facility_performance_summary;
```

---

## 👥 Rol Yetkilendirme Sistemi

### Rol Hiyerarşisi

```
Admin (Süper Yönetici)
    ↓
Grup Admin (Tesis Grubu Yöneticisi)
    ↓
    ├── Denetmen (Auditor)
    ├── Kontrolcü (Controller)
    └── Hastane Yöneticisi (Hospital Manager)
```

### 1. Admin (Süper Yönetici)

#### Yetkiler
- ✅ **Tesis Grupları**
  - Tüm grupları görüntüleme
  - Yeni grup oluşturma
  - Grup düzenleme/silme
  - Grup adminleri atama/kaldırma

- ✅ **Tesisler**
  - Tüm tesisleri görüntüleme
  - Herhangi bir gruba tesis ekleme
  - Tesis düzenleme/silme
  - Tesis aktif/pasif yapma

- ✅ **Kullanıcılar**
  - Tüm kullanıcıları görüntüleme
  - Kullanıcı oluşturma (tüm roller)
  - Rol atama/değiştirme
  - Kullanıcı aktif/pasif yapma
  - Şifre sıfırlama

- ✅ **Denetimler**
  - Tüm denetimleri görüntüleme
  - Denetim iptal etme
  - Denetim yeniden planlama

- ✅ **Raporlar**
  - Tüm raporlara erişim
  - Sistem geneli analiz
  - Karşılaştırmalı raporlar
  - Export (tüm formatlar)

- ✅ **Sistem**
  - Sistem ayarları
  - PostgreSQL admin panel
  - Audit log görüntüleme
  - Backup yönetimi
  - Kullanıcı aktivite raporları

#### Kısıtlamalar
- ❌ Denetim gerçekleştiremez (sadece görüntüler)

---

### 2. Grup Admin (Tesis Grubu Yöneticisi)

#### Yetkiler
- ✅ **Kendi Grubu**
  - Grup bilgilerini düzenleme
  - Grup logosu güncelleme
  - İletişim bilgileri yönetimi

- ✅ **Tesisler** ⭐ YENİ
  - **Kendi grubunda yeni tesis oluşturma**
  - **Kendi tesislerini düzenleme**
  - **Kendi tesislerini aktif/pasif yapma**
  - Tesis bilgilerini güncelleme
  - Tesis iletişim bilgileri
  - Tesis metadata yönetimi

- ✅ **Kullanıcı Yönetimi**
  - Kendi grubunda kullanıcı oluşturma
  - Roller atama:
    - Grup Admin (kendi rolü)
    - Denetmen
    - Kontrolcü
    - Hastane Yöneticisi
  - Kullanıcı-tesis atamaları
  - Kullanıcı aktif/pasif yapma

- ✅ **Soru Havuzu**
  - Soru havuzunu görüntüleme
  - Yeni soru ekleme (otomatik havuza kaydedilir)
  - Kendi eklediği soruları düzenleme
  - Soru etiketleme
  - Soru arama ve filtreleme

- ✅ **Denetim Şablonları**
  - Şablon oluşturma
  - Soru havuzundan soru seçme
  - Şablon düzenleme
  - Şablon kopyalama
  - Şablon versiyonlama
  - Şablon aktif/pasif yapma

- ✅ **Denetim Planlama**
  - Denetim oluşturma
  - Şablon seçimi
  - Hastane seçimi (kendi grubu)
  - Denetim ekibi oluşturma (1-3 kişi)
  - Hastane-ekip eşleştirme
  - Tarih ve saat belirleme
  - Denetim iptal etme
  - Denetim yeniden planlama

- ✅ **Raporlama**
  - Grup bazlı raporlar
  - Tesis karşılaştırmaları
  - Trend analizleri
  - Kategori/bölüm analizleri
  - Export (PDF, Excel, CSV)
  - Dashboard görünümü

- ✅ **Düzeltici Faaliyetler**
  - Tüm aksiyonları görüntüleme (grup içi)
  - Aksiyon durumlarını takip
  - Gecikmiş aksiyonları görüntüleme
  - Raporlar

#### Kısıtlamalar
- ❌ Diğer gruplara erişim yok
- ❌ Diğer grupların tesislerini göremez
- ❌ Sistem ayarlarına erişim yok
- ❌ Admin rolü atayamaz
- ❌ Denetim gerçekleştiremez (sadece planlar)

---

### 3. Denetmen (Auditor)

#### Yetkiler
- ✅ **Denetimler**
  - Atandığı denetimleri görüntüleme
  - Denetim detaylarını görme
  - Denetim tarih/saat bilgisi
  - Denetim ekibini görme

- ✅ **Denetim Gerçekleştirme**
  - Soruları cevaplama (denetim zamanı geldiğinde)
  - Fotoğraf yükleme
  - Belge yükleme (PDF)
  - Açıklama girme
  - Taslak kaydetme
  - Önceki denetim sonuçlarını görme
  - Denetimi tamamlama
  - Denetimi onaylama

- ✅ **Raporlar**
  - Kendi yaptığı denetimlerin raporlarını görme
  - Rapor detaylarını inceleme
  - Rapor export (PDF)

#### Kısıtlamalar
- ❌ Denetim planlayamaz
- ❌ Başkalarının denetimlerini göremez
- ❌ Atanmadığı hastaneleri göremez
- ❌ Kullanıcı yönetimi yapamaz
- ❌ Şablon oluşturamaz
- ❌ Düzeltici faaliyet atayamaz

---

### 4. Kontrolcü (Baş Hekim / Genel Müdür)

#### Yetkiler
- ✅ **Hastane Bilgileri**
  - Kendi hastanesinin bilgilerini görme
  - İletişim bilgilerini görme

- ✅ **Denetim Raporları**
  - Kendi hastanesinin tüm raporlarını görme
  - Rapor detaylarını inceleme
  - Bölüm/kategori analizleri
  - Trend analizleri
  - Karşılaştırmalı raporlar (zaman içinde)
  - Export (PDF, Excel, CSV)

- ✅ **Düzeltici Faaliyetler**
  - Eksiklikleri görüntüleme
  - Hastane yöneticilerine aksiyon atama
  - Termin tarihi belirleme
  - Öncelik belirleme (düşük, orta, yüksek, kritik)
  - Aksiyon durumlarını takip
  - Güncellemeleri görme
  - Aksiyonları onaylama
  - Aksiyonları reddetme (gerekçe ile)
  - Yorum yapma

- ✅ **Bildirimler**
  - Yeni rapor bildirimleri
  - Aksiyon tamamlanma bildirimleri
  - Gecikmiş aksiyon bildirimleri

#### Kısıtlamalar
- ❌ Denetim yapamaz
- ❌ Denetim planlayamaz
- ❌ Başka hastaneleri göremez
- ❌ Kullanıcı yönetimi yapamaz
- ❌ Şablon oluşturamaz
- ❌ Kendisi aksiyon gerçekleştiremez (sadece atar ve onaylar)

---

### 5. Hastane Yönetim Grubu (Teknik/İdari Müdür)

#### Yetkiler
- ✅ **Düzeltici Faaliyetler**
  - Kendisine atanan aksiyonları görme
  - Aksiyon detaylarını inceleme
  - İlgili denetim sorusunu görme
  - Önceki denetim sonucunu görme

- ✅ **Aksiyon Gerçekleştirme**
  - Aksiyonu "İşlemde" olarak işaretleme
  - Güncelleme girme
  - İlerleme yüzdesi girme
  - Fotoğraf yükleme (önce/sonra)
  - Belge yükleme
  - Maliyet bilgisi girme
  - Aksiyonu tamamlama
  - Kontrolcüye gönderme

- ✅ **İletişim**
  - Aksiyon hakkında yorum yapma
  - Kontrolcü ile mesajlaşma
  - Ek süre talep etme

- ✅ **Bildirimler**
  - Yeni aksiyon bildirimleri
  - Termin yaklaşma bildirimleri
  - Onay/red bildirimleri
  - Yorum bildirimleri

#### Kısıtlamalar
- ❌ Denetim yapamaz
- ❌ Rapor göremez (sadece kendi aksiyonları)
- ❌ Başkalarının aksiyonlarını göremez
- ❌ Aksiyon atayamaz
- ❌ Kullanıcı yönetimi yapamaz
- ❌ Hastane bilgilerini düzenleyemez

---

### Rol Geçiş Matrisi

| Özellik | Admin | Grup Admin | Denetmen | Kontrolcü | Hastane Yön. |
|---------|-------|------------|----------|-----------|--------------|
| Grup Oluşturma | ✅ | ❌ | ❌ | ❌ | ❌ |
| Tesis Oluşturma | ✅ | ✅ (kendi grubu) | ❌ | ❌ | ❌ |
| Kullanıcı Oluşturma | ✅ | ✅ (alt roller) | ❌ | ❌ | ❌ |
| Şablon Oluşturma | ✅ | ✅ | ❌ | ❌ | ❌ |
| Denetim Planlama | ✅ | ✅ | ❌ | ❌ | ❌ |
| Denetim Yapma | ❌ | ❌ | ✅ | ❌ | ❌ |
| Rapor Görme | ✅ (tümü) | ✅ (grup) | ✅ (kendi) | ✅ (hastane) | ❌ |
| Aksiyon Atama | ✅ | ✅ | ❌ | ✅ | ❌ |
| Aksiyon Yapma | ❌ | ❌ | ❌ | ❌ | ✅ |
| Aksiyon Onaylama | ✅ | ✅ | ❌ | ✅ | ❌ |
| Sistem Ayarları | ✅ | ❌ | ❌ | ❌ | ❌ |

---

## 🔄 Denetim İş Akışı

### Faz 1: Denetim Şablonu Oluşturma

#### Adımlar
1. **Grup Admin Girişi**
   - Dashboard'a yönlendirilir
   - "Denetim Şablonları" menüsüne tıklar

2. **Yeni Şablon Oluşturma**
   - "Yeni Şablon" butonuna tıklar
   - Şablon adı girer (örn: "Mesai Dışı Denetim v5.1")
   - Açıklama ekler (opsiyonel)
   - Versiyon numarası belirler

3. **Soru Seçimi**
   - **Seçenek A: Havuzdan Seçim**
     - 18 bölüm listelenir
     - Her bölüm genişletilebilir
     - Bölüm içindeki sorular görünür
     - Checkbox ile seçim yapılır
     - Toplu seçim (tüm bölüm)
     - Kategori bazlı filtreleme
     - Arama (soru metni)
   
   - **Seçenek B: Yeni Soru Ekleme**
     - "Yeni Soru Ekle" butonuna tıklar
     - Bölüm seçer (dropdown)
     - Kategori seçer (dropdown)
     - Soru metnini girer
     - Ağırlık belirler (1-5)
     - Açıklama ekler (opsiyonel)
     - Referans ekler (opsiyonel)
     - Etiket ekler (opsiyonel)
     - **Kaydet** → Soru havuza eklenir ve şablona dahil edilir

4. **Soru Düzenleme**
   - Sıralama (drag & drop)
   - Özel ağırlık belirleme (şablona özel)
   - Zorunlu/opsiyonel işaretleme
   - Soru kaldırma

5. **Şablon Önizleme**
   - Bölüm bazlı görünüm
   - Toplam soru sayısı
   - Toplam ağırlık
   - Kategori dağılımı (grafik)

6. **Kaydetme**
   - "Taslak Olarak Kaydet" veya "Kaydet ve Aktif Et"
   - Başarı mesajı
   - Şablon listesine yönlendirilir

#### Öneriler

**1. Şablon Kopyalama**
- Mevcut şablondan başla
- Hızlı düzenleme
- Versiyon artırma

**2. Şablon Karşılaştırma**
- İki şablonu yan yana görüntüleme
- Fark analizi
- Eklenen/çıkarılan sorular

**3. Şablon İstatistikleri**
- Kaç denetimde kullanıldı
- Ortalama tamamlanma süresi
- Ortalama puan
- En çok sorun çıkan sorular

**4. Şablon Paylaşımı**
- Diğer grup adminlere şablon önerisi
- Şablon marketplace (gelecek)

**5. Akıllı Şablon Önerileri**
- AI destekli soru önerisi
- Benzer tesislerin şablonları
- Sektör standartları

---

### Faz 2: Denetim Planlama

#### Adımlar

1. **Yeni Denetim Oluşturma**
   - "Denetimler" menüsü → "Yeni Denetim"
   - Şablon seçimi (dropdown)
   - Şablon önizleme (modal)

2. **Hastane Seçimi**
   - Kendi grubundaki hastaneler listelenir
   - Çoklu seçim (checkbox)
   - Arama ve filtreleme
   - Hastane bilgileri (hover tooltip)

3. **Denetim Ekibi Oluşturma**
   - Denetmen listesi (kendi grubundaki)
   - Kullanıcı arama
   - Kullanıcı bilgileri (ad, email, telefon)
   - Geçmiş denetim sayısı
   - Ortalama denetim süresi
   - Müsaitlik durumu (takvim entegrasyonu)

4. **Hastane-Ekip Eşleştirme**
   
   **Senaryo: 3 Hastane, 6 Denetmen**
   
```
   Hastane A: [Denetmen 1, Denetmen 2] (2 kişi)
   Hastane B: [Denetmen 3] (1 kişi)
   Hastane C: [Denetmen 4, Denetmen 5, Denetmen 6] (3 kişi)
```
   
   **Kurallar:**
   - Minimum 1, maksimum 3 kişi/hastane
   - Aynı tarihte bir denetmen sadece 1 hastaneye atanabilir
   - Eşleştirme yapıldıktan sonra o denetmenler diğer hastaneler için seçilemez
   
   **UI Önerisi:**
   - Drag & drop arayüzü
   - Hastane kartları (sol)
   - Denetmen kartları (sağ)
   - Denetmenleri hastane kartlarına sürükle
   - Çakışma kontrolü (kırmızı uyarı)
   - Otomatik eşleştirme önerisi (AI)

5. **Tarih ve Saat Planlama**
   - Takvim görünümü
   - Her hastane için ayrı tarih/saat
   - Çakışma kontrolü
   - Çalışma saatleri kontrolü
   - Tatil günleri kontrolü
   - Başlangıç ve bitiş saati
   - Tahmini süre hesaplama

6. **Bildirim Ayarları**
   - Bildirim kanalları (email, push, SMS)
   - Hatırlatma zamanları (varsayılan: 7 gün, 3 gün, 1 gün, 30 dk)
   - Özel mesaj ekleme

7
