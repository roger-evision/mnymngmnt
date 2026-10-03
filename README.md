# Bússola de Gastos

Ferramenta para visualizar despesas exportadas do **Money Pro** e definir metas de gastos.
É uma página única (`index.html`), sem instalação nem servidor.

## Como usar

1. Abra `index.html` no navegador (duplo clique).
2. Clique em **Importar planilha** e escolha o `.xlsx` exportado pelo Money Pro
   (colunas `Category`, `Amount`, `Date`, `Account`, `Account (to)`, `Description`).
   Também aceita CSV e cabeçalhos em português (`Categoria`, `Valor`, `Data`, `Conta`, `Descrição`).
3. Navegue pelas abas:
   - **Visão geral**: total realizado, meta e folga; gráfico mês a mês; gastos por categoria;
     composição de cada mês; lista “Onde agir” com as metas estouradas e os maiores gastos ainda
     sem meta.
   - **Metas**: tabela por categoria e subcategoria com média, realizado, meta e uso da meta. A
     meta vale para todo mês, ou só para um mês específico. O botão **Sugerir metas a partir da
     média** preenche a meta com a média dos meses importados menos um corte (0% a 30%).
     A linha **Total** no fim soma todas as categorias.
   - **Lançamentos**: busca e filtro por categoria ou pelos lançamentos a revisar.
   - **Categorias**: árvore categoria › subcategoria › categoria da planilha. Renomeie para
     reorganizar; nomes iguais se juntam. Categorias no formato `Grupo | Item`
     (ex.: `WILLIAM | Escola`) já entram como categoria e subcategoria. “Apostas” entra junto com
     “Rifas e Apostas”.

### Abrir as despesas de qualquer lugar

Clicar numa barra, num bloco do gráfico, num número do resumo, numa linha de “Onde agir”, num
nome ou valor da aba Metas, num lançamento ou numa categoria abre o painel **Despesas** com os
lançamentos daquele recorte, agrupados por dia, com total, média e meta. Dentro do painel:

- os atalhos no topo filtram por subcategoria ou por mês (← volta);
- clicar numa despesa mostra a descrição completa, a conta e a categoria original da planilha;
- dá para editar a descrição (a original da planilha fica guardada e pode ser restaurada);
- dá para mudar a subcategoria só daquele lançamento, ou marcar “Categoria está certa” para
  tirá-lo da lista de revisão.

## Regras de cálculo

- Valores negativos da planilha são despesas; positivos na mesma categoria (estornos,
  devolução de IOF, descontos) abatem a despesa.
- Categorias cujo saldo é positivo são tratadas como receita e ficam fora da análise.
- Lançamentos com `Account (to)` preenchido são transferências e são ignorados.
- Importar uma nova planilha substitui os lançamentos dos meses que ela contém e mantém os
  demais, então dá para ir acumulando trimestres.
- Status da meta: até 90% = dentro da meta; 90–100% = no limite; acima de 100% = acima da meta.

## Onde ficam os dados

Tudo fica no `localStorage` do navegador. Nada é enviado para servidor. Use
**Salvar backup** para gerar um `.json` com lançamentos, categorias e metas, e
**Restaurar backup** para recarregá-lo em outro navegador ou computador.

> Este repositório é público. O `.gitignore` bloqueia `.xlsx`, `.csv` e `.json` para que
> planilhas e backups não sejam commitados por engano.
