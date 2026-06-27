# NotebookLM-DIO
O objetivo desse projeto é criar um NotebookLM que vai ajudar o usuário a sanar qualquer duvida que venha a ter sobre o Entra ID, desde sua função na tenant até politicas que você pode adicionar em sua tenant.


## Ideias de Prompts
Primeiro Prompt

Forneça 5 recomendações de segurança para aplicar em qualquer tenant, visão seguir o protocolo de Zero Trust.

Sua resposta deve ser estruturada da segunte forma:
- Primeira recomendação - Nome da Politica
		- Passo a Passo
		- Licença necessaria para aplicar a politica
Coloque as recomendações em ordem de prioridade, ou seja, as que geram maior impacto em primeiro

Segundo Prompt

Mostre um paralelo entre as diferenças dos planos do Entra ID P1 e P2.
Monte uma tabela mostrando as funções que cada um tem seguindo um esquema parecido com esse:
			P1 X P2
função1		tem	tem
função2		não	tem

Coloque primeiro todas as funções que o P1 e o P2 tem em comum e depois as funções que só um dos dois tem.

