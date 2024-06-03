# Analise de Produtividade 
**Este projeto analisa a produtividade de uma equipe ao longo de vários dias, utilizando dados de horas trabalhadas, bugs corrigidos e tarefas concluídas. O objetivo é calcular métricas de produtividade, identificar os dias mais e menos produtivos e visualizar esses dados.**


# Bibliotecas Utilizadas
`pandas`: **Para manipulação de dados.**  
`numpy`:**Para operações numéricas.**   
`IPython.display`: **Para exibir resultados em formato Markdown.**  
`altair`: **Para criação de gráficos interativos.**  
`matplotlib`: **Para criação de gráficos estáticos.**  
`seaborn`: **Para visualização de dados.**

# Cálculos Realizados
`Total de Horas Trabalhadas`   
`Média Diária de Horas Trabalhadas`    
`Total de Bugs Corrigidos`    
`Média Diária de Bugs Corrigidos `  
`Total de Tarefas Concluídas`    
`Média Diária de Tarefas Concluídas`  
`Produtividade Diária: Calculada como o número de tarefas concluídas por hora trabalhada.`  

# Código
**python
Copiar código
import pandas as pd
import numpy as np
from IPython.display import display, Markdown
import altair as alt
import matplotlib.pyplot as plt
import seaborn as sns**

total_hora = total_hora_trabalhada = np.array(df['Horas Trabalhadas']).sum()
media_diaria_horas = total_hora / len(df)
bugs_corrigidos = np.array(df['Bugs Corrigidos']).sum()
media_bugs_corrigidos = bugs_corrigidos / len(df)
total_tarefas_concluidas = np.array(df['Tarefas Concluidas']).sum()
media_diaria_tarefas_concluidas = total_tarefas_concluidas / len(df)
produtividade_diaria = total_tarefas_concluidas / total_hora

# Total de horas trabalhadas
display(Markdown(f"**Total de horas trabalhadas:** {total_hora} horas"))
# Média diária de horas trabalhadas
display(Markdown(f'**Média de horas trabalhadas:** {media_diaria_horas:.2f} horas'))
# Total de bugs corrigidos
display(Markdown(f'**Total de bugs corrigidos:** {bugs_corrigidos}'))
# Média de bugs corrigidos
display(Markdown(f'**Média de bugs corrigidos por dia:** {media_bugs_corrigidos:.2f}'))
# Total de tarefas concluídas
display(Markdown(f'**Total de tarefas concluídas:** {total_tarefas_concluidas}'))
# Média diária de tarefas concluídas
display(Markdown(f'**Média diária de tarefas concluídas:** {media_diaria_tarefas_concluidas:.2f}'))
# Produtividade Diária
display(Markdown(f'**Produtividade Diária (Tarefas Concluídas por Hora):** {produtividade_diaria:.2f}'))
Interpretação dos Resultados
Produtividade Diária Ideal: A meta é atingir 1 tarefa por hora trabalhada, o que seria 100% de aproveitamento.
Aproveitamento Médio Atual: 67%, ou seja, é necessário mais do que 1 hora para concluir uma tarefa, ou em uma hora é concluído 67% de uma tarefa.
Dias Mais e Menos Produtivos
Dias Mais Produtivos: Selecionando os 3 dias com produtividade acima da média.
Dias Menos Produtivos: Selecionando os 3 dias com produtividade abaixo da média.
python
Copiar código
# Calculando a produtividade
df['Produtividade'] = df['Tarefas Concluidas'] / df['Horas Trabalhadas']

# Dias mais produtivos
df_mais_produtivo = df[df['Produtividade'] > produtividade_diaria]
df_sorted = df_mais_produtivo.sort_values(by='Produtividade', ascending=False)
df_top_3 = df_sorted.head(3)
display(Markdown(f'**Top 3 dias mais produtivos acima da média (0.67):**'))
display(df_top_3)

# Dias menos produtivos
df_menos_produtivo = df[df['Produtividade'] < produtividade_diaria]
df_menos_produtivo = df_menos_produtivo.sort_values(by='Produtividade', ascending=True).head(3)
display(Markdown(f'**Top 3 dias menos produtivos abaixo da média (0.67):**'))
display(df_menos_produtivo)
Visualização dos Dados
Gráfico de Barras: Mostra a produtividade dos dias menos produtivos.
Gráfico de Linhas: Mostra as horas trabalhadas por dia.
python
Copiar código
# Gráfico de barras
chart = alt.Chart(df_menos_produtivo).mark_bar().encode(
    x=alt.X('Produtividade:Q', title='Produtividade (%)', scale=alt.Scale(domain=[0.4, 0.7])),
    y='Dia:N',
    color='Dia:N',
)
chart

# Gráfico de linhas (matplotlib)
plt.figure(figsize=(10, 5))
plt.plot(df_horas_trabalhadas.index, df_horas_trabalhadas['Horas Trabalhadas'], marker='o')
plt.title('Horas Trabalhadas por Dia')
plt.xlabel('Dias')
plt.ylabel('Horas Trabalhadas')
plt.grid(True)
plt.xticks(rotation=45)
plt.show()

# Gráfico de linhas (seaborn)
plt.figure(figsize=(10, 5))
sns.lineplot(x=df_horas_trabalhadas.index, y='Horas Trabalhadas', data=df_horas_trabalhadas, marker='o')
plt.title('Horas Trabalhadas por Dia')
plt.xlabel('Dias')
plt.ylabel('Horas Trabalhadas')
plt.grid(True)
plt.xticks(rotation=45)
plt.show() 

# Conclusão
**Este projeto forneceu uma visão detalhada da produtividade da equipe ao longo dos dias analisados. As métricas calculadas e as visualizações geradas ajudam a identificar os pontos fortes e as áreas de melhoria na gestão do tempo e na eficiência da equipe.**
