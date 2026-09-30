# Falha de acesso ao Qlik Cloud — unidades de saúde dos setores Sul e Leste

## Relato inicial

Informações fornecidas por Lourival Pedrosa em 30/09/2026, para registro e análise posterior:

- Há relato de falha de conexão ao endereço <https://missaosaldaterra.us.qlikcloud.com>.
- O acesso é realizado nas unidades de saúde da Secretaria Municipal de Uberlândia (SMS/PMU) situadas nos setores das regiões Sul e Leste, administradas pela Missão Sal da Terra.
- Lourival Pedrosa atua como Coordenador de Infraestrutura da Missão Sal da Terra.
- Segundo o relato, o acesso à internet dessas unidades ocorre por um link cuja saída para a internet utiliza o mesmo endereço IP público para qualquer acesso realizado dentro da rede PMU/SMS: `177.69.159.129`.
- O objetivo deste registro é reunir informações para uma análise posterior e, em etapa futura, preparar um e-mail ao suporte da NowVertical.

## Evidências apresentadas em 30/09/2026

### Relato do comportamento

- Segundo o usuário, o acesso falha nas unidades dos setores Sul e Leste.
- Segundo o usuário, há acesso ao mesmo endereço com as mesmas credenciais em outra condição de acesso sem a mesma falha. A rede, o horário e demais condições desse acesso bem-sucedido ainda não foram documentados.
- Na imagem fornecida, a mensagem de erro foi transcrita pelo usuário como: “A sua conta foi bloqueada após várias tentativas de login consecutivas”.

### HAR do acesso com falha

Arquivo analisado localmente: `login.qlik.com.har`. SHA-256: `55C7B3EC3BAB260249478382DE9F0860C33B0AB02A4CEBE282A813223B61A754`.

- A captura contém 320 entradas, entre 29/09/2026 13:20:19 e 13:37:28 UTC (10:20:19 a 10:37:28, horário de Brasília).
- Houve duas respostas HTTP `429` para `POST https://login.qlik.com/usernamepassword/login`, às 13:21:12 e 13:37:27 UTC.
- Nas duas respostas, o corpo JSON contém `code: too_many_attempts` e `statusCode: 429`. A descrição da resposta informa, em inglês, que a conta foi bloqueada após múltiplas tentativas consecutivas de login.
- A captura também registra duas respostas HTTP `401` de `GET /api/v1/boot/core-init` no domínio do ambiente, antes do redirecionamento para o login. Esse código, isoladamente, não determina a causa do bloqueio.
- A captura não fornece contagem de conexões simultâneas de todas as unidades, não comprova o IP público de origem das requisições e não contém uma comparação documentada com o acesso bem-sucedido.

O HAR bruto e a imagem não foram publicados neste repositório público. Requisições de autenticação e capturas de tela podem conter dados de sessão, credenciais ou identificadores pessoais. Os arquivos originais permanecem com o usuário.

## Contato do suporte indicado em 30/09/2026

- O usuário informou que a IN1 representa a NowVertical no contrato de suporte e indicou a página <https://nowvertical-pt.in1.com.br/suporte>. A página consultada apresenta o suporte da empresa, menciona equipe certificada Qlik e atendimento centralizado via TopDesk; ela não exibe, no conteúdo consultado, o endereço de e-mail abaixo.
- Uma imagem de cabeçalho de e-mail fornecida pelo usuário mostra uma mensagem de 14/07/2026 enviada por **Suporte - NowVertical** com o endereço `suporte@nowvertical-pt.com`. O mesmo endereço aparece nos destinatários. Isso documenta seu uso naquele contato histórico; não confirma que seja o canal vigente para este novo caso.
- A imagem não foi publicada neste repositório público porque também contém endereços pessoais e informações de outro chamado. Nenhuma mensagem foi enviada ao suporte nesta etapa.
- O usuário informou que **Luan Nunes** foi um contato de suporte que atendeu a organização anteriormente. O cartão de assinatura fornecido o identifica como **IT Support** da NowVertical. Isso documenta o contato anterior, sem confirmar que Luan seja o responsável atual por este caso. Os dados diretos de contato e a imagem não foram publicados neste repositório público.

## Hipótese para investigação

Lourival Pedrosa considera possível que os acessos das unidades Sul e Leste, concentrados no IP público de saída informado (`177.69.159.129`), sejam interpretados pela plataforma como excesso de tentativas ou conexões. Essa relação **não está comprovada** pelas evidências disponíveis. As respostas observadas comprovam o bloqueio apresentado na tentativa de login, mas não identificam se sua causa está ligada ao IP compartilhado, à quantidade de usuários/conexões, a tentativas anteriores ou a outra regra de autenticação.

A análise posterior e eventual contato com o suporte da NowVertical devem pedir a verificação dos registros e das regras aplicadas às tentativas, sem apresentar a hipótese como diagnóstico confirmado.

## Dados ainda não documentados

- Data e horário de início da falha fora da janela capturada no HAR.
- Abrangência por unidade, usuário ou dispositivo.
- Condições e evidência do acesso bem-sucedido com o mesmo endereço e credenciais.
- Contagem de acessos simultâneos e logs do fornecedor que expliquem o bloqueio.
- Confirmação técnica de que o IP informado foi a origem das tentativas capturadas.

Este registro separa relato, evidência observada e hipótese. Não constitui diagnóstico técnico nem confirmação independente do estado atual da conexão.
