# Technology Stack

## Architecture

Windows環境でのクライアントアプリ + SQL Server データベース。競技課題に応じてローカルDB・デスクトップUIを組み合わせる構成を基本とし、追加サービス連携は原則オフライン前提で代替。

## Core Technologies

- **Language**: C#（.NET デスクトップ開発想定）、T-SQL
- **Framework**: .NET（WinForms/WPFいずれか課題指定に追従）
- **Runtime**: .NET 6+（Visual Studio 2022標準を採用）

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
- デスクトップUIとDBの結合はDTO/リポジトリ層を介した疎結合を推奨。

---
_Document standards and patterns, not every dependency_
