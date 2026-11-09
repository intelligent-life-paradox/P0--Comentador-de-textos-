# P0 — Comentador de textos

Aplicação em Python que utilizará um modelo de linguagem (LLM) para explicar trechos de difícil compreensão em linguagem acessível.

Projeto da capacitação Softex/Trends-IA, referente ao **P0 — Primeiro fluxo com LLM**.

**Status:** planejamento. Este repositório contém a proposta inicial; a aplicação ainda não foi implementada e não há testes executados ou instruções de instalação disponíveis.

## O problema

Textos filosóficos, científicos ou escritos com linguagem rebuscada podem ser difíceis de compreender sem familiaridade com os conceitos envolvidos. Expressões regionais também podem exigir contexto.

O Comentador pretende ajudar o leitor a entender um trecho, esclarecendo termos e apresentando exemplos, com cuidado para preservar o sentido e indicar possíveis ambiguidades.

## Proposta e escopo inicial

O usuário fornecerá um trecho de texto pelo terminal. A aplicação enviará uma solicitação à API de um LLM, processará a resposta e exibirá uma explicação em português.

A saída planejada terá três partes:

1. **Em palavras simples:** explicação acessível do trecho.
2. **Termos importantes:** esclarecimento dos conceitos necessários à compreensão.
3. **Um exemplo:** situação concreta ou analogia, quando útil.

Quando o contexto for insuficiente, a resposta deverá explicitar a incerteza ou solicitar mais contexto. Analogias deverão ser identificadas como aproximações.

A primeira versão terá uma interface de terminal e trabalhará com um trecho por solicitação. Interface web, leitura de PDFs e histórico ficam fora do escopo inicial.

## Fluxo previsto

Texto do usuário → validação da entrada → solicitação à API do LLM → processamento da resposta → apresentação da explicação.

## Exemplo de entrada

> O conhecimento científico é provisório e passível de revisão diante de novas evidências.

**Comportamento esperado:** explicar o caráter revisável do conhecimento científico em termos cotidianos, esclarecer os termos relevantes e oferecer um exemplo adequado.

Este exemplo descreve o resultado desejado; não representa uma execução da aplicação.

## Decisões iniciais

- **Python:** linguagem exigida pelo enunciado e adequada para uma aplicação pequena.
- **Terminal:** interface simples para manter o foco no primeiro fluxo com LLM.
- **Resposta organizada:** facilitar a leitura e a avaliação das explicações.
- **Preservação do sentido:** simplificar sem apresentar interpretações incertas como fatos.

O provedor, o modelo, as dependências e o formato de processamento da resposta ainda serão definidos conforme a documentação do serviço e as orientações institucionais aplicáveis.

## Plano de testes

Os casos abaixo estão planejados e ainda não foram executados.

| Situação | Resultado esperado |
|---|---|
| Trecho difícil com contexto suficiente | Explicação organizada, acessível e fiel ao sentido original |
| Expressão ambígua ou sem contexto | Indicação da ambiguidade e pedido de contexto quando necessário |
| Entrada vazia ou somente com espaços | Mensagem de validação, sem chamada à API |
| Chave de API ausente | Orientação clara sobre a configuração necessária |
| Chave de API inválida | Mensagem compreensível de falha de autenticação |
| Falha de conexão ou indisponibilidade do serviço | Mensagem de erro clara, sem apresentar resultado fictício |
| Resposta vazia ou em formato inesperado | Tratamento da resposta inválida e aviso ao usuário |

Além de verificar o funcionamento do programa, será necessário avaliar manualmente se as explicações preservam o sentido dos trechos usados nos testes.

## Etapas para concluir o P0

- [ ] Escolher o provedor e o modelo conforme as orientações do curso.
- [ ] Implementar a entrada textual e sua validação.
- [ ] Integrar a API do LLM.
- [ ] Processar e apresentar a resposta.
- [ ] Tratar falhas de configuração, comunicação e resposta.
- [ ] Executar testes de sucesso e de falha e registrar evidências.
- [ ] Documentar dependências, instalação, configuração e execução.
- [ ] Explicar as principais decisões da implementação.
- [ ] Atualizar a declaração de uso de IA para refletir o desenvolvimento realizado.

A documentação final deverá permitir que outra pessoa instale, configure e execute a aplicação seguindo apenas este repositório.

## Uso de ferramentas de IA

Na etapa de planejamento, o autor utilizou o ChatGPT para discutir a ideia, avaliar sua adequação ao enunciado e delimitar o escopo inicial.

O Codex foi utilizado para redigir e publicar este README e adicionar o projeto ao repositório agregador. Até esta etapa, não houve implementação de código nem execução de testes por essas ferramentas.

Esta declaração deverá ser atualizada conforme novas ferramentas de IA forem utilizadas no desenvolvimento.

## Projetos do curso

Veja o [repositório agregador da capacitação](https://github.com/intelligent-life-paradox/trends-IA-projetos-).
