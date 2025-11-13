# 🏛️ Unity Catalog Databricks

## 📋 Sobre o Projeto

Este repositório contém um workshop prático completo sobre **Unity Catalog** no Databricks, demonstrando a implementação de governança de dados moderna com arquitetura **Medallion (Bronze, Silver, Gold)**.

O projeto aborda desde conceitos fundamentais até implementações avançadas de catálogos, schemas, tabelas, volumes, views, funções e processamento de diferentes formatos de dados.

## 🎯 Objetivos

- ✅ Implementar governança de dados unificada com Unity Catalog
- ✅ Criar arquitetura Medallion para processamento de dados
- ✅ Demonstrar controle de acesso e segurança de dados
- ✅ Estabelecer lineage e metadados centralizados
- ✅ Processar múltiplos formatos de dados (Parquet, CSV, JSON)
- ✅ Implementar volumes para arquivos não estruturados
- ✅ Criar funções personalizadas no Unity Catalog
- ✅ Aplicar Machine Learning com PyTorch para classificação de imagens

```

## 🏗️ Arquitetura do Projeto

```
Unity Catalog
├── demo_catalog/
│   ├── bronze/                    # Dados brutos
│   │   ├── sales                  # Tabela vendas
│   │   ├── image_predictions      # Predições ML
│   │   ├── vw_sales_summary       # View agregada
│   │   ├── raw_files/             # Volume arquivos
│   │   ├── calc_bonus()           # Função UDF
│   │   └── image_classifier       # Modelo MLflow
│   ├── silver/                    # Dados tratados
│   └── gold/                      # Dados negócio
```
            ┌───────────────────────────────┐
            │           Metastore           │
            └───────────────┬───────────────┘
                            │
            ┌───────────────────────────────┐
            │            Catalog            │
            └───────────────┬───────────────┘
                            │
            ┌──────────────────────────────────────────────────┐
            │            Schema / DB                           │
            └───────┬────────┬────────┬──────────┬──────────┬──┘
                    │        │        │          │          │  
                ┌───┴───┐ ┌──┴───┐ ┌──┴───┐ ┌────┴───┐ ┌────┴───┐
                │ Table │ │ View │ │Volume│ │Function│ │ Model  │
                └───────┘ └──────┘ └──────┘ └────────┘ └────────┘

     ```
## 🚀 Funcionalidades Implementadas

### 📊 Catálogo e Schemas
- **Catálogo Principal**: `demo_catalog` - Catálogo de demonstração
- **Schema Bronze**: Armazenamento de dados brutos
- **Schema Silver**: Dados processados e validados
- **Schema Gold**: Dados agregados para análise

### 📈 Tabelas Delta
- **Tabela Sales**: Dados de vendas com schema estruturado
- **Tabela Image Predictions**: Resultados de classificação de imagens com ML

### 📁 Volumes
- **Volume raw_files**: Armazenamento de arquivos não estruturados

### 🔍 Views
- **vw_sales_summary**: Agregação de vendas por produto
- **Views temporárias**: Para processamento de dados Parquet, CSV e JSON

### ⚙️ Funções Personalizadas
- **calc_bonus()**: Função para cálculo de bônus baseado em percentual

### 🤖 MLflow e Machine Learning
- **Registro de Modelos**: Integração com Unity Catalog para versionamento
- **Classificação de Imagens**: Modelo ResNet18 pré-treinado do PyTorch
- **Tracking de Experimentos**: Logs de métricas, parâmetros e artefatos
- **Model Registry**: Gerenciamento centralizado de modelos ML

## 🛠️ Tecnologias Utilizadas

![Databricks](https://img.shields.io/badge/Databricks-%23FF3621.svg?style=for-the-badge&logo=databricks&logoColor=white)
![Apache Spark](https://img.shields.io/badge/Apache%20Spark-E25A1C.svg?style=for-the-badge&logo=apachespark&logoColor=white)
![Delta Lake](https://img.shields.io/badge/Delta%20Lake-00ADD8.svg?style=for-the-badge&logo=deltalake&logoColor=white)
![MLflow](https://img.shields.io/badge/MLflow-0194E2.svg?style=for-the-badge&logo=mlflow&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C.svg?style=for-the-badge&logo=pytorch&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB.svg?style=for-the-badge&logo=python&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-336791.svg?style=for-the-badge&logo=postgresql&logoColor=white)

## 📝 Como Usar

### Pré-requisitos
- Workspace Databricks com Unity Catalog habilitado
- Permissões de administrador ou criação de catálogos
- Cluster Databricks Runtime 11.3 LTS ou superior
- Bibliotecas: PIL, torch, torchvision, mlflow

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

## 📚 Exemplos Completos de Comandos

### 1. 🏛️ Criação de Catálogo
```sql
CREATE CATALOG IF NOT EXISTS demo_catalog
COMMENT 'Catálogo de demonstração criado para o workshop de Unity Catalog';
```

### 2. 📂 Criação de Schemas
```sql
-- Schema Bronze
CREATE SCHEMA IF NOT EXISTS demo_catalog.bronze
COMMENT 'Schema Bronze para dados brutos e heterogêneos';

-- Schema Silver
CREATE SCHEMA IF NOT EXISTS demo_catalog.silver
COMMENT 'Schema Silver para dados tratados';

-- Schema Gold
CREATE SCHEMA IF NOT EXISTS demo_catalog.gold
COMMENT 'Schema Gold para dados que serão utilizados por negócio';
```

### 3. 📊 Criação de Tabelas Delta
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

### 4. 📥 Inserção de Dados Completa
```sql
INSERT INTO demo_catalog.bronze.sales (sales_id, product, quantity, price, sales_date)
VALUES
  -- Grupo 1: Notebook
  (1, 'Notebook Dell', 1, 5500.00, DATE'2025-10-01'),
  (2, 'Notebook Dell', 2, 5200.00, DATE'2025-10-02'),
  (3, 'Notebook Dell', 1, 5300.00, DATE'2025-10-03'),
  (4, 'Notebook Dell', 3, 5400.00, DATE'2025-10-04'),
  (5, 'Notebook Dell', 1, 5600.00, DATE'2025-10-05'),

  -- Grupo 2: Monitor
  (6, 'Monitor LG 27"', 2, 1200.00, DATE'2025-10-06'),
  (7, 'Monitor LG 27"', 1, 1150.00, DATE'2025-10-07'),
  (8, 'Monitor LG 27"', 3, 1180.00, DATE'2025-10-08'),
  (9, 'Monitor LG 27"', 2, 1220.00, DATE'2025-10-09'),
  (10, 'Monitor LG 27"', 1, 1250.00, DATE'2025-10-10'),

  -- Grupo 3: Headset
  (11, 'Headset HyperX', 2, 600.00, DATE'2025-10-11'),
  (12, 'Headset HyperX', 1, 590.00, DATE'2025-10-12'),
  (13, 'Headset HyperX', 3, 620.00, DATE'2025-10-13'),
  (14, 'Headset HyperX', 2, 610.00, DATE'2025-10-14'),
  (15, 'Headset HyperX', 1, 630.00, DATE'2025-10-15');
```

### 5. 👁️ Criação de Views
```sql
CREATE OR REPLACE VIEW demo_catalog.bronze.vw_sales_summary AS
SELECT
  product,
  SUM(quantity) AS total_sold,
  ROUND(SUM(quantity * price), 2) AS revenue
FROM demo_catalog.bronze.sales
GROUP BY product;
```

### 6. 📁 Criação de Volumes
```sql
CREATE VOLUME IF NOT EXISTS demo_catalog.bronze.raw_files
COMMENT 'Volume para arquivos brutos de ingestão inicial';
```

### 7. 🤖 Processamento de Imagens com PyTorch
```python
from PIL import Image
import torch
from torchvision import models, transforms
import urllib.request

# Carregar rótulos do ImageNet
labels_url = "https://raw.githubusercontent.com/pytorch/hub/master/imagenet_classes.txt"
imagenet_labels = urllib.request.urlopen(labels_url).read().decode("utf-8").splitlines()

# Pré-processamento padrão do ResNet
preprocess = transforms.Compose([
    transforms.Resize(256),
    transforms.CenterCrop(224),
    transforms.ToTensor(),
    transforms.Normalize(mean=[0.485, 0.456, 0.406],
                         std=[0.229, 0.224, 0.225])
])

# Carregar imagem e preparar tensor
path = "/Volumes/demo_catalog/bronze/raw_files/gato.jpeg"
input_tensor = preprocess(Image.open(path).convert("RGB")).unsqueeze(0)

# Modelo pré-treinado
model = models.resnet18(weights=models.ResNet18_Weights.DEFAULT)
model.eval()

# Inferência
with torch.no_grad():
    logits = model(input_tensor)
    probs = torch.nn.functional.softmax(logits, dim=1)[0]

topk = torch.topk(probs, k=5)
top5 = [(imagenet_labels[idx], float(probs[idx])) for idx in topk.indices.tolist()]
```

### 8. 💾 Salvando Predições em Tabela Delta
```python
from pyspark.sql import Row
import json

prediction = Row(
    file_path = path,
    top1_label = top5[0][0],
    top1_prob  = top5[0][1],
    top5_json  = json.dumps(top5)
)

spark.createDataFrame([prediction]) \
     .write.mode("append") \
     .saveAsTable("demo_catalog.bronze.image_predictions")
```

### 9. 📄 Leitura Completa de Múltiplos Formatos
```python
# === Leitura com exibição detalhada ===
# Parquet
df_parquet = spark.read.parquet("/Volumes/demo_catalog/bronze/raw_files/dados.parquet")
print("🟢 PARQUET:")
df_parquet.show(truncate=False)

# CSV
df_csv = (
    spark.read
    .option("header", True)
    .option("inferSchema", True)
    .csv("/Volumes/demo_catalog/bronze/raw_files/dados.csv")
)
print("🟢 CSV:")
df_csv.show(truncate=False)

# JSON
df_json = spark.read.json("/Volumes/demo_catalog/bronze/raw_files/dados.json")
print("🟢 JSON:")
df_json.show(truncate=False)
```

### 10. 🔍 Consultas e Filtros
```python
# SELECT específico
df_parquet.select("id", "nome", "salario").show()

# Filtro com WHERE
df_parquet.filter(df_parquet.salario > 9000).select("nome", "salario").show()
```

### 11. 📋 Criação de Views Temporárias
```python
# Criar views temporárias para uso com SQL
df_parquet.createOrReplaceTempView("vw_parquet")
df_csv.createOrReplaceTempView("vw_csv")
df_json.createOrReplaceTempView("vw_json")
```

### 12. ⚙️ Funções Personalizadas
```sql
-- Criar função personalizada
CREATE OR REPLACE FUNCTION demo_catalog.bronze.calc_bonus(salario DOUBLE, percentual DOUBLE)
RETURNS DOUBLE
COMMENT 'Calcula bônus de acordo com o percentual informado'
RETURN salario * (percentual / 100);

-- Usar a função
USE CATALOG demo_catalog;
USE SCHEMA bronze;

SELECT
  nome,
  salario,
  calc_bonus(salario, 10) AS bonus_10
FROM vw_parquet;
```

### 13. 🔍 Consultas e Verificações
```sql
-- Verificar dados na tabela sales
SELECT * FROM demo_catalog.bronze.sales;

-- Consultar view de resumo de vendas
SELECT * FROM demo_catalog.bronze.vw_sales_summary;

-- Verificar predições de imagens
SELECT * FROM demo_catalog.bronze.image_predictions;
```

### 14. 🖼️ Processamento de Imagens Completo
```python
# Visualizar imagem carregada
from PIL import Image

path = "/Volumes/demo_catalog/bronze/raw_files/gato.jpeg"
img = Image.open(path)
display(img)

# Verificar propriedades da imagem
print(img.format, img.size, img.mode)
```

### 15. 📊 Análise de Dados com PySpark
```python
# Exemplo de SELECT * (todos os dados)
df_parquet.select("*").show()

# Exemplo de SELECT específico
df_parquet.select("id", "nome", "salario").show()

# Exemplo com filtro (WHERE)
df_parquet.filter(df_parquet.salario > 9000).select("nome", "salario").show()
```

### 17. 🔍 Comandos de Exploração do Unity Catalog
```sql
-- Listar catálogos disponíveis
SHOW CATALOGS;

-- Listar schemas em um catálogo
SHOW SCHEMAS IN demo_catalog;

-- Listar tabelas em um schema
SHOW TABLES IN demo_catalog.bronze;

-- Listar volumes em um schema
SHOW VOLUMES IN demo_catalog.bronze;

-- Listar funções em um schema
SHOW FUNCTIONS IN demo_catalog.bronze;

-- Descrever estrutura de uma tabela
DESCRIBE TABLE demo_catalog.bronze.sales;

-- Mostrar histórico de uma tabela Delta
DESCRIBE HISTORY demo_catalog.bronze.sales;

-- Mostrar detalhes de um volume
DESCRIBE VOLUME demo_catalog.bronze.raw_files;
```

### 18. 📁 Comandos de Gerenciamento de Arquivos
```python
# Listar arquivos em um volume
dbutils.fs.ls("/Volumes/demo_catalog/bronze/raw_files/")

# Verificar se arquivo existe
dbutils.fs.ls("/Volumes/demo_catalog/bronze/raw_files/gato.jpeg")

# Copiar arquivo para volume (exemplo)
# dbutils.fs.cp("source_path", "/Volumes/demo_catalog/bronze/raw_files/")
```

### 19. 🔄 Configuração de Contexto
```sql
-- Definir catálogo e schema padrão
USE CATALOG demo_catalog;
USE SCHEMA bronze;
```

### 20. 🤖 MLflow - Registro e Versionamento de Modelos
```python
import mlflow
import mlflow.pytorch
from torchvision import models

# Configurar MLflow para usar Unity Catalog
mlflow.set_registry_uri("databricks-uc")

# Iniciar experimento MLflow
mlflow.set_experiment("/Users/<seu-usuario>/image-classification-experiment")

with mlflow.start_run():
    # Carregar modelo pré-treinado
    model = models.resnet18(weights=models.ResNet18_Weights.DEFAULT)
    model.eval()
    
    # Log do modelo no MLflow
    mlflow.pytorch.log_model(
        pytorch_model=model,
        artifact_path="resnet18_model",
        registered_model_name="demo_catalog.bronze.image_classifier"
    )
    
    # Log de métricas e parâmetros
    mlflow.log_param("model_type", "ResNet18")
    mlflow.log_param("pretrained", True)
    mlflow.log_metric("accuracy", 0.95)  # Exemplo de métrica
    
    print("Modelo registrado no Unity Catalog via MLflow!")
```

### 21. 📊 Carregamento de Modelo do MLflow
```python
# Carregar modelo registrado do Unity Catalog
model_name = "demo_catalog.bronze.image_classifier"
model_version = "1"

# Carregar modelo específico
loaded_model = mlflow.pytorch.load_model(
    model_uri=f"models:/{model_name}/{model_version}"
)

# Usar modelo carregado para predição
with torch.no_grad():
    logits = loaded_model(input_tensor)
    probs = torch.nn.functional.softmax(logits, dim=1)[0]
    
print("Modelo carregado e executado com sucesso!")
```

### 22. 🔍 Gerenciamento de Modelos no Unity Catalog
```sql
-- Listar modelos registrados no catálogo
SHOW MODELS IN demo_catalog.bronze;

-- Descrever modelo específico
DESCRIBE MODEL demo_catalog.bronze.image_classifier;

-- Verificar versões do modelo
SHOW MODEL VERSIONS demo_catalog.bronze.image_classifier;
```

## 📊 Benefícios do Unity Catalog

- **🔒 Segurança**: Controle de acesso centralizado e granular
- **📈 Escalabilidade**: Suporte a múltiplos workspaces e clouds
- **🔍 Descoberta**: Catálogo searchável de todos os dados
- **📋 Compliance**: Auditoria completa e lineage automático
- **⚡ Performance**: Otimizações automáticas com Delta Lake
- **🤖 ML Integration**: Suporte nativo para modelos e features
- **📁 Volumes**: Gerenciamento de arquivos não estruturados

## 🎓 Conceitos Avançados Demonstrados

### Unity Catalog
- **Catálogos**: Namespace de alto nível para organização
- **Schemas**: Agrupamento lógico de tabelas e views
- **Tabelas**: Estruturas de dados com governança
- **Volumes**: Armazenamento de arquivos não estruturados
- **Funções**: Lógica reutilizável no catálogo

### Arquitetura Medallion
- **Bronze**: Dados brutos, múltiplos formatos (Parquet, CSV, JSON)
- **Silver**: Dados limpos e validados
- **Gold**: Dados agregados e otimizados para consumo

### Machine Learning Integration
- **PyTorch**: Modelos pré-treinados para classificação
- **Feature Store**: Armazenamento de features para ML
- **Model Registry**: Versionamento de modelos

## 🔧 Instalação de Dependências

### Bibliotecas Python Necessárias
```python
# Instalar PyTorch e torchvision para processamento de imagens
%pip install torch torchvision

# Instalar MLflow para tracking e registro de modelos
%pip install mlflow

# Verificar instalação
import torch
import mlflow
from torchvision import models, transforms
print(f"PyTorch version: {torch.__version__}")
print(f"MLflow version: {mlflow.__version__}")
```

## 🎓 Próximos Passos

- [ ] Implementar transformações Silver e Gold
- [ ] Configurar controle de acesso granular
- [ ] Adicionar data quality checks
- [ ] Implementar pipelines automatizados
- [ ] Configurar alertas e monitoramento
- [ ] Expandir integração MLflow com Unity Catalog
- [ ] Implementar A/B testing de modelos
- [ ] Implementar streaming com Delta Live Tables

## 🤝 Contribuições

Contribuições são bem-vindas! Sinta-se à vontade para:
- Reportar bugs
- Sugerir melhorias
- Adicionar novos exemplos
- Melhorar a documentação

## 📄 Licença

Este projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.

## 👩‍💻
**Vanessa Prado**
- 🔗 LinkedIn: [vanessa-aida](https://www.linkedin.com/in/vanessa-aida/)
- 🐙 GitHub: [@euvanessa-prado](https://github.com/euvanessa-prado)

---

⭐ **Se este projeto foi útil, deixe uma estrela!** ⭐
