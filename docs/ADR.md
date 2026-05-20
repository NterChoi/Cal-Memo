# 🏛 Architecture Decision Records (ADR)

## ADR-001: Selection of Prisma as Primary ORM

### 📅 Date: 2026-05-20
### 🚦 Status: Accepted

---

### 🇯🇵 概要 (Summary)
멀티 플랫폼 실시간 동기화의 핵심인 데이터 정합성을 보장하기 위해, 자동 타입 생성 기능을 갖춘 Prisma를 프로젝트의 주력 ORM으로 채택합니다.
マルチプラットフォームのリアルタイム同期の核心であるデータ整合性を保証するため、自動型生成機能を備えたPrismaをプロジェクトの主力ORMとして採用します。

---

### 🔍 Context (배경)
The 'Cal-Memo' project requires seamless real-time synchronization between Windows and iOS platforms. In such a multi-device environment, **Data Consistency** is the most critical factor. We evaluated several ORMs (TypeORM, Sequelize, Prisma) based on their ability to maintain a 'Single Source of Truth' and minimize human error during development.

### ✅ Decision (결정)
We have decided to use **Prisma ORM** instead of traditional ORMs like TypeORM.

### 💡 Rationale (선택 이유)

#### 1. Automated Type Safety (자동 타입 생성의 혁신)
Unlike traditional Nominal Typing in Java or TypeORM where developers must manually sync DB entities with application classes, Prisma follows a **'Schema-First'** approach.
- **Single Source of Truth**: By auto-generating TypeScript types directly from the `schema.prisma`, we eliminate the risk of desynchronization between the database and the source code.
- **Developer Experience**: It provides instant feedback (red lines) during coding if a developer attempts to handle data that violates the DB schema.

#### 2. Ensuring Data Consistency for Real-time Sync (데이터 정합성 보장)
Real-time synchronization across multiple platforms is highly sensitive to data format errors. 
- Prisma’s strict type enforcement acts as a first line of defense against data corruption.
- It ensures that the data being broadcasted via WebSockets to different devices is always valid and consistent.

#### 3. Market Relevance in Osaka Tech Scene (시장성)
Modern tech-driven companies in Osaka (e.g., LINE Yahoo Japan, startups) are increasingly adopting the NestJS + Prisma stack for its productivity and reliability. Mastering this stack demonstrates readiness for high-level professional environments.

---

### 📈 Consequences (결과 및 영향)
- **Positive**: Significant reduction in runtime errors related to database queries. Faster development cycle due to auto-completion and type-checking.
- **Neutral**: Requires a one-time setup of the Prisma CLI and understanding of the Prisma Schema Language (PSL).
- **Negative**: None identified for the current scope of the MVP.
