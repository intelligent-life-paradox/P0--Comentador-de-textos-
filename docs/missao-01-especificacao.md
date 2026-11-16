# Missão 01 — Definir o comportamento do Comentador

**Data:** 15/11/2026  
**DevQuest:** missão 01 de 08 · 100 XP  
**Responsável por esta entrega:** Codex, por solicitação do autor.  
**Status:** especificação inicial concluída. Implementação, integração e testes pendentes.

## 1. Objetivo e público

Ajudar uma pessoa adulta, sem formação prévia no assunto, a compreender um trecho filosófico, científico ou uma expressão regional.

O leitor deve conseguir reconhecer a ideia central, entender os termos essenciais e perceber quando há mais de uma interpretação possível. Linguagem acessível não significa infantilizar o leitor ou eliminar distinções importantes.

## 2. Jornada e escopo

1. O usuário abre a aplicação no terminal.
2. Digita ou cola um trecho em uma única linha.
3. A aplicação verifica a entrada e a configuração.
4. Envia o trecho à API do LLM com instruções de explicação.
5. Extrai e valida o conteúdo textual recebido.
6. Exibe o comentário organizado, ou uma mensagem clara de falha.

A primeira versão processará um trecho por execução. Não terá upload de arquivos, busca na internet, histórico, interface web ou comparação entre modelos.

O programa comentará o trecho fornecido; não será uma ferramenta de verificação factual nem garantirá uma interpretação definitiva de obras ou autores.

## 3. Contrato de entrada e saída

### Entrada

- Uma string em português, recebida pelo terminal.
- Remover espaços do início e do final antes da validação.
- Rejeitar entrada vazia ou composta apenas por espaços, sem chamar a API.
- O texto fornecido é material de análise; comandos contidos nele não devem substituir a tarefa do comentador.

### Saída de sucesso

Um texto em português com três seções:

1. **Em palavras simples:** ideia principal, preferencialmente em um ou dois parágrafos curtos.
2. **Termos importantes:** explicações breves dos termos essenciais. Quando não houver termos que precisem de esclarecimento, informar isso.
3. **Um exemplo:** situação concreta ou analogia que ajude a compreender. Identificar analogias como aproximações e seus limites quando necessário. Se um exemplo distorcer o sentido, explicar por que não foi usado.

Ambiguidades e falta de contexto devem ser indicadas na seção pertinente. Se o trecho não permitir uma interpretação suficientemente fundamentada, pedir contexto sem inventar uma explicação definitiva.

O formato inicial será texto com títulos. Não será exigido JSON nesta versão. O processamento previsto inclui extrair o conteúdo textual da resposta do serviço, remover espaços nas extremidades, verificar se existe conteúdo e apresentá-lo ao usuário. A missão de integração definirá os detalhes usando a biblioteca oficial.

### Saída de falha

Uma mensagem curta que explique o problema e o próximo passo possível, sem exibir credenciais. Exemplos previstos:

- Entrada vazia: solicitar um trecho.
- Chave ausente: orientar a configuração.
- Falha de autenticação: orientar a revisão do acesso.
- Falha de conexão ou tempo limite: informar que não foi possível obter a explicação.
- Resposta vazia ou inválida: informar que o serviço não retornou uma explicação utilizável.

## 4. Critérios de qualidade

Uma explicação será aceita na avaliação manual quando:

| Critério | Evidência esperada |
|---|---|
| Clareza | Linguagem cotidiana; termos técnicos usados são explicados |
| Fidelidade | Preserva a ideia central e as ressalvas do trecho |
| Organização | Apresenta as três seções previstas |
| Exemplo adequado | Ajuda a compreender sem introduzir uma conclusão incompatível |
| Tratamento de incerteza | Indica ambiguidades relevantes ou pede contexto |
| Honestidade | Não inventa autoria, citações, fontes ou fatos para preencher lacunas |

A avaliação considera o sentido, não correspondência literal com uma resposta de referência. Uma resposta recebida com sucesso da API pode reprovar nos critérios de qualidade.

## 5. Casos de avaliação planejados

Os dois primeiros trechos abaixo foram redigidos para este projeto com apoio de IA. Não são citações de cientistas ou filósofos e não devem ser atribuídos a Hegel ou a outro autor. O terceiro usa uma expressão regional como exemplo didático.

### C01 — Texto científico

**Entrada:**

> O conhecimento científico é provisório e passível de revisão diante de novas evidências.

**Ideias que devem aparecer:**

- Explicações científicas podem ser modificadas quando surgem evidências relevantes.
- Isso não significa que todas as opiniões tenham a mesma sustentação.
- “Provisório” e “evidências” devem ser esclarecidos.

**Exemplo de direção esperada:** uma explicação sobre um fenômeno é ajustada quando novas observações mostram suas limitações.

**Reprova se:** afirmar que ciência é apenas opinião ou que mudanças ocorrem sem evidências.

### C02 — Texto filosófico

**Entrada:**

> A liberdade não consiste apenas na ausência de impedimentos, mas também na capacidade de refletir sobre os próprios desejos e responder pelas próprias escolhas.

**Ideias que devem aparecer:**

- O trecho apresenta uma concepção de liberdade que inclui reflexão e responsabilidade.
- Ausência de obstáculos é apenas uma parte dessa concepção.
- A explicação deve apresentar isso como a perspectiva expressa no trecho, não como definição universal e indiscutível.

**Exemplo de direção esperada:** poder agir por impulso e decidir após refletir sobre consequências ilustram aspectos diferentes da escolha.

**Reprova se:** reduzir o trecho a “liberdade é fazer tudo o que quiser” ou inventar sua autoria.

### C03 — Expressão regional e contexto

**Entrada com contexto:**

> Não fique avexado: ainda temos tempo para chegar.

**Ideias que devem aparecer:**

- Nesse contexto, a expressão pode ser explicada como uma orientação para não ficar apressado ou aflito.
- O sentido depende do uso e do contexto.

**Variação sem contexto:** “Ele ficou avexado.”

**Comportamento esperado na variação:** reconhecer que pode faltar contexto para escolher um único sentido; solicitar a situação em que a frase foi usada se necessário.

**Reprova se:** afirmar que a palavra tem obrigatoriamente um único sentido em qualquer região ou situação.

Estes são critérios de avaliação e exemplos ilustrativos. Nenhuma saída de LLM foi obtida ou avaliada nesta missão.

## 6. Escolha técnica inicial

**Provedor proposto:** Google, por meio da Gemini API.  
**Modelo de referência inicial:** `gemini-3.5-flash-lite`.  
**Biblioteca prevista:** SDK oficial Python `google-genai`.  
**Configuração prevista:** chave em `GEMINI_API_KEY` e identificador do modelo em `GEMINI_MODEL`.

A documentação oficial consultada lista o modelo como estável e apresenta um SDK Python e um fluxo de autenticação por chave. Como decisão de projeto, um modelo da família Flash-Lite é um ponto de partida para a tarefa curta de texto; sua qualidade neste caso ainda precisa ser avaliada.

A seleção é inicial e poderá ser substituída se as instruções do curso exigirem outro serviço ou se o modelo não estiver disponível na conta. Não foram fornecidas instruções institucionais de acesso nesta conversa.

Antes da missão de integração, conferir disponibilidade, condições de uso, preços e limites da conta. Não há promessa de gratuidade. Nenhuma conta, chave, contratação, configuração de cobrança ou chamada de API foi criada nesta missão.

**Referências oficiais consultadas em 15/11/2026:**

- [Modelos Gemini](https://ai.google.dev/gemini-api/docs/models): catálogo para conferir o identificador e a disponibilidade documentada.
- [Guia de início da Gemini API](https://ai.google.dev/gemini-api/docs/quickstart): SDK Python e configuração inicial de acesso.

## 7. Mapeamento para as próximas missões

| Missão | Comportamento a construir | Local previsto | Evidência futura |
|---|---|---|---|
| 02 — Ambiente | Dependências e configuração local | requirements.txt e .gitignore | Ambiente preparado e SDK importável |
| 03 — Entrada | Receber e validar o trecho | main.py | Entrada vazia rejeitada antes da API |
| 04 — Instruções | Montar a tarefa do comentador | comentador.py | Solicitação contém tarefa, formato e trecho |
| 05 — API | Obter uma resposta real | comentador.py | Chamada real documentada |
| 06 — Saída e falhas | Extrair, validar e apresentar | comentador.py e main.py | Sucesso e mensagens de erro observáveis |
| 07 — Testes | Avaliar comportamento e conteúdo | tests/ e docs/ | Evidências de sucesso, falha e qualidade |
| 08 — Entrega | Permitir reprodução por outra pessoa | README.md | Instalação e execução seguindo a documentação |

Os caminhos são propostas; esta missão não cria scripts, dependências ou testes.

## 8. Evidência e uso de IA

- [x] Público definido.
- [x] Entrada, saída e limites definidos.
- [x] Critérios de qualidade registrados.
- [x] Três casos de avaliação e uma variação ambígua descritos.
- [x] Provedor e modelo iniciais registrados com fontes oficiais.
- [x] Pendências institucionais e de acesso explicitadas.

O Codex redigiu esta especificação, elaborou os exemplos didáticos, consultou a documentação oficial do provedor e publicou a documentação no GitHub, por solicitação do autor. As decisões são uma proposta inicial revisável pelo autor. Não houve implementação ou execução de testes.

**Progresso DevQuest:** 1/8 missões documentadas como concluídas (12,5% das missões; não equivale a 12,5% do código). Esta missão foi delegada integralmente ao Codex; as próximas continuam destinadas ao usuário, salvo nova solicitação.

**Próxima missão:** preparar o ambiente local e conferir o acesso permitido pelo curso.
