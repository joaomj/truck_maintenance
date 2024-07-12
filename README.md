# **Manutenção de Caminhões**
Repo para os arquivos do desafio de manutenção de caminhões usando machine learning.

# **O Problema**
Uma nova empresa de consultoria em ciência de dados foi contratada para resolver e melhorar o planejamento de manutenção de uma empresa de transporte terceirizada. A empresa mantém um número razoável de caminhões em sua frota para realizar entregas em todo o país, mas nos últimos 3 anos tem notado um grande aumento nas despesas relacionadas à manutenção do sistema de ar de seus veículos, apesar de ter mantido o tamanho de sua frota relativamente constante.

**Seu objetivo como consultor é diminuir os custos de manutenção deste sistema específico.** Os custos de manutenção do sistema de ar podem variar dependendo da condição real do caminhão:

- Se um caminhão for enviado para manutenção, mas não apresentar nenhum defeito nesse sistema, cerca de $10 serão cobrados pelo tempo gasto durante a inspeção pela equipe especializada (*FP = False Positive*).
- Se um caminhão for enviado para manutenção e apresentar defeito nesse sistema, $25 serão cobrados para realizar o serviço de reparo preventivo (*TP = True Positive*).
- Se um caminhão com defeitos no sistema de ar não for enviado diretamente para manutenção, a empresa paga $500 para realizar a manutenção corretiva do mesmo, considerando a mão de obra, substituição de peças e outros possíveis inconvenientes (por exemplo, o caminhão quebrou no meio da estrada) (*FN = False Negative*).

Durante a reunião de alinhamento com os responsáveis pelo projeto e a equipe de TI da empresa, algumas informações foram fornecidas a você:
- A equipe técnica informou que todas as informações relativas ao sistema de ar dos caminhos serão disponibilizadas a você, mas por razões burocráticas relacionadas aos contratos da empresa, todas as colunas precisaram ser codificadas.
- A equipe técnica também informou que, devido à recente digitalização da empresa, algumas informações podem estar ausentes no banco de dados enviado a você.

Finalmente, a equipe técnica informou que a fonte das informações vem do setor de manutenção da empresa, onde eles criaram uma coluna no banco de dados chamada **classe:** "pos" seriam aqueles caminhões que tinham defeitos no sistema de ar e "neg" seriam aqueles caminhões que tinham defeito em qualquer sistema que não fosse o sistema de ar.

# **Solução**
1. Carregar dados
2. Limpar dados
3. Tratar dados: desbalanceamento, valores nulos, colunas sem variância
4. Feature Engineering: selecionar features mais importantes
5. Modelagem: escolher métricas de desempenho (Macro F1-Score e Custo de Manutenção); construir modelo baseline; avaliar modelos tradicionais de classificação (Decision Trees, Random Forest e XGBoost); otimizar modelos; testar modelos otimizados; escolher o modelo que resultou no menor custo de manutenção da frota.
6. Gravar Modelo Escolhido

# **Resultados**
O modelo escolhido reduziu em 93% o custo de manutenção da frota comparado ao baseline.

# **Questionário de Avaliação**

**1. Quais passos você tomaria para resolver este problema? Por favor, descreva o mais completamente possível todos os passos que você considera essenciais para resolver o problema.**
   - **Definição do problema**: definir o escopo da solução e as métricas de negócio.
   - **Carregamento dos dados**: obter os dados da fonte, neste caso dois arquivos CSV.
   - **Limpeza dos dados**: verificar desbalanceamento de dados, presença de nulos, dados com formatação incorreta, remoção de duplicados e de colunas sem variância.
   - **Análise Exploratória (EDA)**: tratamento de features com nulos, separação de features por tipo, extração de features importantes.
   - **Engenharia de Features**: adicionar features (utilizando PCA), corrigir desbalanceamento.
   - **Modelagem**: determinar métricas de avaliação de modelos, construir modelo baseline, treinar modelos de ML e testar em dados de cross-validation e teste, otimizar modelos e avaliar métricas de machine learning (Macro F1-Score) e de negócio (Custo de Teste). Selecionar o modelo com a melhor métrica de negócio.
   - **Comunicação de Resultados**: apresentar os resultados à equipe de negócio, destacando os ganhos em relação ao baseline.
   - **Disponibilização do Modelo**: colocar o modelo em produção (deploy), disponibilizando-o em um meio de fácil acesso aos stakeholders.

**2. Qual métrica técnica de ciência de dados você utilizaria para resolver este desafio? Ex: erro absoluto, rmse, etc.**

  Utilizei a Macro F1-Score, pois ela equilibra a importância das classes e avalia a eficiência do modelo tanto em relação aos falsos positivos quanto falsos negativos.

**3. Qual métrica de negócio você utilizaria para resolver o desafio?**
   
   Custo, que chamei de *custo de teste*. É o custo para a empresa após utilizar o modelo classificador em sua frota, considerando custos de verdadeiros positivos, verdadeiros negativos, falsos positivos e falsos negativos.

**4. Como as métricas técnicas se relacionam com as métricas de negócio?**
   
   A métrica Macro F1-Score equilibra recall e precisão, minimizando os custos tanto com falsos positivos ($10) quanto falsos negativos ($500), resultando em uma redução geral nos custos de manutenção.

**5. Que tipos de análises você gostaria de realizar no banco de dados do cliente?**

   - Análise descritiva: para entender a estrutura do dataset.
   - Análise exploratória: para verificar a relação entre features e o target.
   - Análise preditiva: para prever a classe de cada ocorrência.

**6. Que técnicas você usaria para reduzir a dimensionalidade do problema?**
   
   Utilizei PCA (Principal Component Analysis), por ser uma técnica simples e eficaz dado o tamanho do dataset e meus recursos computacionais.

**7. Que técnicas você usaria para selecionar variáveis para o seu modelo preditivo?**
  
   Análise visual de gráficos de violin plot e análise de dispersão das features em relação à classe, para identificar features que possuem valores mais distintos conforme a classe.

**8. Quais modelos preditivos você usaria ou testaria para este problema? Por favor, indique pelo menos 3.**
   
   Utilizei árvores de decisão, random forest e xgboost.

**9. Como você avaliaria qual dos modelos treinados é o melhor?**
   
   Avaliei o custo para a empresa após aplicar cada modelo nos dados de teste. O modelo que apresentar o menor custo é considerado o melhor.

**10. Como você explicaria o resultado do seu modelo? É possível saber quais variáveis são mais importantes?**
    
  O modelo escolhido mostrou o melhor equilíbrio entre falsos positivos e falsos negativos, resultando no menor custo de manutenção para a empresa dentre os modelos avaliados. As features mais importantes são *['ba_004', 'cs_002', 'ee_005', 'ba_000', 'ee_000']* e *['aq_000', 'bg_000', 'bh_000', 'bj_000', 'dn_000']*.

**11. Como você avaliaria o impacto financeiro do modelo proposto?**
    
  O modelo escolhido proporcionou uma **redução de 93% nos custos de manutenção** em comparação ao baseline.

**12. Que técnicas você usaria para otimização dos hiperparâmetros do modelo escolhido?**
    
  Realizei cross-validation com o método k-folds, utilizando regressão logística para calibrar o modelo. Todas essas técnicas fazem parte do método *'CalibratedClassifierCV'* do sklearn.

**13. Quais riscos ou precauções você apresentaria ao cliente antes de colocar este modelo em produção?**

  - Garantir a qualidade dos dados de entrada.
  - Monitorar continuamente o desempenho do modelo para detectar a necessidade de recalibração.
  - Estabelecer um cronograma de reavaliações periódicas do modelo.
  - Implementar um ambiente de testes e recalibração antes de colocar o modelo em produção.
  - Assegurar a disponibilidade contínua dos dados da frota para evitar aumento nos custos de manutenção.

**14. Se o seu modelo preditivo for aprovado, como você o colocaria em produção?**
  
  Implementaria o modelo em uma infraestrutura na nuvem e disponibilizaria através de uma API (usando Flask, por exemplo). Desenvolveria uma interface para que os usuários pudessem acessar o modelo (por exemplo, Streamlit ou bot do Telegram). Criaria um pipeline para os dados da frota alimentarem o modelo.

  Exemplo para Amazon: o modelo estaria em uma imagem Docker. Armazenaria essa imagem no ECR, configuraria a tarefa de previsão no ECS, configuraria a API Rest no API Gateway, integrando com ECS, e faria o deploy da API. Os dados seriam coletados em tempo real pelo Amazon IoT (sensores) e enviados para o API Gateway, de onde seriam direcionados para o ECS.

**15. Se o modelo estiver em produção, como você o monitoraria?**
  
  Monitoraria o desempenho do modelo utilizando ferramentas na nuvem, como Amazon SageMaker. Ficaria atento especialmente ao desvio de performance e de dados.

**16. Se o modelo estiver em produção, como você saberia quando retreiná-lo?**
  
  Quando a performance do modelo ou os dados de entrada apresentarem desvios significativos em relação ao benchmark estabelecido.

# **Para reproduzir a solução**

1. Clonar este repositório: `git clone https://github.com/joaomj/truck_maintenance.git`
2. Criar ambiente virtual para este projeto. Eu utilizei o Miniconda em conjunto com o WSL.
3. Instalar dependências: `conda install --yes --file requirements.txt`
4. Execute o Jupyter Notebook. Eu utilizei o Jupyter através do VS Code.

**Atenção:** os datasets do desafio não estão publicados neste repositório porque são privados.

# **Responsável**
- **Tech Lead:** João Marcos - ([Linkedin](https://www.linkedin.com/in/joaomj))
- Fique à vontade para enviar sugestões!
