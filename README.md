# Dinâmica: Design Estratégico do Projeto

## 1. Nome do Projeto
**Green AI**

---

## 2. Objetivo Principal do Projeto
Fornecer um diagnóstico rápido e preciso de doenças em plantas utilizando Inteligência Artificial, a partir de uma foto, para reduzir perdas e aumentar o rendimento da produção e a segurança alimentar.

---

## 3. Identificação dos Subdomínios
Liste os subdomínios do sistema e classifique-os como **Core Domain**, **Supporting Subdomain** ou **Generic Subdomain**.

| **Subdomínio** | **Descrição** | **Tipo** |
| :--- | :--- | :--- |
| Análise de Doenças com IA | É a funcionalidade central que analisa a foto da planta, identifica doenças e sugere ações. | Core Domain |
| Gestão de Assinaturas | Gerencia os planos de assinatura (básico e premium) para os diferentes tipos de produtores. | Supporting |
| Publicidade e Parceiros | Gerencia as recomendações personalizadas de produtos e a receita gerada via anúncios de empresas parceiras. | Supporting |
| Gestão de Contas de Usuário | Responsável pelo cadastro, login e perfis dos agricultores que utilizam a plataforma. | Supporting |
| Pagamentos | Processa os pagamentos das assinaturas dos planos básico e premium. | Generic |
| Relatórios e Histórico | Armazena o histórico de diagnósticos e gera relatórios detalhados para os usuários do plano premium. | Supporting |

---

## 4. Desenho dos Bounded Contexts
Liste e descreva os bounded contexts identificados no projeto. Explique a responsabilidade de cada um.

| **Bounded Context** | **Responsabilidade** | **Subdomínios Relacionados** |
| :--- | :--- | :--- |
| Contexto de Diagnóstico | Recebe a foto da planta, processa na IA, retorna a possível doença e as ações sugeridas. | Análise de Doenças com IA |
| Contexto de Contas e Planos | Gerencia o ciclo de vida dos usuários e suas assinaturas, controlando o acesso a funcionalidades básicas ou premium. | Gestão de Contas de Usuário, Gestão de Assinaturas |
| Contexto de Monetização | Processa os pagamentos das assinaturas e gerencia as parcerias e a exibição de publicidade segmentada. | Pagamentos, Publicidade e Parceiros |
| Contexto de Dados do Produtor | Consolida o histórico de análises e permite a geração de relatórios detalhados para os produtores. | Relatórios e Histórico |

---

## 5. Comunicação entre os Bounded Contexts
Explique como os bounded contexts vão se comunicar. Use os padrões de comunicação, como:
- **Mensageria/Eventos (desacoplado):** Ex.: O Contexto de Consultas emite um evento "Consulta Finalizada", consumido pelo Contexto de Pagamentos.
- **APIs (síncrono):** Ex.: O Contexto de Pagamentos consulta informações de preços no Contexto de Consultas.

| **De (Origem)** | **Para (Destino)** | **Forma de Comunicação** | **Exemplo de Evento/Chamada** |
| :--- | :--- | :--- | :--- |
| Contexto de Diagnóstico | Contexto de Monetização | Mensageria (Evento) | "Diagnóstico Realizado" (para acionar publicidade relevante) |
| Contexto de Diagnóstico | Contexto de Dados do Produtor | Mensageria (Evento) | "Diagnóstico Salvo no Histórico" |
| Contexto de Contas e Planos | Contexto de Monetização | API | Iniciar processamento de pagamento de assinatura. |
| Contexto de Monetização | Contexto de Contas e Planos | Mensageria (Evento) | "Pagamento de Assinatura Confirmado". |
| Contexto de Diagnóstico | Contexto de Contas e Planos | API | Verificar limite de diagnósticos do plano do usuário. |

---

## 6. Definição da Linguagem Ubíqua
Liste os termos principais da Linguagem Ubíqua do projeto. Explique brevemente cada termo.

| **Termo**                    | **Descrição**                                                                                   |
|------------------------------|-----------------------------------------------------------------------------------------------|
| Ex.: Consulta                | Sessão médica entre paciente e médico.                                                       |
| Ex.: Paciente                | Usuário que agenda e realiza consultas.                                                      |
| Ex.: Receita                 | Prescrição médica gerada durante a consulta.                                                 |

---

## 7. Estratégia de Desenvolvimento
Para cada tipo de subdomínio, explique a abordagem para implementação:
- **Core Domain:** Desenvolver internamente com foco total.
- **Supporting Subdomain:** Desenvolver internamente ou parcialmente terceirizar.
- **Generic Subdomain:** Usar ferramentas ou serviços de mercado.

| **Subdomínio**              | **Estratégia**                         | **Ferramentas ou Serviços (se aplicável)** |
|-----------------------------|---------------------------------------|-------------------------------------------|
| Gestão de Consultas         | Desenvolvimento interno               |                                           |
| Cadastro de Usuários        | Interno com uso de Auth0 para login   | Auth0                                     |
| Pagamentos                  | Terceirizar usando API Stripe         | Stripe                                    |

---
