# 🏛️ Unity Catalog Databricks - Workshop Prático

## 📋 Sobre o Projeto

Este repositório contém um workshop prático completo sobre **Unity Catalog** no Databricks, demonstrando a implementação de governança de dados moderna com arquitetura **Medallion (Bronze, Silver, Gold)**.

O projeto aborda desde conceitos fundamentais até implementações avançadas de catálogos, schemas, tabelas e controle de acesso granular.

## 🎯 Objetivos

- ✅ Implementar governança de dados unificada com Unity Catalog
- ✅ Criar arquitetura Medallion para processamento de dados
- ✅ Demonstrar controle de acesso e segurança de dados
- ✅ Estabelecer lineage e metadados centralizados
- ✅ Aplicar melhores práticas de Data Engineering

## 🏗️ Arquitetura

```
Unity Catalog
├── demo_catalog/
│   ├── bronze/          # Dados brutos e heterogêneos
│   │   └── sales        # Tabela de vendas (formato Delta)
│   ├── silver/          # Dados tratados e limpos
│   │   └── [em desenvolvimento]
│   └── gold/            # Dados para consumo de negócio
│       └── [em desenvolvimento]
```

## 🚀 Funcionalidades Implementadas

### 📊 Catálogo e Schemas
- **Catálogo Principal**: `demo_catalog` - Catálogo de demonstração
- **Schema Bronze**: Armazenamento de dados brutos
- **Schema Silver**: Dados processados e validados
- **Schema Gold**: Dados agregados para análise

### 📈 Tabelas Delta
- **Tabela Sales**: Dados de vendas com schema estruturado
  - `sales_id`: Identificador único da venda
  - `product`: Nome do produto
  - `quantity`: Quantidade vendida
  - `price`: Preço unitário
  - `sales_date`: Data da venda

### 🔐 Governança
- Comentários descritivos em todos os objetos
- Estrutura padronizada de nomenclatura
- Controle de acesso baseado em Unity Catalog
- Lineage automático de dados

## 🛠️ Tecnologias Utilizadas

![Databricks](https://img.shields.io/badge/Databricks-%23FF3621.svg?style=for-the-badge&logo=databricks&logoColor=white)
![Apache Spark](https://img.shields.io/badge/Apache%20Spark-E25A1C.svg?style=for-the-badge&logo=apachespark&logoColor=white)
![Delta Lake](https://img.shields.io/badge/Delta%20Lake-00ADD8.svg?style=for-the-badge&logo=deltalake&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-336791.svg?style=for-the-badge&logo=postgresql&logoColor=white)

## 📝 Como Usar

### Pré-requisitos
- Workspace Databricks com Unity Catalog habilitado
- Permissões de administrador ou criação de catálogos
- Cluster Databricks Runtime 11.3 LTS ou superior

### Execução
1. **Clone o repositório**:
   ```bash
   git clone https://github.com/euvanessa-prado/unity_catalog_databricks.git
   ```

2. **Importe o notebook** no Databricks:
   - Acesse seu workspace Databricks
   - Importe o arquivo `Aula -Unity Catalog.ipynb`

3. **Execute as células sequencialmente**:
   - Criação do catálogo
   - Criação dos schemas (Bronze, Silver, Gold)
   - Criação das tabelas Delta
   - Inserção de dados de exemplo

## 📚 Conceitos Abordados

### Unity Catalog
- **Catálogos**: Namespace de alto nível para organização
- **Schemas**: Agrupamento lógico de tabelas e views
- **Tabelas**: Estruturas de dados com governança
- **Volumes**: Armazenamento de arquivos não estruturados

### Arquitetura Medallion
- **Bronze**: Dados brutos, sem transformação
- **Silver**: Dados limpos e validados
- **Gold**: Dados agregados e otimizados para consumo

### Governança de Dados
- **Lineage**: Rastreamento de origem e transformações
- **Metadados**: Informações sobre estrutura e qualidade
- **Controle de Acesso**: Permissões granulares por objeto
- **Auditoria**: Log de todas as operações

## 🔍 Exemplos de Comandos

### Criação de Catálogo
```sql
CREATE CATALOG IF NOT EXISTS demo_catalog
COMMENT 'Catálogo de demonstração criado para o workshop de Unity Catalog';
```

### Criação de Schema
```sql
CREATE SCHEMA IF NOT EXISTS demo_catalog.bronze
COMMENT 'Schema Bronze para dados brutos e heterogêneos';
```

### Criação de Tabela Delta
```sql
CREATE TABLE IF NOT EXISTS demo_catalog.bronze.sales(
   sales_id INT,
   product STRING,
   quantity INT,
   price DOUBLE,
   sales_date DATE
) USING DELTA
COMMENT 'Tabela de vendas brutas no formato Delta';
```

## 📊 Benefícios do Unity Catalog

- **🔒 Segurança**: Controle de acesso centralizado e granular
- **📈 Escalabilidade**: Suporte a múltiplos workspaces e clouds
- **🔍 Descoberta**: Catálogo searchável de todos os dados
- **📋 Compliance**: Auditoria completa e lineage automático
- **⚡ Performance**: Otimizações automáticas com Delta Lake

## 🎓 Próximos Passos

- [ ] Implementar transformações Silver e Gold
- [ ] Configurar controle de acesso granular
- [ ] Adicionar data quality checks
- [ ] Implementar pipelines automatizados
- [ ] Configurar alertas e monitoramento

## 🤝 Contribuições

Contribuições são bem-vindas! Sinta-se à vontade para:
- Reportar bugs
- Sugerir melhorias
- Adicionar novos exemplos
- Melhorar a documentação

## 📄 Licença

Este projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.

## 👩‍💻 Autora

**Vanessa Prado**
- 🔗 LinkedIn: [vanessa-aida](https://www.linkedin.com/in/vanessa-aida/)
- 🐙 GitHub: [@euvanessa-prado](https://github.com/euvanessa-prado)

---

⭐ **Se este projeto foi útil, deixe uma estrela!** ⭐
