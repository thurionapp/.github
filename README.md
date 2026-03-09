# 🚗 Thurion — Plataforma de Visibilidade Veicular

> **Saúde do Ativo • Evidência Fiscal • Visibilidade Inteligente**  
> In-Device First • Backend Soberano • Cache Inteligente • Multi-tenant

---

## 💡 Visão Geral

O Thurion redefine o veículo como uma **Entidade Viva**: um ativo que envelhece, adoece, responde ao uso e pode ser cuidado preventivamente. Traduzimos telemetria, uso e contexto em **Visibilidade Veicular Inteligente** através de processamento embarcado em Rust e modelos matemáticos de severidade.

### O que o Thurion NÃO é
* ❌ Um rastreador
* ❌ Um sistema de vigilância  
* ❌ Um software punitivo

### O que o Thurion É
* ✅ Um sistema de saúde do ativo
* ✅ Uma camada de evidência operacional
* ✅ Um motor de eficiência econômica
* ✅ Um prontuário veicular auditável

---

## 🏗️ Arquitetura Multi-Repository

O projeto Thurion é organizado em repositórios especializados para garantir clareza, manutenibilidade e desenvolvimento paralelo:

### 📱 [thurion-ios](./thurion-ios) — Aplicativo iOS
Implementação iOS completa com SwiftUI e The Composable Architecture (TCA).

**Stack Tecnológico:**
- **SwiftUI** - Interface declarativa moderna
- **TCA** - Arquitetura reativa para gerenciamento de estado
- **CoreML** - Inferência de ML on-device para classificação de eventos
- **ActivityKit** - Live Activities e Dynamic Island
- **CoreMotion/CoreLocation** - Sensores GPS e movimento

**Funcionalidades Principais:**
- Rastreamento automático de trajetos com ML híbrido
- Map matching de alta precisão (HMM/Viterbi)
- Classificação de eventos (buracos, lombadas, curvas)
- Live Activities com Dynamic Island
- Processamento offline completo

---

### 🤖 [thurion-android](./thurion-android) — Aplicativo Android  
Implementação Android que espelha a arquitetura iOS com configuração centralizada.

**Stack Tecnológico:**
- **Kotlin** - Linguagem principal moderna
- **Gradle** - Build system com tasks customizadas
- **JNI Bridge** - Integração com Rust core
- **EncryptedSharedPreferences** - Armazenamento seguro

**Paridade com iOS:**
- Sistema de configuração centralizado (`Project.kt` vs `Project.swift`)
- Build automatizado do Rust core
- Arquitetura de serviços similar
- Toggle local/remote para desenvolvimento

---

### ⚙️ [thurion-core](./thurion-core) — Motor de Computação Rust
Coração embarcado multiplataforma que processa todos os dados dos sensores.

**Capacidades:**
- **Detecção de Direção** - Pipeline ML híbrido (Rust + CoreML)
- **Processamento GPS** - Extended Kalman Filter, normalização
- **Map Matching** - HMM/Viterbi com R-tree e A*
- **Segmentação de Viagem** - Splits automáticos e métricas
- **Cálculo de Saúde** - Modelo matemático H(t) e Score Veicular
- **Persistência** - Armazenamento TLV binário eficiente

**Integração via UniFFI:**
- Bridge Swift ↔ Rust e Kotlin ↔ Rust
- Geração automática de bindings
- Callbacks para comunicação bidirecional
- Build multiplataforma com Makefile centralizado

---

### 📋 [thurion-project](./thurion-project) — Documentação & Arquitetura
Repositório central com documentação de negócio, produto e arquitetura.

**Conteúdo Principal:**
- **Visão de Produto** - Proposta de valor, personas, planos
- **Modelo de Negócio** - Precificação, unit economics, go-to-market  
- **Arquitetura** - ADRs, fluxos de dados, princípios
- **Documentação Técnica** - Integrações, compliance, operações

**Princípios Arquiteturais:**
- Backend é a autoridade única
- Mobile app é offline-first e in-device
- Thurion-Sync como broker de estado (futuro B2B)
- Tudo auditável (LGPD, fiscal, operacional)

---

## 🔄 Como os Repositórios Trabalham Juntos

### Fluxo de Dados Principal

```
Mobile Apps (iOS/Android)
    ↓ (sensores GPS/IMU)
thurion-core (Rust processing)
    ↓ (resultados processados)
Mobile Apps (UI/UX)
    ↓ (sincronização quando online)
Backend (validação/auditoria)
```

### Desenvolvimento Integrado

**Build System:**
- `thurion-core`: Makefile centralizado para builds iOS/Android
- `thurion-ios`: Xcode com script de build Rust integrado
- `thurion-android`: Gradle com tasks para compilação nativa

**Configuração:**
- Toggle local/remote para desenvolvimento do Rust core
- Scripts automatizados para build e integração
- Dependências gerenciadas via submodules e package managers

**Compartilhamento:**
- Tipos de domínio definidos no Rust core
- Contratos de API via UniFFI
- Documentação centralizada no `thurion-project`

---

## 🎯 Personas & Proposta de Valor

### B2C Free — Guardião Familiar
- **Perfil:** Proprietário individual
- **Plano:** Free (gratuito)
- **Valor:** Previsibilidade e tranquilidade

### B2C Pro — Operador Intensivo  
- **Perfil:** Motorista profissional / uso severo
- **Plano:** R$ 25,00/mês
- **Valor:** Proteção de margem e evidência fiscal

### B2B — Gestor de Frota
- **Perfil:** 5-200 veículos (logística, serviços, vendas)
- **Planos:** Essencial e Avançado (por veículo)
- **Valor:** Planejamento preditivo e governança sem vigilância

---

## 🚀 Roadmap de Implementação

### ✅ MVP (v1.0) - Concluído
- [x] Rastreamento automático com ML
- [x] Map matching HMM/Viterbi  
- [x] Classificação de eventos CoreML
- [x] Live Activities & Dynamic Island
- [x] Integração Swift-Rust via UniFFI
- [x] Background tracking (app terminated)

### 🚧 v1.1 - Em Desenvolvimento (Q1 2025)
- [ ] Health Score Dashboard UI
- [ ] UI refinements (animations, dark mode, accessibility)
- [ ] Export features (GeoJSON, share, PDF)

### 📅 v1.2 - Planejado (Q2 2025)  
- [ ] Sistema de Abastecimento com preços ANP
- [ ] Visualização de Desgaste com heatmap de condições

### 🔥 v2.0 - Modelo Estocástico (Q3-Q4 2025)
- [ ] Modelagem Térmica (IET, cache climático)
- [ ] Modelos Avançados de Degradação (Arrhenius, Weibull)
- [ ] Multi-vehicle Support

---

## 🛠️ Começando

### Pré-requisitos
- **iOS:** Xcode 15+, iOS 17+, Swift 5.9+, Rust 1.75+
- **Android:** Android Studio, Android SDK, Rust toolchain com targets Android
- **Core:** Rust 1.75+ com targets iOS/Android

### Setup do Ambiente

```bash
# Clonar repositórios
git clone https://github.com/thurionapp/thurion-ios.git
git clone https://github.com/thurionapp/thurion-android.git  
git clone https://github.com/thurionapp/thurion-core.git
git clone https://github.com/thurionapp/thurion-project.git

# Setup do Rust core (central)
cd thurion-core
make dev-setup  # Configura targets, cargo-ndk, etc.

# Build multiplataforma
make all        # iOS + Android libraries
```

### Build dos Aplicativos

**iOS:**
```bash
cd thurion-ios
git submodule update --init --recursive  # thurion-core
open thurion-ios.xcodeproj
# Build (⌘B) ou Run (⌘R)
```

**Android:**
```bash
cd thurion-android
./gradlew assembleDebug  # Build automático do Rust core
```

---

## 📊 Principais Tecnologias

### Mobile (iOS/Android)
- **SwiftUI/TCA** (iOS) - Arquitetura reativa moderna
- **Kotlin/Gradle** (Android) - Stack moderno com build customizado
- **CoreML** - Inferência ML on-device
- **ActivityKit** - Live Activities e Dynamic Island

### Core (Rust)
- **UniFFI** - Bridge Swift/Kotlin ↔ Rust
- **rusqlite** - SQLite para persistência
- **rstar** - R-tree spatial index (map matching)
- **petgraph** - Grafos para algoritmo A*
- **burn** - ML framework para detecção
- **lz4_flex** - Compressão de telemetria

### Backend & Infra
- **Firebase** - Auth, Analytics, Crashlytics
- **Supabase** - PostgreSQL como Single Source of Truth
- **RevenueCat** - Billing e assinaturas
- **CDN** - Tiles de mapa OSM comprimidos

---

## 📚 Documentação Completa

### Documentação de Produto
- [Visão Geral](thurion-project/docs/product/overview.md)
- [Modelo Matemático](thurion-project/docs/product/mathematical-core.md)
- [Filosofia do Produto](thurion-project/docs/product/product-philosophy.md)

### Documentação Técnica  
- [Arquitetura](thurion-project/README.md#arquitetura)
- [ADRs](thurion-project/docs/adr/) - Architecture Decision Records
- [Integrações](thurion-project/docs/RevenueCat/README.md)

### Guias de Desenvolvimento
- [iOS Build Guide](thurion-ios/README.md#build-do-projeto)
- [Android Build Guide](thurion-android/README.md#build-commands)  
- [Rust Core Build](thurion-core/README.md#build-system-multiplataforma)

---

## 🤝 Contribuição

Contribuições são bem-vindas! Por favor:

1. Leia os [ADRs](thurion-project/docs/adr/) para entender decisões arquiteturais
2. Siga os padrões de código de cada repositório
3. Teste suas mudanças em todas as plataformas
4. Documente novas funcionalidades

---

## 📄 Licença

Este projeto está licenciado sob os termos da licença MIT. Veja o arquivo [LICENSE](thurion-project/LICENSE) para detalhes.

---

## 🔗 Links Úteis

- **Website:** [thurion.app](https://thurion.app)
- **Documentação:** [docs.thurion.app](https://docs.thurion.app)  
- **Status:** [status.thurion.app](https://status.thurion.app)
- **Blog:** [blog.thurion.app](https://blog.thurion.app)

---

**Status:** ✅ **Production Ready** - iOS e Android builds funcionando com Rust core embarcado.
