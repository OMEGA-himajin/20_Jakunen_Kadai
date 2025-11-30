# Project Structure

## Organization Philosophy

ソリューション/プロジェクト単位で機能を分割し、クリーンアーキテクチャ/DDDに沿ってプレゼンテーション(UI)・アプリケーションサービス・ドメイン・インフラを層分離。競技課題ごとにサブプロジェクトを追加するが、共通基盤（DBスクリプト、ユーティリティ）は再利用する。依存方向は内向き（UI -> Application -> Domain）。

## Directory Patterns

### ソリューション/アプリ本体
**Location**: `/`  
**Purpose**: Visual Studio ソリューションと .NET デスクトップ（WinForms）アプリのプロジェクトを配置。UI層は`Views`/`Controls`配下、プレゼンターやViewModelは別フォルダで管理し、アプリケーション層を参照する。  
**Example**: `AppName.App/Views/OrderListForm.cs`, `AppName.App/ViewModels/OrderListViewModel.cs`

### ドメイン・アプリケーション層
**Location**: `/AppName.Domain`, `/AppName.Application`  
**Purpose**: ビジネスルールとユースケースをUIから分離。ドメインモデル、サービス、DTO、ドメインインターフェース（リポジトリ契約）を配置。  
**Example**: `Order.cs`, `OrderService.cs`, `OrderDto.cs`, `IOrderRepository.cs`

### インフラ・データアクセス
**Location**: `/AppName.Infrastructure`, `/db`  
**Purpose**: SQL Server向けのリポジトリ実装、接続設定、マイグレーション/スクリプトを保持。ストアド/ビューは`/db/sql`にまとめ、環境毎の接続文字列はユーザーシークレット等に分離。  
**Example**: `OrderRepository.cs`, `db/sql/01_schema.sql`

## Naming Conventions

- **Files**: C#はPascalCase、SQLスクリプトは`nn_description.sql`形式を推奨。
- **Components**: クラスはPascalCase、インターフェースは`I`接頭辞。フォームは`*Form`。
- **Functions**: PascalCase。非公開ヘルパーでも意図を表す名前を付与。

## Import Organization

```csharp
using System;
using System.Collections.Generic;
using AppName.Domain;
using AppName.Application.Services;
```

- .NET標準 → 外部ライブラリ → 自プロジェクトの順でグルーピングし、`using`の順序と不要削除を維持。

**Path Aliases**:
- C#プロジェクト参照で名前空間をパスに合わせて管理し、`global using`は共通ユーティリティに限定。

## Code Organization Principles

- UIは入力検証・表示に専念し、ビジネスロジックはアプリケーション/ドメイン層に置く。
- DBアクセスはリポジトリ/DAO経由で行い、SQLはパラメータ化してインジェクションを回避。
- サービス・リポジトリはインターフェース越しに依存し、テストや差し替えを容易にする。
- 依存方向はUI/InfrastructureからDomainへの一方向とし、Domainから外部層を参照しない。

---
_Document patterns, not file trees. New files following patterns shouldn't require updates_
