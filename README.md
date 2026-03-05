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
