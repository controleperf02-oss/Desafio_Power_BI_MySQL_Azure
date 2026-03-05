# Desafio_Power_BI_MySQL_Azure
# DESAFIO DE PROJETO
## Integrando Dados com MySQL Azure e Transformando com Power BI

### Ementa - Etapas do Desafio
*   Descrevendo o desafio de projeto
*   Criando uma instância do MySQL na Azure
*   Explorando o Recurso - Instância do MySQL
*   Se conectando ao Banco de Dados com Cloud Shell – corte: manter início-9:06
*   Criando Regra no Firewall na Azure para Acesso ao banco de dados
*   Conectando ao MySQL na Azure utilizando Workbench
*   Integrando Power BI com MySQL na Azure

### Descrição do desafio de projeto
1.  Criação de uma instância na Azure para MySQL
2.  Criar o Banco de dados com base disponível no github
3.  Integração do Power BI com MySQL no Azure
4.  Verificar problemas na base a fim de realizar a transformação dos dados

### Diretrizes para transformação dos dados
1.  **Verifique os cabeçalhos e tipos de dados**
2.  **Modifique os valores monetários** para o tipo double preciso
3.  **Verifique a existência dos nulos** e analise a remoção
4.  **Análise de Gerentes:** Os employees com nulos em `Super_ssn` podem ser os gerentes. Verifique se há algum colaborador sem gerente.
5.  **Departamentos:** Verifique se há algum departamento sem gerente.
6.  **Preenchimento de Lacunas:** Se houver departamento sem gerente, suponha que você possui os dados e preencha as lacunas.
7.  **Projetos:** Verifique o número de horas dos projetos.
8.  **Colunas Complexas:** Separar colunas complexas.
9.  **Mesclagem Employee e Departament:** Criar uma tabela employee com o nome dos departamentos associados aos colaboradores. A mescla terá como base a tabela employee (fique atento ao tipo de junção).
10. **Limpeza:** Neste processo elimine as colunas desnecessárias.
11. **Junção Colaboradores e Gerentes:** Realize a junção dos colaboradores e respectivos nomes dos gerentes. Pode ser feito via SQL ou Power BI.
12. **Nomes:** Mescle as colunas de Nome e Sobrenome para ter apenas uma coluna definindo os nomes dos colaboradores.
13. **Localização:** Mescle os nomes de departamentos e localização para que cada combinação seja única (auxilia no modelo estrela futuro).
14. **Justificativa:** Explique por que, neste caso supracitado, podemos apenas utilizar o mesclar e não o atribuir.
15. **Agrupamento:** Agrupe os dados a fim de saber quantos colaboradores existem por gerente.
16. **Otimização:** Elimine as colunas desnecessárias, que não serão usadas no relatório, de cada tabela.


### README: Diretriz 4
Para resolver o problema da tabela employee da coluna ID manager que possui NULL. Conforme as diretrizes numero 4 do desafio. 
"Ao analisar a tabela Department, identifiquei que o colaborador James E Borg de ID 888665555 consta como ID Dept Manager Headquarters. Isso justifica o valor null em sua coluna ID Manager na tabela Employee, confirmando que ele ocupa o topo da hierarquia organizacional."
O campo null foi substituido pelo ID "888665555".

### README: Diretriz 7
Na etapa de transformação da tabela Works_on, manteve o registro com zero horas para garantir que a matriz de alocação (quem está em qual projeto) permanecesse completa, permitindo uma análise real de disponibilidade da equipe.

### README: Diretriz 9
- **Diferença entre Mesclar consulta e Combinar consulta**
**Mesclar (Merge):** É o equivalente ao JOIN no SQL. Você une tabelas lateralmente com base em uma coluna comum (chave). Você usa quando quer trazer informações extras de outra tabela para a mesma linha (ex: trazer o nome do departamento para a tabela do funcionário).

**Combinar/Acrescentar (Append):** É o equivalente ao UNION no SQL. Você coloca uma tabela embaixo da outra. É usado quando você tem tabelas com as mesmas colunas (ex: Vendas de Janeiro e Vendas de Fevereiro) e quer empilhá-las em uma única tabela.

- **Por que Mesclar neste desafio?** Porque os dados são complementares (colunas differentes sobre a mesma entidade) e não repetidos.

### README: Diretriz 10
Para otimizar o modelo de dados, as tabelas originais que serviram de base para as mesclas (Employee1 e Department1) tiveram sua carga desabilitada. Isso garante que apenas a tabela consolidada e limpa seja carregada para o ambiente de visualização, reduzindo o consumo de memória e melhorando a performance do relatório.

### README: Diretriz 13 
**Por que essa unificação é vital para o Modelo Estrela?**

A unificação dos nomes de departamentos com suas respectivas localizações é um passo crítico para a transição do modelo relacional para o Modelo Estrela (Star Schema) por três motivos principais:

- **Criação de Chave Primária Única:** No Modelo Estrela, as tabelas de dimensão precisam de uma chave única por linha. Sem a mesclagem, nomes repetidos (como "Research") quebrariam a regra de unicidade, impedindo o relacionamento de 1:N (Um para Muitos).
- **Definição de Granularidade:** Ao combinar Nome + Local, definimos com precisão a "fatia" do dado (o grão). Isso garante que, ao filtrar por "Research-Houston", o Power BI não traga acidentalmente dados de outras filiais.
- **Performance e Precisão:** Essa etapa evita a necessidade de relacionamentos complexos de "Muitos para Muitos" (Many-to-Many), que são pesados para o motor do Power BI e podem gerar cálculos errados em medidas DAX.

### README: Diretriz 14 
**Por que usar Mesclar (Merge) e não Atribuir (Append)?**

Neste caso, o Mesclar (Merge) é a operação correta porque o objetivo é realizar um JOIN horizontal. Você precisa trazer informações de colunas diferentes que estão em tabelas distintas (o nome do departamento da tabela Department para a tabela Dept_Locations), unindo-as através de uma chave comum (o ID do Departamento).

O Atribuir (Append) é utilizado para um JOIN vertical (empilhamento). Ele serviria apenas se você tivesse duas tabelas com a mesma estrutura de colunas (ex: vendas de Janeiro e vendas de Fevereiro) e quisesse colocá-las uma embaixo da outra. Se usasse o Atribuir aqui, você teria uma tabela "bagunçada" com linhas de IDs e linhas de Nomes, sem nenhuma relação lateral entre elas.

### README: Diretriz 15
Realizei o agrupamento na tabela Summary_Managers para contabilizar colaboradores por gestor, validando a integridade da cadeia de comando. A análise confirmou a conformidade com a regra de negócio, mantendo o número de funcionários sem gerente (0) abaixo do total de gestores (3). Esta etapa de Data Quality garante que não existam registros "órfãos", permitindo a criação de filtros hierárquicos precisos no modelo final.
A Consulta Summary_Managers esta desabilitada.

