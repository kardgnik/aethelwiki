# Aethel Wiki — Documentação Técnica do Repositório

## 1. Visão Geral da Arquitetura

Este repositório é configurado como um **Obsidian Knowledge Vault** estruturado para gestão de documentação de mundo (worldbuilding), cronologia e transcrições de sessões de RPG. O sistema utiliza grafos de conhecimento bidirecionais suportados por nós de conteúdo em Markdown e indexação relacional.

- **Plataforma:** Obsidian Vault
- **Padrão de Marcação:** GitHub Flavored Markdown (GFM) + Wikilinks (`[[...]]`)
- **Codificação de Arquivos:** UTF-8 (sem BOM)
- **Quebras de Linha:** CRLF / LF compatíveis
- **Topologia de Links:** Bidirecional com suporte a referências a seções (`[[Arquivo#Seção|Label]]`)

---

## 2. Topologia de Diretórios

```
aethelwiki/
├── .obsidian/                  # Configurações do workspace, temas, plugins e grafos do Obsidian
├── IMAGENS/                    # Repositório de mídias estáticas (PNG, JPG, WEBP) referenciadas nas notas
├── NOTAS PRINCIPAIS/           # Nós centrais do grafo (compêndios, cosmologia, facções, índices temporais)
├── NOTAS SOLTAS/               # Nós granulares (personagens, raças, classes, locais, anos, deuses)
├── PJ/                         # Fichas canônicas de Personagens Jogáveis com históricos e atributos
├── SESSOES/
│   └── CRONICAS/               # Transcrições das sessões de jogo com registros temporais estruturados
├── Aethel.md                   # Índice raiz navegacional da wiki
└── README.md                   # Documentação técnica de arquitetura e padrões (este arquivo)
```

### 2.1. Escopo de Cada Diretório

| Diretório | Responsabilidade Técnica | Convenção de Arquivos |
| :--- | :--- | :--- |
| `NOTAS PRINCIPAIS/` | Documentos canônicos estruturais e tabelas-mestras do sistema. | PascalCase / Nomes compostos formais. |
| `NOTAS SOLTAS/` | Nós atômicos do grafo; dados de suporte para entidades específicas. | Nomes diretos (`<Nome>.md`, `<Ano> A.G.md`). |
| `PJ/` | Fichas de personagens dos jogadores com históricos e traços. | `<Nome do Personagem>.md`. |
| `SESSOES/CRONICAS/` | Registros de sessões com transcrição temporal e sumário. | `Sessão XX - Crônicas de Aethel.md`. |
| `IMAGENS/` | Armazenamento de assets de imagem do vault. | Nomes em caixa alta ou padrão snake_case. |

---

## 3. Padrões de Nomenclatura e Sintaxe

### 3.1. Links Internos (Wikilinks)
- **Ligação Simples:** `[[Nome do Arquivo]]`
- **Ligação com Alias:** `[[Nome do Arquivo|Texto Alternativo]]`
- **Ligação com Âncora:** `[[Nome do Arquivo#Seção Específica|Texto]]`
- **Mídia Embutida:** `![[Nome_do_Arquivo.ext]]` (sem necessidade de caminho relativo, gerenciado pelo indexador do Obsidian).

### 3.2. Taxonomia de Tags
A categorização de nós deve utilizar tags semânticas no corpo do documento (prioritariamente nas primeiras linhas ou rodapé):

| Categoria | Tags Autorizadas |
| :--- | :--- |
| **Entidades & Personagens** | `#NPC`, `#personagem`, `#PJ`, `#deuses`, `#Primordial`, `#humano`, `#elfo` |
| **Facções & Grupos** | `#instituições`, `#vilões`, `#Conselho-das-Cinzas`, `#vanguarda` |
| **Cronologia & História** | `#cronologia`, `#lore`, `#história`, `#guerras-primordiais` |
| **Geografia & Espaço** | `#lugares`, `#cidades`, `#virtus`, `#solsis`, `#abutrak`, `#planos` |
| **Sistemas & Itens** | `#classes`, `#guerreiro`, `#magia`, `#alquimia`, `#artefatos` |

---

## 4. Sistema Temporal e Parâmetros Cronológicos

O sistema de datação do repositório é baseado em um marco zero estrito correspondente ao término das Guerras Primordiais.

### 4.1. Notação de Eras
- **A.G. (*Antes das Guerras*):** Contagem regressiva decrescente até o término do conflito (`X A.G.` → `0`).
- **Ano 0 / 0 D.G.:** Ponto de inflexão canônico; demarca o colapso do Conselho das Cinzas e início do calendário contemporâneo.
- **D.G. (*Depois das Guerras*):** Contagem progressiva a partir do Ano 0.
- **Ano Corrente Canônico:** `1.735 D.G.` (especificado em `Dias da Semana e Mês (ano atual 1735).md` e `Depois das Guerras.md`).

### 4.2. Regra de Interpolação de Nascimentos
O cálculo do ano de nascimento segue a fórmula:

$$\text{Ano de Nascimento} = 1735 - \text{Idade Declarada}$$

**Restrição Técnica:** É proibida a interpolação ou atribuição arbitrária de anos para entidades que não possuam idade numérica expressamente declarada nos registros canônicos.

---

## 5. Estrutura de Dados das Sessões (`SESSOES/CRONICAS/`)

Os arquivos de transcrição em `SESSOES/CRONICAS/` seguem uma arquitetura padronizada:

1. **Metadados:**
   - Link canônico do VOD/YouTube.
   - PJs participantes e NPCs em destaque.
   - Locais visitados e organizações envolvidas.
2. **Sumário Executivo:** Resumo analítico dos eventos principais da sessão.
3. **Registros Temporais Estruturados:** Transcrição sequencial com formatação `**[HH:MM:SS]** <texto_transcrito>`.

---

## 6. Métricas do Vault

Dados computados do estado do repositório:

| Métrica | Valor |
| :--- | :--- |
| **Total de Arquivos Markdown (.md)** | 201 |
| **Arquivos na Raiz** | 2 (`Aethel.md`, `README.md`) |
| **Arquivos em `NOTAS PRINCIPAIS/`** | 22 |
| **Arquivos em `NOTAS SOLTAS/`** | 159 |
| **Arquivos em `PJ/`** | 9 |
| **Arquivos em `SESSOES/CRONICAS/`** | 9 |
| **Assets de Mídia (`IMAGENS/`)** | 77 arquivos (PNG, JPG, JPEG) |
| **Volume Total de Dados** | ~273 MB |
| **Tags Únicas Mapeadas** | 28 |

---

## 7. Protocolos de Consistência e Integridade Referencial

1. **Prevenção de Links Órfãos:** Todo novo nó (`.md`) deve ser referenciado em ao menos um documento de índice (`NOTAS PRINCIPAIS/` ou `Aethel.md`).
2. **Imutabilidade Canônica:** Nomes próprios, títulos divinos e entidades com vínculos de linhagem devem respeitar estritamente a ortografia consolidada nos documentos mestres (`COMPENDIO_LORE_AETHEL.md`).
3. **Preservação de Formato:** Arquivos devem ser gravados em UTF-8 puro, sem caracteres nulos ou corrupção de codificação de acentuação gráfica.
