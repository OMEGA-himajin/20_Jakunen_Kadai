# Technology Stack

## Architecture

Windows環境のクライアントアプリ + SQL Server データベース。クリーンアーキテクチャ/DDDを採用し、依存方向は `UI(Presentation) -> Application -> Domain` で内向き、Infrastructure は Domain に依存するが逆方向は禁止。競技課題に応じてローカルDBとWinFormsベースのデスクトップUIを組み合わせ、追加サービス連携は原則オフラインで代替。

## Core Technologies

- **Language**: C#（.NET デスクトップ開発）、T-SQL
- **Framework**: .NET 9 / WinForms（課題指定に追従）
- **Runtime**: .NET 9（Visual Studio 2022 17.12 同梱ランタイムを基準）

## Key Libraries

- 未確定。課題要件に合わせて最小限の公式ライブラリ（例: System.Data.SqlClient）を優先。

## Development Standards

### Type Safety
- C#のnullable有効を前提にし、警告を解消する。`dynamic`使用は例外的な場合に限定。

### Code Quality
- Visual Studioの組み込みアナライザー警告は原則ゼロを維持。
- フォーマッタは.editorconfig/IDE規定に従い、命名/アクセス修飾の警告を解消。

### Testing
- 単体テストは xUnit または MSTest を課題に合わせて用意。ビジネスロジックやDBアクセスは層分離してテスト可能にする。
- UIロジックは可能な限りプレゼンテーション層と分離し、テスト対象を限定。

## Development Environment

### Required Tools
- Visual Studio 2022 Community（.NET デスクトップ開発、SQL Server Data Tools）
- SQL Server 2022 Developer / SSMS 20.x
- Visual Studio Code（補助的な編集/確認用途）

### Common Commands
```bash
dotnet restore
dotnet build
dotnet test
```

## Key Technical Decisions

- AI-DLC/Kiroによるフェーズ管理を前提に、仕様合意後に実装着手。
- Windows/.NET + SQL Server のローカル開発を標準とし、外部SaaS依存は避ける。
- WinForms UIとDBの結合はDTO/リポジトリ層を介した疎結合を推奨。
- クリーンアーキテクチャ/DDDの依存方向を遵守し、UI・InfrastructureからDomainへの一方向依存を維持する。

---
_Document standards and patterns, not every dependency_
