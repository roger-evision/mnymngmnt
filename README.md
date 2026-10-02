# Bússola de Gastos

Ferramenta para visualizar despesas exportadas do **Money Pro** e definir metas de gastos.
É uma página única (`index.html`), sem instalação nem servidor.

## Como usar

1. Abra `index.html` no navegador (duplo clique).
2. Clique em **Importar planilha** e escolha o `.xlsx` exportado pelo Money Pro
   (colunas `Category`, `Amount`, `Date`, `Account`, `Account (to)`, `Description`).
   Também aceita CSV e cabeçalhos em português (`Categoria`, `Valor`, `Data`, `Conta`, `Descrição`).
3. Navegue pelas abas:
   - **Visão geral**: totais de realizado, previsto e meta; gráfico mês a mês; gastos por
     categoria (clique para abrir as subcategorias); composição de cada mês; lista “Onde agir”
     com as metas estouradas e os maiores gastos ainda sem meta.
   - **Previsto e metas**: tabela por categoria e subcategoria. Preencha o **previsto**
     (quanto espera gastar no mês) e a **meta** (o teto que quer respeitar). Os valores valem
     para todo mês, ou só para um mês específico. O botão **Sugerir a partir da média** preenche
     o previsto com a média dos meses importados e a meta com a média menos um corte (5% a 30%).
   - **Lançamentos**: busca e filtro; clique na subcategoria de um lançamento para mudar só ele
     (útil para os marcados “REVISAR CATEGORIA”).
   - **Categorias**: cada categoria da planilha vira uma subcategoria dentro de uma categoria
     principal. Renomeie para reorganizar. Categorias no formato `Grupo | Item`
     (ex.: `WILLIAM | Escola`) já entram como categoria e subcategoria.

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
**Salvar backup** para gerar um `.json` com lançamentos, categorias, previstos e metas, e
**Restaurar backup** para recarregá-lo em outro navegador ou computador.

> Este repositório é público. O `.gitignore` bloqueia `.xlsx`, `.csv` e `.json` para que
> planilhas e backups não sejam commitados por engano.
