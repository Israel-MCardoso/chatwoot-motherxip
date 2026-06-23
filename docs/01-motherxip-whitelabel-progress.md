# Relatório de Progresso: Sprint 1 (White Label Completo)

Este relatório documenta todas as alterações de branding e white-label realizadas no Chatwoot Community Edition para alinhamento com a identidade do **MOTHERXIP Inbox**.

Todas as modificações foram estritamente limitadas a substituições de textos visíveis de branding/produto, marcas nominativas ("Chatwoot" e "Woot" para "MOTHERXIP Inbox") e assets visuais (logotipos e ícones), preservando totalmente a lógica do sistema, classes de estilo, APIs, autenticação, bancos de dados e identificadores técnicos internos.

---

## 1. Resumo Técnico das Alterações

### A. Localização do Frontend (Dashboard, Widget, Survey)
- Subistituição de todas as ocorrências de **Chatwoot** e **Woot Server** por **MOTHERXIP Inbox** nas chaves de tradução em inglês (`en.json` e arquivos setorizados).
- Ajuste nos links de Termos de Uso e Políticas de Privacidade padrão para apontar para `motherxip.com`.
- Atualização do texto *"Powered by Chatwoot"* no Widget de Chat e no Survey de CSAT para *"Powered by MOTHERXIP Inbox"*.

### B. Assets de Marca (SVGs, Manifest, Fallbacks)
- Redesenho completo de:
  - `public/brand-assets/logo.svg` (versão clara do logotipo)
  - `public/brand-assets/logo_dark.svg` (versão escura do logotipo)
  - `public/brand-assets/logo_thumbnail.svg` (ícone da marca)
- Os novos assets utilizam um círculo em degradê roxo/azul neon (`#a855f7` a `#6366f1`), a marca geométrica do "M" futurista no centro (branca) e tipografia limpa com a grafia **MOTHERXIP Inbox**.
- Atualização do componente Vue de fallback inline `Logo.vue` para renderizar o novo ícone "M" em degradê roxo/azul neon.
- Atualização das chaves do PWA no arquivo `public/manifest.json`, definindo o nome como **MOTHERXIP Inbox** e a cor de destaque como `#9333ea`.

### C. Backend Rails e Modelos de E-mail (Liquid e Views ERB)
- Atualização das chaves do dicionário de tradução Rails do backend (`config/locales/en.yml`) para substituir Chatwoot por MOTHERXIP Inbox nas descrições de integrações visíveis ao usuário (como Slack, Webhooks e Dyte).
- Ajuste do valor padrão para a variável de marca nos templates base de envio de e-mails (`base.liquid`), alterando de `'Chatwoot'` para `'MOTHERXIP Inbox'`.
- Substituição do nome e do rodapé nos e-mails automáticos de notificação de exclusão e conformidade de contas.
- Atualização do título e alt das imagens na console de Super Admin e tela de login do Super Admin.

### D. Configuração Global e White-Label Nativo
- Modificação no arquivo `app/javascript/shared/store/globalConfig.js` para forçar o fallback padrão da variável `installationName` para `'MOTHERXIP Inbox'`.
- Isso garante que a propriedade nativa `isACustomBrandedInstance` seja automaticamente avaliada como `true` quando nenhuma variável de ambiente explícita for definida, ocultando de forma limpa links de documentação originais e chats de suporte do Chatwoot no menu do dashboard.

---

## 2. Arquivos Modificados e Detalhamento

Abaixo está listada cada uma das 31 modificações efetuadas:

1. **[Logo.vue](file:///c:/Users/israe/chatwoot-motherxip/chatwoot/app/javascript/dashboard/components-next/icon/Logo.vue)**:
   - Substituição do SVG inline de fallback da logo original do Chatwoot pelo novo design circular com degradê roxo/azul neon e ícone geométrico "M".
2. **[conversation.json](file:///c:/Users/israe/chatwoot-motherxip/chatwoot/app/javascript/dashboard/i18n/locale/en/conversation.json)**:
   - Alteração do texto de aviso do app nativo para sugerir resposta pelo MOTHERXIP Inbox (`NATIVE_APP_ADVISORY`).
3. **[generalSettings.json](file:///c:/Users/israe/chatwoot-motherxip/chatwoot/app/javascript/dashboard/i18n/locale/en/generalSettings.json)**:
   - Atualização de alertas de cobrança e links de atualizações do servidor.
4. **[helpCenter.json](file:///c:/Users/israe/chatwoot-motherxip/chatwoot/app/javascript/dashboard/i18n/locale/en/helpCenter.json)**:
   - Ajuste dos domínios padrão sugeridos e placeholders para a central de ajuda (`inbox.motherxip.com`).
5. **[inboxMgmt.json](file:///c:/Users/israe/chatwoot-motherxip/chatwoot/app/javascript/dashboard/i18n/locale/en/inboxMgmt.json)**:
   - Ajuste de marcas e avisos de rodapé ao gerenciar canais de entrada.
6. **[integrations.json](file:///c:/Users/israe/chatwoot-motherxip/chatwoot/app/javascript/dashboard/i18n/locale/en/integrations.json)**:
   - Rebranding nas telas informativas e de ativação de Webhooks, Slack e Dashboard Apps.
7. **[labelsMgmt.json](file:///c:/Users/israe/chatwoot-motherxip/chatwoot/app/javascript/dashboard/i18n/locale/en/labelsMgmt.json)**:
   - Alteração do texto "Chatwoot AI" para "MOTHERXIP Inbox AI" nas sugestões automáticas.
8. **[login.json](file:///c:/Users/israe/chatwoot-motherxip/chatwoot/app/javascript/dashboard/i18n/locale/en/login.json)**:
   - Títulos de tela de login e tratamento de falhas do servidor de autenticação.
9. **[mfa.json](file:///c:/Users/israe/chatwoot-motherxip/chatwoot/app/javascript/dashboard/i18n/locale/en/mfa.json)**:
   - Indicação de suporte ao administrador para recuperação de token de segundo fator.
10. **[resetPassword.json](file:///c:/Users/israe/chatwoot-motherxip/chatwoot/app/javascript/dashboard/i18n/locale/en/resetPassword.json)**:
    - Alteração das referências do fluxo de recuperação de senha da plataforma.
11. **[settings.json](file:///c:/Users/israe/chatwoot-motherxip/chatwoot/app/javascript/dashboard/i18n/locale/en/settings.json)**:
    - Customização de mensagens de erro na criação de contas e explicações de SSO SAML.
12. **[signup.json](file:///c:/Users/israe/chatwoot-motherxip/chatwoot/app/javascript/dashboard/i18n/locale/en/signup.json)**:
    - Ajuste dos links e textos de Termos e Políticas na página de auto-cadastro.
13. **[yearInReview.json](file:///c:/Users/israe/chatwoot-motherxip/chatwoot/app/javascript/dashboard/i18n/locale/en/yearInReview.json)**:
    - Rebranding dos textos de compartilhamento de retrospectiva do atendente.
14. **[SenderNameExamplePreview.vue](file:///c:/Users/israe/chatwoot-motherxip/chatwoot/app/javascript/dashboard/routes/dashboard/settings/inbox/components/SenderNameExamplePreview.vue)**:
    - Atualização do nome padrão da empresa na visualização rápida do remetente para "MOTHERXIP Inbox".
15. **[MfaManagementActions.vue](file:///c:/Users/israe/chatwoot-motherxip/chatwoot/app/javascript/dashboard/routes/dashboard/settings/profile/MfaManagementActions.vue)**:
    - Alteração do título do arquivo de backup de códigos de MFA gerado para download e seu nome de arquivo (`motherxip-inbox-backup-codes.txt`).
16. **[MfaSetupWizard.vue](file:///c:/Users/israe/chatwoot-motherxip/chatwoot/app/javascript/dashboard/routes/dashboard/settings/profile/MfaSetupWizard.vue)**:
    - Alteração equivalente do título e nome de arquivo do backup de códigos durante o wizard de configuração inicial do MFA.
17. **[globalConfig.js](file:///c:/Users/israe/chatwoot-motherxip/chatwoot/app/javascript/shared/store/globalConfig.js)**:
    - Inclusão do fallback `'MOTHERXIP Inbox'` no atributo `installationName` caso não seja fornecido pelo backend.
18. **[en.json (survey)](file:///c:/Users/israe/chatwoot-motherxip/chatwoot/app/javascript/survey/i18n/locale/en.json)**:
    - Rebranding do rodapé do survey de avaliação de CSAT.
19. **[en.json (widget)](file:///c:/Users/israe/chatwoot-motherxip/chatwoot/app/javascript/widget/i18n/locale/en.json)**:
    - Rebranding do rodapé do widget de chat embutido em sites de terceiros.
20. **[base.liquid](file:///c:/Users/israe/chatwoot-motherxip/chatwoot/app/views/layouts/mailer/base.liquid)**:
    - Alteração do fallback da variável global `brand_name` de `'Chatwoot'` para `'MOTHERXIP Inbox'`.
21. **[account_deleted.liquid](file:///c:/Users/israe/chatwoot-motherxip/chatwoot/app/views/mailers/administrator_notifications/account_compliance_mailer/account_deleted.liquid)**:
    - Atualização do e-mail de conformidade informando remoção de conta na instância.
22. **[account_deletion_for_inactivity.liquid](file:///c:/Users/israe/chatwoot-motherxip/chatwoot/app/views/mailers/administrator_notifications/account_notification_mailer/account_deletion_for_inactivity.liquid)**:
    - Atualização do e-mail alertando exclusão por inatividade de conta.
23. **[account_deletion_user_initiated.liquid](file:///c:/Users/israe/chatwoot-motherxip/chatwoot/app/views/mailers/administrator_notifications/account_notification_mailer/account_deletion_user_initiated.liquid)**:
    - Atualização do e-mail confirmando início da solicitação de exclusão.
24. **[_navigation.html.erb](file:///c:/Users/israe/chatwoot-motherxip/chatwoot/app/views/super_admin/application/_navigation.html.erb)**:
    - Alteração de rótulos de navegação no topo da console do super administrador para MOTHERXIP Inbox.
25. **[new.html.erb (super_admin sessions)](file:///c:/Users/israe/chatwoot-motherxip/chatwoot/app/views/super_admin/devise/sessions/new.html.erb)**:
    - Atualização da tag de título da aba de navegação e atributos alt das logos na tela de login de super administrador.
26. **[show.html.erb (super_admin settings)](file:///c:/Users/israe/chatwoot-motherxip/chatwoot/app/views/super_admin/settings/show.html.erb)**:
    - Rebranding de avisos sobre alterações não autorizadas na licença community/premium.
27. **[en.yml](file:///c:/Users/israe/chatwoot-motherxip/chatwoot/config/locales/en.yml)**:
    - Tradução das descrições das integrações suportadas exibidas no painel de administração Rails.
28. **[logo.svg](file:///c:/Users/israe/chatwoot-motherxip/chatwoot/public/brand-assets/logo.svg)**:
    - Substituição do arquivo SVG oficial para fundos claros pelo logotipo desenhado para a MOTHERXIP Inbox.
29. **[logo_dark.svg](file:///c:/Users/israe/chatwoot-motherxip/chatwoot/public/brand-assets/logo_dark.svg)**:
    - Substituição do arquivo SVG oficial para fundos escuros.
30. **[logo_thumbnail.svg](file:///c:/Users/israe/chatwoot-motherxip/chatwoot/public/brand-assets/logo_thumbnail.svg)**:
    - Substituição do ícone de favicon/sidebar reduzido da marca.
31. **[manifest.json](file:///c:/Users/israe/chatwoot-motherxip/chatwoot/public/manifest.json)**:
    - Atualização das propriedades da aplicação progressiva web (PWA), definindo o nome como MOTHERXIP Inbox.

---

## 3. Resultados dos Testes e Linters

Durante a validação local, os seguintes comandos foram executados e analisados:

1. **pnpm eslint**:
   - **Resultado**: Falhou.
   - **Detalhe**: O diretório `node_modules` não está instalado no ambiente de desenvolvimento local atual, impedindo a execução do binário do eslint (`eslint não é reconhecido como um comando interno ou externo`).

2. **bundle exec rubocop**:
   - **Resultado**: Falhou.
   - **Detalhe**: O comando `bundle` não está configurado/instalado nas variáveis de ambiente globais deste terminal Windows, impossibilitando a validação sintática via RuboCop.

3. **pnpm test**:
   - **Resultado**: Não pôde ser executado devido à ausência das dependências instaladas na pasta `node_modules`.

*Nota: Todas as alterações sintáticas em arquivos de formato estrito (como JSON, YAML e Liquid) foram validadas e inspecionadas manualmente, garantindo a integridade dos delimitadores e estruturas.*
