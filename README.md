# NotebookLM - Microsoft Entra ID - https://notebooklm.google.com/notebook/043d28f9-df28-4661-84fe-dfbf55f118dd

Este projeto foi desenvolvido durante o Bootcamp da DIO com o objetivo de explorar o uso do NotebookLM como ferramenta de estudo técnico.

O tema escolhido foi Microsoft Entra ID, por ser atualmente uma das principais soluções de gerenciamento de identidade e acesso da Microsoft.

A proposta foi utilizar documentação oficial da Microsoft para construir uma base de conhecimento capaz de responder perguntas técnicas, comparar funcionalidades, auxiliar em troubleshooting e servir como material de consulta rápida. 


## Objetivos

- Aprender a utilizar o NotebookLM como ferramenta de estudos.
- Consolidar conhecimentos sobre Microsoft Entra ID.
- Aprender técnicas de Engenharia de Prompt.
- Criar um material reutilizável para consultas futuras.
- Construir um guia prático para administradores Microsoft 365.

## Fontes
Todas as fontes usadas para criar esse Notebook vieram de fontes oficiais da Microsoft, para garantir que tudo está de acordo com as normas e funcionalidades que a Microsoft disponibilizou.

Segue links das fontes:

1. Acesso e Segurança:
	- https://learn.microsoft.com/pt-br/entra/identity/conditional-access/overview
	- https://learn.microsoft.com/pt-br/entra/security-copilot/security-copilot-in-entra
	- https://learn.microsoft.com/pt-br/entra/identity/authentication/overview-authentication
	- https://learn.microsoft.com/pt-br/entra/identity/role-based-access-control/custom-overview
 	- https://learn.microsoft.com/pt-br/entra/id-governance/licensing-fundamentals
  	- https://learn.microsoft.com/pt-br/entra/fundamentals/licensing 
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


## Engenharia de Prompts
### 1. Prompt para sugestões de politicas de segurança
Objetivo:

Listar as 5 melhores recomendações de segurança por politicas de Acesso Condicional aplicando o protocolo de Zero Trust

Prompt final usado:
```text
Forneça 5 recomendações de segurança para aplicar em qualquer tenant, visão seguir o protocolo de Zero Trust.

Sua resposta deve ser estruturada da segunte forma:
- Onde são criadas todas as politicas de acesso condicional
- Explique a estrutura da criação de politicas de acesso condicional, ou seja, todos os campos que podem ser modificados e pra que eles servem
- Nome da Politica
		- Uma explicação sobre como a politica funciona
		- Dizer se a politica é uma já gerada pela Microsoft ou não
		- Passo a Passo para criar a politica, incluir os grupos que podem ser adicionados, os protocolos usados, etc.(Excluir as partes que são comuns a criação de qualquer politica de Acesso Condicional)
		- Licença necessaria para aplicar a politica
Coloque as recomendações em ordem de prioridade, ou seja, as que geram maior impacto em primeiro
```
Respota obtida:
---
Para alinhar sua organização à arquitetura de Confiança Zero (*Zero Trust*), o Acesso Condicional do Microsoft Entra é a ferramenta principal. 

Aqui está a estruturação completa de como esse mecanismo funciona e as 5 principais recomendações de segurança, em ordem de prioridade de impacto:

- **Onde são criadas todas as politicas de acesso condicional**
Os administradores que possuem permissão (no mínimo a função de *Security Reader*) podem criar e gerenciar as políticas acessando o centro de administração Microsoft Entra e navegando em **Entra ID > Acesso Condicional**.

- **Estrutura da criação de politicas de acesso condicional**
As políticas de Acesso Condicional funcionam como declarações lógicas de "se-então": *se* um usuário quiser acessar um recurso, *então* ele deverá concluir uma ação. A estrutura é dividida nos seguintes campos modificáveis:
  * **Usuários, grupos ou agentes (Quem):** Serve para direcionar a quem a política se aplica. Você pode incluir ou excluir usuários individuais, grupos de diretório, funções administrativas ou até mesmo identidades de agentes de IA.
  * **Aplicativos de nuvem ou ações (O quê):** Serve para definir os alvos do acesso. Você seleciona se a política afetará aplicativos de nuvem tradicionais, aplicativos locais ou recursos de agentes.
  * **Condições (Como/Onde):** Serve para avaliar os sinais de contexto da tentativa de acesso. Os campos modificáveis aqui incluem:
      * *Informações de localização de IP:* Mapeia países, regiões ou intervalos de IP para aprovar ou bloquear o acesso.
      * *Dispositivos:* Filtra políticas com base na plataforma (ex: iOS, Windows) ou no estado específico do dispositivo.
      * *Aplicativos cliente:* Identifica o protocolo usado na tentativa de acesso, seja via navegador, apps modernos ou protocolos herdados.
      * *Risco calculado e em tempo real:* Integra-se ao *Entra ID Protection* para avaliar se o comportamento de entrada ou o usuário representam algum risco de segurança.
  * **Controles de acesso / Conceder (Decisão):** Serve para ditar a ação final. As opções são:
      * *Bloquear o acesso:* A decisão mais restritiva que impede totalmente a entrada.
      * *Conceder acesso:* Permite o acesso desde que controles sejam cumpridos, como: requerer autenticação de múltiplos fatores (MFA), exigir dispositivo compatível, exigir dispositivo híbrido, exigir alteração de senha, entre outros.

---

### Recomendações de Segurança (Por Ordem de Prioridade)

- **Exigir a autenticação multifator (MFA) para usuários com funções administrativas**
    - **Uma explicação sobre como a politica funciona:** Garante que qualquer conta que possua privilégios elevados passe por uma verificação explícita de identidade antes de obter acesso, protegendo os recursos críticos da organização contra contas comprometidas,.
    - **Dizer se a politica é uma já gerada pela Microsoft ou não:** Sim, pode ser iniciada a partir de uma política de modelo padrão fornecida no portal.
    - **Passo a Passo para criar a politica:**
        * No campo "Usuários", selecione a opção de direcionar a **Funções de diretório** e marque os grupos de administradores (como Administradores Globais, Administradores de Segurança, etc.).
        * Pule para o campo "Controles de acesso / Conceder" e selecione a opção **Requer autenticação de múltiplos fatores**.
    - **Licença necessaria para aplicar a politica:** Microsoft Entra ID P1 ou Microsoft 365 Business Premium,.

- **Bloquear entradas para usuários que tentam usar protocolos de autenticação herdados**
    - **Uma explicação sobre como a politica funciona:** Bloqueia métodos antigos de autenticação que não suportam recursos modernos de segurança (como MFA). Isso impede que invasores usem esses protocolos ultrapassados para explorar vulnerabilidades e invadir contas.
    - **Dizer se a politica é uma já gerada pela Microsoft ou não:** Sim, está disponível como uma política de modelo.
    - **Passo a Passo para criar a politica:**
        * No campo "Usuários", inclua a opção **Todos os usuários** para garantir proteção em toda a organização.
        * No campo "Condições", vá em **Aplicativos cliente** e selecione os protocolos de autenticação herdados.
        * No campo "Controles de acesso / Conceder", escolha a opção **Bloquear o acesso**.
    - **Licença necessaria para aplicar a politica:** Microsoft Entra ID P1 ou Microsoft 365 Business Premium,.

- **Bloquear comportamentos de autenticação arriscados**
    - **Uma explicação sobre como a politica funciona:** Avalia comportamentos suspeitos em tempo real, integrando-se ao *Entra ID Protection*. Seguindo a premissa de "presunção de violação", a política reage a anomalias bloqueando o acesso ou exigindo ações imediatas de correção pelo usuário,.
    - **Dizer se a politica é uma já gerada pela Microsoft ou não:** Sim. Ela existe como modelo e também pode ser sugerida automaticamente pelo **Agente de Otimização de Acesso Condicional** utilizando inteligência artificial,.
    - **Passo a Passo para criar a politica:**
        * No campo "Condições", ative a **Detecção de risco calculada e em tempo real** e configure para níveis de risco alto ou médio.
        * No campo "Controles de acesso / Conceder", escolha **Bloquear o acesso** ou exija ações corretivas, marcando opções como **Exigir uma alteração de senha** e **Requer autenticação de múltiplos fatores**.
    - **Licença necessaria para aplicar a politica:** Microsoft Entra ID P2 (necessário para os recursos baseados em risco).

- **Exigir dispositivos gerenciados pela organização para aplicativos específicos**
    - **Uma explicação sobre como a politica funciona:** Restringe o acesso a recursos vitais da empresa apenas para os dispositivos que são devidamente gerenciados e cumprem as políticas de segurança da organização, bloqueando acessos via dispositivos pessoais desprotegidos,.
    - **Dizer se a politica é uma já gerada pela Microsoft ou não:** Sim, disponível como uma política de modelo.
    - **Passo a Passo para criar a politica:**
        * No campo "Aplicativos", selecione os aplicativos de nuvem ou locais específicos que precisam de proteção.
        * No campo "Controles de acesso / Conceder", selecione **Exigir que o dispositivo seja marcado como compatível** ou **Exigir um dispositivo híbrido ingressado no Microsoft Entra**.
    - **Licença necessaria para aplicar a politica:** Microsoft Entra ID P1 ou Microsoft 365 Business Premium,.

- **Bloquear ou permitir acesso em localizações específicas**
    - **Uma explicação sobre como a politica funciona:** Avalia o tráfego com base nos intervalos de IP definidos pela organização. Permite restringir o acesso apenas a redes confiáveis ou bloquear países inteiros onde não há operações de negócio,.
    - **Dizer se a politica é uma já gerada pela Microsoft ou não:** Sim, esta também é uma política de modelo pronta no portal.
    - **Passo a Passo para criar a politica:**
        * No campo "Condições", selecione **Informações de localização de IP** e direcione para os intervalos de IPs geográficos (países/regiões) que você deseja bloquear ou permitir.
        * No campo "Controles de acesso / Conceder", escolha **Bloquear o acesso** para os IPs não autorizados, ou defina a concessão de acesso caso a condição seja direcionada às redes corporativas seguras.
    - **Licença necessaria para aplicar a politica:** Microsoft Entra ID P1 ou Microsoft 365 Business Premium.
---
Problemas enfrentados:

Conforme eu fui estruturando o prompt ele me retornava sempre somente as recomendações e não um passo a passo completo de como aplica-las. Precisei ajustar o prompt colocando a estrutura que eu queria e pedindo explicando como que eu queria o passo a passo, para ele não repetir as instruções que são comum a todos.
### 2. Prompt para diferenciar os planos Entra ID P1 e P2
Objetivo:

Listar todas as diferenças entre os planos do Entra ID P1 e P2.

Prompt final:
```text
Mostre um paralelo entre as diferenças dos planos do Entra ID P1 e P2.
Monte uma tabela mostrando as funções que cada um tem separando em categorias como, acesso condicional, proteção de identidade, etc.
A tabela deve ser estruturada da seguinte forma:
			Entra ID P1 x Entra ID P2
categorias	sim ou não + explicação das diferenças desse recurso nos planos, caso tenha
Coloque primeiro todas as funções que o P1 e o P2 tem em comum e depois as funções que só um dos dois tem.
```
Resposta obtida:
---
Aqui está o paralelo detalhado entre os planos do Microsoft Entra ID, estruturado conforme solicitado, apresentando primeiro os recursos em comum e, em seguida, os exclusivos.

| Categorias | Entra ID P1 | Entra ID P2 | Explicação das diferenças desse recurso nos planos, caso tenha |
| :--- | :---: | :---: | :--- |
| **Acesso Condicional (Básico)** | **Sim** | **Sim** | Ambos os planos permitem aplicar políticas de Acesso Condicional para controlar o acesso com base em condições como localização do IP, dispositivo e grupo de usuários. |
| **Autenticação e MFA (Autenticação Multifator)** | **Sim** | **Sim** | Ambos suportam diversos métodos de verificação (aplicativos móveis, SMS, chamadas, FIDO2, etc.), alertas de fraude, IPs confiáveis e SSPR (redefinição de senha por autoatendimento) com write-back para o local. |
| **Provisionamento de Aplicativos e Sincronização** | **Sim** | **Sim** | Ambos oferecem provisionamento automatizado de usuários e grupos para aplicativos SaaS e locais, provisionamento controlado por RH ou API e sincronização entre locatários. |
| **Controle de Acesso Baseado em Função (RBAC)** | **Sim** | **Sim** | O uso de funções internas é gratuito, e ambos os planos (P1 e P2) habilitam a criação e atribuição de funções personalizadas no Microsoft Entra, bem como o uso de unidades administrativas para delegação com privilégios mínimos. |
| **Monitoramento, Relatórios e Integridade** | **Sim** | **Sim** | Ambos fornecem acesso a logs de auditoria, logs de entrada, logs de provisionamento e permitem o roteamento desses dados (por exemplo, para o Azure Monitor), além de análises de uso e insights. |
| **Governança do Locatário (Básica)** | **Sim** | **Sim** | Ambos permitem monitoramento da configuração, criação segura de locatários e relações de governança com privilégios granulares de administração delegada. |
| **Proteção de Identidade (Identity Protection)** | **Não** | **Sim** | O P1 não possui políticas ativas de risco e fornece apenas visibilidade limitada de alertas. O P2 oferece acesso completo ao recurso, detectando de forma automatizada usuários e logins de risco em tempo real, fornecendo relatórios detalhados, notificações e forçando o registro de MFA ou redefinições de senha quando credenciais parecem comprometidas. |
| **Acesso Condicional Baseado em Risco** | **Não** | **Sim** | Como depende dos sinais da Proteção de Identidade, apenas o P2 permite integrar níveis de risco calculados (risco do usuário ou da entrada) diretamente nas políticas de Acesso Condicional para bloquear o acesso ou exigir verificações adicionais. |
| **Privileged Identity Management (PIM)** | **Não** | **Sim** | Apenas o P2 inclui o PIM, que substitui o acesso privilegiado permanente por acesso *just-in-time* (temporário). Ele exige que os usuários ativem as funções de administrador apenas quando necessário, podendo exigir aprovações e justificativas para a ativação. |
| **Revisões de Acesso (Access Reviews)** | **Não** | **Sim** | O P2 inclui ferramentas para configurar campanhas periódicas de revisão. Isso permite que gestores ou os próprios usuários atestem e certifiquem se o acesso a determinados grupos ou aplicativos empresariais ainda é justificado e necessário. |
| **Gerenciamento de Direitos (Entitlement Management)** | **Não** | **Sim** | Exclusivo do P2 (e planos de Governança), esse recurso permite agrupar permissões em "pacotes de acesso". Ele automatiza o ciclo de vida do acesso de funcionários e convidados por meio de portais de solicitação (*My Access*), aprovações em múltiplos estágios e expiração automática de acesso. |
---
Problemas enfrentados:

Ao montar o prompt e enviar percebi que, primeiro, a tabela montada estava faltando alguns recursos, então precisei adicionar mais algumas fontes de conhecimento para montar uma tabela melhor. Segundo que a tabela montada não estava do jeito que eu queria, então dei mais detalhes de como eu queria que a tabela ficasse estruturada.
### 3. Prompt Troubleshooting de um erro
Objetivo:

Simular um erro que algum usuário esteja enfrentando e ver como o notebook pode ajudar a resolver esse problema

Prompt final:
```text
Contexto:
Atue como analista de suporte especializado em Microsoft Entra. O objetivo é explicar como diagnosticar e resolver falhas de autenticação.
Um usuário não consegue acessar o Microsoft 365 devido a erro de autenticação.

Priorize abordagem prática e operacional
Inclua ferramentas reais do Entra
Evite explicações teóricas sem ação
Não omita etapas críticas

Divisão de tarefas:
Identificar causas comuns
Indicar logs e ferramentas de análise
Descrever processo de investigação
Apresentar soluções possíveis

Estrutura:
Possíveis causas
Ferramentas/logs (ex: Sign-in Logs)
Passo a passo de troubleshooting
Soluções recomendadas

Objetivo final:
Fornecer um guia prático e completo para resolução de falhas de autenticação no Microsoft Entra.
```
Resposta obtida:
---
### Possíveis causas
*   **Bloqueio por Políticas de Acesso Condicional:** O usuário pode estar tentando acessar de um IP não configurado como confiável, utilizando um dispositivo não gerenciado/não compatível, ou usando protocolos de autenticação herdados que estão bloqueados.
*   **Falta de cumprimento da Autenticação Multifator (MFA):** O acesso ao Microsoft 365 pode exigir um fator secundário de autenticação que o usuário não concluiu com êxito.
*   **Bloqueio de segurança baseado em risco:** O Microsoft Entra ID Protection pode ter detectado um comportamento anômalo (risco de entrada ou de usuário) e bloqueado a autenticação automaticamente.
*   **Falta de atribuição ao aplicativo:** O usuário pode não ter sido atribuído diretamente ou via grupo para acessar o aplicativo corporativo solicitado.

### Ferramentas/logs
*   **Logs de entrada (Sign-in logs):** A ferramenta primária para diagnosticar falhas de autenticação. Ela captura todas as tentativas de login de usuários e aplicativos cliente, revelando exatamente por que um login falhou e quais agentes estão autenticando.
*   **Logs de auditoria:** Usados para verificar o histórico de alterações no diretório, permitindo identificar se alguém revogou permissões ou alterou grupos do usuário recentemente.
*   **Microsoft Entra ID Protection:** Fornece relatórios de segurança detalhados sobre usuários e entradas de risco.
*   **Co-piloto de Segurança (Security Copilot):** Ferramenta baseada em IA, integrada ao painel, que permite investigar incidentes de identidade e consultar logs de entrada utilizando linguagem natural.

### Passo a passo de troubleshooting
1.  **Acesse o Centro de administração do Microsoft Entra** usando uma conta com privilégios adequados, como a função de Leitor de Segurança.
2.  **Analise os Logs de Entrada:** Vá até a seção de logs de entrada para investigar as tentativas do usuário. Verifique o padrão de entrada e identifique a mensagem de erro exata (ex: falha de senha, recusa de MFA ou bloqueio condicional).
3.  **Avalie o Acesso Condicional:** Acesse **Entra ID > Acesso Condicional** e vá até a aba de **Políticas**. Utilize a ferramenta de cenários **"E se" (What If)** para simular o login do usuário e confirmar qual política específica está negando o acesso.
4.  **Investigue Riscos de Identidade:** Se o bloqueio for por risco, verifique os relatórios do **Microsoft Entra ID Protection** para analisar os detalhes da detecção de risco (ex: acesso de locais atípicos ou dispositivos infectados).
5.  **Utilize o Copilot de Segurança (Opcional, mas recomendado):** No painel de navegação esquerdo, abra o chat do Copilot e use prompts práticos. Por exemplo, digite: *"Você pode me fornecer os logs de logon de [email do usuário] das últimas 48 horas? Coloque essas informações em um formato de tabela"* ou *"Liste os logons de risco recentes para [email do usuário]"* para acelerar a investigação.

### Soluções recomendadas
*   **Correção de Acesso Condicional:** Se uma política estiver bloqueando o acesso de forma não intencional, adicione o endereço IP do usuário aos **intervalos de IPs confiáveis** ou exija que o dispositivo seja marcado como compatível no Intune.
*   **Remediação de Risco com MFA/SSPR:** Caso a conta tenha sido sinalizada com risco médio ou alto, utilize políticas para forçar a **redefinição de senha por autoatendimento (SSPR)** ou exija a **Autenticação Multifator (MFA)** para que o próprio usuário possa remediar o risco e recuperar o acesso.
*   **Recuperação de Acesso MFA:** Se o usuário perdeu o acesso ao seu método de MFA, emita um **Passe de Acesso Temporário (TAP)** para que ele consiga fazer a autenticação primária e secundária e registre um novo método.
*   **Prevenção contra Phishing:** Para evitar falhas de autenticação decorrentes do roubo de credenciais via engenharia social, migre o usuário para **métodos de autenticação resistentes a phishing**, como chaves de acesso (FIDO2) ou Windows Hello para Empresas.
*   **Atribuição Correta:** Se a causa for falta de permissão, certifique-se de **atribuir o usuário ou o grupo de associação dinâmica** apropriado ao aplicativo do Microsoft 365, garantindo o provisionamento correto de acesso.
---

Problemas enfrentados:

Como se trata de um troubleshooting de erro, o contexto para a IA deve ser maior para limitar as possibilidade, então tive que montar um prompt mais robusto para que a IA pudesse me trazer uma resposta satisfatória.

## Guia de Estudos
### O que é Entra ID
O **Microsoft Entra ID** é o principal produto da família Microsoft Entra, atuando como um serviço de gerenciamento de identidade e acesso (IAM) baseado em nuvem. Sua função central é fornecer autenticação, imposição de políticas e proteção para usuários, dispositivos, aplicativos e recursos, sendo uma peça fundamental para ajudar as organizações a implementar uma estratégia de segurança de **Confiança Zero (Zero Trust)**.
### Componentes principais
*   **Gerenciamento Centralizado de Identidades:** O serviço atua como a fonte central de autoridade para gerenciar credenciais e diversos tipos de identidades, englobando **identidades humanas** (funcionários e convidados) e **identidades não humanas** (como dispositivos, cargas de trabalho de software e agentes de IA).
*   **Logon Único (SSO):** Permite que os usuários se autentiquem apenas uma vez para obter acesso contínuo e seguro a milhares de aplicativos, sejam eles o Microsoft 365, aplicativos SaaS de terceiros (pré-integrados) ou recursos locais.
*   **Segurança Avançada e Acesso Condicional:** Habilita o uso de **Autenticação Multifator (MFA)** e políticas de **Acesso Condicional**. Essas políticas avaliam sinais em tempo real (como o endereço IP, o status de conformidade do dispositivo e os riscos calculados pelo Microsoft Entra ID Protection) para tomar decisões de conceder, bloquear ou exigir verificações extras antes de liberar o acesso.
*   **Identidade Híbrida:** O Entra ID não se limita à nuvem. Por meio de ferramentas de sincronização, as organizações conseguem conectar seus diretórios locais (como o Active Directory) à nuvem, criando uma identidade de usuário comum que funciona para autenticação em recursos de ambos os ambientes.
*   **Provisionamento Automatizado:** Simplifica o gerenciamento do ciclo de vida das contas, permitindo automatizar a criação, atualização e exclusão de perfis e funções de usuários em diversos sistemas e aplicativos SaaS à medida que eles entram ou saem da organização.
*   **Controle de Acesso Baseado em Função (RBAC):** Oferece funções integradas e personalizadas que permitem aos administradores aplicar o princípio do privilégio mínimo, delegando permissões granulares e específicas para gerenciar recursos do Entra sem a necessidade de conceder acesso total a todo o ambiente.
*   **Monitoramento e Auditoria:** Oferece uma visão abrangente da atividade de identidade por meio de logs de entradas (sign-ins) e de auditoria, ajudando a identificar padrões comportamentais, rastrear quem alterou configurações e solucionar possíveis falhas e ameaças de segurança.
### Glossário
| Termo               | Definição                      |
| ------------------- | ------------------------------ |
| Tenant              | Ambiente Microsoft             |
| Conditional Access  | Controle de acesso             |
| PIM                 | Privileged Identity Management |
| MFA                 | Multi-Factor Authentication    |
| Sign-in Logs        | Logs de autenticação           |
| Identity Governance | Governança de identidade       |
| Managed Identity    | Identidade para recursos Azure |
| Enterprise App      | Aplicação corporativa          |

### Prompts reutilizáveis

## Conclusão

O NotebookLM mostrou ser uma excelente ferramenta para transformar documentação técnica extensa em uma base de conhecimento consultável.

Durante o projeto foi possível aprender não apenas Microsoft Entra ID, mas também técnicas de Engenharia de Prompt, organização de fontes, documentação técnica e criação de material reutilizável para estudos futuros.
