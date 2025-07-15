# Guia de Contribuição

## 🤝 Bem-vindo!

Obrigado por considerar contribuir para o Sistema de Rastreabilidade! Este documento fornece diretrizes e informações para ajudar você a contribuir de forma efetiva.

## 📋 Código de Conduta

Este projeto adere ao [Código de Conduta do Contributor Covenant](https://www.contributor-covenant.org/). Ao participar, você concorda em manter um ambiente respeitoso e inclusivo.

### Nossos Compromissos

- **Respeito**: Tratar todos com dignidade e respeito
- **Inclusão**: Acolher pessoas de todas as origens e experiências
- **Colaboração**: Trabalhar juntos de forma construtiva
- **Transparência**: Comunicar de forma clara e honesta

## 🐛 Reportando Bugs

Antes de reportar um bug, verifique se ele já não foi reportado nas [Issues existentes](https://github.com/Rcffeitosa/sistema-rastreabilidade-trae/issues).

### Como Reportar um Bug

1. **Use o template de bug report**
2. **Seja específico**: Descreva o problema claramente
3. **Passos para reproduzir**: Liste os passos exatos
4. **Comportamento esperado**: O que deveria acontecer
5. **Comportamento atual**: O que realmente acontece
6. **Ambiente**: SO, versão do Python, versão do projeto
7. **Screenshots**: Se aplicável, adicione capturas de tela
8. **Logs**: Inclua logs relevantes (remova informações sensíveis)

### Template de Bug Report

```markdown
**Descrição do Bug**
Uma descrição clara e concisa do bug.

**Passos para Reproduzir**
1. Vá para '...'
2. Clique em '....'
3. Role para baixo até '....'
4. Veja o erro

**Comportamento Esperado**
Uma descrição clara do que você esperava que acontecesse.

**Screenshots**
Se aplicável, adicione screenshots para ajudar a explicar o problema.

**Ambiente:**
- OS: [ex: Windows 10, Ubuntu 20.04]
- Python: [ex: 3.9.7]
- Versão do Projeto: [ex: 1.0.0]
- Browser: [ex: Chrome 95.0]

**Logs**
```
Cole os logs relevantes aqui
```

**Contexto Adicional**
Adicione qualquer outro contexto sobre o problema aqui.
```

## 💡 Sugerindo Funcionalidades

Sugestões de novas funcionalidades são sempre bem-vindas!

### Antes de Sugerir

1. **Verifique o roadmap**: Consulte issues com label `enhancement`
2. **Pesquise**: Veja se a funcionalidade já foi sugerida
3. **Considere o escopo**: A funcionalidade se alinha com os objetivos do projeto?

### Template de Feature Request

```markdown
**Resumo da Funcionalidade**
Uma descrição clara e concisa da funcionalidade desejada.

**Problema que Resolve**
Descreva o problema que esta funcionalidade resolveria.

**Solução Proposta**
Descreva a solução que você gostaria de ver implementada.

**Alternativas Consideradas**
Descreva alternativas que você considerou.

**Contexto Adicional**
Adicione qualquer outro contexto, mockups ou exemplos.
```

## 🚀 Configuração do Ambiente de Desenvolvimento

### Pré-requisitos

- Python 3.8+
- Git
- Docker (opcional, mas recomendado)
- Make (para usar os comandos do Makefile)

### Setup Local

```bash
# 1. Fork o repositório no GitHub
# 2. Clone seu fork
git clone https://github.com/SEU_USUARIO/sistema-rastreabilidade-trae.git
cd sistema-rastreabilidade-trae

# 3. Configure o remote upstream
git remote add upstream https://github.com/Rcffeitosa/sistema-rastreabilidade-trae.git

# 4. Crie um ambiente virtual
python -m venv venv

# 5. Ative o ambiente virtual
# Windows
venv\Scripts\activate
# Linux/Mac
source venv/bin/activate

# 6. Instale as dependências
make install-dev

# 7. Configure os hooks de pre-commit
pre-commit install

# 8. Execute os testes para verificar se tudo está funcionando
make test
```

### Setup com Docker

```bash
# Clone e configure como acima, então:
make docker-dev-build
make docker-dev
```

## 🏗️ Estrutura do Projeto

```
sistema-rastreabilidade-trae/
├── app/                     # Código principal da aplicação
│   ├── core/               # Componentes centrais
│   ├── data/               # Camada de dados
│   ├── ui/                 # Interface do usuário
│   └── utils/              # Utilitários
├── tests/                  # Testes
│   ├── unit/              # Testes unitários
│   ├── integration/       # Testes de integração
│   └── fixtures/          # Dados de teste
├── docs/                   # Documentação
├── docker/                 # Arquivos Docker
├── scripts/               # Scripts utilitários
└── config/                # Configurações
```

### Componentes Principais

- **app/core/**: Configurações, exceções, logging
- **app/data/**: Carregamento, validação, processamento de dados
- **app/ui/**: Interface Streamlit
- **app/utils/**: Funções auxiliares e decoradores

## 🔄 Processo de Desenvolvimento

### Workflow Git

1. **Sincronize com upstream**:
   ```bash
   git checkout main
   git pull upstream main
   ```

2. **Crie uma branch para sua feature**:
   ```bash
   git checkout -b feature/nome-da-feature
   # ou
   git checkout -b fix/nome-do-bug
   ```

3. **Faça suas mudanças**:
   - Escreva código seguindo os padrões
   - Adicione/atualize testes
   - Atualize documentação se necessário

4. **Teste suas mudanças**:
   ```bash
   make test
   make lint
   make type-check
   ```

5. **Commit suas mudanças**:
   ```bash
   git add .
   git commit -m "feat: adiciona nova funcionalidade X"
   ```

6. **Push para seu fork**:
   ```bash
   git push origin feature/nome-da-feature
   ```

7. **Abra um Pull Request**

### Convenções de Commit

Usamos [Conventional Commits](https://www.conventionalcommits.org/pt-br/):

- `feat:` Nova funcionalidade
- `fix:` Correção de bug
- `docs:` Mudanças na documentação
- `style:` Formatação, ponto e vírgula, etc
- `refactor:` Refatoração de código
- `test:` Adição ou correção de testes
- `chore:` Tarefas de manutenção

**Exemplos**:
```
feat: adiciona validação de arquivo CSV
fix: corrige erro de encoding em arquivos especiais
docs: atualiza README com novas instruções
test: adiciona testes para processador de dados
```

## 📝 Padrões de Código

### Python

- **PEP 8**: Seguir o guia de estilo oficial
- **Type Hints**: Usar anotações de tipo em todas as funções
- **Docstrings**: Documentar todas as classes e funções públicas
- **Imports**: Organizar imports seguindo isort

### Exemplo de Função

```python
from typing import List, Optional
import pandas as pd

def process_data(
    data: pd.DataFrame,
    columns: List[str],
    filter_empty: bool = True
) -> Optional[pd.DataFrame]:
    """
    Processa dados removendo colunas desnecessárias.
    
    Args:
        data: DataFrame com os dados a serem processados
        columns: Lista de colunas a manter
        filter_empty: Se deve filtrar linhas vazias
        
    Returns:
        DataFrame processado ou None se vazio
        
    Raises:
        ValueError: Se colunas obrigatórias estão ausentes
    """
    if not all(col in data.columns for col in columns):
        raise ValueError("Colunas obrigatórias ausentes")
        
    result = data[columns].copy()
    
    if filter_empty:
        result = result.dropna()
        
    return result if not result.empty else None
```

### Testes

- **Cobertura**: Manter cobertura > 80%
- **Nomenclatura**: `test_<funcionalidade>_<cenario>_<resultado_esperado>`
- **Arrange-Act-Assert**: Estruturar testes claramente
- **Fixtures**: Usar fixtures para dados de teste

### Exemplo de Teste

```python
import pytest
import pandas as pd
from app.data.processor import process_data

class TestProcessData:
    """Testes para a função process_data."""
    
    def test_process_data_with_valid_columns_returns_filtered_data(self):
        # Arrange
        data = pd.DataFrame({
            'col1': [1, 2, None],
            'col2': ['a', 'b', 'c'],
            'col3': [10, 20, 30]
        })
        columns = ['col1', 'col2']
        
        # Act
        result = process_data(data, columns, filter_empty=True)
        
        # Assert
        assert result is not None
        assert len(result) == 2
        assert list(result.columns) == columns
        
    def test_process_data_with_missing_columns_raises_error(self):
        # Arrange
        data = pd.DataFrame({'col1': [1, 2, 3]})
        columns = ['col1', 'missing_col']
        
        # Act & Assert
        with pytest.raises(ValueError, match="Colunas obrigatórias ausentes"):
            process_data(data, columns)
```

## 🧪 Executando Testes

### Comandos Disponíveis

```bash
# Todos os testes
make test

# Testes específicos
make test-unit
make test-integration
make test-performance

# Com cobertura
make coverage

# Testes em modo watch (re-executa quando arquivos mudam)
make test-watch

# Testes específicos
pytest tests/unit/test_processor.py::TestProcessData::test_specific_method
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

## 📖 Documentação

### Atualizando Documentação

- **README.md**: Informações gerais e quick start
- **DOCUMENTATION.md**: Documentação técnica completa
- **Docstrings**: Documentação inline do código
- **CHANGELOG.md**: Registro de mudanças

### Gerando Documentação

```bash
# Gerar documentação da API
make docs

# Servir documentação localmente
make docs-serve
```

## 🔍 Pull Request Guidelines

### Antes de Submeter

- [ ] Código segue os padrões estabelecidos
- [ ] Testes passam (`make test`)
- [ ] Linting passa (`make lint`)
- [ ] Type checking passa (`make type-check`)
- [ ] Documentação atualizada se necessário
- [ ] CHANGELOG.md atualizado para mudanças significativas

### Template de Pull Request

```markdown
## Descrição
Descreva brevemente as mudanças implementadas.

## Tipo de Mudança
- [ ] Bug fix (mudança que corrige um problema)
- [ ] Nova funcionalidade (mudança que adiciona funcionalidade)
- [ ] Breaking change (mudança que quebra compatibilidade)
- [ ] Documentação (mudança apenas na documentação)

## Como Testar
1. Passo 1
2. Passo 2
3. Passo 3

## Checklist
- [ ] Meu código segue os padrões do projeto
- [ ] Revisei meu próprio código
- [ ] Comentei código complexo
- [ ] Atualizei a documentação
- [ ] Meus testes passam localmente
- [ ] Adicionei testes para novas funcionalidades

## Screenshots (se aplicável)

## Issues Relacionadas
Fixes #123
```

### Processo de Review

1. **Automated Checks**: CI/CD executa testes automaticamente
2. **Code Review**: Maintainers revisam o código
3. **Feedback**: Discussão e sugestões de melhorias
4. **Approval**: Aprovação após atender aos critérios
5. **Merge**: Merge para a branch principal

## 🏷️ Labels e Milestones

### Labels de Issues

- `bug`: Algo não está funcionando
- `enhancement`: Nova funcionalidade ou melhoria
- `documentation`: Melhorias na documentação
- `good first issue`: Bom para iniciantes
- `help wanted`: Ajuda extra é bem-vinda
- `priority:high`: Alta prioridade
- `priority:medium`: Média prioridade
- `priority:low`: Baixa prioridade

### Labels de Pull Requests

- `work in progress`: PR ainda em desenvolvimento
- `ready for review`: Pronto para revisão
- `needs changes`: Precisa de mudanças
- `approved`: Aprovado para merge

## 🎯 Roadmap e Prioridades

### Próximas Funcionalidades

1. **API REST** - Integração com outros sistemas
2. **Dashboard Avançado** - Métricas em tempo real
3. **Suporte Multi-idioma** - Internacionalização
4. **Integração Cloud** - AWS S3, Azure Blob
5. **Notificações** - Email e webhooks

### Como Contribuir

- **Iniciantes**: Procure issues com `good first issue`
- **Experientes**: Issues com `help wanted` ou `enhancement`
- **Documentação**: Sempre há espaço para melhorias
- **Testes**: Aumente a cobertura de testes
- **Performance**: Otimizações são sempre bem-vindas

## 📞 Suporte e Comunicação

### Canais de Comunicação

- **Issues**: Para bugs e feature requests
- **Discussions**: Para perguntas e discussões gerais
- **Email**: Para questões sensíveis ou privadas

### Obtendo Ajuda

1. **Documentação**: Consulte README e DOCUMENTATION.md
2. **Issues**: Procure issues similares
3. **Discussions**: Faça perguntas na seção de discussões
4. **Code Review**: Peça feedback em PRs

## 🙏 Reconhecimentos

Todos os contribuidores são reconhecidos e valorizados. Contribuições incluem:

- Código
- Documentação
- Testes
- Relatórios de bugs
- Sugestões de funcionalidades
- Revisões de código
- Suporte à comunidade

---

**Obrigado por contribuir para o Sistema de Rastreabilidade!** 🚀

Sua contribuição ajuda a tornar este projeto melhor para todos. Se você tem dúvidas sobre este guia, não hesite em abrir uma issue ou discussion.