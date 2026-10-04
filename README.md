# Godley e dívida pública no Brasil: exercício com dados do BCB

> **Status: exercício de estudo, trabalho em andamento.** Feito para praticar Python e contabilidade nacional (balanços setoriais, à la Godley). As conclusões ainda não são confiáveis; veja "Limitações conhecidas".

## Pergunta

Se o patrimônio financeiro líquido do setor privado é, em essência, o déficit público acumulado (mais o saldo externo), então:

1. a variação da dívida pública acompanha o resultado nominal do governo?
2. a dívida se estabiliza ou explode, dados o juro real (r), o crescimento (g) e o resultado primário (s)?
3. o que acontece com a razão dívida/PIB quando o ajuste fiscal reduz o próprio PIB?

A equação central é `d(t+1) = d(t) · (1+r)/(1+g) − s`, com `d` em % do PIB.

## O que o notebook faz

`Godley_SGS.ipynb`, em células:

1. **Carga e limpeza** dos dados mensais do BCB, com cálculo de IPCA em 12 meses e juro real *ex post*.
2. **Matrizes stock-flow** (balanços e fluxos) com médias recentes.
3. **Gráfico** da DLSP e da DBGG em % do PIB.
4. **Cenários** de trajetória da DBGG (base, otimista, pessimista) e superávit primário de estabilização (s*).
5. **Função de reação fiscal** (Bohn, 1998) por OLS com erros-padrão HAC.
6. **Modelo com multiplicador fiscal**: compara o ajuste "ingênuo" (g fixo) com o ajuste em que o corte reduz o crescimento.

## Limitações conhecidas

- **Cenários:** a célula de projeção subtrai o superávit primário sem converter para pontos percentuais (falta `s * 100`), então o efeito de `s` está subestimado. A célula do multiplicador já está corrigida.
- **Matriz de balanços:** montada com texto, e as linhas não fecham. Falta calcular os valores e incluir o setor externo.
- **Regressão de Bohn:** depende de a série 4945 ser o resultado primário em % do PIB. Com dados mensais, a defasagem da própria variável domina o ajuste.
- **Tratamento de dados:** `interpolate` e `bfill` preenchem lacunas sem avisar.

## Próximos passos

1. Corrigir a unidade de `s` nos cenários.
2. Confirmar as séries 4945 e DLSP em R$.
3. Fazer o teste da identidade e analisar o resíduo.
4. Fazer a matriz de balanços fechar, com o setor externo.

## Referências

- Godley, W. (1999). *Seven Unsustainable Processes*. Levy Economics Institute.
- Godley, W. & Lavoie, M. (2007). *Monetary Economics*. Palgrave Macmillan.
- Bohn, H. (1998). The behavior of U.S. public debt and deficits. *Quarterly Journal of Economics*.
