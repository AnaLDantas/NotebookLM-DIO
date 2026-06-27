# NotebookLM-DIO
O objetivo desse projeto é criar um NotebookLM que vai ajudar o usuário a sanar qualquer duvida que venha a ter sobre o Entra ID, desde sua função na tenant até politicas que você pode adicionar em sua tenant. Link do NotebookLM: https://notebooklm.google.com/notebook/043d28f9-df28-4661-84fe-dfbf55f118dd

## Fontes
Todas as fontes usadas para criar esse Notebook vieram de fontes oficiais da Microsoft, para garantir que tudo está de acordo com as normas e funcionalidades que a Microsoft disponibilizou.

Segue links das fontes:

1. Acesso e Segurança:
	- https://learn.microsoft.com/pt-br/entra/identity/conditional-access/overview
	- https://learn.microsoft.com/pt-br/entra/security-copilot/security-copilot-in-entra
	- https://learn.microsoft.com/pt-br/entra/identity/authentication/overview-authentication
	- https://learn.microsoft.com/pt-br/entra/identity/role-based-access-control/custom-overview
2. Administração e Governança:
   	- https://learn.microsoft.com/pt-br/entra/identity/multi-tenant-organizations/overview
   	- https://learn.microsoft.com/pt-br/entra/id-governance/tenant-governance/overview
   	- https://learn.microsoft.com/pt-br/entra/identity/monitoring-health/overview-monitoring-health
   	- https://learn.microsoft.com/pt-br/entra/identity/users/directory-overview-user-model
   	- https://learn.microsoft.com/pt-br/entra/identity/domain-services/overview
3. Conceitos Fundamentais:
	- https://learn.microsoft.com/pt-br/entra/fundamentals/identity-fundamental-concepts
 	- https://notebooklm.google.com/notebook/043d28f9-df28-4661-84fe-dfbf55f118dd
  	- https://learn.microsoft.com/pt-br/entra/fundamentals/what-is-entra
4. Gestão de Aplicação:
   	- https://learn.microsoft.com/pt-br/entra/identity/saas-apps/tutorial-list
   	- https://learn.microsoft.com/pt-br/entra/identity/enterprise-apps/what-is-application-management
   	- https://learn.microsoft.com/pt-br/entra/identity/app-provisioning/user-provisioning
   	- https://learn.microsoft.com/pt-br/entra/identity/app-proxy/overview-what-is-app-proxy
5. Identidade e Dispositivos:
   	- https://learn.microsoft.com/pt-br/azure/active-directory-b2c/
   	- https://learn.microsoft.com/pt-br/entra/identity/managed-identities-azure-resources/overview
   	- https://learn.microsoft.com/pt-br/entra/identity/hybrid/whatis-hybrid-identity
   	- https://learn.microsoft.com/pt-br/entra/identity/devices/overview


## Ideias de Prompts
### 1. Prompt para sugestões de politicas de segurança
```text
Forneça 5 recomendações de segurança para aplicar em qualquer tenant, visão seguir o protocolo de Zero Trust.

Sua resposta deve ser estruturada da segunte forma:
- Primeira recomendação - Nome da Politica
		- Passo a Passo
		- Licença necessaria para aplicar a politica
Coloque as recomendações em ordem de prioridade, ou seja, as que geram maior impacto em primeiro
```
Respota obtida:
```text
O Acesso Condicional é o mecanismo principal de política de Confiança Zero (Zero Trust) da Microsoft, ajudando as organizações a alinhar suas identidades aos princípios de verificação explícita, uso de privilégios mínimos e presunção de violação
. Para configurar essas políticas, os administradores (com pelo menos a função Security Reader) devem acessar o centro de administração navegando em Entra ID > Acesso Condicional

Aqui estão as 5 recomendações de segurança baseadas nas políticas mais aplicadas, ordenadas por prioridade e impacto:
Primeira recomendação - Exigir a autenticação multifator (MFA) para usuários com funções administrativas - Passo a Passo: Acesse o centro de administração e navegue até Entra ID > Acesso Condicional para criar uma nova política
. Na seção "Usuários", direcione a política selecionando funções de diretório específicas, como administradores
. Na seção de controles de acesso, vá em "Conceder" e selecione a decisão Requer autenticação de múltiplos fatores
. Ative e salve a política para garantir a verificação explícita de contas privilegiadas. - Licença necessaria para aplicar a politica: Microsoft Entra ID P1 ou Microsoft 365 Business Premium

Segunda recomendação - Bloquear entradas para usuários que tentam usar protocolos de autenticação herdados - Passo a Passo: No menu de Acesso Condicional, crie uma nova política
. Na aba "Usuários", direcione para todos os usuários para garantir proteção ampla. Nas "Condições", configure os aplicativos cliente para identificar tentativas de login por protocolos herdados. Na aba "Conceder", selecione a decisão Bloquear o acesso, que é a mais restritiva do sistema
. Ative a política. - Licença necessaria para aplicar a politica: Microsoft Entra ID P1 ou Microsoft 365 Business Premium

Terceira recomendação - Bloquear comportamentos de autenticação arriscados - Passo a Passo: No Acesso Condicional, crie uma nova política
. Nas "Condições", utilize a detecção de risco calculada e em tempo real (risco de entrada ou de usuário) integrada ao Microsoft Entra ID Protection
. Em "Conceder", escolha Bloquear o acesso
 ou exija uma mitigação imediata (como MFA ou troca de senha). Ative e salve a política para bloquear o acesso quando os sinais indicarem que a sessão pode ter sido comprometida. - Licença necessaria para aplicar a politica: Microsoft Entra ID P2 (necessário para utilizar os recursos de risco do Microsoft Entra ID Protection)

Quarta recomendação - Exigir dispositivos gerenciados pela organização para aplicativos específicos - Passo a Passo: Crie uma nova política de Acesso Condicional
. Na aba "Aplicativos", aplique a política direcionando-a a aplicativos de nuvem ou locais específicos
. Na aba "Conceder", aplique a verificação de integridade escolhendo Exigir que o dispositivo seja marcado como compatível ou Exigir um dispositivo híbrido ingressado no Microsoft Entra
. Ative a política. - Licença necessaria para aplicar a politica: Microsoft Entra ID P1 ou Microsoft 365 Business Premium

Quinta recomendação - Bloquear ou permitir acesso em localizações específicas - Passo a Passo: Crie intervalos de endereços IP ou especifique países/regiões inteiros
. No menu de Acesso Condicional, crie uma nova política
. Nas "Condições", acesse as informações de localização de IP e selecione o intervalo que você mapeou
. Na aba "Conceder", opte por conceder ou Bloquear o acesso com base nessa localização
. Ative e salve a política. - Licença necessaria para aplicar a politica: Microsoft Entra ID P1 ou Microsoft 365 Business Premium
```
### 2. Prompt para diferenciar os planos Entra ID P1 e P2
```text
Mostre um paralelo entre as diferenças dos planos do Entra ID P1 e P2.
Monte uma tabela mostrando as funções que cada um tem seguindo um esquema parecido com esse:

			P1 X P2
função1		tem	tem
função2		não	tem


Coloque primeiro todas as funções que o P1 e o P2 tem em comum e depois as funções que só um dos dois tem.
```
Resposta obtida:
```text
Aqui está o paralelo detalhado entre os planos Microsoft Entra ID P1 e P2, estruturado conforme você solicitou. A licença P2 engloba todos os recursos do P1, adicionando capacidades avançadas de proteção de identidade e gerenciamento de privilégios.
Função / Recurso 														Entra ID P1 	Entra ID P2
Acesso Condicional (Padrão) para criar políticas de acesso a recursos
																			tem				tem
Atribuição de acesso a aplicativos empresariais
																			tem				tem
Grupos de associação dinâmica (expansão e redução automática de grupos)
																			tem				tem
Criação de funções personalizadas e grupos atribuíveis a funções
																			tem				tem
Agente de Otimização de Acesso Condicional(integrado ao Copilot,
requerendo também SCU)
																			tem				tem
Acesso Condicional e Governança de identidades para agentes de IA
																			tem				tem
Microsoft Entra ID Protection (detecção de riscos e proteção em tempo real)
																			não				tem
Acesso Condicional Baseado em Risco (risco de entrada e risco do usuário)
																			não				tem
Privileged Identity Management (PIM) (acesso temporário just-in-time a
funções)
																			não				tem
Proteção de ID para agentes de IA
																			não				tem
Operação de recursos avançados em Revisões de Acesso e Gerenciamento de
Direitos
																			não				tem
Como a tabela demonstra, enquanto o P1 foca no controle de acesso essencial (como regras fixas de Acesso Condicional e grupos dinâmicos), o P2 se destaca por adicionar a camada de inteligência e segurança em tempo real (ID Protection e acesso baseado em risco) e governança administrativa avançada (PIM).
```
### 3. Prompt Troubleshooting de um erro
```text
Contexto:
Atue como analista de suporte especializado em Microsoft Entra. O objetivo é explicar como diagnosticar e resolver falhas de autenticação.
Um usuário não consegue acessar o Microsoft 365 devido a erro de autenticação.
---
Priorize abordagem prática e operacional
Inclua ferramentas reais do Entra
Evite explicações teóricas sem ação
Não omita etapas críticas
---
Divisão de tarefas:
Identificar causas comuns
Indicar logs e ferramentas de análise
Descrever processo de investigação
Apresentar soluções possíveis
---
Estrutura:
Possíveis causas
Ferramentas/logs (ex: Sign-in Logs)
Passo a passo de troubleshooting
Soluções recomendadas
---
Objetivo final:
Fornecer um guia prático e completo para resolução de falhas de autenticação no Microsoft Entra.
```
Resposta obtida:
```text
Como analista de suporte especializado em Microsoft Entra, aqui está o guia prático e operacional para diagnosticar e resolver falhas de acesso de usuários ao Microsoft 365, seguindo a estrutura solicitada:

Possíveis causas
Quando um usuário não consegue acessar o Microsoft 365, o problema geralmente ocorre após a conclusão do primeiro fator de autenticação (inserção do login), barrado por algum controle de segurança.
As causas mais comuns incluem:
	Bloqueio por Acesso Condicional: O usuário não atendeu a um requisito da política, como tentar acessar de um local não confiável (endereço IP bloqueado), usar um dispositivo não gerenciado/não compatível, ou falhar na autenticação multifator (MFA).
	Comportamento de entrada arriscado: O sistema detectou uma anomalia (como acesso de uma rede anonimizadora ou local atípico) e o Microsoft Entra ID Protection bloqueou a sessão por suspeita de comprometimento da conta.
	Protocolos de autenticação herdados: O usuário está tentando acessar por meio de um cliente ou aplicativo mais antigo que não suporta a autenticação moderna (como MFA) e está sendo bloqueado por padrão.
	Falta de permissão/Licenciamento: O usuário foi removido de um grupo de segurança crítico ou perdeu a atribuição de licença necessária para acessar o aplicativo.

Ferramentas/logs de análise
Para realizar o troubleshooting, utilize as seguintes ferramentas nativas no centro de administração do Microsoft Entra:
	Logs de entrada (Sign-in Logs): Ferramenta fundamental que captura todas as tentativas de login dos usuários e aplicativos clientes, informando o padrão de entrada, método de autenticação utilizado e o motivo exato de uma falha.
	Microsoft Security Copilot (Entra Copilot): Assistente de IA integrado ao portal que permite investigações rápidas em linguagem natural para cruzar logs de entrada e relatórios de risco.
	Logs de auditoria (Audit Logs): Registra o histórico de alterações no locatário, útil para verificar se alguém alterou as funções ou grupos do usuário recentemente.
	Relatórios do Microsoft Entra ID Protection: Fornecem dados e alertas focados em usuários e entradas que foram classificados com algum nível de risco (médio ou alto).

Passo a passo de troubleshooting
	Consulte os Logs de Entrada: Acesse o centro de administração do Microsoft Entra e abra os Logs de entrada. Filtre pelo nome ou e-mail do usuário afetado para localizar a tentativa de acesso ao Microsoft 365. Verifique o status (Falha) e a guia "Detalhes da Autenticação" ou "Acesso Condicional" para ver exatamente qual 	etapa bloqueou o usuário.
	Utilize o Copilot para acelerar a investigação: No painel esquerdo do centro de administração, abra o Copilot chat e envie comandos operacionais diretos, como: "Você pode me fornecer os logs de logon de [e-mail do usuário] das últimas 48 horas? Coloque essas informações em um formato de tabela" ou "Liste os logons de risco recentes para [e-mail do usuário]".
	Verifique as Políticas de Acesso Condicional: Se o log de entrada indicar um bloqueio de Acesso Condicional, vá para Entra ID > Acesso Condicional. Avalie qual política "se-então" afetou o usuário (por exemplo, a política pode estar configurada para "Exigir que o dispositivo seja marcado como compatível" e o usuário tentou acessar de um dispositivo pessoal).
	Avalie o nível de risco da conta: Cruze os dados do log de entrada com os relatórios do Microsoft Entra ID Protection (se possuir licença P2). Verifique se a conta do usuário foi sinalizada por comportamento suspeito que acionou um bloqueio automático.
	Cheque as permissões e o ciclo de vida: Verifique nos Logs de auditoria se o usuário foi desprovisionado, removido do grupo que concede acesso ao Microsoft 365, ou se suas licenças foram revogadas indevidamente.

Soluções recomendadas
Com base no diagnóstico do passo a passo, aplique a solução correspondente:
	Se bloqueado por Acesso Condicional (Exigência de Dispositivo/MFA): Instrua o usuário a cumprir a exigência, como registrar a Autenticação Multifator (MFA) ou realizar o login a partir de um dispositivo corporativo gerenciado (híbrido ingressado no Microsoft Entra).
	Considere recomendar métodos resistentes a phishing, como Windows Hello para Empresas ou chaves FIDO2.
	Se bloqueado por Risco Elevado (ID Protection): Se for um acesso legítimo (falso positivo), você pode ignorar o risco manualmente. Se houver suspeita real, exija uma mitigação imediata forçando o usuário a fazer uma alteração de senha segura através da Redefinição de Senha de Autoatendimento (SSPR) atrelada à MFA.
	Se bloqueado pelo uso de protocolos herdados: Oriente o usuário (ou a equipe de TI local) a atualizar o cliente/aplicativo de e-mail ou sistema que ele está utilizando para uma versão compatível com a autenticação moderna do Microsoft Entra.
	Perda total de credenciais: Se o usuário não conseguir acessar por ter perdido todos os métodos de autenticação, inicie um processo de recuperação de conta de alta garantia. Utilizando o recurso de ID Verificada do Microsoft Entra com Face Check, o usuário pode comprovar sua identidade com um documento emitido pelo governo e uma biometria facial, permitindo a redefinição segura sem depender de senhas antigas ou do suporte técnico tradicional.
```
