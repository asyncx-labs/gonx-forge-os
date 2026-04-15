# 🛡️ Política de Segurança 

## A Filosofia de Segurança do Gonx Forge OS
Diferente de distribuições comerciais, o **Gonx Forge OS** não possui ferramentas de automação como `apt update` ou `dnf upgrade`. Aqui, a segurança é artesanal e baseada em conhecimento. O controle total do sistema pertence ao operador, o que elimina "caixas-pretas" e fortalece a **Supply Chain Security**.

## Versões Suportadas
Apenas a build estável mais recente do arquivo `.qcow2` é mantida oficialmente.

| Versão | Suportada | Notas |
| :--- | :--- | :--- |
| v1.0.x | ✅ Sim | Versão atual (LFS 12.3 / Kernel 6.13.4) |
| < v1.0 | ❌ Não | Builds de desenvolvimento / Beta |

## Gestão de Vulnerabilidades e Patches
Nesse modelo o processo de correção segue esta lógica simples:

1.  **Divulgação:** Ao identificarmos uma falha em um componente (ex: OpenSSH, Kernel), publicaremos um **Security Advisory** no GitHub.
2.  **O Patch é a Receita:** Não enviaremos um binário atualizado. Em vez disso, forneceremos as **instruções** necessários para que você mesmo aplique a correção.
3.  **Soberania:** É responsabilidade do usuário baixar o novo código-fonte oficial, validar os hashes e recompilar o componente afetado dentro do seu ambiente.
4. **Comunidade:** A aba **Discussions** pode ser usada para trocar informações sobre como realizar patches específicos, mas a execução final é de responsabilidade do desenvolvedor.
5.  **Nova Build:** Periodicamente, lançaremos uma nova imagem `.qcow2` já atualizada para novas instalações.

## Reportando uma Vulnerabilidade
**Não abra Issues públicas para falhas de segurança.** Ajude-nos com a Divulgação Responsável:

1. Envie os detalhes técnicos para: `suporte@asyncx.com.br`
2. Descreva o impacto e como reproduzir a falha.
3. Você receberá um retorno em alguns dias. Validada a falha, você será creditado no anúncio da correção (se desejar).

## O que NÃO é uma vulnerabilidade?
Configurações intencionais de laboratório para fins didáticos:
* Ausência de firewall ou políticas de SELinux/AppArmor pré-configuradas.
* Acesso root direto via console.
* Serviços sem endurecimento (hardening) extremo na build base.

---
*Segurança é um processo de melhoria contínua.*