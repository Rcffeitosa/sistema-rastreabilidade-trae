# Sistema de Rastreabilidade de Dados

## 📋 Descrição

Sistema modular para geração de relatórios de rastreabilidade que consolida dados de múltiplas fontes (Status da Ordem, Rastreabilidade e Estoque) em um relatório unificado. Desenvolvido com arquitetura modular, seguindo as melhores práticas de desenvolvimento Python.

## 🚀 Funcionalidades

- **Carregamento de Dados**: Suporte para arquivos Excel (.xlsx) e CSV
- **Validação Robusta**: Validação de estrutura, tipos de dados e regras de negócio
- **Processamento Assíncrono**: Processamento eficiente de grandes volumes de dados
- **Cache Inteligente**: Sistema de cache com TTL para otimização de performance
- **Interface Web**: Interface Streamlit intuitiva e responsiva
- **Exportação Flexível**: Exportação para Excel e CSV com formatação
- **Monitoramento**: Logging estruturado e métricas de performance
- **Tratamento de Erros**: Tratamento robusto de exceções e recuperação

## 🏗️ Arquitetura

```
app/
├── core/                 # Componentes centrais
│   ├── config.py        # Configurações da aplicação
│   ├── exceptions.py    # Exceções customizadas
│   └── logging_config.py # Configuração de logging
├── data/                # Camada de dados
│   ├── loader.py        # Carregamento de arquivos
│   ├── validator.py     # Validação de dados
│   ├── cache_manager.py # Gerenciamento de cache
│   └── processor.py     # Processamento de relatórios
├── ui/                  # Interface do usuário
│   ├── main.py          # Aplicação principal Streamlit
│   └── components.py    # Componentes reutilizáveis
├── utils/               # Utilitários
│   ├── decorators.py    # Decoradores utilitários
│   ├── file_utils.py    # Utilitários de arquivo
│   └── helpers.py       # Funções auxiliares
tests/                   # Testes unitários
docs/                    # Documentação
```

## 📦 Instalação

### Pré-requisitos

#### Para Desenvolvimento Local
- Python 3.8+
- pip (gerenciador de pacotes Python)

#### Para Docker (Recomendado)
- Docker Engine 20.10+
- Docker Compose 2.0+
- Pelo menos 4GB de RAM disponível
- Portas livres: 8501, 3000, 9090, 9200, 5601, 6379

### Opção 1: Instalação Local

```bash
# Clonar o repositório
git clone https://github.com/Rcffeitosa/sistema-rastreabilidade-trae.git
cd sistema-rastreabilidade-trae

# Instalar dependências
pip install -r requirements.txt

# Instalar dependências de desenvolvimento (opcional)
pip install -r requirements-dev.txt
```

### Opção 2: Docker (Recomendado)

```bash
# Clonar o repositório
git clone https://github.com/Rcffeitosa/sistema-rastreabilidade-trae.git
cd sistema-rastreabilidade-trae

# Primeira execução (setup completo)
make docker-first-run

# OU início rápido (apenas aplicação)
make docker-quick-start
```

### Dependências Principais

- **streamlit**: Interface web
- **pandas**: Manipulação de dados
- **polars**: Processamento de dados de alta performance
- **openpyxl**: Manipulação de arquivos Excel
- **asyncio**: Processamento assíncrono
- **pytest**: Framework de testes

## 🚀 Uso

### Executar a Aplicação

#### Desenvolvimento Local
```bash
streamlit run streamlit_app.py
```

#### Docker
```bash
# Desenvolvimento
make docker-dev

# Produção
make docker-up
```

A aplicação estará disponível em `http://localhost:8501`

### Uso Programático

```python
from app.data.processor import generate_traceability_report

# Gerar relatório
result = await generate_traceability_report(
    status_file="Status_da_Ordem.xlsx",
    rastreabilidade_file="Consulta_Rastreabilidade.csv",
    estoque_file="Consulta_de_Estoque.xlsx",
    output_file="relatorio_consolidado.xlsx"
)

print(f"Relatório gerado: {result['output_file']}")
print(f"Linhas processadas: {result['stats']['total_rows']}")
```

## 🐳 Docker e Containerização

### Arquitetura de Serviços

O sistema utiliza Docker Compose para orquestrar múltiplos serviços:

- **app**: Aplicação Streamlit principal
- **redis**: Cache distribuído para performance
- **nginx**: Proxy reverso para produção
- **prometheus**: Coleta de métricas
- **grafana**: Visualização de métricas e dashboards
- **elasticsearch**: Armazenamento de logs
- **kibana**: Interface para análise de logs
- **filebeat**: Coleta e envio de logs

### Comandos Docker Essenciais

```bash
# Desenvolvimento
make docker-dev              # App + Redis
make docker-dev-full         # Todos os serviços
make docker-dev-build        # Rebuild + desenvolvimento

# Produção
make docker-up               # Inicia todos os serviços
make docker-down             # Para todos os serviços
make docker-restart          # Reinicia serviços

# Monitoramento
make docker-monitoring       # Prometheus + Grafana
make docker-logging          # ELK Stack

# Logs e Status
make docker-logs             # Logs de todos os serviços
make docker-logs-app         # Logs apenas da aplicação
make docker-status           # Status dos containers
make docker-stats            # Estatísticas de recursos

# Utilitários
make docker-shell            # Acessa shell da aplicação
make docker-shell-redis      # Acessa CLI do Redis
make docker-urls             # Mostra URLs de acesso
make docker-backup           # Backup dos dados

# Limpeza
make docker-clean-all        # Remove containers e volumes
make docker-clean-volumes    # Remove apenas volumes
make docker-clean-logs       # Remove logs antigos
```

### URLs de Acesso

| Serviço | URL | Credenciais |
|---------|-----|-------------|
| **Aplicação** | http://localhost:8501 | - |
| **Grafana** | http://localhost:3000 | admin/admin123 |
| **Prometheus** | http://localhost:9090 | - |
| **Kibana** | http://localhost:5601 | elastic/changeme |
| **Elasticsearch** | http://localhost:9200 | elastic/changeme |

## 🧪 Testes

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

# Testes em modo watch
make test-watch
```

### Verificações de Qualidade

```bash
# Linting
make lint

# Formatação
make format
make format-check

# Verificação de tipos
make type-check

# Análise de segurança
make security

# Todas as verificações
make check
```

## 📊 Monitoramento

### Métricas Disponíveis

- Tempo de processamento por arquivo
- Taxa de sucesso/erro
- Número de registros processados
- Uso de memória durante processamento
- Performance do cache (hit rate)
- CPU e memória dos containers
- Latência de rede
- Espaço em disco

### Dashboards Grafana

1. **Dashboard Principal**: Visão geral da aplicação
2. **Dashboard de Sistema**: Recursos dos containers
3. **Dashboard de Cache**: Performance do Redis
4. **Dashboard de Logs**: Análise de erros

## 🔧 Configuração

### Variáveis de Ambiente

```env
# Aplicação
APP_TITLE="Sistema de Rastreabilidade"
APP_VERSION="1.0.0"
MAX_FILE_SIZE_MB=400
CACHE_TTL_HOURS=24
LOG_LEVEL="INFO"

# Performance
ENABLE_ASYNC=true
CHUNK_SIZE=50000
MAX_WORKERS=8

# Cache
REDIS_URL="redis://localhost:6379"
CACHE_ENABLED=true

# Monitoramento
PROMETHEUS_ENABLED=true
GRAFANA_ENABLED=true
ELK_ENABLED=false
```

## 🤝 Contribuição

1. Fork o repositório
2. Crie uma branch para sua feature (`git checkout -b feature/nova-funcionalidade`)
3. Faça commit das suas mudanças (`git commit -m 'feat: adiciona nova funcionalidade'`)
4. Push para a branch (`git push origin feature/nova-funcionalidade`)
5. Abra um Pull Request

### Padrões de Desenvolvimento

- **Código**: Seguir PEP 8 e usar type hints
- **Commits**: Usar Conventional Commits
- **Testes**: Manter cobertura > 80%
- **Documentação**: Atualizar docs para novas features

## 📚 Documentação

- [Documentação Completa](DOCUMENTATION.md)
- [Guia de Contribuição](CONTRIBUTING.md)
- [Changelog](CHANGELOG.md)

## 📄 Licença

Este projeto está licenciado sob a Licença MIT. Veja o arquivo [LICENSE](LICENSE) para detalhes.

## 🏆 Reconhecimentos

- **Streamlit Team** - Framework incrível para aplicações web
- **Polars Team** - Engine de dados de alta performance
- **Docker Team** - Containerização simplificada
- **Comunidade Python** - Ecossistema rico e colaborativo

---

**Desenvolvido com ❤️ para otimizar processos de rastreabilidade**