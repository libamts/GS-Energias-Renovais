# GS-Energias-Renovais
Praça Solar Inteligente — SERS (Global Solution 2026.2)

Contribuição da disciplina Soluções em Energias Renováveis e Sustentáveis (SERS) ao projeto integrador Neighborhood Action Dashboard – CitizenTech (Ciência da Computação).

Integrantes
Nome	RM
Iago Nunes Campos	RM-576738
Jhoel Rayan Calle Soliz	RM-574622
Matheus Libarino da Silva	RM-575073

Vídeo técnico (YouTube, não listado): https://youtu.be/jix_QiGvdRI

Problema

Uma praça comunitária de bairro em São Paulo (praça-tipo, ~0,8 ha) é iluminada por 24 postes com lâmpadas de vapor de sódio (≈ 170 W com reator), acesos em potência plena a noite toda. O consumo é alto, o custo recai sobre o orçamento público e não há medição do uso.

Solução

Combinação de três frentes: eficiência (LED 50 W com dimerização a 30% de madrugada e sensores de presença), fonte renovável (sistema fotovoltaico de 2,75 kWp conectado à rede, com compensação de créditos) e monitoramento (gateway IoT + indicadores para o dashboard).

Três alternativas foram comparadas para a mesma necessidade (24 pontos, 12 h/dia, horizonte de 10 anos):

	Atual	Alt. 1 – LED inteligente	Alt. 2 – Solar autônoma	Alt. 3 – LED + FV conectado
Consumo (kWh/mês)	1.469	273	273	273
Investimento (R$)	0	30.100	138.100	43.300
Retorno simples (anos)	—	2,2	8,8	2,7
Custo total em 10 anos (R$)	171.763	63.860	188.500	55.984
Emissões operacionais (kg CO₂e/ano)	688	128	0	0

Recomendação: Alt. 3 — menor custo total em 10 anos, 81% menos energia e 100% de participação renovável em base anual.

Todos os valores são projeções condicionadas às premissas de sers/dados/premissas.csv (praça-tipo, dados simulados). Veja sers/LIMITACOES.md.

Indicadores (Alt. 3)
Indicador	Valor
Consumo de energia	272,9 kWh/mês
Economia energética	81,4% (1.196 kWh/mês)
Redução de custos	R$ 1.326/mês (R$ 15.908/ano)
Participação renovável	100% (balanço anual)
Emissões evitadas	688 kg CO₂e/ano
Funcionamento eficiente	7 h/dia dimerizadas
Retorno do investimento	2,7 anos
Estrutura do repositório
README.md
sers/
├── dados/
│   ├── premissas.csv          # todas as premissas (tipo: premissa ou fonte)
│   └── fontes.md              # referências e como cada dado foi usado
├── calculos/
│   └── indicadores.py         # consumo, alternativas e indicadores
├── diagramas/                 # diagrama de blocos e gráficos (PNG)
├── dashboard/
│   └── sers_indicadores.json  # dados lidos pelo dashboard
└── LIMITACOES.md
Como executar

Requer apenas Python 3.8+ (biblioteca padrão, sem dependências):

bash
python sers/calculos/indicadores.py

O script lê sers/dados/premissas.csv, imprime um resumo e regrava sers/dashboard/sers_indicadores.json. Para testar outros cenários (tarifa, número de pontos, custos), edite o CSV e rode novamente.

Integração com o dashboard

O front-end do projeto integrador consome sers/dashboard/sers_indicadores.json:

indicadores — valores do mês para os cartões do painel (Alt. 3);
fotovoltaico — dimensionamento (módulos, kWp, geração anual);
alternativas — comparação entre situação atual e Alt. 1, 2 e 3 (investimento, custo operacional, retorno, custo em 10 anos, emissões);
fonte — indica que os dados são simulados; quando houver medições do gateway, troque por medido.
Diagramas
sers/diagramas/fig_diagrama.png — diagrama de blocos (FV → inversor/medidor → quadro → luminárias; sensores → gateway → processamento → dashboard)
sers/diagramas/fig_consumo.png, fig_custo.png, fig_perfil.png — consumo, custo acumulado e dia típico
sers/diagramas/fig_painel.png — protótipo do módulo SERS do dashboard
Documento completo

O relatório em Word (Global_Solution_SERS_Praca_Solar_Inteligente.docx) detalha diagnóstico, fórmulas, alternativas, sensibilidade à tarifa, benefícios e limitações.
