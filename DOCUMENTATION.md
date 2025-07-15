# 📊 Sistema de Rastreabilidade - Trae

> Sistema modular para geração de relatórios de rastreabilidade que consolida dados de múltiplas fontes em um relatório unificado.

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://python.org)
[![Streamlit](https://img.shields.io/badge/Streamlit-1.28%2B-red.svg)](https://streamlit.io)
[![Docker](https://img.shields.io/badge/Docker-Ready-blue.svg)](https://docker.com)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

## 🎯 Visão Geral

O **Sistema de Rastreabilidade Trae** é uma aplicação web moderna desenvolvida em Python que consolida dados de três fontes principais:

- **Status da Ordem** (Excel) - Informações sobre ordens de produção
- **Rastreabilidade** (CSV/Excel) - Dados de localização e movimentação
- **Estoque** (Excel) - Quantidades e status de disponibilidade

Gera um relatório consolidado com informações unificadas, otimizado para grandes volumes de dados com processamento assíncrono e cache inteligente.

## ✨ Funcionalidades Principais

### 🚀 Carregamento de Dados
- ✅ Suporte para arquivos Excel (.xlsx) e CSV
- ✅ Carregamento assíncrono para melhor performance
- ✅ Validação automática de estrutura e integridade
- ✅ Processamento em chunks para arquivos grandes (>50MB)
- ✅ Cache inteligente com TTL configurável

### 🔍 Validação Robusta
- ✅ Verificação de colunas obrigatórias
- ✅ Validação de tipos de dados
- ✅ Detecção de dados nulos e duplicados
- ✅ Relatórios detalhados de qualidade
- ✅ Tratamento de erros com recuperação

### ⚡ Processamento Avançado
- ✅ Engine de alta performance com Polars
- ✅ Processamento paralelo e assíncrono
- ✅ Otimização de memória com chunking
- ✅ Estatísticas em tempo real
- ✅ Monitoramento de performance

### 🎨 Interface Moderna
- ✅ Interface web responsiva com Streamlit
- ✅ Upload drag & drop intuitivo
- ✅ Barras de progresso em tempo real
- ✅ Visualização interativa de dados
- ✅ Dashboard de métricas

### 🐳 Containerização Completa
- ✅ Docker Compose para desenvolvimento e produção
- ✅ Serviços de monitoramento (Prometheus + Grafana)
- ✅ Sistema de logs (ELK Stack)
- ✅ Cache distribuído (Redis)
- ✅ Proxy reverso (Nginx)

## 🏗️ Arquitetura do Sistema

### Estrutura de Diretórios

```
app/
├── core/                 # Componentes centrais
│   ├── exceptions.py    # Exceções customizadas
│   └── logger.py        # Sistema de logging
├── data/                # Camada de dados
│   ├── loader.py        # Carregamento de arquivos
│   ├── validator.py     # Validação de dados
│   ├── processor.py     # Processamento básico
│   ├── enhanced_processor.py # Processamento avançado
│   └── async_processor.py    # Processamento assíncrono
├── ui/                  # Interface do usuário
│   ├── main.py          # Aplicação principal Streamlit
│   └── components.py    # Componentes reutilizáveis
├── utils/               # Utilitários
│   ├── decorators.py    # Decoradores utilitários
│   ├── file_utils.py    # Utilitários de arquivo
│   └── helpers.py       # Funções auxiliares
└── cache/               # Sistema de cache
    └── manager.py       # Gerenciamento de cache
```

## 📦 Instalação e Configuração

### Pré-requisitos

#### Para Desenvolvimento Local
- Python 3.8+
- pip (gerenciador de pacotes Python)
- Git

#### Para Docker (Recomendado)
- Docker Engine 20.10+
- Docker Compose 2.0+
- Pelo menos 4GB de RAM disponível
- Portas livres: 8501, 3000, 9090, 9200, 5601, 6379

### Instalação Local

```bash
# 1. Clonar o repositório
git clone https://github.com/Rcffeitosa/sistema-rastreabilidade-trae.git
cd sistema-rastreabilidade-trae

# 2. Criar ambiente virtual
python -m venv venv

# 3. Ativar ambiente virtual
# Windows
venv\Scripts\activate
# Linux/Mac
source venv/bin/activate

# 4. Instalar dependências
pip install --upgrade pip
pip install -r requirements.txt

# 5. Executar aplicação
streamlit run streamlit_app.py
```

## 🚀 Guia de Uso

### Fluxo Básico de Trabalho

1. **Preparação dos Arquivos**
   - Status da Ordem (Excel): Deve conter colunas "Item", "Descrição do Item", "Quantidade Não Alocada"
   - Rastreabilidade (CSV/Excel): Deve conter "Endereço Origem", "Endereço Destino"
   - Estoque (Excel): Deve conter "Item", "Qtd Atual", "Status"

2. **Upload na Interface**
   - Acesse http://localhost:8501
   - Faça upload dos três arquivos nas seções correspondentes
   - Aguarde validação automática

3. **Processamento**
   - Clique em "Processar Dados"
   - Acompanhe progresso em tempo real
   - Visualize estatísticas de processamento

4. **Resultados**
   - Visualize dados processados na interface
   - Baixe relatório consolidado em Excel
   - Analise métricas e estatísticas

## 🐳 Docker e Containerização

### Arquitetura de Serviços

O sistema utiliza uma arquitetura de microserviços com Docker Compose:

```yaml
serviços:
  app:           # Aplicação Streamlit principal
  redis:         # Cache distribuído
  nginx:         # Proxy reverso (produção)
  prometheus:    # Coleta de métricas
  grafana:       # Dashboards e visualização
  elasticsearch: # Armazenamento de logs
  kibana:        # Interface de análise de logs
  filebeat:      # Coleta de logs
```

### URLs de Acesso dos Serviços

| Serviço | URL | Credenciais | Descrição |
|---------|-----|-------------|----------|
| **Aplicação** | http://localhost:8501 | - | Interface principal |
| **Grafana** | http://localhost:3000 | admin/admin123 | Dashboards e métricas |
| **Prometheus** | http://localhost:9090 | - | Coleta de métricas |
| **Kibana** | http://localhost:5601 | elastic/changeme | Análise de logs |
| **Elasticsearch** | http://localhost:9200 | elastic/changeme | API de logs |
| **Redis** | localhost:6379 | - | Cache (CLI) |

## 🧪 Testes e Qualidade

### Executar Testes

```bash
# Todos os testes
make test

# Testes específicos
make test-unit           # Testes unitários
make test-integration    # Testes de integração
make test-performance    # Testes de performance

# Cobertura de código
make coverage
```

## 📊 Monitoramento e Observabilidade

### Métricas Disponíveis

#### Métricas da Aplicação
- Tempo de processamento por arquivo
- Taxa de sucesso/erro
- Número de registros processados
- Uso de memória durante processamento
- Performance do cache (hit rate)

#### Métricas do Sistema
- CPU e memória dos containers
- Latência de rede
- Espaço em disco
- Status dos serviços

## 🔒 Segurança

### Práticas Implementadas

1. **Validação de Entrada**
   - Sanitização de dados de upload
   - Validação de tipos de arquivo
   - Verificação de tamanho máximo
   - Prevenção de path traversal

2. **Auditoria**
   - Log de todas as operações
   - Rastreamento de mudanças
   - Histórico de acessos
   - Relatórios de segurança

3. **Containerização**
   - Containers com usuários não-root
   - Redes isoladas
   - Volumes com permissões restritas
   - Secrets management

## 🚀 Performance e Otimização

### Otimizações Implementadas

1. **Processamento Assíncrono**
   - Carregamento paralelo de arquivos
   - Processamento não-bloqueante
   - Pool de workers configurável

2. **Cache Inteligente**
   - Cache de arquivos processados
   - TTL configurável
   - Invalidação automática
   - Compressão de dados

3. **Engine de Dados**
   - Polars para performance superior
   - Operações vetorizadas
   - Otimização de joins
   - Indexação inteligente

### Benchmarks

| Tamanho do Arquivo | Tempo de Processamento | Uso de Memória |
|-------------------|----------------------|----------------|
| 10MB | 2-5 segundos | 50-100MB |
| 50MB | 10-20 segundos | 200-400MB |
| 100MB | 20-40 segundos | 400-800MB |
| 500MB | 2-5 minutos | 1-2GB |

## 🤝 Contribuição

### Como Contribuir

1. **Fork o repositório**
2. **Crie uma branch para sua feature**
   ```bash
   git checkout -b feature/nova-funcionalidade
   ```
3. **Faça suas alterações**
4. **Execute os testes**
   ```bash
   make test
   make check
   ```
5. **Commit suas mudanças**
   ```bash
   git commit -m "feat: adiciona nova funcionalidade"
   ```
6. **Push para sua branch**
   ```bash
   git push origin feature/nova-funcionalidade
   ```
7. **Abra um Pull Request**

### Padrões de Desenvolvimento

- **Código**: Seguir PEP 8 e usar type hints
- **Commits**: Usar Conventional Commits
- **Testes**: Manter cobertura > 80%
- **Documentação**: Atualizar docs para novas features
- **Performance**: Considerar impacto na performance

## 📚 Recursos Adicionais

### Documentação

- [Guia de Contribuição](CONTRIBUTING.md)
- [Changelog](CHANGELOG.md)
- [README Principal](README.md)

### Links Úteis

- [Streamlit Documentation](https://docs.streamlit.io)
- [Polars Documentation](https://pola-rs.github.io/polars/)
- [Docker Documentation](https://docs.docker.com)
- [Grafana Documentation](https://grafana.com/docs/)

### Suporte

- **Issues**: Para reportar bugs ou solicitar features
- **Discussions**: Para perguntas e discussões gerais
- **Wiki**: Para documentação adicional

## 📄 Licença

Este projeto está licenciado sob a Licença MIT. Veja o arquivo [LICENSE](LICENSE) para detalhes.

## 🏆 Reconhecimentos

Agradecimentos especiais a:

- **Streamlit Team** - Framework incrível para aplicações web
- **Polars Team** - Engine de dados de alta performance
- **Docker Team** - Containerização simplificada
- **Grafana Team** - Visualização e monitoramento
- **Comunidade Python** - Ecossistema rico e colaborativo

---

**Desenvolvido com ❤️ para otimizar processos de rastreabilidade**

*Última atualização: Janeiro 2024*