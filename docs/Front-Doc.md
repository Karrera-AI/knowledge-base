# FrontEnd - Doc

## 📋 Índice

1. [Visão Geral](#-visão-geral)
2. [Arquitetura](#-arquitetura)
3. [Funcionalidades Principais](#-funcionalidades-principais)
4. [Sistemas Especializados](#-sistemas-especializados)
5. [Componentes por Módulo](#-componentes-por-módulo)
6. [Hooks Personalizados](#-hooks-personalizados)
7. [Internacionalização (i18n)](#-internacionalização-i18n)
8. [Sistema de Cache](#-sistema-de-cache)
9. [Segurança e Criptografia](#-segurança-e-criptografia)
10. [Guia de Desenvolvimento](#-guia-de-desenvolvimento)
11. [Testes](#-testes)
12. [Solução de Problemas](#-solução-de-problemas)

---

## 🎯 Visão Geral

Karrera AI é uma plataforma abrangente de desenvolvimento de carreira que combina princípios de neurociência com insights alimentados por IA para ajudar usuários a construir sua jornada profissional.

### Tecnologias Principais

- **React + TypeScript** - Framework principal
- **React Query** - Gerenciamento de estado do servidor
- **React Router** - Navegação
- **Tailwind CSS** - Estilização
- **i18next** - Internacionalização
- **Web Crypto API** - Criptografia client-side

### Pré-requisitos

- Node.js 18+
- npm ou yarn

### Instalação e Execução

```bash
# Instalação
npm install

# Desenvolvimento
npm run dev

# Build de Produção
npm run build
```

---

## 🏗️ Arquitetura

A aplicação segue uma arquitetura modular baseada em componentes com clara separação de responsabilidades:

```
client/
├── src/
│   ├── components/          # Componentes UI
│   │   ├── auth/           # Autenticação
│   │   ├── memory/         # Sistema de memória
│   │   ├── paths/          # Trilhas de carreira
│   │   ├── chat/           # Sistema de chat
│   │   ├── profile/        # Perfil do usuário
│   │   ├── dashboard/      # Dashboard
│   │   ├── projects/       # Projetos
│   │   └── ui/             # Componentes reutilizáveis
│   ├── hooks/              # Hooks personalizados
│   ├── lib/                # Bibliotecas e utilitários
│   │   ├── Interfaces/     # Definições TypeScript
│   │   ├── services/       # Serviços de API
│   │   ├── Utils/          # Funções utilitárias
│   │   └── repositories/   # Camada de repositório
│   ├── pages/              # Componentes de página
│   ├── locales/            # Traduções (pt/en)
│   ├── data/               # Dados estáticos
│   └── i18n/               # Configuração i18n
```

### Princípios Arquiteturais

1. **Separação de Responsabilidades**: Lógica de negócio separada da apresentação
2. **Modularidade**: Componentes independentes e reutilizáveis
3. **Type Safety**: Cobertura completa de tipos TypeScript
4. **Performance**: Otimizações de renderização e caching inteligente
5. **Escalabilidade**: Estrutura preparada para crescimento

---

## 🚀 Funcionalidades Principais

### 1. Sistema de Memória

Sistema de classificação de memória baseado em neurociência, implementando o framework de Kahneman.

#### Tipos de Memória

- **Semântica** - Conhecimentos gerais, fatos e conceitos
- **Episódica** - Experiências pessoais com contexto
- **Procedural** - Habilidades e padrões comportamentais
- **Emocional** - Memórias com carga emocional

#### Estados de Memória

- **Working Memory** - Memórias temporárias aguardando classificação
- **Long-term Memory** - Base de conhecimento permanente
- **Discarded Memory** - Memórias movidas para lixeira

#### Framework de Kahneman

- **Experiencing Self** - Captura momento a momento
- **Remembering Self** - Construção de narrativa usando análise peak-end

#### Componentes Principais

```tsx
import { 
  MemoryClassificationEngine,    // Motor de classificação com IA
  NarrativeBuilder,               // Construtor de narrativas
  ExperiencingSelfTracker,        // Rastreador de experiências
  LegacyFilesVisualization,       // Gestão de arquivos de memória
  WorkingMemoryView,              // Visualização de memória de trabalho
  LongTermMemoryView,             // Visualização de memória de longo prazo
  DiscardedMemoryView             // Visualização de memórias descartadas
} from '@/components/memory';
```

#### Uso Básico

```tsx
import { MemorySection } from '@/components/memory';

function Dashboard() {
  return <MemorySection />;
}
```

### 2. Trilhas de Carreira (Paths)

Sistema completo de exploração e gestão de trilhas de carreira.

#### Funcionalidades

- **Descoberta de Trilhas**: Navegue por trilhas disponíveis
- **Integração WorkDNA**: Combinação baseada em personalidade
- **Acompanhamento de Progresso**: Monitore o aprendizado
- **Recursos Comunitários**: Conecte-se com outros aprendizes

#### Componentes Principais

```tsx
import { 
  PathCard,                  // Card individual de trilha
  PathDetail,                // Detalhes da trilha
  PathsList,                 // Lista de trilhas
  PathsFilters,              // Filtros e busca
  PathsHeader,               // Cabeçalho com controles
  PathsStats,                // Estatísticas
  WorkDNARadar,              // Visualização de personalidade
  PathWorkDNACharacterSheet, // Ficha de personagem
  PathWorkDNAPeriodicTable   // Tabela periódica
} from '@/components/paths';
```

#### Uso com Hook

```tsx
import { usePaths } from '@/hooks/use-paths';

function PathsPage() {
  const { 
    paths, 
    filteredPaths, 
    filters, 
    updateFilter,
    handleViewDetails 
  } = usePaths();
  
  return (
    <div>
      <PathsHeader />
      <PathsFilters filters={filters} onFilterChange={updateFilter} />
      <PathsList paths={filteredPaths} onViewDetails={handleViewDetails} />
    </div>
  );
}
```

### 3. Sistema de Chat

Interface conversacional alimentada por IA.

#### Funcionalidades

- **Conversas Baseadas em Templates**: Iniciadores de conversa pré-definidos
- **Mensagens em Tempo Real**: Respostas instantâneas da IA
- **Tratamento Robusto de Erros**: Gestão com retry
- **Histórico de Conversas**: Sessões de chat persistentes

#### Componentes Principais

```tsx
import { 
  ChatInterface,    // Interface principal de chat
  ChatSidebar,      // Lista de conversas
  ChatMessages,     // Exibição de mensagens
  ChatInput,        // Input com sugestões
  TemplateDialog,   // Seleção de templates
  ChatSkeleton,     // Estado de carregamento
  ErrorMessage      // Mensagens de erro
} from '@/components/chat';
```

#### Uso com Hook

```tsx
import { useChat } from '@/hooks/use-chat';

function ChatPage() {
  const chat = useChat();
  
  return (
    <div className="flex">
      <ChatSidebar {...chat.sidebarProps} />
      <ChatInterface {...chat.interfaceProps} />
    </div>
  );
}
```

#### Tratamento de Erros

- **Design Consistente**: Mensagens de erro mantêm o mesmo estilo
- **Sem Detalhes Técnicos**: Usuários não veem erros internos da API
- **Funcionalidade de Retry**: Botão "Tentar Novamente"
- **Histórico Limpo**: Mensagens de erro não são salvas

### 4. Perfil do Usuário

Gestão abrangente do perfil do usuário.

#### Funcionalidades

- **Análise WorkDNA**: Avaliação de personalidade e habilidades
- **Sugestões de Carreira**: Recomendações alimentadas por IA
- **Gestão de Personas**: Múltiplas personas profissionais
- **Visualização de Progresso**: Acompanhamento de desenvolvimento

#### Componentes Principais

```tsx
import { 
  ProfileHeader,           // Visão geral do perfil
  WorkDNAVisualization,    // Visualização de personalidade
  CareerPathSuggestions,   // Recomendações de IA
  PersonaManagement        // Criação e edição de personas
} from '@/components/profile';
```

#### Uso com Hook

```tsx
import { useProfile } from '@/hooks/use-profile';

function ProfilePage() {
  const { user, workDNA, isLoading } = useProfile();
  
  if (isLoading) return <LoadingState />;
  
  return (
    <div>
      <ProfileHeader user={user} />
      <WorkDNAVisualization workDNA={workDNA} />
    </div>
  );
}
```

---

## 🔧 Sistemas Especializados

### Sistema de Fila de Validação de Memória

Sistema completo de processamento em background para validação de memórias, permitindo que usuários continuem usando a aplicação sem esperar uploads completarem.

#### Características Principais

- ✅ **Processamento Não Bloqueante**: Usuário pode navegar imediatamente
- 🔄 **Retry Automático**: 3 tentativas automáticas com delay crescente (2s, 4s, 6s)
- ⚠️ **Tratamento Robusto de Erros**: Captura, exibe e permite retry manual
- 💾 **Persistência**: Fila salva em localStorage, sobrevive a reloads
- 📊 **Monitoramento Visual**: Interface em tempo real para acompanhamento
- 🎯 **Zero Bloqueio**: Usuário pode continuar trabalhando imediatamente

#### Arquitetura

```
┌─────────────────────────────────────────────────────────────┐
│                 USUÁRIO CLICA "CONFIRMAR"                   │
└──────────────────────┬──────────────────────────────────────┘
                       │
                       ▼
         ┌─────────────────────────────┐
         │   addToQueue()              │
         │   [Não Bloqueante!]         │
         │   - Retorna ID              │
         │   - Salva localStorage      │
         │   - Notifica listeners      │
         └──────────┬──────────────────┘
                    │
        ┌───────────┴───────────┐
        │                       │
        ▼                       ▼
┌──────────────┐       ┌──────────────────┐
│   UI LIVRE   │       │   BACKGROUND     │
│              │       │   PROCESSING     │
│ - Toast OK   │       │                  │
│ - Navegação  │       │  processQueue()  │
│ - Monitor ON │       │   ├─ Item 1      │
└──────────────┘       │   ├─ Item 2      │
                       │   └─ Item 3      │
                       └──────────────────┘
```

#### Componentes

**1. Serviço Principal**
```typescript
// client/src/lib/services/memory-validation-queue.service.ts
import { MemoryValidationQueueService } from '@/lib/services/memory-validation-queue.service';

const queueService = MemoryValidationQueueService.getInstance();

// Métodos principais:
queueService.addToQueue(memoryId, approvedItems, rejectedItems, memoryName);
queueService.getStats();
queueService.retryFailedItem(itemId);
queueService.clearCompleted();
```

**2. Hook React**
```typescript
// client/src/hooks/use-validation-queue.ts
import { useValidationQueue } from '@/hooks/use-validation-queue';

function MyComponent() {
  const {
    stats,           // Estatísticas da fila
    items,           // Todos os itens
    activeItems,     // Itens ativos
    failedItems,     // Itens falhados
    isProcessing,    // Se está processando
    addToQueue,      // Adicionar à fila
    retryFailedItem, // Tentar novamente
    clearCompleted   // Limpar concluídos
  } = useValidationQueue();
}
```

**3. Monitor Visual**
```tsx
// client/src/components/memory/validation-queue-monitor.tsx
import { ValidationQueueMonitor } from '@/components/memory/validation-queue-monitor';

function WorkingMemoryView() {
  return (
    <>
      <ValidationQueueMonitor />
      {/* Resto do componente */}
    </>
  );
}
```

#### Uso Prático

```tsx
import { useValidationQueue } from '@/hooks/use-validation-queue';
import { ValidationQueueMonitor } from '@/components/memory/validation-queue-monitor';

function WorkingMemoryView() {
  const { addToQueue } = useValidationQueue();

  const handleSubmit = async () => {
    // Adiciona à fila (não espera!)
    const queueItemId = addToQueue(
      memoryId,
      approvedItems,
      rejectedItems,
      memoryName
    );

    // Notifica usuário
    toast({
      title: 'Validação adicionada à fila',
      description: 'Você pode continuar navegando.'
    });

    // Navega IMEDIATAMENTE
    navigate('/next-page');
  };

  return (
    <>
      <ValidationQueueMonitor />
      {/* Rest of component */}
    </>
  );
}
```

#### Estados dos Itens

- `pending` → Aguardando processamento
- `processing` → Em processamento
- `retrying` → Tentando novamente
- `completed` → Concluído com sucesso
- `failed` → Falhou após 3 tentativas

#### Configuração

```typescript
// Parâmetros ajustáveis no serviço
private readonly MAX_RETRIES = 3;           // Tentativas máximas
private readonly RETRY_DELAY = 2000;        // Delay base: 2s
private readonly PROCESSING_DELAY = 500;    // Entre itens: 0.5s
```

#### Persistência e Recuperação

- **Salvamento**: Automático após cada mudança
- **Carregamento**: Automático na inicialização
- **Recuperação**: Continua processamento após reload
- **Comportamento pós-Reload**:
  1. ✅ Itens `pending` → Continuam na fila
  2. 🔄 Itens `processing` → Reset para `pending`
  3. ✅ Itens `completed` → Permanecem para visualização
  4. ❌ Itens `failed` → Mantidos com erros
  5. 🔄 Itens `retrying` → Reset para `pending`

#### Monitoramento e Debug

```javascript
// No Console do DevTools
const queue = MemoryValidationQueueService.getInstance();

// Ver estatísticas
queue.getStats();

// Ver itens ativos
queue.getActiveItems();

// Ver itens falhados
queue.getFailedItems();

// Limpar localStorage
localStorage.removeItem('memory-validation-queue');
```

#### Documentação Adicional

- [README-VALIDATION-QUEUE.md](https://github.com/Karrera-AI/KarreraReplit/blob/main/client/src/lib/services/README-VALIDATION-QUEUE.md) - Documentação completa da arquitetura
- [MANUAL-TESTING-GUIDE.md](https://github.com/Karrera-AI/KarreraReplit/blob/main/client/src/lib/services/MANUAL-TESTING-GUIDE.md) - Guia passo a passo de testes manuais
- [IMPLEMENTATION-VALIDATION-QUEUE.md](https://github.com/Karrera-AI/KarreraReplit/blob/main/client/src/components/memory/IMPLEMENTATION-VALIDATION-QUEUE.md) - Resumo da implementação

---

## 📦 Componentes por Módulo

### Módulo de Autenticação

```tsx
// client/src/components/auth/
import {
  RegistrationWizard,     // Wizard de registro
  LoginForm,              // Formulário de login
  AuthGuard               // Proteção de rotas
} from '@/components/auth';
```

### Módulo de Dashboard

```tsx
// client/src/components/dashboard/
import {
  TopNav,                 // Navegação superior
  Sidebar,                // Barra lateral
  NewDiscussionView,      // Nova discussão
  TopicDetailView         // Detalhes do tópico
} from '@/components/dashboard';
```

### Módulo de Projetos

```tsx
// client/src/components/projects/
import {
  ProjectCard,            // Card de projeto
  ProjectForm,            // Formulário de projeto
  ProjectList             // Lista de projetos
} from '@/components/projects';
```

### Componentes UI Reutilizáveis

```tsx
// client/src/components/ui/
import {
  Button,                 // Botão
  Card,                   // Card
  Dialog,                 // Diálogo
  Input,                  // Input
  Select,                 // Select
  Tabs,                   // Tabs
  Toast,                  // Toast
  Badge,                  // Badge
  Avatar,                 // Avatar
  Skeleton,               // Skeleton loading
  // ... e 40+ componentes mais
} from '@/components/ui';
```

---

## 🎣 Hooks Personalizados

### Hook de Autenticação

```tsx
import { useAuth } from '@/hooks/use-auth';

function MyComponent() {
  const {
    user,              // Dados do usuário
    isAuthenticated,   // Status de autenticação
    isLoading,         // Estado de carregamento
    login,             // Função de login
    logout,            // Função de logout
    refreshUser        // Atualizar dados do usuário
  } = useAuth();
}
```

### Hook de Perfil

```tsx
import { useProfile } from '@/hooks/use-profile';

function ProfileComponent() {
  const {
    user,              // Dados do usuário
    workDNA,           // Dados WorkDNA
    isLoading,         // Estado de carregamento
    error,             // Erro se houver
    updateProfile,     // Atualizar perfil
    refreshProfile     // Recarregar perfil
  } = useProfile();
}
```

### Hook de WorkDNA

```tsx
import { useWorkDNA } from '@/hooks/use-workdna';

function WorkDNAComponent() {
  const {
    workDNA,           // Dados WorkDNA
    isLoading,         // Estado de carregamento
    updateWorkDNA,     // Atualizar WorkDNA
    getMatchScore      // Calcular score de match
  } = useWorkDNA();
}
```

### Hook de Chat

```tsx
import { useChat } from '@/hooks/use-chat';

function ChatComponent() {
  const {
    chatState,         // Estado do chat
    conversations,     // Lista de conversas
    templates,         // Templates disponíveis
    sendMessage,       // Enviar mensagem
    createConversation,// Criar conversa
    retryLastMessage   // Tentar última mensagem novamente
  } = useChat();
}
```

### Hook de Paths

```tsx
import { usePaths } from '@/hooks/use-paths';

function PathsComponent() {
  const {
    paths,             // Todas as trilhas
    filteredPaths,     // Trilhas filtradas
    currentPath,       // Trilha atual
    filters,           // Filtros ativos
    updateFilter,      // Atualizar filtro
    clearFilters,      // Limpar filtros
    handleViewDetails  // Ver detalhes
  } = usePaths();
}
```

### Hook de Memória

```tsx
import { useMemoryTabs } from '@/hooks/use-memory-tabs';

function MemoryComponent() {
  const {
    activeTab,         // Tab ativa
    setActiveTab,      // Mudar tab
    memories,          // Memórias
    isLoading          // Estado de carregamento
  } = useMemoryTabs();
}
```

### Hook de Fila de Validação

```tsx
import { useValidationQueue } from '@/hooks/use-validation-queue';

function ValidationComponent() {
  const {
    stats,             // Estatísticas da fila
    items,             // Todos os itens
    activeItems,       // Itens ativos
    failedItems,       // Itens falhados
    addToQueue,        // Adicionar à fila
    retryFailedItem,   // Tentar novamente
    clearCompleted     // Limpar concluídos
  } = useValidationQueue();
}
```

### Hook de Toast

```tsx
import { useToast } from '@/hooks/use-toast';

function MyComponent() {
  const { toast } = useToast();
  
  const showSuccess = () => {
    toast({
      title: 'Sucesso!',
      description: 'Operação concluída.',
      variant: 'success'
    });
  };
}
```

### Hook de Mobile

```tsx
import { useMobile } from '@/hooks/use-mobile';

function ResponsiveComponent() {
  const isMobile = useMobile();
  
  return isMobile ? <MobileView /> : <DesktopView />;
}
```

### Hook de Sugestões de Carreira

```tsx
import { useCareerSuggestions } from '@/hooks/use-career-suggestions';

function CareerComponent() {
  const {
    suggestions,       // Sugestões de carreira
    isLoading,         // Estado de carregamento
    refreshSuggestions // Atualizar sugestões
  } = useCareerSuggestions();
}
```

---

## 🌍 Internacionalização (i18n)

Sistema completo de multi-idiomas usando react-i18next.

### Idiomas Suportados

- **Português (pt)** - Português Brasileiro
- **English (en)** - Idioma padrão quando não suportado

### Prioridade de Detecção

1. **Seleção Manual** - localStorage/sessionStorage (quando usuário escolhe)
2. **Navegador** - Detecção automática do idioma do navegador
3. **Fallback** - Inglês quando idioma não é suportado

### Estrutura de Arquivos

```
src/
├── i18n/
│   └── index.ts              # Configuração principal do i18next
├── locales/
│   ├── pt/                   # Traduções em português
│   │   ├── common.json       # Textos comuns
│   │   ├── dashboard.json    # Dashboard
│   │   ├── memory.json       # Memória
│   │   ├── profile.json      # Perfil
│   │   └── projects.json     # Projetos
│   └── en/                   # Traduções em inglês
│       ├── common.json
│       ├── dashboard.json
│       ├── memory.json
│       ├── profile.json
│       └── projects.json
└── hooks/
    └── use-i18n.ts           # Hooks personalizados
```

### Uso Básico

```tsx
import { useI18n } from '@/hooks/use-i18n';

function MyComponent() {
  const { t, changeLanguage, language } = useI18n();
  
  return (
    <div>
      <h1>{t('common.title')}</h1>
      <p>Idioma atual: {language}</p>
      <button onClick={() => changeLanguage('en')}>English</button>
      <button onClick={() => changeLanguage('pt')}>Português</button>
    </div>
  );
}
```

### Hooks Específicos por Namespace

```tsx
import { 
  useCommonI18n,
  useDashboardI18n,
  useMemoryI18n,
  useProfileI18n,
  useProjectsI18n
} from '@/hooks/use-i18n';

function MyComponent() {
  const { t: tCommon } = useCommonI18n();
  const { t: tDashboard } = useDashboardI18n();
  
  return (
    <div>
      <button>{tCommon('save')}</button>
      <h1>{tDashboard('title')}</h1>
    </div>
  );
}
```

### Interpolação de Variáveis

```json
// No arquivo de tradução
{
  "welcome": "Bem-vindo, {{name}}!",
  "itemCount": "Você tem {{count}} item",
  "itemCount_plural": "Você tem {{count}} itens"
}
```

```tsx
// No componente
function Welcome({ userName, itemCount }) {
  const { t } = useCommonI18n();
  
  return (
    <div>
      <h1>{t('welcome', { name: userName })}</h1>
      <p>{t('itemCount', { count: itemCount })}</p>
    </div>
  );
}
```

### Seletor de Idioma

```tsx
import LanguageSelector from '@/components/ui/language-selector';

function Header() {
  return (
    <header>
      {/* Seletor dropdown */}
      <LanguageSelector variant="select" showLabel />
      
      {/* Botões */}
      <LanguageSelector variant="button" size="sm" />
    </header>
  );
}
```

### Namespaces Disponíveis

#### common
Textos usados em toda a aplicação:
- `navigation.*` - Menus e navegação
- `common.*` - Ações comuns (salvar, cancelar, etc.)
- `forms.*` - Formulários
- `messages.*` - Mensagens de feedback

#### dashboard
Textos específicos do dashboard:
- `sections.*` - Seções do dashboard
- `stats.*` - Estatísticas

#### memory
Sistema de memória:
- `types.*` - Tipos de memória
- `tabs.*` - Tabs de navegação
- `classification.*` - Motor de classificação
- `narrative.*` - Construtor de narrativa

#### profile
Perfil do usuário:
- `workdna.*` - WorkDNA
- `skills.*` - Habilidades
- `persona.*` - Gestão de personas

#### projects
Gestão de projetos:
- `status.*` - Status dos projetos
- `form.*` - Formulários
- `actions.*` - Ações disponíveis

### Configuração

```typescript
// src/i18n/index.ts
i18n.init({
  resources,
  fallbackLng: 'pt',      // Idioma padrão
  defaultNS: 'common',    // Namespace padrão
  ns: ['common', 'dashboard', 'memory', 'profile', 'projects'],
  
  detection: {
    order: ['localStorage', 'navigator', 'htmlTag'],
    caches: ['localStorage'],
  },
});
```

### Comportamento de Prioridade de Idioma

**⚠️ Importante**: Uma vez que o usuário selecione manualmente um idioma, essa escolha terá **sempre** prioridade sobre a detecção automática do navegador.

```javascript
// Cenário 1: Primeira visita - navegador em português
// Resultado: Interface em português

// Cenário 2: Usuário seleciona manualmente inglês  
// Resultado: Interface muda para inglês E salva preferência

// Cenário 3: Próxima visita do mesmo usuário
// Resultado: Interface em inglês (ignora navegador em português)

// Cenário 4: Navegador em francês (não suportado)
// Resultado: Interface em inglês (fallback)
```

### Melhores Práticas

1. **Use namespaces específicos** quando possível
2. **Organize chaves hierarquicamente** nos arquivos JSON
3. **Mantenha consistência** entre idiomas
4. **Use interpolação** para conteúdo dinâmico
5. **Teste em ambos os idiomas** antes de deployar
6. **Evite traduzir** nomes próprios e marcas
7. **Use fallbacks** para textos que podem não existir

---

## 💾 Sistema de Cache

### Cache do Hook useAuth

O hook `useAuth` foi implementado com um sistema inteligente de cache para evitar requisições repetidas à API, melhorando significativamente a performance da aplicação.

#### Como Funciona

**1. Cache de Dados**
- **Duração**: 5 minutos (configurável via `CACHE_DURATION`)
- **Armazenamento**: LocalStorage usando a classe `StorageData`
- **Chave**: `user_cache`

**2. Estrutura do Cache**
```typescript
interface CachedData {
  user: User;           // Dados do usuário da API
  profile: UserData;    // Dados do perfil Solid
  timestamp: number;    // Timestamp de criação
  expiresAt: number;    // Timestamp de expiração
}
```

**3. Fluxo de Operação**

**Primeira Execução:**
1. Verifica se há dados em cache
2. Se não houver, faz as requisições necessárias
3. Salva dados no cache após sucesso
4. Define estado da aplicação

**Execuções Subsequentes:**
1. Verifica se o cache é válido
2. Se válido, usa dados em cache (sem requisições)
3. Se expirado, remove cache e busca novos dados

**4. Funções de Cache**

```typescript
// Carregar do cache
loadFromCache()         // Carrega dados do cache
                       // Verifica validade temporal
                       // Remove cache expirado automaticamente

// Salvar no cache
saveToCache(user, profile)  // Salva dados no cache
                           // Define timestamps de criação e expiração
                           // Trata erros graciosamente

// Limpar cache
clearCache()            // Remove dados do cache
                       // Usado em logout e erros

// Verificar validade
isCacheValid(timestamp, expiresAt)  // Verifica se cache ainda é válido
                                   // Considera expiração e duração máxima
```

**5. Pontos de Integração**

```tsx
// initializeAuth() - Tenta carregar do cache primeiro
// refreshUser() - Atualiza cache após refresh bem-sucedido
// logout() - Limpa cache no logout
// forceRefresh() - Força atualização ignorando cache
```

#### Benefícios

1. **Performance**: Reduz requisições desnecessárias
2. **UX**: Carregamento mais rápido na navegação
3. **Eficiência**: Menor uso de recursos da API
4. **Confiabilidade**: Fallback para requisições quando necessário

#### Configuração

Para alterar a duração do cache, modifique a constante:

```typescript
const CACHE_DURATION = 10 * 60 * 1000; // 10 minutos
```

#### Debug

O sistema inclui logs para facilitar debug:
- `'Dados salvos no cache com sucesso'`
- `'Dados carregados do cache'`
- `'Cache expirado, removido'`
- `'Cache limpo com sucesso'`

#### Considerações

- Cache é automaticamente limpo em caso de erros
- Dados sempre atualizados após operações de refresh
- Sistema resiliente a falhas de armazenamento
- Cache invalidado no logout por segurança

---

## 🔐 Segurança e Criptografia

### Sistema de Criptografia para localStorage

Sistema que implementa criptografia automática para dados sensíveis armazenados em localStorage, garantindo que informações como webId, email, nome e outros dados de autenticação sejam protegidos.

#### Arquivos Principais

**1. `crypto.ts`**
- **CryptoUtils**: Classe singleton que gerencia criptografia
- **Algoritmo**: AES-GCM com chave de 256 bits
- **Chave**: Gerada automaticamente e armazenada em localStorage
- **IV**: Vetor de inicialização aleatório para cada operação

**2. `Storage.ts` (modificado)**
- **StorageData**: Classe que agora usa criptografia automaticamente
- **Compatibilidade**: Suporta dados não criptografados existentes
- **Transparente**: Código existente não precisa ser modificado

#### Como Funciona

**1. Criptografia Automática**

```typescript
// Ao salvar dados
await StorageData.write('webId', 'https://user.com/profile#me');
// Dados são automaticamente criptografados antes de serem salvos

// Ao ler dados
const webId = await StorageData.read<string>('webId');
// Dados são automaticamente descriptografados ao serem lidos
```

**2. Detecção de Dados Criptografados**

O sistema detecta automaticamente se os dados estão criptografados:
- Se criptografados: descriptografa automaticamente
- Se não criptografados: usa dados como estão (compatibilidade)

**3. Gestão de Chaves**

- Chave de criptografia é gerada automaticamente na primeira execução
- Chave é armazenada em localStorage com o nome `karrera-crypto-key`
- Chave é automaticamente limpa durante logout

#### Segurança

**Pontos Fortes:**
- **AES-GCM**: Algoritmo de criptografia simétrica robusto
- **IV Aleatório**: Cada operação usa um vetor de inicialização único
- **Chave Única**: Cada instalação do app tem sua própria chave
- **Limpeza Automática**: Chave é removida durante logout

**Limitações:**
- **Client-side**: Criptografia acontece no lado do cliente
- **Chave Local**: Chave é armazenada no mesmo dispositivo
- **JavaScript**: Vulnerável a ataques de engenharia reversa

#### Compatibilidade

**Dados Existentes:**

O sistema é totalmente compatível com dados não criptografados existentes:
1. Dados antigos são lidos normalmente
2. Quando reescritos, são automaticamente criptografados
3. Não é necessária migração manual

**Navegadores:**
- **Suporte**: Todos os navegadores modernos com Web Crypto API
- **Fallback**: Se criptografia não estiver disponível, usa dados não criptografados
- **Detecção**: `cryptoUtils.isAvailable()` verifica disponibilidade

#### Uso

**Para Desenvolvedores:**

```typescript
import { StorageData } from '@/lib/Data/Storage';

// Salvar dados (criptografia automática)
await StorageData.write('sensitiveData', { key: 'value' });

// Ler dados (descriptografia automática)
const data = await StorageData.read<{key: string}>('sensitiveData');
```

#### Dados Criptografados

**Chaves que SÃO Criptografadas:**
- `webId`: Identificador do usuário
- `email`: Email do usuário
- `name`: Nome do usuário
- `avatar`: URL do avatar
- `userId`: ID interno do usuário
- `isFirstLogin`: Flag de primeiro login
- `user_cache`: Cache de dados do usuário

**Chaves que NÃO SÃO Criptografadas:**
- `session-id`: ID de sessão (usado para autenticação)
- `callbackUrl`: URL de callback (temporário)

#### Logout e Limpeza

Durante o logout, o sistema:
1. Remove todos os dados de autenticação
2. Limpa chave de criptografia
3. Remove dados de sessionStorage
4. Limpa caches do navegador

#### Monitoramento

**Logs:**

O sistema gera logs detalhados para debug:
- `[Crypto]`: Operações de criptografia
- `[Storage]`: Operações de armazenamento
- `[Auth]`: Operações de autenticação

#### Solução de Problemas

**Problemas Comuns:**

**1. Criptografia não disponível**
- Verifique se o navegador suporta Web Crypto API
- Use `cryptoUtils.isAvailable()` para verificar

**2. Dados corrompidos**
- Sistema remove automaticamente dados corrompidos
- Verifique logs para detalhes de erro

**3. Falha na descriptografia**
- Pode indicar chave corrompida
- Faça logout para gerar nova chave

#### Debug

```typescript
// Verificar se criptografia está funcionando
const isAvailable = cryptoUtils.isAvailable();
console.log('Criptografia disponível:', isAvailable);

// Verificar se dados estão criptografados
const rawData = localStorage.getItem('webId');
const isEncrypted = cryptoUtils.isEncrypted(rawData);
console.log('Dados criptografados:', isEncrypted);
```

#### Implementação Técnica

**Fluxo de Criptografia:**
1. **Inicialização**: Gera ou recupera chave de criptografia
2. **Salvamento**: Serializa dados → Criptografa → Salva no localStorage
3. **Leitura**: Lê do localStorage → Descriptografa → Desserializa
4. **Limpeza**: Remove chave e dados durante logout

**Algoritmo de Criptografia:**
- **AES-GCM**: Criptografia autenticada
- **Chave**: 256 bits gerada com `crypto.subtle.generateKey()`
- **IV**: 12 bytes aleatórios para cada operação
- **Formato**: Base64 para armazenamento no localStorage

**Tratamento de Erros:**
- **Fallback gracioso**: Se criptografia falhar, usa dados não criptografados
- **Compatibilidade**: Suporta dados não criptografados existentes
- **Logs detalhados**: Para debug e monitoramento

---

## 🛠️ Guia de Desenvolvimento

### Padrões de Desenvolvimento

#### Organização de Componentes

- **Single Responsibility**: Cada componente tem um propósito claro
- **Composition over Inheritance**: Composição flexível de componentes
- **Props Interface**: Contratos claros de componentes
- **Default Props**: Defaults sensatos para props opcionais

#### Gestão de Estado

- **Custom Hooks**: Lógica de estado encapsulada
- **Service Layer**: Operações de API separadas dos componentes
- **Optimistic Updates**: Feedback imediato na UI
- **Error Boundaries**: Tratamento gracioso de erros

#### Qualidade de Código

- **TypeScript**: Cobertura completa de tipos
- **ESLint**: Aplicação de qualidade de código
- **Prettier**: Formatação consistente de código
- **Documentação de Componentes**: Exemplos claros de uso

### Estrutura de um Componente

```tsx
// 1. Imports
import React from 'react';
import { useMyHook } from '@/hooks/use-my-hook';
import { MyService } from '@/lib/services/my-service';

// 2. Types/Interfaces
interface MyComponentProps {
  title: string;
  onAction?: () => void;
}

// 3. Component
export function MyComponent({ title, onAction }: MyComponentProps) {
  // 3.1. Hooks
  const { data, isLoading } = useMyHook();
  
  // 3.2. State
  const [isOpen, setIsOpen] = React.useState(false);
  
  // 3.3. Effects
  React.useEffect(() => {
    // Effect logic
  }, []);
  
  // 3.4. Handlers
  const handleClick = () => {
    onAction?.();
  };
  
  // 3.5. Early returns
  if (isLoading) return <LoadingState />;
  
  // 3.6. Render
  return (
    <div>
      <h1>{title}</h1>
      <button onClick={handleClick}>Action</button>
    </div>
  );
}
```

### Estrutura de um Hook

```tsx
// 1. Imports
import { useState, useEffect } from 'react';
import { MyService } from '@/lib/services/my-service';

// 2. Types
interface UseMyHookReturn {
  data: any;
  isLoading: boolean;
  error: Error | null;
  refetch: () => void;
}

// 3. Hook
export function useMyHook(): UseMyHookReturn {
  // 3.1. State
  const [data, setData] = useState<any>(null);
  const [isLoading, setIsLoading] = useState(true);
  const [error, setError] = useState<Error | null>(null);
  
  // 3.2. Functions
  const fetchData = async () => {
    try {
      setIsLoading(true);
      const result = await MyService.getData();
      setData(result);
    } catch (err) {
      setError(err as Error);
    } finally {
      setIsLoading(false);
    }
  };
  
  // 3.3. Effects
  useEffect(() => {
    fetchData();
  }, []);
  
  // 3.4. Return
  return {
    data,
    isLoading,
    error,
    refetch: fetchData
  };
}
```

### Estrutura de um Service

```tsx
// 1. Imports
import { api } from '@/lib/api';
import type { MyData } from '@/lib/Interfaces/my-data.interface';

// 2. Service Class
export class MyService {
  // 2.1. Private properties
  private static readonly BASE_URL = '/api/my-resource';
  
  // 2.2. Public methods
  static async getData(): Promise<MyData[]> {
    const response = await api.get<MyData[]>(this.BASE_URL);
    return response.data;
  }
  
  static async getById(id: string): Promise<MyData> {
    const response = await api.get<MyData>(`${this.BASE_URL}/${id}`);
    return response.data;
  }
  
  static async create(data: Partial<MyData>): Promise<MyData> {
    const response = await api.post<MyData>(this.BASE_URL, data);
    return response.data;
  }
  
  static async update(id: string, data: Partial<MyData>): Promise<MyData> {
    const response = await api.put<MyData>(`${this.BASE_URL}/${id}`, data);
    return response.data;
  }
  
  static async delete(id: string): Promise<void> {
    await api.delete(`${this.BASE_URL}/${id}`);
  }
}
```

### Adicionando Novas Funcionalidades

#### 1. Criar Interface

```typescript
// src/lib/Interfaces/my-feature.interface.ts
export interface MyFeature {
  id: string;
  name: string;
  description: string;
  createdAt: Date;
}
```

#### 2. Criar Service

```typescript
// src/lib/services/my-feature.service.ts
export class MyFeatureService {
  // Implementar métodos
}
```

#### 3. Criar Hook

```typescript
// src/hooks/use-my-feature.ts
export function useMyFeature() {
  // Implementar lógica
}
```

#### 4. Criar Componentes

```tsx
// src/components/my-feature/my-feature-card.tsx
export function MyFeatureCard() {
  // Implementar componente
}
```

#### 5. Adicionar Traduções

```json
// src/locales/pt/my-feature.json
{
  "title": "Minha Funcionalidade",
  "description": "Descrição da funcionalidade"
}
```

```json
// src/locales/en/my-feature.json
{
  "title": "My Feature",
  "description": "Feature description"
}
```

#### 6. Adicionar Rotas (se necessário)

```tsx
// src/App.tsx
<Route path="/my-feature" element={<MyFeaturePage />} />
```

### Melhores Práticas

#### Performance

1. **Memoização**: Use `React.memo()` para componentes pesados
2. **useMemo**: Cache cálculos caros
3. **useCallback**: Evite recriação de funções
4. **Lazy Loading**: Carregue componentes sob demanda
5. **Code Splitting**: Divida o bundle em chunks menores

```tsx
// Exemplo de otimização
import React, { memo, useMemo, useCallback } from 'react';

const MyComponent = memo(({ data, onAction }) => {
  // Cache cálculo caro
  const processedData = useMemo(() => {
    return data.map(item => heavyProcessing(item));
  }, [data]);
  
  // Cache função de callback
  const handleClick = useCallback(() => {
    onAction(processedData);
  }, [onAction, processedData]);
  
  return <div onClick={handleClick}>{/* render */}</div>;
});
```

#### Tipagem TypeScript

1. **Evite `any`**: Use tipos específicos sempre que possível
2. **Interfaces sobre Types**: Prefira interfaces para objetos
3. **Genéricos**: Use para componentes e funções reutilizáveis
4. **Type Guards**: Implemente guards para validação de tipos

```typescript
// Bom exemplo
interface User {
  id: string;
  name: string;
  email: string;
}

function isUser(obj: any): obj is User {
  return typeof obj.id === 'string' 
    && typeof obj.name === 'string'
    && typeof obj.email === 'string';
}

// Componente genérico
interface ListProps<T> {
  items: T[];
  renderItem: (item: T) => React.ReactNode;
}

function List<T>({ items, renderItem }: ListProps<T>) {
  return <>{items.map(renderItem)}</>;
}
```

#### Tratamento de Erros

1. **Error Boundaries**: Capture erros de renderização
2. **Try/Catch**: Use em operações assíncronas
3. **Mensagens Amigáveis**: Não exponha erros técnicos ao usuário
4. **Logging**: Registre erros para debugging

```tsx
// Error Boundary
class ErrorBoundary extends React.Component {
  state = { hasError: false };
  
  static getDerivedStateFromError(error) {
    return { hasError: true };
  }
  
  componentDidCatch(error, errorInfo) {
    console.error('Error caught:', error, errorInfo);
  }
  
  render() {
    if (this.state.hasError) {
      return <ErrorFallback />;
    }
    return this.props.children;
  }
}

// Tratamento em hook
const fetchData = async () => {
  try {
    const data = await api.getData();
    setData(data);
  } catch (error) {
    console.error('Failed to fetch data:', error);
    toast({
      title: 'Erro',
      description: 'Não foi possível carregar os dados.',
      variant: 'destructive'
    });
  }
};
```

#### Acessibilidade

1. **ARIA Labels**: Use labels descritivos
2. **Keyboard Navigation**: Suporte navegação por teclado
3. **Focus Management**: Gerencie foco adequadamente
4. **Semantic HTML**: Use tags semânticas

```tsx
// Bom exemplo
<button
  aria-label="Fechar modal"
  onClick={handleClose}
  onKeyDown={(e) => e.key === 'Escape' && handleClose()}
>
  <X aria-hidden="true" />
</button>
```

---

## 🧪 Testes

### Estrutura de Testes

```
src/
├── components/
│   └── __tests__/
│       └── my-component.test.tsx
├── hooks/
│   └── __tests__/
│       └── use-my-hook.test.ts
└── lib/
    └── services/
        └── __tests__/
            └── my-service.test.ts
```

### Executar Testes

```bash
# Todos os testes
npm test

# Modo watch
npm test:watch

# Com cobertura
npm test:coverage

# Teste específico
npm test my-component.test.tsx
```

### Exemplo de Teste de Componente

```tsx
import { render, screen, fireEvent } from '@testing-library/react';
import { MyComponent } from './my-component';

describe('MyComponent', () => {
  it('should render title', () => {
    render(<MyComponent title="Test Title" />);
    expect(screen.getByText('Test Title')).toBeInTheDocument();
  });
  
  it('should call onAction when button clicked', () => {
    const onAction = jest.fn();
    render(<MyComponent title="Test" onAction={onAction} />);
    
    fireEvent.click(screen.getByRole('button'));
    expect(onAction).toHaveBeenCalled();
  });
});
```

### Exemplo de Teste de Hook

```tsx
import { renderHook, waitFor } from '@testing-library/react';
import { useMyHook } from './use-my-hook';

describe('useMyHook', () => {
  it('should fetch data', async () => {
    const { result } = renderHook(() => useMyHook());
    
    expect(result.current.isLoading).toBe(true);
    
    await waitFor(() => {
      expect(result.current.isLoading).toBe(false);
    });
    
    expect(result.current.data).toBeDefined();
  });
});
```

### Exemplo de Teste de Service

```tsx
import { MyService } from './my-service';
import { api } from '@/lib/api';

jest.mock('@/lib/api');

describe('MyService', () => {
  it('should fetch data', async () => {
    const mockData = [{ id: '1', name: 'Test' }];
    (api.get as jest.Mock).mockResolvedValue({ data: mockData });
    
    const result = await MyService.getData();
    
    expect(result).toEqual(mockData);
    expect(api.get).toHaveBeenCalledWith('/api/my-resource');
  });
});
```

### Testes do Sistema de Fila de Validação

#### Testes Unitários

```bash
npm test memory-validation-queue.test.ts
```

**Cobertura:**
- ✅ Padrão Singleton
- ✅ Adicionar à fila
- ✅ Estatísticas
- ✅ Subscribe/Unsubscribe
- ✅ Itens ativos
- ✅ Limpar concluídos
- ✅ Persistência
- ✅ Recuperação após reload

#### Testes Manuais

Consulte: [MANUAL-TESTING-GUIDE.md](https://github.com/Karrera-AI/KarreraReplit/blob/main/client/src/lib/services/MANUAL-TESTING-GUIDE.md)

**16 cenários detalhados de teste incluindo:**
1. Adicionar à fila e processar com sucesso
2. Múltiplos itens na fila
3. Tratamento de erro com retry
4. Persistência (reload de página)
5. Recuperação de item em processamento
6. Interação com monitor
7. Retry manual de item falhado
8. Remover item
9. Limpar tudo
10. Teste de stress (10 itens)
11. Navegação durante processamento
12. Verificação localStorage
13. Logs completos
14. Auto-processamento ao carregar
15. Comportamento com localStorage cheio
16. Múltiplas abas abertas

---

## 🔍 Solução de Problemas

### Problemas Comuns

#### 1. Aplicação não inicia

**Problema:** Erros ao executar `npm run dev`

**Soluções:**
```bash
# Limpar node_modules e reinstalar
rm -rf node_modules package-lock.json
npm install

# Limpar cache do npm
npm cache clean --force

# Verificar versão do Node
node --version  # Deve ser 18+
```

#### 2. Traduções não aparecem

**Problema:** Textos não são traduzidos

**Soluções:**
1. Verifique se a chave existe no arquivo JSON
2. Confirme o namespace correto
3. Verifique se o arquivo foi importado em `i18n/index.ts`
4. Limpe o cache do navegador

```tsx
// Debug
const { t, language } = useI18n();
console.log('Current language:', language);
console.log('Translation:', t('common.title'));
```

#### 3. Idioma não muda

**Problema:** Idioma não altera ao clicar no seletor

**Soluções:**
1. Verifique se localStorage está funcionando
2. Confirme se o componente está re-renderizando
3. Verifique erros no console

```tsx
// Debug
localStorage.getItem('i18nextLng');  // Ver idioma salvo
```

#### 4. Cache não funciona

**Problema:** Dados não são carregados do cache

**Soluções:**
1. Verifique se localStorage tem espaço
2. Confirme que `CACHE_DURATION` está configurado
3. Verifique logs no console

```tsx
// Debug
const cached = localStorage.getItem('user_cache');
console.log('Cached data:', cached);
```

#### 5. Criptografia não funciona

**Problema:** Dados não são criptografados

**Soluções:**
1. Verifique se navegador suporta Web Crypto API
2. Use `cryptoUtils.isAvailable()` para verificar
3. Verifique se está em HTTPS (necessário em produção)

```tsx
// Debug
import { cryptoUtils } from '@/lib/Utils/crypto';
console.log('Crypto available:', cryptoUtils.isAvailable());
```

#### 6. Fila de validação não processa

**Problema:** Itens ficam presos na fila

**Soluções:**
1. Verifique logs no console
2. Verifique localStorage: `memory-validation-queue`
3. Limpe a fila se necessário

```javascript
// Debug no Console
const queue = MemoryValidationQueueService.getInstance();
console.log('Queue stats:', queue.getStats());
console.log('Active items:', queue.getActiveItems());

// Limpar fila
localStorage.removeItem('memory-validation-queue');
```

#### 7. Erros de autenticação

**Problema:** Usuário não consegue fazer login

**Soluções:**
1. Verifique se backend está rodando
2. Confirme URLs de API nas variáveis de ambiente
3. Limpe cache e cookies
4. Verifique console para erros específicos

```bash
# Limpar tudo
localStorage.clear();
sessionStorage.clear();
# Recarregar página
```

#### 8. Componentes não carregam

**Problema:** Tela branca ou componentes não aparecem

**Soluções:**
1. Verifique Error Boundaries
2. Abra console para ver erros
3. Verifique imports de componentes
4. Confirme que rotas estão configuradas

```tsx
// Adicionar Error Boundary para debug
<ErrorBoundary>
  <MyComponent />
</ErrorBoundary>
```

### Debug Geral

#### Console Logs Úteis

```javascript
// Ver estado da autenticação
console.log('Auth state:', localStorage.getItem('webId'));

// Ver cache de usuário
console.log('User cache:', localStorage.getItem('user_cache'));

// Ver idioma atual
console.log('Language:', localStorage.getItem('i18nextLng'));

// Ver fila de validação
console.log('Queue:', localStorage.getItem('memory-validation-queue'));

// Ver todas as chaves em localStorage
Object.keys(localStorage).forEach(key => {
  console.log(key, localStorage.getItem(key));
});
```

#### DevTools Network

1. Abra DevTools → Network
2. Filtre por requisições específicas
3. Verifique status codes e payloads
4. Use throttling para simular conexão lenta

#### React DevTools

1. Instale extensão React DevTools
2. Inspecione componentes e props
3. Verifique hooks e state
4. Use Profiler para performance

---

## 📚 Recursos Adicionais

### Documentação por Módulo

Cada módulo principal tem sua própria documentação detalhada:

- [Sistema de Memória](https://github.com/Karrera-AI/KarreraReplit/blob/main/client/src/components/memory/README-memory.md)
- [Trilhas de Carreira](https://github.com/Karrera-AI/KarreraReplit/blob/main/client/src/components/paths/README-path.md)
- [Sistema de Chat](https://github.com/Karrera-AI/KarreraReplit/blob/main/client/src/components/chat/README.md)
- [Perfil do Usuário](https://github.com/Karrera-AI/KarreraReplit/blob/main/client/src/components/profile/README.md)
- [Sistema de Cache](https://github.com/Karrera-AI/KarreraReplit/blob/main/client/src/hooks/README-cache.md)
- [Internacionalização](https://github.com/Karrera-AI/KarreraReplit/blob/main/client/src/i18n/README-I18N.md)
- [Criptografia](https://github.com/Karrera-AI/KarreraReplit/blob/main/client/src/lib/Utils/README-crypto.md)
- [Fila de Validação](https://github.com/Karrera-AI/KarreraReplit/blob/main/client/src/lib/services/README-VALIDATION-QUEUE.md)
- [Guia de Testes Manuais](https://github.com/Karrera-AI/KarreraReplit/blob/main/client/src/lib/services/MANUAL-TESTING-GUIDE.md)
- [Implementação da Fila](https://github.com/Karrera-AI/KarreraReplit/blob/main/client/src/components/memory/IMPLEMENTATION-VALIDATION-QUEUE.md)

### Links Úteis

- [React Documentation](https://react.dev/)
- [TypeScript Documentation](https://www.typescriptlang.org/docs/)
- [React Query Documentation](https://tanstack.com/query/latest)
- [Tailwind CSS Documentation](https://tailwindcss.com/docs)
- [react-i18next Documentation](https://react.i18next.com/)

---

## 🤝 Contribuindo

### Como Contribuir

1. Siga os padrões de código estabelecidos
2. Mantenha type safety do TypeScript
3. Adicione documentação para novas funcionalidades
4. Escreva testes para novos componentes
5. Siga o estilo de código existente
6. Mantenhe traduções em ambos os idiomas

### Checklist de Pull Request

- [ ] Código segue padrões estabelecidos
- [ ] Tipos TypeScript estão corretos
- [ ] Testes foram adicionados/atualizados
- [ ] Documentação foi atualizada
- [ ] Traduções foram adicionadas (pt/en)
- [ ] Código foi testado localmente
- [ ] Sem erros de linting
- [ ] Performance foi considerada

---

## 📄 Licença

Este projeto é parte da plataforma Karrera AI.

---

## 📞 Suporte

Para problemas ou dúvidas:
- Verifique os logs do console
- Consulte a documentação específica do módulo
- Verifique localStorage e sessionStorage
- Teste com dados limpos: limpe cache e storage

---

**Última atualização:** Outubro 2025
**Versão da documentação:** 1.0.0
