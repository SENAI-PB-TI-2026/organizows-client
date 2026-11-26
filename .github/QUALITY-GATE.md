# Quality Gate docente — organizows-client

Este fluxo de CI é mantido pelo professor, não é uma atividade avaliativa e não exige testes unitários, de integração, cobertura ou deploy. Não altera as versões de dependências do projeto.

- **Dependency Review**: novas dependências vulneráveis de severidade alta/crítica falham; depende do dependency graph habilitado.
- **Secret Scan (Gitleaks)**: analisa novos commits com redação integral; execução manual examina o histórico. Credenciais reais devem ser revogadas.
- **CodeQL**: analisa workflows do GitHub Actions. Configure proteção de merge de CodeQL (alta ou superior) depois de validar a execução. Não use simultaneamente default setup e advanced setup.
- O frontend ainda não tem código ou manifesto de dependências. O build e análise de linguagem serão configurados assim que a tecnologia for escolhida, sem assumir uma stack.

- **Dependabot**: configuração de atualizações de Actions para develop; precisa chegar à main para ser reconhecida. Habilitar alertas e atualizações de segurança nativas nas configurações do GitHub.
- **CODEOWNERS**: arquivos de CI e instruções sob revisão docente. Exigir code owner review no ruleset existente de main/develop; confirmar acesso de escrita do proprietário e manter revisão cruzada.

## Ativação administrativa (após a homologação)

1. Habilitar Actions, dependency graph, Dependabot alerts/security updates e secret scanning/push protection.
2. Validar cada workflow em PR; investigar falhas de execução, mapear alertas preexistentes e corrigir separadamente.
3. Preservar proteções vigentes. Exigir os checks de Dependency Review, Secret Scan; exigir análise CodeQL com alertas de segurança altos ou críticos, revisar a baseline e manter PMD/Checkstyle informativos.
4. Exigir aprovação do proprietário para mudanças do CI, aprovação da última alteração por outro revisor e restringir bypass ao professor/admin autorizado. Não exigir checks que ainda não estejam disponíveis na branch.
5. Não usar segredos de produção, `pull_request_target` para executar código de PR, permissões de escrita desnecessárias ou auto-merge. A aplicação não deve ser exposta externamente nesta etapa.
